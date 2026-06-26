# Test Run 001 — Riverine Flood × Midwest / MISO Gas Fleet (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `riverine_flood` resource.

## Test parameters

```text
Date:       TBD (execute next)
Scope:      Midwest / MISO gas fleet >= 50 MW in one state (Missouri, Iowa, or Illinois)
            along the Missouri or Mississippi River corridor
Condition:  current or recent riverine flood / elevated river stage
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. external: USGS NWIS gage for Missouri or Mississippi River in scoped state
             -> establish stage condition, flood category, and gage date
2. external: NOAA NWS AHPS forecast for the scoped river / forecast point
             -> add forward flood outlook where current event is in scope
3. external: FEMA NFHL AE/AO zone for scoped county where available
             -> regulatory floodplain context; note map vintage
4. search_plants(fuel="gas", state="<MO|IA|IL>", minMw=50)
             -> Midwest gas fleet; record exact fuel convention used
             NOTE: try "NG" if "gas" returns empty; log whichever works
5. aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity",
             filter={state:<state>, fuel:<convention>})
             if supported; otherwise record why not
6. get_plant(<anchor_id>)   -> location/county/lat-lon, capacity, owner, grid/region, generation CF
7. get_plant(<anchor_id>).generation  -> monthly CF seasonality context only
8. nearby_plants(<anchor_id>, fuel=<gas>)  -> floodplain cluster context
9. search_news(state="<state>", subcategory or keyword=flood/riverine)
             -> realized event corroboration; VERIFY classification + asset linkage
```

## Pass criteria

```text
✓ Dated flood / river-stage condition established (USGS gage ID + date + NWS category)
✓ Gas fleet resolved in one state, with exact MCP fuel convention recorded
✓ At least one anchor plant drilled for location, capacity, owner, generation context
✓ Mechanism stated: elevated stage -> potential component inundation, with the elevation-bridge caveat
✓ Monthly generation used only as seasonality context, not flood-causality proof
✓ FEMA zone context included if accessible, with map vintage labeled
✓ Confidence split per-part: stage condition factual if current; proximity low/medium; inundation/damage blocked
✓ Exact depth, $, EAL, outage duration, return-period, and plant-level attribution blocked
✓ Actor relevance stated for >= 2 actor types
✓ Hazards news hits verified before citing
```

## Results (populate after execution)

```text
[tool call outputs and observations go here]
```

## Verdict

```text
[ ] PASS — directional, proceed to examples/applied_insight_001.md
[ ] PARTIAL — note gaps and conditions for pass
[ ] FAIL — describe what blocked the test and what to fix
```

---

**See also**: `../examples/applied_insight_001.md` (target output) · `../data_requirements.md` (retrieval plan + known gaps).
