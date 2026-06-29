# Knowledge — Riverine Flood / Inland Inundation Exposure For Energy Assets

> **Status**: draft 2026-06-25. The stable "why" for `riverine_flood`. Live river stage, flood zone, and event state comes from USGS NWIS, NOAA NWS AHPS, FEMA NFHL, and event-specific sources pulled per test, dated. This file supplies mechanism and caveat discipline; it never substitutes for substrate grounding.

## 1 · The mechanism — water from upstream, not the sea

The central discipline: **riverine flooding is not storm surge.** Storm surge comes from ocean wind-driven water. Riverine flooding comes from a river channel exceeding its banks — driven by heavy upstream precipitation, snowmelt, ice-jam breakup, dam releases, or levee/dam failure. The hazard reaches energy assets deep inland, along river corridors and floodplains that coastal-flood resources never touch.

```text
heavy precipitation / rapid snowmelt / ice-jam breakup / dam release / levee / dam failure
   -> elevated river stage / channel overflow / backwater flooding
   -> water reaches site / access road / substation / switchyard /
      cooling intake / fuel handling / transmission corridor
   -> possible outcomes:
        (A) ACCESS LOSS        crews and equipment cannot reach site; outage/restart delayed
        (B) ELECTRICAL DAMAGE  transformers, switchgear, inverters, collection systems, substations inundated
        (C) COOLING / FUEL     gas/coal plants lose riverine cooling-water intake or fuel-delivery access
        (D) STRUCTURAL         scour, foundation undermining, or debris impact on structures
        (E) INTERCONNECTION    transmission lines / substations in flood path unavailable even if plant is dry
```

Water claims are **component- and elevation-specific**. A plant centroid in a river county does not prove inundation. A FEMA AE-zone polygon does not prove depth in a specific event. Exact claims need component elevation, event water surface, and damage/outage records.

## 2 · Hazard sub-types — different lead times, different footprints

| Sub-type | Driver | Lead time | Footprint | Key source |
|---|---|---|---|---|
| Mainstem / major-river flood | Multi-day heavy rain / snowmelt over large basin | Days to weeks | Wide river corridor, floodplain, backwater | USGS NWIS, NOAA AHPS |
| Flash flood | Intense localized convective rain | Hours or less | Narrow canyon / small watershed, culverts | NWS Flash Flood Guidance, local gages |
| Snowmelt / spring runoff | Warming temperatures over snowpack | Weeks | Mountain-to-valley river corridors | NRCS SNOTEL, USGS, NWS |
| Dam / levee failure | Structure failure or intentional releases | Minutes to hours | Downstream floodplain | USACE NID, state dam safety |
| Ice-jam flood | River ice breakup blocking flow | Hours | Short reach below ice jam | NWS, USACE |

Riverine flood resources should **label which sub-type applies** when evidence permits; different sub-types carry different lead times and asset-relevance patterns.

## 3 · Asset-class crosswalk

```text
flood × GAS THERMAL    cooling-water intake (riverine source plants most exposed); fuel delivery disruption;
                       switchyard flooding; access road loss; control building inundation
flood × HYDRO          paradoxically, extreme inflow can cause forced outage / spillway operations / dam-safety
                       constraints; upstream basin flooding can damage access and transmission; dam failure upstream
                       of an asset is its own catastrophic event
flood × SOLAR          substation / inverter pad inundation; access road loss; collection cabling at grade;
                       modules themselves may survive submersion, electronics / connections may not
flood × BATTERY        enclosure / HVAC / fire-suppression systems; energized equipment + water = severe risk
flood × COAL           coal-pile runoff / washout; railcar / barge access; cooling-water intake
flood × TRANSMISSION   line foundations / tower scour; substation flooding (often the binding outage point)
```

The binding failure point is **often the substation or switchyard**, not the generating unit itself — the same pattern as coastal flooding, but originating from a river rather than the sea.

## 4 · FEMA flood zone taxonomy (riverine)

| Zone | Meaning | Use in this resource |
|---|---|---|
| AE | 1% annual chance flood (BFE defined) | Primary riverine exposure screen |
| AO | 1% annual shallow sheet / ponding (1–3 ft) | Flat terrain, drainage concerns |
| AH | 1% annual ponding (BFE defined) | Same as AO but with base flood elevation |
| X (shaded) | 0.2% annual chance (500-yr) | Background context only |
| X (unshaded) | Minimal flood hazard | Out of scope |
| VE / V | Coastal velocity / wave action | Coastal resource, not this one |

FEMA maps are **long-run regulatory designations** based on hydraulic models with a fixed vintage. They do not forecast actual water depth in a specific event, and they may be outdated in fast-developing watersheds. Use as a screen and label the map's effective date.

## 5 · Robustness and attribution

```text
mechanism (water damages electrical / cooling / access / structural components)    ROBUST — engineering + flood-loss record
river stage / regional flood condition                                             FACTUAL when USGS/AHPS-sourced and dated
asset is near a river / in a FEMA AE zone                                         DIRECTIONAL from lat/lon/county/FEMA screen
site-specific inundation depth                                                     NOT groundable without elevation + flood model
equipment damage / outage at plant X                                               FACTUAL only with verified damage/outage record
exact EAL/PML/$ / insurance outcome                                                BLOCKED — needs model-gpr / policy / adjuster evidence
stationary return-period claim                                                     BLOCKED — non-stationarity (§6)
```

## 6 · Non-stationarity

Precipitation extremes are becoming more intense in many regions, making the historical flood-frequency record a non-stationary baseline. A "100-year" event defined from pre-2000 records does not carry the same meaning today. Trend claims stay directional unless a named hydraulic / climate-attribution study is cited. This cap applies to all riverine-flood resources.

## 7 · Public data stack

| Input | Job | What it can support | What it cannot support alone |
|---|---|---|---|
| USGS NWIS streamflow + stage gages | **external · grounds** river condition | dated stage, exceedance, flood category | water depth at plant site |
| NOAA NWS AHPS river forecasts | **external · grounds** forward stage outlook | forecast stage + flood category by forecast point | site inundation |
| FEMA NFHL / FIRM (riverine) | **external · frames** regulatory flood zone | AE/AO/AH zone designation, map vintage | event-specific depth |
| USACE NID | **external · frames** dam/levee context | dam location, height, storage, hazard class | failure probability |
| NOAA Atlas 14 | **external · frames** precipitation frequency | regional design storm context | plant-level flood return period |
| InfraSure plant substrate | **substrate · grounds** asset scope | location, capacity, owner, fuel, monthly generation | flood zone / elevation / outage attribution |
| Hazards news | **substrate · corroborates** realized event | named event, affected area, affected assets when verified | unverified labels |

## 8 · Sources

| Source | Use | URL |
|---|---|---|
| USGS NWIS / WaterWatch | Streamflow gages + flood stage + percentiles | https://waterdata.usgs.gov/ / https://waterwatch.usgs.gov/ |
| NOAA NWS AHPS | River stage forecasts + flood categories | https://water.weather.gov/ahps/ |
| FEMA NFHL / MSC | Riverine flood zones + FIS | https://msc.fema.gov/ |
| USACE NID | Dam inventory + hazard class | https://nid.usace.army.mil/ |
| NOAA Atlas 14 | Precipitation frequency | https://hdsc.nws.noaa.gov/hdsc/pfds/ |
