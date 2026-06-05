# Research 01 — Existing Analytical Platforms

> Status: research complete. For reference only — bar is "we can do much better."

## TL;DR (3-4 sentences)

The dominant analytical-platform pattern is "PDF report behind seat-based paywall, loosely linked to a separate proprietary database (Cube/Lens/Terminal)" — content is rich but the atomic unit is human-sized (5-50 page PDFs), poorly addressable, and decays the moment costs/policies/projects shift. The most interesting models split methodology from applied analysis (NREL ATB, AEO Cases, BNEF Tier 1 methodology docs) so a worldview can be cited and reused, but even they treat the *applied* layer as one-off narrative prose rather than as structured, entity-grounded objects. The successful adjacent voices (Levine, Thompson) work because reusable *frameworks* — aggregation theory, capital structure incentives — let them re-apply one analytical lens to a daily stream of new entities; the structural opportunity is to make that re-application a system, not a writer. Across all of them, the failure mode is the same: analytical content lives in unstructured PDFs disconnected from the entities it's about, so it doesn't survive author turnover, doesn't update when underlying data updates, and isn't reachable by an LLM at query time.

## Platforms Investigated

One line per platform: what it is, who pays, what the atomic content unit is.

| Platform | What it is | Who pays | Atomic content unit |
|---|---|---|---|
| **S&P Global Commodity Insights (Platts)** | Price assessments + news + special reports + advisory (CERA) | Traders/utilities/banks; bespoke contracts, undisclosed prices | Daily price assessment (data) + Subscriber Note (governance/methodology event) + Special Report (PDF narrative) |
| **Wood Mackenzie (Lens P&R)** | Asset-by-asset DB + market briefs + multi-client studies | Utilities, developers, financiers, IB analysts; six-figure seat licenses | Asset record (DB row) loosely paired with written commentary in same platform; separate PDF reports in a "store" |
| **BloombergNEF** | Sector intelligence + flagship reports (NEO, Tier 1) + ~200K-project DB on the Terminal | Bloomberg Terminal subscribers (~$28K/seat/yr) and BNEF web sub | "Insight" (research note, mixed-length) + "Tier 1 Report" (annual methodology+ranking) + dataset rows |
| **Rystad Energy** | Domain-specific "Cubes" (UCube, GasMarketCube, WellCube, EmissionsCube…) + analyst commentary | Energy companies, IBs, governments | Cube row (field-by-field economics) + accompanying commentary; weekly Navigator email |
| **Aurora Energy Research** | Market-modeled forecasts + SCED dispatch + advisory (EOS, Origin, Amun) | Developers, financiers; subscription analytics + bespoke | Forecast scenario + bankable valuation outputs + bespoke client deliverables |
| **ICF** | Consulting + modeling + policy advisory | Government, regulators, utilities (project-based) | Project deliverable (bespoke PDF/model) — not a productized library |
| **NREL Cambium / ATB / Standard Scenarios** | Free, published cost/operational data with scenarios, region×year×tech tagged | Free (taxpayer-funded) | Scenario × region × technology × year cell, in published workbooks; methodology in separate PDF |
| **EIA Annual Energy Outlook (AEO)** | Annual flagship: Reference Case + Side Cases + Issues in Focus | Free | A "Case" (a NEMS run with one varied assumption) + Issues in Focus essay; Narrative PDF + tables |
| **Stratechery (Ben Thompson)** | Solo paid newsletter, business strategy + tech | ~$15/month or $150/year, single tier | Daily Update (member-only) or Article (free) — but the underlying unit is a *Concept* (Aggregation Theory, Smiling Curve) re-applied across articles |
| **Money Stuff (Matt Levine, Bloomberg)** | Free daily newsletter, capital-markets analysis | Free (loss-leader for Bloomberg Opinion) | The "five headlines per day, one analytical lens" rhythm; each item ~300-1000 words |
| **Tegus (AlphaSense)** | Expert call transcript library + AI search | $25K-$150K+/year, seat-based | Transcript (Company Deep-Dive / Industry Overview / Topic Deep-Dive / Voice of Customer), tagged by company+topic |
| **RAND** | Public-interest research reports | Funder-paid; published free or restricted | Multi-chapter report with explicit, separable "Methods and Methodology" companion |
| **NBER Working Papers** | Pre-publication economics research | Free abstracts; paywalled fulltext (~$5) | The working paper as one numbered, JEL-classified, MARC-indexed unit |
| **LBNL Electricity Markets & Policy (EMP)** | Free government-funded research reports | Free | Topical report series (Retail Price Trends, Wholesale Price Drivers, etc.) — recurring updates of same backbone analysis |
| **gridstatus.io** *(added 2026-05-31)* | Real-time ISO/RTO data infrastructure (CAISO, ERCOT, PJM, MISO, NYISO, SPP, ISONE, IESO, AESO, EIA) + content surface | Freemium: `gridstatus` Python library OSS on GitHub; gridstatus.io app paid; blog free | Two surfaces. (1) `gridstatus.io/insights` in-app feed = short event-triggered market notes (~paragraph): "NYISO 2026 Gold Book Forecast", "SPP HVDC tie line crossing April 1 2026", RTC+B day-1 updates. (2) `blog.gridstatus.io` = long-form comparative analysis (1,500-2,500 words, static charts, bylined Connor Waldoch + Grid Status team): "Net Load Ramps: Texas vs California", "CAISO Beats the Heat". Methodology embedded in narrative ("we're using 5 minute intervals to determine periods of continuous ramping"); no separable methodology layer. No claim-level grounding to specific data rows. Static charts only — data accessible via separate API but not linked from the post itself. |

