# Prompt Projection — Riverine Flood / Inland Inundation Exposure For Energy Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the riverine flood / inland inundation method below to draft **one grounded applied insight**.

Do not write a generic flood article. Do not draft outreach copy. Do not forecast exact flood depth, plant-level damage, $/EAL/PML, outage duration, return-period probability, or insurance outcomes.

## Task

Draft one riverine-flood exposure insight for one scoped inland energy asset set. Recommended first scope:

```text
Midwest / MISO region — gas or hydro plants >= 50 MW in Missouri, Iowa, or Illinois
near the Missouri or Mississippi River corridor.
Resolve via state= and fuel= filters; confirm grid/regions per plant.
```

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
heavy precipitation / snowmelt / ice-jam / dam release / levee / dam failure
   -> elevated river stage / channel overflow
   -> water reaches plant components: substations, cooling intakes, fuel systems,
      access roads, transmission corridors
   -> outage / damage / access loss depending on component elevation and event water surface
```

Riverine flood is **component- and elevation-specific**, not simply county-level proximity. A FEMA AE zone or a nearby gage in flood stage is a screen, not an inundation model.

## Required reasoning steps

```text
1. Establish flood condition: USGS NWIS gage stage + NOAA AHPS forecast (or post-event maps).
   Cite gage ID, issue date, and NWS flood category (Action / Minor / Moderate / Major).
   Add FEMA AE/AO zone context where available; label the map's effective date.
2. State the mechanism and the missing elevation bridge: plant/component elevation, event water
   surface, and verified damage/outage record mediate any site-level claim.
3. Resolve assets: search_plants(fuel=<gas|hydro>, state="<one state>", minMw=50).
   ⚠ Avoid iso=... unless verified (R1); scope by state then confirm grid/regions.
4. Drill get_plant for anchor plants: capacity, location (county/lat-lon), owner, grid/region,
   monthly generation context.
5. Use nearby_plants for co-located floodplain cluster context.
6. CONTEXT ONLY: monthly generation shows seasonality. Do NOT attribute a monthly dip to flooding
   without event-window outage data.
7. Check hazards news for realized flood events in the scoped geography; VERIFY classification
   and asset linkage before citing.
8. Retrieve owner / optional offtaker context for actor relevance.
9. Assemble: flood condition + scoped assets + mechanism + source refs + confidence + caveat +
   actor relevance.
10. Cap confidence at weakest link; block exact depth/$/EAL/outage duration/return-period/
    plant-level attribution.
```

## Allowed claims

- Directional riverine flood / inland inundation exposure for a scoped asset set near a named river reach
- Dated regional flood condition from USGS/AHPS (gage ID + date + flood category)
- FEMA AE/AO zone context (label map vintage)
- Mechanism statements for specific component pathways (cooling intake, substation, access, fuel)
- Realized-event regional framing from verified hazards news
- Owner / portfolio accumulation in a named basin or corridor
- Monitoring and hardening recommendations

## Blocked claims

- Exact site flood depth, inundation probability, EAL, PML, dollar loss, or insurance payout
- Exact outage duration / restoration curve after a flood event
- Plant-level generation attribution from monthly CF
- Equipment damage without a verified damage / outage record
- Stationary return-period claims from historical flood frequency
- Dam/levee failure probability without a named engineering/regulatory source
- National conclusions from one basin or corridor
- Outreach copy before validation

## Confidence rules

- **High** — not reachable: needs plant/component elevation, event inundation depth, verified outage/damage record
- **Medium** — USGS/AHPS stage current + basin-relevant, asset scope resolved, confirmed proximity to named river reach
- **Low** — default: county/state proximity screen only, no river-reach linkage or FEMA zone join
- **Blocked** — flood condition missing/stale, scope unresolved, or exact depth/$/outage/return-period requested

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part where flood-stage vs plant-exposure differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need... |
|---|---|
| `knowledge.md` | mechanism, hazard sub-types, FEMA zone taxonomy, data stack, non-stationarity |
| `historical_context.md` | major past riverine flood events and energy-infrastructure impacts |
| `examples/applied_insight_001.md` | target output shape |
| `data_requirements.md` | full retrieval plan + known tool gaps + missing-data handling |

---
name: riverine-flood
description: >-
  Draft a grounded riverine flood / inland inundation exposure insight for a scoped set of inland energy assets.
  Use when a user asks which plants, owners, regions, or offtakers face exposure to elevated river stages, floodplain
  inundation, snowmelt runoff, or dam/levee-area risk — e.g. "which Midwest gas plants are in a FEMA flood zone,"
  "river flood exposure for our MISO hydro fleet," or "what does spring flooding mean for assets along the Missouri
  River." Establishes flood condition from USGS streamflow gages and NOAA AHPS stage forecasts; adds FEMA riverine
  flood zone context; resolves the asset fleet via the InfraSure MCP; and produces a directional, caveated exposure
  claim. Never produces exact flood depth, plant-level inundation, $/EAL/PML, outage duration, return-period
  probability, dam/levee failure consequence, or plant-level generation attribution from monthly CF.
  Distinct from hurricane_coastal_flood (storm surge / ocean-driven water); this resource covers inland river
  corridor and floodplain exposure only.
---
