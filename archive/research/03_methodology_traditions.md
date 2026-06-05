# Research 03 — Methodology / Knowledge Representation Traditions

> Status: research complete. For reference only — our methodology briefs ground in a specific substrate, unusual vs. pure-abstract traditions.

## TL;DR (3-4 sentences)

Every mature analytical tradition that has survived author turnover converges on the same shape: a stable identity (slug + persistent ID) decoupled from a versioned content body, with explicit dates/qualifiers governing when a claim is true, machine-readable typed pointers to data sources, and explicit edges to other units of knowledge (cites / supersedes / depends-on). The four traditions that map closest to our problem — Stanford Encyclopedia of Philosophy (evergreen revisable entries with quarterly archived editions), arXiv (immutable versioned snapshots under a stable identifier), the Common Information Model / Open Energy Ontology (typed objects with formal class hierarchies grounding to physical assets), and Diátaxis (separation of *reference* from *explanation* from *how-to*) — give us all the structural primitives we need. The unusual constraint — methodology that must be both reusable AND tied to specific platform queries — is solved by treating the brief as a *typed* unit whose Scope, Substrate Inputs, and Worked Examples fields are first-class entities that resolve against our existing plant / project / region / dimension graph, not freeform prose. None of these traditions does this in our exact way; the gap is the wedge.

## Traditions Investigated

1. **RAND Corporation reports** — Multi-series taxonomy (R-, RM-, monographs, technical reports, research briefs, occasional papers). Unit: the *report*, identified by series-letter + number + optional volume slash (e.g. `R-262/1`). Long-lived archival presence; numbering carries series semantics.
2. **NBER working papers** — Single active series with ISSN. Unit: the *working paper*, periodically revised; subscribers expected to detect revisions. Citation convention allows citing both the working-paper and the eventually-published version, distinguishing claims that differ across versions.
3. **Stanford Encyclopedia of Philosophy (SEP)** — Evergreen revisable entries with **quarterly fixed editions** archived at fixed dates (Sep/Dec/Mar/Jun 21). Unit: the *entry*, with both a "current" mutable URL and immutable archived URLs. Citation rules require the archived URL.
4. **arXiv** — Immutable versioned snapshots (v1, v2, …) under one stable identifier with a DOI that resolves to the latest version. Replacement creates a new version; metadata-only updates do not. Permanent record principle: no version is ever deleted.
5. **NREL Annual Technology Baseline (ATB)** — Annual edition of cost / performance parameters for power-generation technologies through 2050. Unit: the *parameter set*, published as parquet/CSV/Excel/Tableau with wildcard key columns. Annual cadence = annual immutable snapshot.
6. **LBNL Queued Up** — Annual edition (e.g. "2025 Edition" reflects end-of-2024 data) with PDF report + Excel data file + codebook + 35 summary tabs. The codebook is the methodology metadata; the parquet is the substrate. Annual cadence.
7. **CIM / IEC 61970** — UML class model of the power system domain with RDFS mapping (61970-501). Unit: the *typed object* (Transformer, Generator, Substation…). Not methodology per se, but the canonical example of typed objects grounding to physical reality.
8. **Open Energy Ontology (OEO)** — ~900 classes (300 OEO-owned + 600 imported), with first-class concepts like *energy transformation unit*, *nameplate capacity*, *fuel*. Class hierarchy + property constraints.
9. **Diátaxis** — Four-quadrant documentation framework: tutorial / how-to / reference / explanation, distinguished on two axes (acquisition-vs-application × practical-vs-theoretical). Unit: the *document of one quadrant*.
10. **Wikidata** — Statement-with-qualifiers model. Every statement can carry temporal qualifiers (`start time`, `end time`, `point in time`), constraint metadata, and provenance. Unit: the *statement*, not the entity.
11. **Schema.org `ScholarlyArticle` + `Dataset` + `DefinedTerm`** — JSON-LD vocabulary for scholarly content with `sameAs`, `schemaVersion`, `keywords` via `DefinedTerm` (controlled vocabulary). Unit: the *typed creative work*.
12. **CITATION.cff** — YAML metadata file co-located with the artifact (code repo). Required keys: `cff-version`, `title`, `authors`, `message`. Co-location is the philosophy: the citation lives next to the thing cited.
13. **FAIR data principles** — Findable / Accessible / Interoperable / Reusable. Machine-actionable metadata + persistent identifiers + controlled vocabularies + provenance + license = baseline contract.
14. **McKinsey / Brookings topic-hub pattern** — Topic landing pages aggregate evergreen frameworks + dated commentary. Unit: the *topic*, with a stable URL hosting a stream of dated artifacts.

