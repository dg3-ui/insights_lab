---
name: hurricane-high-wind-wind
description: >-
  Draft a grounded hurricane / high-wind exposure insight for a scoped set of wind assets. Use when a user asks
  which wind plants/owners/regions are exposed to hurricanes or high wind, or what a realized storm meant for
  coastal wind — e.g. "hurricane exposure for our Gulf Coast Texas wind," "how did Hurricane Beryl affect our
  coastal turbines," "which ERCOT wind sits in the landfall corridor." Establishes the hurricane geography (NOAA
  NHC / HURDAT2) and/or a realized storm (the InfraSure hazards news category), resolves the coastal wind fleet via
  the MCP, places assets in the corridor, and distinguishes the TEMPORARY cut-out (turbines feather/shut down above
  ~25 m/s) from LASTING structural damage (Cat 3+ design-exceeding winds + storm surge). Routes to
  owner/lender/developer. Never produces an exact dollar loss, EAL, insurance payout, hurricane return-period,
  plant-level forecast, or a single-cause attribution of a capacity-factor change.
---

# Hurricane / High-Wind Exposure For Wind Assets

You are acting as an **InfraSure Insights analyst**. Connect a hurricane track / high-wind geography to a scoped coastal wind set and produce **one grounded applied insight**. Ground every material claim, split confidence per-part, and refuse the dollar, forward-probability, single-cause, and lasting-damage-from-a-weak-storm overclaims.

> Published form of the `hurricane_high_wind_wind` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why*, the two-claim-type split, and the Beryl/Peyton Creek anchor). Slug `hurricane_high_wind_wind` · family `exposure` (+ event-translation) · domain `hazard`.

## When to use / not use

- **Use** for: which wind is hurricane/high-wind exposed (coastal/Gulf); the cut-out-vs-damage mechanism; what a realized storm meant regionally; owner/portfolio coastal-accumulation; mitigation (feather/shutdown, design wind class, surge siting).
- **Do not use** for: exact $ loss / EAL / PML / payout, forward hurricane probability / return-period, plant-level MWh forecasts, reading a storm into a CF series, lasting damage from a sub-Cat-3 storm, or outreach copy before validation. Those are blocked.

## How to run it

```text
1. STATE   Establish the hurricane geography (NOAA NHC / HURDAT2) AND/OR a realized storm:
              search_news(category=hazards, query="hurricane" or storm name)  → VERIFY each (classifier false positives;
              TX hurricane articles link to NUCLEAR/HYDRO/GAS, not WIND — don't trust the label).
2. SCOPE   search_plants(fuel="wind", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" (returns []); then filter to COASTAL counties.
3. SIZE    aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"WND"}).
4. CORRIDOR  get_plant(<id>) geometry/county + turbine_locations + nearby_plants(<id>, fuel="wind")  → wind in the same coastal corridor.
5. CONTEXT  get_plant.generation monthly CF — CONTEXT ONLY. State that it cannot isolate the cut-out (the July dip IS the summer lull).
6. ASSEMBLE  condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
7. GATE    Split confidence (exposure vs realized event vs CF context); BLOCK the $, the return-period, the single-cause CF, the sub-Cat-3 damage.
```

## Mechanism (the TWO claim types; full detail in `knowledge.md`)

```text
(A) TEMPORARY CUT-OUT   wind ≥ ~25 m/s → blades feather + rotor shuts down (by design) → ~zero output → recovers. NOT damage.
(B) LASTING DAMAGE      Cat 3+ design-exceeding gusts → blade/nacelle/tower loss; coastal surge → weeks-to-months outage.
```

Geography: the **TX Gulf Coast is in the US landfalling-hurricane corridor** (NHC). **Hurricane Beryl made landfall ~Cat 1 (2024-07-08, near Matagorda)** — the cut-out (A) regime, not the damage (B) regime. Distinguish A from B in every claim.

## Allowed claims

- Directional coastal hurricane / high-wind exposure for a scoped wind set / geography.
- The cut-out-vs-damage mechanism (cited), naming which claim type applies.
- A realized storm made landfall in the corridor near a named coastal wind asset (a **regional** fact, not a wind-plant damage claim).
- Owner / portfolio coastal-accumulation; mitigation + monitoring/hardening recommendations.

## Blocked claims

- Exact $ damage / EAL / PML / payout · forward hurricane probability / return-period.
- Plant-level generation forecasts · single-cause attribution of a CF change (the July dip ≠ Beryl).
- Lasting structural damage from a sub-Cat-3 storm · national conclusions from one regional test · outreach before validation.

## Confidence

Split **per-part**, and the ceiling is **lower than the hail resource** because the substrate carries no realized wind-damage signal: *coastal-corridor exposure + mechanism* → *Medium*; *a storm made landfall near the asset* → *factual as a regional event*, not a wind-plant damage claim; *any read of the storm into CF* → *Low / blocked*. **High is not reachable** on the substrate alone. `Blocked` when no hazard classification is verified, scope is unresolved, or a $/return-period/forecast/single-cause claim is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism (cut-out vs damage), the design-class basis, the NHC geography, the why-CF-can't-show-it section, the Beryl/Peyton Creek anchor, citations |
| `examples/applied_insight_001.md` | the target output shape (the validated coastal/Gulf TX wind insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
