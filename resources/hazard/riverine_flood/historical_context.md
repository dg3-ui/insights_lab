# Historical Context — Riverine Flood / Inland Inundation Exposure For Energy Assets

> **Status**: draft 2026-06-25. **Role**: frames + external evidence only. This file supplies mechanism illustration, magnitude anchors, materiality calibration, and confidence caps for the `riverine_flood` resource. It **never** grounds scoped assets in a new applied insight — every substrate number and plant identity must be re-grounded live via MCP before use. All figures below are sourced as verified on 2026-06-25; re-verify before citing in any external deliverable.

---

## How To Use This File

```
USE
  Read before drafting to calibrate what riverine flood events have actually caused
    in terms of mechanism, scale, and asset type
  Cite a verified event to anchor a "this is what this hazard does" framing
  Use magnitude figures (MW offline, $ damage, ft above flood stage) as
    order-of-magnitude context for the mechanism being described
  Reference event sub-types (mainstem slow-rise vs. flash, dam-adjacent vs.
    open corridor) to select the correct knowledge.md sub-type label
  Use blocked-claim rows to remind yourself what NOT to emit in any new insight

DO NOT
  Re-use a historic event's plant identity as a current insight's scoped asset
    (entity is dated; re-ground live before naming)
  Convert a verified event figure into a site-specific forecast or return-period
    claim for a different asset or basin
  Treat any "$" figure here as a model output, insurance figure, or EAL/PML
    (these are observed event costs, not forward modeled losses)
  Cite a "search-corroborated only" item as primary source in an external deliverable
  Use any historic generation-loss figure to infer future CF at a named plant
```

---

## Event Ledger

### 1 · 2019 Missouri–Mississippi Spring Flood — Cooper Nuclear Station & WAPA Hydropower

