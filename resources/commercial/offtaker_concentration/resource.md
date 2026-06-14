# Offtaker Concentration & Merchant Exposure — Method (human-readable)

> **Status**: draft 2026-06-14. The human-readable companion to `resource.yml` (the structured operation) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. The **first `commercial`-domain resource** and the **first FACTUAL (non-directional) resource** — it stresses the standard's confidence/caveat machinery on a *fact* (who buys the power) rather than a forecast. Structural reference: `../hazard/hail_solar/`.

## What it answers (and what it refuses)

```text
ANSWERS   who buys the power (the named PPA counterparties) · how CONCENTRATED a scope is in one offtaker
          (count + MW of verified plants) · how much is MERCHANT (no resolved buyer) · who the seller/owner is · who cares
REFUSES   the re-contracting / merchant $/MWh · counterparty default probability / rating · an INFERRED offtaker
          on a null · a look-alike-owner SUM · national-from-one-book · outreach before the gate
```

## Scope

One named offtaker's book **OR** one region per test (test 001 = the **Amazon US solar/storage book** + the **ERCOT/TX merchant tail**) · solar / solar+storage (the buyer fact is fuel-agnostic — a corporate book spans fuels) · operating + queue + planned · actors: owner-operator · investor · lender.

## Mechanism (cite `knowledge.md`; do not re-derive)

A renewable asset's revenue is `contracted (PPA price) + merchant (market price)`. **Concentration in one offtaker** and **heavy merchant exposure** are the two tails of one axis — counterparty-credit + PPA-tenor risk on one side, merchant-price risk on the other; a PPA expiry rolls contracted → merchant (re-contracting risk). This resource grounds the **structure** (who, how concentrated, how merchant). The **level** ($/MWh, default odds, DSCR) is a separate model-owned layer (blocked).

## The new thing this resource tests

```text
HAZARD/WEATHER resources    confidence = DIRECTIONAL ODDS on a shifting baseline (non-stationarity caveat)
THIS resource (factual)     confidence = RESOLVED-FACT QUALITY (one source vs many + per-plant VERIFY)
                            + PARTIAL COVERAGE (the buyer fact resolves only where deal news exists)
```

No teleconnection, no non-stationarity. The discipline is the SAME (ground-or-downgrade, blocked_claims, cap-at-weakest) — the *failure modes* differ: here they are **inferring a null** and **summing look-alike owners**.

## Procedure (the real tool sequence)

```text
1. frame:    declare claim type FACTUAL; pick ONE anchor — (a) named offtaker OR (b) one region/owner book
2. resolve:  find_by_extracted_fact(field="buyer", value="<offtaker>")   → entity_ids + source + as_of + confidence
3. VERIFY:   get_plant(<id>).news_extracted.buyer  per material entity   → confirm the buyer; read confidence + n_articles
             ⚠ the slim `offtakers` array is NULL for these corp PPAs — the resolved FACT is the grounding, not the array
4. seller:   get_plant.ownership.canonical_owner   → route it; FLAG any parent look-alike split (R9) — do NOT sum
5. size:     count verified plants + sum MW ACROSS VERIFIED ENTITIES ONLY; keep operating/queue/acquisition distinct
6. merchant: (regional) search_plants(fuel, state) → a plant with NO resolved buyer = merchant tail (report the NULL as-is)
7. assemble: claim grammar; cap confidence at resolved-fact quality AND coverage; block the $ / credit / inferred / sum
```

## Allowed vs blocked claims

```text
ALLOWED  named-offtaker concentration (N plants / ~X MW, each sourced) · merchant tail (M plants / ~Y MW, null reported) ·
         seller/owner routing (with the look-alike caveat) · QUALITATIVE re-contracting/merchant/credit RISK · monitoring recs
BLOCKED  re-contracting / merchant $/MWh forecast · counterparty default prob / rating · INFERRING a buyer into a null ·
         SUMMING look-alike owner names · treating `offtakers:null` as "no PPA" without checking news_extracted.buyer ·
         a deal_value as a PPA price (field noise) · national-from-one-book · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**, capped at **resolved-fact quality** and **coverage**: a buyer resolved from **multiple sources / high `n_articles_supporting`** + drilled-and-verified → **factual/high** (the *named* concentration); a **single thin source** (conf ~0.7, n=1) or **partial scope coverage** → **medium** (holds for the verified subset; the book may be larger); the **qualitative risk framing** (re-contracting / merchant / credit) → **low** (directional, no number). Required caveats: factual snapshot not a price forecast · coverage partial → omit-don't-infer · parents not canonicalized (flag look-alike splits) · credit + price level are out of scope (model-gpr).

## Actor relevance

Owner (revenue concentration / merchant tail → PPA-laddering + buyer diversification) · investor (revenue-quality / cash-flow-volatility axis) · lender (PPA counterparty + tenor underpin contracted-cashflow coverage — DSCR-stability concern, directional). Relevance never distorts the method.

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + the Amazon-book / ERCOT-merchant anchors) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + the coverage/canonicalization gaps) · `examples/applied_insight_001.md` (the validated output) · `test_runs/test_run_001.md` (the live test record).
