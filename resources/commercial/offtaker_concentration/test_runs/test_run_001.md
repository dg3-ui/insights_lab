# Test Run 001 — Offtaker Concentration (Amazon book) + ERCOT/TX Merchant Tail

> **Status**: 2026-06-14, **PASS** (with logged gaps). The manual MCP/Claude test record (`../../../docs/process/test_protocol.md`). This run authored + validated the `offtaker_concentration` resource against live InfraSure MCP data — the **first FACTUAL (non-directional) resource**, stressing the resource_standard's confidence/caveat machinery on a *fact* (who buys the power) rather than a forecast. (Raw transcript = this session.)

## Question tested

> "Who buys the power from Amazon's US solar/storage book, how concentrated is it, and how much of ERCOT/Texas solar is merchant (uncontracted)?" — one named offtaker's book + one region (ERCOT/TX) · one asset class (solar/storage).

## What the model retrieved (the real call sequence)

```text
1. find_by_extracted_fact(field=buyer, value="amazon")        → 12 entities (plants + queue); each w/ source + as_of + confidence
   (also probed: value="google" → 24 entities; "georgia power" → 3; "pacific gas" → 0)  (buyer-probe to find a real story)
2. get_plant(66240 Ragsdale)   → news_extracted.buyer=Amazon (conf 0.90, Solar Power World), seller=EDP, ppa_term=15;
                                  offtakers:null  ← KEY FINDING: grounding is the FACT, not the slim array
3. get_plant(66598 Baldy Mesa) → buyer=Amazon (conf 0.90); project_lifecycle.offtaker=Amazon n_articles=4; seller=AES;
                                  deal_value_usd=$16.9B tagged to a SPAIN article  ← VERIFY catch: cross-tagged $ noise
4. get_plant(64543 Cedar Creek)→ buyer=Amazon (conf 0.90), seller=Freepoint, planned
5. get_plant(57449 Blue Creek) → buyer=Amazon (conf 0.95, ESG Today), seller=Avangrid — WIND (cross-fuel breadth)
6. get_plant(68396 Sunstone)   → buyer=Amazon (conf 0.80), transaction_type=ACQUISITION (not a signed PPA) — kept distinct
7. search_plants(fuel=solar, state=TX, minMw=200) → big TX solar fleet; the top 4 carry NO resolved buyer = merchant tail
8. get_plant(66912 Hill Solar 1)→ buyer=Google (conf 0.90, Reuters, n=2) — the in-ERCOT contrast to the merchant nulls
9. aggregate(plants, owner, total_capacity, {fuel:SUN,state:TX}) → "Intersect Power" 2,389.2 AND "Intersect USA, LLC" 1,375.5
                                  = SEPARATE groups  ← R9 confirmed live: look-alike parent split, do NOT sum
```

## Accepted claims

- **Amazon is the resolved offtaker on 5 drilled+verified plants** (66240/66598/64543/57449/68396) — *factual/high* (each via `news_extracted.buyer`, conf 0.90–0.95 on four).
- **The Amazon book is ≥12 entities, multi-ISO, multi-fuel, mixed status** — *medium* (exact count; partial coverage; mixes operating/queue/acquisition).
- **The largest ERCOT/TX solar plants (65855/65854/65853/68305) are merchant/unknown** (null buyer) — *medium* (null is real + consistent, but *unresolved* not *proven-merchant*).
- **Hill Solar 1 (66912) → Google within the same ERCOT market** — *factual/high* (Reuters, conf 0.90, n=2) — the contrast.
- Seller routing (EDP/AES/Freepoint/Avangrid/Pine Gate), qualitative risk framing, actor relevance — all grounded/cited.

## Rejected / downgraded claims

| Claim attempted | Disposition | Why (failure taxonomy) |
|---|---|---|
| "Amazon's book re-contracts at $X/MWh" / "merchant tail earns $Y" | **blocked** | external-data: re-contracting / merchant price is model-gpr |
| "Amazon counterparty default probability is Z" | **blocked** | external-data: credit is not in the resolution layer (model-gpr) |
| "Tehuacana/Rowdy/etc. are *merchant*" (definitively) | **downgraded** → "no resolved buyer = merchant/unknown" | method: a null is unresolved, not proven-merchant (partial coverage R5) |
| Inferring a likely buyer for a null-buyer TX plant | **rejected** | method: omit-don't-infer — never back-fill a counterparty |
| Summing "Intersect Power" + "Intersect USA, LLC" as one parent book | **rejected** | MCP-tool: parents not canonicalized (R9) — flagged, not summed |
| Using `deal_value_usd`=$16.9B as the Baldy Mesa deal value | **rejected** | MCP-tool: cross-tagged field noise (a Spain figure) — caught by VERIFY; also a $ model-gpr owns |
| Reading `offtakers:null` as "this plant has no PPA" | **rejected** | MCP-tool: the array is null even where a PPA exists — must check news_extracted.buyer |

## Fixes applied (fail → fix)

- **`offtakers` array null everywhere** → grounding moved to `find_by_extracted_fact(buyer)` + `news_extracted.buyer`; baked a required `blocked_claim` ("null array ≠ no PPA") + a `data_requirements` gap row + a VERIFY step.
- **merchant-null temptation** → "merchant/unknown" language + omit-don't-infer caveat; confidence on the merchant tail capped at *medium*.
- **R9 look-alike split** → required caveat ("parents not canonicalized; flag, don't sum") + a `blocked_claim`; confirmed live with the Intersect split.
- **deal_value noise** → required `blocked_claim` ("a deal_value is not a PPA price; the field carries cross-tagged noise"); the $16.9B catch is the standing example.
- **mixed entity status** → procedure requires keeping operating / queue / acquisition distinct; Sunstone (acquisition) is flagged, not blended into a "signed PPA" total.

## Gaps logged (→ `../../../docs/status/mcp_gaps.md`)

- **`offtakers` array null** while the counterparty lives in `news_extracted.buyer` — serve a first-class `offtakers` array from the resolution layer.
- **No `group_by=buyer` rollup** — can't size a named-offtaker book's total MW in one call; drill + sum verified-only.
- **R9 (confirmed)** — parents not canonicalized (Intersect Power vs Intersect USA, LLC); needs a canonical-parent crosswalk.
- **R5 (partial PPA coverage)** — the buyer fact resolves only where deal news exists; an `is_merchant` vs `unknown` distinction would sharpen the merchant claim.
- **`deal_value_usd` field noise** — cross-tagged $ values; resolution-layer precision pass.

## Verdict

**PASS.** The resource produces a grounded, caveated, properly-split-confidence FACTUAL insight a vanilla LLM could not (it required the resolved-buyer reverse lookup, the per-plant `news_extracted.buyer` VERIFY, the seller chain, and the owner aggregate). The standout: **confidence here is resolved-fact quality + partial coverage, not directional odds** — the resource_standard's machinery (cap-at-weakest, per-part split, blocked_claims, required caveats) **transfers cleanly to a non-directional claim**, with two NEW failure modes (inferring a null buyer, summing look-alike owners) that the directional resources never hit. The `offtakers:null`-vs-`news_extracted.buyer` finding is the load-bearing discovery: the grounding is the resolved fact, never the empty array. Pattern validated and ready to reuse for the rest of the `commercial` family (e.g. owner-portfolio concentration, PPA-tenor / re-contracting-wall).
