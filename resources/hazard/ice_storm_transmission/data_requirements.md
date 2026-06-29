# Data Requirements — Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets

> **Status**: draft 2026-06-29. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`; sibling: `../extreme_cold_winter_storm/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    ice geography + event     -> NOAA NWS freezing-rain climatology + SPIA index + hazards news (pull live, dated)   knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                                                                       (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant (geometry/county/fuel) + delivery corridor               (grounds the claim)
ACTOR       owner / company           -> get_plant.ownership / plants_by_owner (incl. transmission ownership)                (routes the insight)
DESCRIPTIVE blurb / context           -> get_plant.context                                                                  (frames only — never grounds)
LOGIC       materiality, ice belt     -> >=50 MW cut · in/out of the ice belt · A/B/C claim type                           (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Ice-storm geography / event state | external | establish the condition | NWS freezing-rain climatology OR SPIA index OR a VERIFIED hazards-news ice-storm article + access date |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (which of A/B/C) |
| Region / market scope | substrate / logic | bound the test | one resolvable region (test 001 = South-Central ice belt / OK–TX–AR) |
| Plant / generator list + corridor | substrate | asset + delivery-path scope | operating (+ queue) ≥ 50 MW; treat the delivery path as primary |
| Geometry / county | substrate | place in the ice belt | lat/lon + county from `get_plant` |
| Owner / company | substrate / actor | actor relevance (incl. transmission owner) | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA NWS | freezing-rain climatology + winter-storm warnings | https://www.weather.gov/ |
| SPIA Ice Accumulation Index | accretion severity → expected damage tier | https://www.spia-index.com/ |
| InfraSure hazards news | in-substrate realized-event corroboration | `search_news(category=hazards, query="ice storm")` — **VERIFY** each |

Pull live each test; cite the access date. VERIFY that the article is the ICE/delivery mechanism, not the generation-side freeze (which is `extreme_cold_winter_storm`).

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:    NWS freezing-rain climatology + SPIA index AND/OR search_news(category=hazards, query="ice storm") → VERIFY each
2. SCOPE:    search_plants(fuel="wind", state="OK", minMw=50)  [+ "TX","AR"] + the delivery corridor   → the ice-belt fleet
             ⚠ DO NOT use iso= — it returns [] (see Known gaps); scope by state
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"})  → fleet frame
4. ANCHOR:   get_plant(<id>)  → geometry/county, owner chain (incl. transmission owner), monthly CF series
5. CONTEXT:  read get_plant(<id>).generation  → SHOW the CF; note it CANNOT isolate an ice-storm outage from the winter seasonal pattern
6. CORRIDOR: nearby_plants(<id>)  → other assets dependent on the same delivery path
7. HAZARDS:  search_news(category=hazards, query="ice storm"/"freezing rain") + details_json → in-substrate corroboration; VERIFY (ice vs generation-freeze)
8. DRAFT:    assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / restoration cost / probability / per-span-or-plant / single-cause. Distinguish physical damage from delivery stranding.
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso=...)` → `[]` | the `iso` filter is unwired (R1 — same as the sibling hazards) | scope by `state=`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served ice-load / ice-storm model | ice-load failure probability / return-period / restoration cost / $ live in model-gpr, not the MCP | ship **directional**; block the $ + forward probability | a served ice-load hazard model (R12) — upgrades directional → quantitative |
| No conductor/tower ratings or line geometry | the hazard is on the WIRES, but ratings + line routes are not in the substrate | claim geographic ice-belt exposure only; never a per-span failure | transmission conductor-rating + line-geometry substrate |
| Monthly CF cannot resolve an ice-storm outage | a multi-day outage is invisible inside the winter seasonal minimum | use CF as CONTEXT only; never as outage proof | daily/hourly generation or an availability feed |
| Delivery-stranding has no plant-side signal | a stranded healthy generator looks like low output, not damage | reason from the corridor + downed-line mechanism; caveat as delivery-side | a delivery / interconnection-availability feed |
| Hazards-news may be the generation-freeze, not ice | "winter storm" articles can cover gas freeze-off (the other resource) | VERIFY every article; route generation-freeze to `extreme_cold_winter_storm` | hazards-news cause-specific tagging + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NWS/SPIA geography AND no verified hazards-news ice-storm article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable ice-belt geography |
| Fleet / corridor list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No conductor/tower ratings | claim geographic ice-belt exposure only; do NOT assert which spans/towers fail |
| Cannot tell ice from generation-freeze | route to `extreme_cold_winter_storm` if generation-side; do NOT double-count |
