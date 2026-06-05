# 01 - Scope V0

> **Status**: execution scope, deepened 2026-06-05.
>
> **Goal**: define exactly what the first InfraSure Insights team deliverable is and what it is not.

## Scope Statement

V0 creates one methodology-backed insight package for:

```text
El Niño / ENSO exposure
  -> renewable assets
  -> one region or market
  -> actor relevance
```

The package should let a contributor run a manual Claude/MCP test using existing InfraSure data tools. The result should be one applied-insight draft that is grounded, caveated, and reviewable.

## V0 Deliverable

The required deliverable is:

```text
one methodology resource package
  + one prompt projection
  + one data requirements map
  + one applied-insight draft
  + one manual MCP/Claude test run
  + one learning/gap log
```

The resource package lives under `resources/weather_and_climate/el_nino_enso/` and has a fixed shape:

```text
resources/weather_and_climate/el_nino_enso/
├── README.md                      orientation + scope
├── resource.md                    human-readable method        ┐
├── resource.yml                   structured operational fields ├─ the method, 3 forms
├── prompt_projection.md           pasteable session surface     ┘
├── data_requirements.md           input map (substrate/external/descriptive/actor)
├── examples/
│   └── applied_insight_001.md     target output shape (→ replace with real test output)
└── test_runs/
    └── test_run_001.md            manual validation record (→ fill after the test)
```

| Deliverable | Purpose | Pass Condition |
|---|---|---|
| `resource.md` | Human-readable method | Explains the question, scope, mechanism, allowed claims, blocked claims, caveats, and review needs |
| `resource.yml` | Structured operational fields | Encodes identity, scope, inputs, procedure, claims, confidence, caveats, and actor relevance |
| `data_requirements.md` | Input map | Separates substrate inputs, external inputs, descriptive context, and actor context |
| `prompt_projection.md` | Claude/MCP instruction surface | Can be pasted into a Claude project/session without carrying the whole repo |
| `examples/applied_insight_001.md` | Target output shape | Includes claim, scope, refs, confidence, caveats, actor relevance, and review trace |
| `test_runs/test_run_001.md` | Manual validation record | Records loaded files, tools used, output quality, failures, and next fixes |
| `docs/learning/logs/` entry | Learning record | Captures what the contributor learned and what was unclear |

The standard each file must meet is `docs/03_methodology_resource_standard.md`; the learning companions are `docs/learning/03_methodology_resources.md` and `04_prompt_projection.md`.

## MCP-Ready, Not MCP-Integrated

V0 should be MCP-ready. It should not build direct MCP integration.

```text
resource files
  -> prompt projection
  -> manual Claude/MCP session
  -> applied-insight draft
  -> logged gaps
```

Do not build:

- a production agent
- an API orchestrator
- a database table
- automated batch generation
- an email automation workflow
- new MCP tools unless the test proves a specific tool gap

The first test can happen in a Claude project or chat session where the methodology files are loaded or pasted alongside existing InfraSure MCP/data tools. (One real gap is already known — `search_plants(iso=…)` returns empty; scope by `state` and **log** it. The fix is roadmap, not v0 scope. See `docs/learning/01_mcp_basics.md`.)

## Gate 1 - What Analysis Should Exist?

InfraSure Insights should provide infrastructure decision intelligence, not market commentary.

The atomic question is:

```text
What grounded change, exposure, opportunity, or constraint affects
a specific asset, region, company, offtaker, or portfolio,
and what can InfraSure responsibly claim about it?
```

The canonical analysis-family map lives in `docs/02_analysis_catalog.md`.

V0 starts with:

```text
Exposure -> consequence -> actor relevance
```

## Gate 2 - What Evidence And Logic Are Required?

Every methodology resource must identify:

- what InfraSure substrate inputs are needed
- what external sources are needed
- what descriptive context is useful but not claim-grounding
- what actor/account context matters for activation
- what reasoning steps convert inputs into claims
- what claims are allowed, downgraded, or blocked

The standard lives in `docs/03_methodology_resource_standard.md`; the input taxonomy lives in `docs/04_context_and_data_map.md`.

## Learning Track

Learning is a parallel track under `docs/learning/`. It supports contributors but does not replace deliverables.

The learning track should cover:

- basics of MCP
- basics of InfraSure's data substrate
- how methodology resources work
- how prompt projections are used
- how to review LLM output
- what failed during each test

Learning logs should be concrete. They should record confusion, tool gaps, missing context, bad outputs, and useful patterns.

## Acceptance Criteria

V0 is complete when:

- a new contributor can explain the v0 deliverable after reading `README.md` and this file
- `prompt_projection.md` can be used in a manual Claude/MCP test
- the test produces one applied-insight draft
- every material claim in the draft has a source reference or an explicit external-source dependency
- confidence and caveats are present
- actor relevance is present
- failures are categorized as methodology gaps, MCP/tool gaps, external-data gaps, or orchestration gaps

**What a passing draft looks like (grounded sketch, 2026-06-05):**

```text
claim:    "CA solar (e.g. Topaz 57695, Desert Sunlight 57993) is directionally
           exposed to ENSO-driven winter-irradiance shifts" — confidence LOW
refs:     external NOAA CPC ENSO state (dated) + substrate get_plant CF series + aggregate fleet total
caveats:  directional only; not a plant-level or LMP forecast; SW teleconnection is noisy
actor:    owners (Clearway/BHE) + offtaker PG&E should monitor seasonal generation variance
blocked:  any "$/MWh" or "GWh lost" number from ENSO alone
```

## Out Of Scope

V0 does not include:

- direct MCP integration
- new production code
- production database schemas
- public platform pages
- automated outreach
- LinkedIn or people-profile scraping
- exact LMP forecasting
- national all-asset scans

## After V0

After the first successful manual test, work can split:

```text
validated insight object
        ├── in-house architecture track
        └── activation / outreach track
```

The in-house track builds controlled API orchestration, retrieval planning, trace capture, validation gates, persistence, and review queues. (Every tool gap logged during testing — like the `iso` filter — is an input to this track's MCP roadmap.)

The activation track uses validated insight objects with contacts/company/offtaker context to create platform cards, account notes, and informative email drafts.
