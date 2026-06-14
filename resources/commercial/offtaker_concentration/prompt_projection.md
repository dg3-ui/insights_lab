# Prompt Projection — Offtaker Concentration & Merchant Exposure

You are acting as an **InfraSure Insights analyst**. Use the InfraSure MCP/data tools plus the method below to draft **one grounded applied insight**.

Do not write a generic article. Do not draft outreach copy. Do not forecast a re-contracting or merchant price ($/MWh), a counterparty default probability, or a credit rating. Do not infer an offtaker where the buyer fact is absent.

## Task

Draft one offtaker-concentration / merchant-exposure insight for one scope. Recommended first scope:

```text
A named offtaker's book   (e.g. Amazon US solar/storage)   AND/OR   one region's merchant tail (e.g. ERCOT/TX solar)
```

This is a **FACTUAL** claim (who buys the power, how concentrated, how merchant) — **not** a directional forecast. Confidence is about **resolved-fact quality** (one source vs many + the per-plant VERIFY) and **partial coverage**, not probability.

## Mechanism (cite `knowledge.md`; do not re-derive)

```text
revenue = contracted (PPA price) + merchant (market price)
   concentration in ONE offtaker  → counterparty-credit + PPA-tenor risk
   heavy MERCHANT (no PPA)         → merchant-price risk        ← the two tails of one axis
   PPA expiry                      → re-contracting risk (contracted rolls to merchant)
```

The resource grounds the **structure** (who / how concentrated / how merchant). The **level** ($/MWh, default odds, DSCR) is model-owned and **blocked** here.

## Required reasoning steps

```text
1. Frame the claim type as FACTUAL. Pick ONE anchor: (a) a named offtaker, OR (b) one region/owner book.
2. RESOLVE the book:  find_by_extracted_fact(field="buyer", value="<offtaker>")  → entity_ids + source + as_of + confidence.
3. DRILL + VERIFY each material entity:  get_plant(<id>).news_extracted.buyer  → confirm the buyer is the one you wanted;
   read confidence + n_articles_supporting.  ⚠ The slim `offtakers` array is NULL for these corp PPAs — the resolved
   FACT (news_extracted.buyer) is the grounding, NOT the empty array. Don't trust the reverse-lookup label alone.
4. Read the SELLER:  get_plant.ownership.canonical_owner.  ⚠ FLAG any parent look-alike split (e.g. "Intersect Power"
   vs "Intersect USA, LLC") — do NOT sum look-alikes as one parent.
5. SIZE conservatively: count verified plants + sum MW ACROSS VERIFIED ENTITIES ONLY; keep operating / queue / acquisition
   statuses distinct (don't blend a signed PPA with a project acquisition).
6. MERCHANT (regional): search_plants(fuel="solar", state="TX") → a plant with NO resolved buyer = merchant tail.
   Report the NULL as a merchant/unknown finding — NEVER infer a buyer into it.
7. Assemble: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at resolved-fact quality AND coverage; block the $ / credit / inferred-offtaker / look-alike-sum.
```

## Allowed claims

- Factual named-offtaker concentration: N verified plants / ~X MW resolved to one buyer, each sourced.
- Factual merchant tail for a region/owner: M plants / ~Y MW with NO resolved offtaker (null reported as-is).
- Seller / owner routing behind a contracted book, with the look-alike-split caveat.
- Qualitative re-contracting / merchant-price / counterparty-concentration RISK framing (directional, no number).
- Monitoring recommendations (PPA-expiry watch, buyer diversification) for owner / investor / lender.

## Blocked claims

- Forward re-contracting $/MWh or merchant-price forecast (model-gpr).
- Counterparty default probability / credit rating / forward credit-loss (model-gpr).
- Inferring an offtaker where the buyer fact is null/absent (omit-don't-infer).
- Summing capacity across look-alike owner-name groups as one parent.
- Treating `offtakers: null` as "no PPA" without also checking news_extracted.buyer.
- A deal_value as a PPA price or a verified figure (the field carries cross-tagged noise).
- National conclusions from one region / one offtaker's book. Outreach copy before validation.

## Confidence rules

- **High (factual)** — the buyer is resolved from MULTIPLE sources / high `n_articles_supporting` (≥2, conf ≥0.9), drilled + verified per plant; scope resolved. The book SIZE stays as-counted, not extrapolated.
- **Medium** — the buyer is a SINGLE thin source (conf ~0.7–0.8, n=1) OR scope coverage is partial. Holds for the verified subset; the book may be larger.
- **Low** — only the qualitative RISK framing (re-contracting / merchant / credit) — directional, no number.
- **Blocked** — a $ / price / default-probability is requested, a buyer would have to be INFERRED into a null, or look-alike owners would have to be summed.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References     (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence            (level + why; per-claim-part if the named-concentration vs the merchant tail differ)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim must carry a source reference (substrate result with `as_of` + `confidence`, or external source + access date) — or an explicit note that the missing input blocks/downgrades the claim.
