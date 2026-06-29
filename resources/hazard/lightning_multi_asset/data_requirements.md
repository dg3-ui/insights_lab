# Data Requirements — Lightning Exposure For Wind, Solar, and Electrical-Plant Assets

> **Status**: draft 2026-06-29. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`; sibling: `../hail_solar/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    flash density + event     -> NOAA/Vaisala NLDN climatology + NWS outlooks + hazards news (pull live, dated)   knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                                                                    (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant (geometry/county/fuel/hub-height)                     (grounds the claim)
ACTOR       owner / company           -> get_plant.ownership / plants_by_owner                                            (routes the insight)
DESCRIPTIVE blurb / context           -> get_plant.context                                                               (frames only — never grounds)
LOGIC       materiality, flash band   -> >=50 MW cut · in/out of the flash-density band · direct-strike vs surge        (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Flash-density geography / event | external | establish the condition | NLDN flash-density climatology OR a VERIFIED hazards-news lightning article + access date |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (direct strike vs induced surge) |
| Region / market scope | substrate / logic | bound the test | one resolvable region (test 001 = Gulf Coast / FL–TX) |
| Plant / generator list | substrate | asset scope | operating (+ queue) ≥ 50 MW in scope |
| Geometry / county (+ hub height) | substrate | place in the band; frame wind direct-strike exposure | lat/lon + county (+ turbine hub height) from `get_plant` |
| Owner / company | substrate / actor | actor relevance | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA / Vaisala NLDN | cloud-to-ground flash-density climatology | https://www.weather.gov/ · Vaisala Annual Lightning Report |
| NWS / SPC | thunderstorm / convective outlooks (near-term) | https://www.spc.noaa.gov/ |
| InfraSure hazards news | in-substrate realized-event corroboration | `search_news(category=hazards, query="lightning")` — **VERIFY** each |

Pull live each test; cite the access date.

## Retrieval plan (the real call sequence — test 001)

```text
1. STATE:    NLDN flash-density climatology AND/OR search_news(category=hazards, query="lightning") → VERIFY each
2. SCOPE:    search_plants(fuel="wind", state="FL", minMw=50)  [+ "TX"; + fuel="solar"]   → the flash-density-band fleet
             ⚠ DO NOT use iso= — it returns [] (see Known gaps); scope by state
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"})  → fleet frame
4. ANCHOR:   get_plant(<id>)  → geometry/county, turbine hub height (frames direct-strike exposure), owner chain, monthly CF
5. CONTEXT:  read get_plant(<id>).generation  → SHOW the CF; note it CANNOT resolve a component-level strike outage
6. BAND:     nearby_plants(<id>)  → other assets in the flash-density band
7. HAZARDS:  search_news(category=hazards, query="lightning") + details_json → in-substrate corroboration; VERIFY
8. DRAFT:    assemble; split confidence (exposure + mechanism vs realized event vs CF context); block $ / strike-rate / per-plant-damage / single-cause. Frame as cumulative component risk.
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso=...)` → `[]` | the `iso` filter is unwired (R1 — same as the sibling hazards) | scope by `state=`, confirm via `get_plant.grid` | wire the ISO filter / `resolve_region` (R1) |
| No served lightning strike-rate model | strike rate / component-failure probability / EAL / $ live in model-gpr, not the MCP | ship **directional**; block the $ + per-asset strike rate | a served strike-rate model (R12) — upgrades directional → quantitative |
| No LPS / surge-protection-status field | whether an asset has adequate LPS / SPDs is not in the substrate | claim geographic flash-density exposure only; never per-asset adequacy | an LPS / surge-protection-status field in the plant substrate |
| Monthly CF cannot resolve a component strike | a component-level outage is invisible inside the monthly series | use CF as CONTEXT only; never as damage proof | daily/hourly generation or an availability feed |
| Hazards-news classifier noise | lightning is often a sub-cause inside a broader convective event | VERIFY every article against title/`details_json` | hazards-news → cause-specific tagging + classifier precision |

Also log each gap to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No NLDN geography AND no verified hazards-news lightning article | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable flash-density geography |
| Fleet list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | no loss — it is context only; keep directional exposure + mechanism |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
| No LPS status for the asset | claim geographic exposure only; do NOT assert whether the LPS / SPDs are adequate |
