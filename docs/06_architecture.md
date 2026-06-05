# 06 - Architecture

> **Status**: v0 target architecture, 2026-06-05.
>
> **Audience**: seniors deciding whether the design is sound; contributors building toward it; BizDev understanding how they will consume it.
>
> **In one line**: author **methodology skills** in this repo → **publish** them into an MCP-discoverable **skill catalog** → a BizDev user in Claude **searches a topic, loads the matching skill, and grounds it** with the InfraSure data tools + external sources to produce a **validated** report.

## 1. The Thesis

InfraSure already has a **data** surface (MCP tools over the substrate). What it lacks is a **reasoning** surface: packaged, discoverable methodology that tells a model how to reason about a topic, what to claim, and what to refuse. This architecture adds that second surface and connects the two.

```text
THE EXPANDABLE FLOOR — the MCP/served surface grows on two axes, not one:
   axis 1  DATA tools        search_plants · get_plant · aggregate · find_by_extracted_fact · …   (live today)
   axis 2  METHODOLOGY skills  el_nino_enso · (drought · wildfire · curtailment · offtaker-risk …)  (this layer)
```

A vanilla LLM can replicate neither curated axis. Serving both from one place — *here is the data, and here is how an InfraSure analyst reasons over it* — is the moat.

## 2. Core Principle: Repo Is Source, Not the Served Thing

You do **not** bolt the raw `weather_and_climate/` folder onto MCP. The repo is **source of truth**; a **publish step** compiles each resource package into a served unit. Two consequences:

```text
unit of delivery   = ONE SKILL  (el_nino_enso)        ← what a session loads (token-economical)
unit of discovery  = the TAXONOMY (domain·family·drivers·actors) ← how a session finds the right skill
domain folder      = source organization + discovery metadata, NOT a serving boundary
```

Loading one skill (not a whole domain) keeps context lean; skills **compose** at runtime (a "weather & climate analyst" session can load several). Persona = a runtime composition of skills, never a stored folder.

## 3. The Four Layers

```text
┌─ LAYER 0 · SOURCE OF TRUTH — the repo (insights_lab/, authored + versioned) ───────────────────┐
│  resources/<domain>/<skill>/      e.g.  weather_and_climate/el_nino_enso/                       │
│    ├ resource.yml        SPEC  → taxonomy(domain·family·drivers·actors) · confidence_rules ·    │
│    │                              blocked_claims      (drives discovery + gates + the prompt)   │
│    ├ prompt_projection.md METHOD → the instruction body the skill injects                       │
│    ├ knowledge.md         MECHANISM → cited domain reasoning                                     │
│    ├ resource.md          human canon · data_requirements.md  retrieval plan                    │
│    └ examples/ + test_runs/  EVAL SUITE → golden output + pass/fail cases                        │
└───────────────────────────────────────────┬───────────────────────────────────────────────────┘
                                   build / publish step
                                             ▼
┌─ LAYER 1 · SERVED SURFACE — what BizDev's Claude connects to ───────────────────────────────────┐
│  ┌ InfraSure MCP server ──────────────────────┐      ┌ Skill catalog ───────────────────────────┐│
│  │ DATA tools  search_plants · get_plant ·     │      │ one skill per resource package            ││
│  │             aggregate · plants_by_owner ·   │      │   "ENSO Exposure" (weather_and_climate)   ││
│  │             find_by_extracted_fact · news   │◀───▶ │   = prompt_projection + knowledge.md       ││
│  │ DISCOVERY   find_methodology(query|domain|  │      │   + eval examples                         ││
│  │             family) · get_methodology(slug) │      │ matched via resource.yml.taxonomy tags    ││
│  └─────────────────────────────────────────────┘      └───────────────────────────────────────────┘│
└───────────────────────────────────────────┬───────────────────────────────────────────────────┘
                                             ▼
┌─ LAYER 2 · RUNTIME — a BizDev analyst session (Claude Desktop / web / Code) ────────────────────┐
│  "ENSO exposure for our California solar owners this winter?"                                    │
│    1 discover  find_methodology("enso solar exposure") → ENSO skill                              │
│    2 load      inject prompt_projection + knowledge.md                                           │
│    3 ground    external NOAA pull (state)  +  InfraSure DATA tools (real assets)                 │
│    4 assemble  applied-insight contract (claim·scope·refs·confidence·caveats·actor)              │
│    5 gate      resource.yml confidence_rules + blocked_claims enforced (no $/MWh, cap LOW)       │
└───────────────────────────────────────────┬───────────────────────────────────────────────────┘
                                  validated insight object
                                             ▼
┌─ LAYER 3 · OUTPUT — the scope file's activation split ──────────────────────────────────────────┐
│   report · platform card / Ask answer    ── | ──    account note · informative email            │
│                              (a rendering of a VALIDATED insight — never before it passes)       │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Layer notes

- **Layer 0 — Source.** The repo. Authored, reviewed, version-controlled. The `resource.yml` is the spec that downstream everything reads.
- **Layer 1 — Served.** Two cooperating surfaces: the **MCP data tools** (already live) and a **skill catalog** (one skill per package). A small **discovery** capability (an MCP tool or a skill-catalog search) matches a user's topic to a skill via the taxonomy.
- **Layer 2 — Runtime.** A Claude session (the "agent") discovers → loads → grounds → assembles → gates. Grounding uses *both* the external state (NOAA) and the InfraSure substrate.
- **Layer 3 — Output.** Only a **validated** insight is rendered — as a report/card for the platform or an account note/email for BizDev. Activation never precedes validation.

## 4. Request Lifecycle

```mermaid
sequenceDiagram
    participant BD as BizDev user
    participant CL as Claude session (the "agent")
    participant CAT as Skill catalog / MCP discovery
    participant MCP as InfraSure MCP (data tools)
    participant EXT as NOAA CPC (external)

    BD->>CL: "ENSO exposure for our CA solar owners this winter?"
    CL->>CAT: find_methodology("enso solar exposure")
    CAT-->>CL: ENSO Exposure skill (weather_and_climate)
    CL->>CL: load prompt_projection + knowledge.md
    CL->>EXT: pull ENSO state (El Nino Watch, DJF probability)
    EXT-->>CL: forecast + as_of date
    CL->>MCP: search_plants(state=CA, solar, min 50MW) / get_plant / aggregate
    MCP-->>CL: real assets, CF, owners, offtakers (as_of)
    CL->>CL: assemble insight + enforce confidence / blocked-claim gates
    CL-->>BD: validated insight -> report / card / account note
