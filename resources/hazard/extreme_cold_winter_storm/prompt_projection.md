# Prompt Projection — Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the extreme-cold / winter-storm method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage or an insurance payout. Do not claim a winter event caused a capacity-factor dip.

## Task

Draft one extreme-cold / winter-storm exposure insight for one scoped asset set. Recommended first scope:

```text
ERCOT / Texas thermal (gas) fleet ≥ 50 MW   (resolve via state="TX", fuel="gas"; the iso filter is unwired — see step 3)
Optionally fan out to wind and/or solar in the same geography for the correlated systemic picture.
```

## Mechanism — THREE claim types by fuel (cite `knowledge.md`; do not re-derive)

```text
(A) GAS / THERMAL — FORCED OUTAGE
    wellhead + pipeline freeze → gas supply curtailment; instrument freeze → independent forced trip
    → zero output for the freeze window (days). NOT equipment damage — a supply/operability failure.
    Uri: ~87% of the ~32 GW ERCOT peak outage (FERC/NERC 2021-11).

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN
    ice on blades → rotor imbalance + vibration alarm → control system shuts down (by design)
    → zero output for the icing window (hours-to-days). TEMPORARY, similar to the hurricane cut-out.

(C) SOLAR — SNOW COVER + SHORT DAYLIGHT → OUTPUT REDUCTION
    snow blocks irradiance → partial, often brief reduction. Short daylight reduces the daily window.
    A SOFT, OFTEN TEMPORARY effect. Rarely a sustained outage.
```

The correlated systemic nature of a polar-vortex event — mechanisms A, B, and C simultaneously across an entire region — is the key analytical point. **Winter Storm Uri (February 10–20, 2021)** is the canonical realized case (FERC/NERC).

## Required reasoning steps

```text
1. Establish the freeze geography (NOAA NWS / NCEI Storm Events / GHCN-Daily station data) AND/OR a realized event:
   search_news(category=hazards, query="Uri"/"winter storm"/"freeze") → VERIFY each (check fuel classification;
   articles may link to grid-customer outages or the wrong fuel class).
2. Cite FERC/NERC for Uri's regional mechanism + outage scale; cite ERCOT only for system-level operations unless
   unit-level data is available. Use NOHRSC/SNODAS/IMS only for snow/ice context.
3. State WHICH mechanism (A/B/C) applies for each fuel in scope. Do not conflate.
4. Resolve assets:  search_plants(fuel="gas", state="TX", minMw=50)  [+ wind/solar if in scope]
   ⚠ NOT iso="ERCOT" (returns []). Scope by state; confirm grid/regions where available.
5. Place assets in the corridor: get_plant geometry/county + nearby_plants.
6. CONTEXT ONLY: get_plant.generation monthly CF. ⚠ DO NOT read the freeze into it — a February CF dip IS the
   seasonal minimum and cannot isolate a Uri-driven outage. State this explicitly.
7. Retrieve owner chain for actor relevance + portfolio winterization-risk accumulation.
8. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
9. Cap confidence at the weakest link; block the $ loss, the forward probability, the per-plant outage
   attribution, and the single-cause CF claim.
```

## Allowed claims

- Directional freeze / winter-storm exposure for a scoped thermal, wind, or solar set / geography.
- The THREE mechanisms by fuel (cited), naming which claim type applies.
- Realized event framing: Uri caused ~32 GW ERCOT thermal outage at peak (FERC/NERC — a **regional** fact, not a per-plant outage claim).
- Winterization gap as a structural vulnerability (Southern-latitude plants without cold-weather packages).
- Owner / portfolio winterization-risk accumulation in freeze-exposed geographies.
- Mitigation + monitoring/hardening recommendations (cold-weather packages, heat tracing, firm gas contracts, blade de-icing).

## Blocked claims

- Exact $ damage / EAL / insurance payout.
- Forward annual probability or return-period of a Uri-class event.
- Per-plant outage attribution during Uri from the CF series alone.
- Single-cause attribution (a freeze caused an observed CF change — the Feb dip IS the seasonal minimum).
- Which specific wells, pipes, or instruments froze at a given plant.
- Specific plant winterization status unless a named source reports the equipment package / deficiency.
- Wind blade-icing or solar snow-loss magnitude without sub-monthly generation plus weather/snow/icing data.
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — NOT reachable on the substrate alone (would need a verified per-plant outage record or a served cold-weather peril model).
- **Medium** — mechanism + freeze-geography exposure on a clear geography (NOAA/FERC/NERC + resolved scoped fleet), with the fuel-specific mechanism stated.
- **Low** — forward / probabilistic exposure without a climate model; OR any event-context claim leaning on monthly CF.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / return-period / per-plant-outage-attribution / single-cause-CF claim requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part — exposure vs realized event vs CF context differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the THREE mechanisms by fuel, the winterization-gap explanation, the Uri anchor + why CF can't show it, citations |
| `historical_context.md` | historical event ledger and cross-event patterns; use as context only, never as substrate grounding |
| `examples/applied_insight_001.md` | the target output shape (the validated ERCOT/TX thermal insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
