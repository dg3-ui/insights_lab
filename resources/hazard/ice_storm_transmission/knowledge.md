# Knowledge — Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets (cited mechanism library)

> **Status**: draft 2026-06-29. The stable "why" for `ice_storm_transmission`. Live geography/event state comes from NOAA NWS freezing-rain climatology + the SPIA Ice Accumulation Index + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding. Worked reference: `../weather_and_climate/el_nino_enso/knowledge.md`; sibling: `../extreme_cold_winter_storm/knowledge.md` (the GENERATION-side freeze).

## 1 · The mechanism

```text
freezing rain accretes ice on exposed infrastructure → THREE distinct claim types:

(A) TRANSMISSION — ICE-LOAD MECHANICAL FAILURE   [the PRIMARY hazard]
    ice accretes on conductors + towers → mechanical load exceeds the design rating
    → conductor break / tower collapse / cascading span failure → delivery outage
    → capital-intensive rebuild (days-to-weeks)

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN
    ice on blades → mass imbalance + vibration + lost aerodynamic profile → control system shuts down
    → zero output for the icing window (a TEMPORARY loss; recovers on thaw)

(C) DELIVERY-DEPENDENT — STRANDING BEHIND A DOWNED LINE
    a physically UNDAMAGED generator cannot export when the line / distribution network feeding the grid is down
    → revenue loss with NO physical-damage claim
```

The defining framing — and why this is `_transmission` rather than a generation resource — is that the loss is often **grid-side, not plant-side**. A healthy generator can lose revenue while stranded (mechanism C). The variance-driving factor is **ice-accretion thickness vs conductor/tower design rating** (ratings not in the substrate). The **generation-side** freeze (gas wellhead/pipeline freeze-off → forced outage) lives in `extreme_cold_winter_storm` — cross-reference, never double-count.

## 2 · Robustness & attribution

```text
mechanism (ice load fails conductors/towers; icing shuts wind; downed lines strand generation)   ROBUST — physical, well-documented (utility post-event records)
geography (where damaging ice storms concentrate)                                                ROBUST — NWS freezing-rain climatology + SPIA index (the South-Central + Mid-South/Appalachian ice belts)
a realized ice storm hit corridor X near asset Y                                                 FACTUAL when corroborated (multi-source news + NWS)
the forward PROBABILITY / return-period of a damaging ice load at a span                          LOW from climatology alone — needs an ice-load model + line ratings (blocked here)
climate TREND in freezing-rain frequency                                                         LOW-TO-MEDIUM — contested; a poleward ice-belt shift is an emerging, weak signal
```

**Non-stationarity** (standard caveat): freezing-rain climatology is an odds field on a debated baseline — never convert it into a per-span return-period without an ice-load model.

## 3 · State / event basis

- **Geography**: NOAA NWS freezing-rain climatology + winter-storm warnings; the **SPIA (Sperry-Piltz) Ice Accumulation Index** maps accretion severity to expected damage tiers. The South-Central (OK/TX/AR) and the Mid-South/Appalachian corridors carry the bulk of US ice-storm damage.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = ice_storm | freezing_rain | winter_storm`) carries `details_json`. **Verify** each (a "winter storm" article may cover the generation-side freeze — that is the `extreme_cold_winter_storm` resource, not this one).

## 4 · Region / asset-class crosswalk

```text
ice × TRANSMISSION (this resource's primary)   conductor/tower ice-load → mechanical failure → delivery outage (mechanism A)
ice × WIND                                     blade icing → protective shutdown (mechanism B); shared framing with extreme_cold_winter_storm
ice × SOLAR / GAS / BATTERY                    delivery-dependent — stranded behind a downed line (mechanism C); minor direct icing
geography                                      South-Central ice belt (OK/TX/AR) + Mid-South/Appalachian corridor carry the bulk of exposure
```

## 5 · Canonical realized case (anchor to resolve in test 001)

**South-Central ice belt, Oklahoma–Texas–Arkansas.** Major ice storms in the South-Central US have repeatedly downed transmission and distribution networks across the OK–TX–AR corridor, producing widespread, prolonged outages driven by **conductor/tower ice-load failure** rather than generation-equipment damage — the public, well-documented regional anchor for the PRIMARY (transmission) mechanism. The disciplined claim is a **directional ice-belt-exposure + mechanism** statement emphasizing the delivery-infrastructure framing (a healthy generator stranded behind a downed line); the in-substrate plant/corridor anchor (an operating wind asset + its delivery path, test 001 = OK–TX–AR) is to be resolved via `get_plant`/`nearby_plants`. Monthly CF cannot isolate an ice-storm outage from the winter seasonal pattern.

## 6 · Citations

```text
NOAA NWS freezing-rain climatology + winter-storm warnings    https://www.weather.gov/
SPIA (Sperry-Piltz) Ice Accumulation Index                    https://www.spia-index.com/ — accretion severity → damage tier
IEEE / industry transmission ice-loading + NESC standards     IEEE / NESC conductor & structure ice-load design literature
IEC 61400 wind-turbine cold-climate / blade-icing specs       IEC 61400-1 + TR 61400-24 — blade icing / shutdown basis
utility ice-storm restoration + delivery-stranding records    DOE / utility post-event reports (South-Central ice storms)
InfraSure hazards news (subcategory=ice_storm|freezing_rain)  search_news(category=hazards, query="ice storm"/"freezing rain")
```

---

**See also**: `data_requirements.md` (where to pull the ice-storm state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../extreme_cold_winter_storm/knowledge.md` (the GENERATION-side freeze — the do-not-double-count sibling) · `../hurricane_high_wind_wind/knowledge.md`.
