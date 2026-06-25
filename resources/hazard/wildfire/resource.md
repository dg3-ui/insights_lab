# Wildfire Exposure For Solar, Transmission, and Grid-Connected Assets — Method (human-readable)

> **Status**: draft 2026-06-25. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`.

## What it answers (and what it refuses)

```text
ANSWERS   which solar / transmission / grid-connected assets sit in a fire-weather-exposed geography
          (Western WUI, California) · through what mechanism by asset (smoke/ash → solar irradiance
          reduction; heat/flame → transmission corridor damage; PSPS → curtailment of healthy generation) ·
          what a realized fire event or PSPS meant regionally for exposed assets · who should care + what to harden
REFUSES   exact $ ignition liability or structure loss · forward ignition probability / return-period ·
          per-plant smoke-output attribution from the CF series · single-cause CF attribution (the
          summer/fall dip is NOT separable from seasonal variation) · whether a specific line caused / will
          cause ignition · outreach before the gate
```

## Scope

Solar + transmission + any grid-connected generation on a PSPS-eligible circuit (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = CAISO/California — the primary PSPS jurisdiction) · operating + queue (siting/fire-risk-aware interconnection) · actors: owner-operator · investor · lender · developer.

## Mechanism — THREE claim types (cite `knowledge.md`; do not re-derive)

```text
(A) SOLAR — SMOKE/ASH → IRRADIANCE REDUCTION + SOILING
    smoke column reduces DNI/DHI → output drops proportionally to smoke optical depth (20–80%+)
    ash deposits on panel glass → soiling → additional output reduction until cleaned
    → temporary, partial output reduction. NOT structural damage in most cases.

(B) TRANSMISSION — HEAT + FLAME → CORRIDOR DAMAGE + IGNITION LIABILITY
    flame contact with ROW → conductor flashover / sag / tower failure → transmission outage →
    downstream generators lose interconnection → repair weeks-to-months.
    IGNITION LIABILITY: the line STARTS the fire (Camp Fire mechanism) — a separate, high-severity
    tail risk; BLOCKED here (model-gpr / legal).

(C) GRID-CONNECTED GENERATION — PSPS → CURTAILMENT OF HEALTHY GENERATION
    utility de-energizes circuits during extreme fire-weather (red-flag) to prevent ignitions
    → all generators on the circuit are curtailed, regardless of direct fire risk
    → the asset is physically undamaged; interconnection is offline → zero export
    → temporary revenue loss (1–5 days). Fuel type irrelevant; circuit location determines exposure.
```

**Correlated in space, distinct in claim type** — a fire or fire-weather event can trigger all three simultaneously. The discipline is not conflating them.

## Procedure (the real tool sequence)

```text
1. hazard state:  NIFC fire perimeter (geography) AND/OR CAISO PSPS event AND/OR
                  search_news(category=hazards, query="wildfire"/"fire"/"PSPS") → VERIFY each classification
2. mechanism:     state WHICH claim type (A/B/C) applies for each asset class in scope — do not conflate
3. scope:         search_plants(fuel="solar"/"wind"/"gas", state="CA", minMw=50)
                  ⚠ NOT iso="CAISO" → likely [] (same R1 gap as other resources); scope by state
4. footprint:     get_plant geometry/county + nearby_plants → place assets in the fire corridor or PSPS zone
5. context:       get_plant.generation → CONTEXT ONLY; state monthly CF cannot isolate a smoke event from
                  seasonal irradiance variation or maintenance
6. actor:         get_plant.ownership → owner chain + portfolio fire-geography accumulation
7. draft:         assemble; split confidence (exposure vs realized event vs CF context); block $ / ignition
                  liability / forward probability / per-plant smoke attribution / single-cause CF
```

## Allowed vs blocked claims

```text
ALLOWED  directional fire-weather / wildfire exposure for a scoped asset set / geography · the THREE
         mechanisms by asset (cited) · a named fire / PSPS event affected a named geography near a
         scoped asset (REGIONAL fact) · PSPS as an operability + revenue risk · owner/portfolio
         fire-geography accumulation · mitigation recs (cleaning schedules, ROW vegetation mgmt, PSPS
         notification protocols, site ember-hardening)
BLOCKED  exact $ ignition liability / structure loss / EAL / payout · forward ignition probability /
         return-period · per-plant smoke-output attribution from CF · single-cause CF attribution (the
         summer/fall dip ≠ smoke) · whether a specific line caused / will cause ignition · national-from-
         regional · outreach
```

## Confidence + caveats

Confidence is **per-claim-part**:
- *Fire-weather-geography exposure + mechanism by asset* — **Medium** (clear geography, robust physics, NIFC/CAISO documented).
- *A named fire or PSPS event affected a named geography near a scoped asset* — **factual** as a regional event (NIFC + CAISO/hazards news), but NOT a per-plant damage or output claim.
- *Any read of the fire/smoke into the CF series* — **Low / blocked** (monthly CF cannot isolate a smoke event from seasonal variation).
- **High is not reachable** on the substrate alone (would need a verified per-plant smoke-impact or PSPS-curtailment record, or a served fire-risk peril model).

Required caveats: THREE mechanisms stated and distinguished by asset; monthly CF cannot isolate smoke from seasonal variation; PSPS curtailment ≠ physical fire damage; ignition liability is blocked (model-gpr/legal); fire-weather intensification is directional, not a return-period; $ severity is not modeled (model-gpr).

## Actor relevance

Owner (PSPS notification + backup planning; panel cleaning; ROW vegetation management; ember-hardening) · investor (portfolio WUI / CAISO fire-geography accumulation; PSPS as recurring revenue risk; tightening CA wildfire insurance market) · lender (DSCR stress from PSPS curtailment — directional; transmission-owner ignition liability as collateral tail risk) · developer (siting outside high-WUI zones; fire-resistant panel spec; PSPS-aware interconnection circuit selection).

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + three mechanisms + Camp Fire / PSPS anchors) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (the target output) · `test_runs/test_run_001.md` (the live test record) · `../hail_solar/` · `../hurricane_high_wind_wind/` · `../extreme_cold_winter_storm/` (sibling hazard resources).