## 5–7 Distilled Learnings on Modeling Methodology

### Learning 1: Identity must outlive content
**Source(s):** SEP, arXiv, NBER, CITATION.cff, Wikidata
**What it is:** Every survivor decouples a stable identifier (slug / arXiv ID / Q-number / DOI) from a mutable or versioned content body. The identifier is the citation target; the body evolves. Without this split, every revision breaks every citation.
**For us:** **ADOPT — STRONGER VERSION.** A methodology brief gets a slug (`thermal-repower-npv`) and a numeric `brief_id` from day one. Citing surfaces (applied insights, plant pages) reference the slug, not the rendered Markdown.
**Why:** Our applied insights will cite methodology briefs by the thousands. If the citation breaks every time we sharpen the methodology, the system is dead. Slug stability is the spine.

### Learning 2: Two clocks — "current view" and "as-of view"
**Source(s):** SEP (active vs archived editions), arXiv (latest vs vN), Wikidata (point-in-time qualifier)
**What it is:** SEP's killer move is letting users *read* the current entry but *cite* a frozen archived edition. arXiv does the same with v1/v2. The user always sees the freshest synthesis; the citer always pins a specific snapshot.
**For us:** **ADOPT.** Every methodology brief has (a) a live view and (b) periodic immutable snapshots — quarterly is right for our cadence (matches the EIA-860M / queue refresh rhythm). Applied insights cite the snapshot ID, never the live brief. We get the best of both: freshness without breaking the audit trail.
**Why:** Applied insights have a fixed publication date and shouldn't drift in meaning when the methodology beneath them is sharpened later. SEP solved this in 1995; we just adopt it.

### Learning 3: Structure the inputs, not just the prose
**Source(s):** CIM, OEO, Wikidata, NREL ATB, FAIR
**What it is:** Mature analytical traditions treat the *inputs* to a method as first-class structured objects, not paragraphs. CIM types every electrical asset; OEO types every fuel/capacity/conversion; ATB parameterizes by `technology × year × scenario × metric`. The prose narrates; the structure binds.
**For us:** **ADOPT — STRONGER VERSION.** A methodology brief's `substrate_inputs` field is a typed list of references into our existing dimension graph: which plant fields, which generator specs, which financial columns, which region polygons. Not "uses EIA-860 capacity data" in prose — `inputs: [{ dim: engineering_generator, field: nameplate_capacity_mw }, …]`. This is the moat: it makes the methodology *executable*, not just readable.
**Why:** This is exactly what distinguishes us from RAND/Brookings/RFF — our methodology grounds to a substrate that can be queried. If the inputs are prose, we're just another think-tank; if they're typed pointers, we're an analytical engine.

### Learning 4: Explicit edges, not implicit references
**Source(s):** Wikidata (typed properties), Schema.org (`sameAs`/`isBasedOn`/`citation`), arXiv (replaces/replaced-by)
**What it is:** Every mature system models inter-document relationships as typed first-class edges with their own semantics, not as bare URLs in body text. Wikidata's `subclass of`, `superseded by`, `instance of` are properties, not prose. Schema.org distinguishes `citation` from `isBasedOn` from `sameAs`.
**For us:** **ADOPT.** A methodology brief carries: `extends: [other_brief_slug]`, `depends_on: [other_brief_slug]`, `supersedes: [other_brief_slug]`, `cites_data: [source_id]`. Plus a reverse edge so we can render "applied insights using this brief" on every brief page.
**Why:** When we want to mass-update — "we sharpened heat-rate methodology; what depends on it?" — we either have a typed graph or we have a grep problem.

### Learning 5: Reference ≠ Explanation ≠ Methodology — and a brief is all three
**Source(s):** Diátaxis
**What it is:** Diátaxis's contribution is that *reference* (the bare facts), *explanation* (the why), and *how-to* (the steps) are different cognitive modes serving different needs. Mixing them produces docs that fail all three audiences.
**For us:** **ADOPT — with the unusual twist that a methodology brief is intentionally hybrid.** A brief has a Reference section (typed inputs/outputs), an Explanation section (the analytical worldview), and a How-To section (the procedure, ideally as a runnable query template). Diátaxis says don't mix; we say *segment*. Each brief has all three regions but they're labeled and structured separately.
**Why:** Our briefs serve three audiences — applied-insight authors (need how-to), platform users (need explanation), and other methodologists (need reference). Segmenting honors the framework while doing what we actually need.

