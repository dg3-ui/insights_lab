# Prompt Projection — Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the flood method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast exact $ damage or an insurance payout. Do not claim a flood caused a capacity-factor dip.

## Task

Draft one flood-inundation exposure insight for one scoped asset set. Recommended first scope:

```text
Gulf Coast / Texas thermal (gas) ≥ 50 MW sited near water for cooling   (resolve via state="TX", fuel="gas")
Optionally fan out to solar / transmission substations in the same floodplain for the systemic picture.
```

## Mechanism — THREE claim types by asset (cite `knowledge.md`; do not re-derive)

```text
(A) GRID / SWITCHYARD — INUNDATION OUTAGE
    floodwater reaches low-lying substation / switchyard → de-energization → outage (days-to-weeks).
    A DELIVERY failure — the plant may be undamaged but cannot export.

(B) PLANT EQUIPMENT / FUEL STORAGE — FORCED OUTAGE + DAMAGE
    floodwater reaches ground-level inverters / fuel tanks / pad electrical → forced outage + damage.
    Severity scales with equipment-pad elevation — a field NOT in the substrate.

(C) WATER-SITED THERMAL — COOLING-INTAKE COMPROMISE
    intake / screens / pump house compromised by debris-laden floodwater → derate or trip.
    The structural insight: thermal/nuclear cooling siting CONCENTRATES flood exposure.
```

Exposure is set by **site elevation relative to the flood surface** — not in the substrate. State this.

## Required reasoning steps

```text
1. Establish the flood geography (FEMA NFHL zone + NWS AHPS / USGS gauge history) AND/OR a realized event:
   search_news(category=hazards, query="flood"/"flooding"/"inundation") → VERIFY each (check it links to the asset, not grid customers).
2. State WHICH mechanism (A/B/C) applies for each asset class in scope. Do not conflate.
3. Resolve assets:  search_plants(fuel="gas", state="TX", minMw=50)  [+ solar/transmission if in scope]
   ⚠ NOT iso= (returns []). Scope by state; filter to the flood-exposed geography.
4. Place assets in the floodplain: get_plant geometry/county + nearby_plants.
5. CONTEXT ONLY: get_plant.generation monthly CF. ⚠ DO NOT read the flood into it — a CF dip is consistent with
   seasonal/maintenance variation and does not prove an inundation outage. State this explicitly.
6. Retrieve owner chain for actor relevance + portfolio floodplain accumulation.
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link; block the $ loss, the forward probability, the per-plant damage
   attribution, the single-cause CF claim, and any which-pads-flooded claim.
```

## Allowed claims

- Directional flood-inundation exposure for a scoped thermal, solar, wind, or grid set / geography.
- The THREE mechanisms by asset (cited), naming which claim type applies.
- Realized event framing: a named flood affected a named watershed / floodplain near a scoped asset (a **regional** fact, not a per-plant damage claim).
- Water-sited thermal concentration as a structural vulnerability.
- Owner / portfolio floodplain accumulation.
- Mitigation + monitoring/hardening recommendations (equipment-pad elevation, flood walls / berms, submersible-rated equipment, drainage).

## Blocked claims

- Exact $ damage / EAL / insurance payout from a flood.
- Forward inundation probability or return-period at a specific site.
- Per-plant generation loss attributable to a flood from the CF series alone.
- Single-cause attribution (a flood caused an observed CF change).
- Which specific equipment pads or feeders were inundated (site elevation not in the substrate).
- National conclusions from one regional test. Outreach copy before validation.

## Confidence rules

- **High** — NOT reachable on the substrate alone (would need a verified per-plant inundation record, or a served flood model with site elevation).
- **Medium** — mechanism + flood-geography exposure on a clear geography (FEMA NFHL or NWS/USGS + resolved scoped fleet), with the asset-specific mechanism stated.
- **Low** — forward / probabilistic exposure without a flood model + elevation; OR any event-context claim leaning on monthly CF.
- **Blocked** — no verified hazard classification, scope unresolved, or a $ / return-period / per-plant-damage-attribution / single-cause-CF claim requested.

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
