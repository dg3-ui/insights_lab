# Applied Insight 001 — Sea Level Rise & Storm Surge × Gulf Coast Tidewater Nuclear (South Texas Project, Constellation)

> **Status**: VALIDATED 2026-06-29 against the live InfraSure MCP. Real entities / ids / `as_of` — no placeholders. Test record: `../test_runs/test_run_001.md`.

## Applied Insight Draft

### Claim
Constellation's **South Texas Project** (EIA 6251; Matagorda County, TX; 2,708.6 MW nuclear) is a **Gulf Coast tidewater asset directionally exposed to sea-level-rise + storm-surge coastal inundation** — through **(CHRONIC) baseline SLR eroding the cooling-intake/switchyard design flood basis over decades** and **(ACUTE) storm-surge inundation of the switchyard/intake during a storm** — a **Medium-confidence exposure + mechanism** read on the WATER side; the WIND side is the hurricane resource (do not double-count).

### Scope
```text
Anchor:   South Texas Project (EIA 6251) — Matagorda County, TX — 2,708.6 MW NUC — as_of 2026-06-29
Owner:    STP Nuclear Operating Co — Constellation Energy
Geography: Gulf Coast tidewater (Matagorda County), lat 28.795 / lon -96.0481
Fleet:    search_plants(fuel="nuclear", state="TX") → TX nuclear set; STP is the coastal/tidewater one
          (Comanche Peak 6145 = inland Somervell Co; "Project Matador Nuclear" 69798 = inland Carson Co, announced) — STP isolated as the tidewater anchor
```

### Mechanism
Cited `knowledge.md` (§1). **(CHRONIC)** relative SLR raises the mean water level → more frequent tidal flooding + erosion of the cooling-intake / switchyard **design flood basis** the plant was licensed to (decades; uninsurable creep). **(ACUTE)** a tropical storm pushes surge above the tide → switchyard / intake inundation during the storm (hours; insurable). The structural insight: **tidewater cooling siting concentrates exposure** in large, long-lived, hard-to-relocate capital — STP at 2,708.6 MW of coastal nuclear is exactly that. Both are governed by **site elevation — not in the substrate**.

### Source References
```text
substrate · InfraSure search_plants(nuclear, TX) · STP 6251 · 2,708.6 MW, Matagorda County (coastal), lat/lon 28.795/-96.0481, owner Constellation · as_of 2026-06-29 · primary (tidewater siting + scope)
external  · NOAA tide-gauge relative-SLR trends   · TX Gulf Coast · chronic relative-SLR signal (HIGH attribution) · accessed 2026-06-29 · primary (chronic geography)
external  · NOAA NHC SLOSH / FEMA coastal zones    · Matagorda reach · acute surge envelope · accessed 2026-06-29 · support (acute geography)
```
> `get_plant(6251)` for the cooling-intake detail, on-site substation, and exact coastal setback is the logged next drill; not required for the exposure + chronic/acute mechanism claim.

### Confidence
Per-claim-part. **Exposure + mechanism: Medium** — tidewater geography (Matagorda County, lat/lon) + resolved nuclear set + the chronic/acute distinction stated. **Chronic SLR trend: HIGH-attribution** as a regional signal (NOAA), though the per-site rate needs the nearest gauge. **No realized surge event pulled this run.** **Any CF read: Low/blocked** — irrelevant for the chronic horizon; cannot resolve an acute surge. **High is not reachable** on the substrate alone (no site elevation + no served SLR/surge model → no depth or year).

### Caveats
- **Chronic vs acute are distinct** — different horizons (decades vs hours) and financial logic (uninsurable creep vs insurable event). State which applies.
- Exposure is driven by **site elevation** (not in the substrate) — STP may be elevated/levee-protected; the claim is geographic, not a depth or inundation year.
- **WATER side only** — the wind cut-out / structural-damage side is `../hurricane_high_wind_wind/`; do not double-count.
- Chronic SLR is **uninsurable creep**, not a claim event — do not apply acute-event financial logic to it.
- Inundation **depth / year / forward surge probability** are blocked (model-gpr); dollar / decommissioning not modeled.

### Actor Relevance
- **owner_operator (Constellation)** — long-horizon cooling-intake design-basis review under a rising baseline; switchyard elevation; decommissioning-timeline implications for a tidewater nuclear unit. *(platform_card, account_note)*
- **investor** — tidewater accumulation + chronic SLR as a long-lived stranded-asset / residual-value consideration. *(portfolio_note)*
- **lender** — SLR horizon can exceed the debt tenor (directional); coastal-zone + surge-insurance adequacy. *(account_note)*

### Review Trace
Checked against `blocked_claims`: no $ / decommissioning / payout; no inundation year; no forward surge probability; no inundation depth; no single-cause CF; no wind double-count; no national-from-regional; no outreach. Gate: **PASS** — directional, Medium.

### Gaps / Next Fixes
- No **site-elevation / design-flood-basis** field — blocks depth + year; the standing substrate gap.
- No served **SLR/surge model** (R12) — directional only.
- `iso=` not used; scoped by `state="TX"` then isolated the coastal unit by county (R1).
- `get_plant(6251)` cooling-intake drill deferred.

---

**See also**: `../test_runs/test_run_001.md` · `../knowledge.md` (chronic/acute mechanisms + anchors) · `../hurricane_high_wind_wind/` (the WIND side) · `../data_requirements.md`.
