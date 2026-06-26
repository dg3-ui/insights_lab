# Applied Insight 001 — Hurricane Coastal Flood × Texas Gulf Coast Energy Cluster (PENDING)

> **Status**: PENDING — `test_run_001` must be executed against the live InfraSure MCP before this example can be validated. Populate only from a saved test transcript.

## Target scope for test 001

```text
Geography:  Texas Gulf Coast / Houston-Galveston
Fuel:       Gas plants first (or another single asset class chosen before test)
Condition:  named storm-surge / coastal-flood source (NHC/FEMA/SLOSH/tide gage/local study)
Question:   Which coastal energy assets >=50 MW are directionally exposed to storm surge / coastal flooding,
            and what component pathway makes that exposure relevant?
```

## Expected output format (populate after test_run_001)

```text
## Applied Insight Draft

### Claim
[directional storm-surge / coastal-flood exposure + component-pathway claim for scoped coastal assets]

### Scope
[resolved plant list: geography, fuel, minMw=50, as_of=<date>]

### Mechanism
[surge/tide/waves/drainage -> component inundation: substation / transformer / access / fuel/cooling / interconnection]

### Source References
[each: type · source · entity/scope · field/fact · vintage/as_of · role]

### Confidence
[per-claim-part:
 - regional storm/surge/flood source: factual/medium if dated
 - asset exposure screen: low/medium depending on elevation/flood-zone evidence
 - exact depth/damage/outage/$: blocked]

### Caveats
[lat/lon/county is a screen, not inundation model;
 FEMA/SLOSH frame exposure but do not prove damage;
 monthly generation cannot isolate surge outage;
 wind and water are separate claim types;
 $/insurance not modeled]

### Actor Relevance
[owner: hardening / equipment elevation / access
 investor: coastal accumulation
 lender: collateral and DSCR sensitivity
 developer: siting / pad elevation / drainage]

### Review Trace
[tool call sequence + results summary]

### Gaps / Next Fixes
[elevation, flood zone, component location, surge overlay, outage/damage record]
```

---

**See also**: `../test_runs/test_run_001.md` · `../knowledge.md` · `../data_requirements.md`.
