# Prompt Projection — Drought / Low-Hydro Exposure For Hydropower Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the drought / low-hydro method below to draft **one grounded applied insight**.

Do not write a generic drought article. Do not draft outreach copy. Do not forecast exact plant-level MWh, revenue, LMP, PPA, reservoir operations, or return-period impacts.

## Task

Draft one low-hydro exposure insight for one scoped hydropower asset set. Recommended first scope:

```text
California / CAISO hydro >= 50 MW
Resolve via state="CA" and hydro fuel convention; confirm grid/regions where available.
```

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
precipitation deficit / low snowpack / high evaporative demand
   -> lower runoff, streamflow, and reservoir storage
   -> reduced hydro energy volume and/or dispatch flexibility
   -> commercial relevance depends on timing, market price shape, contract terms, water rights,
      environmental flows, flood-control rules, maintenance, and facility type
```

Hydro exposure is **basin/reservoir-linked**, not simply state-linked. A state or market fleet is a screen.

## Required reasoning steps

```text
1. Establish the water condition:
   US Drought Monitor (map date/category) + NOAA/NIDIS/CPC drought outlook.
   Add USGS streamflow, NRCS SNOTEL/NOHRSC snowpack, or reservoir storage if relevant and dated.
2. State the mechanism and the missing operations bridge: reservoir storage, inflow, water rights,
   environmental flows, flood-control rules, and dispatch mediate plant-level generation.
3. Resolve assets: search_plants(fuel="hydro", state="CA", minMw=50) or the MCP hydro fuel convention.
   ⚠ Do not assume iso="CAISO" works (R1); scope by state, then confirm grid/regions where available.
4. Drill get_plant for anchor hydro plants: capacity, location, owner, grid/region, monthly generation/CF.
5. CONTEXT ONLY: monthly generation/CF shows hydro seasonality. Do NOT attribute a monthly dip to drought
   without basin/reservoir/operations evidence.
6. Retrieve owner / optional offtaker context for actor relevance + portfolio concentration.
7. Assemble: condition + scoped hydro assets + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block exact MWh/$/return-period/reservoir operations/single-cause attribution.
```

## Allowed claims

- Directional drought / low-hydro exposure for a scoped hydropower set / geography.
- Dated regional drought, snowpack, streamflow, or reservoir condition.
- Mechanism statements: low precipitation / snowpack / streamflow -> lower inflow/storage -> reduced hydro energy or flexibility.
- Owner / portfolio concentration in drought-exposed hydro geographies.
- Monitoring / hedging / planning recommendations.

## Blocked claims

- Exact plant-level MWh generation loss from drought.
- Exact revenue, LMP, PPA, or hedge impact from drought.
- Forward probability / return-period of low inflow from drought state alone.
- Reservoir rule-curve, water-rights, environmental-flow, or dispatch claims without a named source.
- Single-cause attribution of a monthly hydro generation dip.
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — not reachable on the substrate alone; needs plant/reservoir linkage, inflow/storage, operations/dispatch data, and a validated hydro model.
- **Medium** — current basin-relevant drought/snowpack/streamflow condition + resolved hydro scope, with a regional/directional claim only.
- **Low** — default for state/market hydro screens with imperfect basin/reservoir linkage.
- **Blocked** — water condition missing/stale, hydro scope unresolved, or a precise MWh/$/probability/reservoir-operation claim is requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part if water-state vs plant-impact differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need... |
|---|---|
| `knowledge.md` | the mechanism, source stack, basin/reservoir caveats, and non-stationarity discipline |
| `historical_context.md` | historical drought / hydro event ledger; context only, never substrate grounding |
| `examples/applied_insight_001.md` | the target output shape |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
