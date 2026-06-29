# Applied Insight 001 — Tornado × Southern Plains / Oklahoma Wind (Traverse, AEP)

> **Status**: VALIDATED 2026-06-29 against the live InfraSure MCP. Real entities / ids / `as_of` — no placeholders. Test record: `../test_runs/test_run_001.md`.

## Applied Insight Draft

### Claim
AEP's **Traverse Wind Project** (EIA 63479; Custer County, OK; 999 MW) sits in the **Southern Plains tornado-climatology corridor (Tornado Alley)** and is **directionally tornado-exposed** through **outright structural destruction (extreme wind + debris) of any turbines in a strike path** — a **catastrophic-but-localized** exposure (total loss if hit, low per-asset annual intersection), **not** a fleet-wide derate; **Medium-confidence exposure + mechanism**.

### Scope
```text
Anchor:   Traverse Wind Project (EIA 63479) — Custer County, OK — 999 MW — WND — Operating — as_of 2026-06-29
Owner:    Southwestern Electric Power (SWEPCO) — American Electric Power Company (AEP)
Geography: western Oklahoma — SPC Tornado-Alley touchdown-density corridor (lat 35.71, lon -98.83)
Fleet:    search_plants(fuel="wind", state="OK", minMw=50) → OK wind fleet (Traverse 63479, Wagon Wheel 69224,
          Frontier II 62837, Diamond Spring 63327) — all in the corridor
```

### Mechanism
Cited `knowledge.md` (§1). EF-scale winds + debris loading → blades snapped / nacelle / tower failure → **total loss of the turbines inside a path a few hundred meters wide** → long-lead rebuild. Defining property: **binary and narrow** — unlike a hurricane's wide fleet-wide field. At 999 MW spread across a large turbine count, a tornado would destroy a handful of turbines, **not** the nameplate — so the claim is geographic intersection risk, and **a total loss must NOT be annualized across the full 999 MW**.

### Source References
```text
substrate · InfraSure search_plants(wind, OK, ≥50)  · Traverse 63479 · 999 MW, Custer County, lat/lon 35.71/-98.83, owner AEP · as_of 2026-06-29 · primary (siting + scope)
external  · NOAA SPC tornado climatology            · western OK     · Tornado-Alley touchdown-density maximum · accessed 2026-06-29 · primary (geography)
```
> `get_plant(63479)` for sub-plant turbine layout + monthly CF is the logged next drill; it is **not** required for the exposure + mechanism claim (and sub-plant geometry is not in the substrate regardless).

### Confidence
Per-claim-part. **Exposure + mechanism: Medium** — corridor geography (SPC) + resolved OK wind fleet + the narrow-footprint framing stated. **No realized tornado event was pulled in this run** (the claim is climatological exposure, not an event translation). **Any CF read: Low/blocked** (not drilled; would not resolve a narrow partial-plant strike anyway). **High is not reachable** on the substrate alone (would need a post-event EF survey or a served tornado-hazard model).

### Caveats
- Damage is **binary and narrow** — do **not** annualize a total loss across the 999 MW nameplate.
- **Touchdown density is areal**, not a per-asset strike probability — a per-site return-period needs a hazard model, not the climatology.
- **Sub-plant geometry** (which turbines) is not in the substrate — no per-turbine destruction-extent claim.
- Tornado-frequency/intensity **trends are weakly attributable** — cap any trend at directional; treat a Dixie-Alley eastward shift as debated.
- Dollar severity / EAL / payout not modeled (model-gpr).

### Actor Relevance
- **owner_operator (AEP/SWEPCO)** — rapid-rebuild spares + wind-class / debris-resistant design margins for a low-probability total loss. *(platform_card, account_note)*
- **investor** — portfolio Tornado-Alley accumulation across the OK wind fleet; single-site total-loss tail vs geographic diversification. *(portfolio_note)*
- **lender** — single-asset total-loss tail on a financed project (directional); property/wind-insurance + deductible adequacy. *(account_note)*

### Review Trace
Checked against `blocked_claims`: no $ / EAL / payout; no forward per-asset strike probability / return-period; no per-plant damage from CF; no which-turbines-destroyed; no annualizing-across-nameplate (explicitly refused); no national-from-regional; no outreach. Gate: **PASS** — directional, Medium.

### Gaps / Next Fixes
- No served **tornado-hazard model** (R12) — blocks per-asset strike probability / $; directional only.
- No **sub-plant geometry** — blocks per-turbine extent; standing substrate gap.
- `iso=` not used; scoped by `state="OK"` (R1). `get_plant(63479)` drill deferred (not needed for this claim).
- `search_news` event corroboration not attempted this run — climatological exposure framing only.

---

**See also**: `../test_runs/test_run_001.md` · `../knowledge.md` (mechanism + narrow-footprint framing) · `../data_requirements.md`.
