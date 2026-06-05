# Initial Scope — Methodology Resource Layer v0

> **Status**: draft scope, 2026-06-02.
>
> **Goal**: define the first stable shape of the InfraSure methodology registry: what kinds of insights it should enable, what data and logic those insights require, and why the first prototype should use El Niño / climate-regime effects on energy assets.

---

## 0. First-reader context

InfraSure is a decision-grade risk intelligence platform for energy infrastructure. The front-page promise is:

- **forward-looking** — scenario paths for weather, hazards, prices, revenue, insurance, debt, and resilience
- **localized** — site-level hazard, grid, nodal, corridor, and market context
- **asset-specific** — components, subsystems, policy terms, leverage, cashflow, and resilience levers

The core user is not reading for generic energy commentary. Owners, investors, and lenders are trying to decide:

| Actor | Core Question | InfraSure Job |
|---|---|---|
| Owner / operator | What action does this asset need? | Surface exposure, insurability, resilience ROI, and operational response |
| Investor | What is the downside to the return case? | Translate infrastructure conditions into IRR, downside, and terminal-value implications |
| Lender | Does this asset service debt under stress? | Translate physical and market stress into DSCR, covenants, and credit risk |

The current platform already has a large data substrate: plants, projects, companies, offtakers, news facts, generation, engineering, pricing, financials, and context summaries. The missing layer is the methodology resource that tells an LLM how to reason over that substrate.

The simplest version of the vision is:

```text
MCP data tools
  ↓
Methodology-backed analyst
  ↓
Grounded applied insight
  ↓
Contacts / account overlay
  ↓
Standardized outreach funnel
```

Meaning:

- **MCP data tools** let the LLM use InfraSure's curated data instead of guessing.
- **Methodology-backed analyst** gives the LLM domain depth on one topic: what to retrieve, how to reason, what not to claim, and how to caveat.
- **Grounded applied insight** is the reusable output: claim, scope, sources, confidence, caveats, and actor relevance.
- **Contacts / account overlay** maps the insight to companies, owners, developers, offtakers, portfolios, and eventually people/account context.
- **Standardized outreach funnel** turns the validated insight into account notes, informative emails, platform cards, and follow-up prompts.

Expanded:

```
InfraSure data tools
  plants · projects · generation · pricing · news facts · companies · offtakers
        │
        ▼
Methodology registry
  reasoning procedure · allowed claims · caveats · confidence rules
        │
        ▼
Applied insight
  grounded claim · scope · source refs · actor relevance · review trace
        │
        ▼
Renderings
  platform card · Ask answer · account note · informative email
```

This file scopes that methodology layer.

---

## 1. The two gates

The methodology registry should not start as a folder of interesting topics. It should start with two gates.

```
GATE 1: What kind of intelligence should InfraSure produce?
        ↓
        decides which methodology resources deserve to exist

GATE 2: What evidence + logic does each kind of intelligence require?
        ↓
        decides schemas, folders, test protocol, and MCP/resource shape
```

If Gate 1 is skipped, the registry becomes a pile of methods with no product discipline. If Gate 2 is skipped, the registry becomes prose that Claude can read but cannot reliably operate.

---

## 2. Gate 1 — what kind of insights should exist?

Canonical detail lives in [`00_analysis_catalog.md`](00_analysis_catalog.md). This section keeps the summary needed to understand the v0 scope.

InfraSure Insights should provide **infrastructure decision intelligence**, not market commentary.

The atomic question is:

> What grounded change, exposure, opportunity, or constraint affects a specific asset, region, company, offtaker, or portfolio — and what can InfraSure responsibly claim about it?

### 2.1 Analysis families

These are the initial families of methodology resources worth considering. They are not all v0 work; they define the map.

