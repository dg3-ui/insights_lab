# Lightning Exposure For Wind, Solar, and Electrical-Plant Assets — Method (human-readable)

> **Status**: draft 2026-06-29. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../flooding_multi_asset/`, `../tornado_solar_wind/`.

## What it answers (and what it refuses)

```text
ANSWERS   which wind/solar/electrical-plant assets sit in a high-flash-density geography · the mechanism (direct
          strike to blade/nacelle/structure — tall wind turbines most exposed; vs induced surge into inverters /
          transformers / control electronics) · the high-frequency / lower-severity framing (cumulative component
          risk + design adequacy) · what a realized event meant regionally · who should harden
REFUSES   exact $ loss / EAL / payout · forward strike rate / component-failure probability · per-plant damage from
          the CF series · single-cause CF attribution · whether a given asset has an adequate LPS (status not in
          substrate) · outreach before the gate
```

## Scope

Wind + solar + gas + transmission + battery (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = Gulf Coast / FL–TX — the US flash-density maximum) · operating + queue (siting/design) · actors: owner-operator · investor · lender · developer.

## Mechanism — TWO claim types (cite `knowledge.md`; do not re-derive)

```text
(A) DIRECT STRIKE — STRUCTURE / BLADE / NACELLE
    a cloud-to-ground strike attaches to the tallest object → blade composite damage, nacelle / control
    damage, tower current path → component outage → repair (hours-to-weeks for a blade)
    Wind turbines are the tallest structures in open terrain → the most direct-strike-exposed class.

(B) INDUCED SURGE — INVERTERS / TRANSFORMERS / CONTROL ELECTRONICS
    a nearby strike couples a fast transient into wiring → inverter / transformer / SCADA / BMS damage
    → component outage across ANY generation type → replacement
    The mechanism that hits solar, gas, battery, and substation electronics even without a direct hit.
```

The defining property versus the other hazards: lightning is **high-frequency, lower-per-event-severity**, managed by **design** (air termination, surge protective devices, grounding, blade LPS receptors). Frame it as cumulative component risk + design adequacy, not a single catastrophe. LPS status is **not in the substrate**, so claims stay at geographic flash-density exposure.

## Procedure (the real tool sequence)

```text
1. hazard state:  NLDN cloud-to-ground flash-density climatology (geography) AND/OR search_news(category=hazards, query="lightning")  → VERIFY each
2. scope:         search_plants(fuel="wind"/"solar", state="FL"/"TX", minMw=50)   ⚠ NOT iso= → []; scope by state
3. footprint:     get_plant geometry/county + nearby_plants (hub height frames wind exposure)  → assets in the flash-density band
4. context only:  get_plant.generation                                            → ⚠ monthly CF cannot resolve a component strike; state this
5. actor:         get_plant.ownership                                             → owner chain + portfolio flash-density accumulation
6. draft:         assemble the claim grammar; cap confidence; block the $ / strike-rate / per-plant-damage / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional lightning exposure · the direct-strike vs induced-surge distinction (cited) · the
         high-frequency/lower-severity cumulative-component framing · realized event → area (regional fact) ·
         owner/portfolio flash-density accumulation · mitigation (LPS, SPDs, grounding, blade-receptor) recs
BLOCKED  exact $ / EAL / payout · forward strike rate / failure probability · per-plant damage from CF ·
         single-cause CF · whether an asset's LPS is adequate · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *mechanism + flash-density exposure* reaches **Medium**; a *realized lightning event near a scoped asset* is **factual as a regional event**; any *CF read* is **Low/blocked**. **High is not reachable** on the substrate alone (would need a verified per-asset strike/maintenance record, or a served strike-rate model with LPS status).

Required caveats: two mechanisms distinguished (direct strike vs induced surge); high-frequency/lower-severity → cumulative component risk, not a catastrophe; LPS status not in substrate; monthly CF can't resolve a component strike; lightning trends weakly attributable (cap at directional); $ severity not modeled (model-gpr).

## Actor relevance

Owner (LPS + SPD inspection/upgrade; blade-receptor maintenance; inverter/transformer spares) · investor (portfolio flash-density accumulation; cumulative O&M / availability drag; deductible exposure) · lender (cumulative availability/O&M drag — directional; equipment-breakdown insurance adequacy) · developer (siting + LPS / surge-protection design spec).

---

**See also**: `resource.yml` · `knowledge.md` (the cited "why" + direct-strike / induced-surge mechanisms + flash-density basis) · `prompt_projection.md` · `data_requirements.md` · sibling hazard resources.
