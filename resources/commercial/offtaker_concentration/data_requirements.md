# Data Requirements — Offtaker Concentration & Merchant Exposure

> **Status**: draft 2026-06-14. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked structural reference: `../hazard/hail_solar/data_requirements.md`. **The live state is in-substrate** (the resolution layer), not an external feed — the differentiator from the hazard/weather resources.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
SUBSTRATE   the named-offtaker book   -> find_by_extracted_fact(field="buyer", value="<offtaker>")   (GROUNDS — the reverse lookup)
SUBSTRATE   per-plant buyer fact      -> get_plant.news_extracted.buyer (+ seller, ppa_type, term)   (GROUNDS + VERIFY)
SUBSTRATE   capacity / status         -> search_plants / get_plant.total_capacity_mw, status         (materiality + sizing)
ACTOR       seller / owner            -> get_plant.ownership.canonical_owner                          (routes; exposes R9 split)
SUBSTRATE   merchant null signal      -> offtakers:null AND news_extracted.buyer absent               (the merchant-tail finding)
SUBSTRATE   region / grid             -> get_plant.regions.iso_rto / .grid                            (bounds a regional test)
KNOWLEDGE   mechanism + claim type    -> knowledge.md §1–§2                                           (cite, don't re-derive)
EXTERNAL    deal source article       -> the source_url already under the resolved fact               (cite; never re-grounds)
DESCRIPTIVE plant / company blurb     -> get_plant.context                                            (frames only — never grounds)
LOGIC       materiality, sizing rule  -> >=50 MW; sum verified-only; don't sum look-alikes            (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| Resolved buyer book | substrate | the named-offtaker concentration | `find_by_extracted_fact(buyer=…)` → ≥1 entity with source + as_of + confidence |
| Per-plant buyer fact | substrate | VERIFY each material entity | `get_plant.news_extracted.buyer` confirmed (read confidence + n_articles_supporting) |
| Capacity + status | substrate | materiality + conservative sizing | total_capacity_mw; operating/queue/planned kept distinct |
| Seller / owner | substrate / actor | route + R9 flag | `canonical_owner`; look-alike splits flagged, not summed |
| Region / grid | substrate | bound a regional merchant test | `regions.iso_rto` (e.g. ERCOT) where the anchor is a region |
| Merchant null | substrate | the merchant-tail finding | `offtakers:null` AND no `news_extracted.buyer` → report as merchant/unknown |

## "External" state — it is in-substrate

| Source | Use | Where |
|---|---|---|
| Resolution layer (resolved buyer fact) | the live counterparty state | `find_by_extracted_fact(buyer)` + `get_plant.news_extracted.buyer` |
| Deal-announcement article | the named source under the fact | the `source_url` already in the fact metadata — cite it, don't re-fetch to ground |

There is **no external feed to pull** (unlike NOAA for the hazard resources). The fact is resolved in-substrate; the analyst's job is to RETRIEVE + VERIFY it, not to introduce an outside number.

## Retrieval plan (the real call sequence — test 001, run 2026-06-14)

```text
1. RESOLVE:  find_by_extracted_fact(field="buyer", value="amazon")        → 12 entities (plants + queue, multi-ISO/fuel)
                                                                            also ran: value="google" (24), "georgia power" (3)
2. VERIFY:   get_plant(66240 Ragsdale / 66598 Baldy Mesa / 64543 Cedar Creek / 57449 Blue Creek / 68396 Sunstone)
             → confirm news_extracted.buyer = "Amazon" (conf 0.8–0.95); NOTE offtakers:null on every one (use the FACT)
3. SELLER:   get_plant.ownership.canonical_owner → EDP Renewables / AES / Freepoint / Avangrid / Pine Gate (sellers differ)
4. REGION:   search_plants(fuel="solar", state="TX", minMw=200)            → the big TX solar fleet (the merchant scan)
5. MERCHANT: confirm the largest TX solar (65855/65854/65853/68305) resolve NO buyer = merchant tail;
             contrast Hill Solar 1 (66912) → resolved to Google (Reuters, conf 0.9) within the same market
6. SIZE:     aggregate(plants, owner, total_capacity, filter={fuel:SUN,state:TX})  → CONFIRMED R9: "Intersect Power" 2,389.2
             AND "Intersect USA, LLC" 1,375.5 are separate groups — flag, do not sum
7. DRAFT:    assemble; cap confidence at resolved-fact quality + coverage; block $ / credit / inferred / sum
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `offtakers` array null | the slim `offtakers` field is null even where a PPA exists; the counterparty lives in `news_extracted.buyer` | ground on `find_by_extracted_fact(buyer)` + `news_extracted.buyer`, not the array; never read `null` as "no PPA" | populate/serve a first-class `offtakers` array from the resolution layer |
| Partial PPA-buyer coverage (R5) | the buyer fact resolves only where deal NEWS exists; most merchant + utility-bilateral plants are unresolved | report the null as merchant/unknown; OMIT, never infer; caveat coverage as partial | broaden PPA/EQR ingestion; a `is_merchant` vs `unknown` distinction |
| Parents not canonicalized (R9) | `aggregate(group_by=owner)` splits a parent across look-alike names — confirmed: Intersect Power 2,389.2 + Intersect USA 1,375.5 | name each group; flag the likely-same-parent; do NOT sum look-alikes into one book | a canonical parent crosswalk over `canonical_owner` |
| No reverse buyer→capacity rollup | can't ask "total MW resolved to Amazon" in one call (find_by_extracted_fact returns ids, not summed MW) | drill each id for capacity; sum verified-only; keep statuses distinct | a `group_by=buyer` aggregate over the resolution layer |
| `deal_value_usd` field noise | cross-tagged $ (a $16.9B Spain figure on a CA plant; an $83M acquisition mislabeled) | never use as a PPA price / verified figure; it is a $ field model-gpr owns anyway | resolution-layer precision pass on the $ fields |

Also log each to `../../docs/status/mcp_gaps.md` (gap · workaround · roadmap).

## Missing-data handling

| Missing input | Required action |
|---|---|
| No resolved buyer for the named offtaker | **Block** the named-concentration claim — cannot establish the counterparty (try a different buyer, or pivot to the merchant tail) |
| `news_extracted.buyer` absent on a plant | treat as **merchant/unknown**; do NOT infer the offtaker (omit-don't-infer) |
| Region cannot be resolved | downgrade, or switch to a resolvable region for the merchant scan |
| Owner unavailable / look-alike split | asset-level claim only; flag the split, do **not** sum look-alike owners |
| A $ / price / credit figure requested | **Block** — that layer is model-gpr; ship the factual structure only |
