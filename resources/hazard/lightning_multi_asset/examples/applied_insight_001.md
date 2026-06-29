# Applied Insight 001 — Lightning × Florida Solar+Storage Flash-Density Maximum (Echo River, NextEra/FPL)

> **Status**: VALIDATED 2026-06-29 against the live InfraSure MCP. Real entities / ids / `as_of` — no placeholders. Test record: `../test_runs/test_run_001.md`.

## Applied Insight Draft

### Claim
NextEra/FPL's **Echo River Solar** (EIA 62490; Suwannee County, FL; 104.5 MW solar + storage) sits in the **US cloud-to-ground flash-density maximum (Florida)** and is **directionally lightning-exposed** primarily through **(B) induced surge into inverters / transformers / battery (BMS) control electronics** — a **high-frequency, lower-per-event-severity, design-managed** exposure (cumulative component risk + design adequacy), **not** a catastrophe; **Medium-confidence exposure + mechanism**.

### Scope
```text
Anchor:   Echo River Solar (EIA 62490) — Suwannee County, FL — 104.5 MW — fuel_types [SUN, MWH] (solar + storage) — as_of 2026-06-29
Owner:    Florida Power & Light — NextEra Energy
Geography: north Florida — NLDN cloud-to-ground flash-density maximum (lat 30.296, lon -82.864)
Fleet:    search_plants(fuel="solar", state="FL", minMw=50) → FL solar fleet incl. Echo River (62490) +
          Sunshine Gateway (61763, Columbia Co, NextEra) — same flash-density band
```

### Mechanism
Cited `knowledge.md` (§1). **(B)** A nearby strike couples a fast transient into wiring → inverter / transformer / SCADA / **battery BMS** damage → component outage across the generation set, even without a direct hit — and Echo River, being **solar + storage** (fuel_types include MWH), carries exactly the inverter + BMS electronics this mechanism targets. **(A)** Direct strike is the dominant mechanism for **tall wind** in open terrain (cross-class — not this FL solar anchor). The defining frame: **high-frequency / lower-severity, managed by design** (SPDs, grounding, air termination) — cumulative component risk, not a single loss. **LPS / surge-protection status is not in the substrate.**

### Source References
```text
substrate · InfraSure search_plants(solar, FL, ≥50) · Echo River 62490 · 104.5 MW, Suwannee County, fuel_types [SUN,MWH], lat/lon 30.296/-82.864, owner NextEra · as_of 2026-06-29 · primary (siting + mechanism B substrate)
external  · NOAA/Vaisala NLDN flash-density climatology · Florida · US cloud-to-ground flash-density maximum · accessed 2026-06-29 · primary (geography)
```
> `get_plant(62490)` for inverter/BMS detail + monthly CF is the logged next drill; not required for the exposure + mechanism claim (and LPS status is not in the substrate regardless).

### Confidence
Per-claim-part. **Exposure + mechanism: Medium** — flash-density geography (NLDN, Florida) + resolved FL solar fleet + the direct-strike/induced-surge distinction stated + the solar+storage substrate making mechanism B concrete. **No realized lightning event pulled this run** (cumulative-exposure framing, not an event translation). **Any CF read: Low/blocked** (not drilled; would not resolve a component-level strike). **High is not reachable** on the substrate alone (would need a per-asset strike/maintenance record or a served strike-rate model with LPS status).

### Caveats
- **Two mechanisms distinct**: (B) induced surge here (solar + storage electronics); (A) direct strike is the tall-wind cross-class case.
- Frame as **high-frequency / lower-severity cumulative component risk + design adequacy**, NOT a catastrophe.
- **LPS / surge-protection status not in the substrate** — no per-asset adequacy claim; geographic flash-density exposure only.
- **Monthly CF cannot resolve a component-level strike** — never read a strike into the series.
- Lightning-frequency **trends are weakly attributable** — cap at directional.
- Dollar severity / payout not modeled (model-gpr).

### Actor Relevance
- **owner_operator (NextEra/FPL)** — SPD + grounding inspection/upgrade; inverter / transformer / BMS spares planning for cumulative strike attrition. *(platform_card, account_note)*
- **investor** — flash-density accumulation across the north-FL NextEra solar+storage fleet; cumulative O&M / availability drag. *(portfolio_note)*
- **lender** — cumulative availability / O&M drag (directional); equipment-breakdown insurance adequacy. *(account_note)*

### Review Trace
Checked against `blocked_claims`: no $ / EAL / payout; no forward strike rate / component-failure probability; no per-plant damage from CF; no single-cause CF; no LPS-adequacy claim; no national-from-regional; no outreach. Gate: **PASS** — directional, Medium.

### Gaps / Next Fixes
- No served **strike-rate model** (R12) — blocks per-asset strike rate / $; directional only.
- No **LPS / surge-protection-status** field — blocks per-asset adequacy; standing substrate gap.
- `iso=` not used; scoped by `state="FL"` (R1). `get_plant(62490)` drill deferred.

---

**See also**: `../test_runs/test_run_001.md` · `../knowledge.md` (direct-strike / induced-surge mechanisms + NLDN basis) · `../data_requirements.md`.
