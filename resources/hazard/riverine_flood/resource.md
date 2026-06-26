# Riverine Flood / Inland Inundation Exposure For Energy Assets

> **Status**: draft 2026-06-25. A `hazard` resource extending the catalog into inland fluvial flooding — the distinct inland complement to `hurricane_coastal_flood`. Test 001 targets the Midwest / MISO Missouri-Mississippi River corridor.

## What this is

A methodology package for reasoning about **riverine flooding × inland energy assets** — who is exposed, how elevated river stages and inundation affect plant components, what public flood-zone and gage data can and cannot support, and who should care. Directional + state-grounded; the **plant-level inundation depth / EAL / outage-duration / return-period layer is deliberately blocked** (`model-not-wired`).

## When to use / not use

- **Use** for: directional exposure of inland energy assets to riverine flooding, elevated river stages, floodplain proximity, or dam/levee-area risk; owner/portfolio accumulation; mechanism and monitoring/hardening recommendations.
- **Do not use** for: exact flood depth, plant-level damage, $/EAL/PML, insurance outcomes, outage duration, return-period probabilities, or dam/levee failure consequence modeling.

## Positioning vs. `hurricane_coastal_flood`

```text
hurricane_coastal_flood   driver = storm surge / ocean wind-driven water
                          geography = coastal margins, bays, ship channels
                          assets = coastal-belt solar/wind/gas/battery, near-shore substations

riverine_flood            driver = river stage overflow / precipitation / snowmelt / dam-levee failure
                          geography = inland river corridors, floodplains, river-adjacent industrial clusters
                          assets = gas plants with riverine cooling, hydro dams, inland substations,
                                   transmission corridors crossing river basins
```

Both share the component-elevation gap (R15/R24) and the same blocked-claim floor. They are distinct packages because the driver, external data stack, geography, and asset crosswalk are different.

## How to run it

```text
1. CONDITION  Establish flood / river-stage condition from USGS NWIS gage + NOAA AHPS stage forecast or
              post-event maps. Cite gage ID, date, and flood category.
              Add FEMA AE/AO zone context where available (label map vintage).
2. SCOPE      search_plants(state="<one state>", minMw=50) for a river-adjacent fuel class.
              ⚠ Avoid iso=... unless verified (R1); scope by state/county and confirm grid/regions.
3. DRILL      get_plant(<id>) for location, capacity, owner, fuel, monthly generation context.
4. CLUSTER    nearby_plants(<anchor_id>) for co-located floodplain assets.
5. NEWS       search_news for realized flood/riverine events affecting the scoped geography; VERIFY
              classification and asset linkage before citing.
6. CONTEXT    Monthly generation is seasonality context only; do not attribute a dip to flooding without
              event-window outage data.
7. ASSEMBLE   condition + scoped assets + mechanism + source refs + confidence + caveat + actor relevance.
8. GATE       Block exact depth/$/EAL/PML/outage duration/return-period and plant-level attribution.
```

## Mechanism

```text
heavy precipitation / snowmelt / ice-jam / dam release / levee / dam failure
   -> elevated river stage / channel overflow
   -> water reaches electrical equipment / cooling intakes / fuel systems /
      access roads / substations / transmission corridors
   -> outage / damage / access loss
   (component, elevation, and event water surface determine actual impact)
```

Flood × hydro is a special case: extreme inflow can force spillway operations or dam-safety constraints, causing outage *from too much water*, not just site inundation (see `knowledge.md §3`).

## Allowed claims

- Directional riverine flood / inland inundation exposure for a scoped asset set near a named river reach
- Dated regional flood / river-stage condition from USGS/AHPS, labeled with gage ID and date
- FEMA AE/AO flood zone context for a plant (label map vintage)
- Mechanism statements for specific component pathways (cooling intake, substation, access, fuel)
- Realized-event framing: a named flood affected a geography near scoped assets
- Owner / portfolio accumulation in a named river basin or floodplain corridor
- Monitoring / hardening recommendations

## Blocked claims

- Exact site flood depth, inundation probability, EAL, PML, dollar loss, or insurance payout
- Exact outage duration / restoration curve after a flood
- Plant-level generation attribution from monthly CF
- Asserting equipment damage without a verified record
- Stationary return-period claims from historical flood frequency
- Dam/levee failure probability without a named engineering/regulatory source
- National conclusions from one basin or corridor test
- Outreach copy before validation

## Confidence

Default **Low** for county/state proximity screens with no river-reach linkage or FEMA zone join. **Medium** is reachable when USGS/AHPS stage data is current and basin-relevant and the asset scope is resolved with a confirmed proximity to a named river reach. **High** is not reachable on the substrate alone because plant/component elevation, event inundation depth, and verified outage/damage records are missing.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

## Bundled references (load on demand)

| File | Read it when you need... |
|---|---|
| `knowledge.md` | mechanism, hazard sub-types, FEMA zone taxonomy, data stack |
| `historical_context.md` | past major riverine flood events and energy-infrastructure impacts |
| `examples/applied_insight_001.md` | target output shape |
| `data_requirements.md` | retrieval plan + known tool gaps + missing-data handling |

---

**See also**: `../README.md` (the registry) · `../../../docs/method/resource_standard.md` · `../hurricane_coastal_flood/` (coastal-flood sibling) · `../../../docs/status/mcp_gaps.md` (R26, R27).
