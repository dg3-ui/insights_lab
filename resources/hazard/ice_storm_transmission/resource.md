# Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets — Method (human-readable)

> **Status**: draft 2026-06-29. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../extreme_cold_winter_storm/` (the GENERATION-side freeze), `../hail_solar/`, `../hurricane_high_wind_wind/`, `../wildfire/`, `../flooding_multi_asset/`, `../tornado_solar_wind/`, `../sea_level_rise_surge/`, `../lightning_multi_asset/`.

## What it answers (and what it refuses)

```text
ANSWERS   which transmission corridors / wind assets / delivery-dependent generators sit in the ice belt ·
          the mechanism (ice-load → conductor/tower failure on transmission — the primary hazard; blade icing →
          wind shutdown; distribution downing → healthy generation stranded behind the break) · what a realized
          ice storm meant for the grid + assets regionally · who should care + what to harden
REFUSES   exact $ loss / restoration cost / payout · forward ice-load probability / return-period · per-span or
          per-plant attribution from the CF series · single-cause CF attribution · which spans/towers collapsed
          (line ratings not in substrate) · outreach before the gate
```

## Scope

Transmission (primary) + wind + solar / gas / battery (delivery-dependent) (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = South-Central ice belt / OK–TX–AR) · operating + queue (siting/interconnection) · actors: owner-operator · investor · lender · developer.

## Mechanism — THREE claim types (cite `knowledge.md`; do not re-derive)

```text
(A) TRANSMISSION — ICE-LOAD MECHANICAL FAILURE  [the PRIMARY hazard]
    freezing rain accretes ice on conductors + towers → mechanical load exceeds rating
    → conductor break / tower collapse → delivery outage → capital-intensive rebuild (days-to-weeks)

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN
    ice on blades → rotor imbalance + vibration → control system shuts down → zero output for the icing window
    A TEMPORARY loss (shared with extreme_cold_winter_storm — framed here as part of the delivery picture).

(C) DELIVERY-DEPENDENT — STRANDING BEHIND A DOWNED LINE
    a physically UNDAMAGED generator cannot export when the line/distribution network feeding the grid is down
    → revenue loss with NO physical-damage claim. The defining property of this hazard.
```

The key framing: this is primarily a **delivery-infrastructure** hazard — the loss is often **grid-side, not plant-side**. Distinguish physical generation damage from delivery stranding. The generation-side freeze mechanisms (gas wellhead/pipeline freeze → forced outage) live in `extreme_cold_winter_storm` — cross-reference, do not double-count. Conductor / tower ice-load ratings are **not in the substrate**, so claims stay at geographic ice-belt exposure.

## Procedure (the real tool sequence)

```text
1. hazard state:  NOAA NWS freezing-rain climatology + SPIA ice-accumulation index AND/OR search_news(category=hazards, query="ice storm")  → VERIFY each
2. scope:         search_plants(fuel="wind"/..., state="OK"/"TX"/"AR", minMw=50) + transmission corridor   ⚠ NOT iso= → []; scope by state
3. footprint:     get_plant geometry/county + nearby_plants                       → assets + delivery path in the ice belt
4. context only:  get_plant.generation                                           → ⚠ monthly CF cannot isolate an ice-storm outage from winter seasonal pattern; state this
5. actor:         get_plant.ownership                                            → owner chain + portfolio ice-belt accumulation (incl. transmission)
6. draft:         assemble the claim grammar; cap confidence; block the $ / probability / per-span-or-plant / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional ice-storm exposure · the three mechanisms (cited) · the delivery-infrastructure framing
         (healthy generator stranded, no physical damage) · realized ice storm → corridor/grid (regional fact) ·
         owner/portfolio ice-belt accumulation · mitigation (ice-load design, line/blade de-icing, redundant paths) recs
BLOCKED  exact $ / restoration cost / payout · forward ice-load probability / return-period · per-span or per-plant
         attribution from CF · single-cause CF · which spans/towers collapsed · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *mechanism + ice-belt exposure* reaches **Medium**; a *realized ice storm near a scoped asset / corridor* is **factual as a regional event**; any *CF read* is **Low/blocked**. **High is not reachable** on the substrate alone (would need a verified per-line/per-asset outage record, or a served ice-load model with conductor/tower ratings).

Required caveats: three mechanisms distinguished; primarily a delivery-infrastructure hazard (loss is grid-side; distinguish damage from stranding; generation-side freeze lives in the winter-storm resource); conductor ratings not in substrate; monthly CF can't isolate an ice-storm outage; freezing-rain trends contested (cap at directional); $ + restoration cost not modeled (model-gpr).

## Actor relevance

Owner (transmission: ice-load design, line de-icing, vegetation management, restoration spares; generators: delivery-path redundancy + blade de-icing; stranding awareness) · investor (portfolio ice-belt accumulation incl. transmission; delivery-stranding as recurring revenue risk; T&D restoration-cost exposure) · lender (DSCR stress from stranding or T&D damage — directional; transmission restoration-cost exposure) · developer (interconnection-corridor ice-load design + delivery redundancy + blade-heating spec).

---

**See also**: `resource.yml` · `knowledge.md` (the cited "why" + three mechanisms + ice-belt + ice-storm anchors) · `prompt_projection.md` · `data_requirements.md` · `../extreme_cold_winter_storm/` (the GENERATION-side freeze) · sibling hazard resources.
