# Data Requirements — Hurricane Coastal Flood / Storm-Surge Exposure

> **Status**: draft 2026-06-25. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Sibling references: `../hurricane_high_wind_wind/data_requirements.md`, `../wildfire/data_requirements.md`.

## Input layers (by job — `../../../docs/method/data_map.md`)

```text
EXTERNAL    storm track / surge threat       -> NOAA NHC advisories / HURDAT2 / surge products        knowledge.md §3
EXTERNAL    flood-zone / elevation context   -> FEMA NFHL/FIS, NOAA SLOSH/P-Surge, tide gages, 3DEP    knowledge.md §3
SUBSTRATE   realized event corroboration     -> search_news(category=hazards, query=storm/flood/surge) (VERIFY)
KNOWLEDGE   component mechanism              -> knowledge.md §1, §4                          (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry       -> search_plants -> get_plant                    (scope + materiality)
SUBSTRATE   same-cluster fan-out             -> nearby_plants(anchor_id, fuel?)               (coastal cluster)
SUBSTRATE   generation monthly CF            -> get_plant.generation                          (context only)
ACTOR       owner chain                      -> get_plant.ownership                           (routes insight)
LOGIC       exposure screen                  -> coastal county / bay / floodplain + component caveat
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Storm / flood condition | external | establish condition | NHC storm/surge product, FEMA flood-zone context, SLOSH/P-Surge, tide gage, or local surge source |
| Asset scope | substrate | scoped entity set | one coastal geography + one primary asset class |
| Plant geometry / county | substrate | place near coast / floodplain | lat/lon + county/boundary where available |
| Capacity | substrate | materiality | MW |
| Component mechanism | knowledge | why water matters | cite `knowledge.md`; state component pathway |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA NHC / HURDAT2 / advisories | storm track, landfall, surge products | https://www.nhc.noaa.gov/ |
| NOAA SLOSH / P-Surge | scenario / probabilistic surge footprint | https://slosh.nws.noaa.gov/ |
| FEMA NFHL / FIS | regulatory flood zones and BFE context | https://msc.fema.gov/ |
| NOAA CO-OPS tide gauges | observed water level for realized events | https://tidesandcurrents.noaa.gov/ |
| USGS 3DEP / local lidar | elevation context where manually joined | https://www.usgs.gov/3d-elevation-program |
| Local / state surge studies | event- or region-specific context | cite source/date |

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:   cite NHC storm/surge product or local coastal-flood source for the selected geography.
2. FLOOD:   cite FEMA NFHL/FIS, SLOSH/P-Surge, tide gauge, or local elevation/surge study; record vintage/date.
3. EVENT:   search_news(category=hazards, query="<storm>" OR "storm surge" OR "coastal flood") -> VERIFY.
4. SCOPE:   search_plants(state="TX", county=<coastal county>, fuel=<one asset class>, minMw=50) if county supported,
            or search by state/fuel then drill coastal anchors. Avoid unscoped all-US scans.
5. ANCHOR:  get_plant(<anchor_id>) -> geometry/county/fuel/capacity/owner/monthly generation.
6. CLUSTER: nearby_plants(<anchor_id>, fuel=<same or relevant>) -> same coastal cluster / floodplain.
7. CONTEXT: get_plant.generation monthly CF -> context only; do not assert flood outage/damage from it.
8. DRAFT:   assemble; split confidence (regional flood state vs asset screen vs damage/outage); block exact depth/$/duration.
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| No plant elevation / flood-zone field | R15: substrate lacks elevation, surge, FEMA flood zone per plant | cite external FEMA/NOAA/local sources; caveat as screen | served flood-zone/elevation field |
| No component elevation / substation/pad location | inundation mechanism is component-specific | state mechanism; do not claim damage without record | component-level elevation / critical-asset layer |
| No served surge/inundation overlay | NHC/SLOSH/FEMA sources are external, not joined to plants | manually cite footprint/source; keep directional | geometry overlay / surge footprint tool |
| Monthly CF cannot resolve surge outage | storm outage can be days inside a month | use CF as context only | hourly/daily generation / outage feed (R20) |
| Hazards-news classifier noise | articles may cover load/customer outages, not plant damage | VERIFY title/details_json/fuel/affected_area | classifier precision + plant linking |

## Missing-data handling

| Missing input | Required action |
|---|---|
| No external storm/flood condition | **Block** — cannot establish condition |
| Asset scope unresolved | **Block** — no scoped entity set |
| No elevation/flood-zone context | keep coastal-county / proximity screen; confidence low |
| No damage/outage record | block equipment damage and outage duration claims |
| Owner unavailable | asset / regional claim only; do not infer |
| User asks for exact depth/$/insurance outcome | **Block** and name the missing model/data |
