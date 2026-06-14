# Applied Insight 001 — Hurricane / High-Wind Exposure, Coastal/Gulf ERCOT/Texas Wind (Beryl corridor)

> **Status**: validated 2026-06-14 (test_run_001). Real entities / ids / `as_of` — no placeholders. Meets the applied-insight thin contract (`../../../docs/method/resource_standard.md`). Scope: coastal/Gulf ERCOT/Texas wind ≥ 50 MW, anchored on the realized Hurricane Beryl track. Note: confidence ceiling is deliberately LOWER than `hail_solar/applied_insight_001.md` — the substrate carries no realized wind-damage signal here, and that is the honest finding.

## Applied Insight Draft

### Claim

Three parts, at different confidence (the claim grammar in action):

1. **Directional coastal exposure** — **Texas hosts the largest US wind fleet (49,719.6 MW; #1 state, vs OK 13,491.9 / IA 13,409.5)**, and a material **coastal/Gulf** sub-fleet sits in the **NHC landfalling-hurricane corridor**. Identified coastal-county wind ≥ 50 MW includes, e.g. **Peyton Creek I (62417, 151.2 MW, Matagorda) + Peyton Creek II (67700, 243 MW, Matagorda), Karankawa (61343, 307.1 MW, San Patricio, Avangrid), Pattern Gulf Wind (56661, 283.2 MW, Kenedy, Pattern Energy), Los Vientos 1B (57752, 201.6 MW, Cameron, Duke), Penascal (56795/57095, 2×201.6 MW, Kenedy)** — i.e. several GW of coastal TX wind in the corridor.
2. **Realized event framing (regional)** — **Hurricane Beryl made TX landfall ~Category 1 on 2024-07-08 near Matagorda/Bay City** (NHC; corroborated in-substrate: Newsweek → South Texas Project nuclear (6251) "threatened"; Reuters → ~1M+ TX customers without power). The nearest in-substrate coastal wind anchor, **Peyton Creek Wind Farm LLC (62417), is in Matagorda County — the landfall county** (47× Nordex AW125/3150, hub 87.5m, RWE Clean Energy, COD 2020). At Cat 1, the mechanism most plausibly in play was a **temporary cut-out**, not widespread structural damage.
3. **Mechanism, with the cut-out/damage split** — coastal turbines **feather + shut down above ~25 m/s** (temporary, recoverable zero-output) and take **lasting blade/nacelle/tower damage only at Cat 3+ design-exceeding winds**; coastal sites add storm-surge to foundations/substation. These are **different claim types**; a Cat 1 landfall maps to the first.

### Scope

Coastal/Gulf ERCOT/Texas, wind ≥ 50 MW. Anchor: Peyton Creek I (62417, Matagorda County, ERCOT HB_HOUSTON, lat 28.868/−95.906). Corridor cluster: 67700, 61343, 56661, 57752, 56795/57095 (coastal-county filter on the TX wind fleet).

### Mechanism

Hurricane / high wind → (A) wind ≥ ~25 m/s → turbine feather/shutdown → ~zero output during the storm → recovers (TEMPORARY cut-out); (B) Cat 3+ design-exceeding gusts → blade/nacelle/tower damage + coastal storm-surge → weeks-to-months outage (LASTING). Beryl landfall ~Cat 1 ⇒ regime (A). (`knowledge.md` §1, §6.)

### Source References

```text
1. external · NOAA NHC best-track / HURDAT2 (Beryl AL022024) · TX landfall ~Cat 1, 2024-07-08, near Matagorda · accessed 2026-06-14 (cited, knowledge.md §3) · frames the event + corridor
2. substrate · InfraSure search_news(query="Beryl") · Beryl hazards articles · Newsweek (2024-07-08) South Texas Project (6251 NUC) "threatened", Matagorda/Bay City; Reuters (2024-07-11) ~1M TX customers offline · VERIFIED · support (regional event; NOT a wind-plant record)
3. substrate · InfraSure aggregate(plants, state, total_capacity, fuel=WND) · TX 49,719.6 MW (#1 wind state) · as_of 2026-06-14 · support (fleet size)
4. substrate · InfraSure search_plants(fuel=wind, state=TX, minMw=50) → coastal-county filter · 62417, 67700, 61343, 56661, 57752, 56795/57095 (Matagorda/San Patricio/Kenedy/Cameron) · as_of 2026-06-14 · primary (the corridor scope)
5. substrate · InfraSure get_plant(62417) · Peyton Creek I · 151.2 MW, 47× Nordex AW125/3150 (hub 87.5m), Matagorda County, ERCOT, RWE Clean Energy, COD 2020 · as_of 2026-06-14 · primary (the coastal anchor)
6. substrate · InfraSure get_plant(62417).generation · monthly capacity_factor 2020-06 … 2025-12 · as_of 2026-06-14 · CONTEXT ONLY (used to SHOW the storm is not separable — see Caveats)
7. substrate · InfraSure get_plant(67700) · Peyton Creek II · 243 MW, 54× Vestas V163-4.5 (hub 112m), Matagorda, RWE · COD 2025 (after Beryl → no pre/post window) · as_of 2026-06-14 · support
```

### Confidence

**Per-part**, and the ceiling is deliberately below `hail_solar`:
- *Coastal-corridor exposure + the cut-out/damage mechanism* — **Medium** (clear geography via NHC, resolved coastal wind scope, robust IEC physics).
- *Beryl made landfall ~Cat 1 near Peyton Creek* — **factual as a REGIONAL event** (NHC + corroborated hazards news) — but **not** a wind-plant damage claim (no wind-plant operational record exists in the substrate).
- *Any read of Beryl into the CF series* — **Low / blocked** — see Caveats; the July-2024 CF (0.129) is in-line with the 2021 summer lull (0.129) and ABOVE the 2025-08 (0.078) lull that had no hurricane.
- **High is not reachable** on the substrate alone (would need a verified wind-plant damage record — absent — or a served TC hazard model).

### Caveats

- **Cut-out (temporary) vs damage (lasting) are different claim types.** A turbine feathering/shutting down above ~25 m/s is the design behaving correctly (recoverable); lasting damage needs Cat 3+ design-exceeding winds. Beryl was ~Cat 1 → most plausibly a cut-out, not widespread damage.
- **Monthly capacity factor CANNOT isolate a storm cut-out from the summer wind lull.** Peyton Creek I: 2024-07 CF 0.129 — identical to 2021-07 (0.129, no hurricane), and ABOVE 2025-08 (0.078, no hurricane). A multi-day Beryl cut-out (early July) is invisible at monthly resolution and confounded by the seasonal minimum. (2025-03 CF 0.020 — near-zero, no storm — shows monthly CF swings for non-hazard reasons too.) **No single-cause CF claim.**
- **The hazards-news classification was verified, not taken on the label** — and notably, the TX hurricane articles link to **nuclear/hydro/gas** plants and grid-customer outages, **not** to wind turbines; one "hurricane"-tagged solar article was actually a *tornado*. The wind operational impact was reasoned from the mechanism, not lifted from a wind-plant record.
- Hurricane exposure is **sudden-onset locally and climatologically concentrated on the coast** — geographic exposure, not a dated forecast. Non-stationarity caps any trend claim.
- **No dollar figure / no EAL / no return-period**: that layer is model-gpr (`grounding_maturity: model-not-wired`).

### Actor Relevance

- **Owner (RWE on the anchor; Avangrid/Pattern/Duke across the corridor)** — cut-out availability planning, turbine design-wind-class review (IEC), surge/foundation hardening on coastal sites, outage-recovery protocols.
- **Investor** — coastal-portfolio accumulation in the Gulf hurricane corridor is a real availability/revenue downside axis in a landfall year (several GW of TX wind sits coastal).
- **Lender** — a hurricane-driven outage (cut-out + any repair) is a DSCR stressor on a financed coastal wind asset (directional).
- **Developer** — siting + turbine wind-class + surge-aware foundation choices for queue-stage coastal/Gulf wind (e.g. Peyton Creek II's 2026 interconnection record sits in this corridor).

### Review Trace

Checked against `blocked_claims`: no $/EAL/PML/payout asserted (✓); no forward hurricane probability / return-period (✓); no plant-level forecast (✓); no single-cause CF attribution (✓ — explicitly shown un-separable); no lasting-damage-from-a-Cat-1 claim (✓ — defaulted to cut-out); not national (✓ — scoped coastal TX). Cut-out vs damage distinguished (✓). Hazard classification verified, and flagged as linking to non-wind plants (✓). Each material number carries a substrate `source_ref` with `as_of`; CF used only as context. Confidence split per-part, capped at Medium. **Gate: PASS (directional).**

### Gaps / Next Fixes

- `search_plants(iso="ERCOT")` → `[]` for wind (the R1 `iso`-filter gap, now confirmed for wind too) — used `state="TX"` + a coastal-county filter. Logged.
- No served TC / high-wind peril model → the $ / EAL / forward-probability layer is blocked; logged as `mcp_gaps` R12 (the directional-now-quantify-later wall).
- Hazards news does **not** link to wind plants → the realized wind operational impact had to be reasoned from the mechanism. A hazards→wind-plant link + a daily/hourly (or availability) generation feed would surface a real cut-out signal and lift confidence.
- `nearby_plants(62417, fuel=wind, radius_km=80)` returned only 1 neighbor → built the corridor cluster from the state-wide coastal-county filter instead.
