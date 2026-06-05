# 00 — Analysis Catalog

> **Status**: v0 draft, 2026-06-02.
>
> **Purpose**: define the kinds of intelligence InfraSure Insights should provide before we author individual methodology resources.

---

## Why this file exists

The methodology registry should not start from topics. It should start from the types of questions InfraSure is trying to answer.

Bad starting point:

```text
"Let's make an El Niño methodology."
```

Better starting point:

```text
"What kind of decision-quality improvement should an InfraSure user get
from an El Niño methodology that they cannot get from generic news or a
generic LLM answer?"
```

This file is Gate 1 for the methodology registry:

```text
GATE 1: What kind of intelligence should InfraSure produce?
        ↓
        decides which methodology resources deserve to exist
```

Gate 2 lives in the resource contract and context/data map: what evidence, logic, and tool access each intelligence type needs.

---

## Core position

InfraSure Insights should focus on **infrastructure decision intelligence**, not market commentary.

The unit is:

> A grounded change, exposure, opportunity, or constraint tied to specific assets, companies, regions, offtakers, or counterparties.

Generic commentary says:

```text
"El Niño may affect US weather patterns and electricity markets."
```

InfraSure Insights should say:

```text
"Given this climate-regime signal, these assets / companies / offtakers
in this region are exposed through this mechanism; here is what we can
claim, how confident we are, what caveats apply, and who should care."
```

The insight is useful only if it improves a decision:

- what to diligence
- what to monitor
- which asset or portfolio deserves attention
- which risk transfer or resilience action might matter
- which account should receive a targeted, informative note

---

## Analysis families

These are the initial families of methodology resources worth considering. They are not all v0 work; they are the map that keeps the registry from drifting into unrelated analytical essays.

| Family | Question It Answers | Example Insight |
|---|---|---|
| **Exposure** | Who or what is exposed to this external condition? | Which CAISO solar assets are exposed to ENSO-driven seasonal irradiance shifts? |
| **Performance** | Is this asset behaving differently than comparable assets? | Which plants underperform peers after controlling for region, fuel, and vintage? |
| **Commercial** | Who buys/sells power, and what does that imply? | Which owners have corporate offtaker concentration visible in FERC EQR? |
| **Development Risk** | Which projects are likely delayed, stuck, or fragile? | Which queue projects show multi-signal delay risk? |
| **Portfolio Strategy** | What does this company’s asset base imply? | Which owners are concentrated in a weather/market risk pocket? |
| **Market Context** | How does regional structure affect asset economics? | Which solar assets sit in regions with poor revenue realization or curtailment exposure? |
| **Event Translation** | What does this news/regulatory/weather event mean for assets? | A storm, policy change, or queue update affects which assets and why? |

---

## Family detail

### 1. Exposure

**Question:** Who or what is exposed to this external condition?

This is the v0 priority family. It is the closest match to InfraSure's front-page promise: forward-looking, localized, asset-specific risk intelligence.

Typical inputs:

- external condition: climate regime, hazard, policy change, market rule, weather event
- asset scope: plant/project/fleet/portfolio/region
- mechanism: how the condition affects infrastructure
- actor context: owner, operator, investor, lender, offtaker

Example questions:

- Which CAISO solar assets are exposed to ENSO-driven seasonal irradiance shifts?
- Which coastal thermal assets are exposed to hurricane outage risk?
- Which owner portfolios are concentrated in wildfire-prone solar regions?

### 2. Performance

**Question:** Is this asset behaving differently than comparable assets?

This family turns observed operating data into peer-relative analytical claims.

Example questions:

- Which solar plants underperform regional peers after controlling for capacity, vintage, and location?
- Which wind assets show unusual capacity-factor volatility?
- Which plants are materially below similar assets on revenue realization?

### 3. Commercial

**Question:** Who buys/sells power, and what does that imply?

This family uses companies/offtakers/PPAs to connect assets to commercial counterparties.

Example questions:

- Which owners have corporate offtaker concentration visible in FERC EQR?
- Which offtakers are linked to assets in exposed regions?
- Which assets have disclosed PPA relationships versus merchant exposure?

### 4. Development Risk

**Question:** Which projects are likely delayed, stuck, or fragile?

This family combines queue status, project metadata, news facts, development milestones, and company context.

Example questions:

- Which queue projects show multi-signal delay risk?
- Which developers have clustered projects stuck in late-stage interconnection?
- Which projects have news signals that disagree with their queue status?

### 5. Portfolio Strategy

**Question:** What does this company’s asset base imply?

This family rolls asset-level signals into a company or portfolio view.

Example questions:

- Which owners are concentrated in a weather or market-risk pocket?
- Which companies have a high-share exposure to one ISO, fuel, hazard, or offtaker type?
- Which portfolios look resilient because risk is diversified across regions/technologies?

### 6. Market Context

**Question:** How does regional structure affect asset economics?

This family translates grid, pricing, curtailment, and revenue context into asset implications.

Example questions:

- Which solar assets sit in regions with poor revenue realization?
- Which assets are exposed to congestion, curtailment, or nodal-basis pressure?
- Which regions have asset fleets whose economics depend on one fragile market assumption?

### 7. Event Translation

**Question:** What does this news/regulatory/weather event mean for assets?

This family maps external events into entity-specific implications.

Example questions:

- A policy change affects which projects and owners?
- A queue update changes which development-risk signals?
- A storm, heatwave, drought, or wildfire event affects which assets and portfolios?

---

## v0 priority

For v0, start with:

```text
Exposure → consequence → actor relevance
```

Reasoning:

- It matches the product promise.
- It forces external condition → asset mapping.
- It naturally consumes both MCP data tools and methodology resources.
- It produces actor relevance for the Phase 2 contacts/outreach overlay.
- It is narrow enough to test with one methodology resource.

The first resource should be:

```text
El Niño / ENSO exposure
  → one region or market
  → solar regional fleet or owner portfolio
  → actor relevance
```

---

## Common Q&A grammar

Every methodology resource should be able to answer this sequence:

```text
1. What changed, or what condition exists?
2. Which assets / regions / companies / offtakers are in scope?
3. What mechanism connects the condition to infrastructure outcomes?
4. What can InfraSure claim with confidence?
5. What is only directional, caveated, or not publishable?
6. Who should care, and why?
7. What should be watched next?
```

This grammar is the bridge between the analysis family and the applied-insight object.

---

## What this rules out

The registry should not prioritize:

- broad energy thought pieces
- summaries that could be written without InfraSure data
- generic market predictions with no asset scope
- outreach copy that is not backed by a validated insight
- methodologies whose output cannot be grounded or caveated

The bar is:

```text
Could this insight materially improve how an owner, investor, lender,
developer, operator, or offtaker thinks about a specific asset, region,
portfolio, or counterparty?
```

If the answer is no, the method does not belong in v0.

