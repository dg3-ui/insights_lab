# Methodology Resource - El Nino / ENSO Exposure

> **Status**: v0 draft scaffold.
>
> **Resource slug**: `el_nino_enso_exposure`.
>
> **Purpose**: guide a model through directional exposure analysis that connects ENSO state or forecast to renewable assets, regions, owners, offtakers, and actor relevance.

## 1. Question Grammar

This resource is allowed to answer:

```text
Which assets, regions, owners, or offtakers are directionally exposed
to the current or forecast ENSO state?

Through what mechanism are they exposed?

What can InfraSure claim with confidence, and what must remain caveated?

Who should monitor the exposure, and why?
```

This resource is not allowed to answer:

```text
What exact LMP impact will ENSO cause?

What exact plant-level generation loss will occur?

Which accounts should receive an outreach email before the insight is validated?
```

## 2. Scope

| Scope Type | V0 Value |
|---|---|
| Entity types | plant, generator, company/owner, offtaker where available |
| Technologies | solar first; wind/hydro optional context only |
| Region / market | one selected market or region in the manual test |
| Lifecycle phase | operating assets first |
| Actors | owner/operator, investor, lender, offtaker |

Recommended first test:

```text
CAISO solar assets >= 50 MW
```

## 3. Mechanism

ENSO changes large-scale climate patterns. Those patterns can influence regional cloud cover, precipitation, temperature, demand, hydro conditions, wind patterns, and extreme-weather tendencies.

For v0, use a conservative chain:

```text
ENSO state / forecast
  -> regional weather or irradiance tendency
  -> affected solar asset or fleet scope
  -> owner / offtaker / portfolio exposure
  -> caveated market or revenue relevance
```

Do not turn this into a precise forecast. Treat the output as directional exposure unless a stronger data chain is available.

## 4. Required Inputs

| Input | Type | Required? | Use |
|---|---|---|---|
| ENSO state / forecast | external | required | Establish climate-regime condition |
| Seasonal outlook or historical ENSO reference | external | recommended | Support regional tendency and caveats |
| Plant locations and fuel/technology | substrate | required | Resolve asset scope |
| Capacity and operating status | substrate | required | Filter material assets |
| Owner/company context | substrate / actor | recommended | Identify who should care |
| Offtaker/PPA context | actor | optional | Identify commercial counterparties |
| Generation / capacity factor | substrate | optional | Add performance context if tool access supports it |
| Pricing / revenue context | substrate | optional | Add market relevance only as caveated context |
| Descriptive plant/company context | descriptive | optional | Frame the insight, not ground it |

## 5. Procedure

```text
1. Identify the current or forecast ENSO condition from the external source.
2. State the relevant regional mechanism and whether it is directional, statistical, or mechanistic.
3. Select one region/market and one asset class for the test.
4. Retrieve InfraSure substrate data for assets in scope.
5. Filter to material assets, recommended first threshold: solar >= 50 MW.
6. Retrieve owner/company and optional offtaker context.
7. Draft the claim using the claim grammar.
8. Attach source refs, confidence, caveats, and actor relevance.
9. Block or downgrade any claim that exceeds the evidence.
```

## 6. Allowed Claims

- Directional exposure claims for a scoped asset set.
- Mechanism statements linking ENSO to regional weather/irradiance/demand tendencies when supported by external sources.
- Asset, owner, offtaker, or portfolio relevance when grounded in InfraSure substrate.
- Caveated market or revenue implications when clearly marked as directional.
- Monitoring recommendations for owners, investors, lenders, or offtakers.

## 7. Blocked Claims

- Exact LMP forecasts from ENSO alone.
- Exact plant-level generation forecasts without plant-level resource/weather modeling.
- National conclusions from one regional test.
- Claims based only on generic climate commentary.
- Outreach copy before the applied insight is validated.
- Causal claims when the available evidence only supports correlation or direction.

## 8. Confidence Rules

| Confidence | Rule |
|---|---|
| High | Narrow mechanism, current source, resolved asset scope, and no downstream forecast claim |
| Medium | Regional tendency and asset scope are credible but one input/crosswalk is imperfect |
| Low | Scenario-based, directional, or dependent on external forecasts and incomplete regional mapping |
| Blocked | ENSO source missing/stale, asset scope unresolved, or claim asks for precise market/plant forecast |

## 9. Required Caveats

- Directional exposure is not a plant-level production forecast.
- ENSO teleconnections vary by region and season.
- Market-price effects depend on demand, hydro, congestion, marginal generation, and policy/market structure.
- Asset-level relevance depends on owner, offtaker, contract, and operating context.

## 10. Actor Relevance

| Actor | Why They Care | Rendering |
|---|---|---|
| Owner / operator | Monitor seasonal operating variance and asset concentration | platform card, account note |
| Investor | Identify portfolio concentration and downside sensitivity | platform card, portfolio note |
| Lender | Watch operational/revenue stress signals for financed assets | account note |
| Offtaker | Understand exposure in linked supply assets where PPA context exists | account note, informative email draft |

## 11. Staleness Signals

- NOAA/CPC ENSO status changes.
- Seasonal outlook changes materially.
- New plant/generator/owner/offtaker data lands.
- Region crosswalk changes.
- Pricing or generation substrate gains a better source for the scoped region.

## 12. Review Notes

The first manual test should tell us whether:

- the prompt projection is strict enough
- existing MCP tools can resolve the scoped assets and actors
- external ENSO source handling is clear enough
- the model overclaims market or plant-level impacts
- the applied-insight thin contract is sufficient for review

