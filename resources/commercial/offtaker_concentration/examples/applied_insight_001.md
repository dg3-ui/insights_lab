# Applied Insight 001 — Offtaker Concentration (Amazon US solar/storage book) + ERCOT/TX Merchant Tail

> **Status**: validated 2026-06-14 (test_run_001). Real entities / ids / `as_of` / `confidence` — no placeholders. Meets the applied-insight thin contract (`../../../docs/method/resource_standard.md`). Scope: one named offtaker's book (Amazon) + one region's merchant tail (ERCOT/TX solar). FACTUAL claim type.

## Applied Insight Draft

### Claim

Three parts, at different confidence:

1. **Named-offtaker concentration (factual)** — At least **12 InfraSure-tracked entities** (operating + queue, across PJM/CAISO/MISO/BPA and multiple fuels) carry a **resolved offtaker of Amazon** (`find_by_extracted_fact(buyer="amazon")`, as_of 2026-06-14). Five drilled and **VERIFIED** via each plant's `news_extracted.buyer`: **Ragsdale Solar (66240, MS, 100 MW, operating, conf 0.90)**, **Baldy Mesa Solar+Storage (66598, CA, 225 MW, conf 0.90)**, **Cedar Creek Solar (64543, DE, 114 MW, planned, conf 0.90)**, **Blue Creek Wind (57449, OH, 302 MW, conf 0.95)**, and **Sunstone Solar (68396, OR, 2,400 MW, planned — acquired from Pine Gate's bankruptcy, conf 0.80)**. The sellers **differ per asset** (EDP Renewables, AES, Freepoint, Avangrid, Pine Gate) — Amazon is the concentrating *buyer*, not a single owner relationship.
2. **Merchant tail (factual-by-absence)** — In **ERCOT/Texas**, the largest utility-scale solar plants carry **no resolved offtaker** — **Tehuacana Creek 1 (65855, 1,254.8 MW)**, **Rowdy Creek (65854, 1,050 MW)**, **Middlebrook Creek (65853, 912 MW)**, **Gigawatt Solar (68305, 773 MW)** all return `offtakers: null` and no `news_extracted.buyer` → a **merchant / uncontracted (or unresolved) tail**. Within the same market, **Hill Solar 1 (66912, TotalEnergies, 405 MW)** *is* resolved to **Google** (Reuters, conf 0.90, n=2) — the contrast is the point: the merchant tail is real, but the null is *unresolved*, not *proven-merchant*.
3. **Qualitative risk framing (directional)** — A book concentrated in one offtaker carries counterparty-credit + PPA-tenor (re-contracting) risk; a heavy merchant tail carries merchant-price risk. **No $/MWh, no default probability, no DSCR** is claimed — only the structure.

### Scope

(a) Amazon US solar/storage book (named offtaker), verified subset of 5 plants above; (b) ERCOT/Texas solar ≥ 200 MW (one region) for the merchant scan. FACTUAL claim type — confidence is resolved-fact quality + coverage, not probability.

### Mechanism

Revenue = contracted (PPA price) + merchant (market price). Concentration in one offtaker → counterparty-credit + tenor risk; heavy merchant exposure → merchant-price risk; a PPA expiry rolls contracted → merchant (re-contracting risk). Structure grounds here; the level is model-owned. (`knowledge.md` §1–§2.)

### Source References

```text
1. substrate · InfraSure find_by_extracted_fact(field=buyer, value="amazon") · 12 entities (plants + queue) · as_of 2026-06-14 · primary (the book)
2. substrate · InfraSure get_plant(66240).news_extracted.buyer · Ragsdale Solar (MS, 100 MW, operating) · buyer=Amazon, seller=EDP Renewables NA, ppa_type=physical, ppa_term_years=15, conf 0.90 (Solar Power World 2025-02-19) · as_of 2026-06-14 · primary (VERIFY)
3. substrate · InfraSure get_plant(66598).news_extracted.buyer · Baldy Mesa Solar+Storage (CA, 225 MW) · buyer=Amazon, seller=AES, conf 0.90; project_lifecycle.offtaker=Amazon n_articles=4 (Data Center Dynamics 2024-10-26) · as_of 2026-06-14 · primary (VERIFY)
4. substrate · InfraSure get_plant(64543).news_extracted.buyer · Cedar Creek Solar (DE, 114 MW, planned) · buyer=Amazon, seller=Freepoint Solar, conf 0.90 (Delaware Business Times 2022-04-20) · as_of 2026-06-14 · primary (VERIFY)
5. substrate · InfraSure get_plant(57449).news_extracted.buyer · Blue Creek Wind (OH, 302 MW) · buyer=Amazon, seller=Avangrid, conf 0.95 (ESG Today 2025-10-01) · as_of 2026-06-14 · support (cross-fuel breadth)
6. substrate · InfraSure get_plant(68396).news_extracted.buyer · Sunstone Solar (OR, 2,400 MW, planned) · buyer=Amazon, seller=Pine Gate, transaction_type=acquisition, conf 0.80 (Biz Journals 2026-01-12, n=2) · as_of 2026-06-14 · support (queue/acquisition — kept distinct from signed PPAs)
7. substrate · InfraSure search_plants(fuel=solar, state=TX, minMw=200) · Tehuacana 65855 (1,254.8), Rowdy Creek 65854 (1,050), Middlebrook 65853 (912), Gigawatt 68305 (773) · offtakers=null, no news_extracted.buyer · as_of 2026-06-14 · primary (the merchant tail)
8. substrate · InfraSure get_plant(66912).news_extracted.buyer · Hill Solar 1 (TX, TotalEnergies, 405 MW) · buyer=Google, conf 0.90 (Reuters 2026-02-09, n=2) · as_of 2026-06-14 · support (in-ERCOT contrast)
9. substrate · InfraSure aggregate(plants, owner, total_capacity, filter={fuel:SUN,state:TX}) · "Intersect Power" 2,389.2 MW AND "Intersect USA, LLC" 1,375.5 MW — SEPARATE groups · as_of 2026-06-14 · support (the R9 look-alike-split caveat, NOT summed)
```

