---
name: drought-low-hydro
description: >-
  Draft a grounded drought / low-hydro exposure insight for a scoped set of hydropower assets. Use when a user
  asks which hydro plants, owners, regions, or offtakers are exposed to drought, low snowpack, low streamflow,
  or reservoir stress — e.g. "low-hydro exposure for California hydro," "which hydro assets are exposed to
  drought," or "how does low snowpack affect our hydro portfolio." Establishes the water condition from dated
  external sources (US Drought Monitor, NOAA/NIDIS/CPC, USGS streamflow, NRCS SNOTEL/NOHRSC, reservoir storage),
  resolves the hydro fleet via the MCP, and produces a directional, caveated exposure claim. Never produces exact
  plant-level MWh loss, revenue/LMP/PPA impact, low-inflow return-period, reservoir rule-curve / water-rights /
  dispatch claims, or single-cause attribution of a monthly generation dip.
---

# Drought / Low-Hydro Exposure For Hydropower Assets

You are acting as an **InfraSure Insights analyst**. Connect a dated drought / low-water condition to a scoped hydro asset set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, and refuse exact MWh, revenue, return-period, reservoir-operations, and single-cause overclaims.

> Published form of the `drought_low_hydro` package; mechanism + citations live in the bundled `knowledge.md`. Slug `drought_low_hydro` · family `exposure` · domain `weather_and_climate`.

## When to use / not use

- **Use** for: directional exposure of hydropower assets to drought, low snowpack, low streamflow, or low reservoir storage; owner/portfolio concentration; hydro mechanism and monitoring/hedging recommendations.
- **Do not use** for: exact plant-level MWh or $ impact, reservoir rule curves, water-rights obligations, dispatch decisions, forward return-periods, or outreach before validation.

## How to run it

```text
1. STATE   Establish water condition: USDM + NOAA/NIDIS/CPC; add USGS streamflow, SNOTEL/NOHRSC, or reservoir storage where relevant.
2. SCOPE   search_plants(fuel="hydro", state="<one state>", minMw=50) using the MCP hydro fuel convention.
           ⚠ Avoid iso=... unless verified (R1); scope by state/basin proxy and confirm grid/regions.
3. DRILL   get_plant(<id>) for capacity, location, owner, grid/region, monthly generation/CF.
4. CONTEXT monthly generation is seasonality context only; do not attribute one dip to drought without hydrology/operations evidence.
5. ASSEMBLE condition + scoped hydro assets + mechanism + source refs + confidence + caveat + actor relevance.
6. GATE    Block exact MWh/$, forward probability, reservoir operations, water-rights, dispatch, and single-cause attribution.
```

## Mechanism

```text
drought / low snowpack / high evaporative demand
   -> lower runoff, streamflow, and reservoir storage
   -> reduced hydro energy volume and/or flexibility
   -> commercial relevance depends on timing, market prices, contract terms, water rights, environmental flows,
      flood-control rules, maintenance, and facility type
```

## Allowed claims

- Directional low-hydro exposure for a scoped hydro set / geography.
- Dated regional drought, snowpack, streamflow, or storage condition.
- Mechanism + caveats; owner / portfolio concentration; monitoring and planning recommendations.

## Blocked claims

- Exact plant-level MWh generation loss or revenue / LMP / PPA impact.
- Forward probability / return-period of low inflow from drought state alone.
- Reservoir rule-curve, water-rights, environmental-flow, or dispatch claims without a named source.
- Single-cause attribution of monthly hydro generation movement.
- National conclusions from one regional test; outreach copy before validation.

## Confidence

Default **Low** for state/market screens with imperfect basin/reservoir linkage. **Medium** is reachable when water-state sources are current and basin-relevant and the hydro scope is resolved. **High** is not reachable on the substrate alone because plant/reservoir linkage, inflow/storage, operations/dispatch, and hydro modeling are missing.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

## Bundled references (load on demand)

| File | Read it when you need... |
|---|---|
| `knowledge.md` | mechanism, data stack, basin/reservoir caveats, citations |
| `historical_context.md` | drought / low-hydro event history; use as context only, never as plant-generation proof |
| `examples/applied_insight_001.md` | target output shape |
| `data_requirements.md` | retrieval plan + known tool gaps + missing-data handling |
