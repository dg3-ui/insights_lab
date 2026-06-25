# Applied Insight 001 — Wildfire × CAISO California Solar Fleet + PSPS Curtailment (PENDING)

> **Status**: PENDING — test_run_001 must be executed against the live InfraSure MCP before this example can be validated. This file is a placeholder. Once test_run_001 is complete, populate this file with the actual validated output following the format below.

## Target scope for test 001

```text
Geography:  CAISO / California — the primary PSPS jurisdiction and Western fire-weather epicenter
Fuel:       Solar (primary — mechanism A: smoke/ash); optionally wind/gas (mechanism C: PSPS curtailment)
Events:     2020 CA wildfire season (smoke/solar) + PG&E PSPS events (2019–present) (curtailment)
Question:   Which CAISO solar assets sit in fire-weather-exposed geographies, and what do the smoke and PSPS
            mechanisms mean for their output and revenue exposure?
```

## Expected output format (populate after test_run_001)

```text
## Applied Insight Draft

### Claim
[directional fire-weather exposure + mechanism claim for the scoped CAISO solar fleet;
 PSPS curtailment as the most grounded claim type; smoke/output as directional]

### Scope
[resolved plant list: state="CA", fuel="solar", minMw=50, as_of=<date>]

### Mechanism
[SOLAR mechanism (A): smoke/ash → irradiance reduction + soiling — temporary, not structural damage in most cases
 PSPS mechanism (C): utility de-energizes circuits during red-flag conditions → healthy generators curtailed
 → temporary revenue loss. Fuel irrelevant; circuit location determines PSPS exposure.
 TRANSMISSION mechanism (B): noted as out of scope for this solar-focused test;
 ignition liability BLOCKED — model-gpr / legal]

### Source References
[each: type · source · entity/scope · field/fact · vintage/as_of · role]

### Confidence
[per-claim-part:
 - fire-weather geography + mechanism: Medium (NIFC/NOAA/CAISO documented, robust physics)
 - a named fire / PSPS event affected the geography near a scoped asset: factual as a regional event (NIFC/CAISO) — NOT a per-plant claim
 - any CF read: Low/blocked (summer/fall CA dip is NOT separable from seasonal irradiance variation)
 - PSPS curtailment corroborated by CAISO filing: factual for the event window — most grounded claim type here
 - High: NOT reachable on the substrate alone]

### Caveats
[THREE mechanisms stated and distinguished by asset;
 monthly CF cannot isolate smoke from seasonal irradiance variation;
 PSPS curtailment ≠ physical fire damage;
 ignition liability blocked (model-gpr / legal);
 fire-weather intensification is directional, not a return-period;
 $ severity is not modeled (model-gpr)]

### Actor Relevance
[owner: PSPS notification + backup planning; panel cleaning schedules; ROW vegetation management
 investor: portfolio WUI / CAISO fire-geography accumulation; PSPS as recurring revenue risk; tightening CA wildfire insurance
 lender: DSCR stress from PSPS curtailment — directional; transmission-owner ignition liability as collateral tail risk
 developer: siting outside high-WUI zones; PSPS-aware interconnection circuit selection]

### Review Trace
[tool call sequence + results summary]

### Gaps / Next Fixes
[known gaps surfaced during the test: iso filter, no PSPS circuit field, no WUI geometry field, CF resolution, etc.]
```

---

**See also**: `../test_runs/test_run_001.md` (the live execution record) · `../knowledge.md` (the mechanism + Camp Fire / 2020 / PSPS anchors) · `../data_requirements.md` (the retrieval plan).
