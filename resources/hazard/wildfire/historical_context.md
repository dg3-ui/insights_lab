# Historical Context — Wildfire Exposure For Solar, Transmission, and Grid-Connected Assets

> **Status**: draft 2026-06-25.
>
> **Role**: `frames` + `external` evidence. This file informs wildfire mechanism, actor relevance, confidence caps, and blocked claims. It **never** grounds scoped assets in a new applied insight; re-ground every event, number, and entity live before use.

## How To Use This File

```text
USE       as historical context for ignition liability, PSPS logic, smoke/solar impacts, and mechanism separation
DO NOT    use as plant-specific smoke-loss proof, PSPS curtailment proof, ignition liability determination, or $ loss model
```

## Event Ledger

### Camp Fire — Butte County, California, November 8, 2018

| Field | Notes |
|---|---|
| Geography / market | Northern California / PG&E territory; transmission-ignition mechanism. |
| What happened | PG&E's SEC filing states CAL FIRE identified the Camp Fire start near Tower :27/222 on PG&E's Caribou-Palermo 115 kV transmission line and that the line relayed/deenergized around 6:15 AM on November 8, 2018 ([PG&E SEC filing](https://www.sec.gov/Archives/edgar/data/1004980/000100498019000008/R17.htm), accessed 2026-06-25). A PG&E CPUC letter reports about 153,336 acres burned, 18,793 structures destroyed, and 85 civilian fatalities, while noting the cause was still under investigation at that time ([PG&E CPUC letter](https://www.cpuc.ca.gov/-/media/cpuc-website/files/uploadedfiles/cpucwebsite/content/news_room/newsupdates/2018/12-11-18.pdf), accessed 2026-06-25). |
| Mechanism illustrated | Transmission ignition liability is distinct from fire damage to a generator and distinct from PSPS curtailment. It is a legal/regulatory tail risk. |
| Magnitude / impact | Butte County's public report describes criminal charges against PG&E and states the indictment included 85 felony counts tied to unlawfully and recklessly causing the Camp Fire and 84 involuntary manslaughter counts naming victims ([Butte County Camp Fire public report](https://www.buttecounty.ca.gov/DocumentCenter/View/1952/June-16-2020---Camp-Fire-Public-Report), accessed 2026-06-25). |
| Asset / actor relevance | Transmission owners and lenders face a different exposure than solar/wind/gas asset owners: ignition liability can dominate the financial consequence. |
| What it licenses | A mechanism-separation claim: ignition liability must be treated as its own blocked/model/legal layer. |
| What it does NOT license | A claim that a specific line caused a current/future fire, or any plant-level $/liability result. |

### California Wildfire Smoke and Solar Forecast Error — September 2020

| Field | Notes |
|---|---|
| Geography / market | California / CAISO solar fleet. |
| What happened | A peer-reviewed Environmental Research Letters study found September 2020 wildfire smoke reduced CAISO solar power production by about **10%–30%** during peak production hours on smoke-influenced days and improved solar forecast bias by nearly **50%** when aerosol fields were included ([Juliano et al., ERL](https://iopscience.iop.org/article/10.1088/1748-9326/ac5143), accessed 2026-06-25). |
| Mechanism illustrated | Smoke is an irradiance / forecast error mechanism, not structural damage to panels. |
| Magnitude / impact | NCAR summarized the same finding: during heavy smoke, California solar energy production fell **10%–30%** between noon and 4 PM compared with the same days in prior years, and forecasts overestimated production by an average of **27%** on smokiest days ([NCAR/UCAR](https://news.ucar.edu/132875/california-wildfire-smoke-dimmed-solar-energy-2020), accessed 2026-06-25). |
| Asset / actor relevance | Solar owners/offtakers should treat smoke as a forecast and revenue-shape risk, not a module-damage event. |
| What it licenses | A regional smoke/solar mechanism and forecast-error claim when smoke data is available. |
| What it does NOT license | Plant-level smoke-loss attribution from monthly CF or a current plant's MWh loss without hourly generation + smoke/irradiance data. |

## Cross-Event Patterns

```text
PATTERN 1  Wildfire has multiple mechanisms: ignition liability, smoke irradiance, physical fire damage, and PSPS.
PATTERN 2  Smoke-output claims need sub-monthly irradiance / generation; monthly CF is not enough.
PATTERN 3  Fire-weather history can sharpen severity and actor relevance, but legal ignition causality remains blocked.
```

## Sources

| Source | Use | Accessed |
|---|---|---|
| [PG&E SEC Camp Fire filing](https://www.sec.gov/Archives/edgar/data/1004980/000100498019000008/R17.htm) | Camp Fire ignition / line details | 2026-06-25 |
| [PG&E CPUC Camp Fire letter](https://www.cpuc.ca.gov/-/media/cpuc-website/files/uploadedfiles/cpucwebsite/content/news_room/newsupdates/2018/12-11-18.pdf) | Camp Fire acreage/structures/fatalities context | 2026-06-25 |
| [Butte County Camp Fire public report](https://www.buttecounty.ca.gov/DocumentCenter/View/1952/June-16-2020---Camp-Fire-Public-Report) | Criminal/legal context | 2026-06-25 |
| [Juliano et al. wildfire smoke/solar forecast study](https://iopscience.iop.org/article/10.1088/1748-9326/ac5143) | Smoke-driven solar reduction / forecast bias | 2026-06-25 |
| [NCAR/UCAR smoke solar summary](https://news.ucar.edu/132875/california-wildfire-smoke-dimmed-solar-energy-2020) | Accessible summary of solar reduction and forecast error | 2026-06-25 |

---

**See also**: `knowledge.md` · `resource.yml` · `data_requirements.md` · `../../../docs/method/resource_standard.md`.
