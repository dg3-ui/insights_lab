# extreme_heat_derate — Extreme-Heat Thermal Derate For Solar Assets

> **Status**: draft, test 001 PASS (2026-06-14). A **weather × solar** resource (directional, weather-led — the ENSO pattern), the second `weather_and_climate` package after `el_nino_enso`. The grain is the **(driver × mechanism)** cell: extreme_heat × the PV temperature-coefficient de-rate.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **extreme heat × solar output** — who is exposed in a hot summer, the mechanism (the temperature-coefficient efficiency de-rate), **when** it bites (the hottest afternoon hours), and **why it matters more than its size** (it coincides with the ERCOT summer demand/price peak). Directional + LOW confidence by design; the quantified **%/MWh / $ layer is deliberately blocked** (model-gpr — `../../docs/status/mcp_gaps.md` R12).

## The defining discipline (the reason this resource is hard to get right)

```text
The de-rate is SECOND-ORDER, MODEST, and PEAK-HOUR-CONCENTRATED — never a CF collapse.
Summer monthly CF is HIGH (irradiance-dominated): real data ≈ 0.30 summer vs ≈ 0.09–0.15 winter.
⇒ DO NOT read a heat de-rate off monthly CF. Cap confidence at LOW. The point is PEAK COINCIDENCE, not energy.
```

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · confidence_rules + blocked_claims · non-stationarity)
resource.md           the human-readable method
knowledge.md          the cited mechanism (temperature coefficient) + the honesty section + the Aktina baseline
historical_context.md the event ledger (ERCOT 2023 · CAISO 2022 heat waves)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (R1 iso filter · R11 climate news · R12 thermal model)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the validated output — ERCOT/TX solar, Aktina + South-zone cluster
test_runs/test_run_001.md         the live MCP test record (PASS)
```

## Grounding at a glance

```text
GROUNDS    get_plant (summer-CF baseline / construction / grid zone / owner) · search_plants/aggregate (fleet) ·
           nearby_plants (same zone cluster) · NOAA CPC temperature outlook (the condition, cited + dated)
BLOCKED    exact %/MWh de-rate per plant · $ / MWh · forward heat probability / return-period · plant-level forecast ·
           reading heat off monthly CF (over-magnitude) · single-cause attribution
KEY FIND   the HIGH summer CF is the honesty proof — the de-rate is intra-day + peak-hour, invisible at monthly resolution;
           materiality comes from peak COINCIDENCE with the ERCOT summer price/demand peak, not from a big energy loss
```

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract + the non-stationarity rule) · `../el_nino_enso/` (the worked weather-resource sibling + NOAA-pull discipline) · `../../docs/status/mcp_gaps.md` (R1 · R11 · R12).
