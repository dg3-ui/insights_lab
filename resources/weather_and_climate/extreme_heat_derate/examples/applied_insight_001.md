# Applied Insight 001 — Extreme-Heat Thermal Derate, ERCOT/Texas Solar (Aktina + South-zone cluster)

> **Status**: validated 2026-06-14 (test_run_001). Real entities / ids / `as_of` — no placeholders. Meets the applied-insight thin contract (`../../../docs/method/resource_standard.md`). Scope: ERCOT/Texas solar ≥ 50 MW, summer, directional. A weather × solar resource — the de-rate is second-order; confidence is LOW by design.

## Applied Insight Draft

### Claim

Under NOAA/CPC's summer-2026 lean toward **above-normal temperatures** across much of the lower-48 (issued ~mid-May 2026, accessed 2026-06-14), **ERCOT/Texas utility-scale solar carries directional thermal-derate exposure** — a **modest, peak-hour-concentrated efficiency loss**, not a capacity-factor collapse.

Two parts, both LOW confidence:

1. **Mechanism + magnitude (directional, modest).** On hot afternoons, PV **cell temperature rises tens of °C above the 25 °C STC reference**, and crystalline-silicon module efficiency falls at the **temperature coefficient of power (~ −0.3 to −0.45 %/°C)**; inverter/BOS thermal derating compounds it. The effect is **a few percent on the hottest hours** — real, but **second-order**. The substrate confirms the honesty boundary: **Aktina Solar (EIA 64927, 500 MW AC single-axis-tracker c-Si, Wharton County, ERCOT South)** ran **summer 2025 monthly CF ≈ 0.30 (Jun 0.296, Jul 0.302, Aug 0.307, Sep 0.302) vs winter ≈ 0.09–0.15 (Jan 0.094, Dec 0.150)** — i.e. **summer CF is HIGH, irradiance-dominated**. The de-rate lives *inside* those high-CF months as an intra-day, peak-hour shave; it is **invisible at monthly resolution**, so monthly CF is **not** the heat signal.

2. **Why it matters — peak coincidence (the real point).** The de-rate is at its maximum on the hottest afternoons, which **coincide with the ERCOT summer demand/price peak** (A/C load). So a modest de-rate **bites in the highest-value hours** — the exposure is about *when*, not *how much*. ERCOT is the sharpest US case: **Texas is the #1 US solar fleet (70,349.3 MW across 378 plants)** and a summer-peaking, scarcity-priced market. Aktina sits in **ERCOT South (HB_SOUTH / LZ_SOUTH)**, and at least **~1,127 MW of additional solar sits within ~17 km** — Danish Fields (66914, 600 MW), Red Tailed Hawk (66157, 360 MW), Flag City (65844, 167.3 MW) — the same heat/zone cluster.

### Scope

ERCOT/Texas, solar ≥ 50 MW, summer. Anchor: Aktina Solar (64927, Wharton County, ERCOT South HB_SOUTH/LZ_SOUTH, lat 29.12 / −96.28, single-axis c-Si, COD 2023, Tokyo Gas). Same-cell fan-out: 66914, 66157, 65844 (`nearby_plants`, ≤ 17.1 km).

### Mechanism

High ambient temperature → PV cell temp rises above 25 °C STC → c-Si module efficiency falls at the temperature coefficient (~ −0.3 to −0.45 %/°C) → a MODEST de-rate concentrated in the hottest afternoon hours; inverter/BOS thermal derating compounds it. The de-rate coincides with the ERCOT summer demand/price peak. (`knowledge.md` §1, §4; magnitude is stable PV physics, §6.)

### Source References

```text
1. external · NOAA CPC seasonal temperature outlook (+ summary coverage) · summer-2026 JJA above-normal lean across much of lower-48, highest confidence West; south-central/TX inside the broad lean · issued ~mid-May 2026, accessed 2026-06-14 · primary (the condition)
2. external · PV temperature-coefficient / NOCT references · c-Si power temp coefficient ~ -0.3 to -0.45 %/°C, STC 25 °C, NOCT 40–48 °C · stable physics, cited (knowledge.md §6) · frames the magnitude (modest)
3. substrate · InfraSure get_plant(64927) · Aktina Solar · 500 MW AC, single-axis-tracking c-Si (generators.solar), county Wharton, grid HB_SOUTH/LZ_SOUTH, regions.iso_rto=ERCOT · as_of 2026-06-14 · primary (the anchor asset)
4. substrate · InfraSure get_plant(64927).generation · monthly capacity_factor (2021-08 … 2025-12); summer-2025 CF Jun 0.296/Jul 0.302/Aug 0.307/Sep 0.302 vs winter Jan 0.094/Dec 0.150 · as_of 2026-06-14 · primary (the HONESTY proof: summer CF is HIGH)
5. substrate · InfraSure get_plant(64927).ownership · Tokyo Gas (Japan, publicly listed) via Tokyo Gas America; op. Hecate Energy Ramsey LLC · as_of 2026-06-14 · routes
6. substrate · InfraSure aggregate(plants, state, total_capacity, fuel=SUN) · TX 70,349.3 MW (#1 state; CA 36,843.1) · aggregate(… count) · TX 378 plants · as_of 2026-06-14 · support (fleet size)
7. substrate · InfraSure nearby_plants(64927, solar) · Danish Fields 66914 (600 MW, 13.2 km) · Red Tailed Hawk 66157 (360 MW, 13.7 km) · Flag City 65844 (167.3 MW, 17.1 km) · as_of 2026-06-14 · support (same heat/zone cluster)
```

