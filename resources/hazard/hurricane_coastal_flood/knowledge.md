# Knowledge — Hurricane Coastal Flood / Storm-Surge Exposure For Energy Assets

> **Status**: draft 2026-06-25. The stable "why" for `hurricane_coastal_flood`. Live storm, surge, and flood state comes from NOAA/NHC, FEMA, tide gages, SLOSH/P-Surge, and local flood sources pulled per test, dated. This file supplies mechanism and caveat discipline; it never substitutes for substrate grounding.

## 1 · The mechanism — water, not wind

The central discipline: **storm surge / coastal flooding is not the same claim as hurricane wind.** The high-wind resource asks whether wind causes turbine cut-out or structural loading. This resource asks whether water reaches critical plant components.

```text
hurricane / coastal storm
   -> storm surge + tide + waves + rainfall / drainage backup
   -> water reaches site / access road / substation / inverter pad / transformer / switchgear / fuel handling
   -> possible outcomes:
        (A) ACCESS LOSS         crews and equipment cannot reach site; outage/restart delayed
        (B) ELECTRICAL DAMAGE   inverters, transformers, switchgear, collection system, substation inundated
        (C) FUEL / COOLING      thermal plants lose fuel handling, pumps, cooling, or auxiliary systems
        (D) INTERCONNECTION     grid substation / line / switchyard unavailable even if plant itself is dry
   -> outage / repair / replacement duration depends on component, water depth, salinity, contamination, and spares
```

Water claims are component-specific. A plant centroid in a coastal county does not prove inundation. A FEMA flood-zone polygon or SLOSH envelope does not prove damage. Exact claims need elevation, component location, water depth, and damage/outage records.

## 2 · Robustness & attribution

```text
mechanism (water damages electrical / access / fuel systems)       ROBUST — engineering + flood-loss record
storm track / regional surge threat                                FACTUAL when dated (NHC / NOAA)
asset is near coast / floodplain / surge geography                  DIRECTIONAL from lat/lon/county/FEMA/SLOSH screen
site-specific inundation depth                                      NOT groundable without elevation + flood model
equipment damage / outage at plant X                               FACTUAL only with verified damage/outage record
exact EAL/PML/$ / insurance outcome                                BLOCKED — needs model-gpr / policy / adjuster evidence
```

## 3 · Public data stack — what grounds which part

| Input | Job | What it can support | What it cannot support alone |
|---|---|---|---|
| NOAA NHC track / advisories / HURDAT2 | **external · grounds** storm track and landfall | named storm path and timing | flood depth at plant |
| NHC storm surge products / P-Surge / SLOSH | **external · frames / may ground** surge envelope | regional inundation threat / scenario | equipment damage or exact water level at component |
| FEMA NFHL / FIS | **external · frames** regulatory flood zone / base flood elevation | long-term floodplain context | event-specific surge |
| NOAA tide gages / water-level observations | **external · grounds** observed water level at station | realized water level near a site | water at plant unless location/elevation mapped |
| USGS 3DEP / local lidar | **external · logic** elevation context | relative elevation where manually joined | flood damage without component heights |
| InfraSure plant substrate | **substrate · grounds** asset scope | location, capacity, owner, fuel, monthly generation context | flood-zone / elevation / outage attribution |
| Hazards news | **substrate · corroborates** realized event | named storm, affected area, affected MW when verified | source labels without verification |

## 4 · Asset-class crosswalk

```text
surge × SOLAR       inverter pads, transformers, collection substation, access roads; modules may survive water, electronics may not
surge × WIND        access roads, padmount transformers, collection systems, substations, port/O&M access; offshore/onshore differ
surge × GAS         fuel handling, pumps, electrical systems, cooling-water / intake systems, switchyard
surge × BATTERY     enclosures, HVAC, fire suppression, transformers; water + energized equipment is a severe operational risk
surge × TRANSMISSION/substation  switchgear, relays, transformers, control house; often the binding outage point
```

Because the mechanism is **component inundation**, the same named storm can matter differently for different asset classes. Keep the claim on the component pathway you can support.

## 5 · Geography and first-test anchor

Recommended first test: **Texas Gulf Coast / Houston-Galveston energy cluster**. Reasons:

```text
1. Dense energy infrastructure near bays / ship channels / coastal floodplain.
2. NOAA/NHC and local storm-surge references are strong.
3. The repo already has studio/off-substrate bottom-up work around Galveston / ship-channel surge, which makes the
   exposure logic familiar — but any new claim must be re-grounded live.
```

Do not reuse studio numbers as facts. Use them only as orientation/form; re-fetch substrate assets and external surge/flood sources for the test.

## 6 · Non-stationarity

Sea-level rise raises the baseline on which any surge lands, so a "same" storm can produce more frequent or deeper coastal flooding over time. However, landfall track, tide timing, local bathymetry, drainage, levee performance, and asset elevation determine site impact. Trend claims stay directional unless a named sea-level / hydraulic model is used.

## 7 · Sources

| Source | Use | URL |
|---|---|---|
| NOAA NHC / HURDAT2 / advisories | storm track, landfall, surge products | https://www.nhc.noaa.gov/ |
| NOAA SLOSH / P-Surge | surge scenarios / probabilistic surge | https://slosh.nws.noaa.gov/ |
| FEMA NFHL / Flood Insurance Studies | regulatory flood zone / BFE context | https://msc.fema.gov/ |
| NOAA tide gauges / CO-OPS | observed water levels | https://tidesandcurrents.noaa.gov/ |
| USGS 3DEP | elevation context | https://www.usgs.gov/3d-elevation-program |
| ADCIRC / SFINCS / CoSMoS references | hydraulic-model context | https://adcirc.org/ · https://sfincs.readthedocs.io/ |
| Learning vault source map | flood and hurricane data stack | `~/Desktop/Learning/Reference/modeling-and-research/data-sources/hazard-datasets/natural-hazard-datasets-catalog.md` |

---

**See also**: `data_requirements.md` (retrieval plan + gaps) · `resource.yml` (structured contract) · `../hurricane_high_wind_wind/` (sibling wind mechanism) · `../wildfire/` (multi-mechanism hazard discipline).
