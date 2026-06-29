# riverine_flood — Riverine Flood / Inland Inundation Exposure For Energy Assets

> **Status**: draft, test 001 PENDING (2026-06-25). A `hazard` resource extending the catalog from coastal-flood exposure into inland fluvial flooding. Authored as the next Wave-2 hazard package after `hurricane_coastal_flood`; test 001 targets the Midwest / MISO Missouri-Mississippi River corridor.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **riverine flooding / inland inundation × energy assets** — who is exposed, how elevated river stages and floodplain inundation affect plant components (cooling intakes, substations, access roads, fuel systems), what USGS/AHPS/FEMA data can and cannot support, and who should care. Directional + state-grounded; the **plant-level inundation depth / EAL / outage-duration / return-period layer is deliberately blocked** (`model-not-wired`).

## Positioning vs. `hurricane_coastal_flood`

| | hurricane_coastal_flood | riverine_flood |
|---|---|---|
| Driver | Storm surge / ocean wind-driven water | River stage overflow / precipitation / snowmelt / dam-levee failure |
| Geography | Coastal margins, bays, ship channels | Inland river corridors, floodplains, river-adjacent industrial clusters |
| External data | NHC, SLOSH/P-Surge, FEMA coastal | USGS NWIS, NOAA AHPS, FEMA riverine AE/AO, USACE NID |
| Key asset concern | Near-shore substations, coastal pads | Gas cooling intakes, hydro inflow, inland substations, transmission crossings |

Both share the component-elevation gap (R15/R24) and the same blocked-claim floor. Different packages because the driver, data stack, geography, and crosswalk differ.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · confidence_rules + blocked_claims)
resource.md           the human-readable method
knowledge.md          mechanism + hazard sub-types + FEMA zone taxonomy + data stack
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps
SKILL.md              the published, loadable skill
historical_context.md cited past riverine flood events and energy-infrastructure impacts
examples/applied_insight_001.md   target output — Midwest gas fleet (PENDING)
test_runs/test_run_001.md         live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    search_plants / get_plant (gas/hydro fleet, capacity, owner, location, generation context) ·
           USGS NWIS streamflow gages / NOAA AHPS stage forecasts (flood condition) ·
           FEMA NFHL riverine AE/AO zones (regulatory floodplain context)
BLOCKED    exact flood depth / inundation probability · $/EAL/PML/outage duration ·
           return-period probability · dam/levee failure consequence ·
           plant-level generation attribution from monthly CF
KEY CAVEAT riverine flood exposure is component- and elevation-specific, not simply county-level proximity.
           A FEMA AE zone or a nearby gage in flood stage is a screen, not an inundation model.
```

## New MCP gaps this package surfaces

| Gap | ID |
|---|---|
| No plant-to-river-reach / HUC / watershed linkage | R26 |
| No FEMA riverine flood zone join per plant | R27 |

Both logged to `../../../docs/status/mcp_gaps.md`.

## Next MCP test

```text
/test-resource riverine_flood "Midwest / MISO gas fleet >= 50 MW — Missouri or Mississippi River corridor flood exposure"
```

Run one state and one fuel class first. Keep exact depth/$/outage blocked; treat monthly generation as seasonality context only. Resolve the transcript into `test_runs/test_run_001.md` + `examples/applied_insight_001.md`.

---

**See also**: `../README.md` (the registry) · `../../../docs/method/resource_standard.md` · `../hurricane_coastal_flood/` (coastal-flood sibling) · `../../../docs/status/mcp_gaps.md` (R26, R27).
