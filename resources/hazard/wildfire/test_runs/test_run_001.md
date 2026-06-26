# Test Run 001 — Wildfire × CAISO California Solar Fleet + PSPS Curtailment (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `wildfire` resource.

## Test parameters

```text
Date:       TBD (execute next)
Scope:      CAISO / California solar fleet ≥ 50 MW
Events:     2020 CA wildfire season (smoke context) + one dated utility PSPS event (curtailment)
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. external: NIFC / Cal Fire perimeter + USFS FSim/WHP or LANDFIRE screen → establish fire geography / fuel context
2. external: FIRMS / HRRR-Smoke (or equivalent dated smoke source)         → regional smoke context only
3. external: CPUC / utility / CAISO PSPS filing                            → dated PSPS event, circuit/county where disclosed
4. search_news(category=hazards, query="wildfire")                         → verify in-substrate fire corroboration
5. search_news(category=hazards, query="PSPS")                             → verify in-substrate PSPS corroboration
6. search_plants(fuel="solar", state="CA", minMw=50)                       → CA solar fleet (CAISO proxy)
7. aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={state:"CA", fuel:"SUN"})
8. get_plant(<anchor_id>)                                                   → geometry/county/fuel/owner/grid where available
9. get_plant(<anchor_id>).generation                                        → monthly CF series (context only)
10. nearby_plants(<anchor_id>, fuel="solar")                                → same-geography fan-out
11. [optional] search_plants(fuel="wind", state="CA", minMw=50)             → wind fleet for PSPS curtailment picture
```

## Pass criteria

```text
✓ Fire geography established via NIFC / NOAA reference + verified hazards-news corroboration (or explicit note if absent)
✓ PSPS mechanism established via CAISO / CPUC / utility reference (or directional note if absent from substrate)
✓ CA solar fleet resolved (state="CA", fuel="solar", minMw=50) with at least one anchor plant in a fire-weather-exposed county
✓ Mechanism (A) stated: smoke/ash → irradiance reduction + soiling — temporary, not structural damage
✓ Mechanism (C) stated: PSPS → curtailment of healthy generation — temporary revenue loss; fuel irrelevant; circuit location determines exposure
✓ Plant-specific PSPS curtailment asserted only if an external PSPS/circuit/interconnection record supports it; otherwise kept directional
✓ Ignition liability (mechanism B, Camp Fire) noted as BLOCKED — model-gpr / legal
✓ Monthly CF used as context only, with explicit note that summer/fall CA dip cannot isolate smoke from seasonal irradiance variation
✓ Smoke-loss magnitude blocked unless hourly/daily generation + irradiance/smoke data exist
✓ Confidence split per-part: fire-weather exposure + mechanism = Medium; fire/PSPS event = regional factual; CF read = Low/blocked; High = not reachable
✓ $ loss, ignition liability, forward probability, per-plant smoke attribution, and single-cause CF blocked in the output
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
