# Test Run 001 — Extreme-Heat Thermal Derate, ERCOT/Texas Solar

> **Status**: 2026-06-14, **PASS** (with logged gaps). The manual MCP/Claude test record (`../../../docs/process/test_protocol.md`). This run authored + validated the `extreme_heat_derate` resource against live InfraSure MCP data + a live NOAA pull. (Raw transcript = this session.)

## Question tested

> "Which ERCOT/Texas solar plants ≥ 50 MW are exposed to a hot summer's thermal de-rate, how big is the effect, and why does it matter?" — one region (TX/ERCOT) · one asset class (solar) · summer.

## What the model retrieved (the real call sequence)

```text
1. NOAA/CPC seasonal temperature outlook (web)               → summer-2026 JJA above-normal LEAN across much of lower-48,
                                                               highest confidence West; south-central/TX inside the broad
                                                               lean, NOT the top-confidence region (issued ~mid-May 2026)
2. PV temperature-coefficient / NOCT references (web)         → c-Si power temp coefficient ~ -0.3 to -0.45 %/°C; STC 25 °C;
                                                               NOCT 40–48 °C  (the modest-magnitude ceiling)
3. search_plants(fuel="solar", state="TX", minMw=50, limit=25)→ the TX solar fleet (Tehuacana 1254.8, Rowdy Creek 1050, …)
4. search_plants(fuel="solar", iso="ERCOT", minMw=50)         → []  (GAP: iso filter unwired — see Gaps)
5. aggregate(plants, group_by=state, metric=total_capacity, filter={fuel:SUN}) → TX 70,349.3 MW (#1; CA 36,843.1)
   aggregate(plants, group_by=state, metric=count,        filter={fuel:SUN}) → TX 378 plants
6. get_plant(64927)                                           → Aktina Solar: 500 MW AC single-axis c-Si; Wharton; ERCOT
                                                               South HB_SOUTH/LZ_SOUTH; Tokyo Gas; monthly CF series
7. get_plant(64927).generation                               → summer-2025 CF ≈0.30 vs winter ≈0.09–0.15 (the HONESTY proof)
8. nearby_plants(64927, solar)                               → Danish Fields 66914 (600), Red Tailed Hawk 66157 (360),
                                                               Flag City 65844 (167.3) — same heat/zone cluster
```

## Accepted claims

- **Extreme heat de-rates c-Si PV via the temperature coefficient (~ −0.3 to −0.45 %/°C)** — *low*, directional (robust mechanism, second-order magnitude, no plant-level thermal model).
- **Summer monthly CF is HIGH (≈0.30) vs winter (≈0.09–0.15)** — *factual* (substrate), and used to **bound** the claim (the de-rate is intra-day, not a monthly-CF drop), NOT to size a loss.
- **The de-rate matters because it coincides with the ERCOT summer demand/price peak** — *low*, the strongest framing (logically robust, still directional).
- **TX = #1 solar fleet (70.3 GW / 378 plants); ~1,127 MW more solar within ~17 km of Aktina** — *low* directional exposure + same-zone fan-out.
- Owner routing (Tokyo Gas), single-axis/c-Si construction, mechanism + design recs — all grounded/cited.

## Rejected / downgraded claims

| Claim attempted | Disposition | Why (failure taxonomy) |
|---|---|---|
| "Heat costs this plant X % / Y MWh this summer" | **blocked** | external-data: no plant-level thermal/cell-temp model (model-gpr); only the temperature coefficient ceiling is citable |
| "Summer CF is low / heat drags summer output down" | **rejected** (the defining trap) | method/over-magnitude: summer CF is HIGH (irradiance-dominated) — reading heat off monthly CF is backwards |
| "Heat will cost $Z of revenue" | **blocked** | external-data: $ is model-gpr; no pricing/revenue model here |
| "N-year return-period of a derate-driving heat event" | **blocked** | method: a seasonal outlook has no forward return-period skill; non-stationarity |
| "The Feb-2025 CF collapse shows heat impact" | **rejected** | method: that dip is a WINTER-STORM outage, not heat — single-cause / mis-attribution caught |
| "Texas solar nationally loses output to heat" | **downgraded** → scoped ERCOT/TX | method: national-from-regional |

## Fixes applied (fail → fix)

- **over-magnitude temptation (the core risk)** → made the **honesty rule** a first-class section in `knowledge.md` (§2/§5), `resource.md`, `prompt_projection.md`, and `SKILL.md`: summer CF is HIGH; never read heat off monthly CF; cap at LOW; magnitude MODEST; the point is peak coincidence. Added an explicit `blocked_claim` ("Reading a heat de-rate off a monthly capacity factor").
- **iso filter empty** → switched to `state="TX"`; confirmed ERCOT zone via `get_plant.grid` (HB_SOUTH/LZ_SOUTH) / `.regions.iso_rto`. (Baked into `prompt_projection` step 3 + `data_requirements`.)
- **no hourly data** → reasoned the intra-day de-rate from physics + the peak-coincidence logic; flagged the monthly-only resolution as a gap (pairs with R12).
- **single-cause temptation** → "consistent with / not single-cause" discipline; the Feb-2025 outage flagged as non-heat.

## Gaps logged (→ `../../../docs/status/mcp_gaps.md`)

- **R1 (repeat, confirmed for ERCOT)**: `search_plants(iso=…)` unwired beyond CAISO — used `state="TX"`.
- **R11 (repeat)**: climate-signal news channel empty — `search_news` does not index temperature/climate outlooks; relied on the NOAA pull + substrate.
- **R12 (extends the hazard wall to weather)**: no served plant-level thermal / cell-temp model (the quantified %/MWh de-rate + $) — the directional-now-quantify-later wall; + the substrate generation series is **monthly**, so the intra-day peak-hour de-rate is not directly observable (an hourly series would let us *show* the afternoon shave).

## Verdict

**PASS.** The resource produces a grounded, caveated, correctly-LOW-confidence insight that a vanilla LLM could not (it required the EIA plant_id, the single-axis/c-Si flags, the monthly CF baseline, the ERCOT zone, the owner chain, the fleet aggregate, and the live NOAA pull). The standout — and the discipline test — is that the resource **resists the over-magnitude trap**: it uses the HIGH summer CF to *bound* the claim (the de-rate is intra-day, peak-hour, modest) rather than to manufacture a "big summer loss," and reframes materiality around **peak coincidence** instead of energy. The weather-resource pattern (NOAA pull + substrate baseline + directional-LOW + honest magnitude, $ blocked) is validated; the honesty discipline is the reusable lesson for the next weather × performance resource (e.g. `wind_drought`, `drought_soiling`).
