# Prompt Projection — Severe Hail Exposure For Solar Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the hail method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage, an insurance payout, or a hail return-period.

## Task

Draft one hail-exposure insight for one scoped solar asset set. Recommended first scope:

```text
ERCOT / Texas solar ≥ 50 MW   (resolve via state="TX"; the iso filter is unwired — see step 3)
```

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
severe hail (≳1–2 in) over a solar array → c-Si module glass/cell damage → output + availability loss
   modifiers: single-axis trackers can HAIL-STOW (steep tilt) to cut impact; thin-glass modules are more vulnerable
   geography: the southern Great Plains / Texas is the US hail maximum (SPC climatology)
```

Exposure is **geographic + climatological**, not a dated forecast. A *realized* event hitting a named asset can be **factual** (corroborated news + an observed CF dip); the *forward probability* is **not** groundable here (no hail model).

## Required reasoning steps

```text
1. Establish the hail geography (SPC climatology) AND/OR a realized event (search_news category=hazards, query="hail").
   ⚠ VERIFY each hazards article — the classifier has false positives (don't trust the label).
2. State the mechanism + the tracker/module modifiers; name the claim type (directional exposure vs realized event).
3. Resolve assets:  search_plants(fuel="solar", state="TX", minMw=50)
   ⚠ NOT iso="ERCOT" (returns []). Scope by state; confirm region via get_plant.regions / .grid.
4. Place assets in the footprint: get_plant geometry/county + nearby_plants (same hail cell).
5. Where a realized event exists, drill get_plant.generation for the OBSERVED post-event CF change (compare like months YoY).
6. Retrieve owner chain for actor relevance + portfolio concentration.
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block the $ loss, the forward probability, and single-cause attribution.
```

## Allowed claims

- Directional hail exposure for a scoped solar set / geography.
- Realized event-translation: a named hail event → a specific asset, with **observed** operating impact (CF).
- Owner / portfolio concentration in a hail-exposed geography.
- Mechanism + mitigation statements (hail-stow, hail-rated modules), cited.
- Monitoring / hardening recommendations.

## Blocked claims

- Exact $ damage / EAL / PML / insurance payout from hail.
- Forward hail probability or return-period from climatology alone.
- Plant-level generation forecasts without modeling.
- Single-cause attribution (an observed CF change caused *only* by hail).
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — a realized event with multi-source corroboration **and** an observed substrate signal (post-event CF dip). Reachable for event-translation.
- **Medium** — exposure framing on a climatologically clear geography, resolved scope, no realized-event signal.
- **Low** — forward / probabilistic exposure without a hail model, or one noisy input.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / return-period / plant-level forecast requested.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part if the event vs the forward exposure differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
