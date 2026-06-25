# Test Run 001 — Wildfire × CAISO California Solar Fleet + PSPS Curtailment (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `wildfire` resource.

## Test parameters

```text
Date:       TBD (execute next)
Scope:      CAISO / California solar fleet ≥ 50 MW
Events:     2020 CA wildfire season (smoke) + PG&E PSPS events (curtailment)
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. search_news(category=hazards, query="wildfire")               → verify in-substrate fire corroboration
2. search_news(category=hazards, query="PSPS")                   → verify in-substrate PSPS corroboration
3. search_plants(fuel="solar", state="CA", minMw=50)             → CAISO solar fleet
4. aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={state:"CA", fuel:"SUN"})
5. get_plant(<anchor_id>)                                         → geometry/county/fuel/owner (select a NorCal or Central Valley anchor)
6. get_plant(<anchor_id>).generation                              → monthly CF series (summer/fall 2020 window)
7. nearby_plants(<anchor_id>, fuel="solar")                      → same-geography fan-out
8. [optional] search_plants(fuel="wind", state="CA", minMw=50)  → wind fleet for PSPS curtailment picture
```

## Pass criteria

```text
✓ Fire geography established via NIFC / NOAA reference + verified hazards-news corroboration (or explicit note if absent)
✓ PSPS mechanism established via CAISO / utility reference (or directional note if absent from substrate)
✓ CA solar fleet resolved (state="CA", fuel="solar", minMw=50) with at least one anchor plant in a fire-weather-exposed county
✓ Mechanism (A) stated: smoke/ash → irradiance reduction + soiling — temporary, not structural damage
✓ Mechanism (C) stated: PSPS → curtailment of healthy generation — temporary revenue loss; fuel irrelevant; circuit location determines exposure
✓ Ignition liability (mechanism B, Camp Fire) noted as BLOCKED — model-gpr / legal
✓ Monthly CF used as context only, with explicit note that summer/fall CA dip cannot isolate smoke from seasonal irradiance variation
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
