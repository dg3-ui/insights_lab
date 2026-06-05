# Data Requirements - El Nino / ENSO Exposure

> **Status**: v0 checklist.
>
> **Purpose**: define what data the manual MCP/Claude test must retrieve or explicitly mark as missing.

## Required Inputs

| Input | Type | Needed For | Minimum V0 Standard |
|---|---|---|---|
| ENSO state / forecast | external | Establish condition | Source name, date/vintage, state or forecast |
| Region / market scope | substrate / logic | Limit test | One resolvable region or market |
| Plant/generator list | substrate | Asset scope | Operating solar assets in selected region |
| Capacity | substrate | Materiality filter | Recommended first threshold: >= 50 MW |
| Location / region fields | substrate | Region matching | Enough to justify inclusion in scope |
| Owner/company context | substrate / actor | Actor relevance | Owner/company name where available |

## Recommended Inputs

| Input | Type | Use |
|---|---|---|
| Seasonal outlook | external | Regional mechanism and caveats |
| Historical ENSO reference | external | Context for directional tendency |
| Generation / capacity factor | substrate | Optional performance context |
| Pricing / revenue context | substrate | Optional caveated market relevance |
| Offtaker / PPA context | actor | Optional commercial relevance |
| News facts | substrate | Optional corroborating context |
| Plant/company descriptions | descriptive | Framing only |

## Input Classification

```text
External methodology input
  NOAA CPC / ONI / seasonal outlook

Grounding substrate
  plant, generator, capacity, region, owner/company, generation, pricing

Descriptive context
  plant descriptions, Wikipedia summaries, external links

Actor context
  owner, developer, offtaker, PPA, company/account context

Logic layer
  filters, thresholds, region crosswalk, confidence rules
```

## First Test Retrieval Plan

For the first manual test, ask Claude to:

1. Identify the external ENSO state/source it needs.
2. Select or confirm one region/market.
3. Retrieve operating solar assets in that scope.
4. Filter to assets >= 50 MW if capacity is available.
5. Retrieve owner/company context for the scoped assets.
6. Retrieve offtaker/PPA context only if available through existing tools.
7. Draft the insight with explicit source refs and caveats.

## Missing Data Handling

| Missing Input | Required Action |
|---|---|
| ENSO source | Block the insight; cannot establish condition |
| Region cannot be resolved | Downgrade or switch to a resolvable region |
| Asset list unavailable | Block the insight; no scoped entity set |
| Owner/company unavailable | Draft asset-level claim only; actor relevance becomes generic |
| Offtaker unavailable | Omit offtaker relevance |
| Generation/pricing unavailable | Keep market/revenue implications directional and caveated |

