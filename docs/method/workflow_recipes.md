# Workflow Recipes — composing resources into analytical jobs (the authored-intelligence scaffold)

> **Status**: v0 — **NAMED + one worked recipe PROVEN** (§7), 2026-06-14 (`../plans/2026-06-13_knowledge_base_expansion_v1.md` Phases 1 + 4). This doc *defines* the recipe layer (§1–§6) and carries the first worked, end-to-end-run recipe (§7). Still **no catalog, no engine** — that stays a v0 REJECT.
>
> **The rail (load-bearing, `../principles.md` P1 corollary)**: a recipe is **a docs/spec the model READS, never an engine we BUILD.** No `code/`, no `scripts/`, no planner/orchestrator. The *intelligence* (planning + synthesis) is the model's job — the volatile/L2 layer; a recipe is the *authored scaffold* (stable/L0) that guides it. A "recipe runtime" is a permanent **REJECT** in v0.

## 1 · What a recipe is

A **resource** answers *"how should the model reason about ONE driver?"* (`el_nino_enso`, `hail_solar`). A **recipe** answers the **job-level** question — *"given this portfolio / region, what should I inspect, in what order, and how does it resolve to a decision?"* — by **composing** resources.

```text
recipe = { job · ordered resources it composes · the _method primitives it calls ·
           the human checkpoint · the gate · the render target }
```

```text
financial-services analog        InfraSure
─────────────────────────        ─────────
skill   (comps-analysis)    →     RESOURCE   (one driver×mechanism method)        resources/<domain>/<slug>/
agent   (market-researcher) →     RECIPE     (a job that sequences resources)     docs/method/workflow_recipes.md
                                             — MINUS the runtime (the model executes it, not an engine)
```

## 2 · Why it exists (the grain payoff)

The recipe layer is what lets the catalog stay **dozens, not hundreds**. Driver-keyed resources stay small *because* cross-resource orchestration lives **one layer up**, here — not in a fork per job or per actor:

```text
a RESOURCE stays (driver × mechanism)-keyed   ──because──►   the job composition (Screen / Evaluate / Mitigate,
   (hail×solar, ENSO, hurricane×wind)                         top-down / bottom-up) lives in a RECIPE that
   actor + asset-class are FACETS, never forks                composes resources — not by forking the catalog
```

## 3 · The two things a recipe composes (the two resource classes — `resources/README.md` D7)

```text
(1) driver-keyed RESOURCES        the methodology packages in the domain tree (hail_solar, enso, ...)
                                  → the PARALLEL fan-out (each scores the same fleet independently)
(2) non-driver _method PRIMITIVES damage functions · insurance/materiality · DSCR · EVT (resources/_method/)
                                  → the VERTICAL legs that have NO external driver (no NOAA-style feed for "DSCR")
```

InfraSure's headline chain — **hazard → generation → revenue → insurance $** — is *vertical/sequential*: one step's output is the next's input, and the finance/insurance legs have no external driver, so they are not resources. A recipe stitches the vertical chain from class (2). (This is the exact composition Phase 4 tests — and may surface where it breaks.)

## 4 · How a recipe runs (the model reads it; a human runs the loop)

A recipe is the **L2 runtime loop** (`../architecture.md` §4), *guided* by authored steps — not coded:

```text
resolve scope → select relevant resources/_method → fan out across the fleet → score exposure·materiality·
confidence (_method) → drill the top cases → assemble the validated insight object → GATE → render only post-gate
                              ▲___ human checkpoint (enrich · re-scope · challenge) ___│
```

Every material claim still passes the gate (`confidence_rules` + `blocked_claims`); a recipe **never** relaxes a resource's discipline — it sequences it.

## 5 · The jobs recipes will express (not authored yet)

The job axis (`../use_cases.md`, `analysis_families.md`): **Screen** (rank a portfolio) · **Evaluate** (defend a single-asset position) · **Mitigate** (design transfer/adaptation); and the two buckets — **top-down** (phenomenon → assets) / **bottom-up** (asset → phenomenon). These become *named recipes that compose resources*, not new resources.

## 6 · Status — named, not cataloged

```text
DONE (Phase 1)  the recipe layer is DEFINED (this doc) + the rail is bound.
DONE (Phase 4)  ONE worked recipe — screen_solar_hail_to_insurance_exposure — authored + run end-to-end (§7).
                VERDICT: the layer + the two-resource-class model (D7) HOLD; the vertical $ leg composes via a
                _method primitive (directional) — the $ itself stays blocked to model-gpr.
NEVER in v0     a recipe CATALOG (only after the pattern is proven + demand exists) · a recipe ENGINE/planner (P1).
```

## 7 · Worked recipe — `screen_solar_hail_to_insurance_exposure` (Phase 4, run 2026-06-14)

The first recipe, authored **and** run end-to-end as a manual loop to prove the layer. It composes two driver-keyed resources as a **parallel fan-out** and calls a `_method` primitive for the **vertical** insurance-$ leg — the deliberate test of the grain-verification's predicted sharp edge: *does the vertical hazard → exposure → $ chain have something to compose, or does it break?*

### The recipe (the guided-reasoning spec — the model reads this)

