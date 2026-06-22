# Test Run 001 — Severe Hail Exposure, ERCOT/Texas Solar

> **Status**: 2026-06-14, **PASS** (with logged gaps). The manual MCP/Claude test record (`../../../docs/process/test_protocol.md`). This run authored + validated the `hail_solar` resource against live InfraSure MCP data. (Raw transcript = this session.)

## Question tested

> "Which ERCOT/Texas solar plants ≥ 50 MW are exposed to severe hail, and what did the realized Fighting Jays hailstorm mean for the asset and its owner?" — one region (TX/ERCOT) · one asset class (solar).

## What the model retrieved (the real call sequence)

```text
1. search_news(query="hail", limit=6)                         → hazards/hail articles; Fighting Jays (62945) event,
                                                                 details_json: hazard_type=hail, Fort Bend TX, damaged,
                                                                 event_date 2024-03-15/16  (also surfaced a FALSE positive:
                                                                 a "Struzzi hails decree" regulatory article — discarded)
2. search_plants(fuel="solar", state="TX", minMw=50, limit=100)→ the TX solar fleet (Tehuacana 1254.8 MW, Rowdy Creek 1050, …)
3. search_plants(fuel="solar", iso="ERCOT", minMw=50)          → []  (GAP: iso filter unwired — see Gaps)
4. aggregate(plants, group_by=state, metric=total_capacity, filter={fuel:SUN}) → TX 70,349.3 MW (#1; CA 36,843)
5. get_plant(62945)                                            → 227.5 MW AC single-axis c-Si; CIP owner; Fort Bend;
                                                                 monthly CF series; nearby solar
6. get_plant(62945).generation                                → OBSERVED post-event CF dip + 2025 recovery (the key signal)
7. nearby_plants via get_plant(62945).nearby                  → Cutlass II/I (66262/66310), Old 300 (64133) — same hail cell
```

## Accepted claims

- **Hail struck Fighting Jays (62945), Mar 2024** — *factual/high* (multi-source + in-substrate hazards classification, verified).
- **Observed ~57–60 % YoY CF drop post-event, recovering by mid-2025** — *medium* (observed, large, multi-season, time-aligned; not proven single-cause). e.g. Aug 2023 0.372 → Aug 2024 0.152 → Aug 2025 0.327.
- **TX = #1 solar fleet (70.3 GW / 378 plants) in the US hail maximum; ~744 MW more solar within ~9 km** — *low/medium* directional exposure + same-cell fan-out.
- Owner routing (CIP), mitigation (hail-stow), actor relevance — all grounded/cited.

## Rejected / downgraded claims

| Claim attempted | Disposition | Why (failure taxonomy) |
|---|---|---|
| "$X million in hail damage / EAL" | **blocked** | external-data: $ loss is model-gpr; news "multi-million-dollar" is a frame, not a modeled number |
| "N-year hail return-period at this site" | **blocked** | external-data: no served hail model; climatology alone has low forward skill |
| "Hail caused the entire CF decline" | **downgraded** → "consistent with" | method: single-cause not provable (curtailment/weather co-move CF) |
| "Texas solar will lose Y MWh next hail season" | **blocked** | method: plant-level forecast without a model |
| The "hails decree" regulatory article as a hail event | **rejected** | MCP-tool: hazards-classifier false positive — caught by the VERIFY step |

## Fixes applied (fail → fix)

- **iso filter empty** → switched to `state="TX"`; confirmed ERCOT via `get_plant.grid` / `.regions`. (Baked into `prompt_projection` step 3 + `data_requirements`.)
- **classifier false positive** → added an explicit **VERIFY step** to the procedure + a required caveat ("classification verified, not taken on the label"). This is the standing hazard-resource discipline.
- **single-cause temptation** → confidence split per-claim-part; "consistent with" language + a required caveat.

## Gaps logged (→ `../../../docs/status/mcp_gaps.md`)

- **R1 (repeat, confirmed for ERCOT)**: `search_plants(iso=…)` unwired beyond CAISO.
- **R12 (new)**: no served hazard peril-risk model (hail return-period / severity / EAL / $) — the directional-now-quantify-later wall; + hazards-classifier noise needs a VERIFY step.

## Verdict

**PASS.** The resource produces a grounded, caveated, properly-split-confidence insight that a vanilla LLM could not (it required the EIA plant_id, the monthly CF series, the hazards classification, the owner chain, and the fleet aggregate). The standout: the hail impact is **observable in the substrate generation series**, so the event-translation claim is *stronger than directional* — while the $ layer stays correctly blocked. The hazard pattern (substrate + hazards-news + VERIFY, ship directional, log the $ gap) is validated and ready to reuse for `hurricane_high_wind_wind`.
