# 11 - Use Cases & Validation

> **Status**: product use-case canon, opened 2026-06-08.
>
> **Purpose**: define the use-case shape of the **combined agent (Pillar 3)** in detail — the two buckets, the audience layer, and how the buckets connect — plus the **validation / proof-of-value** method that earns Pillar 1 (MCP) and Pillar 2 (Reference).
>
> **Where this sits**: the whole-project *panorama* (the four summary plots) lives in `01_scope_v0.md`; this doc is the **detail behind it**. The pillar overview is `00_project_brief.md`. This doc deliberately does not re-draw the panorama — it goes deeper.

## The Three Pillars (one line)

```text
PILLAR 1 · MCP            PILLAR 2 · REFERENCE / KB        PILLAR 3 · COMBINED AGENT
data tools (built)        methodology + knowledge (built)  1 + 2 + agentic architecture (open)
   └──── now: REFINE + VALIDATE ────┘                       └── now: DEFINE THE USE CASE (this doc)
```

Pillars 1 and 2 exist and are in **refine + validate**. Pillar 3 is the open work, and its first task — the one that was under-specified — is to define the use case in detail. That is the rest of this doc.

## The Two Buckets (Pillar 3)

Two directions of the same engine. They are not separate products; they are opposite entry points that feed each other (see Connection).

| Axis | **Bucket 1 · BOTTOM-UP** | **Bucket 2 · TOP-DOWN** |
|---|---|---|
| Anchor | a specific **site / portfolio** | a **phenomenon** / latest news / industry signal |
| Direction | asset ──► phenomenon effect | phenomenon ──► affected assets / regions |
| The question | "how does *[phenomenon]* affect **this** site / portfolio?" | "this signal matters — **which** assets / regions does it hit?" |
| Core output | an exposure / risk read for that asset or portfolio | the affected set, rendered as an insight |
| Family it draws on (`docs/02`) | Exposure (asset-anchored) | Exposure + Event-translation (phenomenon-anchored) |
| MCP pattern | `get_plant` / `plants_by_owner` (drill) | `aggregate` / `search_*` + `find_by_extracted_fact` (fan-out) |
| ENSO example | "El Niño's effect on Clearway's CA desert solar book" | "El Niño Watch → which CA ≥50 MW solar is exposed → post" |

## The Audience Layer (cross-cuts both buckets)

Each bucket is produced **internal-team first**, then a **customer / public** subset is derived from it:

```text
                     BUCKET 1 · bottom-up              BUCKET 2 · top-down
   INTERNAL (first)  team exposure / risk read         internal scan of what's affected
   CUSTOMER/PUBLIC   account brief for a named owner    blog / LinkedIn insight post
                     (a subset of the internal read)    (the outward-facing content)
```

**Rule (`08` P2):** the internal read is the source of truth; the customer/public artifact is a *rendering* of it. Nothing is published externally that has not passed the gate internally first.

**Refinement (2026-06-12, the layered-reference plan):** the customer/public level splits into **`client`** (a named account — briefs, curated email) and **`public`** (blog, post). The operational form of this whole grid is the output-contract matrix `direction × audience(internal | client | public) × format(blog | brief | email | post)` in `resources/_style/output_contracts.md`. Two instruments, not one: the **rubric** (`resources/_principles/rubric.md`) scores any rendered artifact's quality; the **with/without method** below proves the moat — quality vs. reachability, neither replaces the other.

## The Connection — one cycle, not two silos

```text
   BUCKET 2 (top-down)  ─►  "in this region, these specific assets are exposed"
                        ─►  each surfaced asset becomes a BUCKET 1 (bottom-up) drill
                        ─►  the per-asset reads aggregate back up into the next top-down view

       phenomenon ─► affected set ─► per-asset exposure ─┐
            ▲                                            │
            └──────────────── feeds the next ────────────┘
```

So Bucket 2 is also a **discovery mechanism for Bucket 1**: a top-down scan is how you find which single sites/regions are worth a deep bottom-up run.

## Validation — the proof-of-value method (Pillars 1 & 2)

The question that *earns* the tools: **does the use case get satisfied by a vanilla cloud LLM + web, WITHOUT our MCP / reference?**

```text
   a DEFINED use case ──┬──► vanilla cloud LLM + web         → satisfies it?     → tool adds NO value
                        └──► + InfraSure MCP / reference      → only this works?  → MOAT PROVEN
```

Run it per pillar, each against a use case chosen to expose that pillar's value:

| Pillar | Use case that tests it | Why vanilla fails (→ the tool earns its keep) |
|---|---|---|
| **MCP** | "rank CA ≥50 MW solar owners by desert-zone exposure" | a plain LLM can't pull + aggregate 15K plants; no entity IDs, no `as_of` |
| **Reference** | "directional ENSO exposure, properly caveated, no overclaim" | a plain LLM over-claims — Medium not LOW, magnitude leakage, weak sourcing |

The output of validation is a **with / without comparison** artifact (the Thursday-deliverable shape). The sharp framing: validation isn't "is the output good," it's "is the output *unreachable without us*." **Caveat:** define the use case *before* the A/B, or "satisfied" can't be judged.

## Reconciliation With The Testing Buckets

The collaboration thread lists **three prompting buckets**; this doc defines **two use-case buckets**. Both are right — different levels:

```text
USE-CASE buckets (2)          prompting buckets (the meet thread, 3)
Bucket 1 · bottom-up    =     #1 single-user query  (asset → phenomenon)
Bucket 2 · top-down     =     #2 internal vlog       (phenomenon → asset/region)
                              #3 precise/structured  = a TESTING LENS, not a 3rd use case
                                 (#2 vs #3 reveals whether the prompt engineering holds)
```

## V0 Is One Slice Of This Map

V0 deliberately picks a **subset**:

```text
   V0  =  Bucket 1 (bottom-up)  ·  INTERNAL-team audience  ·  one resource (ENSO)
          ·  one region / one asset class
   later =  Bucket 2 (top-down) · customer/public renderings · multi-resource
```

**Reconciliation (2026-06-12):** Test Run 001 actually ran **top-down** by this doc's own definitions — a phenomenon → fleet scan (El Niño → CA ≥50 MW solar), not an asset-anchored drill. The V0 slice label was wrong on direction; the record stands corrected here rather than rewritten. The genuinely missing slice is **bottom-up**, completed by the layered-reference plan's Phase 5; the top-down contract cells are live first (`resources/_style/output_contracts.md`).

The full V0 cut and its boundary live in `01_scope_v0.md` (which also carries the four-plot panorama). The "later" line above is now governed by **`docs/plans/2026-06-11_layered_reference_v1.md`**, which deliberately ships the top-down + client/public *contracts* ahead of multi-resource.

---

**See also**: `00_project_brief.md` (the 3-pillar overview), `01_scope_v0.md` (the panorama + the V0 slice), `02_analysis_catalog.md` (the 7 families — orthogonal to the buckets: a family can run bottom-up *or* top-down), `06_architecture.md` (the runtime loop + the content engine that renders Bucket outputs), `08_design_principles.md` P2 (content downstream of a validated insight).
