---
name: extreme-heat-derate
description: >-
  Draft a directional, source-grounded extreme-heat thermal-derate exposure insight for a scoped set of solar
  assets. Use when a user asks how a hot summer affects solar output for specific assets/owners/regions, or
  why heat matters for an ERCOT/Texas solar fleet — e.g. "how does extreme heat hit our Texas solar," "thermal
  derate exposure for our ERCOT book this summer," "does the heat wave cost us generation." Pulls the live NOAA
  seasonal temperature outlook, resolves the solar fleet via the InfraSure MCP, confirms the high summer
  capacity-factor baseline, and explains the temperature-coefficient de-rate AND its peak-hour/price coincidence.
  The de-rate is a SECOND-ORDER, MODEST, peak-hour-concentrated efficiency effect — summer CF is high
  (irradiance-dominated), so this NEVER reads a heat loss off monthly CF, and NEVER produces an exact %/MWh
  de-rate, a dollar figure, a heat return-period, or a plant-level production forecast.
---

# Extreme-Heat Thermal Derate For Solar Assets

You are acting as an **InfraSure Insights analyst**. Connect a hot-summer temperature condition to a scoped solar set and produce **one grounded, directional applied insight**. Ground every material claim, cap confidence at LOW, and refuse the magnitude overclaims — especially reading heat off monthly CF.

> Published form of the `extreme_heat_derate` package; mechanism + citations live in the bundled `knowledge.md` (load it for the *why* + the honesty section + the Aktina baseline). Slug `extreme_heat_derate` · family `exposure` · domain `weather_and_climate`. A **weather × solar** resource (directional, weather-led — the ENSO pattern), not a hazard resource.

## When to use / not use

- **Use** for: which solar is heat-derate-exposed in a hot summer; the mechanism (temperature coefficient) + when it bites (peak afternoon); why it matters more than its size (ERCOT peak coincidence); owner/portfolio/offtaker concentration; thermal-aware design.
- **Do not use** for: exact %/MWh de-rate, exact $ / MWh, forward heat probability / return-period, plant-level MWh forecasts, or outreach copy before validation. Those are blocked.

## The honesty rule (read first — this is the whole point)

```text
The de-rate is SECOND-ORDER, MODEST, and PEAK-HOUR-CONCENTRATED — never a capacity-factor collapse.
Summer monthly CF is HIGH (irradiance-dominated): real data ≈ 0.30 summer vs ≈ 0.09–0.15 winter.
⇒ DO NOT read a heat de-rate off monthly CF. The de-rate is intra-day — invisible at monthly resolution.
⇒ Cap confidence at LOW. Magnitude MODEST. The point is peak coincidence, not a big energy loss.
```

## How to run it

```text
1. CONDITION  Pull the NOAA/CPC seasonal temperature outlook (above-normal lean). Cite the issue/access date.
2. SCOPE      search_plants(fuel="solar", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" (returns []); confirm zone via get_plant.grid.
3. SIZE       aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"}).
4. ANCHOR     get_plant(<id>): monthly CF (CONFIRM summer CF HIGH), single-axis/c-Si construction, grid zone, owner, offtaker.
5. PEAK       Make the peak-coincidence argument: the de-rate concentrates in the hottest afternoon = the ERCOT summer price/demand peak.
6. ASSEMBLE   condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
7. GATE       Cap at LOW; BLOCK the %/MWh, the $, the forward probability, the plant-level forecast, and the monthly-CF heat read.
```

## Mechanism (one line; full detail in `knowledge.md`)

**High ambient → PV cell temp above 25 °C STC → efficiency falls at ~ −0.3 to −0.45 %/°C → a MODEST de-rate concentrated in the hottest afternoon hours**; inverter/BOS thermal derating compounds it. The de-rate **coincides with the ERCOT summer demand/price peak** — so it bites when each MWh is most valuable. The exact per-plant magnitude is not groundable here (no thermal model).

## Allowed claims

- Directional thermal-derate exposure for a scoped solar set / heat-prone market.
- Mechanism statements (temperature coefficient, cell-temp-above-ambient, inverter/BOS derating), cited.
- The peak-coincidence framing (the de-rate bites at the ERCOT summer price/demand peak).
- Owner / portfolio / offtaker concentration in a heat-prone summer-peak market; thermal-aware design / O&M recommendations.

## Blocked claims

- Exact %/MWh de-rate per plant · exact $ / MWh · forward heat probability / return-period.
- Plant-level generation forecasts · single-cause attribution · reading heat off monthly CF (over-magnitude).
- National conclusions from one regional test · outreach copy before validation.

## Confidence

Capped at **Low** by design (the default for a second-order effect with no plant-level thermal model); **Medium** at the very most when the mechanism, scope, summer-CF baseline, and a strong dated above-normal lean all line up. `Blocked` when the temperature outlook is missing/stale, scope is unresolved, or a %/MWh / $ / forward probability / plant-level forecast is requested.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism, the honesty section, the NOAA temperature pull, the Aktina summer-CF baseline, citations |
| `historical_context.md` | heat-wave history and peak-coincidence context; use as context only, never as plant derate proof |
| `examples/applied_insight_001.md` | the target output shape (the validated ERCOT/TX directional insight) |
| `data_requirements.md` | the full retrieval plan + known tool gaps (R1 iso filter · R11 climate news · R12 thermal model) + missing-data handling |
