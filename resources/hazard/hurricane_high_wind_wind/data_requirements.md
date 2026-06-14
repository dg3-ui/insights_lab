# Data Requirements — Hurricane / High-Wind Exposure For Wind Assets

> **Status**: draft 2026-06-14. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Sibling structural reference: `../hail_solar/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    storm track / geography      -> NOAA NHC best-track / HURDAT2 + advisories (Beryl AL022024)   knowledge.md §3
EXTERNAL    non-tropical high wind        -> NOAA SPC high-wind / convective-wind reports                 knowledge.md §3
SUBSTRATE   realized event               -> search_news(category=hazards, query="hurricane"/storm) + details_json  (VERIFY)
KNOWLEDGE   mechanism (cut-out vs damage) -> knowledge.md §1                                  (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry    -> search_plants → get_plant (lat/lon/county/turbine_locations)  (places in corridor)
SUBSTRATE   realized impact (CONTEXT)     -> get_plant.generation monthly CF                  (context only — CANNOT isolate the cut-out)
SUBSTRATE   same-corridor fan-out         -> nearby_plants(plant_id, fuel="wind")             (other coastal wind in the track)
ACTOR       owner chain                   -> get_plant.ownership                              (routes the insight)
DESCRIPTIVE plant blurb                   -> get_plant.context.description                    (frames only — never grounds)
LOGIC       materiality, corridor test    -> ≥50 MW, coastal-county / lat-lon-in-corridor      (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Hurricane track / geography | external | establish the condition | NHC HURDAT2 / advisory cite (landfall point + category) |
| Realized event (optional) | substrate | regional event framing | a VERIFIED hazards-news storm (hazard_type=hurricane) — note it rarely links to a WIND plant |
| Mechanism (cut-out vs damage) | knowledge | the "why" + confidence ceiling | cite `knowledge.md` §1 (state which claim type) |
| Region / market scope | substrate / logic | bound the test | one resolvable coastal region (`state="TX"` + coastal counties) |
| Wind plant list | substrate | asset scope | operating wind ≥ ~50 MW in the coastal corridor |
| Plant geometry / county / turbines | substrate | place in corridor | lat/lon + coastal county (+ turbine_locations / boundary where present) |
| Generation monthly CF | substrate | context ONLY | used only to SHOW it cannot isolate the cut-out — never as damage proof |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA NHC best-track / HURDAT2 | the storm track + landfall (the hurricane corridor) | https://www.nhc.noaa.gov/ |
| NOAA NHC advisory archive | dated live-season advisories | https://www.nhc.noaa.gov/archive/ |
| NOAA SPC high-wind / wind reports | non-tropical high-wind / derecho exposure | https://www.spc.noaa.gov/climo/reports/ |

Track/HURDAT2 is stable (cite); advisories are dated. **Realized storms affecting the grid are often in-substrate** via the `hazards` news category — but in test 001 the TX hurricane articles linked to **nuclear/hydro/gas** plants and grid-customer outages, **not** to wind turbines, so the wind operational impact must be reasoned from the mechanism, not lifted from a wind-plant news record. VERIFY the classification.

## Retrieval plan (the real call sequence — test 001)

```text
1. EVENT:  search_news(query="Beryl")  → Beryl hazards articles (Reuters ~1M TX outages; Newsweek South Texas Project NUC "threatened", Matagorda) — VERIFY each
2. SCOPE:  search_plants(fuel="wind", state="TX", minMw=50)  → the ERCOT/TX wind fleet (Great Prairie 1027 MW, Horse Hollow 735.5, …)
           ⚠ DO NOT use iso="ERCOT" — it returns [] (see Known gaps)
3. SIZE:   aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"})  → TX 49,719.6 MW (#1)
4. COASTAL FILTER: keep plants in coastal counties (Matagorda, Cameron, Willacy, Kenedy, Nueces, San Patricio, Brazoria, …)
5. ANCHOR: get_plant(62417 Peyton Creek I, Matagorda)  → geometry/county, Nordex AW125 turbines, owner chain, monthly CF series
6. CONTEXT: read get_plant(62417).generation  → SHOW the July-2024 CF (0.129) is IN-LINE with the 2021 lull (0.129) and ABOVE 2025-08 (0.078) → cannot isolate Beryl
7. CORRIDOR: nearby_plants(62417, fuel="wind") + the coastal-county cluster  → other coastal wind in the track
8. DRAFT:  assemble; split confidence (exposure vs realized event vs CF context); block $ / probability / single-cause / sub-Cat-3-damage
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="ERCOT")` → `[]` | the `iso` filter is unwired for wind too (same as solar/CAISO — `mcp_gaps` R1) | scope by `state="TX"`, confirm via `get_plant.grid`/`.regions` (iso="ercot") | wire the ISO filter / `resolve_region` (R1) |
| No served TC / high-wind peril model | hurricane return-period / wind-field / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + forward probability; cite qualitative `damage_estimate` only as a frame | a served hazard peril model (`mcp_gaps` R12) — upgrades directional → quantitative |
| Hazards news does NOT link to WIND plants | TX hurricane articles link to nuclear/hydro/gas + grid outages; no wind-plant operational-impact record exists | reason the wind impact from the MECHANISM; use the storm as a REGIONAL fact only; VERIFY every article | hazards-news → wind-plant linking + classifier precision (R12 note) |
| Monthly CF cannot resolve a cut-out | a multi-day storm cut-out is invisible inside the monthly summer-lull minimum | use CF as CONTEXT to PROVE the point (the dip ≠ the storm); never as damage proof | daily/hourly generation or an availability feed would surface a cut-out (new feed) |
| No fleet coastal-corridor rollup | can't ask "how much TX wind capacity sits in the NHC hurricane corridor" in one call | anchor + coastal-county filter + `nearby_plants` + the state total; caveat as illustrative | county/geometry-aware aggregate (pairs with R8/R10) |
| `nearby_plants` radius sparse for wind | pre-computed neighbor list returned only 1 wind plant even at radius_km=80 for the Matagorda anchor | use the state-wide coastal-county filter to build the corridor cluster instead | denser nearby precompute / a bbox query (R8/R10) |

Also log each to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NHC track cite AND no verified hurricane event | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable coastal region |
| Wind list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| A storm is sub-Cat-3 | **default to the cut-out claim type**; block any lasting-damage claim absent a damage record |
