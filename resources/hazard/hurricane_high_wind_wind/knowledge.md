# Knowledge — Hurricane / High-Wind Exposure For Wind Assets (cited mechanism library)

> **Status**: draft 2026-06-14. The stable "why" for `hurricane_high_wind_wind`. Live track/event state comes from NOAA NHC (best-track / advisories) + the InfraSure `hazards` news category (subcategory=hurricane|high_wind), pulled per test, dated. Cite everything; this never substitutes for substrate grounding. Sibling reference: `../hail_solar/knowledge.md`.

## 1 · The mechanism — TWO distinct claim types

The single most important discipline here: **a hurricane does two physically different things to a wind turbine, and they are different claim types.**

```text
(A) TEMPORARY CUT-OUT  (the COMMON, recoverable case)
    sustained wind climbs toward the turbine cut-out speed (~25 m/s / ~55 mph for a typical onshore machine)
       → the control system FEATHERS the blades + SHUTS DOWN the rotor (a protective action, by design)
       → output drops to ~zero for the duration of the high-wind window (hours-to-days)
       → the turbine RESTARTS once wind drops back into the operating band → output recovers
    Net: a short availability/output loss, NOT damage. This is the turbine working as designed.

(B) LASTING STRUCTURAL DAMAGE  (the RARE, design-exceeding case)
    peak gusts exceed the turbine's design wind class (IEC: Class I ~ 50 m/s / Class S for typhoon)
       → blade failure · nacelle / yaw-drive damage · tower buckling / collapse
       → coastal sites add STORM-SURGE exposure to foundations, pad transformers, collection substation
       → repair/replacement → output loss over WEEKS-TO-MONTHS (lasting)
    Net: a capital loss + extended outage. Requires roughly Cat 3+ winds at the turbine.
```

Hurricane category matters: most modern onshore turbines ride out a **Cat 1–2** landfall via cut-out (A); structural damage (B) becomes plausible at **Cat 3+** design-exceeding gusts. **Hurricane Beryl made TX landfall as a Category 1** (2024-07-08, near Matagorda) — squarely in the cut-out regime, NOT the damage regime. Conflating the two is the headline overclaim this resource blocks.

## 2 · Robustness & attribution

```text
mechanism (cut-out above ~25 m/s; structural damage above design class)   ROBUST — IEC 61400 design basis, physical
geography (where landfalling TCs concentrate — the Gulf/Atlantic coast)    ROBUST — NHC HURDAT2 best-track is stable
a named storm made landfall near coastal asset X                           FACTUAL when corroborated (NHC + hazards news)
a wind plant's turbines CUT OUT during the storm                           INFERRED from mechanism (substrate cannot show it directly)
a hurricane caused an observed monthly-CF dip                              NOT separable — the July low IS the summer wind lull (see §4)
lasting turbine DAMAGE from a sub-Cat-3 storm                              UNSUPPORTED — block unless a damage record exists
the forward PROBABILITY / return-period at a given site                    LOW skill from track history alone — needs a TC model (blocked)
climate TREND in TC intensity/landfall                                     CONTESTED — low-to-medium attribution; rapid-intensification
                                                                            + poleward shift are emerging, landfall-frequency is not settled
```

**Non-stationarity** (standard climate/weather caveat): TC climatology is an odds-shift on a *shifting* baseline (warmer SSTs, more rapid intensification, debated track shifts), not a stationary return-period — never state a return-period from a historical track record alone.

## 3 · State / event basis

