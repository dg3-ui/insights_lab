# MCP Ask — Prioritized Tool/Field Requests for the Platform

> **Status**: living hand-off, opened 2026-06-15. The **platform-facing, build-ready** synthesis of `mcp_gaps.md`. Take this to **`renewablesinfo_org`** (the `riorg` package + the InfraSure MCP server) to actually build the surface out.
>
> **Relationship to the ledger** (single-source discipline): `mcp_gaps.md` is the running **LEDGER** — where every gap lands as it's hit, with the workaround the lab is using meanwhile (`gap · workaround · roadmap`). **This doc is the prioritized HAND-OFF derived from it** — ranked, with a contract sketch per ask. It is *not* authoritative: when in doubt, the ledger entry (`Rn`) has the full context, the workaround, and where it was observed. New gaps go in the **ledger first**; promote them here when prioritizing a build.

## How to read

```text
PRIORITY = impact (unblocks a resource, or many) × inverse effort.
Each ask: what to build · a rough contract · what it UNBLOCKS · effort (rough S/M/L) · ledger ref (Rn).
Do the QUICK WIN first (cheap, hit on nearly every test); then the BIG ROCKS (capability unlocks).
The catalog is 12 tools today; each ask grows the floor toward 13+ (learning/01).
```

## The ask, prioritized

