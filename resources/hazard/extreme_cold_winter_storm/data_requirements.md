# Data Requirements — Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets

> **Status**: draft 2026-06-24. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Sibling structural references: `../hail_solar/data_requirements.md`, `../hurricane_high_wind_wind/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    freeze geography / event window  -> NOAA NWS winter storm historical records + watches/warnings       knowledge.md §3
EXTERNAL    authoritative event record        -> FERC/NERC "February 2021 Cold Weather Outages" report (2021-11)  knowledge.md §3
SUBSTRATE   realized event                    -> search_news(category=hazards, query="Uri"/"winter storm"/"freeze") + details_json (VERIFY)
KNOWLEDGE   mechanism (A/B/C by fuel)         -> knowledge.md §1                                  (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry        -> search_plants → get_plant (lat/lon/county)        (places in freeze corridor)
SUBSTRATE   realized impact (CONTEXT)         -> get_plant.generation monthly CF                   (context only — CANNOT isolate the outage)
SUBSTRATE   same-corridor fan-out             -> nearby_plants(plant_id, fuel filter)              (other exposed assets)
ACTOR       owner chain                       -> get_plant.ownership                               (routes the insight)
DESCRIPTIVE plant blurb                       -> get_plant.context.description                     (frames only — never grounds)
LOGIC       materiality, geography test       -> ≥50 MW, Southern-plains / Gulf-Coast geography     (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Freeze geography / event window | external | establish the condition | NOAA NWS cite (storm dates + temperature extremes) |
| Authoritative event record (Uri) | external | regional event grounding | FERC/NERC 2021-11 report (outage scale + mechanism) |
| Realized event (optional) | substrate | in-substrate corroboration | a VERIFIED hazards-news freeze/winter-storm article |
| Mechanism by fuel (A/B/C) | knowledge | the "why" + confidence ceiling | cite `knowledge.md` §1 (state which claim type) |
| Region / market scope | substrate / logic | bound the test | one resolvable geography (`state="TX"` + freeze corridor) |
| Fleet list by fuel | substrate | asset scope | operating thermal/wind/solar ≥ ~50 MW in the geography |
| Plant geometry / county | substrate | place in freeze corridor | lat/lon + state/county |
| Generation monthly CF | substrate | context ONLY | used only to SHOW it cannot isolate the outage — never as event proof |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA NWS winter storm records | storm geography + event window | https://www.weather.gov/ |
| FERC/NERC Feb-2021 report | authoritative Uri mechanism + outage scale | https://www.ferc.gov/media/february-2021-cold-weather-outages-texas-and-south-central-united-states |
| ERCOT post-event analysis | generation-by-fuel timeline during Uri | https://www.ercot.com/ |
| EIA-923 / EIA-930 (where available) | plant-level generation during the event window (if accessible) | https://www.eia.gov/ |

The FERC/NERC report is stable (cite by publication date: 2021-11). NOAA NWS records are stable for historical events; watches/warnings are dated for live events.

## Retrieval plan (the real call sequence — test 001)

```text
1. EVENT:   search_news(query="Uri" OR "winter storm" OR "freeze")  → VERIFY each; check fuel/technology classification;
            note that hazards articles may link to gas/thermal or to grid-customer outages; VERIFY the substrate matches
            the plant fuel class you are analyzing
2. SCOPE:   search_plants(fuel="gas", state="TX", minMw=50)  → the ERCOT gas/thermal fleet
            search_plants(fuel="wind", state="TX", minMw=50) → the ERCOT wind fleet
            search_plants(fuel="solar", state="TX", minMw=50) → the ERCOT solar fleet
            ⚠ DO NOT use iso="ERCOT" — it returns [] (see Known gaps, same as R1 for hail_solar / hurricane)
3. SIZE:    aggregate(entity="plants", group_by=["state","fuel"], metric="total_capacity")  → TX gas/wind/solar totals
4. ANCHOR:  get_plant(<anchor_id>)  → geometry/county, fuel/technology, owner chain, monthly CF series
            Select a large gas plant in TX as the thermal anchor (e.g. a major ERCOT gas generator in the freeze corridor)
5. CONTEXT: read get_plant(<anchor_id>).generation  → SHOW the February CF; note it is consistent with the seasonal
            minimum and CANNOT isolate a Uri-driven forced outage at monthly resolution
6. CORRIDOR: nearby_plants(<anchor_id>, fuel="gas"/"wind") → other exposed assets in the same geography
7. HAZARDS: search_news(category=hazards, query="winter storm"/"freeze") + details_json → in-substrate event corroboration;
            VERIFY each classification
8. DRAFT:   assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / probability /
            per-plant-attribution / single-cause-CF
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="ERCOT")` → `[]` | the `iso` filter is unwired (same as R1 in hail_solar/hurricane) | scope by `state="TX"`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served cold-weather peril model | return-period / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + forward probability | a served cold-weather hazard model — upgrades directional → quantitative |
| Monthly CF cannot resolve a forced outage | a multi-day Uri outage is invisible inside the monthly seasonal minimum | use CF as CONTEXT to PROVE the point; never as outage proof | daily/hourly generation or an availability feed |
| No plant-level winterization status | whether a specific plant has cold-weather packages is not in the substrate | reason from geography + Southern-latitude heuristic + FERC/NERC findings; caveat as inferred | a winterization-status field in the plant substrate |
| No wellhead / pipeline provenance | which gas supply source a plant uses and whether that source froze is not in the substrate | reason from the FERC/NERC mechanism; caveat as regional inference | fuel supply chain data |
| Hazards-news classification may link to wrong fuel | substrate articles may cover grid-customer outages or nuclear/hydro, not the thermal plant you are analyzing | VERIFY every article; check the fuel/technology field | hazards-news → fuel-specific plant linking + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NWS event record AND no verified hazards-news freeze article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No winterization record for the plant | **Infer directionally** from geography (Southern latitude + fuel class) with an explicit caveat; do NOT assert specific winterization status |
