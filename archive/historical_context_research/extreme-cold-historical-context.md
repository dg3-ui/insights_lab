# Executive Summary

- **Recurring Failure Mode**: Across all four major cold events (2011, 2021, 2022, 2025), freezing of generating-unit components and natural gas fuel-supply failures accounted for roughly 75% of outages -> Winterization standards must address both equipment freeze protection and gas-electric interdependency as a single coupled system, not separate silos.
- **Gas-Electric Coupling Is the Dominant Risk**: Natural gas supply issues caused 27-31% of generation outages in Uri and 70% of forced outages in Elliott -> Any reliability claim that treats gas supply as exogenous is under-specified; modeling must incorporate wellhead freeze-offs, processing plant outages, and pipeline compression-power dependencies.
- **Design-Temperature Gap**: 81% of Uri freeze-related outages occurred above units' stated ambient design temperature -> The claim that facilities "met design criteria" does not license the conclusion that they were adequately winterized; design criteria themselves were inadequate.
- **Scale Escalation**: Unplanned outages grew from ~30 GW (2011) to 34 GW average/68 GW peak (Uri 2021) to 46 GW/Eastern Interconnection (Elliott 2022) to 71 GW (January 2025) -> Severity is not monotonically increasing (2025 had far less load shed despite higher outage MW), but exposure is growing with gas-dependent capacity additions.
- **Load-Shed Trajectory**: 23,418 MW firm load shed (Uri, largest in US history) vs. 5,400 MW (Elliott) vs. zero manual load shed (January 2025) -> Improved preparedness and operating practices can decouple outage MW from load-shed consequences, but the improvement is fragile and untested under simultaneous multi-region extremes.
- **Death Toll Uncertainty**: Uri official Texas death toll settled at 246 per Texas Department of State Health Services; Elliott caused no confirmed direct grid-related deaths; 2011 had no deaths reported -> Mortality claims for Uri must cite the 246 figure with its source qualifier; higher estimates (700+) are advocacy figures, not authoritative.
- **Economic Loss Range**: Uri economic loss estimates span $90B (Texas Comptroller) to $195-$300B (Federal Reserve Dallas/consulting reports) -> No single authoritative figure exists; any claim should cite the range and source, not a point estimate.
- **2011 Warnings Went Unheeded**: The 2011 FERC/NERC Southwest report issued recommendations nearly identical to those re-issued after Uri -> The 2011 event licenses the claim that regulatory inertia and voluntary compliance are insufficient; it does not license a causal claim that specific 2011 recommendations would have prevented Uri.
- **January 2025 as Positive Control**: FERC/NERC's April 2025 report documented 71 GW unplanned outages with zero manual load shed, citing improved operating practices and coordination -> This licenses a qualified claim that post-Uri/Elliott reforms can reduce consequences, but not a claim that the grid is "fixed"; 71 GW of outages is still a near-Uri-scale generation failure.
- **January 2024 Authoritative Gap**: The only identified authoritative source is the Western Power Pool's assessment covering RC West only; no FERC/NERC or EIA report specific to January 2024 was found -> January 2024 should not be used as a standalone case study in InfraSure methodology unless supplemented by ISO-specific data; coverage is thin relative to the other events.
- **Standards Trajectory**: FERC/NERC issued 28 recommendations after Uri and additional joint recommendations after Elliott; NERC approved revised cold-weather reliability standards (EOP-011-3, IRO-010-4) effective 2023-2024 -> These standards are necessary but not sufficient; compliance deadlines stretch to 2027, and fuel-security recommendations remain largely voluntary.

---

# 1 Winter Storm Uri February 2021 Ercot Texas And South Central Us

### Dates, Regions, and Markets Affected

Winter Storm Uri impacted the US power system from **February 8 through 20, 2021**, with the most severe conditions between **February 15 and 18**. Affected markets included **ERCOT** (Texas), **Southwest Power Pool (SPP)**, and **MISO South**. The event also affected parts of the **Western Interconnection** via gas supply disruptions. All 254 Texas counties were impacted.

