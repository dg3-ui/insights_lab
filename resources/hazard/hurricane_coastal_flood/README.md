# hurricane_coastal_flood — Hurricane Coastal Flood / Storm-Surge Exposure

> **Status**: draft, test 001 PENDING (2026-06-25). A `hazard` resource covering hurricane storm-surge / coastal-flood exposure for coastal energy assets. It is the water-mechanism sibling of `hurricane_high_wind_wind`.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **hurricane coastal flood / storm surge × energy infrastructure** — who is exposed, what component pathway water affects, how to use public surge/flood sources, and what must stay blocked. Directional + geography-grounded; exact site depth, component damage, outage duration, EAL/PML, and $ remain `model-not-wired`.

## Files

```text
resource.yml          structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           human-readable method
knowledge.md          mechanism + public data stack + wind-vs-water caveat
historical_context.md event ledger (Sandy · Harvey) for coastal-flood component pathways
prompt_projection.md  pasteable session surface
data_requirements.md  retrieval plan + known gaps
SKILL.md              loadable skill
examples/applied_insight_001.md   target output — Texas Gulf Coast energy cluster (PENDING)
test_runs/test_run_001.md         live MCP test record (PENDING)
```

## Grounding at a glance

```text
GROUNDS    get_plant / nearby_plants (coastal asset cluster, capacity, owner, location) · NHC track/surge ·
           FEMA NFHL/FIS · SLOSH/P-Surge · NOAA tide gages · local surge studies · hazards news (VERIFIED)
BLOCKED    exact site flood depth · EAL/PML/$/insurance payout · outage duration · equipment damage without record ·
           monthly-CF attribution · wind-vs-water coverage outcome
KEY FIND   coastal flood exposure is elevation- and component-specific. Plant county/lat-lon is a screen, not an
           inundation model; the future upgrade is served elevation/flood-zone/surge overlay + component data.
```

## Next MCP test

```text
/test-resource hurricane_coastal_flood "Texas Gulf Coast gas plants >=50 MW — storm-surge / coastal-flood exposure"
```

Run one coastal geography and one asset class first. Keep exact water depth, outage duration, and $ blocked. Resolve the transcript into `test_runs/test_run_001.md` + `examples/applied_insight_001.md`.

---

**See also**: `../README.md` (registry) · `../../../docs/method/resource_standard.md` · `../hurricane_high_wind_wind/` · `../wildfire/` · `../../../docs/status/mcp_gaps.md`.
