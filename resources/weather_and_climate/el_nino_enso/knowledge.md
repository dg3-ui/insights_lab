# Knowledge — El Niño / ENSO For Renewable Assets

> **Status**: v0 domain reference, 2026-06-05.
>
> **Purpose**: the **mechanism library** for ENSO exposure analysis — what ENSO is, how it is measured and where to pull it, how it teleconnects to US power-infrastructure conditions (rated by how trustworthy each link is), and how that maps to InfraSure entities. This is the **why/how** layer.
>
> **What this is NOT**: not the method (that is `resource.md`), not the data (that is the MCP substrate). This file supplies the *mechanism* and *caveat* slots of a claim; the substrate supplies the *assets*; NOAA supplies the *state*. Use it to reason correctly, then **cite it** — never let it substitute for retrieving asset data.

## 0. The Three Layers (orientation)

```text
DATA       who / where / how much   →  MCP substrate (search_plants, get_plant)        [retrieve, cite as_of]
KNOWLEDGE  why / how the mechanism  →  THIS FILE + the cited external sources           [reason, cite source]
STATE      what is happening now    →  NOAA CPC / IRI ENSO forecast (pull at test time) [external, has a clock]
```

A good ENSO exposure claim needs all three. This file is the middle layer. The mechanism is cited to authoritative climate sources (§7); the live STATE must be pulled fresh every test (§3).

## 1. What ENSO Is

The **El Niño–Southern Oscillation (ENSO)** is a coupled ocean–atmosphere oscillation in the tropical Pacific. It has three phases:

```text
EL NIÑO   warm phase  — equatorial Pacific SSTs above average; Walker circulation weakens;
                        subtropical jet strengthens over the southern US
NEUTRAL   neither     — SSTs near average
LA NIÑA   cool phase  — equatorial Pacific SSTs below average; Walker circulation strengthens;
                        polar jet dominates, subtropical jet weak
```

ENSO is the single largest source of **year-to-year** climate variability outside the seasonal cycle, and it shifts the **odds** of regional weather months in advance. That predictability-with-lead-time is exactly why it is analytically useful — and the probabilistic, odds-shifting nature is exactly why claims built on it stay **directional**, not deterministic (§6).

## 2. Why It Matters For Power Infrastructure

ENSO does not act on assets directly. It nudges regional **weather** — cloud cover, precipitation, temperature, snowpack, wind, storm frequency — which in turn moves the variables InfraSure assets care about:

```text
ENSO phase → regional weather tendency → asset-relevant variable → revenue / risk implication
   El Niño → wetter/cloudier CA winter  → lower POA irradiance    → lower winter solar generation
   El Niño → milder northern winter     → lower heating demand    → softer winter peak / prices
   La Niña → drier Southwest            → drought / wildfire       → curtailment, outage, panel soiling
   La Niña → wetter Pacific NW          → higher snowpack          → stronger spring/summer hydro
```

## 3. How ENSO Is Measured (and where to pull it)

| Index | What it is | Threshold / use |
|---|---|---|
| **ONI** (Oceanic Niño Index) | 3-month running mean of Niño-3.4 SST anomaly | Official episode definition: **≥ +0.5 °C (El Niño) / ≤ −0.5 °C (La Niña)** sustained for **5 consecutive overlapping seasons** |
| **Niño-3.4 SST anomaly** | weekly/monthly SST anomaly in the Niño-3.4 box | the real-time pulse ahead of the ONI |
| **SOI** | Tahiti–Darwin sea-level pressure difference | atmospheric confirmation of the ocean signal |
| **ENSO Alert System** | CPC status flag | `Watch` (conditions favorable to develop), `Advisory` (in effect), or none |

**Pull the STATE live every test** — it has a freshness clock. Authoritative sources in §7.

```text
┌─ SNAPSHOT (2026-06-05 — ILLUSTRATIVE; RE-PULL BEFORE ANY REAL USE) ──────────────┐
│ Alert: El Niño Watch · now ENSO-neutral · Niño-3.4 ≈ +0.4 °C (subsurface warm)    │
│ Forecast: ~82% El Niño emerges MJJ 2026 · ~96% El Niño persists DJF 2026-27       │
│ Strength: UNCERTAIN — no strength category exceeds 37% (weak/moderate/strong TBD) │
│ Source: NOAA CPC ENSO Diagnostic Discussion, accessed 2026-06-05                  │
└───────────────────────────────────────────────────────────────────────────────────┘
```

The strength uncertainty is itself analytically important: teleconnection signals are generally stronger and more reliable in strong events than weak ones, so "El Niño is likely but strength is unknown" already **caps confidence** before any asset is named.

## 4. Teleconnections That Matter (rated by robustness)

ENSO's regional fingerprints are **probabilistic shifts in the odds**, strongest in DJF (Northern Hemisphere winter). Robustness varies a lot by region and variable — treat the rating column as a confidence ceiling.

