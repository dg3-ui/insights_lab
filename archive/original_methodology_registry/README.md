# Methodology Registry

> **Status**: v0 lab scaffold, started 2026-06-02.
>
> **Purpose**: turn methodology briefs into operational resources that an MCP-enabled LLM can use to produce grounded applied-insight drafts.
>
> **What this is**: a small registry of structured methodology resources. Each resource tells the agent what the methodology covers, which data it needs, how to reason, what claims are allowed, when confidence should be downgraded, and how outputs should be reviewed.
>
> **What this is not**: a production database, an outreach system, or the in-house insight agent. Those come after the registry proves that MCP data tools plus methodology resources can produce useful insight drafts.

## Why this lives inside `insights_lab`

The methodology registry is core to the insights system. It should not be a sibling lab and it should not start as a generic software folder. The first risk is not lack of code; it is weak methodology shape. Code can come later once the resource contract is clear.

The current decision:

- Keep the registry under `.lab/insights_lab/methodology_registry/`.
- Keep resources human-editable and MCP-readable.
- Use Claude + existing MCP/data tools as the first test harness.
- Defer full API orchestration until we know the resource format works.

## Operating sequence

1. **Author one methodology resource.** Start with El Niño / ENSO because it forces external inputs, climate-region mapping, time windows, asset fan-out, and mixed confidence levels.
2. **Expose it to the MCP + Claude test loop.** The data tools are already the substrate. The methodology resource is the missing reasoning layer.
3. **Produce one thin applied-insight draft.** The draft should have claim, scope, methodology reference, source refs, confidence, caveats, and activation relevance. It does not need to be a polished platform page.
4. **Review what failed.** If the agent retrieved the wrong facts, the tool catalog may need a gap fix. If the agent reasoned vaguely, the methodology resource needs sharper operational fields.
5. **Only then expand.** Add 1-2 more methodology resources or begin a small in-house architecture prototype.

## Resource contract

Each methodology resource should eventually carry:

- identity: slug, title, version, snapshot
- scope: entity types, fuels, regions, lifecycle phase, actors
- required inputs: substrate dimensions and external sources
- reasoning procedure: ordered steps, inputs per step, outputs per step
- allowed outputs: claim types, units, sign conventions, confidence defaults
- caveats: what the method does not know or cannot infer
- confidence rules: when to keep, downgrade, or block a claim
- staleness signals: data or market events that force review
- examples: one or more target applied-insight shapes
- prompt projection: the minimal instructions that should be passed to the LLM

## Context inputs

Methodology resources should name their context dependencies explicitly. For v0, there are three distinct context types:

| Context type | Source | Use |
|---|---|---|
| Entity/substrate context | Ask/MCP tools over platform data | Ground claims about assets, projects, owners, offtakers, news facts, generation, financials, and market context |
| Descriptive context | `riorg/dimensions/context/` | Summaries, external links, and generated plant descriptions that help frame an entity, but do not by themselves validate analytical claims |
| Account/actor context | `contacts/` lab and ported companies/offtakers dimensions | Targeting and activation: who owns, develops, buys from, or is commercially exposed to the insight |

The methodology resource itself should remain analytical. Activation/outreach uses account context after the insight is valid; it should not change the methodology to make an email easier to write.

## First files

- `initial_scope.md` — the v0 work packet for the methodology registry.
- `00_analysis_catalog.md` — canonical map of the insight families InfraSure Insights should support.

Future resource files can either live directly in this folder or under `resources/` once there are enough of them to justify the subfolder.
