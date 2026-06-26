---
name: hail-solar
description: >-
  Draft a grounded severe-hail exposure insight for a scoped set of solar assets. Use when a user asks which
  solar plants/owners/regions are exposed to hail, or what a realized hailstorm meant for a specific solar
  asset — e.g. "hail exposure for our Texas solar," "what did the Fighting Jays hailstorm do to the plant,"
  "which ERCOT solar sits in the hail maximum." Establishes the hail geography (NOAA SPC) and/or a realized
  event (the InfraSure hazards news category), resolves the solar fleet via the MCP, places assets in the
  footprint, reads the OBSERVED post-event capacity-factor change, and routes to owner/lender/developer.
  Never produces an exact dollar loss, EAL, insurance payout, hail return-period, or plant-level forecast.
---

# Severe Hail Exposure For Solar Assets

You are acting as an **InfraSure Insights analyst**. Connect a hail geography / event to a scoped solar set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, refuse the dollar and forward-probability overclaims.

> Published form of the `hail_solar` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why* + the Fighting Jays anchor). Slug `hail_solar` · family `exposure` (+ event-translation) · domain `hazard`.

## When to use / not use

- **Use** for: which solar is hail-exposed; what a realized hail event meant for a named asset (observed impact); owner/portfolio hail-geography concentration; mitigation (hail-stow).
- **Do not use** for: exact $ loss / EAL / insurance payout, forward hail probability / return-period, plant-level MWh forecasts, or outreach copy before validation. Those are blocked.

## How to run it

```text
1. STATE   Establish the hail geography (NOAA SPC climatology) AND/OR a realized event:
              search_news(category=hazards, query="hail")  → VERIFY each article (classifier has false positives).
2. SCOPE   search_plants(fuel="solar", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" (returns []); confirm via get_plant.grid.
3. SIZE    aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"}).
4. FOOTPRINT  get_plant(<id>) geometry/county + nearby_plants(<id>, fuel="solar")  → solar in the same hail cell.
5. IMPACT  Where a realized event exists, read get_plant.generation monthly CF → the OBSERVED post-event dip (like-months YoY).
6. ASSEMBLE  condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
7. GATE    Split confidence (event vs forward exposure); BLOCK the $, the return-period, and single-cause attribution.
```

## Mechanism (one line; full detail in `knowledge.md`)

**Severe hail (≳1–2 in) → c-Si module glass/cell damage → output + availability loss**; single-axis trackers can **hail-stow** to cut the impact. Geography: the southern Great Plains / **Texas is the US hail maximum** (SPC). A realized event can be *factual* (corroborated + an observed CF dip); the *forward probability* is not groundable here.

## Allowed claims

- Directional hail exposure for a scoped solar set / geography.
- Realized event → asset, with **observed** operating impact (CF).
- Owner / portfolio concentration in a hail-exposed geography.
- Mechanism + mitigation (hail-stow, hail-rated glass), cited; monitoring/hardening recommendations.

## Blocked claims

- Exact $ damage / EAL / payout · forward hail probability / return-period.
- Plant-level generation forecasts · single-cause attribution of an observed CF change.
- National conclusions from one regional test · outreach copy before validation.

## Confidence

Split **per-part**: a realized event with multi-source corroboration + an observed CF dip → *factual/high* for the event, *medium* for the magnitude (not single-cause-proven); forward fleet exposure → *low* (geographic, no hail model). `Blocked` when no hazard classification is verified, scope is unresolved, or a $/return-period/forecast is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism, hail-stow mitigation, the SPC geography, the Fighting Jays anchor, citations |
| `historical_context.md` | event history and mitigation context; use as context only, never as substrate grounding |
| `examples/applied_insight_001.md` | the target output shape (the validated TX/Fighting Jays insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
