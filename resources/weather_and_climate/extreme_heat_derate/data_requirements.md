# Data Requirements — Extreme-Heat Thermal Derate For Solar Assets

> **Status**: draft 2026-06-14. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked structural reference: `../el_nino_enso/data_requirements.md` (same NOAA-pull + state-proxy discipline).

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    hot-summer condition     -> NOAA CPC seasonal temperature outlook (issued ~mid-month, dated)   knowledge.md §3
KNOWLEDGE   mechanism magnitude      -> knowledge.md §1 (temperature coefficient ~ -0.3 to -0.45 %/°C)     (cite, don't re-derive)
SUBSTRATE   assets, capacity         -> search_plants(fuel="solar", state="TX", minMw=50)                  (the scoped fleet)
SUBSTRATE   summer-CF baseline       -> get_plant.generation monthly CF                                    (the HONESTY proof: summer CF is HIGH)
SUBSTRATE   construction             -> get_plant.generators.solar (single_axis_tracking / crystalline_silicon)  (the de-rate-prone build)
SUBSTRATE   grid zone (peak link)    -> get_plant.grid (HB_/LZ_) + .regions.iso_rto                        (routes the peak-coincidence argument)
SUBSTRATE   same-market fan-out      -> nearby_plants(plant_id, fuel="solar")                              (other solar in the same heat/zone)
ACTOR       owner / offtaker chain   -> get_plant.ownership / .offtakers                                   (routes the insight)
DESCRIPTIVE plant blurb              -> get_plant.context.description                                       (frames only — never grounds)
LOGIC       materiality, peak link   -> ≥50 MW; de-rate concentrates in peak afternoon = ERCOT summer peak (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Temperature outlook | external | establish the hot-summer condition | a DATED NOAA/CPC seasonal outlook (above-normal lean) |
| Mechanism magnitude | knowledge | the "why" + the modest-magnitude ceiling | cite `knowledge.md` §1 (temperature coefficient, NOCT) |
| Region / market scope | substrate / logic | bound the test | one resolvable market (`state="TX"` for ERCOT) |
| Solar plant list | substrate | asset scope | operating solar ≥ ~50 MW in scope |
| Summer-CF baseline | substrate | the HONESTY proof | monthly CF showing summer CF is HIGH (≈0.30) vs winter (≈0.09–0.15) |
| Construction flags | substrate | the de-rate-prone build | `generators.solar.single_axis_tracking` / `crystalline_silicon` where present |
| Grid zone | substrate | the peak-coincidence routing | `grid.hub`/`lmp_node` (HB_/LZ_) + `regions.iso_rto` = ERCOT |
| Owner / offtaker | substrate / actor | actor relevance | owner chain / PPA context where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| NOAA CPC seasonal temperature outlook | the hot-summer condition (above-normal lean) | https://www.cpc.ncep.noaa.gov/products/predictions/long_range/ |
| NOAA CPC 6–10 / 8–14 day + monthly outlooks | shorter-lead heat signals | https://www.cpc.ncep.noaa.gov/ |

The outlook is **dated** (re-pull every test, cite the issue/access date). The mechanism magnitude is **stable physics** (cite `knowledge.md` §6). The **climate news channel is EMPTY for this signal** — `search_news` does not index climate/temperature outlooks (`mcp_gaps` R11), so **omit news** and rely on the NOAA pull + substrate.

## Retrieval plan (the real call sequence — test 001)

```text
1. CONDITION: NOAA/CPC seasonal temperature outlook (JJA above-normal lean) → cite issue/access date (2026-06-14)
2. SCOPE:     search_plants(fuel="solar", state="TX", minMw=50)  → the ERCOT/TX solar fleet (Tehuacana 1254.8 MW, …)
              ⚠ DO NOT use iso="ERCOT" — it returns [] (see Known gaps)
3. SIZE:      aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"})  → TX 70,349.3 MW (#1)
              aggregate(… metric="count" …)  → TX 378 plants
4. ANCHOR:    get_plant(64927)  → 500 MW single-axis c-Si, ERCOT South (HB_SOUTH/LZ_SOUTH), Tokyo Gas, monthly CF series
5. BASELINE:  read get_plant(64927).generation monthly CF  → CONFIRM summer CF HIGH (2025: Jun 0.296/Jul 0.302/Aug 0.307) vs winter (Jan 0.094/Dec 0.150)
6. CELL:      nearby_plants(64927, fuel="solar")  → Danish Fields 66914 (600 MW), Red Tailed Hawk 66157 (360 MW), Flag City 65844 (167.3 MW)
7. DRAFT:     assemble; cap at LOW; block %/MWh, $, forward probability, and the monthly-CF heat read
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `search_plants(iso="ERCOT")` → `[]` | the `iso` filter is unwired (same as CAISO — `mcp_gaps` R1) | scope by `state="TX"`, confirm zone via `get_plant.grid`/`.regions` | wire the ISO filter / `resolve_region` (R1) |
| Climate-signal news channel empty | `search_news` does not index climate/temperature outlooks (`mcp_gaps` R11) | omit news; rely on the NOAA pull + substrate | a climate-signal feed / indexed climate news (R11) |
| No plant-level thermal / cell-temp model | the quantified %/MWh de-rate (and the $) live in model-gpr, not the MCP | ship **directional**; block the number; cite the temperature coefficient only as the magnitude ceiling | a served thermal-derate / cell-temp model (`mcp_gaps` R12) — upgrades directional → quantitative |
| No hourly / sub-monthly generation | the substrate CF is **monthly**, so the intra-day peak-hour de-rate is not directly observable | reason from physics + the peak-coincidence logic; never read the de-rate off monthly CF | hourly generation series (pairs with R12) |

Also log each to `../../docs/status/mcp_gaps.md`.

## Missing-data handling

| Missing input | Required action |
|---|---|
| No dated temperature outlook | **Block** — cannot establish the condition (or scope to a clearly-hot historical summer + caveat) |
| Region cannot be resolved | downgrade, or switch to a resolvable market |
| Solar list unavailable | **Block** — no scoped entity set |
| Summer-CF baseline unavailable | keep directional exposure; state the high-summer-CF expectation as mechanism, flag the missing baseline |
| Construction flags unavailable | claim at the fleet level (c-Si dominates utility PV); do not assert a single plant's build |
| Owner / offtaker unavailable | asset-level claim only; do **not** infer the owner |