## 5-7 Distilled Learnings

### Learning 1: The atomic content unit is almost always a human-sized PDF
**Where seen:** S&P Global Special Reports, Wood Mackenzie "store" reports, BNEF Tier 1, ICF deliverables, RAND reports, NBER working papers, LBNL EMP series.
**Description:** The dominant industry pattern treats a "report" — a 5-50 page document authored once, dated once, downloaded once — as the unit of value. Tagging is post-hoc (sector, region as metadata on a PDF). The DB and the narrative are different products that link weakly.
**For us:** EXPLICITLY AVOID.
**Why:** A PDF report can't be re-grounded when the underlying data changes, can't be subset to one plant, can't be reached by an LLM at query time, and dies the moment its author leaves. Our atomic unit should be the *analytical statement* (scoped to entity + time window + dimension), with the report being one of many possible compositions over those statements.

### Learning 2: Methodology and applied analysis as separate, citable layers
**Where seen:** NREL ATB (cost/performance methodology doc is separate from data workbooks); EIA AEO (Reference Case + Side Cases + Issues in Focus essays sit on a shared NEMS methodology); BNEF Tier 1 Energy Storage Methodology March 2026 is a separately versioned document; RAND breaks "Methods and Methodology Report" out as its own chaptered deliverable.
**Description:** The strongest platforms publish methodology as a versioned, citable artifact and let applied work *reference* it — so the analyst doesn't re-derive their worldview every time, and a reader can audit assumptions independently of the conclusion.
**For us:** DO A STRONGER VERSION OF.
**Why:** This is exactly the methodology-brief vs applied-insight split the lab is already organized around — these platforms validate the shape but their *applied* layer is still unstructured prose. Our version: applied insights are structured objects that explicitly declare which methodology brief they instantiate, which entities they scope, which fields/dimensions they consume. Then we get composability they don't have.

### Learning 3: Reusable analytical frameworks let one voice scale across thousands of entities
**Where seen:** Stratechery's "Concepts" page is the spine — Aggregation Theory, Smiling Curve, Disruption — and every daily piece applies one lens to a new entity. Money Stuff has 4-5 recurring lenses (incentives, capital-structure consequences, "everything is securities fraud," market-microstructure absurdity) applied to whatever's in the news that day.
**Description:** High-output, high-quality analytical writing isn't a per-piece authoring problem — it's a *framework × entity stream* multiplication problem. The framework is the leverage; the daily piece is the application.
**For us:** DO A STRONGER VERSION OF.
**Why:** This is the philosophical core of "methodology before applied" — but where Levine and Thompson re-apply manually, we re-apply systematically. Methodology briefs are the leverage; applied insights are the production line. A worldview about "thermal repower NPV when gas basis decouples from Henry Hub" should produce one applied insight per plant in the eligible set, not one essay.

