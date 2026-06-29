# sea_level_rise_surge — Sea Level Rise & Storm Surge Exposure For Coastal Thermal, Nuclear, and Grid Assets

> **Status**: draft, manual test 001 PASS (2026-06-29, live MCP). The **seventh `hazard`-domain resource** — covering the coastal-inundation family alongside the sibling hazard resources. The WATER side of a coastal storm; the WIND side is `hurricane_high_wind_wind`. Test 001 anchored on South Texas Project (EIA 6251, Matagorda Co TX, 2,708.6 MW NUC, Constellation) — isolated from inland TX nuclear (Comanche Peak 6145, Matador 69798). Gap confirmed: no site-elevation field in the substrate.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **sea level rise + storm surge × coastal thermal, nuclear, grid, and offshore-wind-landfall assets** — who is exposed (tidewater siting of thermal/nuclear for cooling, low-lying coastal substations, offshore-wind landfall infrastructure), the mechanism across TWO timescales (chronic SLR raising the baseline and eroding the cooling-intake design basis vs acute surge inundating the switchyard/intake during a storm), what a realized surge meant regionally, and who should plan or harden. Directional + mechanism-grounded; the **dollar / decommissioning / inundation-year / surge-probability / inundation-depth layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml                      the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md                       the human-readable method (the chronic/acute split; tidewater cooling-siting concentration)
knowledge.md                      the cited mechanism (chronic SLR vs acute surge; tidewater siting; surge anchors)
prompt_projection.md              the pasteable session surface
data_requirements.md              the retrieval plan + known gaps (iso filter · no SLR/surge model · no site-elevation field · CF irrelevant)
SKILL.md                          the published, loadable skill
historical_context.md             cited frames + external evidence (Sandy Oct 2012; Katrina Aug 2005; SE FL tidewater nuclear chronic)
examples/applied_insight_001.md   validated output — South Texas Project (EIA 6251), Matagorda Co TX, chronic/acute split, Medium confidence
test_runs/test_run_001.md         live MCP test record — PASS 2026-06-29
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (TX coastal thermal/nuclear fleet) ·
           NOAA tide-gauge relative-SLR trends (chronic) · NHC SLOSH / FEMA VE zones (acute) ·
           hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ loss / EAL / decommissioning / payout · the inundation YEAR · forward surge probability ·
           inundation DEPTH (site elevation absent) · single-cause CF attribution · national-from-regional
KEY FIND   the substrate carries NO site-elevation field, so depth/year claims are blocked and exposure stays
           geographic/directional. The defining split is CHRONIC SLR (decades, uninsurable creep, planning horizon)
           vs ACUTE surge (hours, insurable event) — different horizons and financial logic. This is the WATER side
           of a coastal storm; the WIND side is hurricane_high_wind_wind — cross-reference, never double-count.
```

---

**See also**: `resource.yml` · `resource.md` · `prompt_projection.md` · `../hurricane_high_wind_wind/` (the WIND side) · `../flooding_multi_asset/` · sibling resources `../hail_solar/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../tornado_solar_wind/`, `../lightning_multi_asset/`, `../ice_storm_transmission/`.