| Family | Question It Answers | Example Insight |
|---|---|---|
| **Exposure** | Who or what is exposed to this external condition? | CAISO solar assets exposed to ENSO-driven seasonal irradiance shifts |
| **Performance** | Is this asset behaving differently than comparable assets? | Plants underperforming peers after controlling for region, fuel, and vintage |
| **Commercial** | Who buys/sells power, and what does that imply? | Owners with corporate offtaker concentration visible in FERC EQR |
| **Development Risk** | Which projects are likely delayed, stuck, or fragile? | Queue projects with multi-signal delay risk from milestones, news facts, and queue status |
| **Portfolio Strategy** | What does this company’s asset base imply? | Owners concentrated in a weather, hazard, or market-risk pocket |
| **Market Context** | How does regional structure affect asset economics? | Solar assets in regions with poor revenue realization or curtailment exposure |
| **Event Translation** | What does this event mean for assets? | Weather, regulatory, queue, or market events mapped to affected assets and actors |

### 2.2 The initial family to test

For v0, start with:

```
Exposure → consequence → actor relevance
```

Why this family first:

- It matches InfraSure’s product promise: forward-looking, localized, asset-specific risk intelligence.
- It forces the system to connect external conditions to concrete assets.
- It naturally produces activation/outreach targets: owners, offtakers, developers, lenders, and regions.
- It is broad enough to matter commercially but narrow enough to test with one resource.

### 2.3 Q&A grammar

Every methodology resource should be able to answer this sequence:

```
1. What changed, or what condition exists?
2. Which assets / regions / companies / offtakers are in scope?
3. What mechanism connects the condition to infrastructure outcomes?
4. What can InfraSure claim with confidence?
5. What is only directional, caveated, or not publishable?
6. Who should care, and why?
7. What should be watched next?
```

This grammar is more important than article structure. It tells the methodology resource what job it has.

---

## 3. Why El Niño / climate regimes first?

El Niño / ENSO is a good first test because it sits directly inside the InfraSure promise:

```
climate regime
   → localized weather / irradiance / demand tendencies
   → asset-level generation, demand, and market implications
   → owner / investor / lender / offtaker relevance
```

It is not just a climate topic. It is a stress test for InfraSure’s ability to translate external conditions into infrastructure-relevant claims.

### 3.1 Why this question matters

Energy assets are affected by climate regimes through multiple pathways:

| Pathway | Asset/Market Effect | Why InfraSure Cares |
|---|---|---|
| Solar irradiance | Capacity factor shifts, seasonal production differences | Asset revenue, offtake delivery, portfolio performance |
| Temperature / demand | Cooling/heating load, peak timing, reserve margin pressure | Market prices, reliability, grid stress |
| Hydro / precipitation | Reservoir storage, hydro generation availability | Regional supply stack and price formation |
| Wind / atmospheric patterns | Seasonal wind resource shifts | Wind output and portfolio balancing |
| Extreme weather correlations | Storm, flood, wildfire, drought, heat stress tendencies | Insurability, resilience, operational planning |
| Market translation | LMP, curtailment, congestion, capacity value | Investor/lender downside and owner operating response |

Generic analysis can say “El Niño changes weather patterns.” InfraSure should answer:

> Which assets and actors in our substrate are exposed to the current or forecast climate regime, through which mechanism, with what confidence, and what should be watched next?

### 3.2 Why it is a strong registry test

El Niño forces the methodology registry to handle:

- **external data** — NOAA CPC / ONI / seasonal outlooks, with their own vintage clocks
- **region crosswalks** — climate regions do not map cleanly to ISO, BA, NERC, state, or plant boundaries
- **vector outputs** — irradiance, generation, demand, LMP, hydro, wind, and hazard implications are different outputs
- **mixed claim types** — mechanistic, statistical, correlational, and scenario-based claims in one methodology
- **temporal scale** — multi-year climate cycles do not fit neatly into quarterly snapshot cadence
- **fan-out** — one methodology can apply to plants, regional fleets, company portfolios, and offtaker-linked assets
- **actor-specific framing** — owner, investor, lender, operator, and offtaker care about different parts of the same causal chain

### 3.3 What not to overclaim in v0

The first prototype should not pretend to predict precise LMP impacts. LMP is a downstream, highly conditional claim. It can be included as caveated market context, but not as the core success criterion.

The cleaner first chain is:

