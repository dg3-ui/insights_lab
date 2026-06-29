# Knowledge — Tornado Exposure For Solar, Wind, and Substation Assets (cited mechanism library)

> **Status**: draft 2026-06-29. The stable "why" for `tornado_solar_wind`. Live geography/event state comes from NOAA SPC tornado climatology + storm reports + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding. Worked reference: `../weather_and_climate/el_nino_enso/knowledge.md`; sibling hazard patterns: `../hail_solar/knowledge.md`, `../hurricane_high_wind_wind/knowledge.md`.

## 1 · The mechanism

```text
tornado (EF-scale winds far above design-basis sustained wind) + airborne debris loading over an asset
   → arrays / trackers flattened · turbine blades snapped or tower toppled · substation equipment destroyed
   → OUTRIGHT structural destruction of the assets inside the path → long-lead rebuild
```

The defining physical property — and the reason this is its own resource rather than a footnote to hurricane — is **footprint**: a tornado path is typically a few hundred meters wide. Damage is **binary and narrow**: total loss if the path crosses the asset, nothing if it misses. The variance-driving factors are therefore **geographic intersection** (is the asset in the high-touchdown-density corridor?) and **structural design margin** (wind-class rating, debris-resistant racking), not a fleet-wide derate fraction.

## 2 · Robustness & attribution

```text
mechanism (EF-scale wind + debris destroys arrays/turbines/substations)   ROBUST — physical, well-documented
geography (where tornadoes concentrate)                                   ROBUST — SPC touchdown-density climatology is stable (Tornado/Dixie Alley)
a realized tornado hit corridor X near asset Y                            FACTUAL when corroborated (multi-source news + SPC/NWS survey)
the forward per-asset STRIKE probability                                  LOW — touchdown density is AREAL, not per-asset; needs a tornado-hazard model (blocked here)
climate TREND in tornado frequency/intensity                              LOW attribution — among the LEAST attributable severe-weather signals; an eastward Dixie-Alley shift is debated
```

**Non-stationarity** (standard caveat): tornado climatology is an areal odds field on a debated baseline — never convert a touchdown density into a per-site return-period without a hazard model.

## 3 · State / event basis

- **Geography**: NOAA Storm Prediction Center (SPC) tornado climatology + storm reports + EF-scale damage surveys. The Southern Plains (Tornado Alley) and the Southeast (Dixie Alley) carry the bulk of US tornado activity.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = tornado | severe_storm`) carries `details_json` — `hazard_type`, `affected_area`, `operational_impact`, `affected_mw`, `event_date`. **Verify** each.

## 4 · Region / asset-class crosswalk

```text
tornado × SOLAR        arrays/trackers flattened, modules shredded by debris — total loss in the path (mechanism A)
tornado × WIND         blades snapped / nacelle / tower failure — total loss in the path (mechanism A)
tornado × SUBSTATION   switchyard / transformer structures flattened — delivery loss (mechanism B)
tornado × thermal      building-enclosed plant equipment is more shielded — generally a different (lower) exposure
geography              Southern Plains (OK/KS/TX) + Dixie Alley (MS/AL/AR/TN) carry the bulk of exposure
```

## 5 · Canonical realized case (anchor to resolve in test 001)

**Southern Plains tornado climatology, Oklahoma–Texas corridor.** Rather than a single famous strike, the honest anchor for this resource is the **catastrophic-but-localized** statistical reality: SPC documents the Southern Plains as a global tornado maximum, and utility-scale solar + wind buildout there places a growing nameplate base inside the corridor — but the annual probability of any single asset being in a path is low. The disciplined claim is a **directional corridor-exposure + mechanism** statement with the catastrophic-but-localized framing; the in-substrate plant anchor (an operating wind/solar asset in the corridor) is to be resolved via `get_plant`/`nearby_plants` in test 001. **Do not annualize a total loss across the full nameplate**, and do not read a strike off monthly CF.

## 6 · Citations

```text
NOAA SPC tornado climatology + storm reports + EF surveys     https://www.spc.noaa.gov/  (WCM page, storm reports)
NWS tornado warnings + damage assessment toolkit              https://www.weather.gov/
Enhanced Fujita (EF) scale basis                              NWS / Texas Tech WiSE — EF-scale damage-indicator standard
wind-turbine / PV structural wind-class + debris literature   IEC 61400-1 (wind classes) · ASCE 7 (wind loads) · industry/reinsurance
InfraSure hazards news (subcategory=tornado)                  search_news(category=hazards, query="tornado"/"severe storm")
```

---

**See also**: `data_requirements.md` (where to pull the geography + event state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hurricane_high_wind_wind/knowledge.md` (the wide-field wind sibling — the contrast) · `../hail_solar/knowledge.md`.
