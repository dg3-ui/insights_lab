# drought_low_hydro — Drought / Low-Hydro Exposure For Hydropower Assets

> **Status**: draft, test 001 PENDING (2026-06-25). A `weather_and_climate` resource extending the catalog from solar weather exposure into hydroclimate exposure. Authored as the next Wave-2 package after `wildfire` and `extreme_cold_winter_storm`; test 001 targets California / CAISO hydro.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **drought / low snowpack / low streamflow × hydropower** — who is exposed, how low-water conditions affect hydro energy and flexibility, what public drought / snowpack / streamflow state can and cannot support, and who should care. Directional + state-grounded; the **plant-level MWh / revenue / reservoir-operation / return-period layer is deliberately blocked** (`model-not-wired`).

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · confidence_rules + blocked_claims)
resource.md           the human-readable method
knowledge.md          the mechanism + public data stack + basin/reservoir caveats
historical_context.md historical low-hydro event ledger (CA drought · Colorado River)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the target output — California hydro drought screen (PENDING)
test_runs/test_run_001.md         the live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    search_plants / get_plant (hydro fleet, capacity, owner, location, monthly generation context) ·
           US Drought Monitor / NOAA-NIDIS-CPC (drought state) · USGS streamflow · NRCS SNOTEL / NOHRSC snowpack ·
           reservoir storage dashboards where relevant
BLOCKED    exact plant-level MWh / $ / LMP / PPA impact · forward low-inflow probability / return-period ·
           reservoir rule-curve / water-rights / dispatch claims · single-cause attribution of monthly generation
KEY FIND   hydro exposure is basin/reservoir-linked, not just state-linked. A state/market hydro fleet is a useful
           first screen, but exact plant impact needs plant-to-basin/reservoir linkage and hydro operations data.
```

## Next MCP test

```text
/test-resource drought_low_hydro "California / CAISO hydro >=50 MW — drought and low-water exposure"
```

Run one region and one asset class first. Keep exact generation/revenue impact blocked; treat monthly generation as seasonality context; only make basin/reservoir-specific claims when the run includes a named USGS/SNOTEL/reservoir source linked to the scoped assets. Resolve the transcript into `test_runs/test_run_001.md` + `examples/applied_insight_001.md`.

---

**See also**: `../README.md` (the registry) · `../../../docs/method/resource_standard.md` (the contract + non-stationarity standard) · `../el_nino_enso/` · `../extreme_heat_derate/` (sibling weather resources) · `../../../docs/status/mcp_gaps.md`.
