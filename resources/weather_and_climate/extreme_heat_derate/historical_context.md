# Historical Context — Extreme Heat Thermal Derate For Solar Assets

> **Status**: draft 2026-06-25.
>
> **Role**: `frames` + `external` evidence. This file informs the peak-coincidence and heat-stress context for `extreme_heat_derate`. It **never** grounds scoped assets in a new applied insight; re-ground every event, number, and entity live before use.

## How To Use This File

```text
USE       as historical context for heat-driven peak demand, solar's grid value, and the peak-hour materiality frame
DO NOT    use as plant-level thermal-derate magnitude, exact MWh loss, $ impact, or proof of a heat signal in monthly CF
```

## Event Ledger

### ERCOT Summer Heat Wave — June-July 2023

| Field | Notes |
|---|---|
| Geography / market | ERCOT / Texas. |
| What happened | EIA says a late-June/July 2023 heat wave drove record-breaking electricity demand in Texas, and ERCOT power plants increased output to meet elevated demand ([EIA ERCOT heat-wave article](https://www.eia.gov/todayinenergy/detail.php?id=57240), accessed 2026-06-25). |
| Mechanism illustrated | Heat is primarily a peak-load / peak-hour value event for solar exposure: PV output is valuable during hot afternoons, while thermal derate remains a modest intra-day shave. |
| Magnitude / impact | EIA says non-fossil resources contributed as much as **55%** of ERCOT generation on June 28-29 and **43%–47%** during evening peak load hours of 4-8 PM CT, while ERCOT added more than **4,000 MW** of wind and solar capacity between September 2022 and May 2023 ([EIA ERCOT heat-wave article](https://www.eia.gov/todayinenergy/detail.php?id=57240), accessed 2026-06-25). |
| Asset / actor relevance | Owners/offtakers should care less about large monthly energy loss and more about hot-afternoon performance during high-value hours. |
| What it licenses | Peak-coincidence materiality: the thermal-derate mechanism lands when demand and prices can matter most. |
| What it does NOT license | Exact module temperature, plant-level % derate, MWh, or revenue loss. |

### CAISO September 2022 Heat Wave — August 31-September 9, 2022

| Field | Notes |
|---|---|
| Geography / market | California ISO / Western heat wave. |
| What happened | CAISO's market performance report says California and much of the West experienced record-setting heat from August 31 through September 9, 2022, with 10 consecutive Flex Alerts and record-breaking load; the ISO maintained reliability without rotating outages ([CAISO September 2022 report](https://www.caiso.com/Documents/SummerMarketPerformanceReportforSeptember2022.pdf), accessed 2026-06-25). |
| Mechanism illustrated | Extreme heat creates simultaneous high demand, late-day net-load stress, and solar forecast/performance challenges; it does not imply monthly solar CF collapse. |
| Magnitude / impact | EIA says CAISO set a new record on September 6, 2022, relied heavily on natural gas, imports, and hydro during highest-demand hours, and natural gas supplied up to **60%** of the generation mix during brief periods that week ([EIA CAISO heat-wave article](https://www.eia.gov/Todayinenergy/detail.php?id=53939), accessed 2026-06-25). |
| Asset / actor relevance | Offtakers and owners with shaped/peak exposure should care about hot-hour performance and evening ramp, not just monthly generation. |
| What it licenses | A grid-context claim: heat materiality is about timing and system stress. |
| What it does NOT license | A plant-specific thermal-derate magnitude without cell-temperature / inverter thermal modeling. |

## Cross-Event Patterns

```text
PATTERN 1  Heat materiality is timing-driven: hot hours coincide with demand stress and higher value.
PATTERN 2  Solar often helps during heat waves; the derate is a modest shave inside high-irradiance months.
PATTERN 3  Monthly CF is the wrong measurement for thermal derate; plant-level model data is needed for exact magnitude.
```

## Sources

| Source | Use | Accessed |
|---|---|---|
| [EIA: Texas grid met record-breaking heat-wave demand](https://www.eia.gov/todayinenergy/detail.php?id=57240) | ERCOT heat-wave generation mix and added wind/solar capacity | 2026-06-25 |
| [CAISO September 2022 market performance report](https://www.caiso.com/Documents/SummerMarketPerformanceReportforSeptember2022.pdf) | CAISO heat-wave operations and reliability context | 2026-06-25 |
| [EIA: California fuel mix during September 2022 heat wave](https://www.eia.gov/Todayinenergy/detail.php?id=53939) | CAISO fuel-mix / natural-gas reliance figures | 2026-06-25 |

---

**See also**: `knowledge.md` · `resource.yml` · `data_requirements.md` · `../../../docs/method/resource_standard.md`.
