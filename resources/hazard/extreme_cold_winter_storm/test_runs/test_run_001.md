# Test Run 001 — Extreme Cold / Winter Storm × ERCOT Texas Thermal Fleet (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `extreme_cold_winter_storm` resource.

## Test parameters

```text
Date:       TBD (execute next)
Scope:      ERCOT / Texas gas fleet ≥ 50 MW
Event:      Winter Storm Uri (February 10–20, 2021)
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. external: NOAA/NCEI Storm Events + GHCN-Daily station data               → event window + temperature anomaly
2. external: FERC/NERC Uri report                                           → regional mechanism + outage scale
3. external: ERCOT post-event / operating reports                           → system-level operating timeline
4. search_news(category=hazards, query="Uri")                               → verify in-substrate event corroboration
5. search_news(category=hazards, query="winter storm")                      → broader freeze news check
6. search_plants(fuel="gas", state="TX", minMw=50)                          → TX gas/thermal fleet (ERCOT proxy)
7. aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={fuel:"GAS", state:"TX"})
8. get_plant(<anchor_id>)                                                    → geometry/county/fuel/owner/grid where available
9. get_plant(<anchor_id>).generation                                         → monthly CF series (context only)
10. nearby_plants(<anchor_id>, fuel="gas")                                   → same-geography fan-out
11. [optional] search_plants(fuel="wind", state="TX", minMw=50)              → wind fleet for correlated picture
```

## Pass criteria

```text
✓ Event established via NOAA/FERC/NERC reference + verified hazards-news corroboration (or explicit note if absent)
✓ Gas fleet resolved (state="TX", fuel="gas", minMw=50) with at least one anchor plant in the freeze corridor
✓ Mechanism (A) stated: wellhead/pipeline freeze → gas curtailment → forced outage; Uri ~32 GW ERCOT (FERC/NERC)
✓ Monthly CF used as context only, with explicit note that Feb dip cannot isolate a Uri outage from the seasonal minimum
✓ Winterization gap named as the structural vulnerability
✓ Specific plant winterization status asserted only if a named source reports it; otherwise kept directional/unknown
✓ Wind icing / solar snow-loss magnitude blocked unless sub-monthly generation + weather/snow/icing data exist
✓ Confidence split per-part: exposure + mechanism = Medium; Uri = regional factual; CF read = Low/blocked; High = not reachable
✓ $ loss, return-period, per-plant attribution, and single-cause CF blocked in the output
✓ Actor relevance stated for ≥2 actor types
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

**See also**: `../examples/applied_insight_001.md` (the target output) · `../data_requirements.md` (the retrieval plan + known gaps).
