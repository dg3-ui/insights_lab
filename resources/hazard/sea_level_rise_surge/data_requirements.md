# Data Requirements — Sea Level Rise & Storm Surge Exposure For Coastal Thermal, Nuclear, and Grid Assets

> **Status**: draft 2026-06-29. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`; sibling: `../hurricane_high_wind_wind/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    SLR trend + surge + event -> NOAA tide gauges + NHC SLOSH + FEMA zones + hazards news (pull live, dated)   knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                                                                 (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant (geometry/county/fuel)                             (grounds the claim)
ACTOR       owner / company           -> get_plant.ownership / plants_by_owner                                         (routes the insight)
DESCRIPTIVE blurb / context           -> get_plant.context                                                            (frames only — never grounds)
LOGIC       materiality, tidewater    -> >=50 MW cut · coastal-county / tidewater flag · chronic vs acute            (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| SLR trend / surge envelope / event | external | establish the condition | NOAA gauge SLR rate OR NHC/FEMA surge envelope OR a VERIFIED hazards-news surge article + access date |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (chronic vs acute) |
| Region / market scope | substrate / logic | bound the test | one resolvable coastal region (test 001 = Gulf Coast / TX) |
| Plant / generator list | substrate | asset scope | operating (+ queue) ≥ 50 MW, tidewater-filtered |
| Geometry / county | substrate | place at/away from tidewater | lat/lon + coastal county from `get_plant` |
| Owner / company | substrate / actor | actor relevance | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA tide gauges + SLR Viewer | chronic relative-SLR rate near the asset | https://tidesandcurrents.noaa.gov/sltrends/ · https://coast.noaa.gov/slr/ |
| NOAA NHC surge (SLOSH/P-Surge) | acute surge envelope for the reach | https://www.nhc.noaa.gov/surge/ |
| FEMA coastal flood zones | VE / coastal-A designation near the asset | https://msc.fema.gov/ |
| InfraSure hazards news | in-substrate realized-event corroboration | `search_news(category=hazards, query="storm surge")` — **VERIFY** each |

Pull live each test; cite the access date.

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:    NOAA tide-gauge SLR rate (chronic) + NHC SLOSH / FEMA VE zone (acute) AND/OR search_news(category=hazards, query="storm surge") → VERIFY each
2. SCOPE:    search_plants(fuel="nuclear", state="TX", minMw=50)  [+ fuel="gas"]   → coastal fleet; filter to tidewater
             ⚠ DO NOT use iso= — it returns [] (see Known gaps); scope by state
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"NUC"})  → fleet frame
4. ANCHOR:   get_plant(<id>)  → geometry/coastal county, distance to shoreline, owner chain, monthly CF series
5. CONTEXT:  read get_plant(<id>).generation  → note it is largely IRRELEVANT for the chronic horizon + cannot resolve an acute surge
6. REACH:    nearby_plants(<id>)  → other tidewater assets along the coast
7. HAZARDS:  search_news(category=hazards, query="storm surge"/"coastal flood") + details_json → in-substrate corroboration; VERIFY
8. DRAFT:    assemble; split confidence (chronic SLR vs acute surge vs CF context); block $ / decommissioning / inundation-year / surge-probability / depth / single-cause
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso=...)` → `[]` | the `iso` filter is unwired (R1 — same as the sibling hazards) | scope by `state=`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served SLR/surge peril model | inundation depth / year / surge probability / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + depth + year | a served SLR/surge hazard model (R12) — upgrades directional → quantitative |
| No site-elevation / design-flood-basis field | a tidewater plant may be elevated / sea-walled — not in the substrate | claim geographic tidewater exposure only; never a depth or year | a site-elevation / design-flood-basis field |
| Monthly CF is irrelevant for the chronic horizon | SLR plays out over decades; surge over hours — neither resolves on monthly CF | use CF as CONTEXT only (note its irrelevance); never as proof | daily/hourly generation or an availability feed (for the acute case) |
| Hazards-news classifier noise | false positives / mislinks | VERIFY every article against title/`details_json` + the plant location | hazards-news → plant linking + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NOAA/NHC/FEMA state AND no verified hazards-news surge article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable coastal geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only (and largely irrelevant); keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No site elevation for the plant | **Infer directionally** from coastal proximity + FEMA VE zone; caveat as inferred; do NOT assert a depth or inundation year |
