# tornado_solar_wind — Tornado Exposure For Solar, Wind, and Substation Assets

> **Status**: draft, manual test 001 PASS (2026-06-29, live MCP). The **sixth `hazard`-domain resource** — covering the tornado family alongside the five sibling hazard resources. Authored to match the live InfraSure MCP data structure; test 001 anchored on Traverse Wind Project (EIA 63479, Custer Co OK, 999 MW, AEP/SWEPCO).

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **tornadoes × solar, wind, and substation assets** — who is exposed (Tornado-Alley / Dixie-Alley climatology corridor), the mechanism (concentrated extreme winds + debris loading → outright structural destruction of arrays / turbines / substation equipment in a narrow path), what a realized tornado meant regionally, and who should care. The defining analytical point is **catastrophic-but-localized**: a strike is a total loss of the assets in the path, but the annual per-asset intersection probability is low — distinct from the fleet-wide derate hazards. Directional + mechanism-grounded; the **dollar / EAL / strike-probability / per-plant-damage layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml                      the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md                       the human-readable method (the destruction mechanism; the narrow-footprint framing)
knowledge.md                      the cited mechanism (EF-scale destruction; touchdown-density basis; corridor anchors)
prompt_projection.md              the pasteable session surface
data_requirements.md              the retrieval plan + known gaps (iso filter · no tornado model · no sub-plant geometry · CF too coarse)
SKILL.md                          the published, loadable skill
historical_context.md             cited frames + external evidence (2011 Super Outbreak; Moore EF5 2013; SPC corridor anchors)
examples/applied_insight_001.md   validated output — Traverse Wind (EIA 63479), Custer Co OK, SPC corridor, Medium confidence
test_runs/test_run_001.md         live MCP test record — PASS 2026-06-29
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (OK/TX wind/solar fleet) ·
           SPC tornado climatology (touchdown density) · hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ loss / EAL / payout · forward per-asset strike probability / return-period · per-plant damage from CF ·
           single-cause CF attribution · which rows/turbines destroyed (sub-plant geometry absent) ·
           national conclusions from one regional test
KEY FIND   unlike the wide, days-long hurricane field, a tornado is a NARROW point-strike total loss. The substrate
           carries NO per-asset strike probability (touchdown density is areal) and NO sub-plant geometry, so the
           claim is geographic intersection risk plus the catastrophic-but-localized framing — never an annualized
           derate across the full nameplate.
```

---

**See also**: `resource.yml` · `resource.md` · `prompt_projection.md` · sibling resources `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../flooding_multi_asset/`, `../lightning_multi_asset/`.
