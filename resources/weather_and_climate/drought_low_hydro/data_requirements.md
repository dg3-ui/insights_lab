# Data Requirements — Drought / Low-Hydro Exposure For Hydropower Assets

> **Status**: draft 2026-06-25. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Structural references: `../el_nino_enso/data_requirements.md` and `../extreme_heat_derate/data_requirements.md`.

## Input layers (by job — `../../../docs/method/data_map.md`)

```text
EXTERNAL    drought condition             -> US Drought Monitor + NOAA/NIDIS/CPC drought outlooks       knowledge.md §3
EXTERNAL    streamflow / snowpack state    -> USGS streamflow + NRCS SNOTEL / NOHRSC / SNODAS            knowledge.md §3
EXTERNAL    reservoir storage              -> USBR / state reservoir dashboards where relevant           knowledge.md §3
KNOWLEDGE   hydro mechanism + caveats      -> knowledge.md §1-4                              (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry     -> search_plants -> get_plant                    (hydro fleet + materiality)
SUBSTRATE   generation monthly CF          -> get_plant.generation                          (seasonality context only)
ACTOR       owner / optional offtaker       -> get_plant ownership / financial context        (routes the insight)
DESCRIPTIVE basin / plant blurb            -> get_plant.context or external public blurb      (frames only)
LOGIC       materiality + basin caution     -> >=50 MW, one geography, basin/reservoir caveat (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Drought condition | external | establish the condition | USDM category + map date or NOAA/NIDIS/CPC dated outlook |
| Hydro plant scope | substrate | scoped entity set | hydro plants >= ~50 MW in one state/market/basin |
| Plant geometry / state / region | substrate | place assets in drought-exposed geography | lat/lon + state/county/grid/region where available |
| Capacity | substrate | materiality | plant MW |
| Monthly hydro generation / CF | substrate | seasonality context | context only; never single-cause attribution |
| Streamflow / snowpack / reservoir state | external | strengthen basin relevance | USGS gage, SNOTEL basin, NOHRSC/SNODAS, or reservoir dashboard dated |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| US Drought Monitor | weekly drought category | https://droughtmonitor.unl.edu/ |
| NOAA / NIDIS Drought.gov | drought status + impacts + outlook links | https://www.drought.gov/ |
| NOAA CPC drought outlooks | persistence / development | https://www.cpc.ncep.noaa.gov/ |
| USGS NWIS / WaterWatch | streamflow gages + percentiles | https://waterdata.usgs.gov/ |
| NRCS SNOTEL / Water and Climate Center | SWE / snowpack basin percentiles | https://www.nrcs.usda.gov/wps/portal/wcc/home/ |
| NOAA NOHRSC / SNODAS | snow analysis / modeled snowpack | https://www.nohrsc.noaa.gov/ · https://nsidc.org/data/g02158 |
| Bureau of Reclamation / state dashboards | reservoir storage where relevant | https://www.usbr.gov/ |

Every external state source must carry `as_of` / issue date / access date. Do not use stale drought categories in a current applied insight.

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:   pull USDM map date/category for California (or selected basin); add NOAA/NIDIS/CPC drought outlook.
2. HYDRO:   pull USGS streamflow, NRCS SNOTEL/NOHRSC snowpack, or reservoir storage for the relevant basin
            if a basin/reservoir anchor is known. If not, keep the claim at state-level directional exposure.
3. SCOPE:   search_plants(fuel="hydro", state="CA", minMw=50)  -> CA hydro fleet (first test)
            ⚠ If fuel label differs (e.g. WAT/HYD), use the repo/MCP's hydro fuel convention from search results.
            ⚠ Avoid iso="CAISO" unless verified; R1 says ISO filters are unreliable.
4. SIZE:    aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={state:"CA", fuel:"hydro"})
            if aggregate supports the fuel convention; otherwise sum drilled scope cautiously.
5. ANCHOR:  get_plant(<anchor_id>) -> location, capacity, owner, grid/region, monthly generation/CF.
6. CONTEXT: read monthly generation/CF as seasonality context; explicitly state it cannot prove drought causality.
7. FANOUT:  nearby_plants(<anchor_id>, fuel="hydro") or other scoped hydro list -> portfolio / regional context.
8. DRAFT:   assemble; split confidence (external water state vs hydro fleet exposure vs plant-level impact);
            block exact MWh/$/return-period/reservoir operations/single-cause attribution.
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| Hydro fuel convention may differ | MCP may use `WAT`, `hydro`, `HYC`, or another internal fuel code | inspect search results / existing substrate convention; state the filter used | documented fuel taxonomy / alias resolver |
| `search_plants(iso=...)` unreliable | R1 confirmed for CAISO/ERCOT tests | scope by state or basin proxy; confirm grid/regions per plant | wire ISO / `resolve_region` |
| No plant-to-basin / reservoir linkage | hydro exposure is watershed/reservoir-linked, not just state-linked | use external basin/reservoir sources manually; caveat state scope as screen | served watershed/reservoir IDs per hydro plant |
| No reservoir inflow/storage/rule-curve data in substrate | exact generation depends on operations and non-power constraints | ship directional; block exact MWh/$ and operations claims | hydro operations / reservoir module |
| Monthly generation cannot prove drought causality | generation moves with seasonality, dispatch, maintenance, water obligations | use monthly CF as context only | sub-monthly hydro generation + inflow/storage join |
| No water-rights / environmental-flow obligations | non-power constraints may dominate hydro dispatch | name as caveat; do not infer | served water-rights / operating constraints where public |

Also log new recurring gaps to `../../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No dated drought / streamflow / snowpack / reservoir state | **Block** the condition; cannot make a current low-hydro claim |
| Hydro fleet cannot be resolved | **Block** — no scoped entity set |
| Basin/reservoir linkage unavailable | keep state/market-level screen; confidence low; do not make basin-specific plant claims |
| Monthly generation unavailable | no loss; keep directional exposure + external water state |
| Owner unavailable | asset / region-level claim only; do not infer owner |
| User asks for exact MWh/$/return-period | **Block** and explain model/data requirement |
