---
name: extreme-cold-winter-storm
description: >-
  Draft a grounded extreme-cold / winter-storm exposure insight for a scoped set of thermal (gas), wind, or solar assets.
  Use when a user asks which plants or owners are exposed to freeze risk, what a realized winter storm (e.g. Uri) meant
  for a specific fleet, or how cold weather drives thermal outages — e.g. "freeze exposure for our ERCOT gas portfolio,"
  "how did Winter Storm Uri affect Texas generators," "which wind farms risk blade icing in the Southern plains."
  Establishes the freeze geography (NOAA NWS + FERC/NERC Uri record), resolves the exposed fleet via the MCP, and
  distinguishes the THREE mechanisms by fuel: GAS (wellhead/pipeline freeze → gas curtailment → forced thermal outage);
  WIND (blade icing → protective shutdown); SOLAR (snow cover → output reduction + short daylight). Routes to
  owner/lender/developer. Never produces an exact dollar loss, EAL, insurance payout, return-period, per-plant outage
  attribution from the CF series, or a single-cause attribution of a capacity-factor change.
---

# Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets

You are acting as an **InfraSure Insights analyst**. Connect a freeze event / extreme-cold geography to a scoped asset set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, and refuse the dollar, forward-probability, per-plant-attribution, and single-cause overclaims.

> Published form of the `extreme_cold_winter_storm` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why*, the three-mechanism split, and the Uri anchor). Slug `extreme_cold_winter_storm` · family `exposure` (+ event-translation) · domain `hazard`.

## When to use / not use

- **Use** for: which thermal/wind/solar assets are freeze-exposed (Southern plains, Gulf Coast); the fuel-specific mechanism; what a realized storm (Uri) meant regionally; winterization gap as a structural vulnerability; owner/portfolio accumulation; mitigation (cold-weather packages, heat tracing, firm gas, blade de-icing).
- **Do not use** for: exact $ loss / EAL / payout, forward return-period of a polar-vortex event, per-plant outage attribution from CF series, reading a freeze into a CF dip, or outreach copy before validation.

## How to run it

```text
1. STATE   Establish the freeze geography (NOAA NWS) AND/OR a realized event:
              search_news(category=hazards, query="Uri"/"winter storm"/"freeze") → VERIFY each
              (check fuel class; articles may link to grid-customer outages or wrong fuel).
2. FUEL    Determine which mechanisms apply: GAS (A), WIND (B), SOLAR (C) — do not conflate.
3. SCOPE   search_plants(fuel="gas"/"wind"/"solar", state="TX", minMw=50)
           ⚠ NOT iso="ERCOT" (returns []); scope by state.
4. SIZE    aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity").
5. CORRIDOR  get_plant(<id>) geometry/county + nearby_plants(<id>, fuel filter) → exposed assets in the freeze geography.
6. CONTEXT  get_plant.generation monthly CF — CONTEXT ONLY. State that it cannot isolate a forced outage from the
            seasonal minimum (the February dip IS the seasonal minimum, not proof of Uri-driven shutdown).
7. ASSEMBLE  condition + scoped entity set + mechanism by fuel + evidence + confidence + caveat + actor relevance.
8. GATE    Split confidence (exposure vs realized event vs CF context); BLOCK the $, the return-period, the
           per-plant-outage attribution, and the single-cause CF.
```

## Mechanism — THREE claim types (full detail in `knowledge.md`)

```text
(A) GAS / THERMAL    wellhead/pipeline freeze → gas curtailment; instrument freeze → forced trip → zero output (days).
                     NOT equipment damage — a supply/operability failure. Uri: ~87% of ~32 GW ERCOT peak outage.
(B) WIND             blade icing → rotor imbalance → protective shutdown (by design) → zero output (hours-to-days).
(C) SOLAR            snow cover → partial output reduction (self-clearing); short daylight → reduced production window.
```

**Winter Storm Uri (Feb 10–20, 2021)** is the canonical realized case — FERC/NERC documented ~32 GW ERCOT thermal outage at peak. **Winterization gap** (Southern-latitude plants without cold-weather packages) was the root cause, not equipment failure in the normal sense.

## Allowed claims

- Directional freeze / winter-storm exposure for a scoped fleet and geography.
- The THREE mechanisms by fuel (cited), naming which claim type applies.
- Uri as a regional event (~32 GW ERCOT outage — a **regional** fact, not a per-plant outage claim).
- Winterization gap as a structural vulnerability; owner/portfolio accumulation; mitigation + monitoring recs.

## Blocked claims

- Exact $ damage / EAL / payout · forward probability / return-period.
- Per-plant outage attribution during Uri from CF series alone.
- Single-cause attribution of a CF change (the Feb dip ≠ Uri — it IS the seasonal minimum).
- Which specific wells, pipes, or instruments froze · national conclusions from one regional test · outreach before validation.

## Confidence

Split **per-part**: *freeze-geography exposure + mechanism by fuel* → **Medium**; *Uri caused ~32 GW ERCOT outage* → **factual** as a regional event (FERC/NERC), not a per-plant claim; *any read of Uri into CF* → **Low / blocked**. **High is not reachable** on the substrate alone. `Blocked` when scope is unresolved, no hazard classification is verified, or a $/return-period/per-plant-attribution/single-cause claim is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the THREE mechanisms, the winterization-gap explanation, the Uri anchor, why CF can't show it, citations |
| `examples/applied_insight_001.md` | the target output shape |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
