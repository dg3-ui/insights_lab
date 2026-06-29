---
name: riverine-flood
description: >-
  Draft a grounded riverine flood / inland inundation exposure insight for a scoped set of inland energy assets.
  Use when a user asks which plants, owners, regions, or offtakers face exposure to elevated river stages,
  floodplain inundation, snowmelt runoff, or dam/levee-area risk — e.g. "which Midwest gas plants are in a
  FEMA flood zone," "river flood exposure for our MISO hydro fleet," or "what does spring flooding mean for
  assets along the Missouri River." Establishes the flood condition from USGS streamflow gages and NOAA AHPS
  stage forecasts; adds FEMA riverine flood zone context; resolves the asset fleet via the InfraSure MCP;
  and produces a directional, caveated exposure claim. Distinct from hurricane_coastal_flood (storm surge /
  ocean-driven coastal water); this skill covers inland river corridor and floodplain exposure only. Never
  produces exact flood depth, plant-level inundation, $/EAL/PML, outage duration, return-period probability,
  dam/levee failure consequence, or plant-level generation attribution from monthly CF.
---

# Riverine Flood / Inland Inundation Exposure For Energy Assets

You are acting as an **InfraSure Insights analyst**. Connect a dated riverine flood condition to a scoped inland energy asset set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, and refuse exact flood depth, $/EAL/PML, outage duration, return-period, and plant-level overclaims.

> Published form of the `riverine_flood` package; mechanism + citations live in the bundled `knowledge.md`. Slug `riverine_flood` · family `exposure` · domain `hazard`.

## When to use / not use

- **Use** for: directional exposure of inland energy assets to riverine flooding, elevated river stages, floodplain proximity, or dam/levee-area risk; owner/portfolio accumulation; mechanism and monitoring/hardening recommendations.
- **Do not use** for: exact flood depth, plant-level inundation depth, $/EAL/PML, outage duration, return-period probabilities, dam/levee failure consequence, or outreach before validation.
- **Not the same as** `hurricane-coastal-flood`: that skill covers storm surge / ocean-driven coastal water. This skill covers inland river corridor and floodplain flooding only.

## How to run it

```text
1. CONDITION  Establish flood / river-stage condition: USGS NWIS gage stage + flood category +
              NOAA AHPS forecast. Cite gage ID, date, and NWS flood category.
              Add FEMA AE/AO zone context where available; label map vintage.
2. SCOPE      search_plants(fuel=<gas|hydro>, state="<one state>", minMw=50) using the MCP fuel convention.
              ⚠ Avoid iso=... unless verified (R1); scope by state/county and confirm grid/regions.
3. DRILL      get_plant(<id>) for capacity, location (county, lat/lon, river proximity), owner,
              grid/region, monthly generation/CF.
4. CLUSTER    nearby_plants(<anchor_id>) for floodplain co-location context.
5. NEWS       search_news for realized flood events; VERIFY classification + asset linkage.
6. CONTEXT    Monthly generation is seasonality context only; do not attribute a dip to flooding
              without event-window outage data.
7. ASSEMBLE   flood condition + scoped assets + mechanism + source refs + confidence + caveat + actor relevance.
8. GATE       Block exact depth/$/EAL/PML/outage duration/return-period and plant-level attribution.
```

## Mechanism

```text
heavy precipitation / snowmelt / ice-jam / dam release / levee / dam failure
   -> elevated river stage / channel overflow
   -> water reaches electrical equipment / cooling intakes / fuel systems /
      access roads / substations / transmission corridors
   -> outage / damage / access loss (component, elevation, and event water surface determine actual impact)
```

## Allowed claims

- Directional riverine flood / inland inundation exposure for a scoped asset set near a named river reach
- Dated regional flood condition from USGS/AHPS (gage ID + date + flood category)
- FEMA AE/AO zone context (label map vintage)
- Mechanism statements for specific component pathways
- Realized-event regional framing from verified hazards news
- Owner / portfolio accumulation in a named basin or corridor
- Monitoring and hardening recommendations

## Blocked claims

- Exact site flood depth, inundation probability, EAL, PML, dollar loss, or insurance payout
- Exact outage duration / restoration curve
- Plant-level generation attribution from monthly CF
- Equipment damage without a verified record
- Stationary return-period claims
- Dam/levee failure probability without a named source
- National conclusions from one basin
- Outreach copy before validation

## Confidence

Default **Low** for county/state screens with no river-reach linkage. **Medium** when USGS/AHPS stage is current + basin-relevant and asset scope is resolved with confirmed proximity to a named reach. **High** not reachable without component elevation, event inundation depth, and verified damage records.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

## Bundled references (load on demand)

| File | Read it when you need... |
|---|---|
| `knowledge.md` | mechanism, hazard sub-types, FEMA zone taxonomy, data stack, non-stationarity |
| `historical_context.md` | major past riverine flood events and energy-infrastructure impacts |
| `examples/applied_insight_001.md` | target output shape |
| `data_requirements.md` | retrieval plan + known tool gaps + missing-data handling |
