# Knowledge — Wildfire Exposure For Solar, Transmission, and Grid-Connected Assets (cited mechanism library)

> **Status**: draft 2026-06-25. The stable "why" for `wildfire`. Live fire/PSPS event state comes from NIFC (fire perimeters) + CAISO PSPS records + the InfraSure `hazards` news category (subcategory=wildfire|fire|psps), pulled per test, dated. Cite everything; this never substitutes for substrate grounding. Siblings: `../hail_solar/knowledge.md`, `../hurricane_high_wind_wind/knowledge.md`, `../extreme_cold_winter_storm/knowledge.md`.

## 1 · The mechanism — THREE distinct claim types by asset

The single most important discipline here: **wildfire does three physically different things depending on the asset type, and they are different claim types with different confidence ceilings and different mitigation levers.**

```text
(A) SOLAR — SMOKE/ASH → IRRADIANCE REDUCTION + PANEL SOILING  (a temporary, irradiance-driven effect)
    wildfire smoke column drifts over a solar plant
       → particulate matter scatters and absorbs direct normal irradiance (DNI) and diffuse irradiance (DHI)
       → output drops proportionally to the smoke optical depth (can be 20–80%+ under a dense smoke column)
    ash also deposits on panel glass
       → soiling blocks transmittance → additional output loss until panels are cleaned
       → self-cleaning (rain, wind) typically restores output within days-to-weeks
    Net: a temporary, partial output reduction. NOT structural damage to the panels in most cases
    (embers that land on panels are a separate, lower-probability structural risk).

(B) TRANSMISSION — HEAT + FLAME → CORRIDOR DAMAGE + IGNITION LIABILITY  (a lasting, structural risk)
    FLAME DAMAGE:
       fire burns into the transmission right-of-way (ROW)
       → conductor sag from heat → flashover to vegetation → line trip; or
       → direct contact with burning vegetation → conductor damage / tower failure
       → transmission outage → downstream generators lose their interconnection
       → repair (vegetation clearance + conductor/tower replacement) → outage weeks-to-months
    IGNITION LIABILITY (the high-severity tail):
       a transmission line in high-voltage / high-wind conditions arcs or makes contact with vegetation
       → the line STARTS a wildfire (the Camp Fire / Caribou-Palermo mechanism)
       → regulatory / legal liability for the transmission owner (PG&E: ~$16B Camp Fire liability)
       → this is a DISTINCT, HIGH-SEVERITY TAIL RISK — NOT a grounded claim here; it is model-gpr / legal

(C) GRID-CONNECTED GENERATION — PSPS → CURTAILMENT OF OTHERWISE-HEALTHY GENERATION  (a temporary revenue loss)
    during extreme fire-weather conditions (low humidity + high wind + high temperature)
       → a utility (PG&E, SCE, SDG&E) proactively de-energizes transmission and distribution lines
          to prevent the lines from causing ignitions
       → ALL generators on the de-energized circuit are curtailed — even those with NO direct fire risk
       → the generator is physically undamaged; it cannot export because its interconnection is offline
       → PSPS duration: typically 1–5 days per event; PG&E has conducted dozens of events since 2019
    Net: a temporary, recurring revenue loss for physically healthy generators. DIFFERENT from fire damage.
    Affects solar, wind, gas, battery storage equally — fuel type does not matter; circuit location does.
```

**What distinguishes wildfire from other hazards:** the three mechanisms are CORRELATED in space (a fire or fire-weather event affects solar output, transmission integrity, and PSPS curtailment simultaneously in the same geography) but are DIFFERENT in claim type — temporary revenue vs lasting infrastructure damage vs tail ignition liability. Conflating them is the headline overclaim this resource blocks.

## 2 · Robustness & attribution

```text
mechanism (smoke → solar irradiance reduction; flame → transmission damage; PSPS → curtailment)  ROBUST — physics + CAISO/utility record
geography (Western WUI, California = primary PSPS jurisdiction + high fire-weather frequency)       ROBUST — NIFC historical + NWS red-flag climatology
a named fire affected a specific geography / transmission corridor                                 FACTUAL when corroborated (NIFC + hazards news)
a specific solar plant lost output due to smoke from a named fire                                  INFERRED from proximity + smoke column; NOT directly in the substrate CF series
a PSPS event curtailed generation on circuit X                                                    FACTUAL when CAISO / utility filing corroborates; substrates may carry a news item
the ignition liability of a specific transmission line                                             NOT grounded here — liability determination is regulatory/legal/model-gpr (block)
the forward ignition probability or return-period at a given asset                                 LOW skill from fire-history alone — needs a fire-risk model (blocked)
```

**Non-stationarity (standard climate caveat):** fire-weather intensification is one of the better-attributed climate signals — hotter temperatures, lower humidity, longer fire seasons, and more extreme wind events (particularly in California) are well-documented trends. However, individual ignition probability and perimeter spread are driven by fine-scale vegetation, topography, and ignition-source factors that are not forecastable from trend data alone. Cap trend claims at directional; never state a return-period from fire-history alone.

## 3 · Fire-weather geography and PSPS context

