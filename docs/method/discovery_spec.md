# Discovery Spec — find_methodology / get_methodology

> **Status**: v0 spec — **design, MCP-ready not built**, 2026-06-05.
>
> **Purpose**: define the contract + matching algorithm for the discovery layer that turns *"a BizDev user searches a topic"* into *"the right skill is found and loaded,"* over the registry built from each package's taxonomy. Resolves `../status/capabilities.md` Open Decision #5(b) (top-N selection) and #5(c) (tie-break) and adopts an alias map for #5(a); **recommends** (does not resolve) #2 (location).
>
> **Companions**: `../architecture.md` §8 (where discovery sits), `resources/README.md` (the registry this indexes), `resources/weather_and_climate/el_nino_enso/SKILL.md` (the first skill).

## 1. v0 Stance

Discovery is **spec'd here, not built** (v0 = MCP-ready, not MCP-integrated). Today the human-readable registry (`resources/README.md`) **is** the index — a person or a Claude session reads it to pick a skill. This doc defines the **target tool contract** so a manual test can simulate it and a later build can implement it unchanged.

In v0 the methodology is **served via the InfraSure MCP**: `get_methodology` *returns* the SKILL.md-format body as tool output. `SKILL.md` is the **authoring/packaging format** — in this deployment the body is served as MCP output, **not** *installed* as a native Claude Agent Skill that the model auto-selects. In this served model `find_methodology` **is** the authoritative discovery path, because nothing else is auto-selecting. (Installing the packages as native Agent Skills is an alternative deployment — then the model auto-selects by `description` and `find_methodology` is only a catalog aid, not the loader; see `architecture.md` §5 / §7 / §13 #1.)

## 2. Where It Sits

```text
BizDev query ──▶ find_methodology(query|domain|family|actor) ──▶ ranked SkillIndexRecord[]
                                                                      │ session picks a slug
                                                                      ▼
                                  get_methodology(slug) ──▶ skill payload (SKILL.md body + bundled refs + version)
                                                                      │
                                                                      ▼  loaded into the session = the "agent"
                                                          runs the method vs MCP data tools + NOAA
```

## 3. The Registry Index

Built at publish from every package — one record per skill:

```text
SkillIndexRecord {
  slug:               string    // = resource.yml.identity.slug — the canonical key (folder == slug)
  name:               string    // = SKILL.md frontmatter `name` (kebab, e.g. el-nino-enso)
  title:              string    // = resource.yml.identity.title
  domain:             string    // taxonomy.domain   (enum)
  family:             string    // taxonomy.family   (enum, analysis_families.md)
  drivers:            string[]   // taxonomy.drivers  (free-form leaf tags)
  actors:             string[]   // taxonomy.actors
  description:        string     // = SKILL.md frontmatter `description`  ← PRIMARY match text (what + when)
  confidence_default: string     // derived from resource.yml.confidence_rules (ENSO → "low")
  version:            string     // resource.yml.identity.version  (echoed by get_methodology)
  status:             string     // = resource.yml.identity.status: draft | active | deprecated
                                  //   only "active" (eval-passed) is indexed by default (`../architecture.md` §7 gate, `../status/capabilities.md` Open Decision #7)
}
```

**Source-of-truth note**: the matchable `description` comes from **`SKILL.md`** (it is literally the Claude-Skill discovery field — *what it does and when to use it*); `taxonomy` + `identity` come from `resource.yml`. The publish step asserts `folder == slug` and stamps `version` (`../status/capabilities.md` Open Decision #4/#6).

**Publish-eligibility**: the publish step indexes a skill **only after its eval suite passes** (`../architecture.md` §7). `status` is copied from `resource.yml.identity.status`; a `draft` / eval-failing skill is **not** added to the served index by default (it can still be fetched with `include_deprecated=true`). This is the discovery analog of the §9 gate — discovery must not surface a method that never passed its gate.

**Description cap**: `description` is the platform-capped (≤1024-char) model-facing field, so it is *intentionally* the match text; the publish step should lint a warning when a description nears the cap (and may later also match `title` + `drivers`).

**Index lifecycle**: the index — the `SkillIndexRecord` set **plus** the §7 alias map — is one artifact, **fully rebuilt** by every publish from a full scan of `resources/` (not incrementally patched). The scan covers **package folders only**: leading-underscore folders (`_principles` · `_style` · `_craft` · `_reference`) are shared layers, not packages — no `resource.yml`, no slug, never a `SkillIndexRecord`; the `folder == slug` assertion applies to packages only (`resources/README.md`, the underscore rule). A removed or deprecated package drops/flags its record on the next publish (the §6 rows consume the flag). The index carries a build timestamp + content hash, echoed in `find_methodology`'s `query_echo`, so a running session can confirm which index vintage it queried. This extends `../status/capabilities.md` Open Decision #4 atomicity from per-resource to the whole-catalog index.

## 4. `find_methodology` — Contract

```text
find_methodology({
  query?:  string     // free text, e.g. "el nino solar exposure"
  domain?: string     // hard filter (enum)
  family?: string     // hard filter (enum)
  actor?:  string     // hard filter (enum)
  limit?:  number = 5
  include_deprecated?: boolean = false   // default indexes only status=active; true also surfaces draft/deprecated
})
```

At least one of `query | domain | family | actor` is required.

```text
→ {
    matches: [ { slug, name, title, domain, family, drivers, actors, description,
                 confidence_default, score, match_reasons[] } ],   // ranked desc, length ≤ limit
    total:   number,
    query_echo: {...},
    note?:   string    // e.g. "0 matches — broaden; nearest domains: hazard, market"
  }
```

It returns **ranked candidates — it does not auto-load**. The session (via `get_methodology`) loads the chosen slug. This resolves `../status/capabilities.md` Open Decision #5(b) toward **top-N, never silent auto-bind**.

**v0 scope**: single-value hard filters + top-N retrieval only. Multi-driver queries and paging beyond `limit` are deliberately deferred to the ~15–20-skill threshold (§11) — not an oversight.

## 5. Matching & Ranking

```text
1. HARD FILTERS  domain/family/actor (if given) restrict the candidate set by exact enum match.
                 (draft/deprecated excluded unless include_deprecated=true — §3 publish-eligibility.)
2. QUERY SCORE   (when query present) tokenize, alias-normalize (§7), then per candidate:
      driver match (incl. alias)        weight 3  (per matched driver)
      family / domain term in query     weight 2
      actor term in query               weight 1.5
      text hit on description / title   weight 1  (term-frequency-ish)
   raw   = weighted sum.
   score = raw / DENOM, where DENOM = the max achievable weight for the signals PRESENT IN THE QUERY,
           so score is 0–1 and comparable across candidates and queries (a candidate hitting every
           query signal = 1.0).
3. FLOOR         drop candidates with score < FLOOR (v0 default 0.15, absolute; tuned by the discovery eval, §11).
4. TIE-BREAK     when scores are equal within EPS, compare a per-signal tuple lexicographically:
      (exact_driver_hits, alias_driver_hits, family_hit, actor_hit, desc_hits, title_hits)
      where an "exact driver" is a literal driver token present in the query BEFORE alias expansion,
      vs an alias-matched driver (the §7-collapsed form).   EPS/FLOOR/MARGIN are named, eval-tuned.
      (resolves `../status/capabilities.md` Open Decision #5c)
```

## 6. Edge Cases

| Case | Behavior |
|---|---|
| **zero match** | `matches: []` + `note`: broaden suggestion + nearest domains (by partial tag overlap) |
| **exactly one above FLOOR** | return it as top-1 — the session still confirms; **no blind auto-run** |
| **multiple** | ranked top-N (≤ `limit`); if the top-2 scores are within `MARGIN` (a named tunable), `note: "ambiguous — N candidates"`, where N = count of candidates within `MARGIN` of the top |
| **fragmented driver** (e.g. `el_nino` vs `enso`) | the alias map (§7) collapses synonyms **before** scoring |
| **draft / not-eval-passed skill** | excluded by default; publish refuses to index it until its eval suite passes (§3, `../architecture.md` §7); surfaced only with `include_deprecated=true` |
| **deprecated skill** | excluded by default; surfaced only with `include_deprecated=true` |

## 7. Synonym / Alias Map (resolves `../status/capabilities.md` Open Decision #5a, pragmatically)

`drivers` are free-form, which fragments across authors. A **registry-level alias map** normalizes query terms → canonical drivers before scoring:

```yaml
aliases:
  enso:       ["el nino", "el niño", "la nina", "la niña", "oni", "southern oscillation"]
  irradiance: ["solar resource", "insolation", "cloud cover", "sunlight"]
  # … extended as drivers are added
```

It lives in the registry as **`resources/aliases.yml`**, loaded/merged at publish into the index. **Publish asserts** every alias's canonical key is a real `drivers` value present somewhere in the registry — a dangling alias **fails the publish loud**, not silently at query time (mirroring the `folder == slug` assertion in §3 / `../status/capabilities.md` Open Decision #6). The deeper "full controlled vocabulary vs. fuzzy embedding match" choice stays open (`../status/capabilities.md` Open Decision #5a); this spec adopts the **alias map** as the pragmatic middle for the current scale.

## 8. `get_methodology` — Contract

```text
get_methodology({ slug, file? })   // slug = resource.yml.identity.slug — the canonical key (`../architecture.md` §6)
→ {
    slug, name, title, version,    // version echoed for publish coherence (`../status/capabilities.md` Open Decision #4)
    skill_md:  string,             // the SKILL.md body — the loadable method (returned when `file` omitted)
    bundled:   [ { path, role } ], // MANIFEST (not content); each path is RELATIVE to the skill folder <slug>/
    taxonomy:  {...},
    confidence_default
  }
```

`bundled` is a **manifest, not content** (progressive disclosure). Fetch a bundled file on demand with `get_methodology({ slug, file: "<path>" })` → `{ content: string }`. The MCP surface therefore stays two tools (`find_methodology` + `get_methodology`).

Unknown slug → `{ error: "not_found" }`. Deprecated slug → returned with a `deprecated: true` flag.

## 9. Where It Lives (recommendation for `../status/capabilities.md` Open Decision #2)

**Recommend an InfraSure MCP tool** — same surface as the data tools, so BizDev needs one connection. The contract is **identical** whether it is an MCP tool or a separate catalog service, so the location is an *implementation* choice, not a *contract* choice. Discovery and data tools share the "expandable floor."

## 10. Worked Example

```text
query: "how does el nino affect our california solar this winter"

  alias map   "el nino"  → driver `enso`
  text hits   "solar" (title/desc), "california" (scope hint)
  family      none given → unfiltered ("affect/exposure" weakly implies exposure)

→ find_methodology returns (today the catalog holds 5 skills — el_nino_enso · hail_solar ·
  hurricane_high_wind_wind · extreme_heat_derate · offtaker_concentration; the ENSO match ranks top here):
   matches: [ {
     slug: "el_nino_enso", name: "el-nino-enso", title: "El Niño / ENSO Exposure For Renewable Assets",
     domain: "weather_and_climate", family: "exposure", drivers: ["enso","irradiance"],
     actors: ["owner_operator","investor","lender","offtaker"],
     score: 1.0, match_reasons: ["driver:enso (via 'el nino') = 3", "text:solar = 1"]
   } ]                          // raw 4 / DENOM 4 (the driver+text signals present in the query) = 1.0

   NOTE: this skill is currently identity.status="draft" — until its eval suite passes it is indexed
   only under include_deprecated=true; shown here as the post-promotion (active) shape.

→ get_methodology("el_nino_enso") returns:
   { skill_md: <ENSO SKILL.md body>,
     bundled: [knowledge.md, examples/applied_insight_001.md, data_requirements.md],  // manifest; fetch via file=
     version: "0.0.1-draft", confidence_default: "low" }

→ the session loads it and runs the ENSO method against the MCP data tools + a live NOAA pull.
```

## 11. Carried Open Questions

- **`../status/capabilities.md` Open Decision #2** (where discovery lives) — recommended MCP tool; contract is location-agnostic.
- **`../status/capabilities.md` Open Decision #5a** (controlled vocabulary vs. fuzzy) — this spec adopts an alias map as the pragmatic middle; revisit a full controlled vocabulary / embedding match at ~15–20 skills.
- **Discovery eval** — discovery needs its own eval ("does query X return skill Y in the top-K?"); folds into the eval harness (`../status/capabilities.md`).

---

**See also**: `../architecture.md` §8, `resources/README.md`, `resources/weather_and_climate/el_nino_enso/SKILL.md`.