### Confidence

**Per-part** (the claim grammar in action):
- *Amazon is the resolved offtaker on the 5 drilled plants* — **factual / high** (each VERIFIED via `news_extracted.buyer`, conf 0.90–0.95, multi-source on three of them; the slim `offtakers` array was null on all five — grounded on the resolved fact, not the array).
- *The book is at least 12 entities* — **medium** (the reverse-lookup count is exact, but coverage is partial and the entities mix operating / queue / acquisition; the true Amazon book is likely larger and not all are signed PPAs — Sunstone is an asset acquisition, conf 0.80).
- *The big ERCOT/TX solar plants are merchant* — **medium** (the null is real and consistent across the four largest, but a null is *unresolved*, not *proven-merchant* — coverage gap, not a confirmed merchant designation).
- *Re-contracting / merchant-price / credit risk* — **low** (qualitative, directional, no number).

### Caveats

- This is a **factual snapshot** of resolved counterparties, **not a price forecast** — no re-contracting or merchant $/MWh is claimed.
- **Coverage is partial.** The big TX solar nulls are reported as merchant/**unknown**, not back-filled — a null is never inferred into a buyer (omit-don't-infer).
- The slim **`offtakers` array was null on every plant drilled** — the grounding is the resolved `news_extracted.buyer` fact, not the empty array; `null` alone is not proof of "no PPA".
- **Owner parents are not canonicalized**: TX solar shows **"Intersect Power" (2,389.2 MW)** and **"Intersect USA, LLC" (1,375.5 MW)** as separate groups — likely the same parent; **flagged, not summed**.
- **Counterparty credit quality + merchant-price level are out of scope** (model-gpr) — only the concentration *structure* is claimed. The `deal_value_usd` field (e.g. a $16.9B Spain figure cross-tagged onto Baldy Mesa) was **not** used.

### Actor Relevance

- **Owner (e.g. AES on Baldy Mesa, EDP on Ragsdale)** — a single-offtaker revenue line (or a merchant tail) is a re-contracting + counterparty-credit axis; informs PPA-laddering + buyer diversification.
- **Investor** — concentration in one counterparty (Amazon across the book) is a revenue-quality / cash-flow-volatility axis for an equity position.
- **Lender** — PPA counterparty + tenor underpin contracted-cashflow coverage; a single-offtaker book or a heavy merchant tail is a DSCR-stability concern (directional — no DSCR number here).

### Review Trace

Checked against `blocked_claims`: no re-contracting / merchant $/MWh (✓); no counterparty default probability / rating (✓); no inferred offtaker on a null (✓ — TX nulls reported as merchant/unknown); no look-alike-owner sum (✓ — Intersect split flagged, not added); `offtakers:null` not read as "no PPA" without the buyer fact (✓); `deal_value_usd` not used as a PPA price (✓ — flagged as cross-tagged noise); not national (✓ — scoped to one buyer + one region). Each material fact carries a substrate `source_ref` with `as_of` + `confidence`; per-plant VERIFY done. Confidence split per-part and capped at resolved-fact quality + coverage. **Gate: PASS.**

### Gaps / Next Fixes

- The slim `offtakers` array is null even where a PPA exists → grounded on `news_extracted.buyer`; flagged (serve a first-class `offtakers` array from the resolution layer).
- No `group_by=buyer` rollup → had to drill each id for capacity and sum verified-only; logged.
- Parent canonicalization (R9) confirmed live (Intersect split) → flagged; a canonical-parent crosswalk would let the book be sized cleanly.
- Partial PPA coverage (R5) → the merchant nulls are "unknown", not "proven merchant"; an `is_merchant` vs `unknown` distinction would sharpen the merchant-tail claim.
