# Severe Hail Exposure For Solar Assets — Method (human-readable)

> **Status**: draft 2026-06-14. The human-readable companion to `resource.yml` (the structured operation) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. The first hazard-domain resource (`hazard/`); the worked structural reference is `../weather_and_climate/el_nino_enso/`.

## What it answers (and what it refuses)

```text
ANSWERS   which solar assets/owners/regions sit in a severe-hail geography · what a realized hail event meant
          for a named asset (observed operating impact) · the mechanism + mitigation · who should care
REFUSES   exact $ loss / EAL / insurance payout · forward hail probability / return-period · plant-level
          forecast · single-cause attribution of an observed CF change · outreach before the gate
```

## Scope

Solar (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = ERCOT/Texas) · operating + queue (siting) · actors: owner-operator · investor · lender · developer.

## Mechanism (cite `knowledge.md`; do not re-derive)

Severe hail (≳1–2 in) → c-Si module glass/cell damage → output + availability loss. The two modifiers that carry the variance: **single-axis trackers can hail-stow** (the main mitigation lever) and **module glass spec** (hail-rated vs thin). Geography: the southern Great Plains / **Texas is the US hail maximum** (SPC). Claim type splits: a **realized event** can be *factual* (corroborated + observed CF dip); **forward probability** is *not* groundable here.

## Procedure (the real tool sequence)

```text
1. hazard state:  SPC hail climatology (geography) AND/OR search_news(category=hazards, query="hail")  → VERIFY each
2. scope:         search_plants(fuel="solar", state="TX", minMw=50)   ⚠ NOT iso="ERCOT" → [] (R1); confirm region via get_plant
3. footprint:     get_plant geometry/county + nearby_plants            → solar in the same hail cell
4. realized:      get_plant.generation                                 → OBSERVED post-event CF change (like-months YoY)
5. actor:         get_plant.ownership                                  → owner chain + portfolio concentration
6. draft:         assemble the claim grammar; cap confidence; block the $ / probability / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional hail exposure · realized event→asset with observed CF impact · owner/portfolio concentration ·
         mechanism + mitigation (hail-stow) · monitoring/hardening recs
BLOCKED  exact $ / EAL / payout · forward probability / return-period · plant-level forecast · single-cause
         attribution · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *realized event-translation* can reach **High** (multi-source event + observed CF dip); the *forward fleet exposure* stays **Medium/Low** (geographic/directional, no hail model). Required caveats: observed CF change is *consistent with* not *solely caused by* hail; the hazard classification is *verified*, not taken on the label; hail is sudden-onset + climatologically concentrated; $ severity is not modeled here. The $ / insurance layer is the model-gpr upgrade (`mcp_gaps` R12).

## Actor relevance

Owner (hail-stow protocol, hail-rated glass, deductible exposure, outage recovery) · investor (hail-geography portfolio concentration) · lender (DSCR stress from a hail outage — directional) · developer (siting/design in the hail maximum). Relevance never distorts the method.

---

**See also**: `resource.yml` (the structured contract) · `knowledge.md` (the cited "why" + the Fighting Jays anchor) · `prompt_projection.md` (the session surface) · `data_requirements.md` (retrieval plan + gaps) · `examples/applied_insight_001.md` (the validated output) · `test_runs/test_run_001.md` (the live test record).
