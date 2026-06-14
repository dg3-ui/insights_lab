# offtaker_concentration — Offtaker Concentration & Merchant Exposure

> **Status**: draft, test 001 PASS (2026-06-14). The **first `commercial`-domain resource** — and the **first FACTUAL (non-directional) resource** in the lab. It proves the resource_standard's confidence/caveat machinery works on a *fact* (who buys the power) as well as a forecast.

## What this is

A methodology package teaching a model to reason like an InfraSure analyst about **revenue-counterparty risk** — who buys a scope's power (named PPA offtakers), how **concentrated** the revenue is in one buyer, and how much is **merchant / uncontracted** (the null is a finding). Factual, resolution-layer grounded; the **price / credit layer is deliberately blocked** (model-gpr).

## Files

```text
resource.yml          the structured seam (taxonomy · maturity · confidence_rules + blocked_claims) — NO peril block (factual)
resource.md           the human-readable method
knowledge.md          the cited mechanism (revenue = contracted + merchant) + the resolution-layer fact basis + the anchors
prompt_projection.md  the pasteable session surface
data_requirements.md  the retrieval plan + known gaps (offtakers-null · partial coverage R5 · parent canonicalization R9)
SKILL.md              the published, loadable skill
examples/applied_insight_001.md   the validated output — Amazon US book + ERCOT/TX merchant tail
test_runs/test_run_001.md         the live MCP test record (PASS)
```

## Grounding at a glance

```text
GROUNDS    find_by_extracted_fact(buyer) [THE reverse lookup] · get_plant.news_extracted.buyer (+seller/ppa_type) [VERIFY] ·
           total_capacity_mw (sum verified-only) · ownership.canonical_owner (route) · the merchant NULL (reported as-is)
BLOCKED    re-contracting / merchant $/MWh · counterparty default prob / rating · INFERRING a buyer into a null ·
           SUMMING look-alike owners · `offtakers:null` read as "no PPA" · a deal_value as a PPA price · national-from-one-book
KEY FIND   the slim `offtakers` array is NULL even where a PPA exists → grounding is the RESOLVED FACT (news_extracted.buyer),
           never the empty array. The new failure modes vs directional resources: inferring a null + summing look-alike owners.
```

## How it differs from the hazard/weather resources

```text
hail_solar / el_nino_enso   DIRECTIONAL odds on a shifting baseline (non-stationarity caveat)
offtaker_concentration      FACTUAL — resolved-fact quality (one source vs many + VERIFY) + PARTIAL COVERAGE
```

Same discipline (ground-or-downgrade, blocked_claims, cap-at-weakest, per-part confidence) — different failure modes.

---

**See also**: `../README.md` (the registry) · `../../docs/method/resource_standard.md` (the contract this factual resource stresses) · `../hazard/hail_solar/` (the structural reference) · `../../docs/method/analysis_families.md` (the Commercial family).
