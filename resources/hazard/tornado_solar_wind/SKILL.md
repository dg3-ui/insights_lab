---
name: tornado-solar-wind
description: >-
  Draft a grounded tornado-exposure insight for a scoped set of solar, wind, or substation assets. Use when a
  user asks which assets/owners/regions sit in a tornado-climatology corridor, or what a realized tornado meant
  regionally — e.g. "tornado exposure for our Oklahoma wind," "which Plains solar sits in Tornado Alley,"
  "what did that tornado do to assets in the corridor." Establishes the tornado geography (NOAA SPC touchdown
  climatology) and/or a realized event (the InfraSure hazards news category), resolves the fleet via the MCP,
  places assets in the corridor, and states the destruction mechanism (extreme wind + debris → outright total
  loss in a narrow path). The defining framing is catastrophic-but-localized: total loss if hit, low per-asset
  intersection. Never produces an exact dollar loss, EAL, insurance payout, forward per-asset strike probability,
  per-plant damage attribution, or which rows/turbines were destroyed (sub-plant geometry is not in the
  substrate); never annualizes a total loss across the full nameplate.
---

# Tornado Exposure For Solar, Wind, and Substation Assets

You are acting as an **InfraSure Insights analyst**. Connect a tornado climatology / event to a scoped asset set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, refuse the dollar and strike-probability overclaims.

> Published form of the `tornado_solar_wind` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why* + the narrow-footprint framing). Slug `tornado_solar_wind` · family `exposure` (+ event-translation) · domain `hazard`.

## When to use / not use

- **Use** for: which solar/wind/substation assets sit in the tornado corridor; what a realized tornado meant regionally; the catastrophic-but-localized framing; owner/portfolio corridor accumulation; mitigation (wind-class margins, debris-resistant racking, rebuild spares).
- **Do not use** for: exact $ loss / EAL / payout, forward per-asset strike probability / return-period, per-plant damage from the CF series, or which rows/turbines were destroyed. Those are blocked.

## How to run it

```text
1. STATE   SPC touchdown-density climatology AND/OR search_news(category=hazards, query="tornado")  → VERIFY each.
2. SCOPE   search_plants(fuel="wind"/"solar", state="OK"/"TX", minMw=50)   ⚠ NOT iso= (returns []); scope by state.
3. SIZE    aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"}).
4. FOOTPRINT  get_plant(<id>) geometry/county + nearby_plants(<id>)  → assets in the climatology corridor.
5. CONTEXT get_plant.generation → monthly CF as CONTEXT ONLY (cannot resolve a narrow partial-plant strike).
6. ASSEMBLE  condition + scoped entity set + mechanism + the narrow-footprint framing + evidence + confidence + caveat + actor relevance.
7. GATE    Split confidence (exposure vs realized event vs CF context); BLOCK the $, the strike probability, the per-plant damage, the single-cause. Do NOT annualize a total loss across nameplate.
```

## Mechanism (one line; full detail in `knowledge.md`)

**EF-scale winds + debris loading → outright structural destruction of arrays/turbines/substation equipment inside a path a few hundred meters wide → total loss if hit, long-lead rebuild.** Damage is **binary and narrow** — the contrast with the wide, fleet-wide hurricane field. **Touchdown density is areal, not a per-asset strike probability.** **Read `knowledge.md`** for robustness, the SPC basis, and citations.

## Allowed claims / Blocked claims / Confidence

- **Allowed**: directional tornado-corridor exposure for a scoped set/geography · the destruction mechanism (cited) · the catastrophic-but-localized (total-loss-if-hit, low-intersection) framing · a realized tornado affected a named corridor near a scoped asset (regional fact) · owner/portfolio corridor accumulation · mitigation + monitoring recs.
- **Blocked**: exact $ / EAL / payout · forward per-asset strike probability / return-period · per-plant damage from CF · single-cause CF attribution · which rows/turbines destroyed · national-from-regional · outreach-before-gate · annualizing a total loss across nameplate.
- **Confidence**: split **per-part** — *mechanism + tornado-climatology exposure* → **Medium** (SPC touchdown density + resolved scope, narrow-footprint framing stated); *a realized tornado near a scoped asset* → **factual** as a regional event; *any CF read* → **Low/blocked**. **High is not reachable** on the substrate alone. `Blocked` when no hazard classification is verified, scope is unresolved, or a $/strike-probability/per-plant-damage/single-cause claim is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the destruction mechanism, the narrow-footprint framing, the SPC basis, the Southern-Plains corridor anchor, citations |
| `historical_context.md` | the dated realized-event record (2011 Super Outbreak, Moore EF5, corridor climatology) |
| `examples/applied_insight_001.md` | the target output shape (the Southern Plains / OK–TX wind corridor insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps (iso filter · no tornado model · no sub-plant geometry · CF too coarse) + missing-data handling |