### Learning 4: Entity tagging exists in DBs, almost never in narrative
**Where seen:** Bloomberg RMS tags research to security tickers + auto-derives sector/country tags; BNEF claims ~200K-project DB; Wood Mac Lens has asset-level records; Rystad Cubes are field-by-field; Tegus tags transcripts to companies.
**Description:** Every major platform has structured entity registries — but the *narrative content* is only loosely linked to them. "Tagged to ticker" usually means "filed under" not "every analytical claim grounds to a specific entity + field + time window." The DB and the narrative are different products with weak interop.
**For us:** DO A STRONGER VERSION OF.
**Why:** We already have the entity substrate (15,528 plants, 29,738 generators, ~9,783 queue projects, news with extracted atomic facts grounded to entities). The structural opportunity is that every applied insight grounds to (plant_id / project_id / region / fuel-segment / time-window) at the *claim* level, not just as a top-level tag. That makes insights queryable, composable, and stale-detectable.

### Learning 5: Time-stamping and "what stays evergreen" is mostly a vibes call
**Where seen:** S&P Subscriber Notes versus market commentary versus methodology change — three different time-decay regimes with the same look-and-feel. Wood Mac and BNEF mix scenarios (multi-year evergreen-ish) with weekly briefs (decay in days). AEO is "annual snapshot" but Issues in Focus essays may stay relevant for 3-5 years. Stratechery Concepts pages live forever; Daily Updates decay fast.
**Description:** Almost no platform explicitly declares a content item's expected half-life or invalidation conditions. Readers (and LLM crawlers) can't tell stale from fresh without manually inspecting dates.
**For us:** ADOPT (with our own structure).
**Why:** Methodology briefs should declare their invalidation conditions ("revisit if X policy passes, Y cost falls below Z, or Q quarters elapse"). Applied insights should declare their underlying-data vintage and auto-deprecate when the underlying data refreshes. Both should expose this in machine-readable form. This is downstream of having a structured atomic unit (Learning 1).

### Learning 6: Pricing model reveals (and often constrains) the audience
**Where seen:** Tegus' $25K-$150K seat-based pricing aligns content to "person whose job is to read this" — limiting volume and discouraging entity-level granularity. BNEF and Wood Mac similar. Stratechery's $15/mo expands audience but caps depth. Free public data (NREL, EIA, LBNL) maximizes reach, sacrifices commercial sustainability, and accepts a slower cadence.
**Description:** Seat-based pricing forces the content to be dense, expensive-feeling, and infrequent (so a seat feels valuable). Per-piece or freemium expands audience but caps research depth. There isn't a clean middle path in the current market.
**For us:** EXPLICITLY AVOID copying any single existing pricing model. Decide pricing from audience and unit-economics, not from genre expectations.
**Why:** Because our atomic unit is structured (not a 30-page PDF), our cost-to-produce per unit is fundamentally different from a Wood Mac/BNEF report. We don't need to charge $30K to a single seat to amortize a research analyst's quarter. The pricing-shape decision should follow from "what's the unit, who consumes it, how does it embed into their workflow," not from "what do energy research firms charge."

### Learning 7: AlphaSense/Tegus is the closest "structured analytical primitive" pattern, and it's still essentially a search index
**Where seen:** Tegus transcript types (Company Deep-Dive / Industry Overview / Topic Deep-Dive / Voice of Customer) are typed structured atoms; AlphaSense layers AI search on top.
**Description:** This is the only major platform whose atomic unit is small, structured-by-type, entity-tagged at production time, and indexed for retrieval. It's the proof of concept that "library of small typed analytical units, AI-searchable" is a viable commercial pattern.
**For us:** Reference the *shape*, not the genre.
**Why:** Tegus' content is expert-call testimony — first-party primary material. Ours is synthesized analytical statements grounded in structured data — second-party derived material. The structural innovation is the same (typed, tagged, queryable units); the substance is fundamentally different and complementary.

### Learning 8: gridstatus.io as the closest "structured substrate + prose content" comparable — and the most instructive gap *(added 2026-05-31)*

**Where seen:** gridstatus.io (the only platform among the 15 investigated that pairs a genuinely well-typed substrate, exposed via OSS Python library, with a content surface aimed at the energy-infrastructure audience).

