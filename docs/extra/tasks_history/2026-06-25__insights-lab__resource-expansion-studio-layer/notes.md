# Notes — Resource Expansion + Studio Layer Planning

---

## Historical-Context Verification Workflow

The parallel citation-sweep workflow is now reusable. The script lives at:
```
.../workflows/scripts/verify-historical-context-citations-wf_b650a441-b4f.js
```

Pattern: 8 agents in parallel → one per `historical_context.md` → each fetches every cited URL, reads PDFs via the Read tool, uses WebSearch for paywalled sources → returns per-citation verdicts (verified / mismatch / attribution_error / unfetchable / url_dead).

**Key learnings from the sweep:**
- Binary PDFs: WebFetch cannot parse them — it saves to a local path. Use `Read` with `pages:` param on the saved path.
- Paywalled journals: use WebSearch to corroborate specific figures from the abstract or coverage (e.g. Nature Communications paper on 2023/24 El Niño teleconnections).
- Bot-blocking 403s (Houston Chronicle, PG&E SEC filing, pv-magazine): the underlying facts were corroborated via other sources; leave the original URL, note bot-blocking in the gap.
- The `>$75M` → `~$70M` correction for Midway Solar was the most impactful: multiple industry sources report $70M; the `>$75M` figure was unverifiable. Changed to "approximately $70 million" with the $70–80M range noted.

---

## Deep-Research Workflow for `historical_context.md`

The 3-phase pattern (research → verify → synthesize) is now the standard for every new package:

```
Phase 1 — Research (parallel, one agent per candidate event)
  WebSearch for citable energy-infrastructure figures
  Look for: DOE, EIA, NERC, NRC, FERC, NWS, USGS, utility filings, NERC event analyses
  Return: viable flag + best_sources array + energy_impact summary

Phase 2 — Verify (parallel, one agent per viable event)
  WebFetch every URL → confirm number appears verbatim
  PDF binary → Read saved path with pages: param
  Paywall → WebSearch corroboration
  Return: citation verdicts + verified_narrative + use_this_event flag

Phase 3 — Synthesize (single agent)
  Takes all verified_narratives
  Writes complete historical_context.md in the canonical format
  Embeds corrections in "What it does NOT license" rows
```

For `riverine_flood`: 5/5 candidate events verified; workflow ran 11 agents, 329 tool uses, ~23 minutes.

---

## Key `riverine_flood` historical-context findings

**Pattern 3 (non-obvious):** Extreme riverine inflow is a *hydro generation surplus* event, not just a threat. WAPA 6-dam Missouri mainstem system produced +38% above long-run average generation in 2019 and $40M+ in surplus hydropower revenue (2-year). Any riverine flood insight that includes hydro assets must explicitly bifurcate: *thermal/distribution assets face outage risk; hydro assets may benefit*. This is now in Pattern 3 of the cross-event section.

**Fort Calhoun attribution trap (important for blocked-claims discipline):** The 2011 outage lasted 2.5 years — but the extension was driven primarily by pre-existing safety deficiencies, not flooding. UCS, EIA, and the NRC IMC 0350 record all confirm this. Citing this as "the flood caused a 2.5-year outage" is a causation error. The `What it does NOT license` row explicitly flags this.

**The substation pattern (holds across ALL 5 events):** The binding failure point in every event was a substation or switchgear room, not the generating unit. OPPD switchgear at Offutt (2019), Fort Calhoun AquaDam breach → grid disconnect (2011), Des Moines electrical infrastructure (1993), Cedar Rapids two substations total-loss (2008), Nashville three substations in one storm (2010). This is Pattern 1 and it directly informs the `blocked_claims` discipline: plant-centroid proximity is never sufficient; substation/switchyard location and elevation are the actual exposure variables.

---

## MCP Gap Ledger State After This Session

| Range | New this session | Total |
|---|---|---|
| R1–R20 | pre-existing | 20 |
| R21–R23 | drought_low_hydro | +3 |
| R24–R25 | hurricane_coastal_flood | +2 |
| R26–R27 | riverine_flood | +2 |
| **Total** | **+7** | **27** |

Highest-priority new gaps:
- **R26** (HUC/river-reach per plant) and **R27** (FEMA riverine zone join) are P3 — medium effort, directly unblock `riverine_flood` moving from county-screen to basin-specific claims.
- **R21–R22** are the equivalent for `drought_low_hydro` (plant-to-basin/reservoir; hydro operations surface).

---

## The Studio Orchestration Gap (the most important note)

The lab now has 10 resources and a validated output layer (`/render` + `studio/`). What it does NOT have is the **composition logic** — the answer to "given these resources, what deliverables can I make, for which actors, in which combinations?"

This logic is currently implicit and hand-assembled per deliverable. At 10 resources it's becoming the bottleneck. The missing layer has several sub-components:

### A. Output type × resource mapping
Which resources can feed which output types:

| Output type | Resources likely needed |
|---|---|
| Single-hazard risk brief (1 asset class, 1 peril) | 1 resource (e.g. `hail_solar`) |
| Multi-hazard risk brief (1 asset class, n perils) | n hazard resources (e.g. `wildfire` + `extreme_cold` for ERCOT wind) |
| Climate + hazard combined brief | weather_and_climate resource + relevant hazard resource |
| Commercial concentration read | `offtaker_concentration` + optional hazard for the same portfolio |
| Full risk appetite brief (all exposures for 1 owner) | 3–5 resources composed |
| Sector / domain theme (all hazard at once) | all hazard domain resources |

### B. Risk-appetite tiers (the user's framing)
This maps to how much surface area to cover in one deliverable:

```
TIER 1 — Single resource     One risk, one asset class, one region (current default)
TIER 2 — Domain bundle       All hazard at once OR all weather_and_climate OR commercial
TIER 3 — Full portfolio      All resources for a named owner / portfolio
TIER 4 — Cross-connection    e.g. ENSO + drought_low_hydro + riverine_flood (correlated water-risk bundle)
```

### C. Actor routing
Each output type needs different framing for each actor (owner, investor, lender, developer). The `actor_relevance` fields in every `resource.yml` define this, but there's no orchestration layer that reads them to pick the right framing at compose time.

### D. The cross-connection problem
Some resources share correlated drivers and produce stronger insights together than apart:
```
water-risk bundle:   drought_low_hydro + riverine_flood (both water-stress; opposite direction for hydro)
winter bundle:       extreme_cold_winter_storm + wind_drought (correlated cold/low-wind events)
climate × hazard:    el_nino_enso + wildfire (ENSO → dry winter → elevated fire risk)
                     el_nino_enso + hurricane_coastal_flood (ENSO → Atlantic hurricane modulation)
```

These cross-connections exist in the knowledge bases today but aren't explicitly mapped anywhere. That map is what the orchestration layer needs.

### E. What this layer looks like concretely
A `studio/orchestration/` subdirectory (or a plan document) containing:
- A **recipe library** (`docs/method/workflow_recipes.md` is a stub) — named recipes for each output type/tier with explicit resource lists, composition order, and actor routing
- A **cross-connection map** — which resources share correlated drivers and how to combine them
- A **deliverable catalog** — for each of the 10 resources, what output types it can anchor or support
- A **test-to-deliverable gate** — the rule for when a resource's test 001 PASS unlocks it for a given output tier (currently implicit)

The `/render` skill already handles the final rendering step. The orchestration layer is the *upstream* logic that decides *what* to render.