| Region (US) | El Niño (DJF) tendency | La Niña (DJF) tendency | Robustness | Power-infra relevance |
|---|---|---|---|---|
| **California / Southwest** | wetter, cloudier, more storms | drier, sunnier, drought-prone | **Moderate–High** (one of the more reliable signals; stronger in strong events) | **Solar**: El Niño ↓ winter irradiance; La Niña ↑ irradiance but ↑ wildfire/curtailment/soiling |
| **Pacific Northwest** | drier, milder; lower snowpack | wetter, cooler; higher snowpack | Moderate | **Hydro**: snowpack → spring/summer runoff; La Niña tends to favor PNW hydro |
| **Northern tier / Upper Midwest** | milder winters | colder winters | Moderate | **Demand**: heating load + winter peak prices |
| **Gulf Coast / Southeast** | wetter, cooler | drier, warmer | Moderate | mixed solar/demand; flooding risk |
| **Texas / ERCOT (winter cold)** | — | sometimes linked to cold outbreaks | **Low / noisy** | tempting but unreliable — do **not** assert ENSO→Texas-freeze causation (e.g. Feb-2021 Uri occurred in La Niña, but attribution is contested) |
| **Atlantic hurricane season** (JJA–ON) | **suppressed** (more wind shear) | **enhanced** | **High** | Gulf/SE/offshore-wind & coastal-asset storm-outage odds |

## 5. Solar-Specific Mechanism (the v0 focus)

Utility-scale PV output scales with **plane-of-array irradiance**, which falls with cloud cover (and, secondarily, soiling/snow/precip). Winter is already the low season (low sun angle, short days), so a wetter/cloudier El Niño winter depresses an **already-low** baseline.

```text
El Niño → strengthened subtropical jet → more winter storms over CA/SW
        → more cloud cover + precip → lower winter POA irradiance
        → lower winter capacity factor on CA/SW solar fleets
```

The substrate already holds the baseline this perturbs. Desert Sunlight 300 (`57993`) monthly capacity factor:

```text
summer peak ≈ 0.38   (Jun)        winter trough ≈ 0.13   (Dec/Jan)
```

**The discipline-defining counter-example (in our own data):** winter 2022-23 was a *La Niña* winter, yet California was anomalously **wet** (atmospheric rivers) and Desert Sunlight's Q1-2023 CF ran low (~0.15–0.20). That is the *opposite* of the "dry La Niña" composite — a single season defying the odds. It is the cleanest possible argument for why ENSO→solar claims are capped at **directional / LOW** (§6): ENSO shifts the odds; it does not set the outcome of any one winter.

## 6. From Knowledge To Confidence (how this caps claims)

Map the weakest link to the claim's confidence — never upgrade past it:

```text
forecast lead/strength   DJF from June ≈ 6-month lead; occurrence ~96% BUT strength uncertain   → caps at LOW–MED
teleconnection robustness CA/SW winter precip = Moderate–High; most others lower                 → caps at MED at best
single-season noise       any one winter can defy the composite (see 2022-23)                    → caps at LOW
downstream modeling       production / LMP not modeled here                                      → BLOCK quantitative claims
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────
NET for ENSO → asset exposure:  DIRECTIONAL, LOW confidence.  Never "High". Never a number.
```

## 7. Region Crosswalk (climate region → InfraSure entity)

| Climate region | InfraSure scoping | Note |
|---|---|---|
| California | `state="CA"` (≈ CAISO) | `search_plants(iso="CAISO")` returns `[]` — filter unwired; use `state`, confirm per-plant via `get_plant.regions.iso_rto` |
| Southwest | `state IN (AZ, NM, NV)` | desert solar belt |
| Pacific Northwest | `state IN (WA, OR, ID)` (≈ BPA / WECC-NW) | hydro-weighted |
| Texas | `iso`/`region = "ERCOT"` | projects carry `region`; plants use `state="TX"` |
| Southeast | `state IN (FL, GA, …)` (≈ SERC) | — |

## 8. Sources (pull STATE live; cite mechanism)

| Source | Use | URL |
|---|---|---|
| NOAA CPC ENSO Diagnostic Discussion | official current state + DJF forecast + Alert status | https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/ensodisc.shtml |
| NOAA CPC ENSO probabilities / ONI | strength probabilities, ONI history | https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso/roni/probabilities/ |
| IRI ENSO Forecast | model-ensemble plume + probabilities | https://iri.columbia.edu/our-expertise/climate/forecasts/enso/current/ |
| NWS / NOAA ENSO explainer | teleconnection background | https://www.weather.gov/twc/enso |

**Citation rule**: every material claim cites either a substrate tool result (with `as_of`) or an external source name + access date. The mechanism statements in this file are general climate science (cite the sources above); the *current state* must always carry the date it was pulled.
