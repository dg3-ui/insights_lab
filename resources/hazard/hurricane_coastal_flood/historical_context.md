# Historical Context — Hurricane Coastal Flood / Storm-Surge Exposure

> **Status**: draft 2026-06-25.
>
> **Role**: `frames` + `external` evidence. This file informs coastal-flood mechanism, confidence caps, caveats, and blocked claims. It **never** grounds scoped assets in a new applied insight; re-ground every event, number, and entity live before use.

## How To Use This File

```text
USE       as historical context for water-to-component pathways, substation/access failure, and outage restoration risk
DO NOT    use as plant-specific flood depth, equipment damage, outage duration, insurance outcome, or $ loss model
```

## Event Ledger

### Hurricane Sandy / Nor'easter — Northeast U.S., October-November 2012

| Field | Notes |
|---|---|
| Geography / market | New York / New Jersey / Mid-Atlantic and Northeast electric infrastructure. |
| What happened | DOE says Sandy and the following Nor'easter produced peak outages across 21 affected states totaling **8.6 million customers** without power, with severe energy infrastructure damage concentrated in New York and New Jersey ([DOE Sandy overview](https://www.energy.gov/sites/prod/files/2013/05/f0/DOE_Overview_Response-Sandy-Noreaster_Final.pdf), accessed 2026-06-25). |
| Mechanism illustrated | Storm surge flooded low-lying substations and made them inoperable until water receded, equipment was dried, tested, replaced where necessary, and re-energized. DOE Situation Report 7 says PSE&G brought three flooded substations back online and continued work on other river-adjacent stations ([DOE Sandy Situation Report 7](https://www.energy.gov/sites/prod/files/2012_SitRep7_Sandy_10312012_300PM.pdf), accessed 2026-06-25). |
| Magnitude / impact | NERC's Sandy event analysis says about **264 transmission assets** tripped over the New York power system, **20,007 MW** of generation capacity was rendered unavailable over the event, and about **8.35 million** electric customer outages were reported by late October 29 ([NERC Sandy event analysis](https://www.nerc.com/globalassets/our-work/reports/event-reports/hurricane_sandy_ear_20140312_final.pdf), accessed 2026-06-25). |
| Asset / actor relevance | Lenders and owners should care about substation/control-house elevation and recovery logistics, not just plant centroid or wind category. |
| What it licenses | A component-pathway claim: low-lying substations and electrical systems can be the binding outage point in coastal flooding. |
| What it does NOT license | Exact site flood depth or damage for a current plant without elevation + event inundation data. |

### Hurricane Harvey — Texas Gulf Coast, August 2017

| Field | Notes |
|---|---|
| Geography / market | ERCOT Gulf Coast; Corpus Christi, Houston/Galveston, Beaumont/Port Arthur. |
| What happened | EIA says Harvey caused substantial electricity outages as power plants and transmission infrastructure in South Texas and along the Gulf Coast were affected by high winds and significant flooding; more than **10,000 MW** of ERCOT generating capacity and many transmission/distribution lines experienced forced outages ([EIA Harvey article](https://www.eia.gov/todayinenergy/detail.php?id=32892), accessed 2026-06-25). |
| Mechanism illustrated | Rain/flooding affected generator fuel supplies, transmission infrastructure connecting generators to the grid, and personnel access to generating facilities ([EIA Harvey article](https://www.eia.gov/todayinenergy/detail.php?id=32892), accessed 2026-06-25). |
| Magnitude / impact | NERC says Harvey made about **225 transmission assets** impacted, several low-lying stations flooded and became completely inoperable, and maximum unavailable generation capacity reached **10,992 MW** ([NERC Harvey event analysis](https://www.nerc.com/globalassets/our-work/reports/event-reports/nerc_hurricane_harvey_ear_20180309.pdf), accessed 2026-06-25). |
| Asset / actor relevance | Gulf Coast energy clusters need access-road, substation, fuel-system, and interconnection resilience checks. |
| What it licenses | A coastal-cluster exposure claim: flooding and access/interconnection loss can matter even when the generating unit itself is not the damaged component. |
| What it does NOT license | A specific plant's flood depth, equipment damage, outage duration, or insurance outcome. |

## Cross-Event Patterns

```text
PATTERN 1  Coastal flood risk is component-specific: substation, transformer, access road, fuel/cooling system,
           and interconnection can drive outage before the prime mover matters.
PATTERN 2  Regional outage / unavailable MW figures are useful historical context but not plant-damage proof.
PATTERN 3  Elevation and flood-zone joins are the missing data layer; county/lat-lon is only a screen.
```

## Sources

| Source | Use | Accessed |
|---|---|---|
| [DOE Sandy overview](https://www.energy.gov/sites/prod/files/2013/05/f0/DOE_Overview_Response-Sandy-Noreaster_Final.pdf) | Sandy customer outages and response recommendations | 2026-06-25 |
| [DOE Sandy Situation Report 7](https://www.energy.gov/sites/prod/files/2012_SitRep7_Sandy_10312012_300PM.pdf) | Flooded substation restoration context | 2026-06-25 |
| [NERC Sandy event analysis](https://www.nerc.com/globalassets/our-work/reports/event-reports/hurricane_sandy_ear_20140312_final.pdf) | Sandy transmission/generation outage figures | 2026-06-25 |
| [EIA Harvey grid article](https://www.eia.gov/todayinenergy/detail.php?id=32892) | Harvey generation/transmission outage mechanism | 2026-06-25 |
| [NERC Harvey event analysis](https://www.nerc.com/globalassets/our-work/reports/event-reports/nerc_hurricane_harvey_ear_20180309.pdf) | Harvey unavailable generation / transmission assets | 2026-06-25 |

---

**See also**: `knowledge.md` · `resource.yml` · `data_requirements.md` · `../../../docs/method/resource_standard.md`.
