# Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets — Method (human-readable)

> **Status**: draft 2026-06-24. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hail_solar/`, `../hurricane_high_wind_wind/`.

## What it answers (and what it refuses)

```text
ANSWERS   which thermal/wind/solar assets sit in a freeze-exposed geography (Southern plains, Gulf Coast) ·
          through what mechanism by fuel (wellhead/pipeline freeze → gas curtailment → thermal outage;
          blade icing → wind shutdown; snow cover → solar reduction) · what Winter Storm Uri (Feb 2021)
          meant regionally for the ERCOT fleet · who should care + what to harden
REFUSES   exact $ loss / EAL / insurance payout · forward return-period of a Uri-class event · per-plant
          outage attribution from the CF series · plant winterization status without a named source · single-cause
          attribution of a CF change (the Feb dip IS the seasonal minimum) · which specific wells/pipes froze ·
          wind icing / solar snow-loss magnitude without sub-monthly data · outreach before the gate
```

## Scope

Thermal (gas) + wind + solar (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = ERCOT/Texas — the Uri epicenter) · operating + queue (siting/winterization) · actors: owner-operator · investor · lender · developer.

## Mechanism — THREE claim types (cite `knowledge.md`; do not re-derive)

```text
(A) GAS / THERMAL — FORCED OUTAGE
    wellhead + pipeline freeze → gas supply curtailment; plant instrumentation freeze → independent forced trip
    → zero output for the freeze window (days) → recovery hours-to-days after thawing
    NOT equipment damage — a supply and operability failure from missing cold-weather packages.
    Uri mechanism: ~87% of the ~32 GW ERCOT outage at peak (FERC/NERC 2021).

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN
    ice accumulates on blades → rotor imbalance + vibration → control system shuts down
    → zero output for the icing window (hours-to-days)
    → restarts once ice melts or active de-icing engages. A TEMPORARY loss, similar to the hurricane cut-out.

(C) SOLAR — SNOW COVER + SHORT DAYLIGHT → OUTPUT REDUCTION
    snow blocks irradiance → partial output reduction (self-clears in hours-to-days)
    short winter daylight hours reduce the daily production window regardless of snow
    A SOFT, OFTEN TEMPORARY effect. Rarely a sustained outage.
```

The **correlated, systemic** nature of a polar-vortex event is what distinguishes extreme cold from other hazards — mechanisms A, B, and C can occur simultaneously across an entire region. Uri produced all three.

## Procedure (the real tool sequence)

```text
1. hazard state:  NOAA/NCEI storm record + GHCN-Daily station context + FERC/NERC Uri report (geography/mechanism) AND/OR
                  search_news(category=hazards, query="winter storm"/"Uri"/"freeze") → VERIFY each classification
2. system:        ERCOT post-event / operating reports for system timeline only; do not infer plant outages unless unit data exists
3. scope:         search_plants(fuel="gas"/"wind"/"solar", state="TX", minMw=50); filter to freeze-exposed geography
                  ⚠ NOT iso="ERCOT" → [] (R1); scope by state, then confirm grid/regions where available
4. mechanism:     state WHICH claim type (A/B/C) applies for each fuel in scope — do not conflate
5. footprint:     get_plant geometry/county + nearby_plants → build the fleet picture in the freeze corridor
6. context:       get_plant.generation → CONTEXT ONLY; state monthly CF cannot isolate a forced outage from the seasonal minimum
7. actor:         get_plant.ownership → owner chain + portfolio winterization-risk accumulation
8. draft:         assemble; split confidence; block the $ / return-period / per-plant attribution / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional freeze / winter-storm exposure for a scoped fleet and geography · the THREE mechanisms by fuel
         (cited) · Uri as a regional event (~32 GW ERCOT outage, FERC/NERC — a fact, not a per-plant claim) ·
         winterization gap as a structural vulnerability · owner/portfolio accumulation · mitigation recs
         (cold-weather packages, heat tracing, firm gas contracts, blade de-icing)
BLOCKED  exact $ / EAL / payout · forward probability / return-period · per-plant outage attribution from CF series ·
         plant winterization status without a named source · wind icing / solar snow-loss magnitude without sub-monthly
         generation + weather/snow/icing data · single-cause CF attribution (the Feb dip ≠ Uri) · which specific
         wells/pipes froze · national-from-regional · outreach
```

## Confidence + caveats

Confidence is **per-claim-part**:
- *Freeze-geography exposure + mechanism by fuel* — **Medium** (clear geography, robust physics, FERC/NERC documented for Uri).
- *Uri caused ~32 GW ERCOT thermal outage at peak* — **factual** as a regional event (FERC/NERC), but it is **not** a per-plant damage or outage claim.
- *Any read of Uri into the CF series* — **Low / blocked** (monthly CF cannot isolate a forced outage from the seasonal minimum).
- **High is not reachable** on the substrate alone (would need a verified per-plant outage record or a served cold-weather peril model).

Required caveats: the THREE mechanisms stated and distinguished by fuel; monthly CF cannot isolate a forced outage from the seasonal minimum; per-plant attribution blocked without an outage record; winterization status and fuel-supply provenance are unknown unless a named source reports them; Uri was a tail event (polar vortex displacement) and forward return-period requires a climate model; winterization gap is concentrated in Southern-latitude plants, not universal; $ severity is not modeled (model-gpr).

## Actor relevance

Owner (cold-weather package investment; wellhead heat-tracing; firm gas contracts; blade de-icing spec) · investor (portfolio freeze-geography accumulation; correlated revenue + fuel-cost exposure during a scarcity event) · lender (DSCR stress from a freeze-driven multi-day outage — directional; winterization status as an underwriting input) · developer (cold-weather-package spec for queue-stage thermal and wind in freeze-exposed geographies).

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + the three mechanisms + the Uri anchor) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (the target output) · `test_runs/test_run_001.md` (the live test record) · `../hail_solar/` · `../hurricane_high_wind_wind/` (sibling hazard resources).
