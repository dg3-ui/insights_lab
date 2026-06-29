# Handoff — Resource Expansion + Studio Layer Planning

> **Read this first.** 60-second summary of what happened, then the explicit next-session execution roadmap.

---

## 10-Bullet Summary

1. **Catalog grew from 7 → 10 resources** — added `drought_low_hydro`, `hurricane_coastal_flood`, `riverine_flood`; all test 001 PENDING by design.
2. **`historical_context.md` now exists in all 10 packages** — a deep-researched, citation-verified event ledger; 73 citations swept; 3 corrected before shipping.
3. **The verification workflow is now the standard** — parallel agents (one per file), WebFetch → Read PDFs → WebSearch for paywalls; run it on every new `historical_context.md`.
4. **`riverine_flood` is the highest-quality new package** — 5 verified events, non-obvious Pattern 3 (hydro surplus from extreme inflow), Fort Calhoun attribution trap documented; commits `3088e4e` on main.
5. **R21–R27 added to the gap ledger** — HUC/river-reach linkage (R26), FEMA zone join (R27), hydro basin/operations (R21–R22), fuel alias (R23), coastal elevation/surge (R24–R25).
6. **Cleanup done** — `_writetest` deleted; raw deep-research output moved to `archive/historical_context_research/`; `InfraSure-Customer-Tracker.xlsx` NOT committed (customer list — keep local or gitignore).
7. **The resource queue continues** — `wind_drought` (weather_and_climate) and a 2nd commercial resource are next; same pattern: method → deep-research historical_context → citation-verify → register.
8. **Tests are intentionally PENDING** — the gate is studio readiness, not resource count; running tests without a clear deliverable path produces validated resources with nowhere useful to go.
9. **Studio orchestration is the most important missing layer** — at 10 resources the *composition problem* is the bottleneck; without it, every deliverable is hand-assembled one-off.
10. **All work is committed and pushed to main** — `8406148`, `ec57698`, `3088e4e`; working tree clean except `InfraSure-Customer-Tracker.xlsx`.

---

## Files the Next Session Should Read First

```
resources/README.md                          — the registry (10 resources, current state)
docs/status/mcp_gaps.md                      — R1–R27, especially R21–R27 (new this session)
docs/status/capabilities.md                  — what is and isn't built (the capability roadmap)
docs/plans/README.md                         — active plans (check for anything relevant)
studio/README.md                             — the output layer front door
docs/method/workflow_recipes.md (if exists)  — the recipe stub (if it was created)
resources/hazard/riverine_flood/README.md    — the newest package, as a quality reference
```

---

## Repro / Verification Commands

```bash
# confirm catalog state
grep "resources across" resources/README.md

# confirm all 10 packages have historical_context.md
find resources -name historical_context.md | sort

# confirm new gaps exist
grep -E "R2[1-7]" docs/status/mcp_gaps.md | head -14

# confirm clean working tree (except xlsx)
git status --short

# confirm last 3 commits
git log --oneline -3
```

---

## Next-Session Execution Roadmap

### PHASE A — Immediate catalog queue (1–2 sessions)

These follow the exact same pattern as `riverine_flood`:

**A1. `wind_drought` resource (weather_and_climate)**
- Slug: `wind_drought` / Skill: `wind-drought`
- Driver: extended low-wind-resource periods (multi-week to seasonal); distinct from single-storm wind events
- External grounding: NOAA CPC wind outlook, ERA5/NCEI wind speed anomalies, ISOs (ERCOT/MISO/SPP) wind generation data
- Asset class: onshore wind (primary); offshore secondary
- Key mechanism: low-capacity-factor periods → merchant revenue shortfall, PPA shape risk, portfolio CF variance
- Block: exact LMP/revenue impact, plant-level MWh from wind anomaly alone
- Historical context candidates: 2021 ERCOT February (low wind before freeze → compound), 2019 MISO low-wind summer, multi-year wind drought patterns from NOAA
- New gap to log: served regional wind-resource anomaly / drought index per wind asset (no plant-to-wind-regime linkage today)

**A2. 2nd commercial resource**
- Candidates (pick one): `merchant_exposure` (no PPA / merchant tail risk), `curtailment_cost` (curtailment × revenue shape), or `re_contracting_risk` (PPA expiry + merchant transition)
- `merchant_exposure` is probably the cleanest: grounded in substrate (PPA coverage, contract vintage, expiry dates in `get_plant.offtakers`), corroborated by `offtaker_concentration`
- Block: exact forward LMP, future PPA pricing

---

### PHASE B — Studio orchestration layer (the most important missing piece)

This is the priority after A1/A2. The goal: make the 10 resources composable into named deliverable types without hand-assembly every time.

**B1. Write `docs/method/workflow_recipes.md` (stub exists; needs content)**

Populate with named recipes — each recipe is: name + output type + resource list + actor framing + risk-appetite tier.

Start with these 4 immediately useful recipes:

```
RECIPE 1 — single-hazard brief
  Resources: 1 hazard resource (e.g. hail_solar)
  Actor: owner or lender
  Tier: 1 (single resource)
  Output: platform card + account note

RECIPE 2 — water-risk bundle
  Resources: drought_low_hydro + riverine_flood (+ el_nino_enso for seasonal framing)
  Actor: investor or lender
  Tier: 4 (cross-connection: correlated water-stress, opposite direction for hydro)
  Output: risk brief (2–3 page report)
  Key: bifurcate hydro (surplus vs. outage) from thermal/distribution (outage)

RECIPE 3 — all-hazard domain brief
  Resources: all 5+ hazard resources for a named owner's geography
  Actor: investor / portfolio risk
  Tier: 2 (domain bundle)
  Output: multi-hazard exposure summary (one section per peril)

RECIPE 4 — full owner risk appetite read
  Resources: relevant hazard + weather_and_climate + commercial resources
  Actor: lender / investor
  Tier: 3 (full portfolio)
  Output: structured risk brief across all exposure dimensions
```

**B2. Write `studio/orchestration/cross_connection_map.md`**

A matrix of resource pairs / clusters with correlated drivers:

| Cluster | Resources | Correlation type |
|---|---|---|
| Water stress | drought_low_hydro + riverine_flood | Same driver (precipitation deficit / excess); bifurcated impact for hydro |
| Winter compound | extreme_cold_winter_storm + wind_drought | Co-occurrence in cold/stagnant air masses; gas-electric compound risk |
| ENSO → hazard | el_nino_enso + wildfire | Dry-winter ENSO → elevated fire-season risk (SW U.S.) |
| ENSO → water | el_nino_enso + drought_low_hydro | Wet/dry ENSO pattern → hydro resource outlook |
| Coastal natcat | hurricane_coastal_flood + hurricane_high_wind_wind | Same storm, two mechanisms (wind ≠ surge) |
| Commercial + hazard | offtaker_concentration + any hazard | Buyer concentration × physical risk in same geography |

**B3. Write `studio/orchestration/deliverable_catalog.md`**

For each of the 10 resources:
- Which output types it can *anchor* (the primary resource for a deliverable)
- Which output types it can *support* (a secondary resource in a multi-resource recipe)
- Which actors it primarily routes to
- Its test status (PASS / PENDING) and what that unlocks for deliverable eligibility

**B4. Add a `studio/_triage.md` entry for each new resource**

`studio/_triage.md` is the internal ACT/WATCH/NOISE board. Each new resource should have a line saying whether it is:
- ACT: ready for a studio brief now (test passed + recipe exists)
- WATCH: pending test; recipe designed; waiting for the gate
- NOISE: not ready; needs more methodology work

---

### PHASE C — Test 001 loop (when studio is ready)

Run in priority order based on which recipes are ready:
1. `wildfire` (test 001 PENDING) — can anchor RECIPE 1 (single-hazard brief) once studio B1 is done
2. `extreme_cold_winter_storm` — RECIPE 1 + RECIPE 3 (all-hazard)
3. `hurricane_coastal_flood` + `riverine_flood` — RECIPE 2 (water risk is actually a flood risk bundle at this point, but the water-stress bundle for hydro is also valuable)
4. `drought_low_hydro` — RECIPE 2
5. `hurricane_high_wind_wind` — combine with `hurricane_coastal_flood` for RECIPE 4 (coastal natcat)

---

### PHASE D — `.gitignore` hygiene (5 minutes)

```bash
# Add to .gitignore:
docs/extra/InfraSure-Customer-Tracker.xlsx
# (and any other *.xlsx / *.pptx / *.docx in docs/extra/ that shouldn't be versioned)
```

---

## Critical Gotchas for the Next Session

1. **ISO filter (R1) is still broken** — always use `state=` not `iso=` in every MCP test. Confirmed broken for CAISO and ERCOT.
2. **Hydro fuel convention** — the MCP may use `WAT`, `HYD`, or `hydro`; always record the exact fuel token from search results before building on it.
3. **`historical_context.md` numbers must be re-verified before any external deliverable** — these are verified as of 2026-06-25; they can drift (URL rot, corrected figures). Re-sweep before shipping anything.
4. **Fort Calhoun causation trap** — the 2.5-year outage was pre-existing safety deficiencies, not flood. Do not attribute to flooding alone. The `What it does NOT license` row in `riverine_flood/historical_context.md` is explicit about this.
5. **Hydro surplus from extreme inflow (Pattern 3)** — if a riverine flood insight includes hydro assets, the framing must bifurcate: thermal/distribution faces outage risk; hydro may benefit. Not handling this is an overclaim.
6. **The studio tests are PENDING by design** — don't run them until the studio orchestration logic (Phase B) is in place. The gate is intentional.
7. **`InfraSure-Customer-Tracker.xlsx` is NOT in git** — it's sitting uncommitted in `docs/extra/`. Add to `.gitignore` before the next commit sweep.