| Pri | Ask | What to build (sketch) | Unblocks | Effort | Ledger |
|---|---|---|---|---|---|
| **P0** | Wire `search_plants(iso=…)` | join the existing per-plant `regions.iso_rto` to the filter (data exists, filter is dead) | every ISO-scoped test (CAISO, ERCOT…) — stop the `state=` workaround | **S** | R1 |
| **P1** | Served **hazard peril model** | return-period · severity · EAL/PML · $ loss by asset; + a hazards-classifier precision pass; + a finer-than-monthly generation/availability feed | hail · hurricane · heat → **directional → quantitative** (the `model-gpr` wall) | **L** | R12 |
| **P1** | **Offtaker** grounding | first-class `offtakers` array from the resolution layer; `aggregate(group_by=buyer)`; precision pass on `deal_value_usd` | `offtaker_concentration` (currently **BLOCKED**); any counterparty-concentration read | **M** | R13 |
| **P1** | `get_external_state(driver)` | returns current external state (NOAA CPC ENSO/ONI, temp/season outlook) + `as_of` + source URL, cached with a freshness window | the state-freshness gate for **every** weather/climate resource | **M** | R4 |
| **P2** | `aggregate` **seasonal-CF rollup** | `aggregate(entity=plants, metric=seasonal_cf, group_by=month, filter={state,fuel,minMw})` | fleet-level exposure baselines (no more single-plant "illustrative" caveat) | **M** | R2 |
| **P2** | `aggregate group_by=county` | add `county` (+ `ba`/`nerc`) to the group_by dimensions | sub-state exposure geography (the cell a hazard/weather signal lands on) | **S–M** | R8 |
| **P2** | `aggregate` **owner canonicalization** | map owner aliases → parent UBO, or expose `parent_id` to group on | concentration claims (stop splitting/double-counting one parent's book) | **M** | R9 |
| **P2** | `coverage(entity, fields, filter)` | fill-rate per field over a scope | the confidence-cap-for-missing-context rule firing **deterministically**, up front | **M** | R5 |
| **P3** | `nearby_by_coords(lat, lon, radius_km, fuel?)` | radius query seeded by an arbitrary coordinate, not a center `plant_id` | the **outlier** class — drop a pin on any off-substrate asset (port, mine) → its energy cluster | **S–M** | R14 |
| **P3** | Elevation / surge / flood-zone field | a coastal-elevation / storm-surge / FEMA-flood-zone attribute per plant | the **coastal hazard** class → substrate-grounded, not research-grounded | **M–L** | R15 |
| **P3** | Served **geometry** | lightweight state/county centroids + simplified polygons as an MCP resource | a real choropleth map (data side of the render tool) | **M** | R10 |
| **P4** | Serve the **brand kit** | logo SVG, palette tokens, the artifact skeleton as MCP resources | on-brand rendering in any session without carrying files | **S** | R6 |
| **P4** | **Render/export** tool | validated insight + output type → styled HTML/DOCX, **with the gate enforced at the tool layer** | the Layer-3 render step (today hand-assembled); the gate stops being prompt-level | **L** | R7 |
| **P5** | Queue **resolved facts** | extend `find_by_extracted_fact` coverage onto queue projects; or a coverage flag | Development-Risk / Portfolio actor-routing (today `developer` is null on queue rows) | **M** | R3 |
| **P5** | **Climate/weather** news lane | a climate-driver lane in the news classifier (NWS alerts already flow upstream — surface + link per plant/region) | corroborating news for weather-driven Exposure pieces (hazard events ARE indexed; climate drivers aren't) | **L** | R11 |

## The quick win — do this first

**R1 · wire `search_plants(iso=…)`.** The cheapest high-value fix on the board: the per-plant `regions.iso_rto` already exists (`get_plant(57993).regions.iso_rto = CAISO`), the filter just isn't joined to it — `search_plants(iso="CAISO")` returns `[]`. It's hit on **nearly every** scoped test (confirmed for CAISO *and* ERCOT, solar *and* wind), and every test currently pays the `state=` workaround + a per-plant `get_plant` confirm. Wiring it (or adding a `resolve_region` tool) removes that tax everywhere. Start here.

## The big rocks — the capability unlocks

- **R12 · served hazard peril model** is the headline. Today the lab ships hazard reads **directional** (geography + observed CF) and **blocks** the $ / return-period / EAL (it lives in `model-gpr`, off the public MCP). A served peril model (return-period · severity · EAL by asset) flips hail / hurricane / heat from *directional → quantitative* in one stroke. Pair it with: a hazards-classifier **precision pass** (false positives like a "hails decree" article, a boiler explosion) and a **finer-than-monthly** generation/availability feed (monthly CF can't show a storm cut-out or an intra-day heat de-rate). This is the biggest single lever on the lab's output quality.
- **R13 · offtaker grounding** unblocks an entire resource: `offtaker_concentration` is currently **BLOCKED** because `get_plant.offtakers` is null book-wide (the resolved buyer lives in `news_extracted.buyer`, and there's no `group_by=buyer` to size a book in one call). Serve a first-class `offtakers` array + `aggregate(group_by=buyer)` and the resource goes from blocked → groundable. (Note: the PPA *price* is partly recoverable from `financial.ppa_price_per_mwh`, but not the counterparty — so it's a structure signal, not concentration.)
- **R4 · `get_external_state`** removes the one un-enforced freshness hole: external causal state (NOAA ENSO/ONI, the temp/season outlook) is WebFetched ad hoc each test today. A served call with an `as_of` + a freshness window makes every weather resource's state-gate deterministic.

## The rest, by theme

- **`aggregate` rollups (R2 · R8 · R9 · R5)** — the high-reuse rollup quartet: a fleet seasonal-CF rollup, a `county` (+ ba/nerc) group_by, owner-parent canonicalization, and a `coverage()` introspection call. None is a headline alone, but together they make Exposure + Portfolio + Concentration reads sharper and let the confidence-cap fire up front.
- **Geospatial / outlier (R14 · R15 · R10)** — the coastal + off-substrate class: a coordinate-seeded nearby query, an elevation/surge/flood-zone field, and served geometry for a real map. R14 + R15 turn the outlier-playbook reads (ports, mines, coastal clusters) from research-grounded → substrate-grounded.
- **Render tooling (R6 · R7)** — serve the brand kit, then a render/export tool that enforces the gate at the tool layer (the Layer-3 content engine, today hand-assembled per `/render`).
- **Coverage extensions (R3 · R11)** — queue-project resolved facts (actor routing), and a climate/weather news lane (hazard *events* are indexed; climate *drivers* like ENSO are not).

---

**See also**: `mcp_gaps.md` (the running ledger — the single source; each `Rn` here links back to its full entry + workaround) · `capabilities.md` (the capability roadmap these feed) · `../use_cases.md` (the post-V0 in-house track) · `../../CLAUDE.md` (the standing instruction to log gaps) · `../../README.md` "Where this sits" (the `renewablesinfo_org` platform repo this hand-off targets).
