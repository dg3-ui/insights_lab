# Hurricane / High-Wind Exposure For Wind Assets — Method (human-readable)

> **Status**: draft 2026-06-14. The human-readable companion to `resource.yml` (the structured operation) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resource + structural reference: `../hail_solar/`.

## What it answers (and what it refuses)

```text
ANSWERS   which wind assets/owners/regions sit in a hurricane / high-wind (coastal/Gulf) geography · through what
          mechanism (TEMPORARY cut-out vs LASTING structural damage) · what a realized storm (Beryl) meant
          regionally · who should care
REFUSES   exact $ loss / EAL / PML / payout · forward hurricane probability / return-period · plant-level forecast ·
          single-cause attribution of a CF change (the July dip IS the summer wind lull) · lasting damage from a
          sub-Cat-3 storm · outreach before the gate
```

## Scope

Wind (onshore, utility-scale ≥ ~50 MW) · one region/market per test (test 001 = coastal/Gulf ERCOT/Texas) · operating + queue (siting) · actors: owner-operator · investor · lender · developer.

## Mechanism (cite `knowledge.md`; do not re-derive) — the TWO claim types

```text
(A) TEMPORARY CUT-OUT   wind ≥ ~25 m/s → blades feather + rotor shuts down (by design) → ~zero output during the
                        storm → restarts + recovers. A short availability loss, NOT damage. The common case.
(B) LASTING DAMAGE      Cat 3+ gusts exceed the turbine design wind class → blade/nacelle/tower loss; coastal sites
                        add storm-surge to foundations/substation → weeks-to-months outage. The rare, capital case.
```

Geography: the **Texas Gulf Coast is in the US landfalling-hurricane corridor** (NHC HURDAT2). **Hurricane Beryl (2024-07-08) made TX landfall as ~Cat 1 near Matagorda** — squarely the cut-out (A) regime, not the damage (B) regime. The whole discipline of this resource is **not conflating A and B**, and **not reading the storm into the monthly CF series** (the July low is the seasonal wind minimum — `knowledge.md` §4).

## Procedure (the real tool sequence)

```text
1. hazard state:  NHC track / HURDAT2 (geography + landfall) AND/OR search_news(category=hazards, query="hurricane"/storm name) → VERIFY each
2. scope:         search_plants(fuel="wind", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" → [] (R1); filter to coastal counties via get_plant
3. footprint:     get_plant geometry/county + turbine_locations + nearby_plants  → wind in the same coastal corridor
4. realized:      get_plant.generation  → CONTEXT ONLY; state explicitly that monthly CF cannot isolate the cut-out from the summer lull
5. actor:         get_plant.ownership   → owner chain + coastal-portfolio accumulation
6. draft:         assemble the claim grammar; cap confidence; block the $ / probability / single-cause / sub-Cat-3-damage claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional coastal hurricane/high-wind exposure · the cut-out-vs-damage mechanism (cited) · a realized storm
         made landfall in the corridor near a named coastal wind asset (REGIONAL fact) · owner/portfolio coastal
         accumulation · mitigation (feather/shutdown, design wind class, surge siting) · monitoring/hardening recs
BLOCKED  exact $ / EAL / PML / payout · forward probability / return-period · plant-level forecast · single-cause CF
         attribution (the July dip ≠ Beryl) · lasting DAMAGE from a sub-Cat-3 storm · national-from-regional · outreach
```

## Confidence + caveats

Confidence is **per-claim-part**, and the ceiling is **lower than `hail_solar`** because the realized-impact signal that made hail strong does NOT exist here:
- *Coastal-corridor exposure + cut-out/damage mechanism* — **Medium** (clear geography, resolved scope, robust physics).
- *A realized storm (Beryl) made landfall near the asset* — **factual** as a *regional* event (NHC + hazards news), but it is **not** a wind-plant damage claim.
- *Any read of the storm into the CF series* — **Low / blocked** (monthly CF cannot isolate the cut-out; July IS the summer lull).
- **High is not reachable** on the substrate alone (would need a verified wind-plant damage record — which the substrate does not carry — or a served TC hazard model).

Required caveats: cut-out (temporary) vs damage (lasting) stated; monthly CF cannot isolate the cut-out from the seasonal minimum; Beryl was Cat 1 (below most turbines' design class → cut-out, not widespread damage); classification verified, not taken on the label (and it links to nuclear/hydro, not wind); $ severity is not modeled (model-gpr). This is `grounding_maturity: model-not-wired` — the $ / damage-severity / forward-probability layer is the model-gpr upgrade (`mcp_gaps` R12).

## Actor relevance

Owner (cut-out availability planning, design-class review, surge/foundation hardening, outage recovery) · investor (Gulf coastal-portfolio accumulation) · lender (DSCR stress from a hurricane outage — directional) · developer (siting/turbine-class/surge-aware foundations for queue-stage coastal wind). Relevance never distorts the method.

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + the two-claim-type split + the Beryl/Peyton Creek anchor) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (the validated output) · `test_runs/test_run_001.md` (the live test record) · `../hail_solar/` (the sibling hazard resource).