```

## 5. Skill vs Agent (terminology)

| Term | What it is | In our stack |
|---|---|---|
| **Skill** | a packaged capability (instruction + knowledge + procedure + eval), loaded on demand | one resource package; maps ~1:1 to a **Claude Agent Skill** (`SKILL.md` + bundled files) |
| **Agent** | a running session that has loaded a skill + the tools | the BizDev Claude session behaving as an "ENSO analyst" |
| **Tool** | a single callable function (data or discovery) | the MCP data tools + `find_methodology` |

**Skill = the noun we build and store. Agent = the verb, a session running the skill.** Name the packages **"InfraSure Insight Skills."**

## 6. Artifact Roles (which file feeds what)

```text
SERVED to the model (the skill payload)          AUTHORED for humans / validation
  resource.yml       spec · taxonomy · gates       resource.md          human canon
  prompt_projection  the method instruction body    data_requirements    retrieval plan / gaps
  knowledge.md       cited mechanism                 examples/+test_runs  EVAL SUITE (golden + pass/fail)
```

`resource.yml` is load-bearing — one file drives **three** things: **discovery** (taxonomy/tags), **the served prompt** (which sections to inject), and **the validation gates** (`confidence_rules` + `blocked_claims`).

## 7. Delivery Model (recommended hybrid)

```text
METHODOLOGY (how to reason)  → Claude Skills           (alt: MCP Prompts)
DATA        (what is true)    → MCP tools               (live today)
DISCOVERY   (find the skill)  → MCP tool over the registry (resource.yml.taxonomy — mirrored in resources/README.md)
```

Mapping to platform primitives:

| Need | Mechanism | Notes |
|---|---|---|
| Reason like an analyst | **Claude Agent Skill** per package | description-matched + progressively loaded; `prompt_projection` ≈ the skill body, `knowledge.md` a bundled file |
| Retrieve grounded data | **MCP Tools** | already implemented |
| Find the right skill | **MCP Tool** `find_methodology` (or skill-catalog search) | indexes the taxonomy we built |
| Optional: serve method text | **MCP Prompts / Resources** | viable alternative to Skills if delivery must be MCP-only |

Recommendation: **Skills for method + MCP for data + an MCP discovery tool.** It matches the BizDev mental model ("search a topic → get a skill") and reuses the registry/taxonomy as the index.

## 8. Discovery In Detail

```text
find_methodology(query | domain | family | actor)
   → ranks skills by taxonomy match (resource.yml.taxonomy: domain · family · drivers · actors)
   → returns {slug, title, domain, family, summary, confidence_default}
get_methodology(slug)
   → returns the skill payload (prompt_projection + knowledge.md + example)

slug = resource.yml.identity.slug — the single get_methodology resolution key.
       The source folder name may differ and is NEVER the key; the publish step MUST
       assert folder name == identity.slug. (Today they diverge: folder el_nino_enso vs
       slug el_nino_enso_exposure — reconcile before publish; see Open Decision 6.)
