# Use Cases & Scope — Who It's For, and the V0 Slice

> **Status**: use-case + scope canon, 2026-06-13 (merges the old `11_use_cases` + the canon half of `01_scope_v0`; the V0 status ladder moved to `status/capabilities.md`).
>
> **Purpose**: define the use-case shape of the combined agent (Pillar 3) — the two buckets, the audience layer, how they connect — and the exact V0 slice + scope boundary. The 3-pillar overview is in `architecture.md` §1; this doc owns the Pillar-3 detail and the scope contract.

## The Two Buckets (Pillar 3)

Two directions of the same engine. Not separate products; opposite entry points that feed each other (see Connection).

| Axis | **Bucket 1 · BOTTOM-UP** | **Bucket 2 · TOP-DOWN** |
|---|---|---|
| Anchor | a specific **site / portfolio** | a **phenomenon** / latest news / industry signal |
| Direction | asset ──► phenomenon effect | phenomenon ──► affected assets / regions |
| The question | "how does *[phenomenon]* affect **this** site / portfolio?" | "this signal matters — **which** assets / regions does it hit?" |
| Core output | an exposure / risk read for that asset or portfolio | the affected set, rendered as an insight |
| Family it draws on (`method/analysis_families.md`) | Exposure (asset-anchored) | Exposure + Event-translation (phenomenon-anchored) |
| MCP pattern | `get_plant` / `plants_by_owner` (drill) | `aggregate` / `search_*` + `find_by_extracted_fact` (fan-out) |
| ENSO example | "El Niño's effect on Clearway's CA desert solar book" | "El Niño Watch → which CA ≥50 MW solar is exposed → email" |

## The Audience Layer (cross-cuts both buckets)

Each bucket is produced **internal-team first**, then a **customer / public** subset is derived from it:

```text
                     BUCKET 1 · bottom-up              BUCKET 2 · top-down
   INTERNAL (first)  team exposure / risk read         internal scan of what's affected
   CLIENT (named)    a REPORT (targeted) → EMAIL        a REPORT (targeted) → EMAIL
   PUBLIC            (rarely — client-first)            a BLOG (generic, public)
```

(Output types: **blog** = top-down/generic/public · **report** = a blog scoped to a portfolio/client/region · **email** = the condensed subset of either — see `resources/_style/output_contracts.md`.)

**Rule (`principles.md` P2):** the internal read is the source of truth; the customer/public artifact is a *rendering* of it. Nothing is published externally that has not passed the gate internally first.

**Outputs and build order.** The three outputs are **blog · report · email**: a **blog** is top-down/generic, a **report** is the same format scoped to a specific portfolio/client/region/purpose (blog and report overlap in nature), and an **email** is a condensed subset of either. **Build order ≠ delivery order**: we build the **rich pair (blog / report) first** — they create the richest feedback loop, where you can see whether the insight is deep and well-grounded — and **email last**, as the distillation of a proven piece. *Delivery* sequencing (which output ships when, to whom) is a separate business question, not settled here; do not conflate it with how we build. The output model is owned by `resources/_style/output_contracts.md` — this doc points, it does not re-enumerate.

> Two judging instruments, not one: the **rubric** (`resources/_principles/rubric.md`) scores any rendered artifact's quality; the **with/without method** below proves the moat.

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

| Pillar | Use case that tests it | Why vanilla fails (→ the tool earns its keep) |
|---|---|---|
| **MCP** | "rank CA ≥50 MW solar owners by desert-zone exposure" | a plain LLM can't pull + aggregate 15K plants; no entity IDs, no `as_of` |
| **Reference** | "directional ENSO exposure, properly caveated, no overclaim" | a plain LLM over-claims — Medium not LOW, magnitude leakage, weak sourcing |

The output is a **with / without comparison** artifact. The sharp framing: validation isn't "is the output good," it's "is the output *unreachable without us*." Define the use case *before* the A/B, or "satisfied" can't be judged.

## Reconciliation With The Testing Buckets

The collaboration thread lists **three prompting buckets**; this doc defines **two use-case buckets**. Both right, different levels:

```text
USE-CASE buckets (2)          prompting buckets (the meet thread, 3)
Bucket 1 · bottom-up    =     #1 single-user query  (asset → phenomenon)
Bucket 2 · top-down     =     #2 internal top-down   (phenomenon → asset/region)
                              #3 precise/structured  = a TESTING LENS, not a 3rd use case
```

## Scope — the V0 Slice

V0 deliberately picks a **subset**:

```text
   V0  =  one resource (ENSO) · one region / one asset class · INTERNAL-team audience · one manual test
   later =  client/public renderings · multi-resource · the other buckets
```

**Reconciliation:** Test Run 001 actually ran **top-down** by this doc's own definitions (a phenomenon → fleet scan: El Niño → CA ≥50 MW solar), not an asset-anchored drill. The V0 label was wrong on direction; corrected here. The genuinely missing slice is **bottom-up**, completed by `plans/2026-06-11_layered_reference_v1.md` Phase 5 (which ships the top-down + client/public contracts ahead of multi-resource).

### Scope Statement (V0)

```text
El Niño / ENSO exposure  ->  renewable assets  ->  one region or market  ->  actor relevance
```

The package lets a contributor run a manual Claude/MCP test using existing InfraSure data tools, producing one applied-insight draft that is grounded, caveated, and reviewable.

### V0 Deliverable

```text
one methodology resource package  +  one prompt projection  +  one data requirements map
  +  one applied-insight draft  +  one manual MCP/Claude test run  +  one learning/gap log
```

The package shape and the contract each file meets are `method/resource_standard.md`; the input taxonomy is `method/data_map.md`; the learning companions are `learning/03_methodology_resources.md` + `04_prompt_projection.md`.

### MCP-Ready, Not MCP-Integrated

V0 is MCP-ready, not MCP-integrated. **Do not build**: a production agent · an API orchestrator · a database table · automated batch generation · an email automation workflow · new MCP tools unless a test proves a specific gap. The first test happens in a Claude project/session with the methodology files loaded alongside the live MCP tools. (One real gap is known — `search_plants(iso=…)` returns empty; scope by `state` and log it — `status/mcp_gaps.md` R1.)

### Gate 1 — what analysis should exist?

Infrastructure decision intelligence, not market commentary. The atomic question:

```text
What grounded change, exposure, opportunity, or constraint affects a specific asset, region,
company, offtaker, or portfolio, and what can InfraSure responsibly claim about it?
```

The family map is `method/analysis_families.md`; V0 starts with `Exposure → consequence → actor relevance`.

### Gate 2 — what evidence and logic are required?

Every resource must name: substrate inputs · external sources · descriptive context (not claim-grounding) · actor/account context · the reasoning steps that convert inputs to claims · which claims are allowed / downgraded / blocked. The standard is `method/resource_standard.md`; the input taxonomy is `method/data_map.md`.

### Acceptance Criteria (V0)

V0 is complete when a new contributor can explain the deliverable from `README.md` + this doc; the projection runs a manual test; the test yields one applied-insight draft; every material claim has a source ref or an explicit external dependency; confidence + caveats + actor relevance are present; and failures are categorized (method / MCP-tool / external-data / orchestration gaps). The current status ladder is `status/capabilities.md`.

---

**See also**: `architecture.md` (the 3-pillar overview + the 4 layers), `method/analysis_families.md` (the families, orthogonal to these buckets), `resources/_style/output_contracts.md` (the three-output model this scopes), `principles.md` P2 (content downstream of validated insight), `status/capabilities.md` (where V0 stands).
