# Knowledge — Extreme Cold / Winter Storm Exposure For Thermal, Wind, and Solar Assets (cited mechanism library)

> **Status**: draft 2026-06-24. The stable "why" for `extreme_cold_winter_storm`. Live freeze-event state comes from NOAA NWS (watches/warnings/historical) + the InfraSure `hazards` news category (subcategory=winter_storm|extreme_cold|freeze), pulled per test, dated. Cite everything; this never substitutes for substrate grounding. Siblings: `../hail_solar/knowledge.md`, `../hurricane_high_wind_wind/knowledge.md`.

## 1 · The mechanism — THREE distinct claim types by fuel

The single most important discipline here: **extreme cold does three physically different things depending on the asset type, and they are different claim types with different confidence ceilings.**

```text
(A) THERMAL / GAS — FORCED OUTAGE via SUPPLY CURTAILMENT  (the dominant Uri mechanism)
    sustained sub-freezing temperatures reach wellhead equipment + pipeline infrastructure
       → gas at the wellhead freezes / hydrates form in the pipe → pressure drops / flow stops
       → gas-fired generators lose fuel supply → forced to derate or shut down (not a protective choice)
       → plant instrumentation also freezes: temperature sensors, valve actuators, cooling-water lines
         fail → additional forced trips even where gas supply is intact
       → output drops to ~zero for the duration of the cold window (days)
       → restart requires wellhead/pipe thawing + instrumentation checks → recovery is hours-to-days
    Net: a large-scale, correlated, multi-day capacity loss. NOT equipment damage in the typical sense —
    it is a supply and operability failure. This is the plant NOT working as designed (winterization gap).

(B) WIND — BLADE ICING → PROTECTIVE SHUTDOWN  (similar to the hurricane cut-out concept)
    sustained cold + moisture → ice accumulates on rotor blades
       → ice changes the blade aerodynamic profile → rotor imbalance → vibration alarm
       → control system shuts down the turbine (a protective action, by design)
       → output drops to ~zero for the icing window
       → turbine restarts once ice melts or is actively shed (blade heating systems where installed)
    Net: a temporary availability loss. Duration is hours-to-days depending on conditions and
    whether de-icing equipment is installed. NOT structural damage in most cases.

(C) SOLAR — SNOW COVER + SHORT DAYLIGHT → OUTPUT REDUCTION  (a softer, often temporary effect)
    snow accumulates on panels → blocks irradiance → output drops proportionally
       → panels typically self-clear as sun angle and panel heat cause sliding (hours-to-days)
       → short winter daylight hours reduce the daily production window regardless of snow
    Net: a partial, often brief output reduction. Rarely a sustained outage. NOT structural damage.
```

**What distinguishes winter storms from other hazards:** the mechanisms are **correlated across a geography** — a Uri-class polar vortex displacement brings extreme cold to an entire region simultaneously, so wellhead freezes, wind shutdowns, and solar reductions happen at the same time across hundreds of assets. This systemic, correlated nature is what made Uri so severe (not just one plant — the whole ERCOT gas fleet).

## 2 · Robustness & attribution

```text
mechanism (wellhead/pipe freeze → gas curtailment; blade icing → shutdown; snow → solar reduction)  ROBUST — physics + industry record
geography (Southern plains / Gulf Coast = low-winterization zone)                                   ROBUST — historical and FERC/NERC documented
Uri caused ~32 GW ERCOT thermal outage at peak                                                      FACTUAL — FERC/NERC report (2021-11), well-documented
a specific named plant was offline during Uri                                                        INFERRED from geography + mechanism; NOT directly in the substrate CF series
an observed Q1/Feb CF dip was caused by the freeze                                                  NOT separable — winter is seasonally low for gas (heat-rate economics) and solar (short daylight)
the exact MWh lost / $ impact at a given plant from a freeze event                                  UNSUPPORTED — block unless an outage record (EIA-930/ISO data) is available
forward return-period of a Uri-class event                                                          LOW skill from history alone — needs a climate model (blocked)
```

**Non-stationarity (standard climate caveat)**: polar vortex disruption / sudden stratospheric warming (SSW) events may be increasing the frequency of extreme cold intrusions into southern latitudes — an emerging but contested signal. Simultaneously, average winter temperatures are rising in most regions. Never state a return-period from event history alone; cap trend claims at directional.

## 3 · Winter Storm Uri — the canonical realized case

**Winter Storm Uri, February 10–20, 2021** — a displaced polar vortex delivered sustained Arctic air across the Southern plains. The canonical record:

