# 02 - Analysis Catalog

> **Status**: v0 catalog, deepened 2026-06-05.
>
> **Purpose**: define the kinds of intelligence InfraSure Insights should support before individual methodology resources are written.
>
> **Grounded in**: live InfraSure MCP output, 2026-06-05 — every "real example" below is a pulled entity, not invented.

## Why This File Exists

The methodology registry should not start from interesting topics. It should start from the questions InfraSure should be able to answer better than a generic LLM, a generic news summary, or broad market commentary.

```text
GATE 1: What kind of intelligence should InfraSure produce?
        |
        v
        decides which methodology resources deserve to exist
```

Gate 2 is handled by the methodology resource standard (`docs/03`) and the context/data map (`docs/04`).

## Core Position

InfraSure Insights should focus on **infrastructure decision intelligence**, not market commentary.

The unit is:

```text
a grounded change, exposure, opportunity, or constraint
tied to specific assets, companies, regions, offtakers, or counterparties
```

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

## Analysis Families

| Family | Question It Answers | Real example (2026-06-05) |
|---|---|---|
| **Exposure** | Who or what is exposed to this external condition? | CA solar fleet (36,843 MW) vs ENSO winter-irradiance shift; Desert Sunlight 300 (`57993`) CF 0.24 |
| **Performance** | Is this asset behaving differently than comparable assets? | Desert Sunlight 300 CF vs its peer set (Solar Star 1 `58388` 318 MW; Myrtle `66910` 313 MW) |
| **Commercial** | Who buys/sells power, and what does that imply? | Desert Sunlight → Pacific Gas & Electric, 28 contracts, PPA $160.95/MWh to 2039 |
| **Development Risk** | Which projects are likely delayed, stuck, or fragile? | Corby battery (`CAISO-1270`) permit extension — `R01_COD_DELAY` + `R11_REGULATORY` |
| **Portfolio Strategy** | What does this company's asset base imply? | NextEra/Clearway CA-solar concentration (McCoy 500.6 MW, Genesis 250 MW, …) |
| **Market Context** | How does regional structure affect asset economics? | Desert Sunlight on SP15 hub, node `DSRTSN_2_DS2BX2-APND`; curtailment risk `R06` |
| **Event Translation** | What does this news / weather / queue event mean for assets? | New Colgate penstock failure: 315 MW hydro (`454`) offline, ~300K homes, 1–2 yr |

## V0 Priority

V0 starts with:

```text
Exposure -> consequence -> actor relevance
```

Reasons:

- It matches InfraSure's product promise: forward-looking, localized, asset-specific intelligence.
- It forces external condition to asset mapping.
- It naturally consumes MCP data tools and methodology resources.
- It produces actor relevance for the later contacts/outreach overlay.
- It is narrow enough to test with one resource.

The first resource should be:

```text
El Niño / ENSO exposure
  -> one region or market
  -> solar regional fleet or owner portfolio
  -> actor relevance
```

## Which Tools Feed Which Family

Every family is grounded by a different slice of the MCP surface (full tool reference: `docs/learning/01_mcp_basics.md`):

```text
Exposure          search_plants + aggregate  ->  get_plant (location, CF, region)
Performance       get_plant.similar / nearby  +  compare_entities
Commercial        get_plant.offtakers  +  find_by_extracted_fact(buyer / ppa_type)
Development Risk   search_projects  +  get_project  +  get_news_extracted (milestone, delay)
Portfolio Strategy plants_by_owner  +  aggregate(group_by=owner)
Market Context    get_plant.grid (LMP node, hub)  +  pricing context  +  news risk_factors
Event Translation  search_news (lane=CONSTRAINT/COMMITMENT)  +  get_news_extracted
```

## Family Detail

### Exposure

**Question:** Who or what is exposed to this external condition?

Inputs: external condition (climate regime, hazard, policy, market rule, weather) · asset scope (plant / project / fleet / portfolio / region) · mechanism · actor context.