### Learning 6: Staleness signals must be machine-readable
**Source(s):** Wikidata qualifiers, FAIR (reusable + provenance), ATB (annual edition flag), SEP (last-revised date)
**What it is:** Every system that fights staleness encodes it as data: "this claim is valid as-of 2024-12-31", "this entry was last revised on X", "this parameter set is the 2025 edition". Never relegated to a footnote.
**For us:** **ADOPT.** Each brief carries: `last_reviewed`, `expected_review_cadence` (quarterly / annual / triggered-by-dataset-update), `validity_window` (when the claim holds), and a `staleness_signals` list — events that should trigger a review (e.g. "FERC EQR schema change", "new LBNL Queued Up edition"). When a feeder dataset refreshes, we can compute which briefs are now stale.
**Why:** Without this we drift into the think-tank failure mode where 2018 frameworks linger unchallenged on the site for 5 years. With it, the system tells us what to refresh.

### Learning 7: The thing cited is not the thing read
**Source(s):** SEP archived editions, CITATION.cff, arXiv DOI-vs-version
**What it is:** Citation metadata is a separate artifact from the readable content. CITATION.cff sits next to the code; SEP's "How to cite" is a different page from the entry; arXiv DOIs resolve to a metadata abstract page, not the PDF.
**For us:** **ADOPT (LIGHTWEIGHT).** Every brief generates a citation block — JSON-LD `ScholarlyArticle` + a copy-paste APA/BibTeX/inline-Markdown snippet — derived from the structured fields, not hand-written. Plus a stable `/insights/methodology/<slug>/cite` URL that always resolves.
**Why:** If the brief is genuinely useful, people outside InfraSure.ai will want to cite it. Making citation a structured derivative (not editorial work) costs us nothing and means every brief is citable on day one.

## Proposed Structure for a Methodology Brief