```text
Geography:       Texas (ERCOT), Oklahoma, Arkansas, Louisiana, Mississippi were all affected
Temperature:     Houston reached 9°F (2021-02-15) — well below any design basis for Gulf Coast gas infrastructure
ERCOT outage:    ~32 GW of thermal generation offline at peak (FERC/NERC, Nov 2021 report); ~4.5 million TX homes lost power
Primary cause:   natural gas supply chain failure — wellhead freeze, instrument air failures, and generator-level equipment freeze
                 accounted for ~87% of the ERCOT unplanned outage (FERC/NERC)
Wind / solar:    a secondary contributor (~3 GW wind offline from icing; solar minimal in Feb TX)
Winterization:   the FERC/NERC report identified lack of cold-weather packages at Southern-latitude plants as the root cause;
                 plants with winterization equipment (e.g. some TX panhandle wind assets) continued operating
Economic damage: ~$195B total TX economic loss (Busby et al. 2021, UT Energy Institute)
```

Uri is the **authoritative grounding anchor** for this resource — it is in the InfraSure hazards news substrate AND in the public FERC/NERC record. Use it as a regional fact; do NOT use the substrate CF series to attribute a specific plant's outage.

## 4 · Why the winter CF dip is NOT the outage (the same discipline as `hail_solar` and `hurricane_high_wind_wind`)

Gas plants in ERCOT follow **heat-rate economics** — they often back down in mild winter months when demand is lower. Solar has short daylight in December–February regardless of weather. A February CF dip for either fuel is consistent with seasonal patterns, independent of any freeze event. A multi-day Uri forced outage (Feb 10–20) would be ~10 days inside an already seasonally-low February — **not separable at monthly resolution, and confounded by the seasonal minimum**. Conclusion: **the substrate CF series cannot ground a Uri→outage claim for a specific plant.** Monthly CF is *context only* here. Be honest: per-plant outage attribution stays blocked unless an outage record (EIA-930 / ISO real-time data) is available.

## 5 · The winterization gap — the structural vulnerability

The Uri mechanism was not primarily "it got cold" — it was **"Southern-latitude plants were built without cold-weather packages because it almost never got this cold."** This is the structural vulnerability this resource captures:

```text
Cold-weather package (CWP)      insulated / heat-traced pipes, instrument-air dryers, cold-weather lubricants,
                                 heated enclosures for sensitive equipment — standard in northern plants, absent in many TX/Gulf plants
Wellhead heat tracing            prevents water-and-condensate hydrates from blocking the wellhead at the gas supply side
Fuel supply contractual status   firm gas contract vs interruptible — interruptible gas is curtailed first in a shortage
Blade de-icing                   active (heated blade systems) or passive (special coatings) — not universally installed on TX wind
```

**The key insight**: a plant's freeze vulnerability is a function of its winterization specification, not just its geography — a TX panhandle wind farm WITH heated blades continued operating during Uri while a comparable farm without did not. This is what an analyst should probe, to the extent it is knowable from the substrate.

## 6 · Region / asset-class crosswalk

```text
extreme_cold × GAS / thermal (this resource — mechanism A)   wellhead/pipeline freeze → gas curtailment → forced outage
extreme_cold × WIND (this resource — mechanism B)            blade icing → rotor imbalance → protective shutdown
extreme_cold × SOLAR (this resource — mechanism C)           snow cover → output reduction; short daylight → reduced window
extreme_cold × nuclear                                        different (cooling-water supply, switchyard ice) — different resource
extreme_cold × hydro                                          ice on intakes / penstock — different resource
```

This crosswalk is why the catalog forks by mechanism (`resources/README.md` grain rule): extreme_cold×gas ≠ extreme_cold×wind ≠ extreme_cold×solar — each drives different `allowed_claims` and `blocked_claims`, but they are authored together here because Uri produced all three simultaneously and the correlated systemic exposure is the analytical point.

## 7 · Citations

```text
FERC / NERC Report on Uri (2021-11)                           "The February 2021 Cold Weather Outages in Texas and the South Central United States" — the authoritative record
NOAA NWS winter storm historical records / watches/warnings   https://www.weather.gov/
Busby et al. 2021 (UT Energy Institute)                       "Cascading risks: Understanding the 2021 Texas blackout" — $195B estimate
IEC 61400 wind turbine design cold-climate specs              IEC 61400-1 + TR 61400-24 (lightning/ice) — industry standard for blade icing
ERCOT post-event analysis (2021)                              https://www.ercot.com/ (outage timeline, generation-by-fuel data)
InfraSure hazards news (subcategory=winter_storm|freeze)      search_news(category=hazards, query="Uri"/"winter storm"/"freeze")
```

---

**See also**: `data_requirements.md` (where to pull event state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hail_solar/knowledge.md` · `../hurricane_high_wind_wind/knowledge.md` (sibling hazard patterns).
