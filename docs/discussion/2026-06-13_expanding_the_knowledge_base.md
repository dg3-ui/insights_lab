# Discussion — Expanding the Knowledge Base (which resource to add, and how)

> **Status**: **RESOLVED-INTO-PLAN** (`../plans/2026-06-13_knowledge_base_expansion_v1.md`), 2026-06-14 — opened 2026-06-13 as a **draft to argue with**; its decisions now live in the plan (kept here as the record of *why*). Seeded by a 4-source research sweep (the InfraSure front page · the owner's `.learning` vault · the lab's existing taxonomy · what the platform can actually ground).
>
> **The question**: we have one validated resource (`el_nino_enso`). The domain is huge — weather, climate, energy, and underneath it research, math, climate science, hazard analysis, price analysis, project finance, insurance. Before authoring more, settle **how to categorize and prioritize** so we add the *right* resources in the *right* manner — without category sprawl or ungroundable resources.
>
> **How to read it**: each section gives a **proposal + the open question**. The decisions that are genuinely yours are collected in §9. Nothing here is locked; it feeds iteration, then a plan.

## 1 · What InfraSure Is (the frame)

InfraSure is **decision-grade risk intelligence for US energy infrastructure** — forward-looking, localized, asset-specific risk / insurability / resilience intelligence for **owners · investors · lenders**. Its core abstraction: each asset is a **physical twin + financial twin**, where 8 inputs (Weather · Hazard · Grid · Equipment · Policy · Debt · Revenue · Resilience) recompute through one engine to produce a coherent chain — **hazard → generation → revenue → DSCR → insurance trigger** ("weather-to-cashflow coherence") — feeding three workflows: **Screen** (rank a portfolio) · **Evaluate** (defend a single-asset position) · **Mitigate** (design transfer/adaptation).

The lab sits on the **open public substrate beneath that product** (~15.5K plants, generators, ~9.8K queue, ~57K news), served read-only via the MCP tools. A methodology resource teaches a model to reason like the analyst over *that substrate*.

## 2 · The honesty check that bounds everything (read first)

The product **shows** EAL / VaR / PML, P50/P90 generation, DSCR/CFADS, nodal LMP, 45yr ERA5, CMIP6. **Most of that lives in `model-gpr`'s dev database, not the public MCP the lab can query.** So the moat-true question for every candidate resource is:

```text
Can the MCP substrate + ONE named external feed actually GROUND a defensible claim today?
   substrate-only (directional)      → ship now (the ENSO pattern)
   model exists but not on the MCP   → ship DIRECTIONAL now, log the tool gap, upgrade later
   needs data we don't have          → defer
```