**Description:** gridstatus has solved the substrate half of our equation as well as anyone in the market. Their two content surfaces — short event-triggered "Insights" in-app feed (e.g., "SPP HVDC tie line crossing April 1 2026") and long-form comparative blog posts (e.g., "Net Load Ramps: Texas vs California", ~2,200 words, bylined, static charts) — are produced manually by a small editorial team. Methodology is embedded in narrative prose; no separable methodology layer; no claim-level grounding to specific data rows; no machine-readable staleness; no two-clocks pattern. Posts are frozen at publication.

The most informative observation: their content is implicitly **marketing-first** — every post demonstrates that gridstatus has interesting data, but the editorial filter doesn't seem to be "what decision does this enable a reader to make better." "Net Load Ramps Texas vs California" reads beautifully and changes no operational decision. The data-API-subscription business model makes content a marketing surface, not the product.

**For us:** REFERENCE — and learn from two specific things they do well, while structurally departing on a third.

**Why ADOPT — comparative framing as a lens** — Their "ERCOT vs CAISO" framing is exactly the framework × entity stream leverage shape we want (commitment 2). They execute it manually; we systematize it via the methodology brief layer.

**Why ADOPT — event-triggered insight surface alongside periodic** — Their split between in-app `/insights` feed (event-driven, ~paragraph-length, decays fast) and blog (periodic, comparative, longer-lived) is structurally useful. Our `applied_insight.cadence` field should support both `event_triggered` and `periodic` (candidate addition to the schema, validated by this observation).

**Why DO A STRONGER VERSION OF — decision-grounded editorial filter** — Their content fails the five-question filter (who reads this? what decision? counterfactual? delta? worth it?) on most long-form pieces. Ours can't. The five-question filter is what stops the platform from drifting into the "marketing-first content" failure mode.

## Key Failure Modes I Noticed

1. **PDF-as-atomic-unit decays at the speed of energy markets.** Solar costs fell ~75% in the decade these platforms have been operating; queue capacity grew 5x in five years; LMPs move daily. A ~30-page Wood Mac PDF written in Q2 with Q1 data is partially obsolete by Q3. Yet the platform sells it for years.

2. **Methodology lives in a separate-and-rarely-read companion doc.** Even the platforms that explicitly version methodology (NREL ATB, BNEF Tier 1 methodology) treat it as a one-time read; applied work cites it but readers don't audit it. Methodology-vs-applied separation becomes ceremonial, not load-bearing.

3. **Analyst voice doesn't survive turnover.** Wood Mackenzie's post-Verisk turnover and offshoring is the worked example — institutional voice degrades because it was always carried by individual analysts, not by structured worldviews. Every analyst who leaves takes their lens with them.

4. **The DB and the narrative are different products.** Bloomberg RMS "auto-tagging" is genuinely useful but the tag is metadata on prose; it doesn't make a claim inside the prose addressable. You can find which reports mention Vistra, but not "which analytical claims about Vistra remain valid given the Q4 data refresh."

5. **Seat-based pricing constrains content shape.** It pushes toward long, dense, infrequent reports — because that's what makes a single $30K seat feel justified. The Aurora/Wood Mac/BNEF/Rystad bundle is a class, not a coincidence. It actively works against entity-granular, frequently-updated analytical primitives.

