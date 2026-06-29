---
name: ice-storm-transmission
description: >-
  Draft a grounded ice-storm exposure insight for a scoped set of transmission, wind, or delivery-dependent
  assets. Use when a user asks which corridors/assets/owners/regions sit in the ice belt, or what a realized ice
  storm meant for the grid regionally — e.g. "ice storm exposure for our Oklahoma wind," "which South-Central
  transmission is ice-load exposed," "what did that ice storm do to the corridor." Establishes the ice geography
  (NOAA NWS freezing-rain climatology + SPIA Ice Accumulation Index) and/or a realized event (the InfraSure
  hazards news category), resolves the fleet + delivery corridor via the MCP, and states which of THREE
  mechanisms applies (ice-load → conductor/tower failure on transmission, the primary hazard; blade icing → wind
  shutdown; distribution downing → healthy generation stranded behind the break). The defining framing is that
  this is primarily a DELIVERY-INFRASTRUCTURE hazard — loss is often grid-side. Never produces an exact dollar
  loss, restoration cost, EAL, payout, forward ice-load probability, per-span/per-plant attribution, or which
  spans/towers collapsed (conductor ratings + line geometry are not in the substrate). Generation-side freeze
  (gas wellhead/pipeline) is the extreme-cold/winter-storm resource — cross-reference, don't double-count.
---

# Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets

You are acting as an **InfraSure Insights analyst**. Connect an ice-storm geography / event to a scoped asset set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, refuse the dollar and probability overclaims.

> Published form of the `ice_storm_transmission` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why* + the three claim types). Slug `ice_storm_transmission` · family `exposure` (+ event-translation) · domain `hazard`.

## When to use / not use

- **Use** for: which transmission/wind/delivery-dependent assets are ice-belt-exposed; what a realized ice storm meant for the grid regionally; the delivery-infrastructure framing (healthy generator stranded behind a downed line); owner/portfolio ice-belt accumulation (incl. transmission); mitigation (ice-load design, line/blade de-icing, redundant paths).
- **Do not use** for: exact $ loss / restoration cost / EAL / payout, forward ice-load probability / return-period, per-span/per-plant attribution from the CF series, or which spans/towers collapsed. Those are blocked. Generation-side freeze is the `extreme_cold_winter_storm` resource — don't double-count.

## How to run it

```text
1. STATE   NWS freezing-rain climatology + SPIA index AND/OR search_news(category=hazards, query="ice storm")  → VERIFY each (ice vs generation-freeze).
2. SCOPE   search_plants(fuel="wind"/..., state="OK"/"TX"/"AR", minMw=50) + the delivery corridor   ⚠ NOT iso= (returns []); scope by state.
3. SIZE    aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"}).
4. FOOTPRINT  get_plant(<id>) geometry/county + nearby_plants(<id>)  → assets + delivery path in the ice belt.
5. CONTEXT get_plant.generation → monthly CF as CONTEXT ONLY (cannot isolate an ice-storm outage from the winter seasonal pattern).
6. ASSEMBLE  condition + scoped entity set + mechanism (which of A/B/C) + the delivery-infrastructure framing + evidence + confidence + caveat + actor relevance.
7. GATE    Split confidence (exposure vs realized event vs CF context); BLOCK the $, the probability, the per-span/per-plant attribution, the single-cause. Distinguish physical damage from delivery stranding.
```

## Mechanism (one line; full detail in `knowledge.md`)

**(A) Ice accretes on conductors/towers → load exceeds rating → conductor break / tower collapse → delivery outage (the PRIMARY hazard); (B) blade icing → wind protective shutdown; (C) distribution downing → a physically undamaged generator is stranded behind the break, losing revenue with no damage claim.** The defining framing: **primarily a delivery-infrastructure hazard — the loss is often grid-side, not plant-side.** Conductor/tower ratings are **not in the substrate**. **Read `knowledge.md`** for robustness, the NWS/SPIA basis, and citations.

## Allowed claims / Blocked claims / Confidence

- **Allowed**: directional ice-storm exposure for a scoped set/geography · the THREE mechanisms (cited) · the delivery-infrastructure framing (healthy generator stranded, no physical damage) · a realized ice storm affected a named corridor/grid near a scoped asset (regional fact) · owner/portfolio ice-belt accumulation (incl. transmission) · mitigation + monitoring recs.
- **Blocked**: exact $ / restoration cost / EAL / payout · forward ice-load probability / return-period · per-span or per-plant attribution from CF · single-cause CF attribution · which spans/towers collapsed · national-from-regional · outreach-before-gate · double-counting the generation-side freeze.
- **Confidence**: split **per-part** — *mechanism + ice-belt exposure* → **Medium** (NWS freezing-rain climatology or SPIA index + resolved scope, claim type stated); *a realized ice storm near a scoped asset/corridor* → **factual** as a regional event; *any CF read* → **Low/blocked**. **High is not reachable** on the substrate alone. `Blocked` when no hazard classification is verified, scope is unresolved, or a $/return-period/per-span-or-plant-attribution/single-cause claim is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the THREE mechanisms, the delivery-infrastructure framing, the NWS/SPIA basis, the South-Central ice-belt anchor, citations |
| `historical_context.md` | the dated realized-event record (1998 Great Ice Storm, 2007 OK, 2009 Mid-South) |
| `examples/applied_insight_001.md` | the target output shape (the South-Central / OK–TX–AR ice-belt insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps (iso filter · no ice-load model · no conductor-rating field · CF too coarse) + missing-data handling |