This is exactly the wall ENSO hit (it can't make a plant-level production forecast). It will recur for hazard (EAL), price (forward LMP), and finance (DSCR). **Grounding maturity, not topic appeal, sequences the buildout.**

## 3 · Categorization — keep the spine, extend in three places (proposal)

The existing model is already validated against both the `.learning` vault (~377 files) and the product's own IA. **Recommendation: do not reinvent it.**

```text
KEEP (the spine)
  · ONE driver-grouped DOMAIN folder per resource   (storage axis; materialize on first resource)
  · FAMILY · DRIVERS · ACTORS as faceted tags        (find axes; family = the 7 question-types)
  · a resource = one (family × driver) cell          (el_nino_enso = Exposure × ENSO)
  · persona (owner/investor/lender) is a TAG, never a folder
      — "one probabilistic reality, many stakeholder projections": don't fork a resource per stakeholder
  · underscore shared layers (_principles · _style · _craft · _reference) — form/method, never grounding

EXTEND (three minimal additions)
  1. FINISH THE DOMAIN TREE. The 5 planned domains (weather_and_climate ✅ · hazard · market · policy ·
     commercial) don't house finance/insurance or the deep research/math. Proposal: add `hazard` and
     `finance` as domains, and put the cross-cutting math/finance/insurance methodology (EVT, copulas,
     DSCR mechanics, parametric/basis-risk, climate-stationarity) in a NEW shared layer `_method/` —
     cited by many resources, quarantined from grounding like _reference. Math gets a home without
     inventing a fake "research" domain.
  2. TWO SEQUENCING FACETS (not folders): grounding_maturity (substrate-only | model-not-wired |
     needs-data) and data_maturity (H/M/L). They don't categorize — they set the confidence ceiling
     and the build order.
  3. A PERIL FIELD STANDARD: adopt the vault's hazard-CSV columns (predictability · key-datasets ·
     climate-attribution-confidence · financial-materiality · insurance-treatment) as the resource.yml
     shape for any peril resource — so peril authoring is a CSV-row → package transform.
```

Deliberately **left as runtime views, not tags**: bucket-direction (top-down/bottom-up) and audience-tier (internal/client/public) — composing them at session time beats bloating the tag axis.

## 4 · The grain question — the #1 hurdle you named

"Which resource, and in what *manner*" is really: **what is a resource keyed on?** This one choice sets the count (dozens vs hundreds).

| Option | A resource is… | Count | 
|---|---|---|
| **A — driver/peril-keyed** (recommended) | one per driver (ENSO, drought, wildfire, congestion), with **actor + asset-class as facets** | dozens |
| B — (peril × asset-class) | split per asset because damage functions differ | ~100s |
| C — (peril × actor) | split per stakeholder | ~100s, and fights the "one reality" principle |

**Recommendation to debate**: **A** — key on the driver; **split by asset-class only when the physical mechanism genuinely differs** (hail on trackers ≠ hail on transmission); **actor is always a facet, never a split** (the risk-spine: one reality, many projections). This keeps the catalog small and the ENSO pattern intact.

> **What lets A work** (see `2026-06-13_architecture_lessons_anthropic_fs.md` §5): the cross-resource orchestration (Screen/Evaluate/Mitigate, bucket-1/bucket-2) lives **one layer up**, in a named **recipe** that composes driver-keyed resources — *not* by forking the resource per job or actor. Driver-keyed grain is only safe **because** the recipe layer absorbs the composition. The two decisions are linked: adopt the recipe layer and grain A holds; reject it and pressure to fork the catalog returns.

## 5 · Prioritization — what to add next (proposed criteria, in order)

```text
1. GROUNDING MATURITY first   — can the substrate + one named feed stand up a defensible claim today?
2. MOAT (the vanilla-LLM A/B)  — if a generic model could write it with no InfraSure entity/ID/field, it's commentary
3. REUSE LEVERAGE             — the FIRST resource in a domain builds the shared feed/region/caveat machinery the
                                whole domain inherits; sequence first-in-domain deliberately
4. COVERAGE VALUE             — today 1/7 families + 1/5 domains exercised; an untested family×domain cell
                                teaches the scaffold more than deepening a proven one
5. ACTOR VALUE               — owner / investor / lender; which persona is wave-1 priority?
6. FINANCIAL MATERIALITY     — TIE-BREAKER only (so the moat wins): high-materiality + low-data ships caveated or waits
7. STRESS-TESTS THE METHOD   — does it prove the ENSO pattern generalizes beyond one climate regime?
```

The tension to resolve: **grounding-led** (moat-true, ship cheap directional) vs **materiality-led** (chase the biggest-impact perils). The ENSO evidence favors grounding-led.

## 6 · Candidate longlist (raw material, feasibility-tagged — NOT commitments)

| Category | Candidates | Feasible today? |
|---|---|---|
| **weather_and_climate** (extend ENSO's neighbors) | drought/low-hydro · heat-wave de-rate · wind-drought · cold-snap (Uri) · other regimes (NAO/PDO, atmospheric rivers) | ✅ directional — near-copy of the ENSO scaffold, NOAA-class external pulls |
| **hazard** (NEW domain — first resource builds the FEMA/USGS feed) | wildfire (transmission + WUI solar) · hurricane+coastal-flood · flood (solar) · hail (trackers) · winter-storm · tornado/SCS | ◑ partial — substrate grounds location/attributes; damage models exist in model-gpr but **not on the MCP** → directional now + log the gap |
| **market** (NEW domain — LMP/curtailment slice) | curtailment/negative-pricing by hub · congestion/basis risk · PPA re-contracting/merchant-tail · hedgeability | ◑ partial — node crosswalk + historical LMP ground bounded claims; exact forward $/MWh stays blocked (like ENSO) |
| **commercial** (partly grounded today) | offtaker concentration / PPA roll-off · owner hazard-concentration rollup · SPV→parent resolution | ✅ factual (partial coverage) — FERC EQR + ownership chain |
| **policy / development-risk** (NEW domain) | interconnection-queue delay/withdrawal · permit/regulatory event-translation · IRA/ITC-PTC/tariff exposure | ◑ partial — queue + news ground the signal; `developer` null weakens actor-routing; policy needs a docket feed |
| **performance + event-translation** (untested families, substrate exists) | peer-relative CF underperformance · degradation/vintage profiling · outage→owner/offtaker translation · M&A translation | ✅ today — historical generation, compare_entities, classified news |
| **_method/ primitives** (NOT topical resources — the math/finance, factored out) | statistics/EVT scoring · project-finance mechanics (DSCR/CFADS) · insurance peril-pricing + basis-risk · the external-live-state (NOAA-pull) discipline | ✅ as documentation — form/method, no substrate dependency |

## 7 · Sequencing — two honest options

```text
DEEP        more weather_and_climate (drought, heat, wind-drought) — reuse NOAA + the proven ENSO pattern,
            lowest cost, but only re-validates one corner of the scaffold.
BROAD       one first-in-domain resource each across hazard / market / commercial / performance — higher cost
            (stands up new feeds), but validates the family×domain grid and stress-tests the resource_standard.

WAVE MODEL (a reconciler): Wave 1 = a cheap set of substrate-only DIRECTIONAL resources spanning a few families
            (validate the grid with ~zero MCP work); Wave 2 = wire model-gpr to upgrade their confidence from
            directional → quantitative. The ENSO evidence favors proving generalizability cheaply first.
```

## 8 · Risks to avoid (you said: it's broad, be careful)

- **Scope creep via breadth** — each of weather/hazard/price/finance/insurance is a *body of knowledge*, not a resource. The GATE-1 bar (needs an InfraSure entity/ID/field; beats the vanilla-LLM A/B) is the real scope filter — apply it *before* authoring.
- **Ungroundable resources** (the biggest trap) — authoring one whose core claim needs a field the MCP can't return (EAL, forward LMP, DSCR). The product shows these; the lab can't retrieve them. Tag `grounding_maturity`, log the gap, ship directional, never assume the field.
- **Category / axis sprawl** — 6 axes already exist; only `grounding_maturity` + `data_maturity` earn new facets. No folder-per-family, no fork-per-stakeholder.
- **Reinventing the spine** — it's already aligned with the vault *and* the product IA; extend in the three named places, don't redesign.
- **Materiality-led drift** — chasing hurricane/hail before checking they're groundable produces confident commentary that fails the moat.
- **Premature breadth** — ENSO is the *only* proof point; stand up 2–3 more that stress different parts of the standard (a non-weather one, a factual-commercial one) before declaring the taxonomy validated.

## 9 · Decisions for you (what we iterate on)

1. **Grain** (§4): key resources on the **driver** (actor + asset-class as facets, split only when the mechanism differs) — agree, or prefer (peril×asset-class) / (peril×actor)?
2. **Domain tree** (§3): add **`hazard` + `finance` domains + a `_method/` shared layer** — or fold finance into commercial/market? This gates everything else.
3. **Family set** (§3): are the 7 families frozen as we leave Exposure, or do we reconcile them with the vault's analytical-mode (descriptive/predictive/evaluative/prescriptive) + finance topics first?
4. **Sequencing** (§7): **deep** (more weather), **broad** (one per domain), or the **two-wave** model?
5. **Grounding-led vs materiality-led** (§5): which leads the priority order?
6. **Substrate-boundary inventory** (§2): do an honest "what can the MCP actually return vs what's only in model-gpr" pass before prioritizing hazard/price/finance? (I'd argue yes, it's cheap and prevents ungroundable resources.)
7. **Non-stationarity** : make climate non-stationarity a first-class `confidence_rule` on every weather/climate resource?

Pick any to start — or react to the proposals and I'll iterate the doc. When enough of these settle, this becomes a plan in `docs/plans/`.

---

**See also**: `README.md` (what a discussion is), `../method/analysis_families.md` (the 7 families) + `../../resources/README.md` (the domain·family·drivers·actors spine this extends), `../principles.md` P6 (references inform, don't bind — the longlist is raw material, not a mandate), `../status/mcp_gaps.md` (where the model-gpr / hazard-tool gaps get logged), `.learning/` (the owner's vault the categories were mined from).