6. **Data-API-as-primary-product makes content marketing-first.** *(added 2026-05-31)* gridstatus.io is the worked example: when the data API is the revenue product, content exists to demonstrate-the-data-is-interesting rather than to enable-the-reader-to-decide-better. Every post passes the "publishable" bar (technically accurate, well-written) and fails the "decision-grounded usefulness" bar (no actor's decision changes from reading it). We should not let our content drift into this mode — utility is the editorial test, marketing is a downstream effect.

## What's Unique to Our Position

We already have what these platforms structurally lack: a unified entity substrate (15,528 plants, 29,738 generators, ~9,783 queue projects) with atomic-fact-level extraction from the news stream, plus generation/financial/regional/pricing/weather/engineering dimensions all keyed to the same identifiers. The platforms above either have entities-without-analytics (Tegus is a transcript index, not an analytical layer), analytics-without-clean-entity-grounding (BNEF, Wood Mac, Aurora — their narratives don't bind to identifiers at the claim level), or open data without synthesis (NREL, EIA, LBNL).

The structural play: applied insights as small, typed, entity-grounded objects that *systematically* re-apply a methodology brief across the eligible entity set, declare their data vintage and invalidation conditions, and live in the same query surface as the underlying entities. That's a category none of them are positioned to ship — Wood Mac/BNEF would have to dismantle their PDF/seat economics to get there, and NREL/EIA aren't commercial entities and don't move at that cadence.

The one thing to internalize from this research: the prize isn't "better reports than Wood Mackenzie." It's that the entire genre of "analytical report" is the wrong unit, and the platforms above are stuck with it because they built on it. We're not yet committed to that unit — and shouldn't be.

## Sources

Primary URLs surfaced in searches that informed this report:

*(gridstatus.io references added 2026-05-31:)*
- https://www.gridstatus.io/insights
- https://blog.gridstatus.io/
- https://blog.gridstatus.io/net-load-ramps/
- https://blog.gridstatus.io/caiso-beats-the-heat/
- https://blog.gridstatus.io/western-markets-evolution-2025/
- https://github.com/gridstatus/gridstatus

*(Original 2026-05-31 research:)*

- https://www.spglobal.com/commodity-insights/en
- https://www.spglobal.com/energy/en/pricing-benchmarks/our-methodology/subscriber-notes
- https://www.spglobal.com/energy/en/pricing-benchmarks/our-methodology/methodology-review-change
- https://www.woodmac.com/lens/power-and-renewables/
- https://www.woodmac.com/press-releases/2024-press-releases/wood-mackenzie-launches-lens-power--renewables/
- https://www.woodmac.com/lens/carbon/
- https://www.woodmac.com/store/browse-categories/
- https://www.glassdoor.com/Reviews/Wood-Mackenzie-Principal-Analyst-Reviews-EI_IE36813.0,14_KO15,32.htm
- https://about.bnef.com/
- https://about.bnef.com/insights/
- https://about.bnef.com/tier-1-reports/
- https://about.bnef.com/what-we-do/
- https://assets.bnef.com/public/tiering/batterymethodology
- https://gsb-research-help.stanford.edu/library/faq/380483
- https://www.rystadenergy.com/downloads
- https://clients.rystadenergy.com/old-corporate-web/energy-themes/supply-chain/subsea/subsea-cube/
- https://pages.rystadenergy.com/UCube-10-years-products
- https://auroraer.com/
- https://auroraer.com/software
- https://auroraer.com/products/power-renewables
- https://atb.nrel.gov/
- https://atb.nrel.gov/electricity/2024/about
- https://www.nrel.gov/analysis/cambium
- https://docs.nrel.gov/docs/fy25osti/93005.pdf
- https://scenarioviewer.nrel.gov/
- https://www.eia.gov/outlooks/aeo/
- https://www.eia.gov/outlooks/aeo/narrative/index.php
- https://www.eia.gov/outlooks/aeo/section_issues.php
- https://emp.lbl.gov/
- https://emp.lbl.gov/news/new-berkeley-lab-report-quantifies-0
- https://stratechery.com/
- https://stratechery.com/concepts/
- https://stratechery.com/concept/aggregation-theory/
- https://en.wikipedia.org/wiki/Ben_Thompson_(analyst)
- https://www.bloomberg.com/account/newsletters/money-stuff
- https://www.bloomberg.com/opinion/authors/ARbTQlRLRjE/matthew-s-levine
- https://www.harvardmagazine.com/2025/07/harvard-bloomberg-column-matt-levine
- https://tegus.com/experts
- https://marketing.tegus.com/pricing
- https://www.vendr.com/marketplace/tegus
- https://help.alpha-sense.com/hc/en-us/articles/43616741825939-Tegus-Expert-Transcript-Library-Understanding-Transcript-Types-Perspectives
- https://www.rand.org/content/dam/rand/pubs/research_reports/RR200/RR292/RAND_RR292.pdf
- https://www.nber.org/research/data/nber-working-papers-and-chapters-metadata
- https://www.nber.org/subscribe/information-libraries
- https://www.bloomberg.com/professional/insights/risk/leverage-bloomberg-internal-research-management/
- https://www.nature.com/articles/s41597-025-05951-4 (cost data staleness in energy research)
- https://onlinelibrary.wiley.com/doi/10.1111/1911-3846.12875 (analyst report failure-mode research)