### Confidence

**Per-part — both LOW** (the claim grammar in action):
- *Extreme heat de-rates ERCOT/TX solar in the hottest hours* — **low** (the mechanism is robust physics, but the magnitude is second-order and there is **no plant-level thermal model**; the temperature condition is a credible-but-modest above-normal *lean*, not the top-confidence region).
- *The de-rate matters because it coincides with the ERCOT summer peak* — **low** (logically robust and the strongest framing, but still directional — no hourly generation, no price/$ modeling here).
- Confidence is **capped at LOW by design** for this resource (`resource.yml.confidence_rules`); MEDIUM would require a strong dated lean *and* a clean baseline *and* still no plant-level magnitude.

### Caveats

- This is a **second-order efficiency effect — MODEST and concentrated in the hottest afternoon hours**, not a capacity-factor collapse.
- **Summer monthly CF is HIGH (irradiance-dominated)** — Aktina's summer-2025 CF ≈ 0.30 vs winter ≈ 0.09–0.15 — so the heat de-rate does **not** show up as a monthly-CF drop; monthly CF is **not** a heat signal. (The Feb-2025 CF 0.009 dip is a winter-storm outage, **not** heat — CF moves for many reasons.)
- **Directional, NOT a plant-level production forecast.** The exact %/MWh de-rate needs a plant-level thermal/cell-temp model (model-gpr — not modeled here).
- The materiality is **peak coincidence** (the de-rate bites at the ERCOT summer price/demand peak), **not** a large energy loss.
- **No dollar figure**, no forward heat probability/return-period; climate **non-stationarity** caps any trend claim.

### Actor Relevance

- **Owner (Tokyo Gas)** — thermal-aware design (inverter sizing, DC/AC ratio, ventilation) and O&M during heat waves; the peak-hour revenue exposure on a summer-peaking ERCOT South asset.
- **Investor** — portfolio concentration in a single summer-peaking, heat-prone market (ERCOT) is a downside on the most valuable hours, even if monthly CF stays high.
- **Lender** — P50/P90 generation assumptions should reflect thermal derating in the hottest hours; directional DSCR sensitivity on a financed ERCOT solar asset.
- **Offtaker** — a shaped / peak-hour PPA or merchant position feels the de-rate-at-peak most (where PPA context exists; Aktina's offtaker is not in-substrate here).

### Review Trace

Checked against `blocked_claims`: no per-plant %/MWh de-rate (✓ — kept directional + flagged); no $ / MWh (✓); no forward probability / return-period (✓); no plant-level forecast (✓); **no heat read off monthly CF** (✓ — explicitly used the high summer CF to *bound* the claim, not to size a loss); no single-cause attribution (✓ — Feb-2025 dip flagged as non-heat); not national (✓ — scoped ERCOT/TX). Each material number carries a substrate `source_ref` with `as_of` or an external source + access date. Confidence capped at LOW. **Gate: PASS.**

### Gaps / Next Fixes

- `search_plants(iso="ERCOT")` → `[]` (the R1 `iso`-filter gap, confirmed again) — used `state="TX"`, confirmed ERCOT via `get_plant.grid`/`.regions`. Logged.
- Climate-signal news channel empty (R11) — `search_news` does not index temperature outlooks → relied on the NOAA pull + substrate. Logged.
- No plant-level thermal / cell-temp model → the quantified %/MWh de-rate (and the $) are blocked; logged as `mcp_gaps` R12 (the directional-now-quantify-later wall).
- Substrate generation is **monthly**, not hourly — the intra-day peak-hour de-rate is not directly observable; reasoned from physics + peak coincidence. An hourly series (pairs with R12) would let us *show* the afternoon shave.
