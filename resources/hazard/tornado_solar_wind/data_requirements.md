# Data Requirements — Tornado Exposure For Solar, Wind, and Substation Assets

> **Status**: draft 2026-06-29. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`; sibling: `../hurricane_high_wind_wind/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    tornado geography + event -> NOAA SPC climatology / storm reports + hazards news (pull live, dated)   knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                                                             (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant (geometry/county/fuel)                         (grounds the claim)
ACTOR       owner / company           -> get_plant.ownership / plants_by_owner                                     (routes the insight)
DESCRIPTIVE blurb / context           -> get_plant.context                                                        (frames only — never grounds)
LOGIC       materiality, corridor     -> >=50 MW cut · in/out of the touchdown-density corridor                  (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Tornado geography / event state | external | establish the condition | SPC touchdown-density climatology OR a VERIFIED hazards-news tornado article + access date |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (the narrow-footprint framing) |
| Region / market scope | substrate / logic | bound the test | one resolvable region (test 001 = Southern Plains / OK–TX) |
| Plant / generator list | substrate | asset scope | operating (+ queue) ≥ 50 MW in scope |
| Geometry / county | substrate | place in/out of the corridor | lat/lon + county from `get_plant` |
| Owner / company | substrate / actor | actor relevance | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA SPC | tornado touchdown-density climatology + storm reports | https://www.spc.noaa.gov/ |
| NWS | tornado warnings + EF damage surveys | https://www.weather.gov/ |
| InfraSure hazards news | in-substrate realized-event corroboration | `search_news(category=hazards, query="tornado")` — **VERIFY** each |

Pull live each test; cite the access date. For hazards: query the `hazards` news category and VERIFY the classification.

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:    SPC touchdown-density climatology AND/OR search_news(category=hazards, query="tornado") → VERIFY each
2. SCOPE:    search_plants(fuel="wind", state="OK", minMw=50)  [+ "TX"; + fuel="solar"]   → the corridor fleet
             ⚠ DO NOT use iso= — it returns [] (see Known gaps); scope by state
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"})  → fleet frame
4. ANCHOR:   get_plant(<id>)  → geometry/county, owner chain, monthly CF series
5. CONTEXT:  read get_plant(<id>).generation  → SHOW the CF; note it CANNOT resolve a narrow partial-plant strike
6. CORRIDOR: nearby_plants(<id>)  → other assets in the touchdown-density band
7. HAZARDS:  search_news(category=hazards, query="tornado") + details_json → in-substrate corroboration; VERIFY
8. DRAFT:    assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / strike-probability / per-plant-damage / single-cause
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso=...)` → `[]` | the `iso` filter is unwired (R1 — same as the sibling hazards) | scope by `state=`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served tornado-hazard model | strike probability / return-period / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + per-asset strike probability | a served tornado-hazard model (R12) — upgrades directional → quantitative |
| Touchdown density is areal, not per-asset | the climatology gives an area rate, not a site strike probability | claim corridor exposure + intersection risk; never a per-site return-period | a hazard model that resolves per-asset strike probability |
| No sub-plant geometry | which array rows / which turbines is not in the substrate | claim asset-level exposure only; never which rows/turbines were destroyed | a sub-plant layout / inventory field |
| Monthly CF cannot resolve a narrow strike | a partial-plant total loss is invisible inside the monthly series | use CF as CONTEXT only; never as damage proof | daily/hourly generation or an availability feed |
| Hazards-news classifier noise | false positives / mislinks | VERIFY every article against title/`details_json` + the plant location | hazards-news → plant linking + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No SPC geography AND no verified hazards-news tornado article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable tornado geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No sub-plant geometry | claim asset-level corridor exposure only; do NOT assert which rows/turbines |
