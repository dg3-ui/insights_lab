# Prompt Projection — Hurricane / High-Wind Exposure For Wind Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the hurricane/high-wind method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage, an insurance payout, or a hurricane return-period. Do not claim a hurricane caused a capacity-factor dip.

## Task

Draft one hurricane / high-wind exposure insight for one scoped wind asset set. Recommended first scope:

```text
Coastal / Gulf ERCOT / Texas wind ≥ 50 MW   (resolve via state="TX", then filter to coastal counties; the iso filter is unwired — see step 3)
```

## Mechanism (cite `knowledge.md`; do not re-derive) — the TWO claim types

```text
(A) TEMPORARY CUT-OUT   wind ≥ ~25 m/s → blades feather + rotor shuts down (by design) → ~zero output DURING the
                        storm → restarts + recovers. A short availability loss, NOT damage. The common case.
(B) LASTING DAMAGE      Cat 3+ gusts exceed the turbine design wind class → blade/nacelle/tower loss; coastal sites
                        add storm-surge → weeks-to-months outage. The rare, capital case.
```

Geography is **coastal + climatological**, not a dated forecast. The TX Gulf Coast is in the US landfalling-hurricane corridor (NHC). **Hurricane Beryl made TX landfall ~Cat 1 (2024-07-08, near Matagorda)** — the cut-out (A) regime, NOT the damage (B) regime.

## Required reasoning steps

```text
1. Establish the hurricane geography (NHC track / HURDAT2) AND/OR a realized storm (search_news category=hazards, query="hurricane" or storm name).
   ⚠ VERIFY each hazards article — the classifier has false positives, AND TX hurricane articles link to NUCLEAR/HYDRO/GAS plants, not WIND (don't trust the label).
2. State the mechanism + name WHICH claim type (temporary cut-out vs lasting damage). Default to cut-out for a Cat 1–2 landfall.
3. Resolve assets:  search_plants(fuel="wind", state="TX", minMw=50)
   ⚠ NOT iso="ERCOT" (returns []). Scope by state; then filter to COASTAL counties (Cameron, Willacy, Kenedy, Nueces, San Patricio, Matagorda, Brazoria, …) via get_plant.county / lat-lon.
4. Place assets in the corridor: get_plant geometry/county + turbine_locations + nearby_plants (same coastal corridor).
5. CONTEXT ONLY: get_plant.generation monthly CF. ⚠ DO NOT read the storm into it — the July dip IS the summer wind lull (a Beryl cut-out is invisible at monthly resolution). State this explicitly.
6. Retrieve owner chain for actor relevance + coastal-portfolio accumulation.
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block the $ loss, the forward probability, the plant-level forecast, single-cause CF attribution, and lasting-damage-from-a-sub-Cat-3-storm.
```

## Allowed claims

- Directional coastal hurricane / high-wind exposure for a scoped wind set / geography.
- The cut-out-vs-damage mechanism (cited), naming which claim type applies.
- Realized event framing: a named storm made landfall in the corridor near a named coastal wind asset (a **regional** fact, not a wind-plant damage claim).
- Owner / portfolio coastal-accumulation in the hurricane corridor.
- Mitigation + monitoring/hardening recommendations (feather/shutdown protocol, design wind class, surge siting).

## Blocked claims

- Exact $ damage / EAL / PML / insurance payout from a hurricane.
- Forward hurricane probability or return-period from track history alone.
- Plant-level generation forecasts without modeling.
- Single-cause attribution (a hurricane caused an observed CF change — the July dip ≠ Beryl).
- Lasting structural damage from a sub-Cat-3 storm (Beryl was Cat 1 → cut-out, not widespread damage).
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — NOT reachable on the substrate alone (would need a verified wind-plant damage record, which the substrate lacks, or a served TC hazard model).
- **Medium** — mechanism + coastal-corridor exposure on a clear geography (NHC landfall + resolved coastal wind scope), with the cut-out/damage distinction stated.
- **Low** — forward / probabilistic exposure without a TC model; OR any event-context claim leaning on monthly CF.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / return-period / plant-level forecast / single-cause-CF claim requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part — the exposure vs the realized event vs the CF context differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
