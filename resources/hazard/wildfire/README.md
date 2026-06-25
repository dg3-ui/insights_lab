# wildfire — Wildfire Exposure For Solar, Transmission, and Grid-Connected Assets

> **Status**: draft, test 001 PENDING (2026-06-25). The **fourth `hazard`-domain resource** — covering the wildfire family alongside `hail_solar`, `hurricane_high_wind_wind`, and `extreme_cold_winter_storm`. Authored to match the live InfraSure MCP data structure; test 001 targets the CAISO / California solar fleet.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **wildfire × solar, transmission, and grid-connected assets** — who is exposed (Western WUI / California fire-weather geography), the mechanism (THREE asset-specific claim types: smoke/ash → solar irradiance reduction + soiling; heat/flame → transmission corridor damage + ignition liability; PSPS → curtailment of otherwise-healthy generation), what realized events (Camp Fire 2018, 2020 CA fire season, PG&E PSPS events) meant regionally, and who should care. Directional + mechanism-grounded; the **dollar / ignition-liability / EAL / forward-probability / per-plant-smoke-attribution layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method (the THREE claim types; the PSPS detail)
knowledge.md          the cited mechanism (A/B/C by asset; PSPS in detail; Camp Fire / 2020 / PSPS anchors; why CF can't show smoke)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (iso filter · no fire-risk peril model · no PSPS circuit field · CF too coarse)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the target output — CAISO/CA solar + PSPS corridor (PENDING)
test_runs/test_run_001.md         the live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (CA solar/wind fleet) ·
           NIFC fire perimeters (fire geography) · NOAA NWS red-flag climatology (fire-weather exposure) ·
           CAISO PSPS records (curtailment events) · hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ ignition liability / structure loss / EAL / payout · forward ignition probability / return-period ·
           per-plant smoke-output attribution from CF · single-cause CF attribution (summer/fall CA dip ≠ smoke) ·
           whether a specific line caused / will cause ignition · national conclusions from one regional test
KEY FIND   like hurricane_high_wind_wind and extreme_cold_winter_storm — the substrate carries NO separable
           per-plant fire/smoke signal at monthly CF resolution. The most tractable mechanism is PSPS (C) —
           a CAISO / utility filing can corroborate which circuits were de-energized and when, making the
           curtailment claim more factually grounded than the smoke/output claim.
```

## The PSPS distinction — what makes this resource novel

Unlike other hazard resources, wildfire introduces a **grid-operator-driven curtailment mechanism (PSPS)** that creates a revenue loss for physically undamaged generators. This is the most analytically distinctive feature:

```text
hail_solar              physical damage → CF dip is observable in the substrate (High reachable for event-translation)
hurricane_high_wind_wind cut-out is invisible at monthly CF + confounded by the summer lull → Medium ceiling
extreme_cold_winter_storm forced outage invisible at monthly CF + confounded by the winter minimum → Medium ceiling
wildfire                 smoke reduction invisible at monthly CF + confounded by seasonal irradiance → Medium ceiling for (A)
                         BUT: PSPS curtailment is FACTUALLY VERIFIABLE via CAISO/utility filings → most grounded mechanism here
                         AND: ignition liability (Camp Fire) is a high-severity tail risk that is BLOCKED (model-gpr/legal)
```

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract + peril-field/non-stationarity standard) · `../hail_solar/` · `../hurricane_high_wind_wind/` · `../extreme_cold_winter_storm/` (sibling hazard resources) · `../../docs/status/mcp_gaps.md`.
