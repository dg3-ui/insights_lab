# Knowledge — Offtaker Concentration & Merchant Exposure (cited mechanism library)

> **Status**: draft 2026-06-14. The stable "why" for `offtaker_concentration`. Unlike the hazard/weather resources, the live state is **in-substrate** (the resolution layer — `find_by_extracted_fact(buyer)` + `get_plant.news_extracted.buyer`), not an external feed. This is the **first FACTUAL (non-directional) resource**: the claim is *who buys the power and how concentrated*, resolved-fact quality, not a probability. Cite everything; descriptive blurbs never substitute for the resolved fact.

## 1 · The mechanism (commercial, not physical)

```text
a renewable asset's revenue = (contracted MWh × PPA price)  +  (merchant MWh × market price)
   → if ONE offtaker buys most of the output      → COUNTERPARTY-CONCENTRATION risk (one buyer's credit + one PPA's tenor)
   → if a large share is UNCONTRACTED (no PPA)     → MERCHANT-PRICE exposure (revenue rides the spot/forward market)
   → when a PPA EXPIRES                            → RE-CONTRACTING risk (the contracted slice rolls to merchant terms)
```

The revenue-risk axis is **the counterparty mix**: concentration in one buyer and heavy merchant exposure are the **two tails of the same axis**. The fact this resource grounds is the *structure* — who, how concentrated, how merchant. The **level** ($/MWh, default probability, DSCR) is a separate, model-owned layer (blocked here).

## 2 · Robustness & claim type

```text
who the named offtaker is (resolved buyer)     FACTUAL — most-cited-wins resolution; cap at source count + VERIFY
how many plants resolve to one buyer (count)   FACTUAL — a reverse-lookup over the resolution layer
summed MW of the verified subset               FACTUAL — but sum ONLY across drilled+verified entities
a plant is MERCHANT (no resolved buyer)        FACTUAL-BY-ABSENCE — the null is the finding; never infer a buyer in
the re-contracting / merchant PRICE            BLOCKED — model-gpr (no forward $ from the fact alone)
counterparty DEFAULT probability / rating      BLOCKED — model-gpr (credit is not in the resolution layer)
```

**This is not a directional resource.** There is no teleconnection, no odds-shift, no non-stationarity caveat. Confidence is about **resolved-fact quality** (one source vs many; the per-plant VERIFY) and **partial coverage** (the buyer fact is resolved only where deal news exists). That is the new thing test 001 checks: the resource_standard's confidence + caveat machinery, applied to a fact rather than a forecast.

## 3 · State / fact basis (in-substrate — the resolution layer)

- **The reverse lookup**: `find_by_extracted_fact(field="buyer", value="<offtaker>")` — returns every plant/project resolved to that buyer, each with `source_name`, `source_url`, `as_of`, `confidence`, `n_articles_supporting`. This is "THE DIFFERENTIATOR" (the tool docstring): no other public source exposes resolved-fact reverse lookup.
- **The per-plant fact**: `get_plant(<id>).news_extracted.buyer` (+ `.seller`, `.ppa_type`, `.ppa_term_years`). Carries the same provenance. **Always VERIFY here** — confirm the buyer is the one you wanted and read `confidence` + `n_articles_supporting`.
- **The merchant null**: a plant with **`offtakers: null` AND no `news_extracted.buyer`** has no resolved counterparty = merchant / uncontracted (or simply not-yet-resolved). Report the null as a *merchant-tail* finding; do **not** infer a buyer into it.
- **Coverage reality (2026-06-14)**: across every plant drilled for this resource the slim **`offtakers` array was null** — the resolved counterparty lived in `news_extracted.buyer`, not in `offtakers`. So `offtakers: null` alone is **not** proof of "no PPA"; the news-resolved fact is the grounding (this is a required `blocked_claim`).

## 4 · The two known data hazards (drive the caveats)

```text
PARTIAL COVERAGE (R5)   the buyer fact resolves where deal NEWS exists (corp PPAs, hyperscaler deals).
                        most merchant + utility-bilateral plants have NO resolved buyer. OMIT, never infer.
PARENT NOT CANONICAL    aggregate(group_by=owner) splits a parent across look-alike names — confirmed live:
(R9)                    TX solar shows BOTH "Intersect Power" (2,389.2 MW) AND "Intersect USA, LLC" (1,375.5 MW).
                        summing them as one parent is a BLOCKED claim — flag the split, don't add.
FIELD NOISE             news_extracted.deal_value_usd carries cross-tagged $ (e.g. a $16.9B Spain-investment figure
                        attached to a CA plant). NEVER use it as a PPA price or a verified deal figure.
```

## 5 · Region / asset-class crosswalk

```text
offtaker × CORP PPA (hyperscaler)   Amazon / Google / Meta buy a NAMED plant's output — high-confidence resolved buyer,
                                    often multi-source. A corporate book spans fuels + ISOs (note it, don't force a fuel).
offtaker × UTILITY bilateral        a utility (Georgia Power) buys output — resolved where deal news exists; thinner.
MERCHANT × ERCOT solar              the merchant tail is largest in ERCOT (energy-only market, weaker bilateral norms) —
                                    the big TX solar plants resolve NO buyer = merchant/unknown. The canonical merchant case.
```

## 6 · Canonical worked cases (the anchors — real, drilled 2026-06-14)

- **Named-offtaker concentration**: `find_by_extracted_fact(buyer="amazon")` → **12 entities** (plants + queue, multiple ISOs/fuels). Verified subset: **Ragsdale Solar (66240, MS, 100 MW, operating)**, **Baldy Mesa Solar+Storage (66598, CA, 225 MW)**, **Cedar Creek Solar (64543, DE, 114 MW, planned)**, **Blue Creek Wind (57449, OH, 302 MW)**, **Sunstone Solar (68396, OR, 2,400 MW, planned/acquired-from-bankruptcy)** — each confirmed via `news_extracted.buyer` (conf 0.8–0.95). See `examples/applied_insight_001.md`.
- **Merchant tail (ERCOT/TX)**: the largest TX solar plants — **Tehuacana Creek 1 (65855, 1,254.8 MW)**, **Rowdy Creek (65854, 1,050 MW)**, **Middlebrook Creek (65853, 912 MW)**, **Gigawatt Solar (68305, 773 MW)** — carry **no resolved buyer** = merchant/unknown. Within the same market, **Hill Solar 1 (66912, TotalEnergies, 405 MW)** *is* resolved to **Google** (Reuters, conf 0.9). The contrast IS the insight.

## 7 · Citations

```text
InfraSure resolution layer — find_by_extracted_fact(buyer) + get_plant.news_extracted   THE DIFFERENTIATOR (tool docstring)
Amazon book (verified)        ESG Today / Solar Power World / Data Center Dynamics / Delaware Business Times / Biz Journals
Hill Solar 1 → Google PPA     Reuters 2026-02-09 / Benzinga (conf 0.9, n=2)
merchant-market structure     ERCOT energy-only market design (industry/market literature — frames, never grounds a number)
```

---

**See also**: `data_requirements.md` (the retrieval plan + the coverage/canonicalization gaps) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the confidence + caveat contract this factual resource stresses) · `../_method/README.md` (the screen/segment/score skeleton this specializes).
