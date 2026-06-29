# flooding_multi_asset — Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets

> **Status**: draft, test 001 PENDING (2026-06-29). The **fifth `hazard`-domain resource** — covering the flood family alongside `hail_solar`, `hurricane_high_wind_wind`, `extreme_cold_winter_storm`, and `wildfire`. Authored to match the live InfraSure MCP data structure; test 001 targets the Gulf Coast / Texas floodplain.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **flood inundation × thermal, solar, wind, and grid assets** — who is exposed (coastal / riverine / FEMA-flood-zone geography, with water-sited thermal plants most exposed), the mechanism (THREE asset-specific claim types: switchyard/substation inundation → outage; fuel-storage/plant-equipment inundation → forced outage + damage; cooling-water-intake compromise at a water-sited thermal plant), what a realized flood meant regionally for assets in the watershed, and who should care. Directional + mechanism-grounded; the **dollar / EAL / forward-probability / per-plant-damage-attribution layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method (the THREE claim types; the elevation-not-in-substrate point)
knowledge.md          the cited mechanism (A/B/C by asset; water-sited thermal; flood-of-record anchors)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (iso filter · no flood model · no site-elevation field · CF too coarse)
SKILL.md              the published, loadable skill — TO AUTHOR
examples/applied_insight_001.md   the target output — Gulf Coast / TX thermal floodplain (PENDING)
test_runs/test_run_001.md         the live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (TX thermal/solar fleet) ·
           FEMA NFHL flood zones (flood geography) · NWS AHPS / USGS gauges (riverine crest history) ·
           hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ loss / EAL / payout · forward inundation probability / return-period · per-plant damage from CF ·
           single-cause CF attribution · which pads/feeders flooded (site elevation absent) ·
           national conclusions from one regional test
KEY FIND   like the sibling hazard resources — the substrate carries NO separable per-plant flood signal at monthly
           CF resolution, and crucially NO site-elevation field, so exposure stays geographic/directional. The
           structural insight is WATER-SITED THERMAL CONCENTRATION — plants placed at tidewater/riverbank for
           cooling are the addressable vulnerability this resource illuminates.
```

---

**See also**: `resource.yml` · `resource.md` · `prompt_projection.md` · sibling resources `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../sea_level_rise_surge/`.
