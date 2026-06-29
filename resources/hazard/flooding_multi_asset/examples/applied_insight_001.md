# Applied Insight 001 — Flood Inundation × Gulf Coast / Texas Water-Sited Thermal (Sabine, Entergy)

> **Status**: VALIDATED 2026-06-29 against the live InfraSure MCP. Real entities / ids / `as_of` — no placeholders. Meets the applied-insight thin contract (`../../docs/method/resource_standard.md`). Test record: `../test_runs/test_run_001.md`.

## Applied Insight Draft

### Claim
Entergy's **Sabine** station (EIA 3459; Orange County, TX; 1,811.8 MW gas steam) is a **directionally flood-inundation-exposed, water-sited thermal asset** — sited on Sabine Lake / the Sabine River for once-through cooling, in the Gulf Coast riverine-and-coastal floodplain that Hurricane Harvey (Aug 2017) inundated — exposed through **(C) cooling-water-intake compromise** and **(A) inundation of its on-site 230 kV switchyard**; this is a **Medium-confidence exposure + mechanism** read, not a damage or dollar claim.

### Scope
```text
Anchor:   Sabine (EIA 3459) — Orange County, TX — 1,811.8 MW — 4× NG steam (1962–1979) — Operating — as_of 2026-06-29
Owner:    Entergy Texas — Entergy (publicly listed) — BlackRock 9.7% / Vanguard 8.7%
Grid:     MISO / SERC-Delta, 230 kV substation on-site (substation_operator Entergy)   ⚠ MISO, not ERCOT — East-TX Entergy
Cooling:  once-through, source = "Sabine Lake" / "Sabine River", brackish (BR)   → mechanism C substrate
Fleet:    search_plants(fuel="gas", state="TX", minMw=50) → resolved TX gas fleet; aggregate TX NG context
Floodplain fan-out (nearby_plants 3459): Orange County Advanced Power Station (66621, 0.7 km, 1,306 MW NG),
          Sabine River Operations (10789, 12.1 km, 594.9 MW NG) — same tidewater reach
```

### Mechanism
Cited `knowledge.md` (§1). **(C)** Floodwater / debris compromises the cooling intake, screens, or pump house of a water-sited thermal plant → derate or trip; **(A)** floodwater reaches the low-lying switchyard → de-energization → delivery outage. Sabine is the structural-insight case in the flesh: it sits **at** the water (Sabine Lake) for cooling, which is exactly what concentrates flood exposure. Exposure severity is set by **site elevation relative to the flood surface — a field not in the substrate** — so this stays geographic and directional.

### Source References
```text
substrate · InfraSure get_plant(3459)         · Sabine          · lat/lon 30.0242/-93.878, Orange County, cooling_water_source="Sabine Lake"/"Sabine River" · as_of 2026-06-29 · primary (siting + mechanism C/A)
substrate · InfraSure get_plant(3459).grid    · Sabine          · on-site 230 kV substation, MISO/SERC          · as_of 2026-06-29 · primary (mechanism A)
substrate · InfraSure get_plant(3459).ownership · Sabine        · Entergy → BlackRock/Vanguard                  · as_of 2026-06-29 · support (actor)
substrate · InfraSure get_plant(3459).generation · Sabine       · monthly CF; Harvey window 2017-08=0.308, 2017-09=0.306 (≈ normal) · as_of 2026-06-29 · support (CF-can't-show-it)
substrate · InfraSure nearby_plants(3459)      · 66621 / 10789   · same-floodplain fan-out                       · as_of 2026-06-29 · support (portfolio accumulation)
external  · public record (FEMA DR-4332-TX / NOAA) · Gulf Coast TX · Hurricane Harvey Aug 2017 catastrophic flooding · accessed 2026-06-29 · primary (realized event, REGIONAL)
```

### Confidence
Per-claim-part. **Exposure + mechanism (C/A): Medium** — geography is clear (Gulf Coast tidewater siting confirmed by the cooling-water source field), the fleet is resolved, the asset-specific mechanism is stated. **Harvey as a realized event: factual as a REGIONAL fact** (public FEMA/NOAA record) — *not* a per-Sabine damage claim; note **no in-substrate hazards-news article corroborated it in this run** (see Gaps), so the event leg rests on the public record. **Any CF read: Low/blocked** — Sabine's Aug/Sep 2017 CF is essentially normal, and the visible near-zero months (2023-12 = 0.003, 2024-12 = 0.022) are unrelated anomalies; the series cannot isolate a flood. **High is not reachable** on the substrate alone.

### Caveats
- The mechanisms are distinct; this claim is **(C)** cooling-intake + **(A)** switchyard, not equipment-damage attribution.
- Exposure is driven by **site elevation** (not in the substrate) — Sabine may be partially pad-elevated or bermed; the claim is geographic, not a per-pad depth.
- **Monthly CF cannot isolate an inundation outage** — proven here: CF through Harvey is normal; CF dips elsewhere have other causes.
- **VERIFY catch**: `news_extracted.company` tags Sabine as "Cheniere Energy" (conf 0.60, n=1) — this fails verification (owner is Entergy); the tag was not used.
- **Forward caveat**: 3 of 4 units (gen 1/3/4) carry `planned_retirement = 2026-07`; a forward-looking exposure read must note the asset is largely retiring next month.
- Dollar severity / EAL / payout not modeled (model-gpr).

### Actor Relevance
- **owner_operator (Entergy)** — cooling-intake + switchyard flood resilience; but weigh against the July-2026 retirement of 3 units. *(platform_card, account_note)*
- **investor** — Gulf Coast tidewater floodplain accumulation across the Sabine/Neches reach (Sabine + Orange County APS + Sabine River Operations). *(portfolio_note)*
- **lender** — FEMA flood-zone status + flood-insurance adequacy as underwriting inputs for any financed coastal-thermal asset in the reach. *(account_note)*

### Review Trace
Checked against `blocked_claims`: no $ / EAL / payout; no forward inundation probability / return-period; no per-plant damage from CF (explicitly refused — CF is normal through Harvey); no which-pads-flooded; no national-from-regional; no outreach. Gate: **PASS** — directional exposure + mechanism, Medium.

### Gaps / Next Fixes
- `search_news` has **no `category` param** (uses query + lane/event_type); the planned `search_news(category=hazards,...)` is not the live signature — `data_requirements.md` retrieval step updated. → log to `../../docs/status/mcp_gaps.md`.
- `search_news(query="flood…", state="TX")` returned **`[]`** (as_of 2026-06-29) — no in-substrate flood-event corroboration found this run; event leg rests on the public Harvey record.
- No **site-elevation** field (R-new) — blocks depth/return-period; the standing gap for this resource.
- `iso=` not used; scoped by `state="TX"` per R1 (confirmed: Sabine resolves to MISO, not ERCOT — state-scoping correctly captured an Entergy/MISO East-TX asset).

---

**See also**: `../test_runs/test_run_001.md` (the live execution record) · `../knowledge.md` (mechanism + Harvey anchor) · `../data_requirements.md`.
