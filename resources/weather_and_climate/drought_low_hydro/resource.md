# Drought / Low-Hydro Exposure For Hydropower Assets — Method (human-readable)

> **Status**: draft 2026-06-25. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../../docs/method/resource_standard.md`. Sibling weather resources: `../el_nino_enso/`, `../extreme_heat_derate/`.

## What it answers (and what it refuses)

```text
ANSWERS   which hydro assets / owners / regions are directionally exposed to drought, low snowpack,
          low streamflow, or low reservoir storage · through what hydro mechanism that matters ·
          what public drought/snowpack/streamflow state can and cannot support · who should monitor it
REFUSES   exact plant-level MWh generation loss · exact revenue / LMP / PPA impact · forward
          return-period of low inflow · reservoir rule-curve / water-rights / dispatch claims without
          named evidence · single-cause attribution of a monthly hydro generation dip · outreach before the gate
```

## Scope

Hydropower assets (conventional hydro first; pumped storage only with a caveat) · one region / basin / market per test · operating assets · actors: owner-operator · investor · lender · offtaker.

Recommended first test: **California / CAISO hydro >= 50 MW**, scoped by `state="CA"` as a proxy and then checked against grid/region context where available. Hydro is basin-linked, so state/market is a first-pass screen, not a final hydrology boundary.

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
precipitation deficit / low snowpack / high evaporative demand
   -> lower runoff, streamflow, and reservoir storage
   -> lower hydro energy volume and/or reduced dispatch flexibility
   -> commercial relevance depends on timing, market price shape, contract terms, water rights,
      environmental flows, flood-control rules, maintenance, and facility type
```

The discipline: a dated drought / snowpack / streamflow source can ground a **regional condition**; it does not by itself ground a **plant-level MWh loss**.

## Procedure (the real tool sequence)

```text
1. external state: US Drought Monitor + NOAA/NIDIS/CPC drought outlook; where relevant, USGS streamflow,
                   NRCS SNOTEL / NOHRSC snowpack, and reservoir storage. Cite all dates.
2. mechanism:      state the hydro pathway and the missing operations bridge (reservoir, inflow, water rights, dispatch).
3. scope:          search_plants(fuel="hydro", state="<one state>", minMw=50) or equivalent hydro filter.
                   ⚠ ISO filters may be unwired (R1); use state/region proxy and confirm grid/regions.
4. drill:          get_plant(<id>) for capacity, location, owner, monthly generation/CF context, grid/region.
5. context:        use monthly generation as seasonality context only; do not read drought causality from one dip.
6. actor:          retrieve owner / optional offtaker context for portfolio and contract relevance.
7. draft:          assemble condition + scoped hydro assets + mechanism + evidence + confidence + caveat + actor relevance.
8. gate:           block exact MWh/$, forward probability, reservoir operations, and single-cause attribution.
```

## Allowed vs blocked claims

```text
ALLOWED  directional drought / low-hydro exposure for a scoped hydro fleet · dated regional drought,
         snowpack, streamflow, or storage condition · mechanism + caveats · owner / portfolio
         concentration · monitoring and planning recommendations
BLOCKED  exact plant-level MWh or $ impact · LMP / PPA impact from drought alone · forward return-period ·
         reservoir rule curve / water-rights / dispatch claims without a named source · single-cause generation
         attribution · national-from-regional · outreach
```

## Confidence + caveats

Confidence is **per-claim-part**:
- *Drought / snowpack / streamflow condition* can be **factual** when a dated source is cited.
- *Hydro fleet exposure in that geography* is usually **low/medium** because basin/reservoir linkage is imperfect.
- *Plant-level MWh or revenue impact* is **blocked** without inflow/storage/operations/dispatch data.
- **High is not reachable** on the public substrate alone.

Required caveats: hydro exposure is basin/reservoir-linked, not simply state-linked; monthly generation is context, not proof of drought causality; operations and non-power water obligations mediate output; climate non-stationarity caps trend and return-period claims.

## Actor relevance

Owner (reservoir scheduling, maintenance timing, hedging) · investor (portfolio concentration in low-water regions) · lender (DSCR sensitivity to low-water years) · offtaker (contracted hydro volume / shape risk where contract context exists).

---

**See also**: `resource.yml` (structured contract) · `knowledge.md` (mechanism + source stack) · `prompt_projection.md` (session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (target output) · `test_runs/test_run_001.md` (pending test record).
