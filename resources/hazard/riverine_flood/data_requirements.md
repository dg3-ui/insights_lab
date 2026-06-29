# Data Requirements — Riverine Flood / Inland Inundation Exposure For Energy Assets

> **Status**: draft 2026-06-25. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Structural references: `../hurricane_coastal_flood/data_requirements.md` and `../extreme_cold_winter_storm/data_requirements.md`.

## Input layers (by job — `../../../docs/method/data_map.md`)

```text
EXTERNAL    flood / river-stage condition  -> USGS NWIS streamflow gages + NOAA NWS AHPS stage forecasts   knowledge.md §7
EXTERNAL    regulatory flood-zone context  -> FEMA NFHL riverine zones (AE/AO/AH) + FIS                    knowledge.md §4
EXTERNAL    dam / levee context            -> USACE NID + levee databases                                   knowledge.md §7
KNOWLEDGE   riverine mechanism + caveats   -> knowledge.md §1-6                               (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry     -> search_plants -> get_plant                     (fleet + materiality)
SUBSTRATE   generation monthly CF          -> get_plant.generation                           (context only)
SUBSTRATE   hazards news                   -> search_news (flood/riverine/dam events)         (verify before citing)
ACTOR       owner / optional offtaker       -> get_plant ownership / financial context         (routes the insight)
DESCRIPTIVE plant / county / river blurb   -> get_plant.context or external summary            (frames only)
LOGIC       materiality + proximity screen  -> >= 50 MW, one basin/reach, FEMA zone caveat     (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Flood / river-stage condition | external | establish the condition | USGS gage ID + stage date + NWS flood category, OR NOAA AHPS forecast point + issue date |
| Asset scope | substrate | scoped entity set | plants >= ~50 MW in one state / river basin |
| Plant location (lat/lon, county, state) | substrate | confirm proximity to river / flood zone | lat/lon + state/county where available |
| Capacity | substrate | materiality | plant MW |
| FEMA AE/AO zone context | external | regulatory floodplain screen | zone designation + map effective date |
| Monthly generation / CF | substrate | context only | context only; never single-cause attribution |
| Owner / company | substrate / actor | actor relevance | owner chain where available |
| Hazards news (flood events) | substrate | realized-event corroboration | verify classification + asset linkage before citing |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| USGS NWIS / WaterWatch | Streamflow gages + flood stage + percentiles | https://waterdata.usgs.gov/ · https://waterwatch.usgs.gov/ |
| NOAA NWS AHPS | River stage forecasts + flood categories by forecast point | https://water.weather.gov/ahps/ |
| FEMA MSC / NFHL | Riverine flood zones (AE/AO/AH) + FIS by county/state | https://msc.fema.gov/ |
| USACE NID | Dam inventory + hazard class + storage | https://nid.usace.army.mil/ |
| NOAA Atlas 14 | Precipitation frequency (design storm context) | https://hdsc.nws.noaa.gov/hdsc/pfds/ |

Every external state source must carry `as_of` / issue date / gage ID / map vintage. Do not use stale stage data or outdated flood-zone maps in a current applied insight without flagging the vintage.

## Retrieval plan (the real call sequence — test 001)

```text
1. CONDITION: pull USGS NWIS stage for a named gage on the Missouri or Mississippi River in the scoped state.
              Identify flood category from NWS flood stage thresholds (Action / Minor / Moderate / Major).
              Add NOAA AHPS forecast if a current or near-term event is in scope.
2. FEMA:      pull FEMA AE/AO zone designation for the scoped county/state if accessible; note map vintage.
3. SCOPE:     search_plants(fuel="gas", state="<MO|IA|IL>", minMw=50)  -> regional gas fleet (first test)
              ⚠ Adjust fuel label if MCP uses different convention (e.g. "NG"); record exact filter used.
              ⚠ Avoid iso="MISO" unless verified; R1 confirms ISO filters are unreliable.
4. HYDRO:     Optionally search_plants(fuel="hydro", state="<one state>", minMw=50) for hydro context.
5. SIZE:      aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity",
              filter={state:"<state>", fuel:"gas"}) if supported; otherwise sum drilled scope.
6. ANCHOR:    get_plant(<anchor_id>) -> location (lat/lon, county, river proximity), capacity, owner,
              grid/region, monthly generation/CF.
7. CLUSTER:   nearby_plants(<anchor_id>, fuel="gas") or fuel-agnostic -> floodplain cluster context.
8. NEWS:      search_news(state="<state>", subcategory="flood" or "riverine_flood") -> verified events;
              VERIFY asset/fuel linkage before citing.
9. CONTEXT:   read monthly generation/CF as seasonality context; explicitly block flood-causality attribution.
10. DRAFT:    assemble; split confidence (external flood/stage condition vs asset proximity vs plant-level impact);
              block exact depth/$/EAL/outage duration/return-period.
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| No plant-to-river-reach / HUC linkage | substrate has lat/lon + county, not a river-reach or HUC watershed join | use county/state proximity + external USGS gage geography; caveat as a screen | R26: serve HUC / river-reach IDs per plant |
| No FEMA flood zone join per plant | NFHL is not served as a substrate field | pull FEMA zone externally by county; caveat no site-specific join | R27: serve FEMA AE/AO zone flag per plant |
| `search_plants(iso=...)` unreliable | R1 confirmed for CAISO/ERCOT tests | scope by state or county; confirm grid/regions per plant | wire ISO / `resolve_region` |
| No component elevation data | same gap as R15/R24 (coastal flood) | ship directional; block exact inundation claims | R15/R24: serve component elevation |
| Monthly generation cannot prove flood causality | generation moves with dispatch, maintenance, weather | use monthly CF as context only | sub-monthly generation + outage records |
| Hazards news classifier noise | flood labels may not be event-specific or correctly attributed | VERIFY each news hit before citing (classification + asset linkage) | improved hazard classification confidence scores |

Also log new recurring gaps to `../../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No dated flood / river-stage condition | **Block** the condition; cannot make a current riverine-flood exposure claim |
| Asset scope cannot be resolved | **Block** — no scoped entity set |
| No FEMA zone / river-reach linkage | keep county/state proximity screen; confidence low; caveat prominently |
| Monthly generation unavailable | no loss; keep directional exposure + external flood condition |
| Owner unavailable | asset / region-level claim only; do not infer owner |
| User asks for exact flood depth / $/EAL / outage duration / return-period | **Block** and explain model/data requirement |
| Hazards news hit unverifiable | do not cite; note gap in Gaps section |
