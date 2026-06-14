# Applied Insight 001 — Severe Hail Exposure, ERCOT/Texas Solar (Fighting Jays)

> **Status**: validated 2026-06-14 (test_run_001). Real entities / ids / `as_of` — no placeholders. Meets the applied-insight thin contract (`../../../docs/method/resource_standard.md`). Scope: ERCOT/Texas solar ≥ 50 MW, anchored on a realized event.

## Applied Insight Draft

### Claim

Two parts, at different confidence:

1. **Realized event-translation** — A mid-March 2024 severe hailstorm in Fort Bend County, TX struck **Fighting Jays Solar (EIA 62945, 227.5 MW AC, single-axis-tracker c-Si, Copenhagen Infrastructure Partners)**. The impact is **observable in the substrate**: monthly capacity factor fell ~57–60 % year-over-year across the two seasons after the event (e.g. **Aug 2023 CF 0.372 → Aug 2024 CF 0.152**; Sep 0.339 → 0.140; May 0.289 → 0.115), then **recovered toward prior levels by mid-2025** (Aug 2025 CF 0.327) — a profile **consistent with** array damage followed by panel repair/replacement.
2. **Directional fleet exposure** — **Texas hosts the largest US utility-solar fleet (70,349 MW across 378 plants)** and sits in the **US severe-hail maximum** (SPC climatology). Single-axis-tracker c-Si plants without a fast hail-stow protocol carry directional hail-availability exposure. At least **~744 MW of additional solar sits within ~9 km of Fighting Jays** — Cutlass Solar I/II (110.9 + 202.8 MW) and Old 300 Solar (430 MW) — i.e. the same hail cell.

### Scope

ERCOT/Texas, solar ≥ 50 MW. Anchor: Fighting Jays (62945, Fort Bend County, ERCOT HB_HOUSTON, lat 29.35/−95.74). Same-cell fan-out: 66262, 66310, 64133 (`nearby_plants`, ≤ 8.6 km).

### Mechanism

Severe hail (≳1–2 in) → c-Si module glass/cell damage → output + availability loss; single-axis trackers can **hail-stow** to cut the impact footprint (the main mitigation lever). Geography: TX/southern Great Plains = US hail maximum. (`knowledge.md` §1, §3.)

### Source References

```text
1. substrate · InfraSure get_plant(62945) · Fighting Jays · capacity 227.5 MW AC, single-axis c-Si, county Fort Bend, ERCOT · as_of 2026-06-14 · primary
2. substrate · InfraSure get_plant(62945).generation · monthly capacity_factor (2022-07 … 2025-12) · as_of 2026-06-14 · primary (the observed dip + recovery)
3. substrate · InfraSure get_plant(62945).ownership · Copenhagen Infrastructure Partners Holding (DK); op. AP Solar 2 LLC · as_of 2026-06-14 · routes
4. substrate · InfraSure search_news(category=hazards,query="hail") · Fighting Jays hail event · hazard_type=hail, affected_area=Fort Bend County, operational_impact=damaged, event_date 2024-03-15/16 · VERIFIED vs PV Tech / Houston Chronicle / Fox News · primary (the event)
5. substrate · InfraSure aggregate(plants, state, total_capacity, fuel=SUN) · TX 70,349.3 MW (#1 state) · as_of 2026-06-14 · support (fleet size)
6. substrate · InfraSure nearby_plants(62945, solar) · Cutlass II 66262 (202.8 MW, 6.2 km) · Cutlass I 66310 (110.9 MW, 6.4 km) · Old 300 64133 (430 MW, 8.6 km) · as_of 2026-06-14 · support (same-cell fan-out)
7. external · NOAA SPC severe-hail climatology · TX/southern Great Plains = US hail maximum · accessed 2026-06-14 (cited, knowledge.md §3) · frames the geography
```

### Confidence

**Per-part** (the claim grammar in action):
- *Hail struck Fighting Jays* — **factual / high** (multi-source corroboration + an in-substrate hazards classification + a visible CF break).
- *The ~57–60 % CF drop reflects hail damage* — **medium** (observed, large, multi-season, and time-aligned to the event — but not proven single-cause; curtailment/weather also move CF).
- *Forward fleet hail exposure* — **low** (geographic/directional; no hail model, no forward probability).

### Caveats

- The observed CF decline is **consistent with** hail damage, **not** proof hail was the sole cause (ERCOT curtailment and weather also move solar CF).
- The hazards-news classification was **verified** against the underlying articles, not taken on the label.
- Hail is **sudden-onset and climatologically concentrated** — this is geographic exposure, not a dated forecast.
- **No dollar figure**: the news "multi-million-dollar" wording is a qualitative frame, not a modeled loss; EAL / insurance outcome is out of scope here.

### Actor Relevance

- **Owner (CIP)** — hail-stow protocol + hail-rated glass on the TX book; insurance deductible exposure; outage-recovery planning. The Fighting Jays recovery curve is the reference case.
- **Investor** — portfolio concentration in the TX hail maximum is a real availability/revenue downside axis.
- **Lender** — a hail-driven multi-season availability loss is a DSCR stressor on a financed TX solar asset (directional).
- **Developer** — siting + tracker hail-stow + module spec choices for queue-stage TX solar.

### Review Trace

Checked against `blocked_claims`: no $/EAL/payout asserted (✓ — kept qualitative + flagged); no forward probability (✓); no plant-level forecast (✓); no single-cause attribution (✓ — "consistent with"); not national (✓ — scoped TX). Each material number carries a substrate `source_ref` with `as_of`. Confidence split per-part and capped. **Gate: PASS.**

### Gaps / Next Fixes

- `search_plants(iso="ERCOT")` → `[]` (the R1 `iso`-filter gap, now confirmed beyond CAISO) — used `state="TX"`. Logged.
- No served hail peril-risk model → the $ / EAL / forward-probability layer is blocked; logged as `mcp_gaps` R12 (the directional-now-quantify-later wall).
- A county/geometry-aware `aggregate` would let us size "TX solar in the SPC hail maximum" directly (pairs with R8/R10).
