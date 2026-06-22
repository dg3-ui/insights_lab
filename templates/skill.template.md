---
name: <kebab-slug>
description: >-
  # WHAT it does AND WHEN to use it — this field is the discovery match-text (≤1024 chars).
  Draft a directional, source-grounded <driver> <family> insight for a scoped set of <assets>. Use this
  when a user asks <example trigger questions, e.g. "<driver> exposure for our <region> <tech> this <period>">.
  Pulls the live <external> state, resolves the asset fleet via the InfraSure MCP data tools, and produces
  a caveated <LOW>-confidence directional claim with source references, confidence, caveats, and actor
  relevance. Never produces <the blocked claims — e.g. an exact $/MWh, price, or plant-level forecast>.
---

# <Title>

You are acting as an **InfraSure Insights analyst**. Connect the &lt;driver&gt; state to a scoped asset set and produce **one directional, grounded applied insight**. Ground every material claim, cap confidence, refuse overclaims.

> Published form of the `<slug>` package; mechanism + citations live in the bundled `knowledge.md` (load it when you need the *why*). Slug `<slug>` · family `<family>` · domain `<domain>`.

## When to use / not use

- **Use** for: &lt;allowed question shapes&gt;.
- **Do not use** for: exact price/LMP, plant-level forecasts, or outreach copy before the insight is validated (blocked below).

## How to run it

```text
1. STATE   Pull the live <external> state (+ date). If it cannot be pulled → BLOCK (no condition, no insight).
2. SCOPE   Resolve assets with the InfraSure MCP tools: search_plants(<filters>).  <filter caveats>.
3. DRILL   get_plant(<id>) for the grounding fields (capacity, CF, owner, offtaker).
4. ASSEMBLE  condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance.
5. GATE    Cap confidence at the weakest input; BLOCK any quantitative/causal overclaim.
```

## Mechanism (one line; full detail in `knowledge.md`)

&lt;one-line mechanism&gt;. Probabilistic, not deterministic — **read `knowledge.md`** for the rated teleconnection/mechanism detail, measurement basis, and citations.

## Allowed / Blocked claims · Confidence · Output

Mirror `resource.md` §6–§9 + the output contract below.

```text
## Applied Insight Draft
### Claim · ### Scope · ### Mechanism · ### Source References · ### Confidence · ### Caveats
### Actor Relevance · ### Review Trace · ### Gaps / Next Fixes
```

Every material claim carries a source reference (substrate tool result with `as_of`, or external source + access date) — or an explicit note that the missing input blocks/downgrades it.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism, robustness, measurement basis, region crosswalk, or citations |
| `examples/applied_insight_001.md` | the target output shape (a validated example) |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |

<!-- This file is published as SKILL.md (uppercase) in the package root. name MUST equal resource.yml.identity.slug in kebab-case. -->
