# Extreme-Heat Thermal Derate For Solar Assets — Method (human-readable)

> **Status**: draft 2026-06-14, test 001 PASS. The human-readable companion to `resource.yml` (the structured operation) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. A **weather × solar** resource (directional, weather-led — the ENSO pattern), NOT a hazard/peril resource. Worked sibling: `../el_nino_enso/`.

## What it answers (and what it refuses)

```text
ANSWERS   which solar assets/owners/regions carry directional thermal-derate exposure in a hot summer ·
          the mechanism (temperature coefficient) + WHEN it bites (peak afternoon hours) · why it matters
          MORE than its size (it coincides with the ERCOT summer price/demand peak) · who should care
REFUSES   exact %/MWh de-rate per plant · exact $ / MWh impact · forward heat probability / return-period ·
          plant-level forecast · single-cause attribution · reading heat off monthly CF · outreach before the gate
```

## Scope

Solar (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = ERCOT/Texas) · operating (+ queue, directional) · actors: owner-operator · investor · lender · offtaker.

## Mechanism (cite `knowledge.md`; do not re-derive)

High ambient temperature → **PV cell temp rises above the 25 °C STC reference** → module efficiency falls at the **temperature coefficient of power (~ −0.3 to −0.45 %/°C)** → a **MODEST de-rate concentrated in the hottest afternoon hours**; inverter/BOS thermal derating compounds it. The **(driver × mechanism)** detail: it is an **intra-day efficiency** effect, and it **coincides with the ERCOT summer demand/price peak**, so it bites when output is most valuable.

## The honesty rule (this resource's defining discipline — `knowledge.md` §2)

```text
SECOND-ORDER + MODEST + PEAK-HOUR-CONCENTRATED  — never a capacity-factor collapse.
Summer monthly CF is HIGH (irradiance-dominated): real data shows summer CF ~0.30 vs winter ~0.09–0.15.
⇒ DO NOT read a heat signal off monthly CF. The de-rate lives INSIDE high-CF summer months as a peak-hour shave.
⇒ Confidence is LOW, magnitude MODEST, claim DIRECTIONAL + peak-hour-scoped. Resist over-magnitude.
```

## Procedure (the real tool sequence)

```text
1. condition:   NOAA/CPC seasonal temperature outlook (hot-summer above-normal lean)  → cite the issue/access date
2. mechanism:   state the temperature-coefficient de-rate + inverter/BOS compounding; name claim type (directional, 2nd-order)
3. scope:       search_plants(fuel="solar", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" → [] (R1); confirm zone via get_plant.grid
4. baseline:    get_plant.generation monthly CF                      → CONFIRM summer CF is HIGH (the honesty proof)
5. construction:get_plant.generators.solar                           → single-axis / c-Si flags (the de-rate-prone build)
6. peak-coincidence: get_plant.grid (HB_/LZ_ zone) + the ERCOT summer-peak fact → the de-rate-bites-at-peak argument
7. actor:       get_plant.ownership / offtakers                      → owner chain + portfolio / PPA concentration
8. draft:       assemble the claim grammar; cap at LOW; block the %/MWh, the $, the forward probability, the monthly-CF read
```

## Allowed vs blocked claims

```text
ALLOWED  directional thermal-derate exposure for a scoped solar set · mechanism (temp coefficient, BOS derating, cited) ·
         the PEAK-COINCIDENCE framing · owner/portfolio/offtaker concentration in a heat-prone summer-peak market ·
         thermal-aware design / O&M monitoring recommendations (directional)
BLOCKED  exact %/MWh de-rate per plant · exact $ / MWh · forward probability / return-period · plant-level forecast ·
         heat read off monthly CF (over-magnitude) · single-cause attribution · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is capped at **LOW** by design (the default), **MEDIUM at the very most** when the mechanism, scope, summer-CF baseline, and a strong dated temperature lean all line up — because there is **no plant-level thermal model** (the quantified magnitude is model-gpr, `mcp_gaps` R12). Required caveats: it is a **second-order, modest, peak-hour-concentrated** effect, **not** a CF collapse; **summer CF is high (irradiance-dominated) so monthly CF is not a heat signal**; directional, not a plant-level forecast; the materiality is **peak coincidence**, not a large energy loss; climate **non-stationarity** caps any trend claim. The quantified %/MWh / $ layer is the model-gpr upgrade.

## Actor relevance

Owner (thermal-aware design — inverter sizing, DC/AC ratio, ventilation; O&M during heat waves; peak-hour revenue exposure) · investor (concentration in a single summer-peaking heat-prone market; downside on the most valuable hours) · lender (P50/P90 should reflect thermal derating; directional DSCR sensitivity) · offtaker (shaped/peak-hour PPA or merchant exposure feels the de-rate-at-peak most). Relevance never distorts the method.

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + the honesty section + the Aktina baseline) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (the validated output) · `test_runs/test_run_001.md` (the live test record).