### Generation Outages

ERCOT averaged **34,000 MW of generation outages** for over two consecutive days, nearly half of its **69,871 MW winter peak load**. Cold-weather-critical component outages totaled **68 GW in ERCOT, 27 GW in SPP, and 21 GW in MISO South**. Across all regions, **1,045 generating units** experienced **4,124 unplanned outages, derates, or failures to start**. Natural gas-fired generators accounted for **604 units (58%)** of total outages, followed by wind (27%), coal (6%), solar (2%), other (7%), and nuclear (<1%).

**Root causes** of outages: freezing issues (44.2%) and fuel issues (31.4%), totaling **75.6%** of all outage events. Of freezing-related outages, **81% occurred at temperatures above the units' stated ambient design temperature**, indicating systemic under-specification of design criteria rather than equipment operating beyond its rated envelope.

### Gas Supply and Wellhead Freeze-Offs

US Lower 48 natural gas production fell **28% between February 8 and 17**. **Texas natural gas production declined 70.1%** during the event. Gas supply declines were driven by: freezing issues at production facilities (25.3%), power outages at midstream/wellhead/gathering facilities (21.5%), and wellhead shut-ins (18.0%). Of fuel-related outages, **87% were natural gas supply issues** (mostly production and processing) and 13% involved other fuels. The EIA reported that in Texas, natural gas production declined **almost 45% during Uri**, with power outages at gas facilities contributing to production losses.

### Load Shed and Customers Affected

Total firm load shed was **23,418 MW**, the **largest controlled firm load-shed event in US history**. ERCOT peak load shed reached **20,000 MW** over nearly three consecutive days (orders escalated from 1,000 MW at 1:20 AM on Feb 15, to 10,000 MW at 4:30 AM, to 20,000 MW by 7:00 PM). SPP peak load shed was **2,718 MW** over approximately five hours. MISO South peak load shed was **700 MW** over more than two hours. More than **4.5 million people** in Texas lost power, some for up to four days. ERCOT's maximum import capability was only **1,220 MW** via DC ties with SPP and Mexico, severely limiting external assistance.

### Deaths

The **Texas Department of State Health Services** finalized the death toll at **246**. The Utility Dive coverage of the FERC/NERC January 2025 report also cited "an estimated 246 deaths" for Uri. Higher figures (e.g., 700+) appear in advocacy and media sources but are not from authoritative government statistical agencies.

### Economic Loss

Estimates vary widely: the **Texas Comptroller** cited at least **$90 billion**; a **Federal Reserve Bank of Dallas** report estimated economic losses of **$80-$130 billion**; a consulting report cited by KERA News estimated up to **$300 billion**. AccuWeather initially estimated over **$100 billion**. No single authoritative figure exists.

### Reliability Recommendations and Winterization Changes

The FERC/NERC final report (November 2021) issued **28 formal recommendations**. Key recommendations include:

- Requiring Generator Owners to identify and implement freeze protection for cold-weather-critical components (protecting four specific component categories could have reduced outages by **67% in ERCOT, 55% in MISO, and 47% in SPP**)
- Accounting for wind and precipitation effects in temperature data used for winterization planning
- Requiring Balancing Authorities to calculate the percentage of capacity they believe can be relied upon during forecasted cold weather
- Requiring natural gas infrastructure to prepare for cold weather (including wellhead freeze protection, gas processing facility winterization, and backup power for compression)
- Improving gas-electric coordination and communication protocols

**Regulatory changes**: Texas SB 3 (June 2021) mandated weatherization for Texas power generators and certain gas facilities; PUCT adopted implementing rules. NERC revised cold-weather reliability standards (EOP-011-3, IRO-010-4) with phased compliance deadlines extending to 2027.

### What Uri Does and Does Not License as a Claim

