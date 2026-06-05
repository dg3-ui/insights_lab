# InfraSure.ai — Insights Lab

> **Status**: ideation phase, started 2026-05-31. Lab folder; not yet in the platform repo.
>
> **What this is**: a structured exploration of a future "Insights" layer for InfraSure.ai — synthesized, scope-grounded analytical content that sits *on top of* the existing news/structural/financial/regional substrate. Two content types under one roof:
> - **Methodology briefs** — reusable analytical worldviews. Evergreen. Spine of the system.
> - **Applied insights** — specific, scoped, time-bound analytical statements that ground in methodology + substrate.
>
> **What this is NOT**: an extension of the news pipeline. News is one of many feeders; insights is a step up — synthesis, not extraction.

## How this lab is organised

```
insights_lab/
├── README.md                            ← you are here
├── 00_research_synthesis.md             ← unified read across the three research threads
├── 01_principles.md                     ← analysis principles (graduates to business/ once user signs off)
├── 02_methodology_brief_shape.md        ← what a methodology brief IS as a structured unit (v0 schema)
├── 03_applied_insight_shape.md          ← (next) what an applied insight IS — depends on 02
├── 04_agent_architecture.md             ← (next) the agentic system that produces them
├── methodology_registry/                ← operational methodology resources for MCP/Claude testing
│   ├── README.md
│   ├── initial_scope.md
│   └── 00_analysis_catalog.md           ← Gate 1: what analysis InfraSure Insights should provide
├── 05_first_methodology_brief/          ← El Niño — the crucible
│   ├── README.md
│   ├── brief.md                          ← stub, awaiting domain knowledge dump
│   └── what_we_learned.md
└── research/                             ← raw research threads, archival
    ├── README.md
    ├── 01_platforms.md
    ├── 02_agentic_systems.md
    └── 03_methodology_traditions.md
```

**Read order for someone new**: README → `00_research_synthesis.md` → `01_principles.md` → `02_methodology_brief_shape.md` → `methodology_registry/README.md` → `methodology_registry/initial_scope.md` → `methodology_registry/00_analysis_catalog.md` → `05_first_methodology_brief/`. The `research/` folder is reference; rarely needed unless you want to dig into a specific learning.

## Operating principles for this lab (carry forward unless explicitly overridden)

1. **Research is reference, not template.** Pull learnings from existing systems but never let them constrain ambition. The bar is "we can do much better than anything that exists." If our menu is shaped by what's already out there, we've lost.
2. **Methodology before applied.** Encode the analytical worldview as structured methodology briefs first; applied insights are then a production line that runs on them.
3. **Substrate grounding is the moat.** If an insight could be written from public data alone, it's the wrong insight to publish. Every insight must be hard to produce without InfraSure.ai's specific data.
4. **LLM-led, human-reviewed.** LLMs do the cross-dimensional synthesis; humans review/suggest/edit. Not the other way around. LLMs are *better* than humans at this kind of multi-dimensional synthesis at scale; the human role is editorial judgment.
5. **Architecture won't be right on the first pass.** But the philosophy + principles need to be there so each iteration converges on a real system, not drifts.
6. **Lives here until it earns its way out.** Graduates to `riorg/dimensions/insights/` + `web/src/app/insights/` only when the design is stable.

## Current build sequence

The first practical move is **not** a full in-house insight agent and not an email/outreach system. The platform already has a typed data-tool layer through Ask/MCP. The missing foundation is the **methodology resource layer**: structured resources that tell the model how to reason with the data.

1. **Data MCP is the starting substrate.** Existing typed tools retrieve platform data: plants, projects, news facts, generation, financials, companies, offtakers, and related context. Some tool gaps may remain, but the pattern is already proven enough for lab testing.
2. **Build a methodology registry v0.** Start with 1-3 schema-valid, MCP-readable methodology resources. The analysis catalog defines which insight families deserve resources; the resources then define required inputs, reasoning steps, allowed claims, confidence rules, caveats, actor framing, staleness signals, and example outputs.
3. **Test MCP + methodology resources in Claude.** This is the lab loop. The question is: when Claude has both the platform data tools and a methodology resource, can it produce a useful, grounded applied-insight draft?
4. **Then split into two parallel tracks.**
   - **In-house architecture**: build the controlled API/orchestrator path for scale: LLM calls, retrieval plan, trace capture, validation gates, persistence, review queue, batch production.
   - **Activation/outreach**: use the same validated insight outputs to test platform cards, account context, and informative email drafts. This does not wait for the full in-house architecture, but it should consume validated insight objects rather than raw prompts.

## Caveats for the current stage

- Do not call this a methodology database yet. Start with a small registry and let the schema harden under real examples.
- Do not create a generic `software/` folder before the resource shape proves itself. If code prototypes become useful, they can live under `methodology_registry/software/` or `software/` later, but the first artifact is the resource layer.
- Methodology resources are not essays. They are agent-operational objects: what to retrieve, how to reason, what not to claim, when to downgrade confidence, and how to cite.
- MCP + Claude is the prototype environment, not the production architecture. It validates the reasoning shape before we spend engineering time on orchestration.
- Activation and outreach should run in parallel after the first MCP + methodology test, but they must not contaminate the methodology itself. The methodology is analytical first; emails are renderings.

## Context inputs and activation bridge

The methodology registry consumes context from several places:

| Context source | What it contributes | How insights use it |
|---|---|---|
| Platform data MCP | Typed access to plants, projects, news facts, generation, financials, companies, offtakers | Retrieval substrate for grounded claims |
| `riorg/dimensions/context/` | Wikipedia summaries, external links, generated plant descriptions | Background context and entity summaries; useful but not a substitute for claim grounding |
| `contacts/` lab | Companies, owner/developer relationships, offtakers, PPAs, future people/account layer | Actor and account context for activation/outreach |
| `news_details_spike/` + news substrate work | Extracted facts, event signals, corroboration patterns | Event and evidence layer for applied insights |
| `index_analysis_lab/` | Resource, pricing, revenue, and market-value evidence | Quantitative inputs for market/financial methodologies |

Step 4 has two parallel paths after the first MCP + methodology test:

1. **In-house architecture inside the lab/platform** — turn the manual MCP + Claude loop into a controlled orchestrator with trace capture, validation, persistence, and review.
2. **Activation/outreach** — use validated insight objects to create platform cards, account context, and informative emails. This path should lean heavily on `contacts/`, but it should consume insights rather than define them.

## What's queued next

- A new "analysis" principles file in `business/principles/` (technical + philosophical level), at the same authority level as the existing scalability / SEO / etc. principles. The risk frame from the initial discussion (scope creep into a weak content site, quality drift, LLM over-authoring, maintenance debt) becomes principle-level commitments, not loose flags.
- First methodology registry resource — use El Niño / ENSO as the crucible, because it stress-tests external inputs, regional crosswalks, asset fan-out, confidence, caveats, and actor-specific framing.
