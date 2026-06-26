# extreme_cold_winter_storm — Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets

> **Status**: draft, test 001 PENDING (2026-06-24). The **third `hazard`-domain resource** — the extreme-cold sibling of `hail_solar` and `hurricane_high_wind_wind`. Authored to match the live InfraSure MCP data structure; test 001 is the next step.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **extreme cold / winter storms × thermal (gas), wind, and solar assets** — who is exposed (Southern plains / Gulf Coast geography with a winterization gap), the mechanism (THREE fuel-specific claim types: wellhead freeze → gas curtailment → thermal outage; blade icing → wind shutdown; snow cover → solar reduction), what Winter Storm Uri (Feb 2021) meant regionally for the ERCOT fleet, and who should care. Directional + mechanism-grounded; the **dollar / EAL / forward-probability / per-plant-outage-attribution layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method (the THREE claim types; the winterization gap)
knowledge.md          the cited mechanism (A/B/C by fuel; winterization gap; Uri anchor; why CF can't show it)
historical_context.md the deeply researched event ledger (2011 Southwest · Uri · Elliott · Jan-2025)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (iso filter · no cold-weather peril model · CF too coarse)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the target output — ERCOT/TX thermal + Uri corridor (PENDING)
test_runs/test_run_001.md         the live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (TX gas/wind/solar fleet) ·
           NOAA NWS / NCEI / GHCN-Daily (freeze geography + event window + station temperature) ·
           FERC/NERC Uri report (regional event + outage scale) · ERCOT reports (system timeline) ·
           NOHRSC/SNODAS/IMS (snow/ice context) · hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ loss / EAL / payout · forward probability / return-period · per-plant outage attribution from CF ·
           plant winterization status without a named source · wind icing / solar snow-loss magnitude without sub-monthly data ·
           single-cause CF attribution (the Feb dip IS the seasonal minimum) · which specific wells/pipes froze ·
           national conclusions from one regional test
KEY FIND   like hurricane_high_wind_wind — the substrate carries NO separable per-plant storm signal; the February CF
           dip IS the seasonal minimum; Uri is a REGIONAL fact (FERC/NERC), not a substrate-grounded per-plant claim.
           The structural insight is the WINTERIZATION GAP (Southern-latitude plants without cold-weather packages) —
           that is the addressable vulnerability this resource illuminates.
```

## How it fits the hazard family

```text
hail_solar              the realized hail impact IS observable in the CF series → event-translation reachable at High
hurricane_high_wind_wind the realized cut-out is invisible at monthly CF + confounded by the summer lull → Medium ceiling
extreme_cold_winter_storm the forced outage is invisible at monthly CF + confounded by the winter seasonal minimum → Medium ceiling
                          BUT the SYSTEMIC, CORRELATED nature (all fuels simultaneously, across a region) + the FERC/NERC
                          regional record + the WINTERIZATION GAP structural story is what distinguishes this resource
```

## Next MCP test

```text
/test-resource extreme_cold_winter_storm "ERCOT/Texas gas fleet >=50 MW — Uri-class freeze exposure"
```

Run one region and one asset class first. Keep Uri as a regional factual mechanism unless the run has a named unit outage source; keep plant winterization status, wind-icing magnitude, and solar snow-loss magnitude blocked unless a named source provides the missing plant-level or sub-monthly data. Resolve the transcript into `test_runs/test_run_001.md` + `examples/applied_insight_001.md`.

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract + historical-context role discipline) · `historical_context.md` (event ledger) · `../hail_solar/` · `../hurricane_high_wind_wind/` (sibling hazard resources) · `../../docs/status/mcp_gaps.md`.
