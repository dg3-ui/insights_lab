# Knowledge — Drought / Low-Hydro Exposure For Hydropower Assets (cited mechanism library)

> **Status**: draft 2026-06-25. The stable "why" for `drought_low_hydro`. Live drought, snowpack, streamflow, and reservoir state must be pulled per test, dated, and matched to the scoped hydro geography. This file supplies the mechanism + caveat slots; it never substitutes for asset retrieval.

## 0 · The three layers

```text
DATA       who / where / how much   -> InfraSure substrate (hydro plants, capacity, owner, generation)  [retrieve, cite as_of]
KNOWLEDGE  why the mechanism works  -> THIS FILE + public hydrology / hydro operations references       [reason, cite source]
STATE      what water condition now -> USDM / NOAA-NIDIS-CPC / USGS gages / SNOTEL / reservoir storage [pull live, date]
```

A defensible low-hydro claim needs all three. The common failure mode is jumping from "state X is in drought" to "plant Y will lose Z MWh." This resource blocks that jump unless basin/reservoir/operations evidence is available.

## 1 · The mechanism

```text
precipitation deficit / warm winter / low snowpack / high evaporative demand
   -> lower runoff into river basin and reservoirs
   -> lower reservoir storage and/or lower natural streamflow
   -> reduced hydro energy volume, reduced dispatch flexibility, or altered seasonal shape
   -> commercial relevance depends on market price shape, contract structure, water rights, environmental-flow rules,
      flood-control rules, and whether the facility is conventional hydro or pumped storage
```

Hydro is not a simple "fuel input" resource. Water has multiple jobs: generation, flood control, irrigation, municipal supply, fish flows, recreation, and treaty / compact obligations. In many basins, generation is the residual after non-power constraints. That is why the resource can support **directional exposure** today but blocks exact plant-level MWh or $ impacts.

## 2 · Robustness & attribution

```text
mechanism (low inflow/storage can reduce hydro energy/flexibility)       ROBUST — basic hydrology + hydro operations
drought state over a basin / state                                      FACTUAL when dated (USDM / NOAA / NIDIS)
snowpack / SWE deficit in a Western basin                               FACTUAL when dated (NRCS SNOTEL / NOHRSC)
low streamflow at a USGS gage                                           FACTUAL when dated, but gage-to-plant mapping matters
a specific plant's monthly generation dip was caused by drought          NOT separable without basin/reservoir/dispatch evidence
exact MWh / revenue loss at a plant                                     NOT grounded here — needs hydro model + operations data
forward return-period of low inflow                                     BLOCKED from current drought state alone
```

**Non-stationarity**: drought, snowpack, runoff timing, evapotranspiration, and rain-vs-snow fraction are shifting. Historical drought frequency is not a stationary return-period. Trend claims stay directional unless a named climate/hydrology model is used.

## 3 · Public data stack — what grounds which part

| Input | Job | What it can support | What it cannot support alone |
|---|---|---|---|
| US Drought Monitor (USDM) | **external · state** drought category | weekly drought condition over a county/state/basin | hydro generation loss |
| NOAA/NIDIS/CPC drought outlooks | **external · state** persistence/development outlook | near-term drought tendency, with issue date | plant-level inflow or generation |
| USGS WaterWatch / NWIS streamflow gages | **external · grounds** streamflow condition | current/historical flow percentile at a gage | reservoir inflow at a plant unless mapped |
| NRCS SNOTEL / snow water equivalent | **external · grounds** snowpack runoff proxy | basin snowpack percentile for Western hydro | exact generation without reservoir operations |
| NOAA NOHRSC / SNODAS snow products | **external · state** snow cover / SWE grids | regional snowpack context | plant-level production |
| Bureau of Reclamation / state reservoir storage | **external · state** storage condition | reservoir level / storage percent, where named | dispatchable energy without rule curve and obligations |
| EIA / InfraSure monthly generation | **substrate · context** hydro seasonality | observed historical generation and owner context | single-cause drought attribution |

The strongest v0 claim is a **screen**: scoped hydro assets + dated drought/snowpack/streamflow/storage stress + mechanism + actor relevance. The quantified loss leg is the future model-wired upgrade.

## 4 · Hydro technology and scope caveats

```text
conventional hydro       water inflow + reservoir / run-of-river constraints -> energy and flexibility exposure
pumped storage           drought may affect water availability / reservoir operation, but market arbitrage and pumping dominate
run-of-river             more directly tied to streamflow; less storage buffer
large storage reservoir  more buffered; rule curves and non-power obligations dominate timing
```

Do not mix these without naming the distinction. If the substrate does not identify facility type, treat all hydro as a first-pass screen and cap confidence.

## 5 · Recommended first scopes

```text
CAISO / California hydro      drought + snowpack + reservoir storage are well documented; state=CA is a workable first screen
Pacific Northwest hydro       snowpack / streamflow sensitivity is central; market boundaries are less clean than CAISO
Colorado River / Southwest    reservoir storage is the key input; plant-to-reservoir linkage matters
```

The first MCP test should use one scope only, probably California hydro >= 50 MW. California has strong public drought and reservoir reporting, and the CAISO state proxy follows the existing weather-resource pattern. Do not make a national hydro conclusion from it.

## 6 · Sources

| Source | Use | URL |
|---|---|---|
| US Drought Monitor | weekly drought category | https://droughtmonitor.unl.edu/ |
| NOAA / NIDIS Drought.gov | drought status and outlook context | https://www.drought.gov/ |
| NOAA CPC drought outlooks | drought persistence / development | https://www.cpc.ncep.noaa.gov/ |
| USGS NWIS / WaterWatch streamflow | gage streamflow and percentiles | https://waterdata.usgs.gov/ |
| NRCS SNOTEL / Water and Climate Center | snowpack / SWE by basin | https://www.nrcs.usda.gov/wps/portal/wcc/home/ |
| NOAA NOHRSC / SNODAS | snow analysis / modeled snowpack | https://www.nohrsc.noaa.gov/ · https://nsidc.org/data/g02158 |
| Bureau of Reclamation / state reservoir dashboards | reservoir storage where relevant | https://www.usbr.gov/ |
| Learning vault source map | public hazard/water datasets | `~/Desktop/Learning/Reference/modeling-and-research/data-sources/hazard-datasets/natural-hazard-datasets-catalog.md` |

---

**See also**: `data_requirements.md` (retrieval plan + gaps) · `resource.yml` (structured contract) · `../el_nino_enso/` and `../extreme_heat_derate/` (weather-resource discipline).