```text
recipe: screen_solar_hail_to_insurance_exposure
job:    Screen a solar fleet for severe-hail + heat-derate exposure, rank by exposure × materiality,
        and translate the top cases toward insurance relevance — for an owner / lender.
composes (driver-keyed RESOURCES — parallel fan-out, each scores the same fleet):
   · hail_solar           → hail exposure + realized-event impact per asset
   · extreme_heat_derate  → thermal-derate exposure (peak-coincident) per asset
calls (NON-driver _method PRIMITIVES — the vertical leg, class (2)):
   · screen / rank / score  → order the fleet by exposure × materiality × confidence
   · insurance_materiality  → exposure → DIRECTIONAL insurance relevance (the $ stays model-gpr — blocked)
checkpoint:  human reviews the ranked screen + the drilled top cases before any render
gate:        per-part confidence · block $ / EAL / forward probability · VERIFY every hazards classification
render:      (post-gate only) a portfolio-screen card / account note
```

### The run (manual loop, grounded — `as_of` 2026-06-14)

```text
1. SCOPE     ERCOT/TX solar ≥ 50 MW (state=TX; iso filter unwired, R1). Fleet = 70,349 MW / 378 plants (aggregate).
2. FAN OUT   score the fleet on two drivers (each resource independently):
               hail_solar          → TX = US hail maximum; single-axis c-Si arrays exposed; realized events in hazards news
               extreme_heat_derate → ERCOT summer heat → modest peak-hour de-rate (directional, LOW)
3. RANK      by exposure × materiality × confidence (screen/rank/score _method):
               #1  the Fort Bend hail cell — Fighting Jays (62945, REALIZED Mar-2024 hail, CF 0.37→0.15→0.33)
                   + same-cell Cutlass I/II (66310/66262, ~314 MW) + Old 300 (64133, 430 MW) ≈ 970 MW in one footprint
               +   Aktina (64927, 500 MW) — heat-derate, peak-coincident
4. DRILL     top case Fighting Jays — realized hail (factual/medium), CIP-owned, single-axis c-Si
5. VERTICAL  insurance_materiality(_method) on the top cases → DIRECTIONAL: hail = high financial-materiality,
             typically sub-limited / separate deductible → an owner/lender concern.  $ / EAL = BLOCKED (model-gpr)
6. GATE      per-part confidence (realized event medium · forward exposure low · $ blocked); VERIFY held
```

### The validated screen (the recipe's output)

> **Claim** — Within the ERCOT/TX solar fleet (70,349 MW / 378 plants), the highest-ranked severe-hail exposure is the **Fort Bend County cell**: **Fighting Jays (62945, 227.5 MW, CIP)** — which took a realized Mar-2024 hailstorm **visible in its CF (0.37 → 0.15, recovered to 0.33 by mid-2025)** — sits with same-cell **Cutlass I/II (66310/66262, ~314 MW)** and **Old 300 (64133, 430 MW)**: ≈ **970 MW of single-axis c-Si solar in one hail footprint**. Heat-derate adds a **modest, peak-coincident** second exposure across the fleet (e.g. Aktina 64927). For an owner/lender, hail on this book is a **high-materiality, typically sub-limited / deductible** insurance exposure.
>
> **Confidence (per-part)**: realized hail event = *factual/medium* · forward fleet hail + heat exposure = *low/directional* · insurance-$ severity = **blocked** (model-gpr).
> **Held**: no $/EAL/payout · no forward hail probability · no plant-level forecast · no single-cause attribution · hazards classifications VERIFIED.
> **Source refs**: `aggregate` (TX 70,349 MW) · `get_plant`/`nearby_plants` (62945 + the cell) · `get_plant.generation` (the CF series) · the `hail_solar` + `extreme_heat_derate` methods · `_method insurance_materiality` (directional). `as_of` 2026-06-14.

### Verdict — does the composition hold?

```text
PARALLEL fan-out   ✅ HOLDS — hail_solar + extreme_heat_derate independently scored the same fleet; no forking,
                      no per-job/per-actor resource needed. The recipe absorbed the composition (the grain payoff).
VERTICAL $ leg     ✅ HOLDS — the predicted sharp edge is RESOLVED by the two-resource-class model (D7): the
                      vertical insurance-$ leg had a legitimate thing to compose — the _method insurance_materiality
                      PRIMITIVE — NOT a missing driver-resource. The leg ran DIRECTIONAL; the quantified $ stayed
                      correctly blocked to model-gpr (the Wave-2 upgrade).
LIMITATION (honest) the _method primitives are STUBS, so the vertical leg's scoring is qualitative/directional,
                      not yet a computation. EXPECTED — the recipe is the forcing function that defines the
                      primitive's contract (what insurance_materiality must return directional now, and quantitatively
                      once model-gpr is wired). Logged, not papered over.
NET                the recipe layer + D7 two-class model are VALIDATED on one end-to-end run. No catalog, no engine,
                      no code. The "intelligence" stayed the model's job, guided by the authored scaffold (P1 corollary).
```

---

**See also**: `../principles.md` (P1 corollary — scaffold/L0 vs orchestration/L2 + the no-code rail) · `../../resources/_method/README.md` (the primitives class (2) recipes call) · `../architecture.md` §4 (the runtime loop a recipe guides) · `analysis_families.md` (the 7 families + the Q&A grammar a recipe composes) · `../use_cases.md` (Screen/Evaluate/Mitigate + the two buckets) · `../plans/2026-06-13_knowledge_base_expansion_v1.md` (Phase 4 authors the first worked recipe).