- **Track / geography**: NOAA National Hurricane Center (NHC) best-track / HURDAT2 + live advisories — the **Texas Gulf Coast (Lower Rio Grande Valley → Coastal Bend → Matagorda/Brazoria) is in the US landfalling-hurricane corridor**. SPC carries non-tropical high-wind / derecho reports.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = hurricane | high_wind`) carries `details_json` — `hazard_type`, `event_name`, `affected_area`, `operational_impact`, `affected_mw`, `event_date`, sometimes a qualitative `damage_estimate`. **Verify** each — and note a structural quirk found in test 001: **TX hurricane articles in the substrate link to nuclear / hydro / gas plants and to grid-customer outages, NOT to wind turbines** (Beryl → South Texas Project nuclear "threatened"; Helene → Douglas Dam hydro; one Lake Placid solar article mis-tagged "hurricane" was actually a *tornado*). The wind-turbine operational impact is **not** in the substrate.

## 4 · Why the monthly CF dip is NOT the storm (the discipline that defines this resource)

Coastal/Gulf Texas wind has a pronounced **summer wind minimum** — July–August are the lowest-CF months every year, hurricane or not. Worked from the in-substrate anchor (Peyton Creek Wind Farm LLC, 62417, Matagorda; `get_plant.generation`):

```text
month     CF      note
2021-07   0.129   summer lull (no TX-landfall hurricane)
2022-07   0.238
2023-07   0.206
2024-07   0.129   ← Beryl made landfall 2024-07-08 in this county … but this CF is IN-LINE with the 2021 lull
2025-07   0.187   summer lull (no hurricane)
2024-08   0.090
2025-08   0.078   ← LOWER than the Beryl-month neighbor, with NO hurricane
2025-03   0.020   ← near-zero output, NO storm (maintenance/curtailment) — shows monthly CF swings wildly for non-hazard reasons
```

A multi-day Beryl cut-out (early July) would be a handful of near-zero days inside an already-low month — **invisible at monthly resolution and confounded by the seasonal minimum**. Conclusion: **the substrate cannot ground a Beryl→CF claim for wind.** Monthly CF is *context only* here; the realized-impact leg that made `hail_solar` strong does NOT exist for this resource. Be honest: confidence stays low.

## 5 · Region / asset-class crosswalk

```text
hurricane × WIND turbine (this resource)   cut-out (temporary) + structural/surge damage (lasting, Cat 3+) — TWO claim types
hurricane × solar PV                       module/tracker wind-load + surge/flood (a different mechanism → hail_solar's sibling)
hurricane × gas / thermal / nuclear        flood/surge to plant systems + grid-side customer outage (different resource)
hurricane × hydro / dam                    inflow/flood management (the Beryl/Helene substrate hits are mostly THIS)
geography                                  the TX/Gulf coast (and Atlantic coast) carries US landfalling-TC wind exposure
```

This crosswalk is *why* the catalog forks by mechanism (`resources/README.md` grain rule): hurricane×wind ≠ hurricane×solar ≠ hurricane×gas — each drives different `blocked_claims`.

## 6 · Canonical realized case (the worked anchor — note its limits)

**Hurricane Beryl (NHC; TX landfall 2024-07-08, ~Cat 1, near Matagorda) over coastal/Gulf TX wind.** The event is corroborated in the InfraSure `hazards` news (Reuters: ~1M+ TX customers without power; Newsweek: South Texas Project nuclear "threatened", Matagorda/Bay City). The nearest in-substrate wind anchor is **Peyton Creek Wind Farm LLC (EIA 62417, 151.2 MW, Matagorda County, 47× Nordex AW125/3150, hub 87.5m, RWE Clean Energy, COD 2020)** — same county as landfall, with a CF series spanning the event. But per §4, **the substrate shows no separable Beryl signal** — the worked insight in `examples/applied_insight_001.md` is therefore a *directional coastal-exposure + mechanism* claim, with the realized event as regional framing, NOT a wind-plant damage claim. (The bigger sibling Peyton Creek II, 67700, came online in 2025 — after Beryl — so it has no pre/post window at all.)

## 7 · Citations

```text
NOAA NHC best-track / HURDAT2 + advisories (Beryl 2024)        https://www.nhc.noaa.gov/   (Beryl: AL022024)
NOAA SPC high-wind / convective-wind reports                   https://www.spc.noaa.gov/climo/reports/
IEC 61400 wind-turbine design classes (cut-out, class I/S)     industry standard (turbine design basis)
InfraSure hazards news (subcategory=hurricane) — Beryl/TX      Reuters (2024-07-11), Newsweek (2024-07-08)
turbine hurricane survivability / cut-out + surge literature   industry / reinsurance literature (e.g. NREL, AWEA/ACP, Lloyd's)
```

---

**See also**: `data_requirements.md` (where to pull the track + event state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hail_solar/knowledge.md` (the sibling hazard pattern).
