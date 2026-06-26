---
name: offtaker-concentration
description: >-
  Draft a grounded, FACTUAL offtaker-concentration / merchant-exposure insight for a scoped set of renewable
  assets. Use when a user asks who buys the power, how concentrated a region/owner is in one PPA counterparty,
  or how much of a fleet is merchant/uncontracted — e.g. "which plants sell to Amazon," "how concentrated is
  our book in one offtaker," "how much of ERCOT solar is merchant." Resolves the named-buyer book via
  find_by_extracted_fact(buyer=…), VERIFIES each plant's news_extracted.buyer (the slim offtakers array is null —
  the resolved FACT is the grounding), routes to the seller/owner, and reports the merchant tail from the NULLs.
  Never produces a re-contracting/merchant price, a counterparty default probability, an inferred offtaker on a
  null, or a sum across look-alike owner names.
---

# Offtaker Concentration & Merchant Exposure

You are acting as an **InfraSure Insights analyst**. Connect a named offtaker (or a region/owner book) to a scoped asset set and produce **one grounded applied insight**. This is a **FACTUAL** claim — who buys the power, how concentrated, how merchant — not a directional forecast. Ground every material claim on the resolution layer, cap confidence at resolved-fact quality + coverage, refuse the price / credit / inferred-offtaker overclaims.

> Published form of the `offtaker_concentration` package; mechanism + citations live in the bundled `knowledge.md`. Slug `offtaker_concentration` · family `commercial` · domain `commercial`. The first FACTUAL (non-directional) resource.

## When to use / not use

- **Use** for: who buys a plant's/region's output; how concentrated a book is in one offtaker (count + MW); how much is merchant/uncontracted; the seller/owner behind a contracted book; who should care.
- **Do not use** for: a re-contracting or merchant $/MWh, a counterparty default probability / credit rating, an inferred offtaker on a null field, a look-alike-owner sum, or outreach copy before validation. Those are blocked.

## How to run it

```text
1. FRAME    Declare the claim type FACTUAL. Pick ONE anchor: (a) a named offtaker, OR (b) one region/owner book.
2. RESOLVE  find_by_extracted_fact(field="buyer", value="<offtaker>")  → entity_ids + source + as_of + confidence.
3. VERIFY   get_plant(<id>).news_extracted.buyer per material entity → confirm the buyer; read confidence + n_articles.
            ⚠ The slim `offtakers` array is NULL for corp PPAs — the resolved FACT is the grounding, not the empty array.
4. SELLER   get_plant.ownership.canonical_owner → route it; FLAG any parent look-alike split (don't sum look-alikes).
5. SIZE     Count verified plants + sum MW ACROSS VERIFIED ENTITIES ONLY; keep operating/queue/acquisition distinct.
6. MERCHANT (regional) search_plants(fuel, state) → a plant with NO resolved buyer = merchant tail. Report the NULL as-is.
7. ASSEMBLE  condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. GATE     Cap confidence at resolved-fact quality + coverage; BLOCK the $ / credit / inferred-offtaker / look-alike sum.
```

## Mechanism (one line; full detail in `knowledge.md`)

**Revenue = contracted (PPA price) + merchant (market price)**; concentration in one offtaker (counterparty-credit + tenor risk) and heavy merchant exposure (merchant-price risk) are the two tails of one axis; a PPA expiry rolls contracted → merchant (re-contracting risk). This resource grounds the **structure** (who / how concentrated / how merchant); the **level** ($/MWh, default odds, DSCR) is model-owned and blocked.

## Allowed claims

- Factual named-offtaker concentration: N verified plants / ~X MW resolved to one buyer, each sourced.
- Factual merchant tail for a region/owner: M plants / ~Y MW with NO resolved offtaker (null reported as-is).
- Seller / owner routing behind a contracted book, with the look-alike-split caveat.
- Qualitative re-contracting / merchant / counterparty-concentration RISK framing (directional, no number); monitoring recs.

## Blocked claims

- Re-contracting / merchant $/MWh forecast · counterparty default probability / rating.
- Inferring an offtaker into a null · summing look-alike owner names · `offtakers:null` read as "no PPA" without the buyer fact.
- A deal_value used as a PPA price (field noise) · national-from-one-book · outreach before validation.

## Confidence

Split **per-part**, capped at resolved-fact quality + coverage: a buyer resolved from MULTIPLE sources / high `n_articles_supporting` + per-plant VERIFY → *factual/high* (the named concentration); a single thin source (conf ~0.7, n=1) or partial coverage → *medium* (holds for the verified subset; the book may be larger); the qualitative risk framing → *low* (directional, no number). `Blocked` when a $/price/default-probability is requested, a buyer would be inferred into a null, or look-alikes would be summed.

## Output format

```text
## Applied Insight Draft
### Claim / Scope / Mechanism / Source References / Confidence / Caveats / Actor Relevance / Review Trace / Gaps
```

Every material claim carries a source reference (substrate result with `as_of` + `confidence`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism, the resolution-layer fact basis, the two data hazards, the Amazon / ERCOT-merchant anchors, citations |
| `historical_context.md` | PPA/counterparty distress history; use as context only, never as proof a current buyer is risky |
| `examples/applied_insight_001.md` | the target output shape (the validated Amazon-book + ERCOT-merchant insight) |
| `data_requirements.md` | the full retrieval plan + known gaps (offtakers-null · partial coverage R5 · parent canonicalization R9) |
