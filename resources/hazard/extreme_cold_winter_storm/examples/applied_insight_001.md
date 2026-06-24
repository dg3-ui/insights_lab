# Applied Insight 001 — Extreme Cold / Winter Storm × ERCOT Texas Thermal Fleet (PENDING)

> **Status**: PENDING — test_run_001 must be executed against the live InfraSure MCP before this example can be validated. This file is a placeholder. Once test_run_001 is complete, populate this file with the actual validated output following the format below.

## Target scope for test 001

```text
Geography:  ERCOT / Texas — the Uri epicenter
Fuel:       Gas / thermal (primary); optionally fan out to wind for the correlated picture
Event:      Winter Storm Uri (February 10–20, 2021)
Question:   Which ERCOT gas generators sit in the freeze-exposed geography, and what does the Uri mechanism mean for their exposure?
```

## Expected output format (populate after test_run_001)

```text
## Applied Insight Draft

### Claim
[directional freeze-exposure + mechanism claim for the scoped ERCOT gas fleet]

### Scope
[resolved plant list: state="TX", fuel="gas", minMw=50, as_of=<date>]

### Mechanism
[GAS mechanism (A): wellhead/pipeline freeze → gas curtailment; instrument freeze → forced trip
 → DISTINCT from equipment damage; Uri: ~87% of ~32 GW ERCOT peak outage (FERC/NERC 2021-11)]

### Source References
[each: type · source · entity/scope · field/fact · vintage/as_of · role]

### Confidence
[per-claim-part:
 - exposure + mechanism: Medium (clear geography, robust physics, FERC/NERC documented)
 - Uri as regional event: factual (FERC/NERC) — NOT a per-plant outage claim
 - any CF read: Low/blocked (February dip IS the seasonal minimum)
 - High: NOT reachable on the substrate alone]

### Caveats
[THREE mechanisms stated and distinguished by fuel;
 monthly CF cannot isolate a forced outage from the seasonal minimum;
 per-plant attribution blocked without an outage record;
 Uri was a tail event — return-period requires a climate model;
 winterization gap is concentrated in Southern-latitude plants, not universal;
 $ severity is not modeled (model-gpr)]

### Actor Relevance
[owner: cold-weather package investment decision + firm gas contracts
 investor: portfolio freeze-geography accumulation + correlated scarcity exposure
 lender: DSCR stress from a multi-day forced outage — directional
 developer: cold-weather-package spec for queue-stage TX thermal/wind]

### Review Trace
[tool call sequence + results summary]

### Gaps / Next Fixes
[known gaps surfaced during the test: iso filter, no winterization field, CF resolution, etc.]
```

---

**See also**: `../test_runs/test_run_001.md` (the live execution record) · `../knowledge.md` (the mechanism + Uri anchor) · `../data_requirements.md` (the retrieval plan).
