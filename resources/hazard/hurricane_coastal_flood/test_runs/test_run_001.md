# Test Run 001 — Hurricane Coastal Flood × Texas Gulf Coast Energy Cluster (PENDING)

> **Status**: PENDING — this file will record the live MCP tool call sequence, results, and pass/fail verdict for the first manual test of the `hurricane_coastal_flood` resource.

## Test parameters

```text
Date:       TBD
Scope:      Texas Gulf Coast gas plants >= 50 MW (or one selected coastal asset class)
Condition:  dated NHC / FEMA / SLOSH / tide-gage / local surge source
Tester:     TBD
Model:      TBD
```

## Planned tool call sequence

```text
1. external: NHC storm track / surge product or local surge source       -> establish coastal-flood condition
2. external: FEMA NFHL/FIS, SLOSH/P-Surge, tide gage, or elevation source -> flood-zone / inundation context
3. search_news(category=hazards, query="<storm>" OR "storm surge" OR "coastal flood") -> verify event corroboration
4. search_plants(state="TX", fuel="<chosen>", minMw=50)                  -> scoped coastal fleet proxy
5. get_plant(<anchor_id>)                                                 -> geometry/county/capacity/owner/generation context
6. nearby_plants(<anchor_id>, fuel="<chosen or relevant>")                -> same coastal cluster
7. get_plant(<anchor_id>).generation                                      -> monthly CF context only
```

## Pass criteria

```text
✓ Dated external storm/flood condition established
✓ One coastal geography and one primary asset class resolved
✓ At least one anchor plant drilled for location, capacity, owner, and generation context
✓ Component pathway stated (substation, transformer, inverter pad, access, fuel/cooling, or interconnection)
✓ Monthly generation used only as context, not flood outage proof
✓ Confidence split per-part: regional flood source vs asset screen vs blocked exact damage/depth/$
✓ Exact flood depth, damage, outage duration, EAL/PML/$, and insurance outcome blocked
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

**See also**: `../examples/applied_insight_001.md` · `../data_requirements.md`.
