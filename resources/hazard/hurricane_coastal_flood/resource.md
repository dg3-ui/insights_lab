# Hurricane Coastal Flood / Storm-Surge Exposure For Energy Assets — Method

> **Status**: draft 2026-06-25. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../../docs/method/resource_standard.md`. Sibling hazard resource: `../hurricane_high_wind_wind/`.

## What it answers (and what it refuses)

```text
ANSWERS   which coastal energy assets / owners / regions sit in storm-surge or coastal-flood exposed
          geographies · through what component pathway water matters · what a named storm or surge
          product can support regionally · who should harden / diligence the exposure
REFUSES   exact site flood depth · exact $ / EAL / PML / insurance payout · exact outage duration ·
          plant-level monthly-generation attribution · equipment damage without a verified record ·
          wind-vs-water insurance coverage outcome · outreach before the gate
```

## Scope

Coastal solar, wind, gas, battery, transmission/substation, and other grid-connected assets · one coastal geography and one primary asset class per test · operating + queue · actors: owner-operator · investor · lender · developer.

Recommended first test: **Texas Gulf Coast / Houston-Galveston energy cluster**, with one primary asset class selected before drafting.

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
hurricane / coastal storm
   -> storm surge + tide + waves + rainfall / drainage backup
   -> water reaches critical component (substation, transformer, inverter pad, switchgear, access road, fuel/cooling system)
   -> outage / damage / delayed restoration depending on water depth, salinity, component elevation, spares, access
```

The discipline: **water at component elevation** is the real mechanism. Plant county / centroid / flood-zone screen is not an inundation model.

## Procedure (the real tool sequence)

```text
1. hazard state:  NHC track / surge product + FEMA NFHL/FIS + SLOSH/P-Surge or tide-gage / local surge source.
2. mechanism:     state the component pathway for the asset class in scope (substation, inverter, access, fuel/cooling, etc.).
3. scope:         resolve one coastal asset set via MCP (state/county/nearby anchor; one primary fuel/technology).
4. footprint:     get_plant geometry/county + nearby_plants for same coastal cluster; use external flood/surge sources for footprint.
5. context:       get_plant.generation monthly CF is context only; do not read surge outage from it.
6. actor:         retrieve owner/company context for accumulation and lender/developer relevance.
7. draft:         assemble condition + scope + mechanism + evidence + confidence + caveat + actor relevance.
8. gate:          block exact depth, $, outage duration, damage attribution, insurance outcome, and national claims.
```

## Allowed vs blocked claims

```text
ALLOWED  directional coastal-flood / storm-surge exposure for a scoped coastal asset set · component
         mechanism statements · named storm / surge affected a regional geography near scoped assets ·
         owner / portfolio accumulation · monitoring / hardening recommendations
BLOCKED  exact flood depth / EAL / PML / $ / insurance payout · exact outage duration · monthly-CF
         attribution · equipment damage without verified record · wind-vs-water coverage outcome ·
         national-from-regional · outreach
```

## Confidence + caveats

Confidence is **per-claim-part**:
- *Storm track / regional surge / flood-zone context* can be **factual/medium** when dated sources are cited.
- *Scoped asset exposure* is usually **low/medium** because elevation, component location, and flood-zone joins are missing.
- *Plant damage, outage duration, or $ impact* is **blocked** without verified event and component data.
- **High is not reachable** on the substrate alone.

Required caveats: flood exposure is elevation/component-specific; FEMA/SLOSH products frame exposure but do not prove damage; monthly generation cannot isolate surge outage; wind and water are distinct claim types; $ and insurance outcomes are not modeled.

## Actor relevance

Owner (hardening, equipment elevation, drainage, access/recovery) · investor (coastal portfolio accumulation) · lender (collateral/DSCR sensitivity and insurance uncertainty) · developer (siting, pad/substation elevation, drainage, flood barriers, interconnection resilience).

---

**See also**: `resource.yml` (structured contract) · `knowledge.md` (mechanism + source stack) · `prompt_projection.md` (session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (target output) · `test_runs/test_run_001.md` (pending test record).