**Licenses**: (1) The claim that inadequate winterization of both generating units and gas infrastructure was the primary cause of the blackout; (2) the claim that 81% of freeze-related outages occurred above design temperature, indicating design criteria gaps; (3) the claim that gas-electric coupling was the dominant systemic risk; (4) the claim that ERCOT's island status (limited DC ties) worsened the outcome; (5) the claim that protecting specific components could have prevented roughly 60-67% of ERCOT outages.

**Does NOT license**: (1) The claim that any specific fuel type "caused" the blackout in isolation (multiple fuel types and non-fuel factors contributed); (2) the claim that renewable energy was the primary cause (wind accounted for 27% of outages by unit count, but less by MW); (3) a precise economic loss figure (range is $90-$300B depending on source); (4) the claim that post-Uri reforms have "fixed" the problem (January 2025 showed 71 GW of unplanned outages, albeit without load shed); (5) capacity-availability estimates as "strict liability" figures - the report views them as "good faith, reasonable estimates."

| Metric | ERCOT | SPP | MISO South | Total |
|---|---|---|---|---|
| Peak gen outages (GW) | 68 | 27 | 21 | ~116 |
| Avg outages over 2+ days | 34 GW | - | - | - |
| Peak load shed (MW) | 20,000 | 2,718 | 700 | 23,418 |
| Generating units affected | ~604 (gas) + others | - | - | 1,045 units |
| Gas production decline | 70.1% (TX) | - | - | 28% (Lower 48) |
| People affected | 4.5M+ | - | - | - |
| Deaths (TX DSHS) | 246 | - | - | 246 |

Takeaway: Uri exposed a coupled gas-electric failure mode at unprecedented scale. The 23,418 MW load shed and 246 deaths are the largest cold-weather reliability failure in US history. The event's most important analytical lesson is that design-temperature gaps and gas-supply dependencies are shared across all thermal fuel types, not isolated to any single technology.

---

# 2 Winter Storm Elliott December 2022 Pjm Eastern Interconnection

### Dates, Regions, and Markets Affected

Winter Storm Elliott occurred **December 21-26, 2022**, with the most severe impacts on **December 23-25**. Affected regions spanned the **Eastern Interconnection**, primarily **PJM Interconnection** (13 states and DC, serving 65 million customers), along with portions of **MISO, NYISO, ISO-NE, and southern utilities** (Duke, TVA, Southern Company). The event is distinct from Uri in affecting primarily the Eastern Interconnection rather than ERCOT.

### Generation Outages

The FERC/NERC final report (November 2023) found that a **record 13% of Eastern Interconnection generating capacity** failed during Elliott. Approximately **46 GW of generation was unexpectedly offline** at the peak. PJM experienced approximately **40 GW of coal and natural gas forced outages**. Gas generators were responsible for **70% of forced outages** in PJM during the event. In total across the Eastern Interconnection, approximately **91 GW** of generation was unexpectedly offline at some point during the event (per the Utility Dive summary of the FERC/NERC report). **55% of generating unit outages, derates, and failures to start were primarily caused by freezing and fuel issues**.

PJM's load forecasts for December 23 and 24 were approximately **8% under the actual peak**, contributing to operational shortfalls.

### Gas Supply and Fuel Issues

Natural gas fuel-supply failures were the dominant reliability concern. The FERC/NERC report documented widespread gas production and delivery disruptions across the Appalachian Basin and Gulf Coast supply regions feeding the Eastern Interconnection. PJM's report highlighted that gas generators could not procure fuel due to: pipeline pressure drops, gas production freeze-offs, and contractual priority issues (firm vs. interruptible service). The NRDC/Sustainable FERC analysis noted that gas generators' **70% share of forced outages** was primarily driven by fuel unavailability rather than mechanical failures.

### Load Shed and Customers Affected

Rolling blackouts totaled **5,400 MW** across the Eastern Interconnection. PJM operators avoided electricity interruptions for their own footprint, but **neighboring utilities** (Duke Energy Carolinas, Duke Energy Progress, TVA, and Louisville Gas & Electric/KU) implemented rolling blackouts affecting approximately **500,000+ customers**. TVA experienced its first-ever mandatory load shed. Duke Energy implemented rolling outages affecting ~300,000 customers in the Carolinas. PJM itself narrowly avoided load shedding through emergency operations, including deploying **7,650 MW of exports** to assist neighbors during the January 2025 event (demonstrating improved post-Elliott coordination).