```
ENSO state / forecast
  → regional weather or irradiance tendency
  → affected asset or regional fleet
  → owner / offtaker / portfolio exposure
  → caveated market or revenue implication
```

---

## 4. Gate 2 — what data and logic are needed?

The registry needs to distinguish data by job. Not all context is claim grounding.

| Layer | Examples | Job |
|---|---|---|
| **Grounding substrate** | plant, project, generation, engineering, financial, pricing, news facts, companies, offtakers | Supports material claims |
| **Descriptive context** | `riorg/dimensions/context`, plant descriptions, Wikipedia summaries | Frames the entity; does not by itself validate analytical claims |
| **External methodology input** | NOAA CPC, ONI, seasonal outlooks, climate-region definitions | Supplies non-platform causal state |
| **Actor context** | companies, owners, developers, offtakers, PPAs, future people/account layer | Determines activation/outreach relevance |
| **Logic layer** | formulas, thresholds, crosswalks, confidence rules, caveat rules | Converts data into claims |

### 4.1 Claim grammar

Applied insights should be built from a consistent claim grammar:

```
condition
  + scoped entity set
  + mechanism
  + evidence
  + confidence
  + caveat
  + actor relevance
  = applied insight claim
```

Example shape:

```yaml
claim:
  condition: "Forecast El Niño conditions for winter 2026-2027"
  scope: "CAISO solar plants >= 50 MW in affected climate-region crosswalk"
  mechanism: "ENSO-associated cloud/precipitation pattern may reduce seasonal irradiance"
  evidence:
    - external: "NOAA CPC ENSO status / seasonal outlook"
    - substrate: "plant locations, fuel=SUN, capacity, region mapping"
  confidence: low
  caveat: "Directional climate-regime exposure; not a plant-level production forecast"
  actor_relevance: "Owner/investor should monitor seasonal generation variance and revenue sensitivity"
```

### 4.2 Methodology resource contract

The methodology resource should encode the logic layer explicitly:

```text
methodology_resource
├── identity
│   └── slug · title · version · status
├── question_grammar
│   └── what the resource is allowed to answer
├── scope
│   └── entity types · fuels · regions · lifecycle phase · actors
├── inputs
│   ├── substrate_inputs
│   ├── external_inputs
│   ├── descriptive_context
│   └── actor_context
├── region_resolution
│   └── external geography → platform entities
├── procedure
│   └── ordered reasoning steps
├── allowed_claims
│   └── what can be stated
├── blocked_claims
│   └── what must not be stated
├── confidence_rules
│   └── when to keep, downgrade, or block
├── caveats
│   └── required caveats by claim type
├── actor_relevance
│   └── who cares, why, and which rendering uses it
└── prompt_projection
    └── concise instructions for Claude/MCP test
```

---

## 5. Initial folder architecture

The registry should become artifact-first, not code-first. Do not create a generic `software/` folder yet. If code becomes useful, add a `test_harness/` or `prototypes/` folder after the first resource proves the shape.

Proposed v0 architecture:

```text
methodology_registry/
├── README.md
├── initial_scope.md
├── 00_analysis_catalog.md          # families of insights + question grammar
├── 01_resource_contract.md         # what every methodology resource must contain
├── 02_context_and_data_map.md      # grounding vs framing vs activation inputs
├── 03_test_protocol.md             # how MCP + Claude tests are judged
├── schemas/
│   ├── methodology_resource.schema.yml
│   ├── applied_insight_thin.schema.yml
│   └── source_ref.schema.yml
├── resources/
│   └── el_nino_enso/
│       ├── resource.md             # human-readable method
│       ├── resource.yml            # structured operational fields
│       ├── prompt_projection.md    # what Claude sees
│       ├── data_requirements.md    # MCP/external input checklist
│       ├── examples/
│       │   └── applied_insight_001.md
│       └── test_runs/
│           └── 2026-06-02_run_001.md
└── notes/
    └── open_questions.md
```

This is the architecture implied by the two gates:

- `00_analysis_catalog.md` answers Gate 1.
- `01_resource_contract.md`, `02_context_and_data_map.md`, and `03_test_protocol.md` answer Gate 2.
- `resources/el_nino_enso/` is the first applied test.

