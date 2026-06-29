# Data Requirements — Wildfire Exposure For Solar, Transmission, and Grid-Connected Assets

> **Status**: draft 2026-06-25. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Sibling structural references: `../hail_solar/data_requirements.md`, `../hurricane_high_wind_wind/data_requirements.md`, `../extreme_cold_winter_storm/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    fire geography / perimeter       -> NIFC / IRWIN fire perimeter data                              knowledge.md §3
EXTERNAL    fire-potential / fuel screen     -> USFS FSim / WHP + LANDFIRE                                    knowledge.md §3
EXTERNAL    smoke context                    -> NASA FIRMS active fire + NOAA HRRR-Smoke                       knowledge.md §3
EXTERNAL    fire-weather geography           -> NOAA NWS red-flag watches + fire-weather outlooks             knowledge.md §3
EXTERNAL    PSPS event record                -> CPUC / utility PSPS filings + CAISO notices where available    knowledge.md §4
SUBSTRATE   realized event                  -> search_news(category=hazards, query="wildfire"/"PSPS"/"fire") + details_json (VERIFY)
KNOWLEDGE   mechanism (A/B/C by asset)      -> knowledge.md §1                                (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry      -> search_plants → get_plant (lat/lon/county)     (places in fire corridor or PSPS zone)
SUBSTRATE   realized impact (CONTEXT)       -> get_plant.generation monthly CF                (context only — CANNOT isolate smoke event)
SUBSTRATE   same-corridor fan-out           -> nearby_plants(plant_id, fuel filter)           (other exposed assets)
ACTOR       owner chain                     -> get_plant.ownership                            (routes the insight)
DESCRIPTIVE plant blurb                     -> get_plant.context.description                  (frames only — never grounds)
LOGIC       materiality, geography test     -> ≥50 MW, Western WUI / CA geography             (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Fire geography / perimeter | external | establish the condition (mechanisms A/B) | NIFC IRWIN perimeter cite (fire name + date + geography) |
| Fire-potential / fuel screen | external | exposure screening | USFS FSim/WHP or LANDFIRE vintage; frames relative exposure only |
| Smoke plume / active fire | external | smoke context for mechanism A | NASA FIRMS / HRRR-Smoke date and geography; not a plant-loss proof |
| PSPS event record | external | establish the condition (mechanism C) | CAISO / utility PSPS filing (circuit + date + duration) |
| Fire-weather geography | external | exposure framing | NOAA NWS red-flag climatology cite |
| Realized event (optional) | substrate | in-substrate corroboration | a VERIFIED hazards-news fire/PSPS article |
| Mechanism by asset (A/B/C) | knowledge | the "why" + confidence ceiling | cite `knowledge.md` §1 (state which claim type) |
| Region / market scope | substrate / logic | bound the test | one resolvable geography (`state="CA"` for PSPS; Western states for smoke/fire) |
| Fleet list by fuel | substrate | asset scope | operating solar/wind/gas ≥ ~50 MW in the fire-weather geography |
| Plant geometry / county | substrate | place in fire corridor or PSPS zone | lat/lon + state/county |
| Generation monthly CF | substrate | context ONLY | used only to SHOW it cannot isolate a smoke event — never as impact proof |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NIFC / IRWIN fire perimeter data | fire geography + active/historical perimeters | https://www.nifc.gov/ |
| USFS FSim / Wildfire Hazard Potential | probabilistic / relative fire-potential screen | https://data-usfs.hub.arcgis.com/ |
| LANDFIRE | fuel / vegetation context for ROW and WUI exposure | https://www.landfire.gov/ |
| NASA FIRMS / NOAA HRRR-Smoke | active-fire detections + smoke transport context | https://firms.modaps.eosdis.nasa.gov/ · https://rapidrefresh.noaa.gov/hrrr/ |
| NOAA NWS red-flag / fire-weather | fire-weather exposure geography + watches | https://www.weather.gov/ |
| CAISO PSPS market notices | PSPS event record: which circuits, when, duration | https://www.caiso.com/ |
| Cal Fire incident records | California-specific fire ignition + perimeter | https://www.fire.ca.gov/ |
| CPUC wildfire mitigation filings | utility WMP + PSPS program rules | https://www.cpuc.ca.gov/ |
| PG&E / SCE / SDG&E PSPS filings | circuit-level PSPS records | utility CPUC filings |

NIFC perimeters and Cal Fire records are stable for historical events (cite by fire name + date). CAISO PSPS notices are dated. NOAA NWS climatology is stable; current watches are dated.

## Retrieval plan (the real call sequence — test 001)

```text
1. EVENT:   search_news(category=hazards, query="wildfire" OR "PSPS" OR "Camp Fire")  → VERIFY each; check whether the article links
            to a generation plant or to a transmission/grid event; note that hazards articles may cover utility
            liability or grid outages rather than a specific solar/wind plant
