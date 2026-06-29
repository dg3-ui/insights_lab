# Knowledge — Sea Level Rise & Storm Surge Exposure For Coastal Thermal, Nuclear, and Grid Assets (cited mechanism library)

> **Status**: draft 2026-06-29. The stable "why" for `sea_level_rise_surge`. Live state comes from NOAA tide-gauge SLR trends + NOAA NHC surge (SLOSH/P-Surge) + FEMA coastal zones + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding. Worked reference: `../weather_and_climate/el_nino_enso/knowledge.md`; sibling: `../hurricane_high_wind_wind/knowledge.md` (the WIND side).

## 1 · The mechanism

```text
TWO timescales over the same coastal geography — keep them DISTINCT:

(CHRONIC) SEA LEVEL RISE — baseline creep, DECADES
    relative SLR (global rise + local vertical land motion) raises the mean water level
    → more frequent nuisance / tidal flooding of low-lying coastal equipment
    → erosion of the cooling-intake + switchyard DESIGN FLOOD BASIS the plant was built to
    A planning-horizon risk — largely uninsurable creep, not a claim event.

(ACUTE) STORM SURGE — event inundation, HOURS
    a tropical / extratropical storm pushes a surge above the tide
    → inundation of the switchyard / cooling intake / pump house → outage + damage
    An event — NHC-forecastable during a storm; insurable under coastal flood / surge sub-limits.
```

The variance-driving factor for both is **site elevation relative to the water surface** (not in the substrate). The structural insight: **tidewater cooling siting concentrates exposure** in large, long-lived, hard-to-relocate capital (thermal + nuclear). This is the **water** side of a coastal storm; the **wind** side (cut-out, blade/structural damage) is `hurricane_high_wind_wind` — cross-reference, never double-count.

## 2 · Robustness & attribution

```text
mechanism (inundation compromises intake / switchyard / low-lying equipment)   ROBUST — physical, well-documented
chronic SLR trend                                                              HIGH attribution — among the best-attributed climate signals (thermal expansion + land-ice melt); local relative rate adds vertical land motion
acute surge envelope for a coastal reach                                       ROBUST — NHC SLOSH / historical high-water marks
a realized surge hit reach X near asset Y                                      FACTUAL when corroborated (multi-source news + NHC/FEMA)
the YEAR a site is permanently inundated / forward surge probability at a site LOW from trend alone — needs an SLR/surge model + site elevation (blocked here)
```

**Non-stationarity** here runs the other way from most hazards: the baseline is *rising with high confidence*, so a historical design flood basis is **optimistic**, not stationary — but a specific inundation depth or year still requires a model + elevation, which the substrate lacks.

## 3 · State / measurement basis

- **Chronic**: NOAA tide-gauge relative-SLR trends + the NOAA Sea Level Rise Viewer (rate per gauge, decadal projections by scenario).
- **Acute**: NOAA NHC storm-surge (SLOSH / P-Surge) + historical high-water marks; FEMA coastal flood zones (VE / coastal-A).
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = surge | coastal_flood | sea_level`) carries `details_json`. **Verify** each.

## 4 · Region / asset-class crosswalk

```text
SLR/surge × NUCLEAR (tidewater)     cooling-intake + safety-related siting — highest-consequence chronic + acute exposure
SLR/surge × GAS / thermal (coastal) cooling-intake + ground-level electrical (mechanism A/B)
SLR/surge × TRANSMISSION            low-lying coastal substations (mechanism B)
SLR/surge × OFFSHORE-WIND LANDFALL  export-cable landings + onshore substations — emerging exposure (Atlantic)
geography                           Gulf Coast + Southeast Atlantic tidewater carry the bulk of US coastal-generation exposure
```

## 5 · Canonical realized cases (anchors to resolve in test 001)

**Acute anchor — Hurricane Sandy (Oct 2012) coastal surge.** Sandy's surge inundated low-lying coastal electrical infrastructure across the NY/NJ tidewater — the public, well-documented anchor for the ACUTE mechanism (switchyard/substation inundation). Disciplined use: a regional event framing for surge exposure, not a per-plant damage claim.

**Chronic anchor — Gulf Coast / Southeast tidewater thermal + nuclear siting.** The CHRONIC mechanism is best illustrated by the simple structural fact that many large thermal and nuclear plants are sited at tidewater for cooling, placing their design flood basis under a rising baseline. The in-substrate plant anchor (an operating coastal thermal/nuclear asset, test 001 = Gulf Coast / TX) is to be resolved via `get_plant`/`nearby_plants`; note monthly CF is largely irrelevant for the chronic horizon and cannot resolve an acute surge.

## 6 · Citations

```text
NOAA tide-gauge relative-SLR trends + Sea Level Rise Viewer    https://tidesandcurrents.noaa.gov/sltrends/ · https://coast.noaa.gov/slr/
NOAA NHC storm surge (SLOSH / P-Surge) + high-water marks      https://www.nhc.noaa.gov/surge/
FEMA coastal flood zones (VE / coastal-A)                      https://msc.fema.gov/
Hurricane Sandy coastal-infrastructure surge record (2012)     FEMA / DOE / utility post-event reports
coastal-power-plant SLR adaptation + intake design literature  EPRI / DOE / NRC (nuclear siting) literature
InfraSure hazards news (subcategory=surge|coastal_flood)       search_news(category=hazards, query="storm surge")
```

---

**See also**: `data_requirements.md` (where to pull the SLR + surge state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field + non-stationarity standard) · `../hurricane_high_wind_wind/knowledge.md` (the WIND side) · `../flooding_multi_asset/knowledge.md` (the riverine/inland sibling).
