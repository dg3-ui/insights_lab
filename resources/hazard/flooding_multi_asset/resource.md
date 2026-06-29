# Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets — Method (human-readable)

> **Status**: draft 2026-06-29. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`.

## What it answers (and what it refuses)

```text
ANSWERS   which thermal/solar/wind/grid assets sit in a flood-exposed geography (coastal, riverine, FEMA zone) ·
          through what mechanism by asset (switchyard inundation → outage; fuel/equipment inundation → forced
          outage + damage; cooling-intake compromise at a water-sited thermal plant) · what a realized flood
          meant regionally for assets in the watershed · who should care + what to harden
REFUSES   exact $ loss / EAL / insurance payout · forward inundation probability / return-period · per-plant
          damage attribution from the CF series · single-cause attribution of a CF change · which pads/feeders
          went underwater (site elevation not in substrate) · outreach before the gate
```

## Scope

Thermal (gas, nuclear) + solar + wind + transmission + battery (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = Gulf Coast / Texas — the Harvey-corridor floodplain) · operating + queue (siting/elevation) · actors: owner-operator · investor · lender · developer.

## Mechanism — THREE claim types (cite `knowledge.md`; do not re-derive)

```text
(A) GRID / SWITCHYARD — INUNDATION OUTAGE
    floodwater reaches low-lying substation / switchyard / collector → de-energization
    → outage for the inundation window + dry-out/inspection → recovery days-to-weeks
    A DELIVERY failure: the plant may be undamaged but cannot export.

(B) PLANT EQUIPMENT / FUEL STORAGE — FORCED OUTAGE + DAMAGE
    floodwater reaches ground-level inverters / combiners / fuel tanks / pad electrical
    → forced outage + physical damage → long-lead component replacement
    A site-equipment loss; severity scales with pad elevation (a field NOT in the substrate).

(C) WATER-SITED THERMAL — COOLING-INTAKE COMPROMISE
    a plant sited at tidewater / riverbank for cooling can have its intake, screens, or
    pump house compromised by debris-laden floodwater → derate or trip
    The structural insight: thermal/nuclear cooling siting CONCENTRATES flood exposure.
```

The exposure is set by **site elevation relative to the flood surface** — which the substrate does not carry. A plant inside a FEMA zone may still be pad-elevated or flood-walled. Claims stay geographic and directional.

## Procedure (the real tool sequence)

```text
1. hazard state:  FEMA NFHL flood zone (geography) + NWS AHPS / USGS gauge history AND/OR search_news(category=hazards, query="flood")  → VERIFY each
2. scope:         search_plants(fuel="gas"/"solar"/..., state="TX", minMw=50)   ⚠ NOT iso= → []; scope by state
3. footprint:     get_plant geometry/county + nearby_plants                      → assets in the same floodplain / watershed
4. context only:  get_plant.generation                                          → ⚠ monthly CF cannot isolate an inundation outage; state this
5. actor:         get_plant.ownership                                           → owner chain + portfolio floodplain accumulation
6. draft:         assemble the claim grammar; cap confidence; block the $ / probability / per-plant-damage / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional flood exposure · the three mechanisms by asset (cited) · realized flood → watershed (regional fact) ·
         water-sited thermal concentration · owner/portfolio floodplain accumulation · mitigation (pad elevation, berms) recs
BLOCKED  exact $ / EAL / payout · forward inundation probability / return-period · per-plant damage from CF ·
         single-cause CF · which pads/feeders flooded · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *mechanism + flood-geography exposure* reaches **Medium** (FEMA/NWS/USGS + resolved scope); a *realized flood near a scoped asset* is **factual as a regional event**; any *CF read* is **Low/blocked**. **High is not reachable** on the substrate alone (would need a verified per-plant inundation record or a served flood model with site elevation).

Required caveats: three mechanisms stated and distinguished by asset; exposure is driven by site elevation (not in substrate); monthly CF cannot isolate an inundation outage; flood classification is VERIFIED; water-sited thermal concentration is structural; $ severity is not modeled (model-gpr).

## Actor relevance

Owner (pad elevation + flood-barrier investment; cooling-intake resilience; long-lead transformer planning) · investor (portfolio floodplain accumulation; rising flood-insurance cost + FEMA remapping) · lender (DSCR stress from a flood outage — directional; FEMA zone + insurance adequacy as underwriting inputs) · developer (siting outside the floodplain; equipment-pad elevation spec).

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + three mechanisms + flood-of-record anchors) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `../hail_solar/` · `../hurricane_high_wind_wind/` · `../extreme_cold_winter_storm/` · `../wildfire/` · `../sea_level_rise_surge/` (sibling hazard resources).