2. STATE:   cite NIFC/Cal Fire for the named fire perimeter; cite USFS FSim/WHP or LANDFIRE for fire-potential/fuel
            screening; cite NASA FIRMS / HRRR-Smoke only when making a smoke-context claim.
3. SCOPE:   search_plants(fuel="solar", state="CA", minMw=50)   → the CA solar fleet (CAISO proxy)
            search_plants(fuel="wind", state="CA", minMw=50)    → the CA wind fleet (PSPS exposure)
            ⚠ DO NOT use iso="CAISO" — likely returns [] (same R1 gap as other resources). Confirm grid/regions per plant.
4. SIZE:    aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity", filter={state:"CA"})
5. ANCHOR:  get_plant(<anchor_id>)  → geometry/county, fuel/technology, owner chain, monthly CF series
            Select a large CA solar plant in a fire-weather-exposed county (e.g. San Bernardino, Riverside,
            Kern, or a North Bay / NorCal county) as the anchor
6. CONTEXT: read get_plant(<anchor_id>).generation  → SHOW the summer/fall CF; note it is consistent with
            seasonal irradiance and CANNOT isolate a smoke-driven reduction at monthly resolution
7. CORRIDOR: nearby_plants(<anchor_id>, fuel="solar"/"wind") → other exposed assets in the same fire-weather geography
8. HAZARDS: search_news(category=hazards, query="wildfire"/"fire"/"PSPS") + details_json → in-substrate corroboration;
            VERIFY classification (check whether it links to the right fuel class)
9. DRAFT:   assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / ignition
            liability / forward probability / per-plant smoke attribution / single-cause CF
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="CAISO")` → likely `[]` | the `iso` filter is unwired (same R1 gap as other resources) | scope by `state="CA"`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No PSPS circuit-level field in the substrate | which interconnection circuit a plant is on, and whether that circuit is PSPS-eligible, is not in the substrate | reason from geography (county + NWS red-flag zone); caveat as inferred | a PSPS-eligibility or circuit field in the plant substrate |
| No served fire-risk peril model | ignition probability / return-period / EAL / $ live in model-gpr | ship **directional**; block the $ + forward probability | a served fire-risk model — upgrades directional → quantitative |
| Monthly CF cannot resolve a smoke event | a days-to-weeks smoke reduction is invisible inside the monthly seasonal-irradiance baseline | use CF as CONTEXT to PROVE the point; never as smoke-impact proof | daily/hourly generation or irradiance-adjusted CF |
| No smoke / irradiance join | the resource can cite FIRMS/HRRR-Smoke, but it cannot join smoke optical depth to plant generation | state smoke mechanism directionally; do not quantify plant loss | served smoke/AOD + irradiance-adjusted generation feed |
| Hazards-news may not link to generation plants | fire/PSPS articles often cover utility liability, grid outages, or residential customers — not the solar/wind plant | VERIFY every article; check fuel/technology field and affected_area | hazards-news → generation-plant linking + classifier precision |
| No WUI / fire-zone geometry field | whether a plant sits inside a WUI or high fire-hazard severity zone (HFHSZ) is not in the substrate | reason from county + state fire-risk maps (Cal Fire HFHSZ); caveat as inferred | a fire-hazard-zone field in the plant substrate |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NIFC perimeter AND no CAISO PSPS record AND no verified fire hazards-news article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable fire-weather geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No PSPS circuit record for the plant | **Infer directionally** from geography (county + NWS red-flag zone); caveat as inferred; do NOT assert specific PSPS eligibility |
| Smoke optical depth data unavailable | state the mechanism directionally; do NOT quantify the output reduction without a smoke model |