| Field | Notes |
|---|---|
| **Geography / market** | Missouri River corridor, Nebraska; upstream WAPA mainstem dams (Oahe, Garrison, and four others), North Dakota / South Dakota / Nebraska; MISO footprint |
| **What happened** | Extreme spring runoff and snowmelt produced record-high Missouri River stages across the lower basin. Cooper Nuclear Station (Brownville, NE) declared an NRC Notification of Unusual Event (NOUE) at 5:46 a.m. on March 15, 2019, when the river reached 899.05 ft MSL — the NRC-level threshold. The river crested at 900.6 ft MSL on March 18, 2019. The plant remained online throughout. NOUE status exited at 4:01 p.m. on March 24 when the river fell to 896 ft MSL — a 9-day event window. ([NPPD press release](https://www.nppd.com); [power-technology.com](https://www.power-technology.com), accessed 2026-06-25) Meanwhile, the six USACE-managed Missouri River mainstem dams generated 13 billion kWh in 2019 vs. a long-term average of ~9.4 billion kWh/yr since 1967 — 38% above the long-run mean. Oahe Dam: 4.2B vs. 2.7B kWh average. Garrison Dam: 3.2B vs. 2.2B kWh average. WAPA sold at least $40 million in excess hydropower over 2018–2019 combined. ([world-energy.org, AP wire, Jan 2020](https://www.world-energy.org/article/5921.html), accessed 2026-06-25) Separately, Offutt AFB (OPPD service territory) suffered 720 million gallons of inundation, destroying or severely damaging 137 structures (>$700M total losses). OPPD de-energized base equipment rapidly enough that only one switchgear unit was lost; subsequent recovery included five new duct banks and rerouted circuits that had run beneath the runway — an 18-month reconstruction project with phased electrical refurbishment extending across multiple subsequent years. ([OPPD The Wire, oppdthewire.com](https://www.oppdthewire.com), accessed 2026-06-25) |
| **Mechanism illustrated** | §1 (water from upstream, mainstem / spring-runoff sub-type); §2 (snowmelt/runoff sub-type — days-to-weeks lead time, wide corridor); §3 asset crosswalk: nuclear → NRC emergency classification thresholds; hydro → paradoxical generation *increase* from extreme inflow (§3 hydro); transmission/distribution → substation inundation (OPPD switchgear) |
| **Magnitude / impact** | Cooper Nuclear (820 MW gross / 764 MW net per EIA): crested 0.9 ft below protective-offline threshold (901.5 ft MSL) and 1.4 ft below NRC Alert threshold (902 ft MSL); NOUE duration 9 days; plant never offline. WAPA 6-dam system: +38% above long-run average generation; $40M+ in surplus hydropower revenue (2-year total). Offutt AFB: >$700M total facility losses; 1 switchgear unit lost despite rapid de-energization. |
| **Asset / actor relevance** | Nuclear operators (threshold-based NRC classification disciplines operator behavior well before physical damage); hydro operators and WAPA offtakers (extreme inflow is a revenue tailwind, not only a threat); distribution utilities with flood-zone substation infrastructure (OPPD pattern: de-energization speed determined loss severity) |
| **What it licenses** | Directional: mainstem spring flood events can place nuclear plants in NRC NOUE classification without causing generation loss, if plant is above flood-stage water surface; directional: extreme-inflow events produce hydro generation surplus that is not uniformly negative for owners/offtakers; directional: distribution switchgear vulnerability is component- and elevation-specific, and rapid de-energization can limit loss extent |
| **What it does NOT license** | Exact flood depth at Cooper or any plant in a future event; return-period claims; plant-level generation attribution; exact dollar loss, EAL, or PML; generalization from this event to any specific scoped asset in a new insight without re-grounding the named entity against live MCP data |

---

### 2 · 2011 Missouri River Flood — Fort Calhoun Nuclear Station (OPPD) Extended Outage

| Field | Notes |
|---|---|
| **Geography / market** | Missouri River corridor, Nebraska (Blair, NE); MISO footprint |
| **What happened** | Fort Calhoun Nuclear Generating Station (478 MW net / OPPD) entered cold shutdown on April 9, 2011 for a scheduled refueling outage — weeks before floodwaters arrived. From approximately June through September 2011, the Missouri River surrounded the station. On June 6, OPPD declared an NRC NOUE (Level 1). On June 7, a switchgear room fire interrupted spent fuel pool cooling for approximately 90 minutes, with a ~3°F temperature rise in the pool; OPPD declared an NRC Alert (Level 2). On June 19, the river reached 1,005.5 ft elevation against the plant's site grade of 1,004 ft, with design tolerance to 1,014 ft. On June 26, a 2,000-ft rubber AquaDam berm was punctured by earthmoving equipment, flooding the facility; plant managers disconnected from the external grid and ran safety systems from on-site diesel power. The river crested at approximately 1,006 ft, some 36 feet above normal. ([World Nuclear News](https://www.world-nuclear-news.org/Articles/Fort-Calhoun-defends-against-flood), accessed 2026-06-25) Pre-existing safety problems discovered during the outage — not flood damage alone — extended the shutdown. OPPD spent $26 million in June 2011 alone: $20 million in plant protection work and $6 million replacing lost generating capacity. ([Wikipedia, 2011 Missouri River flood, citing OPPD statement July 13, 2011](https://en.wikipedia.org/wiki/2011_Missouri_River_floods), accessed 2026-06-25) Fort Calhoun did not restart until December 2013 — over 2.5 years offline. ([UCS blog, blog.ucs.org](https://blog.ucs.org/mike-jacobs/wind-in-the-great-plains-and-the-flood-that-shut-fort-calhoun-nuclear-plant-353/), accessed 2026-06-25) Before restart, OPPD spent $180 million recommissioning and cleared approximately 450 corrective items. (Wikipedia Fort Calhoun article; UCS blog, accessed 2026-06-25) The NRC implemented special oversight under IMC 0350 effective December 13, 2011. Cooper Nuclear Station (764 MW net / EIA) also issued a NOUE on June 19, 2011, ending July 12 when the river dropped to 895.8 ft. Cooper operated throughout. ([Wikipedia, 2011 Missouri River flood](https://en.wikipedia.org/wiki/2011_Missouri_River_floods), accessed 2026-06-25) |
| **Mechanism illustrated** | §1 (mainstem slow-rise flood, multi-week duration); §2 (mainstem/major-river sub-type; dam/levee-adjacent failure mode: AquaDam berm puncture = improvised protection failure); §3 (nuclear crosswalk: NRC classification hierarchy, grid disconnection, diesel backup; coal crosswalk: spent fuel and safety systems at flood risk when grid disconnected) |
| **Magnitude / impact** | Fort Calhoun: 478 MW offline >2.5 years (UCS blog, EIA); $26M acute flood-protection cost (June 2011 alone); $180M recommissioning spend pre-restart. Cooper Nuclear: 764 MW (EIA); NOUE declared, full operation maintained throughout (~23 days). Flood crest: ~1,006 ft, 36 ft above normal, site grade at 1,004 ft — 1.5 ft overtopping of site grade, 8 ft margin to design tolerance (1,014 ft). |
| **Asset / actor relevance** | Nuclear operators (combined pre-existing deficiency + flood risk; secondary protection failure — AquaDam breach — caused grid disconnect); OPPD ratepayers/investors (extended outage driven primarily by pre-existing safety backlog, not flood alone — causation is mixed); NRC oversight signal (IMC 0350 = heightened scrutiny layer) |
| **What it licenses** | Directional: improvised temporary flood-protection (flexible berms) carries meaningful failure risk; a flooded switchgear room is a credible outage trigger even when the plant was already offline for unrelated reasons; $26M acute cost is an order-of-magnitude anchor for event-window expenditure at a ~500 MW nuclear asset. Secondary: extended outage costs can dwarf acute flood-protection costs when pre-existing safety issues compound flood exposure. |
| **What it does NOT license** | Attribution of the 2.5-year outage to flooding alone — UCS, EIA, and the NRC IMC 0350 record confirm that pre-existing safety deficiencies were the primary driver. The $71/MWh vs. $20/MWh generation-cost-vs-market figure attributed in some narratives to this event actually describes the 2016 retirement economics (different temporal context — do not use). No exact depth, EAL, PML, return-period, or outage-duration claim for any other asset. |

---

### 3 · 1993 Great Midwest Flood — Regional Power Outages & Callaway Nuclear Operation

| Field | Notes |
|---|---|
| **Geography / market** | Mississippi and Missouri River basins, nine-state footprint (April–October 1993); Missouri, Iowa, Illinois epicenter |
| **What happened** | The Great Flood of 1993 was one of the most destructive US riverine flood events of the 20th century, causing approximately $15 billion in damages across nine states and 50 deaths. ([NOAA NWS Davenport, weather.gov/dvn/071993_greatflood](https://www.weather.gov/dvn/071993_greatflood), accessed 2026-06-25) In Des Moines, IA: more than 40,000 customers lost power when floodwaters overwhelmed the water and electrical systems, beginning July 12, 1993 when the Raccoon River topped its levee and forced the Des Moines Water Works offline at 1 a.m. ([Des Moines Public Library archive, projectdesmoines.dmpl.org](http://projectdesmoines.dmpl.org/items/show/63), accessed 2026-06-25) Approximately 35,000 customers had electricity restored by July 13 (secondary corroboration via Wikipedia and DMPL search snippets; not confirmed in directly fetched DMPL page text — cite with caveat). Callaway Nuclear Generating Station (1,236 MW, Fulton, MO / Ameren): "Callaway operated throughout the flooding of 1993 when the Missouri River at Jefferson City crested at 38.3 feet — almost 15 feet above flood stage." ([moenergyfuture.org, citing Ameren statements](http://moenergyfuture.org/news/ameren-missouri-river-no-threat-to-callaway-plant-safety/), accessed 2026-06-25) A coal fuel-delivery interruption claim for Callaway's coal-fired sister plants is indexed in Google snippets from a now-redirected Ameren corporate page but is not directly verifiable from a live primary source — treat as search-corroborated only. No authoritative electric-sector aggregate figure (MW offline, total customer-hours, or dollar-loss breakdown) is publicly available from DOE/NERC/FERC for this event. |
| **Mechanism illustrated** | §1 (mainstem slow-rise, prolonged duration — months); §2 (mainstem/major-river sub-type; levee overtopping → backwater flooding of urban utility infrastructure); §3 (distribution utility: substation / service infrastructure inundation → city-scale outage; coal crosswalk: inland barge/rail fuel delivery disruption when river flooding closes waterways; nuclear: large design margins allow continued operation even at ~15 ft above flood stage) |
| **Magnitude / impact** | >40,000 customers without power in Des Moines alone (DMPL archive); ~$15 billion total damages across nine states (NOAA NWS); Callaway (1,236 MW) operated without interruption when Missouri River was 15 ft above flood stage at Jefferson City. No verified aggregate MW-offline or electric-sector dollar figure for the region as a whole. |
| **Asset / actor relevance** | Distribution utilities (city-scale infrastructure vulnerability — levee failure can cascade from water utility to power utility); nuclear operators (Callaway illustrates that generous site elevation + design margins can sustain operation in extreme prolonged flood events); coal/gas plant fuel logistics (inland waterway and rail disruption when flood covers access) |
| **What it licenses** | Directional: major-basin floods can cause multi-day, city-scale distribution outages via substation inundation even where generation assets remain intact; directional: nuclear plants with adequate siting margins above flood-stage can operate through extreme multi-month flood events; directional: fuel delivery interruption for coal/gas assets is a credible mechanism during prolonged high-water events (note: coal-delivery claim is search-corroborated only) |
| **What it does NOT license** | Any specific asset's outage duration or restoration curve from this event; Midwest-wide electric-sector aggregate losses (no verified figure exists); the "substation inundation" mechanism for Des Moines is confirmed by secondary narrative sources (notesoniowa.com) but the primary DMPL archive does not use that specific word — do not over-attribute the mechanism to the primary source. Stationary return-period claims. |

---

### 4 · 2008 Iowa Flood — Cedar River / Cedar Rapids Utility Infrastructure

| Field | Notes |
|---|---|
| **Geography / market** | Cedar River basin, Cedar Rapids, Iowa; Alliant Energy and MidAmerican Energy service territories; MISO footprint |
| **What happened** | The Cedar River crested at 31.12 ft at Cedar Rapids at 10:15 a.m. on June 13, 2008 — more than 11 ft above the previous record of 20 ft (set in 1929/1951) — inundating more than 10 sq mi (14% of the city). ([Wikipedia, Iowa flood of 2008](https://en.wikipedia.org/wiki/2008_Iowa_flood); [USGS OFR 2010-1190](https://pubs.usgs.gov/publication/ofr20101190), accessed 2026-06-25) Of 30,000 Alliant Energy customers who lost power, approximately 2,000 were still without power weeks after the event. ([The Gazette](https://www.thegazette.com/news/politics/utilities-in-the-corridor-emerge-from-floods-with-stronger-systems/article_c61a1fb7-e51c-5baa-b7dc-3688033be953.html), accessed 2026-06-25) Alliant Energy faced damage to five of its Cedar Rapids facilities totaling $225 million; water reached 7 ft 6 in at its highest point inside the Alliant Energy Tower downtown. ([Buildings.com](https://www.buildings.com/articles/34349/flood-2008-alliant-energy), accessed 2026-06-25) The most expensive single recovery project was restoration of Prairie Creek Generating Station ($152 million); phased return began February 2009, ending that summer with capacity to serve 200,000 households. Restoring two downtown substations (RiverRun + Downtown Industrial) cost a combined $25 million. A Cedar Temporary substation was constructed within weeks to bridge lost capacity. MidAmerican Energy began terminating natural gas service to northwest Cedar Rapids neighborhoods on June 10; post-event recovery included replacing 15 miles of low-pressure gas mains and 900 services with an intermediate-pressure system. ([The Gazette](https://www.thegazette.com/news/politics/utilities-in-the-corridor-emerge-from-floods-with-stronger-systems/article_c61a1fb7-e51c-5baa-b7dc-3688033be953.html), accessed 2026-06-25) Note: claims about ITC Midwest transmission substation losses, >30 contractors, and specific substation locations trace to a now-404 Gazette URL — treat as dead-URL-sourced until re-verified. |
| **Mechanism illustrated** | §1 (major-river flash-to-mainstem transition, record-breaking single event); §2 (mainstem/major-river sub-type — record stage, 14% city inundation); §3 asset crosswalk: gas thermal generating station (Prairie Creek) — inundation of entire facility; distribution substations — two flooded beyond repair, one temporary bypass built; gas distribution — pre-emptive service termination and infrastructure replacement |
| **Magnitude / impact** | Cedar River crest: 31.12 ft (11+ ft above previous record); 30,000 Alliant customers lost power; ~2,000 still without power weeks later; Alliant total damage: $225M across five facilities; Prairie Creek restoration: $152M; RiverRun + Downtown Industrial substations: $25M combined; Prairie Creek restored capacity for ~200,000 households after phased recovery. MidAmerican: 15 miles of gas mains replaced, 900 services. All figures verified from live sources. |
| **Asset / actor relevance** | Distribution utilities (two verified substation total-loss events — RiverRun and Downtown Industrial; temporary bypass as resilience pattern); gas thermal plant operators (Prairie Creek illustrates that major generating station inundation triggers multi-month recovery at nine-figure cost); gas distribution operators (pre-emptive service termination and system-level infrastructure replacement) |
| **What it licenses** | Directional: record-stage events in a river corridor can produce total-loss substation and generating-station inundation requiring nine-figure recovery; directional: post-flood restoration involves temporary bypass infrastructure before permanent rebuild; directional: gas distribution systems may require system-level re-engineering (mains + services) after flood inundation, not just pipe repair |
| **What it does NOT license** | ITC Midwest transmission substation figures (dead-URL sourced — not usable as cited primary facts); exact outage durations; return-period claims; EAL/PML for any specific asset in a future event; plant-level generation attribution |

---

### 5 · 2010 Nashville / Tennessee Flood — NES Distribution & TVA Substation

| Field | Notes |
|---|---|
| **Geography / market** | Cumberland River basin, Greater Nashville, Tennessee; Nashville Electric Service (NES) territory; TVA system; SERC / Southern region |
| **What happened** | 13.57 inches of rain fell over 36 hours at Nashville International Airport (KBNA), breaking a 139-year record; a single-day total of 7.25 inches on May 2 set a calendar-day record. ([NWS Service Assessment, NOAA/NWS, January 2011](https://www.weather.gov/media/ohx/May2010_NashvilleFloodAssessment.pdf); [Metro Nashville OEM After Action Report, July 6, 2011](https://www.nashville.gov/sites/default/files/2025-10/AfterActionReport-Flood.pdf), accessed 2026-06-25) The Cumberland River at Nashville crested at 51.86 ft on Monday evening May 3 — approximately 4 ft above the previous flood-control-era peak of 47.64 ft (March 1975). (NWS Service Assessment, Metro OEM AAR, accessed 2026-06-25) NES peak outage: 43,677 customers without power at 1:58 p.m. Sunday May 2 (Metro OEM AAR p.109, verbatim). Over the full event period, almost 90,000 of NES's 355,000 customers experienced an outage; NES worked 3,717 outages total. NES West Substation: all 13.8 kV feeder breakers damaged beyond repair by inundation on May 2. NES McCrory Substation (Bellevue area): similarly flooded; feeder breakers replaced. ([Metro OEM AAR pp.110–111](https://www.nashville.gov/sites/default/files/2025-10/AfterActionReport-Flood.pdf); [NES 2011 Annual Report, President's letter p.1](https://www.nespower.com/-/media/Project/NES/Common/PDFs/Annual%20Reports/2011/AnnualReport2011), accessed 2026-06-25) At 3:00 a.m. May 4, Demonbreun Substation tripped offline, cutting power to approximately one-third of downtown Nashville; major affected buildings included the AT&T Building, Hilton, Schermerhorn Symphony Center, and others. By 8:00 p.m. May 7, all downtown customers who could receive power were restored. (Metro OEM AAR p.112; [Wikipedia, 2010 Tennessee floods](https://en.wikipedia.org/wiki/2010_Tennessee_floods), accessed 2026-06-25) TVA infrastructure: a TVA substation was submerged in over 5 ft of water when 15 inches of rain fell in 2 days; TVA subsequently relocated the substation to higher ground at a cost of approximately $9 million. ([GAO-23-105375, January 2023, Fast Facts and Highlights](https://www.gao.gov/products/gao-23-105375), accessed 2026-06-25) Total property damage in Greater Nashville exceeded $2 billion (NWS Service Assessment; Metro OEM AAR). Presidential Disaster Declaration FEMA-1909-DR. |
| **Mechanism illustrated** | §1 (rapid-onset flash-to-riverine transition; extreme short-duration rainfall driving river flooding); §2 (multi-mechanism: extreme precipitation + mainstem river rise, hours-to-days onset); §3 asset crosswalk: transmission/distribution — substation feeder-breaker inundation as binding outage mechanism (West + McCrory + Demonbreun); bulk-power (TVA) — substation relocation as adaptation response |
| **Magnitude / impact** | Peak NES outage: 43,677 customers (1:58 p.m. May 2, verbatim from OEM AAR). Total NES customers affected during event: ~90,000 of 355,000. Two NES substations (West + McCrory): all feeder breakers damaged beyond repair. Demonbreun Substation: ~one-third of downtown Nashville de-energized, restored by 8:00 p.m. May 7. TVA substation relocation cost: ~$9 million (GAO-23-105375, verbatim). Total Nashville-area damage: >$2 billion. |
| **Asset / actor relevance** | Distribution utilities (three documented substation flooding events in one storm — feeder-breaker inundation as a total-loss mechanism even in smaller substations); TVA and bulk-power operators (relocation to higher ground as post-event hardening — $9M verified cost anchor); city planners / resilience leads (multi-substation concurrent failure compounds outage footprint) |
| **What it licenses** | Directional: extreme short-duration rainfall can drive riverine flooding and concurrent multi-substation loss within a single utility service area; directional: feeder-breaker inundation is a verified, specific failure mode — not generic "flooding"; directional: substation relocation to higher ground is a documented and costed adaptation response (~$9M for TVA example); directional: restoration from multi-substation flood loss can be achieved within days for customers who can receive power, but weeks for those in the most affected areas |
| **What it does NOT license** | No specific MW-of-generation offline figure is confirmed (documented impacts are distribution/transmission only, not bulk generation); no exact outage-duration claim for any future event; no EAL/PML or insurance figure; the 52.55 ft crest figure from the NWS WFO OHX event webpage conflicts with the NWS Service Assessment's 51.86 ft figure — the Service Assessment is used here as primary authoritative; do not mix these figures |

---

## Cross-Event Patterns

```
PATTERN 1 — The substation is usually the binding failure point, not the generating unit
  Confirmed across: OPPD/Offutt 2019 (switchgear lost), Fort Calhoun 2011 (AquaDam breach → grid
  disconnect), Des Moines 1993 (city outage from electrical infrastructure inundation), Cedar Rapids 2008
  (RiverRun + Downtown Industrial substations total-loss, Prairie Creek Generating Station itself inundated),
  Nashville 2010 (West, McCrory, Demonbreun — three substations in one storm).
  Implication: riverine flood exposure analysis should prioritize substation/switchyard location and
  elevation, not just generating unit location. The same pattern holds for storm-surge coastal flood.

PATTERN 2 — NRC classification thresholds create an observable, documented record
  Cooper Nuclear 2019 (NOUE; threshold-aware operation; 9-day event, no offline);
  Fort Calhoun 2011 (NOUE → Alert → IMC 0350 oversight); Cooper Nuclear 2011 (NOUE, operated through).
  Implication: NRC NOUE and Alert declarations are in the public record and usable as event-window anchors.
  They signal that a plant was within threshold proximity — not that it was damaged. The distinction between
  the NRC NOUE threshold, the protective-offline threshold, and the formal Alert classification must be
  preserved; they are not synonymous.

PATTERN 3 — Extreme inflow can produce a hydro generation surplus, not only outage
  WAPA 6-dam Missouri mainstem system 2019: +38% above long-run average generation; $40M+ surplus
  hydropower sales (2018–2019 combined). This is the §3 hydro anomaly: extreme riverine flood events
  can be materially positive for hydro owners/offtakers even as they threaten thermal and distribution
  infrastructure in the same basin. Any riverine flood insight that includes hydro assets must explicitly
  label this bifurcated impact direction.
```

---

## Sources

| Source | Event(s) | URL |
|---|---|---|
| NPPD press release (Cooper Nuclear) | 2019 Missouri–Mississippi | https://www.nppd.com |
| Power Engineering — Cooper Nuclear | 2019 Missouri–Mississippi | https://www.power-eng.com/nuclear/cooper-nuclear-station-still-operational-despite-nebraska-flooding/ |
| power-technology.com — Cooper Nuclear | 2019 Missouri–Mississippi | https://www.power-technology.com |
| nebraska.tv — NOUE exit | 2019 Missouri–Mississippi | https://nebraska.tv |
| world-energy.org (AP wire) — WAPA hydro | 2019 Missouri–Mississippi | https://www.world-energy.org/article/5921.html |
| OPPD The Wire — Offutt AFB | 2019 Missouri–Mississippi | https://www.oppdthewire.com |
| World Nuclear News — AquaDam / grid disconnect | 2011 Missouri River | https://www.world-nuclear-news.org/Articles/Fort-Calhoun-defends-against-flood |
| UCS blog — 478 MW / 2+ yr offline / $180M | 2011 Missouri River | https://blog.ucs.org/mike-jacobs/wind-in-the-great-plains-and-the-flood-that-shut-fort-calhoun-nuclear-plant-353/ |
| EIA Today in Energy — Fort Calhoun / Cooper capacities | 2011 Missouri River | https://www.eia.gov/todayinenergy/detail.php?id=28572 |
| Wikipedia — 2011 Missouri River floods | 2011 Missouri River | https://en.wikipedia.org/wiki/2011_Missouri_River_floods |
| NOAA NWS Davenport — Great Flood of 1993 | 1993 Midwest Flood | https://www.weather.gov/dvn/071993_greatflood |
| Des Moines Public Library archive | 1993 Midwest Flood | http://projectdesmoines.dmpl.org/items/show/63 |
| moenergyfuture.org — Callaway 1993 operation | 1993 Midwest Flood | http://moenergyfuture.org/news/ameren-missouri-river-no-threat-to-callaway-plant-safety/ |
| USGS OFR 2010-1190 — 2008 Iowa flood hydrology | 2008 Iowa Flood | https://pubs.usgs.gov/publication/ofr20101190 |
| The Gazette — Alliant customer outage / Prairie Creek / substations | 2008 Iowa Flood | https://www.thegazette.com/news/politics/utilities-in-the-corridor-emerge-from-floods-with-stronger-systems/article_c61a1fb7-e51c-5baa-b7dc-3688033be953.html |
| Buildings.com — Alliant $225M / Alliant Tower water depth | 2008 Iowa Flood | https://www.buildings.com/articles/34349/flood-2008-alliant-energy |
| Metro Nashville OEM After Action Report (FEMA-1909-DR) | 2010 Nashville Flood | https://www.nashville.gov/sites/default/files/2025-10/AfterActionReport-Flood.pdf |
| NES 2011 Annual Report — substation feeder breakers | 2010 Nashville Flood | https://www.nespower.com/-/media/Project/NES/Common/PDFs/Annual%20Reports/2011/AnnualReport2011 |
| GAO-23-105375 — TVA substation relocation / $9M | 2010 Nashville Flood | https://www.gao.gov/products/gao-23-105375 |
| Wikipedia — 2010 Tennessee floods | 2010 Nashville Flood | https://en.wikipedia.org/wiki/2010_Tennessee_floods |

---

*See also*: `knowledge.md` (mechanism · sub-types · crosswalk · confidence robustness · non-stationarity) · `resource.yml` (blocked_claims · confidence_rules · allowed_questions) · `data_requirements.md` (USGS/AHPS/FEMA source stack) · `docs/method/confidence_model.md` (cap grades · axes)
