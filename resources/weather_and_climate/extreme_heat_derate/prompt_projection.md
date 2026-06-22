# Prompt Projection — Extreme-Heat Thermal Derate For Solar Assets

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the thermal-derate method below to draft **one grounded, directional applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast an exact %/MWh de-rate, an exact $ / MWh impact, or a plant-level generation number.

## Task

Draft one directional extreme-heat thermal-derate exposure insight for one scoped solar asset set. Recommended first scope:

```text
ERCOT / Texas solar ≥ 50 MW, summer   (resolve via state="TX"; the iso filter is unwired — see step 3)
```

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
high ambient temperature → PV CELL temp rises above 25 °C STC → module efficiency falls at the
temperature coefficient (~ -0.3 to -0.45 %/°C) → a MODEST de-rate CONCENTRATED in the hottest afternoon
hours; inverter/BOS thermal derating compounds it. The de-rate COINCIDES with the ERCOT summer
demand/price PEAK — so it bites when each MWh is most valuable.
```

This is a **second-order efficiency** effect. It is **directional, MODEST, and peak-hour-concentrated** — never a capacity-factor collapse.

## The honesty rule (do not violate — this is the whole point)

```text
Summer monthly CF is HIGH (irradiance-dominated): real data ≈ 0.30 summer vs ≈ 0.09–0.15 winter.
⇒ DO NOT read a heat de-rate off monthly CF. The de-rate is intra-day, peak-hour — invisible at monthly resolution.
⇒ The honest claim: summer CF is high BECAUSE of irradiance, AND heat quietly shaves the most valuable peak hours.
⇒ Cap confidence at LOW. Magnitude MODEST. Resist any over-magnitude / "big summer loss" framing.
```

## Required reasoning steps

```text
1. Pull the temperature CONDITION live from NOAA/CPC (seasonal outlook above-normal lean). Cite the issue/access date.
2. State the mechanism (temperature coefficient + inverter/BOS derating) + its robustness; name the claim type (directional, 2nd-order).
3. Resolve assets:  search_plants(fuel="solar", state="TX", minMw=50)
   ⚠ NOT iso="ERCOT" (returns []). Confirm the ERCOT load zone via get_plant.grid (HB_/LZ_) and .regions.iso_rto.
4. Drill get_plant: monthly CF (CONFIRM summer CF is HIGH — the honesty proof), single-axis/c-Si construction, owner, offtaker.
5. Make the PEAK-COINCIDENCE argument: the de-rate concentrates in the hottest afternoon hours = the ERCOT summer price/demand peak.
6. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
7. Cap confidence at LOW; block/downgrade the per-plant %/MWh, the $, the forward probability, and any monthly-CF heat read.
```

## Required inputs

- external NOAA/CPC temperature outlook (source + access date) · region/market scope · plant/generator list
- fuel/technology · capacity · single-axis/c-Si construction · summer-CF baseline · grid zone · owner/company · offtaker (if available)

## Allowed claims

- Directional thermal-derate exposure for a scoped solar set / heat-prone market.
- Mechanism statements (temperature coefficient, cell-temp-above-ambient, inverter/BOS derating), cited.
- The **peak-coincidence** framing (the de-rate bites at the ERCOT summer price/demand peak).
- Owner / portfolio / offtaker concentration in a heat-prone summer-peak market.
- Thermal-aware design / O&M monitoring recommendations (directional).

## Blocked claims

- Exact %/MWh thermal de-rate per plant (no plant-level thermal model).
- Exact summer generation (MWh) or revenue ($) impact from heat.
- Plant-level generation forecasts without modeling.
- Forward heat probability / return-period from a seasonal outlook alone.
- **Reading a heat de-rate off monthly CF** (over-magnitude error — summer CF is HIGH).
- Single-cause attribution (an observed CF/generation change caused *only* by heat).
- National conclusions from one regional test · outreach copy before validation.

## Confidence rules

- **High** — not reachable here (second-order effect, no plant-level thermal model).
- **Medium** — mechanism + scope + summer-CF baseline clean AND a strong dated above-normal lean; the ceiling.
- **Low** — directional exposure on a credible-but-modest temperature lean → **the default for this resource**.
- **Blocked** — temperature outlook missing/stale, scope unresolved, or a %/MWh / $ / forward probability / plant-level forecast is requested.

The modest, broad nature of a seasonal temperature lean caps confidence on its own — exactly as ENSO strength-uncertainty does.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part if useful)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate tool result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