---

## 6. First prototype scope

Use the El Niño / ENSO methodology as the first resource.

The first prototype should be general enough to describe the methodology, but narrow enough to test on one concrete scope.

Recommended first test scope:

```
El Niño / ENSO exposure
  → one region or market
  → solar regional fleet or owner portfolio
  → actor relevance
```

Do not start with:

- a precise LMP forecast
- a national all-asset scan
- a fully automated email campaign
- a production database schema

### Deliverables

1. **Methodology resource v0**
   - Human-readable Markdown/YAML shape.
   - MCP-readable enough to be pasted or loaded into a Claude/MCP test.
   - Includes scope, required inputs, reasoning procedure, outputs, caveats, confidence rules, staleness signals, and examples.

2. **Prompt projection**
   - A concise version of the resource that can be passed to Claude as instructions.
   - Should not include broad prose that dilutes tool-use discipline.

3. **Applied-insight thin contract**
   - Not the full production schema.
   - Enough to judge outputs consistently:
     - claim
     - scope
     - methodology reference
     - source refs
     - confidence
     - caveats
     - activation relevance

4. **One MCP + Claude test run**
   - Use MCP/data tools plus the methodology resource.
   - Produce one applied-insight draft scoped to one asset, region, company, or offtaker.
   - Record what worked and what failed.

5. **Context dependency note**
   - Name which context sources were used:
     - platform MCP tools
     - `riorg/dimensions/context/`
     - `contacts/` company/offtaker artifacts
     - news facts or news-substrate artifacts
   - Record whether each context source was useful for framing, claim grounding, or activation.

---

## 7. Acceptance criteria

- The methodology resource is operational, not just explanatory.
- The model can identify which tools or data inputs it needs before drafting the insight.
- Every material claim in the output has either a platform source reference or an explicitly named external source reference.
- Confidence is declared and caveats are attached to low/uncertain claims.
- The applied-insight draft is structured enough to support at least two renderings: platform card and informative email/account note.
- Failures are documented as either methodology-resource gaps, MCP-tool gaps, external-data gaps, or model/orchestration gaps.

---

## 8. Parallel track decision after the first test

After the first successful MCP + methodology test, work can split:

```
validated insight object
        ├── in-house architecture track
        └── activation/outreach track
```

### 8.1 In-house architecture track

- API-based orchestration
- LLM provider calls
- retrieval planning
- trace capture
- validation gates
- storage and review queue
- batch/scaled production

### 8.2 Activation/outreach track

- target selection by asset, company, offtaker, or region
- account context assembly
- informative email draft generation
- platform insight cards
- Ask/MCP answer reuse

The activation track does not have to wait for the full in-house architecture. It does have to consume a validated insight object, not raw ungrounded prompts. Its primary context source is `contacts/` plus the ported companies/offtakers dimensions; the future people layer is additive, not a prerequisite.

---

## 9. Caveats

- Do not overbuild the database layer yet. A registry of 1-3 resources is enough to test the premise.
- Do not start with email generation. Email is a rendering and activation surface, not the insight source of truth.
- Do not rely on LinkedIn personal-profile scraping. Company/offtaker/asset context is enough for the first activation tests.
- Do not treat the methodology brief as a prose article. It must function as a control surface for the model.
- Do not build a generic multi-agent framework until the first resource demonstrates that the reasoning shape works.
- Do not let LMP or market-price precision become the v0 success criterion. Directional, caveated exposure intelligence is the right first test.

---

## 10. Open questions

1. Should the first El Niño resource be scoped to CAISO, ERCOT, or another region?
2. Should the first applied insight target a regional solar fleet, an owner portfolio, or an offtaker/account?
3. Which external climate source should be treated as the first-class input for the prototype: NOAA CPC ENSO status, seasonal outlooks, historical ONI, or a small manually curated snapshot?
4. What is the minimum source-reference format that is good enough for the Claude/MCP test before production tuple refs exist?
5. How much actor relevance belongs inside the methodology resource versus inside the activation/outreach layer?