```yaml
# methodology_brief.schema.yml — DRAFT v0
# (provocative, expect iteration)

# ── Identity (immutable after first publish) ──────────────────────────────
slug: thermal-repower-npv                  # URL slug, never changes
brief_id: MB-0007                          # numeric persistent ID
title: "Estimating Thermal Repower NPV from Heat Rate + Fuel Cost + Capacity Payments"
short_title: "Thermal Repower NPV"         # for chips, breadcrumbs
kind: methodology_brief                    # vs. applied_insight

# ── Versioning (two clocks) ───────────────────────────────────────────────
version: "1.2.0"                           # semver; major = breaking re-interpretation
current_snapshot: "2026-Q2"                # latest immutable edition
snapshots:                                 # archived editions (SEP-style)
  - id: "2026-Q1"
    published: 2026-03-21
    snapshot_url: /insights/methodology/thermal-repower-npv/2026-Q1
  - id: "2026-Q2"
    published: 2026-06-21
    snapshot_url: /insights/methodology/thermal-repower-npv/2026-Q2
last_reviewed: 2026-05-31

# ── Subject matter ────────────────────────────────────────────────────────
topics:                                    # controlled vocabulary (DefinedTerm-style)
  - fuel:natural_gas
  - lifecycle:repower
  - finance:npv
  - finance:capacity_payments
keywords: [heat rate, repower, NPV, capacity market, capacity factor]

# ── Scope (what entities the methodology applies to) ──────────────────────
scope:
  entity_types: [plant, generator]
  fuel_filter: [NG, DFO, RFO, BIT, SUB, LIG]   # thermal only
  region_filter: any                            # ISO-agnostic
  capacity_filter: { min_mw: 50, max_mw: null } # utility-scale
  lifecycle_phase: [operating, retiring]

# ── Substrate inputs (THE differentiator) ─────────────────────────────────
# Typed pointers into our dimension graph — not prose.
substrate_inputs:
  - dim: engineering_generator
    fields: [nameplate_capacity_mw, heat_rate_btu_per_kwh, prime_mover, fuel_primary]
    required: true
  - dim: generation
    fields: [annual_net_generation_mwh, capacity_factor]
    required: true
    aggregation: trailing_12_months
  - dim: financial
    fields: [fuel_cost_per_mmbtu, capacity_payment_per_kw_month]
    required: false
    fallback: { source: NREL_ATB_2025, scenario: "Moderate" }
  - dim: regions
    fields: [iso_rto, capacity_market]
    required: true

# ── Analytical procedure ──────────────────────────────────────────────────
procedure:
  reference:                                  # Diátaxis: bare facts
    output_metric: { name: repower_npv_usd, unit: USD, sign: positive_is_attractive }
    horizon_years: 20
    discount_rate_default: 0.085
  explanation: |                              # Diátaxis: the worldview (prose)
    Thermal repower economics turn on whether the spread between the
    capacity payment + energy margin under a new heat rate exceeds the
    capex of the retrofit, after netting the residual book value of
    the existing asset. The methodology assumes …
  how_to:                                     # Diátaxis: executable recipe
    - step: pull_inputs
      query: SELECT … FROM engineering_generator WHERE plant_id = :id
    - step: compute_baseline_margin
      formula: "(lmp_avg - heat_rate * fuel_cost) * net_gen"
    - step: compute_repowered_margin
      formula: "(lmp_avg - heat_rate_new * fuel_cost) * net_gen_uplift"
    - step: discount_and_sum
      formula: "Σ (cf_t / (1 + r)^t) - capex_retrofit"

# ── Worked examples (how applied insights consume this) ───────────────────
worked_examples:
  - title: "Permian Basin gas peakers — repower candidates Q1 2026"
    applied_insight_slug: ercot-thermal-repower-q1-2026
    entity_filter: { iso: ERCOT, fuel: NG, prime_mover: GT, capacity_mw_min: 100 }
    notes: "Demonstrates fuel_cost fallback to NREL ATB when EIA-923 lags."

# ── Citation & lineage ────────────────────────────────────────────────────
citation:
  authors: [InfraSure.ai Research]            # human-or-team handle
  first_published: 2026-03-21
  doi: null                                   # reserved
  cite_as: "InfraSure.ai Research (2026). Thermal Repower NPV. Methodology Brief MB-0007 (2026-Q2). https://www.infrasure.ai/insights/methodology/thermal-repower-npv/2026-Q2"

lineage:
  extends: []                                 # other briefs this builds on
  depends_on: [heat-rate-fundamentals, lmp-locational-basis]
  supersedes: []                              # prior brief slugs replaced
  cites_data:
    - source: EIA-860
      vintage: "2024 Annual"
    - source: NREL_ATB
      vintage: "2025"
    - source: LBNL_Queued_Up
      vintage: "2025 Edition"
  cites_external:                             # outside literature
    - { type: paper, title: "…", url: "…", role: theoretical_basis }

# ── Validity & staleness ──────────────────────────────────────────────────
validity:
  asserted_window:                            # when these claims hold
    start: 2026-01-01
    end: null                                 # open-ended
  expected_review_cadence: quarterly
  staleness_signals:                          # events that trigger review
    - { source: FERC_EQR, event: schema_change }
    - { source: LBNL_Queued_Up, event: new_edition }
    - { source: NREL_ATB, event: new_edition }
    - { internal: capacity_market_reform, severity: high }
  confidence:                                 # editorial honesty
    level: medium                             # low | medium | high
    caveats:
      - "Capacity-payment forecast is mechanical; doesn't model auction dynamics."
      - "Assumes single-axis retrofit, not full repower."

# ── Surfacing ─────────────────────────────────────────────────────────────
surfacing:
  applies_to_pages:                           # where the brief earns its keep
    - { surface: plant_page, condition: "fuel in scope.fuel_filter and capacity_mw >= 50" }
    - { surface: portfolio_page, condition: "any plant matches scope" }
  applied_insights:                           # back-edge (computed, not hand-set)
    - ercot-thermal-repower-q1-2026
    - miso-coal-to-gas-repower-2026
```

## Open Questions

1. **Snapshot cadence: fixed dates vs. content-driven?** SEP picks fixed quarterly dates regardless of changes; arXiv snapshots only on author push. We're in between — our data substrate refreshes on a known cadence (monthly EIA-860M, quarterly FERC, annual ATB/LBNL), so fixed quarterly aligns nicely. But low-churn briefs would generate identical snapshots. Worth deciding: do we snapshot every brief every quarter, or only on actual content change?
2. **Who is the "author"?** When an LLM drafts and a human reviews, what does `authors: [InfraSure.ai Research]` mean for credibility? RAND/NBER attach real names; SEP attaches real names; we may not want individual names. Is a team handle enough? Does the audience care?
3. **How rich should the `how_to` block be?** Aspirational answer: literal SQL/Python that the platform can execute against the substrate, making the brief a *runnable artifact*. Realistic answer: pseudo-code for v1. Open whether we commit to runnable from day one (forcing-function for clarity, but raises the bar a lot) or treat runnable as a Phase 2 promotion.
4. **Inter-brief edges — directed or bidirectional?** `depends_on` is naturally directed. But for navigation we want bidirectional ("briefs that depend on this one"). Computed reverse edges keep storage normalized but require a build step. Worth it, or do we denormalize for simpler rendering?
5. **What's the lowest acceptable confidence level we'd publish?** SEP entries are written by domain experts and rarely admit "low confidence"; nowcasting working papers happily publish low-confidence estimates with wide intervals. We need an editorial policy on `validity.confidence.level` — is `low` publishable, or do we hold it back?

