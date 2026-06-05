# Applied Insight Example - ENSO Exposure Target Shape

> **Status**: target shape only, not a validated test output.
>
> **Methodology reference**: `el_nino_enso_exposure@0.0.1-draft`.

## Claim

```text
If the current or forecast ENSO state is confirmed by the external source
used in the test, InfraSure can produce a directional exposure view for
the selected regional solar fleet. The claim should identify scoped assets
or owners, explain the regional mechanism, declare low/medium confidence,
and state that this is not a plant-level production or LMP forecast.
```

## Scope

| Field | Value |
|---|---|
| Entity scope | Operating solar assets resolved by MCP tools |
| Region / market | First test target: CAISO or nearest resolvable region |
| Capacity filter | Recommended: >= 50 MW |
| Time window | External ENSO source vintage/date from test |
| Actor | Owner/operator first; investor/lender/offtaker where context exists |

## Mechanism

ENSO state can influence regional weather, irradiance, precipitation, demand, and market conditions. For v0, the insight should focus on directional exposure from the ENSO condition to the selected solar fleet and avoid exact plant-level or market-price forecasts.

## Source References

| Source Type | Source | Entity / Scope | Field or Fact | Vintage / Date | Role |
|---|---|---|---|---|---|
| external | NOAA CPC or selected ENSO source | ENSO state / forecast | ENSO condition | To be filled during test | primary |
| substrate | InfraSure MCP/data tool | selected solar asset set | plant/generator list, capacity, region | To be filled during test | primary |
| substrate / actor_context | InfraSure MCP/data tool | owners/companies for scoped assets | owner/company context | To be filled during test | activation |
| actor_context | InfraSure MCP/data tool, if available | offtakers/PPAs for scoped assets | offtaker/PPA context | To be filled during test | activation |

## Confidence

| Claim Part | Confidence | Reason |
|---|---|---|
| ENSO condition exists | blocked until external source is cited | Must be grounded in current or explicitly dated source |
| Asset set is in scope | blocked until MCP data is cited | Requires resolved plant/generator scope |
| Directional exposure | low or medium | Depends on source quality and regional mechanism |
| Exact LMP or plant output | blocked | Outside v0 allowed claims |

## Caveats

- This is directional exposure, not a plant-level production forecast.
- ENSO teleconnections vary by region and season.
- Market implications depend on demand, hydro, congestion, marginal generation, and market structure.
- Actor relevance depends on owner, offtaker, contract, and portfolio context.

## Actor Relevance

| Actor | Why It Matters | Suggested Rendering |
|---|---|---|
| Owner / operator | Monitor seasonal operating variance and asset concentration | platform card, account note |
| Investor | Identify portfolio concentration and downside sensitivity | portfolio note |
| Lender | Watch financed assets for operational/revenue stress signals | account note |
| Offtaker | Understand linked supply exposure where PPA context exists | informative email draft after validation |

## Review Trace

| Review Item | Result |
|---|---|
| Claims supported by refs? | Pending test |
| Confidence declared? | Yes, but must be updated after test |
| Caveats present? | Yes |
| Overclaims blocked? | Exact LMP and plant-level forecasts blocked |
| Next fix | Run `test_runs/test_run_001.md` and replace placeholders with source-backed output |

