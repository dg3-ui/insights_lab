# ice_storm_transmission — Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets

> **Status**: draft, manual test 001 PASS (2026-06-29, live MCP). The **ninth `hazard`-domain resource** — covering the ice-storm family alongside the sibling hazard resources. Test 001 anchored on Wagon Wheel Wind (EIA 69224, Logan Co OK, 598.4 MW, AEP/SWEPCO). Gap confirmed: no conductor/tower ratings or line geometry in the substrate; delivery-stranding framed from corridor + mechanism.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **ice storms × transmission, wind, and delivery-dependent assets** — who is exposed (the ice belt; transmission corridors and open-terrain wind most directly, all generation indirectly via delivery), the mechanism (THREE claim types: ice-load → conductor/tower mechanical failure on transmission, the primary hazard; blade icing → wind protective shutdown; distribution downing → otherwise-healthy generation stranded behind the break), what a realized ice storm meant for the grid regionally, and who should care. The defining analytical point is that this is **primarily a delivery-infrastructure hazard** — the loss is often grid-side, and a physically undamaged generator can lose revenue with no damage claim. Directional + mechanism-grounded; the **dollar / restoration-cost / ice-load-probability / per-span-or-plant layer is deliberately blocked** (model-gpr). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml                      the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md                       the human-readable method (three claim types; the delivery-infrastructure framing)
knowledge.md                      the cited mechanism (ice-load failure; blade icing; delivery stranding; ice-belt anchors)
prompt_projection.md              the pasteable session surface
data_requirements.md              the retrieval plan + known gaps (iso filter · no ice-load model · no conductor-rating field · CF too coarse)
SKILL.md                          the published, loadable skill
historical_context.md             cited frames + external evidence (Great Ice Storm 1998 Hydro-Québec; Dec 2007 OK; Jan 2009 Mid-South)
examples/applied_insight_001.md   validated output — Wagon Wheel Wind (EIA 69224), Logan Co OK, delivery-infrastructure framing, Medium confidence
test_runs/test_run_001.md         live MCP test record — PASS 2026-06-29
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/fuel/owner) · search_plants/aggregate (OK/TX/AR wind fleet + corridor) ·
           NOAA NWS freezing-rain climatology + SPIA ice-accumulation index · hazards news (VERIFIED)
BLOCKED    $ loss / restoration cost / payout · forward ice-load probability / return-period · per-span or per-plant
           attribution from CF · single-cause CF attribution · which spans/towers collapsed (line ratings absent) ·
           national conclusions from one regional test
KEY FIND   this is primarily a WIRES hazard, not a generation-equipment hazard — the loss is often grid-side and a
           healthy generator can be stranded behind a downed line with NO physical-damage claim. The substrate
           carries NO conductor/tower ratings or line geometry, so exposure stays geographic/directional. The
           generation-side freeze (gas wellhead/pipeline) lives in extreme_cold_winter_storm — cross-reference,
           never double-count.
```

---

**See also**: `resource.yml` · `resource.md` · `prompt_projection.md` · `../extreme_cold_winter_storm/` (the GENERATION-side freeze) · sibling resources `../hail_solar/`, `../hurricane_high_wind_wind/`, `../wildfire/`, `../flooding_multi_asset/`, `../tornado_solar_wind/`, `../sea_level_rise_surge/`, `../lightning_multi_asset/`.
