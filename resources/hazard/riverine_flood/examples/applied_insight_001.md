# Applied Insight 001 — Riverine Flood × Midwest / MISO Gas Fleet (PENDING)

> **Status**: PENDING — `test_run_001` must be executed against the live InfraSure MCP before this example can be validated. This file is a placeholder. Populate it only from a saved test transcript.

## Target scope for test 001

```text
Geography:  Midwest / MISO region — Missouri, Iowa, or Illinois
Fuel:       Natural gas (primary); hydro optional secondary
Condition:  current or recent riverine flood / elevated river stage condition
Question:   Which gas (and optionally hydro) plants >= 50 MW near the Missouri or Mississippi
            River corridor are directionally exposed to riverine flooding, and what can we
            responsibly claim without plant/component elevation or verified outage data?
```

## Expected output format (populate after test_run_001)

```text
## Applied Insight Draft

### Claim
[directional riverine flood exposure + mechanism claim for a scoped Midwest gas fleet]

### Scope
[resolved plant list: state=<MO|IA|IL>, fuel=<gas convention>, minMw=50, as_of=<date>]

### Mechanism
[heavy precipitation / snowmelt / dam release -> elevated river stage -> water reaches cooling
 intakes / substations / access roads / fuel systems; component elevation and event water surface
 mediate plant-level result]

### Source References
[each: type · source · entity/scope · field/fact · vintage/as_of · role]

### Confidence
[per-claim-part:
 - dated flood / river-stage condition: factual if USGS/AHPS-sourced and current
 - asset proximity / floodplain exposure: low/medium depending on river-reach linkage
 - plant-level inundation / damage: blocked
 - exact depth / $ / outage duration / return-period: blocked]

### Caveats
[county/state proximity is a screen, not an inundation model;
 FEMA AE zone is a long-run regulatory designation, not event-specific depth;
 monthly generation is context, not flood attribution;
 component elevation is the missing bridge;
 stationary return-period claims are blocked (non-stationarity);
 dam/levee failure consequences are not modeled]

### Actor Relevance
[owner: flood hardening, equipment elevation, cooling-intake protection, emergency response
 investor: portfolio accumulation in river-basin floodplain
 lender: DSCR sensitivity to flood-driven outage, repair, and flood-insurance gaps
 developer: siting, pad/switchyard elevation, drainage, interconnection resilience]

### Review Trace
[tool call sequence + results summary]

### Gaps / Next Fixes
[river-reach / HUC linkage, FEMA zone join per plant, component elevation, hazards news
 flood classification fidelity, sub-monthly generation + outage records]
```

---

**See also**: `../test_runs/test_run_001.md` (the live execution record) · `../knowledge.md` (mechanism + data stack) · `../data_requirements.md` (retrieval plan).
