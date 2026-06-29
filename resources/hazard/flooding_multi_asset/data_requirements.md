# Data Requirements — Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets

> **Status**: draft 2026-06-29. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`; sibling: `../hurricane_high_wind_wind/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    flood geography + event   -> FEMA NFHL + NOAA NWS AHPS / USGS gauges + hazards news (pull live, dated)   knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                                                               (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant (geometry/county/fuel)                           (grounds the claim)
ACTOR       owner / company           -> get_plant.ownership / plants_by_owner                                       (routes the insight)
DESCRIPTIVE blurb / context           -> get_plant.context                                                          (frames only — never grounds)
LOGIC       materiality, flood-zone   -> >=50 MW cut · in/out of NFHL zone · water-sited thermal flag              (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Flood geography / event state | external | establish the condition | FEMA NFHL zone OR NWS/USGS gauge history OR a VERIFIED hazards-news flood article + access date |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (which of A/B/C) |
| Region / market scope | substrate / logic | bound the test | one resolvable region (test 001 = Gulf Coast / TX) |
| Plant / generator list | substrate | asset scope | operating (+ queue) ≥ 50 MW in scope |
| Geometry / county | substrate | place in/out of the floodplain | lat/lon + county from `get_plant` |
| Owner / company | substrate / actor | actor relevance | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| FEMA NFHL | flood-zone geography (100/500-yr) near the asset | https://msc.fema.gov/ |
| NOAA NWS AHPS + USGS gauges | riverine crest forecast + flood-of-record history | https://water.weather.gov/ · https://waterdata.usgs.gov/ |
| InfraSure hazards news | in-substrate realized-event corroboration | `search_news(category=hazards, query="flood")` — **VERIFY** each |

Pull live each test; cite the access date. For hazards: query the `hazards` news category and VERIFY the classification (it may link to grid-customer flooding, not the plant).

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:    FEMA NFHL zone + NWS/USGS gauge history AND/OR search_news(category=hazards, query="flood") → VERIFY each
2. SCOPE:    search_plants(fuel="gas", state="TX", minMw=50)   → the Gulf Coast / TX thermal fleet
             ⚠ DO NOT use iso= — it returns [] (see Known gaps); scope by state
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"NG"})  → fleet frame
4. ANCHOR:   get_plant(<id>)  → geometry/county, water-sited-thermal flag, owner chain, monthly CF series
5. CONTEXT:  read get_plant(<id>).generation  → SHOW the CF; note it CANNOT isolate an inundation outage from seasonal variation
6. FLOODPLAIN: nearby_plants(<id>)  → other assets in the same watershed / behind the same levee
7. HAZARDS:  search_news(category=hazards, query="flood") + details_json → in-substrate corroboration; VERIFY
8. DRAFT:    assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / probability / per-plant-damage / single-cause
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso=...)` → `[]` | the `iso` filter is unwired (R1 — same as hail/hurricane/winter-storm) | scope by `state=`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served flood peril model | inundation probability / depth / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + forward probability | a served flood hazard model (R12) — upgrades directional → quantitative |
| No site-elevation field | a plant inside a FEMA zone may still be pad-elevated / flood-walled — not in the substrate | claim geographic exposure only; never a per-pad depth | a site-elevation / design-flood-basis field in the plant substrate |
| Monthly CF cannot resolve an outage | a multi-day inundation outage is invisible inside the monthly series | use CF as CONTEXT only; never as outage proof | daily/hourly generation or an availability feed |
| Hazards-news classification may mislink | a "flood" article may cover grid customers or a non-asset location | VERIFY every article against title/`details_json` + the plant location | hazards-news → plant linking + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No FEMA/NWS geography AND no verified hazards-news flood article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable flood geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No site elevation for the plant | **Infer directionally** from FEMA zone + proximity to water; caveat as inferred; do NOT assert a per-pad depth or outage |
