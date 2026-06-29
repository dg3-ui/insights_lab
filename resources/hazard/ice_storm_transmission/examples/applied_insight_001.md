# Applied Insight 001 — Ice Storm × South-Central Ice Belt / Oklahoma Wind + Delivery Corridor (Wagon Wheel, AEP/SWEPCO)

> **Status**: VALIDATED 2026-06-29 against the live InfraSure MCP. Real entities / ids / `as_of` — no placeholders. Test record: `../test_runs/test_run_001.md`.

## Applied Insight Draft

### Claim
AEP/SWEPCO's **Wagon Wheel Wind** (EIA 69224; Logan County, OK; 598.4 MW) sits in the **South-Central ice-storm belt** and is **directionally ice-storm-exposed** primarily as a **delivery-infrastructure** risk — through **(A) ice-load failure of the transmission it depends on**, **(C) stranding behind a downed line** (a physically undamaged turbine that cannot export), and secondarily **(B) blade icing → protective shutdown** — a **Medium-confidence exposure + mechanism** read; the loss is **grid-side, not plant-side**.

### Scope
```text
Anchor:   Wagon Wheel Wind (EIA 69224) — Logan County, OK — 598.4 MW — WND — as_of 2026-06-29
Owner:    Southwestern Electric Power (SWEPCO) — American Electric Power Company (AEP)  — AEP/SWEPCO also owns regional transmission (delivery-corridor relevance)
Geography: central Oklahoma — NOAA/SPIA South-Central freezing-rain ice belt (lat 36.153, lon -97.575)
Fleet:    search_plants(fuel="wind", state="OK", minMw=50) → OK wind fleet (Wagon Wheel 69224, Traverse 63479,
          Frontier II 62837, Diamond Spring 63327) — all delivery-dependent in the ice belt
```

### Mechanism
Cited `knowledge.md` (§1). **(A)** Freezing rain accretes on conductors/towers → load exceeds rating → conductor break / tower collapse → delivery outage (the PRIMARY hazard — capital-intensive rebuild). **(C)** A physically undamaged wind plant **cannot export** when the line/distribution network feeding the grid is down → revenue loss with **no physical-damage claim** — the defining property. **(B)** Blade icing → protective shutdown (temporary). Conductor/tower ratings + line geometry are **not in the substrate**, so the claim is geographic ice-belt exposure, not a per-span failure. Generation-side freeze (gas wellhead/pipeline) is `../extreme_cold_winter_storm/` — cross-reference, do not double-count.

### Source References
```text
substrate · InfraSure search_plants(wind, OK, ≥50) · Wagon Wheel 69224 · 598.4 MW, Logan County, lat/lon 36.153/-97.575, owner AEP/SWEPCO · as_of 2026-06-29 · primary (siting + scope)
external  · NOAA NWS freezing-rain climatology + SPIA Ice Accumulation Index · South-Central OK · ice-belt geography · accessed 2026-06-29 · primary (geography)
```
> AEP/SWEPCO owning both the wind plant and regional transmission is the delivery-corridor hook; `get_plant(69224).grid` for the interconnection + substation detail is the logged next drill (not required for the exposure + mechanism claim).

### Confidence
Per-claim-part. **Exposure + mechanism: Medium** — ice-belt geography (NOAA/SPIA) + resolved OK wind fleet + the delivery-infrastructure framing + the three claim types stated. **No realized ice-storm event pulled this run** (climatological exposure framing). **Any CF read: Low/blocked** — monthly CF cannot isolate an ice-storm outage from the winter seasonal pattern. **High is not reachable** on the substrate alone (no conductor/tower ratings + no served ice-load model).

### Caveats
- **Three mechanisms distinct**: (A) transmission ice-load failure [primary]; (B) blade icing → shutdown; (C) delivery stranding. State which applies.
- **Primarily a delivery-infrastructure hazard** — loss is grid-side; distinguish physical generation damage from delivery stranding.
- **Conductor/tower ratings + line geometry not in the substrate** — no per-span failure claim; geographic ice-belt exposure only.
- **Monthly CF cannot isolate an ice-storm outage** from the winter seasonal minimum — never read it in.
- Generation-side freeze (gas wellhead) is the **`extreme_cold_winter_storm`** resource — do not double-count.
- Freezing-rain **trends contested** — cap at directional. Dollar / restoration cost not modeled (model-gpr).

### Actor Relevance
- **owner_operator (AEP/SWEPCO)** — as a transmission owner: conductor/tower ice-load design + line de-icing + vegetation management + restoration spares; as a generator owner: delivery-path redundancy + blade de-icing; stranding awareness. *(platform_card, account_note)*
- **investor** — ice-belt accumulation including transmission holdings; delivery-stranding as a recurring revenue risk distinct from physical damage. *(portfolio_note)*
- **lender** — DSCR stress from a delivery-stranding or T&D-damage outage on a financed asset (directional). *(account_note)*

### Review Trace
Checked against `blocked_claims`: no $ / restoration cost / payout; no forward ice-load probability / return-period; no per-span or per-plant attribution from CF; no single-cause CF; no which-spans-collapsed; no generation-freeze double-count; no national-from-regional; no outreach. Gate: **PASS** — directional, Medium.

### Gaps / Next Fixes
- No **conductor/tower ratings or line geometry** — blocks per-span failure; standing substrate gap (the hazard is on the wires).
- No served **ice-load model** (R12) — directional only.
- Delivery-stranding has **no plant-side signal** — reasoned from corridor + downed-line mechanism, caveated as delivery-side.
- `iso=` not used; scoped by `state="OK"` (R1). `get_plant(69224).grid` drill deferred.

---

**See also**: `../test_runs/test_run_001.md` · `../knowledge.md` (three mechanisms + delivery-infrastructure framing) · `../extreme_cold_winter_storm/` (generation-side freeze) · `../data_requirements.md`.
