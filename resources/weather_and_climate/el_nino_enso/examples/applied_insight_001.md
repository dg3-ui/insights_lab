# Applied Insight 001 — ENSO Exposure, CAISO Solar (Winter 2026-27)

> **Status**: validated test output (produced in `test_runs/test_run_001.md`, 2026-06-05).
>
> **Methodology**: `el_nino_enso` · **Knowledge**: `knowledge.md` · **As-of**: 2026-06-05.

## Claim

For the upcoming Northern Hemisphere winter (DJF 2026-27), NOAA CPC carries an **El Niño Watch** with a **~96% chance of El Niño** during DJF. El Niño winters tend toward **wetter, cloudier conditions across California**, which would depress an **already-low winter solar capacity factor**. The operating California utility-scale solar fleet (≥ 50 MW; ~36.8 GW of CA solar in total) therefore carries **directional downside exposure on winter 2026-27 generation**. **Confidence: LOW** — El Niño *occurrence* is likely, but its *strength* (and thus the size of any effect) is not yet determinable, and the teleconnection is noisy at the single-season level.

## Scope

| Field | Value |
|---|---|
| Entity scope | Operating CA solar ≥ 50 MW (resolved via `state="CA"`; `iso="CAISO"` filter unwired) |
| Fleet size | CA solar total **36,843 MW** (`aggregate`, as-of 2026-06-05) |
| Named exemplars | Topaz Solar Farm (`57695`, 585.9 MW), Desert Sunlight 300 (`57993`, 313.7 MW), Darden I–IV (`69661-4`, 646.4 MW ea.), Pelicans Jaw (`68607`, 678.5 MW) |
| Time window | DJF 2026-27 (forward-looking, from the current forecast) |
| Actors | owner/operator first; offtaker, lender/investor where context exists |

## Mechanism

```text
El Niño (DJF) → strengthened subtropical jet → wetter/cloudier CA & Southwest winters
             → lower winter plane-of-array irradiance → lower winter solar capacity factor
```

Robustness: the CA/Southwest winter-precipitation signal is **moderate-to-high** but **probabilistic** (`knowledge.md` §4–§6). The substrate already holds the baseline this perturbs — Desert Sunlight 300 monthly CF runs **~0.38 in summer vs ~0.13 in winter**; a wetter El Niño winter pushes the low season lower. Claim type: **directional**, not causal/quantitative.

## Source References

| Type | Source | Entity / scope | Field or fact | Vintage / as-of | Role |
|---|---|---|---|---|---|
| external | NOAA CPC ENSO Diagnostic Discussion | ENSO state | El Niño Watch · ~96% El Niño DJF 2026-27 · Niño-3.4 +0.4 °C · strength uncertain | accessed 2026-06-05 | primary |
| external | IRI ENSO Forecast | ENSO state | corroborating model-ensemble outlook | accessed 2026-06-05 | corroborating |
| knowledge | `knowledge.md` §4–§6 | CA/SW | El Niño → wetter/cloudier winter → ↓ irradiance (moderate-high, noisy) | 2026-06-05 | mechanism |
| substrate | `aggregate` (plants) | CA solar | total_capacity 36,843 MW | 2026-06-05 | primary |
| substrate | `search_plants(fuel=solar, state=CA, minMw=50)` | CA solar fleet | fleet roster (Topaz, Desert Sunlight, Darden, …) | 2026-06-05 | primary |
| substrate | `get_plant(57993)` | Desert Sunlight 300 | seasonal CF (summer ~0.38 / winter ~0.13); owner Clearway; offtaker PG&E | 2026-06-05 | primary |

## Confidence

| Claim part | Confidence | Reason |
|---|---|---|
| El Niño present in DJF 2026-27 | Medium-Low | ~96% occurrence, but **strength uncertain** (no category > 37%) |
| CA solar fleet in scope | High | resolved from substrate (`aggregate` + `search_plants`) |
| Directional winter-CF downside | **Low** | teleconnection probabilistic + noisy; single winter can defy composite |
| Any MWh / $ / LMP figure | **Blocked** | outside allowed claims — no plant-level or price model |

Net: **directional exposure, LOW confidence.**

## Caveats

- Directional exposure — **not** a plant-level production or LMP forecast.
- ENSO teleconnections are probabilistic and vary by region, season, and event strength.
- A single winter can defy the composite — winter **2022-23** was a *wet La Niña* CA winter (Desert Sunlight Q1-2023 CF ran low), the opposite of the dry-La Niña expectation.
- Effect size scales with event strength, which is **not yet known**.
- Revenue/market effects depend on demand, hydro, congestion, marginal generation, and contract structure.

## Actor Relevance

| Actor | Why it matters | Rendering |
|---|---|---|
| Owner / operator (Clearway, BHE/Topaz, Intersect/Darden, Terra-Gen, Avantus) | watch winter generation variance + CA-solar concentration | platform card, account note |
| Offtaker (PG&E — 28 contracts on Desert Sunlight 300) | volume/settlement sensitivity on linked supply | account note |
| Lender / investor | DSCR / downside sensitivity to a weak-generation winter (caveated) | portfolio note |

## Review Trace

| Review item | Result |
|---|---|
| Every material claim has a source ref? | Yes — NOAA + substrate, all with as-of |
| Confidence declared + conservative? | Yes — LOW, capped at the weakest link (strength uncertainty) |
| Caveats attached to uncertain claims? | Yes |
| Overclaims blocked? | Yes — no MWh/$/LMP figures; no causal language |
| Scoped (not national)? | Yes — CA only |

## Gaps / Next Fixes

- **Tool gap**: `search_plants(iso="CAISO")` → `[]`; scoped via `state="CA"`. → wire ISO filter / add region resolution.
- A **fleet-level seasonal-CF rollup** (vs one drilled plant) would strengthen the generation evidence.
- No forward production model — quantitative effect remains blocked by design.
- Re-pull the ENSO forecast as it sharpens (strength resolves over summer/fall).
- A complementary **La Niña** resource would cover the drought/wildfire/curtailment side of the same domain.
