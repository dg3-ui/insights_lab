# Data Requirements — Severe Hail Exposure For Solar Assets

> **Status**: draft 2026-06-14. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked structural reference: `../weather_and_climate/el_nino_enso/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    hail geography / climatology  -> NOAA SPC (climatology stable; storm reports dated)   knowledge.md §3
SUBSTRATE   realized event               -> search_news(category=hazards, query="hail") + details_json  (VERIFY)
KNOWLEDGE   mechanism + mitigation        -> knowledge.md §1                                  (cite, don't re-derive)
SUBSTRATE   assets, capacity, geometry    -> search_plants → get_plant (lat/lon/county/boundary)  (places in footprint)
SUBSTRATE   realized impact               -> get_plant.generation monthly CF                  (the OBSERVED dip)
SUBSTRATE   same-cell fan-out             -> nearby_plants(plant_id, fuel="solar")            (other solar in the hail cell)
ACTOR       owner chain                   -> get_plant.ownership                              (routes the insight)
DESCRIPTIVE plant blurb                   -> get_plant.context                                (frames only — never grounds)
LOGIC       materiality, footprint test   -> ≥50 MW, county/geometry-in-hail-region           (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Hail geography / event | external + substrate | establish the condition | SPC climatology cite **or** a VERIFIED hazards-news event (hazard_type=hail) |
| Mechanism + mitigation | knowledge | the "why" + confidence ceiling | cite `knowledge.md` (hail-stow, glass spec) |
| Region / market scope | substrate / logic | bound the test | one resolvable region (`state="TX"` for ERCOT) |
| Solar plant list | substrate | asset scope | operating solar ≥ ~50 MW in scope |
| Plant geometry / county | substrate | place in footprint | lat/lon + county (+ boundary where present) |
| Generation monthly CF | substrate | realized impact | needed only for the event-translation claim |
| Owner / company | substrate / actor | actor relevance | owner chain where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA SPC severe-hail climatology | the hail-exposed geography | https://www.spc.noaa.gov/ |
| NOAA SPC storm reports | dated realized hail days | https://www.spc.noaa.gov/climo/reports/ |

Climatology is stable (cite); storm reports are dated. **Realized events affecting tracked assets are usually already in-substrate** via the `hazards` news category — prefer that (it links to the plant_id), and VERIFY the classification.

## Retrieval plan (the real call sequence — test 001)

```text
1. EVENT:  search_news(query="hail")  → hazards/hail articles (Fighting Jays 62945, Fort Bend TX) — VERIFY each
2. SCOPE:  search_plants(fuel="solar", state="TX", minMw=50)  → the ERCOT/TX solar fleet
           ⚠ DO NOT use iso="ERCOT" — it returns [] (see Known gaps)
3. SIZE:   aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"})  → TX 70,349 MW
4. ANCHOR: get_plant(62945)  → geometry/county, single-axis c-Si, owner chain, monthly CF series
5. IMPACT: read get_plant.generation monthly capacity_factor  → post-event CF dip (like-months YoY)
6. CELL:   nearby_plants(62945, fuel="solar")  → other solar in the same hail footprint
7. DRAFT:  assemble; split confidence (event vs forward exposure); block $ / probability / single-cause
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="ERCOT")` → `[]` | the `iso` filter is unwired (same as CAISO — `mcp_gaps` R1) | scope by `state="TX"`, confirm via `get_plant.grid`/`.regions` | wire the ISO filter / `resolve_region` (R1) |
| No served hail peril-risk model | hail return-period / severity / EAL / $ loss live in model-gpr, not the MCP | ship **directional**; block the $; cite the qualitative `damage_estimate` only as a frame | a served hazard peril model (`mcp_gaps` R12) — upgrades directional → quantitative |
| Hazards-news classifier noise | false positives (a "hails decree" reg article matched "hail"; a boiler explosion mis-tagged) | **VERIFY** every hazards article against title/`details_json` before using it | classifier precision pass (R12 note) |
| No fleet hail-footprint rollup | can't ask "how much TX solar capacity sits in the SPC hail maximum" in one call | anchor + `nearby_plants` cluster + the state total; caveat as illustrative | county/geometry-aware aggregate (pairs with R8/R10) |

Also log each to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No verified hail event AND no climatology cite | **Block** — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable region |
| Solar list unavailable | **Block** — no scoped entity set |
| Generation CF unavailable | drop the realized-impact claim; keep directional exposure only |
| Owner unavailable | asset-level claim only; do **not** infer the owner |
