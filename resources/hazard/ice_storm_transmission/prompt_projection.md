# Prompt Projection — Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the ice-storm method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage, a restoration cost, or an insurance payout. Do not claim an ice storm caused a capacity-factor dip.

## Task

Draft one ice-storm exposure insight for one scoped asset set. Recommended first scope:

```text
South-Central ice belt / Oklahoma–Texas–Arkansas wind ≥ 50 MW + the transmission corridor that delivers it
(resolve via state="OK"/"TX"/"AR", fuel="wind"; treat the delivery path as the primary exposure surface)
Optionally fan out to delivery-dependent gas / solar in the same corridor.
```

## Mechanism — THREE claim types (cite `knowledge.md`; do not re-derive)

```text
(A) TRANSMISSION — ICE-LOAD MECHANICAL FAILURE   [the PRIMARY hazard]
    freezing rain accretes on conductors + towers → load exceeds rating → conductor break / tower collapse
    → delivery outage → capital-intensive rebuild (days-to-weeks).

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN
    ice on blades → imbalance + vibration → control shutdown → zero output for the icing window. A TEMPORARY loss.

(C) DELIVERY-DEPENDENT — STRANDING BEHIND A DOWNED LINE
    a physically UNDAMAGED generator cannot export when the line / distribution network is down
    → revenue loss with NO physical-damage claim. The defining property of this hazard.
```

Frame this as primarily a DELIVERY-INFRASTRUCTURE hazard — the loss is often grid-side, not plant-side. Distinguish physical generation damage from delivery stranding. Generation-side freeze (gas wellhead/pipeline) lives in `extreme_cold_winter_storm` — cross-reference, do not double-count. Conductor/tower ratings are NOT in the substrate.

## Required reasoning steps

```text
1. Establish the ice-belt geography (NOAA NWS freezing-rain climatology + SPIA index) AND/OR a realized event:
   search_news(category=hazards, query="ice storm"/"freezing rain") → VERIFY each.
2. State WHICH claim type (A/B/C) applies. Do not conflate. Note conductor/tower ratings are not in the substrate.
3. Resolve assets + corridor:  search_plants(fuel="wind"/..., state="OK"/"TX"/"AR", minMw=50)
   ⚠ NOT iso= (returns []). Scope by state; treat the delivery path as the primary surface.
4. Place assets + delivery path in the ice belt: get_plant geometry/county + nearby_plants.
5. CONTEXT ONLY: get_plant.generation monthly CF. ⚠ DO NOT read an ice storm into it — monthly CF cannot isolate
   an ice-storm outage from the normal winter seasonal pattern. State this explicitly.
6. Retrieve owner chain for actor relevance + portfolio ice-belt accumulation (incl. transmission ownership).
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block the $ / restoration cost, the forward ice-load probability, the
   per-span/per-plant attribution, the single-cause CF claim, and any which-spans-collapsed claim.
```

## Allowed claims

- Directional ice-storm exposure for a scoped transmission, wind, or delivery-dependent set / geography.
- The THREE mechanisms (cited), naming which claim type applies.
- The delivery-infrastructure framing: a healthy generator stranded behind a downed line loses revenue with no physical-damage claim.
- Realized event framing: a named ice storm affected a named corridor / grid near a scoped asset (a **regional** fact, not a per-span / per-plant damage claim).
- Owner / portfolio ice-belt accumulation (including transmission ownership).
- Mitigation + monitoring/hardening recommendations (conductor / tower ice-load design upgrades, line de-icing, blade de-icing / heating, vegetation management, redundant delivery paths).

## Blocked claims

- Exact $ damage / restoration cost / EAL / insurance payout from an ice storm.
- Forward annual probability or return-period of a damaging ice load at a specific span / site.
- Per-plant or per-span generation/delivery loss attributable to an ice storm from the CF series alone.
- Single-cause attribution (an ice storm caused an observed CF change — the winter seasonal pattern confounds).
- Which specific transmission spans or towers collapsed (conductor ratings + line geometry not in the substrate).
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — NOT reachable on the substrate alone (would need a verified per-line / per-asset outage record, or a served ice-load model with conductor/tower ratings).
- **Medium** — mechanism + ice-belt-geography exposure on a clear geography (NOAA freezing-rain climatology or SPIA index + resolved scoped fleet/corridor), with the claim type stated.
- **Low** — forward / probabilistic ice-load exposure without an ice-load model; OR any event-context claim leaning on monthly CF.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / return-period / per-span-or-plant-attribution / single-cause-CF claim requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part — transmission ice-load vs blade icing vs stranding vs CF context differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
