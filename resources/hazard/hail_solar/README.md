# hail_solar — Severe Hail Exposure For Solar Assets

> **Status**: draft, test 001 PASS (2026-06-14). The **first `hazard`-domain resource** — and the flagship of the live product (hail insurance for solar). Authored in `docs/plans/2026-06-13_knowledge_base_expansion_v1.md` Phase 2.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **severe hail × solar** — who is exposed (geography), what a realized event meant (observed CF impact), the mechanism + mitigation (hail-stow), and who should care. Directional + realized-event grounded; the **dollar / insurance layer is deliberately blocked** (model-gpr — `../../docs/status/mcp_gaps.md` R12).

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · peril fields · confidence_rules + blocked_claims)
resource.md           the human-readable method
knowledge.md          the cited mechanism (hail → c-Si damage; hail-stow) + the Fighting Jays anchor
historical_context.md the deeply researched event ledger (Fighting Jays · Fort Bend stow comparison · Midway)
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (R1 iso filter · R12 peril model · classifier noise)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the validated output — ERCOT/TX solar, Fighting Jays
test_runs/test_run_001.md         the live MCP test record (PASS)
```

## Grounding at a glance

```text
GROUNDS    get_plant (geometry/CF/owner) · search_plants/aggregate (fleet) · nearby_plants (same cell) ·
           hazards news (the realized event, VERIFIED) · SPC climatology (the geography, cited)
BLOCKED    $ loss / EAL / payout · forward hail probability / return-period · plant-level forecast · single-cause
KEY FIND   the hail impact is OBSERVABLE in the generation CF series → the event-translation claim beats directional
```

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract) · `../weather_and_climate/el_nino_enso/` (the worked structural reference) · `../../docs/plans/2026-06-13_knowledge_base_expansion_v1.md` (Phase 2).