```

Example: `find_methodology("el nino solar exposure")` → returns the **ENSO Exposure** skill (slug `el_nino_enso_exposure`; domain `weather_and_climate`; family `exposure`; drivers `enso, irradiance`). This is why the taxonomy exists — it is the discovery index, not decoration.

`find_methodology` is the **single authoritative discovery path**: when methodology is delivered as a Claude Agent Skill, the skill is loaded via the `find_methodology` / `get_methodology` result — not by relying on (or racing) the client's native description-matching. Where that discovery logic *lives* is Open Decision 2.

## 9. Validation Gate

The **applied-insight thin contract** + `resource.yml` rules are the quality firewall before anything renders:

```text
confidence_rules   → cap confidence at the weakest input (ENSO default = LOW)
blocked_claims     → refuse exact LMP / plant-level forecasts / pre-validation outreach
examples/+test_runs → the EVAL SUITE: a skill must reproduce its golden output + pass its cases before publish
```

In production these become *enforced* gates and a *trace* attached to each insight object (the scope file's in-house track).

**Input-availability gate** (distinct from `blocked_claims`, which gate claim *type*): empty asset scope for the region ⇒ **BLOCKED** (scope unresolved); a failed/stale external (NOAA) pull ⇒ **BLOCKED** (state missing/stale); partial *optional* inputs ⇒ cap at **LOW**. These are the `resource.yml.confidence_rules.blocked` conditions applied at the tool-result layer. (Enforcing a freshness *window* on the NOAA pull is Open Decision 3.)

**v0 caveat — the gate is self-policing.** In v0 it is a *prompt-level convention* enforced by the **same** session that drafts the insight: the session that produced a blocked `$/MWh` figure is the one asked to refuse emitting it, with no independent validator. This is a known v0 weakness; production moves enforcement out of the drafting session.

## 10. Mapping To The Scope File

| Scope-file concept | Architecture home |
|---|---|
| validated insight object | Layer 2 output (the applied-insight contract) |
| in-house architecture track | the publish step + discovery + enforced gates + trace capture (Layer 0→1) |
| activation / outreach track | Layer 3 rendering (report / card / account note / email) |
| "outreach is a rendering, not the source" | the validation gate sits *between* insight and activation |

## 11. Build Status & Roadmap

| Capability | Status | Next |
|---|---|---|
| Data tools (MCP) | ✅ live | wire the `iso` filter (logged gap) / add region resolution |
| Source repo + taxonomy registry | ✅ built | — |
| One validated skill (ENSO) | ✅ test 001 PASS | — |
| Skill **format** (`SKILL.md` from a package) | ☐ design | author the ENSO skill bundle |
| Discovery tool (`find_methodology`) | ☐ design | spec it over the registry |
| Publish step (repo → served) | ☐ design | minimal: a build script that emits skill bundles + a registry index |
| Eval harness (examples/test_runs → CI) | ☐ design | turn golden outputs into pass/fail checks |

## 12. Boundaries & Non-Goals (v0)

- No autonomous outreach — activation always follows a passed validation gate.
- No raw-folder serving — only the published skill + registry are served.
- No production agent/orchestrator yet — v0 stays manual (MCP-ready, not MCP-integrated).
- No quantitative forecasts where the method only supports direction.
- No auth/authz layer in v0 — assumes a single trusted internal BizDev Claude session against the existing MCP; per-user MCP credentials, skill-catalog gating, and external-access scoping are post-v0.

## 13. Open Decisions

1. **Delivery format**: Claude Agent Skills vs MCP Prompts vs both (recommend Skills + MCP data + MCP discovery).
2. **Where discovery lives**: an InfraSure MCP tool vs a separate catalog service.
3. **State freshness enforcement**: how a skill guarantees the external state (NOAA) was pulled within an acceptable window before it renders.
4. **Skill versioning & coherence**: how `resource.yml.version` + eval suite gate a re-publish — *and* how a single publish stamps every derived artifact (skill bundle, registry index entry, enforced gate set) with that version, so a session can confirm the loaded prompt, the discovery entry, and the gates all came from one `resource.yml`. (Make publish atomic per resource; have `get_methodology` and the insight trace echo the version.)
5. **Discovery index at scale**: the taxonomy is a flat tag rank with one skill today; revisit before ~15–20 skills. (a) a controlled `drivers` vocabulary + synonym/alias map (e.g. `enso ← el_nino, la_nina, oni`) vs. fuzzy query matching — `drivers` is currently free-form, which fragments across authors; (b) auto-bind the single top match (as §4/§8 show) vs. return ranked top-N for the session to choose; (c) tie-break order (exact-driver > family > actor) + zero-match behavior.
6. **Canonical slug**: reconcile `resource.yml.identity.slug` vs the folder name (today `el_nino_enso_exposure` vs `el_nino_enso`), pick one canonical value, align all surfaces (folder, registry README, package files, this doc), and assert `folder == identity.slug` at publish.
7. **Catalog maintainership & deprecation**: who owns the served catalog and approves a publish, and how a skill is marked deprecated/unpublished so it stops surfacing in `find_methodology`.

---

**See also**: `00_project_brief.md` (why), `01_scope_v0.md` (the v0 deliverable + after-V0 split), `resources/README.md` (the registry this discovery indexes), `resources/weather_and_climate/el_nino_enso/` (the first validated skill).
