# Applied Insight 001 — Drought / Low-Hydro × California Hydro Fleet (PENDING)

> **Status**: PENDING — `test_run_001` must be executed against the live InfraSure MCP before this example can be validated. This file is a placeholder. Populate it only from a saved test transcript.

## Target scope for test 001

```text
Geography:  California / CAISO proxy
Fuel:       Hydropower
Condition:  dated drought / snowpack / streamflow / reservoir-storage state
Question:   Which California hydro assets >= 50 MW are directionally exposed to low-water conditions, and
            what can we responsibly claim without plant/reservoir operations data?
```

## Expected output format (populate after test_run_001)

```text
## Applied Insight Draft

### Claim
[directional low-hydro exposure + mechanism claim for a scoped California hydro fleet]

### Scope
[resolved plant list: state="CA", fuel=<hydro convention>, minMw=50, as_of=<date>]

### Mechanism
[drought / low snowpack / low streamflow -> lower inflow/storage -> reduced hydro energy or flexibility;
 operations, water rights, environmental flows, flood-control rules, maintenance, and dispatch mediate plant-level result]

### Source References
[each: type · source · entity/scope · field/fact · vintage/as_of · role]

### Confidence
[per-claim-part:
 - dated drought / snowpack / streamflow state: factual if source current
 - hydro fleet exposure: low/medium depending on basin/reservoir linkage
 - plant-level MWh/$ impact: blocked
 - reservoir operations / water rights / dispatch: blocked unless named source]

### Caveats
[state/market is a screen, not a basin boundary;
 monthly generation is context, not drought attribution;
 exact plant impact needs plant-to-basin/reservoir linkage + operations model;
 non-stationarity blocks stationary return-period claims]

### Actor Relevance
[owner: reservoir scheduling / hedging / maintenance timing
 investor: portfolio concentration in low-water hydro
 lender: DSCR sensitivity to low-water years
 offtaker: contracted hydro volume / shape risk where contract context exists]

### Review Trace
[tool call sequence + results summary]

### Gaps / Next Fixes
[hydro fuel convention, ISO filter, plant-to-basin/reservoir linkage, reservoir operations, sub-monthly generation]
```

---

**See also**: `../test_runs/test_run_001.md` (the live execution record) · `../knowledge.md` (mechanism + source stack) · `../data_requirements.md` (retrieval plan).