- **Western WUI (Wildland-Urban Interface)**: the primary fire-risk zone — California (Coast Ranges, Sierra Nevada foothills, North Bay), Pacific Northwest (eastern Washington / Oregon), Mountain West (Colorado, Arizona, New Mexico), and expanding into the Southern plains (Texas Hill Country, West Texas). NIFC tracks fire perimeters nationally.
- **California / CAISO**: the primary PSPS jurisdiction. PG&E, SCE, and SDG&E have established PSPS programs post-Camp Fire (2018). CAISO PSPS events are documented in utility filings and CAISO market notices.
- **Red-flag conditions**: NOAA NWS red-flag warnings signal fire-weather conditions (sustained wind ≥ 25 mph or gusts ≥ 35 mph + relative humidity ≤ 15% + temperature threshold). Red-flag frequency maps to PSPS risk geography.

## 4 · The PSPS mechanism in detail — why it matters for generation assets

PSPS is the **most operationally novel** mechanism in this resource — it is a grid-operator / utility decision that creates a revenue loss for a physically healthy generator. Key facts:

```text
Trigger:        extreme fire-weather conditions (NWS red-flag) → utility determines de-energization is necessary
Notice:         typically 24-48 hours ahead (NWS forecast → utility assessment → customer/asset notification)
Scope:          de-energizes specific distribution and transmission circuits; not all of CAISO at once
Duration:       1–5 days typically; until conditions normalize + lines are inspected and re-energized
Revenue impact: the generator cannot export during the PSPS window → zero or near-zero revenue
Fuel type:      does NOT matter — solar, wind, gas, battery on the affected circuit are all curtailed equally
Frequency:      PG&E has conducted dozens of PSPS events since 2019; SCE and SDG&E also have active programs
Regulatory:     CPUC oversees PSPS programs; utilities file post-event reports; program rules are evolving
```

A generator's PSPS exposure is determined by **which circuit it is interconnected to** — not by its proximity to fire. A solar plant in a non-fire-risk location can be curtailed if its interconnection circuit passes through a high fire-weather zone. This is the discipline: physical fire risk ≠ PSPS curtailment risk.

## 5 · Why the summer/fall CF dip is NOT the smoke (same discipline as sibling resources)

California solar has high seasonal output in summer and fall, which overlaps with peak fire season. Smoke events during August–October can reduce output, but:
- A smoke-driven output reduction is measured in **days-to-weeks** inside a month that is otherwise seasonally high
- Monthly CF averages out the smoke effect against the high-irradiance baseline
- Seasonal variation, curtailment, maintenance, and cloud cover all move monthly CF in the same direction
- A specific CF dip in August–October is **NOT separable from these confounders at monthly resolution**

Conclusion: **the substrate CF series cannot ground a smoke→output claim for a specific plant.** Monthly CF is *context only* here; the realized-impact leg that made `hail_solar` strong (an observable post-event CF dip) does NOT exist for smoke. Be honest: per-plant smoke-output attribution stays blocked.

## 6 · Canonical realized cases

**Camp Fire (2018-11-08) — the ignition mechanism anchor:**
PG&E's Caribou-Palermo 230kV transmission line in Butte County ignited the fire during high-wind / red-flag conditions. The Camp Fire destroyed Paradise, CA; killed 85 people; and caused ~$16.5B in losses. PG&E filed for bankruptcy in 2019. This is the case that drove the California PSPS program — the utility decided proactive de-energization was preferable to ignition risk. **This is a TRANSMISSION MECHANISM (B) / ignition-liability case — NOT a solar-output case.**

**2020 California wildfire season — the smoke/solar mechanism anchor:**
The 2020 CA fire season was the largest on record at the time. CAISO documented measurable reductions in solar output during the August–September 2020 smoke events. This is the best-documented **SMOKE MECHANISM (A)** case — but even here, isolating the smoke effect from seasonal variation at the plant level requires hourly/daily data, not monthly CF.

**PG&E PSPS events (2019–present) — the curtailment mechanism anchor:**
PG&E has conducted dozens of PSPS events since October 2019. These events de-energized circuits serving both load and generation, curtailing solar and other generation assets for 1–5 days per event. **This is the PSPS MECHANISM (C) — the most operationally tractable claim type in this resource.**

## 7 · Citations

```text
NIFC / IRWIN fire perimeter data                              https://www.nifc.gov/
NOAA NWS red-flag / fire-weather watches + climatology        https://www.weather.gov/
CAISO PSPS event records / market notices                     https://www.caiso.com/
Cal Fire incident records                                     https://www.fire.ca.gov/
CPUC wildfire mitigation plan filings (post-AB 1054)         https://www.cpuc.ca.gov/
PG&E Camp Fire ignition / bankruptcy record                  CPUC, PG&E PSPS filings, Cal Fire (2018-11)
2020 CA fire season / CAISO solar output documentation       CAISO, EIA, LBNL
IEC / industry literature on smoke optical depth + solar PV  NREL, IEA-PVPS, Sandia
```

---

**See also**: `data_requirements.md` (where to pull fire/PSPS state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hail_solar/knowledge.md` · `../hurricane_high_wind_wind/knowledge.md` · `../extreme_cold_winter_storm/knowledge.md` (sibling hazard patterns).
