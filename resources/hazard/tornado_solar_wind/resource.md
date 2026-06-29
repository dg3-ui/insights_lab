# Tornado Exposure For Solar, Wind, and Substation Assets — Method (human-readable)

> **Status**: draft 2026-06-29. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../flooding_multi_asset/`.

## What it answers (and what it refuses)

```text
ANSWERS   which solar/wind/substation assets sit in a tornado-climatology corridor (Tornado/Dixie Alley) ·
          the mechanism (extreme wind + debris → outright destruction in a narrow path) · the
          catastrophic-but-localized framing (total loss if hit, low per-asset intersection) · what a realized
          tornado meant regionally · who should care + what to harden
REFUSES   exact $ loss / EAL / payout · forward per-asset strike probability / return-period · per-plant damage
          from the CF series · single-cause CF attribution · which rows/turbines were destroyed (sub-plant
          geometry not in substrate) · outreach before the gate
```

## Scope

Solar + wind + transmission (substation) + battery (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = Southern Plains / OK–TX — the Tornado-Alley corridor) · operating + queue (siting) · actors: owner-operator · investor · lender · developer.

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
EXTREME WIND + DEBRIS LOADING → OUTRIGHT STRUCTURAL DESTRUCTION
    EF-scale winds (much higher than design-basis sustained wind) + airborne debris
    → arrays/trackers flattened, turbines snapped/toppled, substation equipment destroyed
    → TOTAL LOSS of assets inside the path → long-lead rebuild
    The defining property: the path is a few hundred meters wide. Damage is BINARY and NARROW —
    a strike is catastrophic, but the annual probability of any one asset being in the path is low.
```

This is the key contrast with the hurricane resource: a hurricane is a wide, days-long field that produces fleet-wide cut-out; a tornado is a point-strike total loss. **Do not annualize a total loss across the whole nameplate**, and do not treat touchdown density (an areal climatology) as a per-asset strike probability.

## Procedure (the real tool sequence)

```text
1. hazard state:  SPC tornado climatology (touchdown density) AND/OR search_news(category=hazards, query="tornado")  → VERIFY each
2. scope:         search_plants(fuel="solar"/"wind", state="OK"/"TX", minMw=50)   ⚠ NOT iso= → []; scope by state
3. footprint:     get_plant geometry/county + nearby_plants                       → assets in the climatology corridor
4. context only:  get_plant.generation                                           → ⚠ monthly CF cannot resolve a narrow strike; state this
5. actor:         get_plant.ownership                                            → owner chain + portfolio corridor accumulation
6. draft:         assemble the claim grammar; cap confidence; block the $ / strike-probability / per-plant-damage / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional tornado-corridor exposure · the destruction mechanism (cited) · the catastrophic-but-localized
         framing · realized tornado → corridor (regional fact) · owner/portfolio corridor accumulation ·
         mitigation (wind-class margins, debris-resistant racking, rebuild spares, diversification) recs
BLOCKED  exact $ / EAL / payout · forward per-asset strike probability / return-period · per-plant damage from CF ·
         single-cause CF · which rows/turbines destroyed · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *mechanism + tornado-climatology exposure* reaches **Medium**; a *realized tornado near a scoped asset* is **factual as a regional event**; any *CF read* is **Low/blocked**. **High is not reachable** on the substrate alone (would need a verified post-event EF survey of the asset, or a served tornado-hazard model).

Required caveats: damage is binary and narrow (don't annualize a total loss across nameplate); touchdown density is areal, not per-asset; sub-plant geometry not in substrate; monthly CF can't resolve a narrow strike; tornado trends are weakly attributable (cap at directional); $ severity not modeled (model-gpr).

## Actor relevance

Owner (rapid-rebuild spares + restoration planning; debris-resistant racking + wind-class margins; deductible exposure) · investor (portfolio corridor accumulation; single-site total-loss tail vs diversification; convective reinsurance cost) · lender (single-asset total-loss tail — directional; property/wind insurance adequacy) · developer (siting + wind-class/debris-resistant design + geographic spread).

---

**See also**: `resource.yml` · `knowledge.md` (the mechanism + EF-scale basis + corridor anchors) · `prompt_projection.md` · `data_requirements.md` · sibling resources `../hail_solar/`, `../hurricane_high_wind_wind/`, `../extreme_cold_winter_storm/`, `../wildfire/`, `../flooding_multi_asset/`.
