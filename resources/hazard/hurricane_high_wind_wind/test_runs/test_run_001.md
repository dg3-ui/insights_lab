# Test Run 001 — Hurricane / High-Wind Exposure, Coastal/Gulf ERCOT/Texas Wind

> **Status**: 2026-06-14, **PASS (directional, lower ceiling)** with logged gaps. The manual MCP/Claude test record (`../../../docs/process/test_protocol.md`). This run authored + validated the `hurricane_high_wind_wind` resource against live InfraSure MCP data. (Raw transcript = this session.) Pattern reused from `../../hail_solar/test_runs/test_run_001.md` — but the realized-impact leg is intentionally weaker (see Verdict).

## Question tested

> "Which coastal/Gulf ERCOT/Texas wind plants ≥ 50 MW are exposed to hurricanes / high wind, through what mechanism, and what did the realized Hurricane Beryl (July 2024) mean for a coastal asset and its owner?" — one region (coastal/Gulf TX/ERCOT) · one asset class (wind).

## What the model retrieved (the real call sequence)

```text
1. search_plants(fuel="wind", state="TX", minMw=50, limit=100)  → the TX wind fleet (Great Prairie 1027 MW, Horse Hollow 735.5, …);
                                                                   coastal-county filter → Peyton Creek I/II, Karankawa, Pattern Gulf
                                                                   Wind, Penascal, Los Vientos 1B, … (Matagorda/San Patricio/Kenedy/Cameron)
2. search_plants(fuel="wind", iso="ERCOT", minMw=50)            → []  (GAP: iso filter unwired for wind too — see Gaps)
3. aggregate(plants, group_by=state, metric=total_capacity, filter={fuel:WND}) → TX 49,719.6 MW (#1; OK 13,491.9, IA 13,409.5)
4. search_news(query="Beryl") + (query="hurricane", state="TX") → Beryl: Newsweek South Texas Project (6251 NUC) "threatened" Matagorda;
                                                                   Reuters ~1M TX customers offline. VERIFY surfaced ONLY non-wind hits
                                                                   (nuclear/hydro/gas) + a "hurricane"-tagged article that was a TORNADO (Lake Placid solar)
5. search_news(plant_id=67700) / search_news(fuel="WND")        → []  (GAP: no hazards news links to a WIND plant)
6. get_plant(67700) Peyton Creek II                            → 243 MW, 54× Vestas V163-4.5, Matagorda; COD 2025 → AFTER Beryl, no pre/post window
7. get_plant(62417) Peyton Creek I                             → 151.2 MW, 47× Nordex AW125/3150, Matagorda; COD 2020; full monthly CF series
8. read get_plant(62417).generation                            → CONTEXT: 2024-07 CF 0.129 == 2021-07 lull (0.129), > 2025-08 lull (0.078) → NOT separable from Beryl
9. nearby_plants(67700, fuel=wind, radius_km=80)               → only 1 neighbor (62417) → corridor built from coastal-county filter instead
```

## Accepted claims

- **TX = #1 US wind fleet (49,719.6 MW); a material coastal/Gulf sub-fleet sits in the NHC landfall corridor** — *medium* directional exposure (Peyton Creek I/II, Karankawa, Pattern Gulf Wind, Penascal, Los Vientos 1B, …).
- **Beryl made TX landfall ~Cat 1 (2024-07-08) near Matagorda; Peyton Creek I (62417) is in the landfall county** — *factual as a regional event* (NHC + corroborated hazards news), NOT a wind-plant damage claim.
- **Mechanism: cut-out (temporary, ≥~25 m/s) vs lasting damage (Cat 3+); Cat 1 ⇒ cut-out** — *medium*, cited (`knowledge.md` §1).
- Owner routing (RWE / Avangrid / Pattern / Duke), mitigation (feather/shutdown, design wind class, surge siting), actor relevance — all grounded/cited.

## Rejected / downgraded claims

| Claim attempted | Disposition | Why (failure taxonomy) |
|---|---|---|
| "Beryl caused the July-2024 CF dip at Peyton Creek" | **blocked** | method: not separable — 2024-07 CF (0.129) == 2021-07 lull; 2025-08 (0.078) lower with no storm |
| "Hurricane Beryl damaged the coastal TX wind fleet" | **downgraded** → "temporary cut-out, not widespread damage" | method/knowledge: Cat 1 is below modern turbine design wind class |
| "$X million in hurricane damage / EAL / PML" | **blocked** | external-data: $ loss is model-gpr; news has no wind-plant damage_estimate |
| "N-year hurricane return-period at this site" | **blocked** | external-data: no served TC model; track history alone has low forward skill |
| "Coastal TX wind will lose Y MWh next hurricane season" | **blocked** | method: plant-level forecast without a model |
| The Newsweek/Reuters Beryl articles as a WIND-plant impact | **rejected as wind evidence** | MCP-tool: hazards news links to nuclear/grid, not wind — caught by the VERIFY step |
| A "hurricane"-tagged Lake Placid (solar) article | **rejected** | MCP-tool: it was a *tornado* during Milton — classifier false positive, caught by VERIFY |

## Fixes applied (fail → fix)

- **iso filter empty (wind)** → switched to `state="TX"` + a coastal-county filter; confirmed ERCOT via `get_plant.grid` (iso="ercot"). (Baked into `prompt_projection` step 3 + `data_requirements`.)
- **classifier noise + non-wind links** → added an explicit **VERIFY step** + a required caveat ("classification verified, not on the label; links to nuclear/hydro, not wind"). Standing hazard-resource discipline.
- **CF temptation** → the CF series is reframed as **context that PROVES the storm is not separable** (the dip == the lull), with a required caveat + a blocked single-cause claim. This is the defining discipline of the resource.
- **cut-out/damage conflation** → forced a two-claim-type split in the mechanism + a required caveat; default to cut-out for sub-Cat-3.

## Gaps logged (→ `../../../docs/status/mcp_gaps.md`)

- **R1 (repeat, confirmed for wind)**: `search_plants(iso=…)` unwired beyond CAISO — now confirmed for ERCOT wind.
- **R12 (repeat + extended)**: no served TC / high-wind peril model (return-period / wind-field / EAL / $); + hazards news does NOT link to wind plants (needs hazards→wind linking); + monthly CF cannot resolve a cut-out (needs daily/hourly or an availability feed); + sparse `nearby_plants` for wind (R8/R10).

## Verdict

**PASS (directional, with an honestly lower ceiling than `hail_solar`).** The resource produces a grounded, caveated, properly-split-confidence insight that a vanilla LLM could not (it required the TX wind fleet aggregate, the EIA plant ids, the coastal-county geometry + turbine models, the NHC landfall fact, and the verified — and correctly *rejected-as-wind-evidence* — hazards classification). The standout discipline is **negative**: unlike hail (where the impact was *observable* in the CF series), here the substrate carries **no separable Beryl signal** for wind — the July dip is the summer lull, and the hazards news links to nuclear/hydro, not turbines. The resource therefore ships **exposure + mechanism at Medium**, frames Beryl as a **regional** event, and **blocks** the CF-attribution, the lasting-damage-from-a-Cat-1, the $, and the return-period. `grounding_maturity: model-not-wired`. The hazard pattern (substrate + hazards-news + VERIFY, ship directional, log the $ gap) holds; this run is the cautionary sibling that shows *when the realized-impact leg is genuinely absent*.
