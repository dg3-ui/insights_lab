# Prompt Projection — Lightning Exposure For Wind, Solar, and Electrical-Plant Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the lightning method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage or a strike rate. Do not claim lightning caused a capacity-factor dip.

## Task

Draft one lightning-exposure insight for one scoped asset set. Recommended first scope:

```text
Gulf Coast / Florida–Texas wind ≥ 50 MW   (resolve via state="FL"/"TX", fuel="wind"; hub height frames direct-strike exposure)
Optionally fan out to solar / substations in the same flash-density band for the induced-surge picture.
```

## Mechanism — TWO claim types (cite `knowledge.md`; do not re-derive)

```text
(A) DIRECT STRIKE — STRUCTURE / BLADE / NACELLE
    a cloud-to-ground strike attaches to the tallest object → blade / nacelle / control damage → component outage.
    Wind turbines are the tallest structures in open terrain → the most direct-strike-exposed class.

(B) INDUCED SURGE — INVERTERS / TRANSFORMERS / CONTROL ELECTRONICS
    a nearby strike couples a transient into wiring → inverter / transformer / SCADA / BMS damage → component outage
    across ANY generation type, even without a direct hit.
```

Frame the hazard as HIGH-FREQUENCY, LOWER-PER-EVENT-SEVERITY, managed by design (air termination, SPDs, grounding, blade LPS receptors) — cumulative component risk + design adequacy, not a single catastrophe. LPS status is NOT in the substrate.

## Required reasoning steps

```text
1. Establish the flash-density geography (NLDN cloud-to-ground climatology) AND/OR a realized event:
   search_news(category=hazards, query="lightning"/"storm") → VERIFY each.
2. State WHICH mechanism (A/B) applies for each asset class. Do not conflate. Note LPS status is not in the substrate.
3. Resolve assets:  search_plants(fuel="wind"/"solar", state="FL"/"TX", minMw=50)
   ⚠ NOT iso= (returns []). Scope by state; filter to the flash-density band.
4. Place assets in the band: get_plant geometry/county + nearby_plants (hub height frames wind exposure).
5. CONTEXT ONLY: get_plant.generation monthly CF. ⚠ DO NOT read a strike into it — monthly CF cannot resolve a
   component-level strike outage. State this explicitly.
6. Retrieve owner chain for actor relevance + portfolio flash-density accumulation.
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block the $ loss, the forward strike rate, the per-plant damage attribution,
   the single-cause CF claim, and any is-the-LPS-adequate claim. Frame as cumulative component risk.
```

## Allowed claims

- Directional lightning exposure for a scoped wind, solar, or electrical-plant set / geography.
- The direct-strike vs induced-surge distinction (cited), naming which claim type applies.
- The high-frequency / lower-severity cumulative-component-risk + design-adequacy framing.
- Realized event framing: a named lightning event affected a named area near a scoped asset (a **regional** fact, not a per-component damage claim).
- Owner / portfolio flash-density accumulation.
- Mitigation + monitoring/hardening recommendations (lightning protection systems / receptors, surge protective devices, grounding, blade LPS inspection).

## Blocked claims

- Exact $ damage / EAL / insurance payout from lightning.
- Forward annual strike rate or component-failure probability at a specific asset.
- Per-plant generation loss attributable to a strike from the CF series alone.
- Single-cause attribution (lightning caused an observed CF change).
- Whether a specific turbine / inverter has an adequate LPS or surge-protection system (status not in the substrate).
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — NOT reachable on the substrate alone (would need a verified per-asset strike/maintenance record, or a served strike-rate model with LPS status).
- **Medium** — mechanism + flash-density exposure on a clear geography (NLDN climatology + resolved scoped fleet), with the direct-strike / induced-surge distinction stated.
- **Low** — forward / probabilistic strike exposure without a strike model; OR any event-context claim leaning on monthly CF.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / strike-rate / per-plant-damage-attribution / single-cause-CF claim requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part — direct strike vs induced surge vs CF context differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
