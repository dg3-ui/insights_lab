# MCP Gap Ledger

> **Status**: living ledger, opened 2026-06-05.
>
> **Purpose**: the persistent home for "this MCP call / field / filter would be super useful" — the agent's back-of-mind for the tool surface. Every gap or idea hit while authoring or testing a resource lands here, so the *expandable floor* (`learning/01`) actually accumulates instead of evaporating at the end of a session.
>
> **This is data, not instruction.** The *instruction* to log here lives in `CLAUDE.md` / `AGENTS.md`; this file is the resolved ledger it feeds (`../principles.md` P3).
>
> **The prioritized build hand-off is the [Build Priority](#build-priority--the-platform-hand-off) section just below** — the ranked, platform-facing view of this ledger, for `renewablesinfo_org` (the `riorg` package + the MCP server). The body stays the running log: new gaps land in the **Ledger** as you hit them; re-rank the top table when planning a build.

## Build Priority — the platform hand-off

This is the **prioritized, build-ready view** of the ledger below, for the platform team to build from. The per-gap detail (contract, workaround, where observed) lives **once**, in each `Rn` entry; this table is the ranked index into them. Priority = impact (unblocks a resource, or many) × inverse effort; effort is a rough S/M/L. The catalog is 12 tools today — each ask grows the floor toward 13+ (`../learning/01_mcp_basics.md`).

| Pri | Ask | Unblocks | Effort | Entry |
|---|---|---|---|---|
| **P0** | Wire `search_plants(iso=…)` — join the existing per-plant `regions.iso_rto` (data exists, filter is dead) | every ISO-scoped test (CAISO, ERCOT…); ends the `state=` workaround | **S** | R1 |
| **P1** | Served **hazard peril model** (return-period · severity · EAL/PML · $) + classifier precision pass + a finer-than-monthly generation feed | hail · hurricane · heat → **directional → quantitative** | **L** | R12 |
| **P1** | **Offtaker** grounding — first-class `offtakers` array + `aggregate(group_by=buyer)` | `offtaker_concentration` (currently **BLOCKED**); any concentration read | **M** | R13 |
| **P1** | `get_external_state(driver)` — served NOAA state + `as_of` + freshness window | the state-freshness gate for every weather/climate resource | **M** | R4 |
| **P2** | `aggregate` seasonal-CF rollup | fleet exposure baselines (no single-plant "illustrative" caveat) | **M** | R2 |
| **P2** | `aggregate group_by=county` (+ ba/nerc) | sub-state exposure geography | **S–M** | R8 |
| **P2** | `aggregate` owner parent-canonicalization | concentration claims (stop splitting one parent's book) | **M** | R9 |
| **P2** | `coverage(entity, fields, filter)` introspection | the confidence-cap-for-missing-context firing deterministically, up front | **M** | R5 |
| **P3** | `nearby_by_coords(lat, lon, radius_km, fuel?)` | the **outlier** class — off-substrate pin → its energy cluster | **S–M** | R14 |
| **P3** | Elevation / surge / flood-zone field per plant | the **coastal hazard** class → substrate-grounded | **M–L** | R15 |
| **P3** | Plant wildfire / WUI / fire-hazard-zone field | `wildfire` exposure can move beyond county heuristics | **M** | R16 |
| **P3** | PSPS circuit / de-energization linkage per plant | `wildfire` PSPS curtailment can become plant-specific | **M–L** | R17 |
| **P3** | Smoke/AOD + irradiance-adjusted generation feed | `wildfire` smoke-output claims become measurable | **L** | R18 |
| **P3** | Plant winterization / cold-weather-package field | `extreme_cold_winter_storm` can route asset-specific hardening | **M** | R19 |
| **P3** | Sub-monthly generation / availability feed | smoke, freeze, heat, hurricane cut-out events can be resolved below monthly CF | **L** | R20 |
| **P3** | Plant-to-basin / reservoir linkage for hydro | `drought_low_hydro` can move beyond state screens | **M** | R21 |
| **P3** | Hydro inflow / reservoir storage / rule-curve surface | low-hydro exposure can become plant/reservoir-specific | **L** | R22 |
| **P3** | Coastal component elevation / critical-equipment layer | `hurricane_coastal_flood` can move beyond plant-centroid screens | **M–L** | R24 |
| **P3** | Served storm-surge / inundation overlay by event/scenario | coastal-flood resources can test event footprints against plant geometry | **L** | R25 |
| **P3** | Plant-to-river-reach / HUC / watershed linkage | `riverine_flood` can move beyond county/state proximity screens | **M** | R26 |
| **P3** | FEMA riverine flood zone join per plant | `riverine_flood` can make regulatory-floodplain claims without external lookup | **M** | R27 |
| **P4** | Fuel taxonomy alias / resolver | hydro and other resources avoid fuel-code guessing | **S** | R23 |
| **P3** | Served **geometry** (centroids + simplified polygons) | a real choropleth map (data side of the render tool) | **M** | R10 |
| **P4** | Serve the **brand kit** (logo · palette · skeleton) as MCP resources | on-brand rendering without carrying files | **S** | R6 |
| **P4** | **Render/export** tool (insight → HTML/DOCX, gate enforced at the tool layer) | the Layer-3 render step (today hand-assembled) | **L** | R7 |
| **P5** | Queue **resolved facts** (`find_by_extracted_fact` over projects) | Development-Risk / Portfolio actor-routing (`developer` null on queue) | **M** | R3 |
| **P5** | **Climate/weather** news lane in the classifier | corroborating news for weather-driven Exposure pieces | **L** | R11 |

**Start here (the quick win):** **R1** — the data exists (`get_plant().regions.iso_rto`), the filter just isn't joined to it; it's hit on nearly every scoped test (CAISO + ERCOT, solar + wind). Cheapest high-value fix.

**The biggest lever:** **R12** — a served hazard peril model flips hail/hurricane/heat from directional to quantitative in one stroke (the `model-gpr` wall). **R13** unblocks an entire resource (`offtaker_concentration` is BLOCKED today). **R4** removes the one un-enforced freshness hole. These three are the capability unlocks; the rest sharpen reads or build the render layer.

## Why This File Exists

A model has no memory between sessions. An MCP gap noticed today is gone tomorrow unless it is written down. This ledger is the tool-surface analog of what `test_runs/` extraction is to the methodology: **resolved feedback that grows the platform** (`capabilities.md` (the capability roadmap)). Each entry is also a roadmap input for the post-V0 in-house track (`../use_cases.md`).

## How To Add An Entry

Every entry has the three-part shape from `../learning/01_mcp_basics.md` + `../process/test_protocol.md`, plus where it was observed and a status:

```text
gap/idea:   what the surface can't do, or what would help
workaround: what kept the session moving (or "none yet")
roadmap:    the concrete tool / field / filter to build
observed:   the session / doc where it surfaced (+ date)
status:     open · proposed · building · shipped · wontfix
kind:       tool gap · field/coverage gap · new tool · filter · external-state
```

Keep entries terse. A recurring entry is a signal to prioritize it; note the repeat rather than duplicating.

## Ledger

### R1 — `search_plants(iso=…)` filter is unwired

```text
gap:        search_plants(fuel=solar, iso="CAISO", minMw=50) -> []  (empty; even iso alone returns [])
            yet get_plant(57993).regions.iso_rto = CAISO exists per-plant — the data is there, the filter isn't.
workaround: scope by state="CA" (CA ≈ CAISO, minus LADWP/SMUD/IID), then confirm each plant's
            regions.iso_rto via get_plant.
roadmap:    wire the search_plants ISO filter to the existing per-plant region join, OR add a
            resolve_region tool. This single fix turns the surface from 12 tools toward 13.
observed:   ../learning/01_mcp_basics.md + ENSO test_run_001 (2026-06-05);
            REPEAT confirmed for iso="ERCOT" in hail_solar + hurricane_high_wind_wind (incl. fuel=wind)
            test_runs (2026-06-14) — not CAISO- or solar-specific.
status:     open      kind: filter
```

### R2 — No fleet-level seasonal-CF rollup

```text
idea:       ENSO (and any Exposure-family) insight wants the seasonal capacity-factor baseline for a
            *fleet*, not one drilled plant. Today the only CF evidence is get_plant on a single asset.
workaround: drill one representative plant (e.g. 57993) and caveat that it is illustrative, not fleet-wide.
roadmap:    an aggregate-style call returning monthly/seasonal CF distribution across a scoped fleet
            (e.g. aggregate(entity=plants, metric=seasonal_cf, group_by=month, filter={state,fuel,minMw})).
observed:   test_run_001 next-fixes (2026-06-05)
status:     open      kind: new tool
```

### R3 — `developer` (and other resolved facts) null on queue rows

```text
gap:        search_projects rows return developer: null across DARDEN / UMBRIEL / WINGTIP etc. —
            so Development-Risk + Portfolio actor-routing has no actor to route to.
workaround: omit actor relevance where absent; do NOT infer a developer. Flag as a context gap.
roadmap:    extend resolved-fact coverage onto queue projects (find_by_extracted_fact over projects),
            or expose a coverage flag so the agent knows when routing is simply unavailable.
observed:   ../method/analysis_families.md (Development Risk) (2026-06-05)
status:     open      kind: field/coverage gap
```

### R4 — No served external-state call (NOAA ENSO etc.)

```text
idea:       the external causal state (NOAA CPC ENSO / ONI) is fetched ad hoc via WebFetch each test,
            with no enforced freshness. The methodology supplies it; nothing serves it with an as_of.
workaround: WebFetch the NOAA discussion live and hand-stamp the as_of in the insight.
roadmap:    a get_external_state(driver) MCP tool that returns the current state + as_of + source URL,
            cached with a freshness window. Closes architecture Open Decision 3 (state-freshness gate).
observed:   architecture §9 Open Decision 3 + test_run_001 (2026-06-05)
status:     proposed  kind: new tool / external-state
```

### R5 — No coverage / introspection call

```text
idea:       the agent cannot cheaply ask "what fraction of this scoped fleet has offtaker / financial /
            generation data?" — so it can't decide *up front* whether to downgrade for missing context.
workaround: drill plants until a pattern is obvious; expensive and ad hoc.
roadmap:    a coverage(entity, fields, filter) call returning fill-rates per field over a scope, so the
            confidence-cap-for-missing-context rule (08 P-data / confidence_rules) can fire deterministically.
observed:   inferred from ../method/data_map.md + confidence_rules discipline (2026-06-05)
status:     open      kind: new tool / introspection
```

### R6 — Brand assets not served via MCP

```text
gap:        rendered outputs need the brand kit (Inter / JetBrains Mono faces, palette, logo) in
            every session; nothing serves it — fonts ride a CDN link, the logo is vendored SVG.
workaround: brand vendored in resources/_style/ (brand.md + brand_assets/), composed post-gate.
roadmap:    serve the brand kit as MCP resources (logo SVG, palette tokens, artifact skeleton) so
            any session/agent renders on-brand without carrying files.
observed:   docs/plans/2026-06-11_layered_reference_v1.md Phase 2 (2026-06-12)
status:     open      kind: new tool / served asset
```

### R7 — No rendering/export tool (HTML artifact + DOCX assembled by hand)

```text
gap:        the canonical rendering is an HTML artifact hand-assembled from the skeleton each
            session; DOCX export for client deliverables is manual. Artifact-sandbox font fetches
            may also fail (the mandatory degradation stack covers it — _style/brand.md §B1).
workaround: brand_assets/artifact_skeleton.html + the output-contract envelopes; degrade to the
            system grotesque stack when the font CDN is blocked.
roadmap:    a render/export tool: validated insight object + contract tuple → styled HTML/DOCX,
            with the gate precondition enforced at the tool layer (not prompt-level).
observed:   docs/plans/2026-06-11_layered_reference_v1.md Phase 2 (2026-06-12)
status:     open      kind: new tool / rendering
```

### R8 — `aggregate` cannot group_by county

```text
gap:        aggregate group_by = state | fuel | iso | technology | status | owner only.
            No COUNTY. The top-down ENSO build wanted county concentration (Riverside,
            San Bernardino, Kern) — the geography the signal actually lands on.
workaround: pull flagship plants and read each one's county field; cannot get a county rollup.
roadmap:    add `county` (and ideally `ba`/`nerc`) to aggregate group_by, so exposure can be
            rolled to the sub-state geography an Exposure piece leads with.
observed:   InfraSure_ENSO_California_Solar build (2026-06-12)
status:     open      kind: field/coverage gap
```

### R9 — `aggregate(group_by=owner)` does not canonicalize parents

```text
gap:        owner rollup returned "Intersect" (2,586 MW) and "Intersect Power" (1,336 MW) as
            SEPARATE owners (substring/canonical_owner). Risk of splitting one parent's book,
            or double-counting, in any concentration claim.
workaround: name owners as returned; flag the split in text; do not sum across look-alikes.
roadmap:    parent-level canonicalization for the owner dimension (map aliases → UBO), or expose
            a parent_id to group on. Pairs with the 4-layer ownership chain get_plant already has.
observed:   InfraSure_ENSO_California_Solar build (2026-06-12); CONFIRMED LIVE in offtaker_concentration
            test_run_001 (2026-06-14): "Intersect Power" 2,389.2 MW vs "Intersect USA, LLC" 1,375.5 MW as separate groups.
status:     open      kind: field/coverage gap
```

### R10 — No served geometry for a real map

```text
gap:        a true geographic choropleth (the owner-requested CONUS map) needs state/county
            centroids or simplified boundaries; the MCP serves none, and the sandbox lacks
            Chrome/geopandas, so only a schematic tile-grid is renderable in-session.
workaround: matplotlib statebin tile-grid (the _craft spatial fallback) keyed to aggregate GW.
roadmap:    serve lightweight geometry (state/county centroids + simplified polygons) as an MCP
            resource so the render tool (R7) can draw an accurate map. Data side of R7.
observed:   InfraSure_ENSO_California_Solar build (2026-06-12)
status:     open      kind: new tool / served asset
```

### R11 — News corpus does not index climate / weather signals

```text
gap:        search_news for "El Nino / ENSO / winter" → 0 articles. The ~57K-article corpus
            indexes deal/construction/regulatory lanes, not climate-driver signals, so a
            weather-driven Exposure piece gets no corroborating news.
            NB: physical-HAZARD events (hail/wildfire/hurricane) ARE indexed in the `hazards` category with
            structured details_json — this gap is specifically CLIMATE/WEATHER drivers (ENSO). (hail_solar test 001)
workaround: rely on the external NOAA pull + substrate; omit the news channel; do NOT confess
            the gap in client copy (voice §5).
roadmap:    a climate/weather lane in the news classifier (NWS alerts already flow into the
            platform pipeline upstream — surface + link them per plant/region).
observed:   InfraSure_ENSO_California_Solar build (2026-06-12)
status:     open      kind: field/coverage gap
```

### R12 — No served hazard peril-risk model (+ hazards-news classifier noise)

```text
gap:        hazard EXPOSURE + realized EVENT-TRANSLATION ground today (substrate geometry/CF + the
            `hazards` news category), but the modeled peril RISK — hail return-period/severity, EAL/PML,
            $ loss, insurance pricing — lives in model-gpr, not the MCP. Also the hazards classifier
            carries false positives (a "hails decree" regulatory article + a boiler explosion both mis-tagged).
workaround: ship DIRECTIONAL (geography + observed CF impact); block the $ / return-period; add a VERIFY
            step to every hazard resource's procedure (don't trust the classification label).
roadmap:    a served hazard peril model (return-period · severity · EAL by asset) — upgrades hazard
            resources directional → quantitative (Wave-2 "wire model-gpr"); + a classifier-precision pass.
observed:   hail_solar (2026-06-14); EXTENDED across Wave-1 — no thermal/cell-temp model (extreme_heat_derate,
            so weather × performance hits the same wall), no TC/high-wind model (hurricane_high_wind_wind);
            AND: hazards news does NOT link to wind plants (TX hurricane articles link to nuclear/hydro/gas only);
            AND: monthly CF is too coarse to show a storm cut-out or an intra-day heat de-rate (need hourly/daily/availability feed).
status:     open      kind: field/coverage gap · external-state
```

### R13 — Offtaker grounding: `offtakers` array null; resolved buyer lives in `news_extracted.buyer`

```text
gap:        get_plant.offtakers is null on EVERY plant drilled (Ragsdale, Baldy Mesa, Cedar Creek, Blue Creek,
            Sunstone, Hill Solar 1) even where a PPA demonstrably exists — the resolved counterparty lives in
            news_extracted.buyer. Also: find_by_extracted_fact(buyer) returns entity_ids but no summed capacity,
            and aggregate has no group_by=buyer (can't size a named-offtaker book in one call). And
            news_extracted.deal_value_usd carries cross-tagged $ noise (a $16.9B Spain figure on CA's Baldy Mesa).
workaround: ground on find_by_extracted_fact(buyer) + per-plant news_extracted.buyer (VERIFY); never read a null
            offtakers array as "no PPA"; drill each id for capacity + sum verified-only; never use deal_value_usd
            as a PPA price. NUANCE (2026-06-15): the PPA *price* is sometimes recoverable from
            financial.years[].ppa_price_per_mwh even when offtakers is null (Gallup 62406 = $44.08/MWh) — useful
            as a fixed-vs-merchant *structure* signal, but it is NOT the counterparty (no identity, no concentration).
roadmap:    serve a first-class offtakers array from the resolution layer; add group_by=buyer to aggregate;
            a precision pass on the $ fields.
observed:   offtaker_concentration test_run_001 (2026-06-14); + confirmed in the brookfield_standard_solar studio
            briefs (2026-06-14; re-confirmed 2026-06-15 on get_plant 62406 + 67747) — offtakers null per-asset for an
            owner rollup, though a fixed PPA price surfaced on 62406; compare_entities also returns
            canonical_owner=null (owner on a nested path it doesn't surface).
status:     open      kind: field/coverage gap
```

### R14 — No geometry/coordinate-seeded nearby query

```text
gap:        nearby_plants requires a center plant_id — you cannot ask "what plants are within R km of an arbitrary
            lat/lon." For an OFF-SUBSTRATE pin (a port, a mine, any non-power asset), you must first anchor on a known
            nearby plant to fan out (the anten_ports brief anchored on Baytown 55327 to read the Galveston cluster).
workaround: find a known in-substrate plant near the target, then nearby_plants from it.
roadmap:    a nearby_by_coords(lat, lon, radius_km, fuel?) call — turns ANY off-substrate outlier (the outlier
            playbook's class) into a substrate-grounded energy-cluster overlay directly.
observed:   galveston_ship_channel_surge/storm_surge studio brief (2026-06-14; folded 2026-06-15)
status:     open      kind: new tool / filter
```

### R15 — No elevation / surge / flood-zone attribute on a plant

```text
gap:        get_plant carries lat/lon + boundary geometry but no coastal-elevation, storm-surge, or FEMA-flood-zone
            attribute — so a coastal/surge exposure read must pull the hazard footprint from external public sources
            (the anten_ports brief used City-of-Houston surge briefings), not the substrate.
workaround: external surge/elevation sources, cited + dated; co-location MW from nearby_plants as the substrate anchor.
roadmap:    a served coastal-elevation / surge / flood-zone field per plant (pairs with R10 served-geometry) — makes the
            COASTAL hazard class substrate-grounded instead of research-grounded.
observed:   galveston_ship_channel_surge/storm_surge studio brief (2026-06-14; folded 2026-06-15)
status:     open      kind: field/coverage gap
```

### R16 — No wildfire / WUI / fire-hazard-zone field per plant

```text
gap:        The substrate has plant lat/lon + county, but no Wildland-Urban Interface, CAL FIRE Fire Hazard
            Severity Zone, USFS Wildfire Hazard Potential, FSim burn-probability, or LANDFIRE fuel-context field
            attached to each plant. `wildfire` can screen by county / external maps, but cannot make a clean
            plant-level fire-zone claim from the substrate alone.
workaround: use external NIFC / Cal Fire / USFS / LANDFIRE layers as dated sources; state geography directionally;
            avoid precise plant-zone claims unless manually checked against a named external map.
roadmap:    add a served fire-hazard-zone / WUI / fuel-context field per plant, or a geometry overlay tool that
            joins plant coordinates to NIFC/Cal Fire/USFS/LANDFIRE layers.
observed:   resources/hazard/wildfire (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R17 — No PSPS circuit / de-energization linkage per plant

```text
gap:        PSPS exposure depends on the interconnection / utility circuit, not just plant county or fuel.
            The substrate does not expose a plant-to-circuit / utility-territory / PSPS-eligibility field, so
            `wildfire` cannot assert that a specific generator was curtailed by a PSPS event unless an external
            CPUC / utility / CAISO filing names the asset or circuit.
workaround: treat PSPS as directional geography / utility-territory exposure; require external PSPS filings for
            any plant-specific curtailment claim.
roadmap:    add circuit / utility-territory / PSPS-event linkage to plant records, or a PSPS event overlay keyed
            by circuit / substation / interconnection.
observed:   resources/hazard/wildfire (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R18 — No served smoke/AOD + irradiance-adjusted generation join

```text
gap:        Smoke can reduce PV output over days-to-weeks, but monthly capacity factor cannot isolate smoke from
            seasonal irradiance, curtailment, clouds, or maintenance. The MCP does not serve smoke optical depth,
            HRRR-Smoke, irradiance, or hourly/daily generation in one joinable surface.
workaround: cite FIRMS / HRRR-Smoke / external smoke sources as regional context; block plant-level smoke-loss
            magnitude and any single-cause CF attribution.
roadmap:    serve smoke/AOD + irradiance-adjusted hourly/daily generation (or an availability / performance index)
            so smoke-output event translation can be tested like hail's monthly-CF signal.
observed:   resources/hazard/wildfire (authored draft, 2026-06-25); extends R12's finer-than-monthly note.
status:     open      kind: external-state · field/coverage gap
```

### R19 — No plant winterization / cold-weather-package field

```text
gap:        `extreme_cold_winter_storm` needs to know whether a plant has cold-weather packages, heat tracing,
            firm gas supply, instrument-air protection, blade de-icing, or other winterization controls. The
            substrate has fuel/geometry/owner, but not plant winterization status.
workaround: use FERC/NERC Uri findings at the regional mechanism level; infer only directionally from geography
            and fuel; never assert plant-specific winterization status without a named source.
roadmap:    add winterization / cold-weather package / fuel-supply-firmness fields where public or resolved facts
            exist; expose coverage flags so missing equipment context caps confidence explicitly.
observed:   resources/hazard/extreme_cold_winter_storm (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R20 — No sub-monthly generation / availability feed for short-duration events

```text
gap:        Monthly CF is too coarse for short-duration hazards: smoke plumes, PSPS events, Uri forced outages,
            hurricane cut-outs, and intra-day heat de-rates happen over hours-to-days inside a month. The current
            substrate can show broad context, but not separable event attribution.
workaround: use monthly generation only as context; keep event-specific output claims regional/directional unless
            an external outage / hourly-generation source is available.
roadmap:    serve hourly/daily generation, availability, outage, or event-window performance metrics with `as_of`
            metadata and plant IDs.
observed:   resources/hazard/wildfire + resources/hazard/extreme_cold_winter_storm (authored drafts, 2026-06-25);
            repeats R12's finer-than-monthly limitation across new hazards.
status:     open      kind: field/coverage gap · new tool
```

### R21 — No plant-to-basin / reservoir linkage for hydro

```text
gap:        `drought_low_hydro` needs to know which river basin, watershed, reservoir, or upstream gage serves a
            hydropower plant. The substrate has plant location and monthly generation, but not a first-class basin /
            reservoir / gage linkage, so a state-level hydro fleet is only a screen.
workaround: use state/market scope as a first-pass filter; manually cite USGS gages, SNOTEL basins, NOHRSC/SNODAS,
            or reservoir dashboards where a named linkage is clear; caveat unresolved basin linkage.
roadmap:    add watershed / basin / reservoir / upstream-gage identifiers to hydro plants, or expose a hydro
            basin-resolution tool keyed by plant_id.
observed:   resources/weather_and_climate/drought_low_hydro (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R22 — No hydro inflow / reservoir storage / operating-rule surface

```text
gap:        Exact low-hydro generation and flexibility depend on reservoir storage, inflow timing, rule curves,
            water rights, environmental-flow obligations, flood-control constraints, maintenance, and dispatch.
            None of these are served as structured MCP fields, so `drought_low_hydro` must block exact MWh/$ and
            operations claims.
workaround: cite external reservoir / water-agency dashboards for context; keep claims directional unless a named
            source provides the specific operating constraint.
roadmap:    serve reservoir storage / inflow / rule-curve / water-obligation fields or a hydro-operations module
            for named hydro plants.
observed:   resources/weather_and_climate/drought_low_hydro (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap · new tool
```

### R23 — Fuel taxonomy alias / resolver is not explicit

```text
gap:        New resources sometimes need to guess the MCP fuel convention (`hydro` vs `WAT` / `HYD`, `gas` vs
            `NG` / `GAS`, etc.). Existing packages carry local workarounds, but there is no lightweight way to ask
            the MCP for valid fuel tokens and aliases before a test.
workaround: inspect prior resources / search results and record the exact filter used in each test_run; switch
            filters if the first call returns empty unexpectedly.
roadmap:    expose a fuel taxonomy / alias resolver, or document valid `search_plants(fuel=...)` tokens in the MCP
            discovery surface.
observed:   resources/weather_and_climate/drought_low_hydro (authored draft, 2026-06-25)
status:     open      kind: filter · docs gap
```

### R24 — No coastal component elevation / critical-equipment layer

```text
gap:        `hurricane_coastal_flood` is component-specific: substations, transformers, inverter pads,
            switchgear, access roads, fuel/cooling systems, and interconnection equipment can drive the outage.
            The substrate has plant location, but not component location/elevation or critical-equipment height.
workaround: make only directional plant / cluster exposure claims; use external FEMA/NOAA/local flood sources for
            context; block exact inundation, equipment damage, and outage-duration claims.
roadmap:    add component-level elevation / equipment-location fields for substations, pads, transformers,
            switchgear, access roads, and interconnection assets where public or model-derived.
observed:   resources/hazard/hurricane_coastal_flood (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R25 — No served storm-surge / coastal-inundation overlay

```text
gap:        Coastal-flood exposure needs a joined event/scenario footprint: NHC/P-Surge/SLOSH, FEMA NFHL/FIS,
            tide-gage observations, local surge studies, and elevation all live externally. The MCP cannot ask
            whether a plant geometry intersects a named surge / coastal flood footprint.
workaround: cite external storm-surge / flood products manually; keep claims directional and geography-scoped.
roadmap:    serve storm-surge / coastal-inundation overlays by event/scenario, with plant geometry intersection
            and `as_of` / source metadata.
observed:   resources/hazard/hurricane_coastal_flood (authored draft, 2026-06-25); extends R15.
status:     open      kind: external-state · field/coverage gap · new tool
```

### R26 — No plant-to-river-reach / HUC / watershed linkage

```text
gap:        `riverine_flood` needs to know which river reach, HUC watershed, or upstream drainage basin a
            plant sits in or near. The substrate has lat/lon and county, but not a first-class river-reach
            or HUC linkage, so riverine exposure claims stay at a county/state proximity screen.
workaround: use state/county scope as a first-pass filter; manually cite USGS NWIS gages and NOAA AHPS
            forecast points whose geography overlaps the scoped county; caveat as a proximity screen.
roadmap:    add HUC-8 / HUC-12 watershed or nearest-named-river-reach identifiers to plants, or expose
            a spatial river-proximity tool keyed by plant_id and radius.
observed:   resources/hazard/riverine_flood (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

### R27 — No FEMA riverine flood zone join per plant

```text
gap:        `riverine_flood` uses FEMA NFHL AE/AO/AH zone designations to establish regulatory floodplain
            exposure, but the substrate does not serve a per-plant FEMA zone flag. Analysts must look up
            zone designations externally by county, and no plant-level join exists.
workaround: pull FEMA NFHL by county externally; caveat that no site-specific join was performed; label
            the FIRM map's effective date.
roadmap:    serve FEMA AE/AO/AH zone flag and FIRM map vintage as structured fields per plant, derived
            from a spatial join against the NFHL layer.
observed:   resources/hazard/riverine_flood (authored draft, 2026-06-25)
status:     open      kind: field/coverage gap
```

---

**See also**: `../learning/01_mcp_basics.md` (the floor-not-ceiling thesis + the gap-log format), `../process/test_protocol.md` (the failure taxonomy each gap maps to), `capabilities.md` (the capability roadmap these entries feed), `../principles.md` P3 (why this is resolved data, not instruction), `CLAUDE.md` (the standing instruction to log here).