```text
Real: aggregate(plants, group_by=state, metric=total_capacity, filter=fuel:SUN) -> CA 36,843 MW.
      Drill get_plant(57993): seasonal CF (summer ≈0.38 / winter ≈0.13) is the baseline ENSO perturbs.
Claim type: directional exposure. Block exact LMP / plant-output forecasts.
```

This is the v0 family — see `resources/weather_and_climate/el_nino_enso/`.

### Performance

**Question:** Is this asset behaving differently than comparable assets?

Turns observed operating data into peer-relative claims (underperformance after controlling for region, fuel, vintage, capacity).

```text
Real: get_plant(57993).similar -> Solar Star 1 (58388, 318 MW), Myrtle (66910, 313 MW), BT Hickerson (66903).
      Compare CF / generation against that peer set rather than against an absolute bar.
Claim type: statistical / peer-relative. Control for region + vintage before asserting under/over-performance.
```

### Commercial

**Question:** Who buys or sells power, and what does that imply?

Connects assets to companies, owners, offtakers, PPAs, and counterparty concentration.

```text
Real: get_plant(57993).offtakers -> Pacific Gas & Electric, 28 contracts, energy_ppa_escalating, to 2039-12-16.
      find_by_extracted_fact(developer="primergy solar") -> plants 63352/66625/66391 with source + confidence.
Claim type: factual (FERC EQR / resolved facts). Note coverage is partial — omit where absent, don't infer.
```

### Development Risk

**Question:** Which projects are likely delayed, stuck, or fragile?

Combines queue status, development milestones, company context, and news/event facts.

```text
Real: search_projects(state=CA, technology=Solar) -> multi-GW Solar+Battery (DARDEN CAISO-1949, 2,365 MW; UMBRIEL; WINGTIP).
      search_news CONSTRAINT -> Corby (CAISO-1270) permit extension: risk_factors R01_COD_DELAY + R11_REGULATORY.
      ⚠ developer is null across these queue rows today — a coverage gap to flag, not paper over.
Claim type: multi-signal risk. Name the signals; don't assert cancellation from one permit notice.
```

### Portfolio Strategy

**Question:** What does this company's asset base imply?

Rolls asset-level signals into owner, developer, investor, or offtaker portfolio views.

```text
Real: plants_by_owner("NextEra", fuel=solar, state=CA) -> McCoy (58462, 500.6 MW), Genesis (57394, 250 MW), Blythe II/III.
      Pair with aggregate(group_by=owner) to size concentration. Note owner ≠ operator (Clearway owns, NextEra operates).
Claim type: concentration / exposure rollup. Resolve the ownership layer before naming "who is exposed".
```

### Market Context

**Question:** How does regional structure affect asset economics?

Translates pricing, curtailment, congestion, revenue, and grid context into asset implications.

```text
Real: get_plant(57993).grid -> hub TH_SP15_GEN-APND, node DSRTSN_2_DS2BX2-APND, 230 kV, CAISO/WECC.
      News risk_factors R06_CURTAILMENT mark curtailment-exposed contexts.
Claim type: caveated economic implication. Pricing coverage varies by region — keep directional where thin.
```

### Event Translation

**Question:** What does this event mean for assets?

Maps storms, policy changes, queue updates, regulatory changes, or market events into entity-specific implications.

```text
Real: search_news(state=CA, lane=CONSTRAINT) -> New Colgate Powerhouse penstock failure (plant 454, 315 MW hydro,
      Yuba Water Agency): ~300K homes affected, 1–2 yr repair, risk_factors R03_RESOURCE + R06_CURTAILMENT.
Claim type: event → asset/owner implication. Cite the article + as_of; don't extrapolate grid-wide price effects.
```

## Common Q&A Grammar

Every methodology resource should be able to answer:

```text
1. What changed, or what condition exists?
2. Which assets / regions / companies / offtakers are in scope?
3. What mechanism connects the condition to infrastructure outcomes?
4. What can InfraSure claim with confidence?
5. What is directional, caveated, or not publishable?
6. Who should care, and why?
7. What should be watched next?
```

## What This Rules Out

Do not prioritize:

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

If the answer needs no InfraSure entity, ID, or field to stand up, it is commentary — not a candidate for a methodology resource.
