# Test Run 001 — Drought / Low-Hydro × California Hydro Fleet (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `drought_low_hydro` resource.

## Test parameters

```text
Date:       TBD (execute next)
Scope:      California / CAISO hydro fleet >= 50 MW
Condition:  current dated drought / snowpack / streamflow / reservoir-storage state
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. external: US Drought Monitor + NOAA/NIDIS/CPC drought outlook          -> establish drought state and issue dates
2. external: USGS streamflow and/or NRCS SNOTEL / NOHRSC snowpack         -> basin-relevant water-state context
3. external: reservoir storage dashboard if a named reservoir is relevant -> storage context, not dispatch proof
4. search_plants(fuel="hydro", state="CA", minMw=50)                      -> California hydro fleet
   NOTE: adjust hydro fuel convention if MCP uses WAT/HYD/etc.; record exact filter used.
5. aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={state:"CA", fuel:<hydro>})
   if supported; otherwise record why not.
6. get_plant(<anchor_id>)                                                  -> geometry/county/capacity/owner/grid/generation context
7. get_plant(<anchor_id>).generation                                       -> monthly generation / CF seasonality context only
8. nearby_plants(<anchor_id>, fuel=<hydro>) or scoped fleet drilldown       -> nearby / regional hydro context if useful
```

## Pass criteria

```text
✓ Dated water condition established (USDM / NOAA-NIDIS-CPC, plus streamflow/snowpack/storage if used)
✓ Hydro fleet resolved in one geography, with exact MCP hydro fuel convention recorded
✓ At least one anchor plant drilled for capacity, location, owner, monthly generation context
✓ Mechanism stated: low snowpack/streamflow/storage -> lower hydro energy or flexibility, mediated by operations
✓ Monthly generation used only as seasonality context, not drought-causality proof
✓ Confidence split per-part: water state factual if current; fleet exposure low/medium; plant-level MWh/$ blocked
✓ Exact MWh, $, return-period, reservoir rule curve, water rights, dispatch, and single-cause claims blocked
✓ Actor relevance stated for >=2 actor types
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
