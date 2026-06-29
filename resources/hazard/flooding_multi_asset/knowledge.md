# Knowledge — Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets (cited mechanism library)

> **Status**: draft 2026-06-29. The stable "why" for `flooding_multi_asset`. Live geography/event state comes from FEMA NFHL + NOAA NWS AHPS / USGS gauges + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding. Worked reference: `../weather_and_climate/el_nino_enso/knowledge.md`; sibling hazard patterns: `../hail_solar/knowledge.md`, `../hurricane_high_wind_wind/knowledge.md`.

## 1 · The mechanism

```text
floodwater (riverine crest, flash flood, or coastal backwater) reaches asset elevation
   → THREE distinct asset outcomes, by where the water arrives:

(A) GRID / SWITCHYARD — INUNDATION OUTAGE
    water reaches a low-lying substation / switchyard / collector → de-energization
    → outage for the inundation window + dry-out / inspection → recovery days-to-weeks
    A DELIVERY failure: the plant may be physically fine but cannot export.

(B) PLANT EQUIPMENT / FUEL STORAGE — FORCED OUTAGE + DAMAGE
    water reaches ground-level inverters / combiners / fuel tanks / pad electrical
    → forced outage + physical damage → long-lead component replacement

(C) WATER-SITED THERMAL — COOLING-INTAKE COMPROMISE
    a plant sited at tidewater / riverbank for cooling has its intake / screens / pump house
    compromised by debris-laden floodwater → derate or trip
```

The single biggest controllable / variance-driving factor is **site elevation relative to the flood surface** (equipment-pad height, flood walls, berms). The structural insight that makes this a portfolio question: **thermal/nuclear cooling siting concentrates flood exposure** — plants are deliberately placed at water for cooling.

## 2 · Robustness & attribution

```text
mechanism (inundation damages ground-level electrical / fuel / intake)   ROBUST — physical, well-documented (insurance + utility post-event literature)
geography (where flood hazard concentrates)                              ROBUST — FEMA NFHL + NWS/USGS gauge history are stable references
a realized flood hit watershed X near asset Y                            FACTUAL when corroborated (multi-source news + FEMA/NWS)
the forward PROBABILITY / depth at a given site                          LOW from zones alone — needs a flood model + site elevation (blocked here)
climate TREND in flood frequency/severity                                MEDIUM — precip-intensity increase is reasonably attributed; riverine-frequency trends are regional + land-use-confounded
```

**Non-stationarity** (standard climate/weather caveat): a FEMA flood zone is an odds band on a shifting baseline (land-use change, precip intensification, remapping), not a stationary return-period — never state a per-site return-period from the zone alone.

## 3 · State / event basis

- **Geography**: FEMA National Flood Hazard Layer (NFHL) flood zones (100-yr / 500-yr); NOAA NWS AHPS river forecasts + USGS stream gauges for riverine crest history. Coastal backwater overlaps the `sea_level_rise_surge` resource.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = flood | flooding | inundation`) carries `details_json` — `hazard_type`, `affected_area`, `operational_impact`, `affected_mw`, `event_date`. **Verify** each (the classifier can link to grid-customer flooding or a non-asset location, not the plant).

## 4 · Region / asset-class crosswalk

```text
flood × WATER-SITED THERMAL (gas/nuclear)   cooling-intake + ground-level electrical — the concentration insight (mechanism C/B)
flood × SOLAR                               ground-level inverters / combiner pads (mechanism B); modules usually above flood surface
flood × WIND                                turbine bases + collector substation (mechanism A/B); nacelle is high
flood × TRANSMISSION                        low-lying substations / switchyards — the delivery mechanism (A)
geography                                   Gulf Coast + major riverine corridors (Mississippi/Missouri/Ohio) carry the bulk of US flood exposure
```

## 5 · Canonical realized case (anchor to resolve in test 001)

**Hurricane Harvey (Aug 2017), Gulf Coast / Houston–Texas.** Harvey produced record rainfall and catastrophic riverine + urban flooding across the Texas Gulf Coast — the public, well-documented regional anchor for this resource. The disciplined claim is a **directional flood-exposure + mechanism** statement for water-sited thermal in the affected watershed, with the realized event as regional framing — **NOT** a per-plant damage claim. The in-substrate plant anchor (an operating thermal/solar asset in the Harvey floodplain, with a CF series spanning the event) is to be resolved via `get_plant`/`nearby_plants` in test 001; note monthly CF cannot isolate an inundation outage from seasonal variation.

## 6 · Citations

```text
FEMA National Flood Hazard Layer (NFHL) flood zones           https://www.fema.gov/flood-maps  /  msc.fema.gov
NOAA NWS AHPS river forecasts + USGS stream gauges            https://water.weather.gov/  /  https://waterdata.usgs.gov/
FEMA disaster declarations (Harvey: DR-4332-TX)              https://www.fema.gov/disaster/
utility flood-hardening / substation inundation literature   industry / EPRI / IEEE substation-flooding mitigation literature
InfraSure hazards news (subcategory=flood) — Harvey/TX        search_news(category=hazards, query="flood"/"flooding")
```

---

**See also**: `data_requirements.md` (where to pull the flood geography + event state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../sea_level_rise_surge/knowledge.md` (the coastal-water sibling) · `../hail_solar/knowledge.md` · `../hurricane_high_wind_wind/knowledge.md`.