### Deaths

No confirmed direct grid-related deaths were reported from Elliott. Some hypothermia and carbon monoxide poisoning cases were reported in broader media, but these were not attributed to the grid event by FERC/NERC in their formal report.

### Economic Loss

No authoritative aggregate economic loss figure was identified from FERC/NERC or EIA sources. Estimated insured losses from Winter Storm Elliott overall (including non-grid damage) were reported in insurance industry sources, but grid-specific loss figures are not available from authoritative sources.

### Reliability Recommendations and Winterization Changes

The FERC/NERC final report on Elliott (November 2023) issued **joint recommendations** that built on and extended the Uri recommendations:

- Completion of needed cold-weather reliability standard revisions initially identified after Uri
- Improved gas-electric coordination, including better communication between gas pipeline operators and electric grid operators during emergencies
- Requiring generators to have firm fuel supply arrangements or equivalent backup plans for winter operations
- PJM's internal report issued **30 recommendations** focusing on: winter risk assessment, generator performance incentives, gas-electric coordination, Performance Assessment Interval (PAI) system evaluations, and emergency procedure education
- FERC/NERC emphasized the need for Congress to address the lack of mandatory winterization standards for natural gas infrastructure (which remains largely outside FERC's jurisdiction)

**Regulatory changes**: NERC's revised EOP-011-3 standard (effective 2023-2024) requires generators to implement cold-weather preparedness plans. PJM enhanced its winter readiness protocols and capacity performance incentives.

### What Elliott Does and Does Not License as a Claim

**Licenses**: (1) The claim that gas-electric coupling failures are not a Texas-only phenomenon but a systemic Eastern Interconnection risk; (2) the claim that 13% of Eastern Interconnection capacity can fail simultaneously in extreme cold; (3) the claim that gas generators are disproportionately vulnerable (70% of forced outages); (4) the claim that load forecast underestimation (8% error) contributes to inadequate preparation; (5) the claim that neighboring utilities bore the load-shed burden even when PJM itself avoided it.

**Does NOT license**: (1) The claim that PJM's market design "caused" the outages (generators failed across multiple RTOs); (2) a precise economic loss figure; (3) the claim that post-Elliott reforms have resolved gas-electric coupling (January 2025 still showed 71 GW outages, though with no load shed); (4) the claim that capacity markets alone can solve fuel-security problems (firm fuel arrangements remain voluntary in most RTOs).

| Metric | Elliott (Dec 2022) | Comparison: Uri (Feb 2021) |
|---|---|---|
| Primary region | Eastern Interconnection (PJM+) | ERCOT/SPP/MISO South |
| Peak gen outages | ~46 GW (PJM), ~91 GW (EI-wide) | ~34 GW avg, 68 GW peak (ERCOT) |
| EI capacity failed | 13% record | N/A (ERCOT isolated) |
| Gas gen share of outages | 70% | 58% of units |
| Peak load shed | 5,400 MW (EI-wide) | 23,418 MW |
| Customers affected | ~500,000+ | 4.5 million+ |
| Deaths (grid-related) | 0 confirmed | 246 (TX DSHS) |
| FERC/NERC recs | Joint recs + PJM 30 recs | 28 formal recs |

Takeaway: Elliott demonstrated that gas-electric coupling failures are a continental-scale risk, not a Texas anomaly. The 70% gas-generator outage share is the strongest single data point for InfraSure methodology: any model that does not incorporate gas-supply vulnerability will systematically understate winter reliability risk.

---

# 3 February 2011 Southwest Cold Weather Event

### Dates, Regions, and Markets Affected

The event occurred **February 1-5, 2011**, affecting the **Southwest United States**, primarily **ERCOT** (Texas), **SPP** (particularly New Mexico, Arizona, and parts of Colorado and Kansas), and the **Western Interconnection** (Arizona, New Mexico, southern California). Affected RTOs/utilities included ERCOT, SPP, Arizona Public Service (APS), Tucson Electric Power (TEP), El Paso Electric (EPE), and Public Service Company of New Mexico (PNM).

### Generation Outages

The FERC/NERC staff report (August 2011) documented that approximately **29,729 MW of generation** experienced outages, derates, or failures to start across the affected regions during the event. Natural gas-fired generation accounted for the largest share of outages. A total of **210 generating units** experienced **724 outages, derates, or failures to start**. In ERCOT specifically, approximately **9,613 MW** of generation was lost at the peak. The majority of outages were caused by **freezing of equipment** (instrument lines, sensing lines, water lines, valves, and other cold-weather-critical components) and **natural gas fuel supply curtailments**.

### Gas Supply and Wellhead Freeze-Offs

Natural gas production in the Permian Basin and other Southwest production areas declined significantly due to wellhead freeze-offs and processing facility outages. The FERC/NERC report documented that gas curtailments to electric generators occurred due to: priority of residential heating over power generation under interruptible service contracts, physical declines in gas production due to freeze-offs, and loss of electric power at gas production and processing facilities (creating circular gas-electric dependency). Specific quantitative gas production decline figures were reported in the full FERC/NERC report but are less widely cited than Uri figures.

### Load Shed and Customers Affected

ERCOT implemented **firm load shedding** during the event. SPP also declared Energy Emergency Alerts. Arizona utilities (APS, TEP) implemented rolling outages affecting approximately **50,000-100,000 customers** in the Phoenix and Tucson areas. El Paso Electric implemented rolling blackouts affecting approximately **30,000-40,000 customers**.

### Deaths

No deaths were reported as directly attributable to the power outages during the 2011 event.

### Economic Loss

No authoritative aggregate economic loss figure was identified. The event was less economically destructive than Uri due to shorter duration and smaller geographic scope of load shedding.

### Reliability Recommendations and Winterization Changes

The FERC/NERC 2011 report issued recommendations that were **nearly identical** to those re-issued after Uri a decade later:

- Generators should identify and protect cold-weather-critical components from freezing
- Generators should account for wind chill and precipitation in winterization design
- Natural gas production and processing facilities should winterize equipment and ensure backup power
- Balancing Authorities should require generators to provide accurate cold-weather capability data
- Gas-electric coordination should be improved, including communication protocols during emergencies
- States should consider requiring winterization of gas infrastructure

**Regulatory outcome**: Most recommendations were **not implemented** as mandatory standards. NERC did not adopt binding cold-weather preparedness standards after 2011, relying instead on voluntary guidelines. This regulatory gap was a central finding of the post-Uri FERC/NERC report, which explicitly noted that the same failures recurred because 2011 recommendations were not enforced.

### What the 2011 Event Does and Does Not License as a Claim

**Licenses**: (1) The claim that cold-weather reliability failures in the Southwest are recurring and predictable; (2) the claim that voluntary winterization guidelines are insufficient (the central lesson of the 2011-to-2021 trajectory); (3) the claim that gas-electric coupling was identified as a systemic risk as early as 2011; (4) the claim that equipment freezing and gas fuel-supply curtailment are the two dominant failure modes (confirmed in 2011, 2014, 2021, and 2022).

**Does NOT license**: (1) The causal claim that implementing all 2011 recommendations would have prevented Uri (the counterfactual is untestable, though the FERC/NERC Uri report strongly implies it); (2) the claim that the 2011 event was a "preview" of Uri in terms of scale (2011 was an order of magnitude smaller in load shed and duration); (3) any claim about nuclear or renewable energy vulnerability (the 2011 event primarily affected gas and some coal units).

---

# 4 January 2024 Gulf Eastern Us Cold Snap

### Authoritative Source Assessment

The only identified authoritative source is the **Western Power Pool (WPP) Assessment of January 2024 Cold Weather Event**, which covers the RC West reliability coordinator area only. **No FERC/NERC report, EIA Today in Energy article, or ISO-specific report** focused on the January 2024 cold event was identified. The FERC/NERC January 2025 performance report covers January 2025 storms, not January 2024.

### Limited Available Data

The WPP assessment (dated January 12, 2024) provides a high-level overview of actions taken by RC West during the January 2024 cold weather event. Specific quantitative data on generation outages, gas supply impacts, or load shed for the broader Gulf/Eastern US was not extracted from this source. The January 2024 event primarily affected the **Gulf Coast, Texas, and portions of the Eastern US**, with temperatures dropping below freezing across much of the South.

### What January 2024 Does and Does Not License as a Claim

**Licenses**: Very limited claims. The WPP assessment may support region-specific claims about RC West operations. No authoritative cross-ISO or national-level data is available.

**Does NOT license**: (1) Any claim about national or multi-region reliability performance; (2) comparison with Uri or Elliott; (3) claims about winterization progress or regression. **Recommendation for InfraSure methodology**: January 2024 should be treated as a secondary/partial reference only, with explicit notation that authoritative FERC/NERC data is not available.

---

# 5 January 2025 Arctic Blast Gulf Eastern Us

### Dates, Regions, and Markets Affected

The January 2025 arctic event (Storms **Blair, Cora, Demi, and Enzo**) occurred primarily **January 5-24, 2025**, with peak conditions around **January 21-22**. Affected regions included **PJM Interconnection, ERCOT, MISO, SPP, NYISO, ISO-NE**, and utilities across the **Gulf Coast and Eastern US**. The FERC/NERC report on January grid performance was released **April 17, 2025**.

### Generation Outages

Unplanned generation outages peaked at **71,022 MW** on January 21-22, according to the FERC/NERC report. This is the **second-highest documented unplanned outage total** after Elliott's ~91 GW Eastern Interconnection total, but the outage-to-load-shed conversion was dramatically lower. Mechanical and electrical generator outages (not freeze/fuel-related) accounted for approximately **54% of generator outages with a reported cause**, suggesting that freeze-protection improvements may have shifted the failure-mode distribution.

### Gas Supply

Natural gas demand peaked at **150 Bcf/day** during January 21-22, a near-record. Electric demand peaked at **683 GW**. No major gas production collapse comparable to Uri's 70% Texas decline was reported, though localized freeze-offs occurred.

### Load Shed and Customers Affected

**No manual load shedding was required** during the January 2025 event. This is the most significant finding: despite 71 GW of unplanned outages (comparable to or exceeding Uri and Elliott), the grid did not require rolling blackouts. PJM exported **7,650 MW** during peak demand periods to assist neighbors. ERCOT reported that **battery storage provided 3,800 MW** at peak times.

### Deaths

No grid-related deaths were reported. The event caused weather-related disruptions and some outages due to distribution-system damage (ice storms), but no bulk-power-system load shed.

### Economic Loss

No authoritative aggregate economic loss figure from grid impacts was identified.

### Reliability Performance and Winterization Progress

The FERC/NERC April 2025 report highlighted **improved outcomes** compared to Uri and Elliott:

- Enhanced operating practices and communication protocols between gas and electric entities
- Better coordination between RTOs and neighboring utilities
- Implementation of some Uri and Elliott recommendations (though not all)
- PJM's improved winter readiness protocols and capacity performance incentives
- ERCOT's post-SB 3 winterization requirements showing results

However, the report also noted that **71 GW of unplanned outages is still a near-Uri-scale generation failure**, and the system has not yet been tested under simultaneous multi-region extreme conditions with coincident gas infrastructure failures.

### What January 2025 Does and Does Not License as a Claim

**Licenses**: (1) The qualified claim that post-Uri/Elliott reforms have reduced the consequence severity of comparable generation outage levels (zero load shed vs. 23,418 MW in Uri); (2) the claim that battery storage and inter-RTO coordination can provide meaningful winter reliability value; (3) the claim that 71 GW of unplanned outages can occur without triggering load shed, under improved preparedness conditions.

**Does NOT license**: (1) The claim that the grid is "winterized" or "fixed" (71 GW of unplanned outages is still a massive failure); (2) the claim that January 2025 conditions were as severe as Uri or Elliott (temperatures and duration were less extreme); (3) any claim about gas infrastructure resilience (no major gas production collapse occurred, so the gas-electric coupling was not stress-tested to the same degree); (4) extrapolation to future events with different weather patterns or coincident multi-region failures.

---

# Synthesis Cross Event Comparative Analysis

### Failure-Mode Persistence Across Events

The four major cold events (2011, 2021, 2022, 2025) reveal a **persistent failure-mode structure**: equipment freezing and gas fuel-supply issues consistently account for roughly 55-75% of generation outages. The relative proportions shift (gas was 58% of Uri units, 70% of Elliott forced outages; mechanical/electrical issues rose to 54% in January 2025), but the overall pattern is stable. This persistence licenses the InfraSure methodology claim that cold-weather reliability risk is **structurally** driven by gas-electric coupling and freeze-vulnerable equipment, not by idiosyncratic weather conditions.

### Scale vs. Consequence Decoupling

The most important cross-event insight is that **generation outage MW does not deterministically predict load-shed MW**:

| Event | Peak Unplanned Outages | Peak Load Shed | Conversion Rate |
|---|---|---|---|
| Uri (Feb 2021) | ~34 GW avg (68 GW peak) | 23,418 MW | ~34-69% |
| Elliott (Dec 2022) | ~46 GW (PJM), ~91 GW (EI) | 5,400 MW | ~6-12% (EI-wide) |
| Jan 2025 | 71 GW | 0 MW | 0% |

This decoupling is not random: it reflects the role of **operational preparedness, inter-RTO coordination, reserve margins, and demand-response** in absorbing outage shocks. InfraSure methodology should model outage-to-load-shed conversion as a function of system state, not as a fixed ratio.

### Regulatory Trajectory: Voluntary to Mandatory, with Gaps

The 2011-to-2025 arc shows a clear regulatory trajectory: voluntary guidelines (2011) -> identification of voluntary-compliance failure (2021) -> mandatory standards with phased compliance (2023-2027) -> partial evidence of effectiveness (2025). However, **critical gaps remain**: (1) FERC lacks jurisdiction over natural gas infrastructure winterization; (2) NERC standards focus on generators but not on gas producers/processors; (3) compliance deadlines extend to 2027, meaning the grid is operating under partial implementation; (4) fuel-security arrangements remain largely voluntary in most RTOs.

### Gas-Electric Coupling: The Unresolved Systemic Risk

Every FERC/NERC report from 2011 onward identifies gas-electric coupling as the central reliability vulnerability. Yet regulatory authority over gas infrastructure remains fragmented (FERC has limited jurisdiction over intrastate gas production and gathering). The January 2025 event did not test this vulnerability at Uri-scale intensity (no major gas production collapse). **InfraSure methodology should treat gas-electric coupling as the dominant but incompletely observed risk**: the 2011, 2021, and 2022 events all demonstrated it; the 2025 event did not contradict it but also did not test it at full severity.

### What the Full Event Sequence Licenses for InfraSure

The complete sequence licenses the following **composite claims** for InfraSure methodology:

1. Cold-weather generation outages of 30-70+ GW are historically normal, not outliers, for extreme events affecting major US power regions.
2. Gas fuel-supply failures are the single largest driver of winter reliability risk across all US interconnections.
3. Design-temperature specifications at generating units were systematically inadequate pre-Uri; post-Uri standards are improving but not yet fully implemented.
4. The outage-to-load-shed conversion rate is highly variable and depends on operational preparedness, reserve margins, and inter-regional coordination.
5. Voluntary winterization standards failed; mandatory standards with compliance deadlines are necessary but still being phased in.
6. No cold event in the historical record has tested gas-electric coupling at Uri-scale intensity under fully implemented post-Uri/Elliott mandatory standards.

---
