# lightning_multi_asset — Lightning Exposure For Wind, Solar, and Electrical-Plant Assets

> **Status**: draft, test 001 PENDING (2026-06-29). The **eighth `hazard`-domain resource** — covering the lightning family alongside the sibling hazard resources. Authored to match the live InfraSure MCP data structure; test 001 targets the Gulf Coast / Florida–Texas flash-density maximum.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **lightning × wind, solar, and electrical-plant assets** — who is exposed (high cloud-to-ground flash-density geography, with tall wind turbines in open terrain most direct-strike-exposed), the mechanism (TWO claim types: direct strike to blade / nacelle / structure vs induced surge into inverters / transformers / control electronics across all generation), what a realized event meant regionally, and who should harden. The defining analytical point is **high-frequency / lower-per-event-severity** — cumulative component risk + design adequacy, not a single catastrophe. Directional + mechanism-grounded; the **dollar / EAL / strike-rate / per-plant-damage layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method (direct-strike vs induced-surge; the cumulative-component framing)
knowledge.md          the cited mechanism (direct strike vs induced surge; flash-density basis; design mitigation)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (iso filter · no strike-rate model · no LPS-status field · CF too coarse)
SKILL.md              the published, loadable skill — TO AUTHOR
examples/applied_insight_001.md   the target output — FL/TX wind flash-density band (PENDING)
test_runs/test_run_001.md         the live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/hub-height/owner) · search_plants/aggregate (FL/TX wind/solar fleet) ·
           NLDN cloud-to-ground flash-density climatology · hazards news (in-substrate corroboration, VERIFIED)
BLOCKED    $ loss / EAL / payout · forward strike rate / component-failure probability · per-plant damage from CF ·
           single-cause CF attribution · whether an asset's LPS is adequate (status absent) · national-from-regional
KEY FIND   unlike the catastrophe hazards, lightning is HIGH-FREQUENCY / LOWER-PER-EVENT-SEVERITY, managed by DESIGN
           (air termination / SPDs / grounding / blade receptors). The substrate carries NO LPS-status field and
           monthly CF cannot resolve a component strike, so the claim is geographic flash-density exposure framed as
           cumulative component risk + design adequacy — never a single-event catastrophe figure.
```

---

**See also**: `resource.yml` · `resource.md` · `prompt_projection.md` · sibling resources `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../flooding_multi_asset/`, `../tornado_solar_wind/`, `../sea_level_rise_surge/`, `../ice_storm_transmission/`.
