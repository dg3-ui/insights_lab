# Data Requirements - El Niño / ENSO Exposure

> **Status**: v0 input map, deepened 2026-06-05.
>
> **Purpose**: define exactly what the manual MCP/Claude test must retrieve (and from where), what is external, and what to do when an input is missing.
>
> **Companions**: `knowledge.md` (mechanism + sources), `resource.md` (method).

## Input Layers (by job)

```text
EXTERNAL    ENSO state/forecast        -> NOAA CPC / IRI (pull live)            knowledge.md §3, §8
KNOWLEDGE   mechanism + robustness     -> knowledge.md §4–§6                    (cite, don't re-derive)
SUBSTRATE   assets, capacity, region   -> search_plants → get_plant            (grounds the claim)
SUBSTRATE   generation / CF            -> get_plant.generation                 (seasonal baseline)
ACTOR       owner / offtaker           -> get_plant.ownership / .offtakers     (routes the insight)
DESCRIPTIVE plant blurb / Wikipedia    -> get_plant.context                    (frames only — never grounds)
LOGIC       thresholds, region map     -> ≥50 MW, state=CA crosswalk           (converts inputs to claims)
```

## Required Inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| ENSO state / forecast | external | establish condition | source name, access date, phase + Alert status + DJF outlook + strength |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` teleconnection rating |
| Region / market scope | substrate / logic | bound the test | one resolvable region (`state="CA"` for CAISO) |
| Plant / generator list | substrate | asset scope | operating solar in scope |
| Capacity | substrate | materiality | recommended ≥ 50 MW |
| Owner / company | substrate / actor | actor relevance | owner/operator name where available |

## External STATE — Where To Pull It

The ENSO state is **not** in the substrate. Pull it live each test and cite the access date:

| Source | Use | URL |
|---|---|---|
| NOAA CPC ENSO Diagnostic Discussion | current phase, Alert status, DJF forecast | https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/ensodisc.shtml |
| NOAA CPC ENSO probabilities / ONI | strength probabilities | https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso/roni/probabilities/ |
| IRI ENSO Forecast | model-ensemble plume | https://iri.columbia.edu/our-expertise/climate/forecasts/enso/current/ |

## First-Test Retrieval Plan (the real call sequence)

```text
1. STATE:    WebFetch NOAA CPC ENSO discussion → phase, Alert, DJF %, strength    (cite access date)
2. SCOPE:    search_plants(fuel="solar", state="CA", minMw=50)                      → fleet rows
             ⚠ DO NOT use iso="CAISO" — it returns [] (see "Known gaps")
3. SIZE:     aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"})
4. DRILL:    get_plant(<id>)  → seasonal capacity_factor, regions.iso_rto, ownership, offtakers
5. ACTOR:    get_plant.ownership / .offtakers  (or plants_by_owner for portfolio view)
6. DRAFT:    assemble the claim; cap confidence at the weakest link; block quantitative claims
```

## Known Gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="CAISO")` → `[]` | ISO filter unwired; data exists per-plant in `get_plant.regions.iso_rto` | scope by `state="CA"`, confirm per-plant | wire ISO filter / add `resolve_region` tool |
| No plant-level irradiance/weather model | substrate has *historical* CF, not a forward production model | keep claims directional; block plant-level forecasts | future modeling layer |
| ENSO strength unknown at lead time | NOAA gives occurrence % but not strength early | cap confidence at LOW | re-pull as forecasts sharpen |

## Missing-Data Handling

| Missing input | Required action |
|---|---|
| ENSO source | **Block** the insight — cannot establish the condition |
| Region cannot be resolved | downgrade, or switch to a resolvable region |
| Asset list unavailable | **Block** — no scoped entity set |
| Owner/company unavailable | asset-level claim only; actor relevance goes generic |
| Offtaker unavailable | omit offtaker relevance (do not infer) |
| Generation/pricing unavailable | keep revenue implications directional and caveated |
