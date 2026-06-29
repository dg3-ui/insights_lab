# Knowledge — Lightning Exposure For Wind, Solar, and Electrical-Plant Assets (cited mechanism library)

> **Status**: draft 2026-06-29. The stable "why" for `lightning_multi_asset`. Live geography/event state comes from NOAA / Vaisala NLDN flash-density climatology + NWS thunderstorm outlooks + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding. Worked reference: `../weather_and_climate/el_nino_enso/knowledge.md`; sibling: `../hail_solar/knowledge.md`.

## 1 · The mechanism

```text
cloud-to-ground lightning over / near an asset → TWO claim types:

(A) DIRECT STRIKE — STRUCTURE / BLADE / NACELLE
    a strike attaches to the tallest object → blade composite delamination, nacelle / control damage,
    tower current path → component outage → repair (a blade can be hours-to-weeks)
    Wind turbines are the tallest structures in open terrain → the most direct-strike-exposed class.

(B) INDUCED SURGE — INVERTERS / TRANSFORMERS / CONTROL ELECTRONICS
    a nearby strike couples a fast transient into wiring → inverter / transformer / SCADA / BMS damage
    → component outage across ANY generation type, even without a direct hit
```

The defining property — and why this resource is framed differently from the catastrophe hazards — is **frequency profile**: lightning is **high-frequency, lower-per-event-severity**, managed by **design** (air termination, surge protective devices (SPDs), grounding, blade lightning-protection systems (LPS) with tip receptors). The right frame is **cumulative component risk + design adequacy**, not a single catastrophic event. The variance-driving factor is **flash density × structure height × LPS adequacy** (LPS status not in the substrate).

## 2 · Robustness & attribution

```text
mechanism (strike / surge damages blades / inverters / transformers / electronics)   ROBUST — physical, well-documented (IEC 61400-24 for wind)
geography (where flash density concentrates)                                         ROBUST — NLDN cloud-to-ground climatology is stable (Gulf Coast / Florida max)
a realized lightning event affected area X near asset Y                              FACTUAL when corroborated (multi-source news)
the forward per-asset STRIKE RATE / component-failure probability                    LOW from climatology alone — needs a strike model + LPS status (blocked here)
climate TREND in lightning frequency                                                 LOW attribution — methodologically contested; never assert a trend as settled
```

**Non-stationarity** (standard caveat): flash-density climatology is an odds field, not a per-asset strike count — and because the hazard is design-managed, geographic exposure ≠ realized damage when LPS is adequate.

## 3 · State / measurement basis

- **Geography**: NOAA / Vaisala National Lightning Detection Network (NLDN) cloud-to-ground flash-density climatology — the **Gulf Coast / Florida** carries the US flash-density maximum. NWS thunderstorm / convective outlooks for near-term state.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = lightning | convective_storm`) carries `details_json`. **Verify** each (lightning is often a sub-cause inside a broader convective event).

## 4 · Region / asset-class crosswalk

```text
lightning × WIND          DIRECT STRIKE to blade tip / nacelle — tallest in open terrain → most exposed (mechanism A); blade LPS receptors are the mitigation
lightning × SOLAR         INDUCED SURGE into inverters / combiners / SCADA (mechanism B); SPDs + grounding are the mitigation
lightning × GAS / thermal INDUCED SURGE into control electronics / transformers (mechanism B)
lightning × TRANSMISSION  direct strike + induced surge into transformers / substation electronics (mechanisms A/B); shield wires + arresters
geography                 Gulf Coast / Florida (flash-density max) + the Southeast carry the bulk of US exposure
```

## 5 · Canonical realized case (anchor to resolve in test 001)

**Gulf Coast / Florida flash-density maximum.** Lightning has no single famous catastrophe — that absence *is* the point. The honest anchor is the **cumulative** reality: NLDN places the highest US cloud-to-ground flash density along the Gulf Coast and Florida, where utility-scale wind and solar accumulate component-replacement and availability drag over time rather than a single loss event. The disciplined claim is a **directional flash-density-exposure + mechanism** statement framed as cumulative component risk + design adequacy; the in-substrate plant anchor (an operating wind/solar asset in the flash-density band, test 001 = FL–TX) is to be resolved via `get_plant`/`nearby_plants`. Monthly CF cannot resolve a component-level strike.

## 6 · Citations

```text
NOAA / Vaisala NLDN cloud-to-ground flash-density climatology   https://www.weather.gov/ · Vaisala Annual Lightning Report
NWS thunderstorm / convective outlooks                          https://www.spc.noaa.gov/ · https://www.weather.gov/
IEC 61400-24 wind-turbine lightning-protection standard         IEC TR 61400-24 — blade LPS / receptor design basis
IEEE / industry surge-protection (SPD) + grounding literature   IEEE C62 series · industry PV / substation surge-protection literature
InfraSure hazards news (subcategory=lightning)                  search_news(category=hazards, query="lightning"/"storm")
```

---

**See also**: `data_requirements.md` (where to pull the flash-density state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hail_solar/knowledge.md` · `../hurricane_high_wind_wind/knowledge.md` (sibling hazard patterns).