## Sources

- [RAND Research Reports](https://www.rand.org/pubs/research_reports.html)
- [Browse RAND Reports by Series](https://www.rand.org/pubs/series.html)
- [NBER Working Papers and Chapters Metadata](https://www.nber.org/research/data/nber-working-papers-and-chapters-metadata)
- [NBER Working Papers (information for libraries)](https://www.nber.org/subscribe/information-libraries)
- [Stanford Encyclopedia of Philosophy — How to Cite](https://plato.stanford.edu/cite.html)
- [SEP — Archives index](https://plato.stanford.edu/archives/)
- [SEP — Guidelines and Policies for Entry Content](https://plato.stanford.edu/guidelines.html)
- [arXiv — Version Availability](https://info.arxiv.org/help/versions.html)
- [arXiv — Submit a new version of a work](https://info.arxiv.org/help/replace.html)
- [arXiv — Understanding arXiv Assigned DOIs](https://info.arxiv.org/help/doi.html)
- [Diátaxis](https://diataxis.fr/)
- [Diátaxis — Start here](https://diataxis.fr/start-here/)
- [NREL Annual Technology Baseline (ATB) for Electricity — PUDL docs](https://catalystcoop-pudl.readthedocs.io/en/stable/data_sources/nrelatb.html)
- [OEDI: 2024 ATB Cost and Performance Data](https://data.openei.org/submissions/6006)
- [Common Information Model (electricity) — Wikipedia](https://en.wikipedia.org/wiki/Common_Information_Model_(electricity))
- [OEO Ontology — Power Plant class](https://openenergyplatform.org/ontology/oeo/OEO_00000031/)
- [OEO Ontology — Nameplate Capacity class](https://openenergyplatform.org/ontology/oeo/OEO_00230003/)
- [Introduction to the Open Energy Ontology — Open Energy Academy](https://openenergyplatform.github.io/academy/courses/05_ontology/)
- [LBNL Energy Markets & Policy — Queued Up 2025 Edition](https://emp.lbl.gov/publications/queued-2025-edition-characteristics)
- [LBNL — Queued Up landing page](https://emp.lbl.gov/queues)
- [Schema.org — ScholarlyArticle](https://schema.org/ScholarlyArticle)
- [Schema.org — Dataset](https://schema.org/Dataset)
- [ESIPFed science-on-schema.org — Dataset guide](https://github.com/ESIPFed/science-on-schema.org/blob/main/guides/Dataset.md)
- [Bioschemas — ScholarlyArticle Profile](https://bioschemas.org/profiles/ScholarlyArticle/0.3-DRAFT)
- [Wikidata — Help: Qualifiers](https://www.wikidata.org/wiki/Help:Qualifiers)
- [Wikidata — Help: Property constraints portal / Qualifiers](https://www.wikidata.org/wiki/Help:Property_constraints_portal/Qualifiers)
- [Wikidata — Data model](https://www.wikidata.org/wiki/Wikidata:Data_model)
- [CITATION.cff — Citation File Format](https://citation-file-format.github.io/)
- [CITATION.cff — schema guide](https://github.com/citation-file-format/citation-file-format/blob/main/schema-guide.md)
- [FAIR Principles — GO FAIR](https://www.go-fair.org/fair-principles/)
- [The FAIR Guiding Principles — Nature Scientific Data](https://www.nature.com/articles/sdata201618)
- [Brookings — Topics](https://www.brookings.edu/topics/)
- [Brookings — Research & Commentary](https://www.brookings.edu/research-commentary/)
- [McKinsey — Featured Insights](https://www.mckinsey.com/featured-insights)
- [McKinsey — About the Quarterly](https://www.mckinsey.com/quarterly/about-the-quarterly)
- [Enduring Ideas: Classic McKinsey frameworks](https://www.mckinsey.com/capabilities/strategy-and-corporate-finance/our-insights/enduring-ideas-classic-mckinsey-frameworks-that-continue-to-inform-management-thinking)
