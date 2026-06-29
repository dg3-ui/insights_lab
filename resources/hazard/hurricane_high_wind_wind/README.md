# hurricane_high_wind_wind — Hurricane / High-Wind Exposure For Wind Assets

> **Status**: draft, test 001 PASS (directional, 2026-06-14). The **second `hazard`-domain resource** — the hurricane×wind sibling of `hail_solar`. Authored against live InfraSure MCP data.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **hurricane / high wind × wind turbines** — who is exposed (coastal/Gulf geography), the mechanism (the **temporary cut-out** vs the **lasting structural damage** split), what a realized storm (Hurricane Beryl) meant *regionally*, and who should care. Directional + mechanism-grounded; the **dollar / damage-severity / forward-probability layer is deliberately blocked** (model-gpr — `../../docs/status/mcp_gaps.md` R12). `grounding_maturity: model-not-wired`.

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method (the TWO claim types)
knowledge.md          the cited mechanism (cut-out vs damage; design wind class) + the Beryl/Peyton Creek anchor + why CF can't show it
historical_context.md the deeply researched event ledger (Beryl · Harvey)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (R1 iso filter · R12 TC model · no hazards→wind link · CF too coarse)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the validated output — coastal/Gulf TX wind, Beryl corridor
test_runs/test_run_001.md         the live MCP test record (PASS, directional)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/turbine model/owner) · search_plants/aggregate (TX wind 49,719.6 MW, #1) ·
           coastal-county corridor filter · NHC HURDAT2 (Beryl landfall, cited) · hazards news (the regional event, VERIFIED)
BLOCKED    $ loss / EAL / PML / payout · forward hurricane probability / return-period · plant-level forecast ·
           single-cause CF attribution (the July dip ≠ Beryl) · lasting damage from a sub-Cat-3 storm · national-from-regional
KEY FIND   the OPPOSITE of hail_solar — the substrate carries NO separable storm signal for wind (the July CF dip IS the
           summer lull; hazards news links to nuclear/hydro, not turbines) → ship exposure + mechanism at Medium, frame the
           storm as regional, and keep the realized-impact leg honestly LOW
```

## How it differs from `hail_solar`

```text
hail_solar              the realized hail impact was OBSERVABLE in the CF series → event-translation beat directional (High reachable)
hurricane_high_wind_wind the realized cut-out is INVISIBLE at monthly CF + confounded by the summer lull → event-translation stays
                         directional/regional (High NOT reachable on the substrate); the discipline is to NOT over-read the data
```

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract + peril-field/non-stationarity standard) · `../hail_solar/` (the sibling hazard resource + structural reference) · `../../docs/status/mcp_gaps.md` (R1 · R12).
