# Outlier Playbook — reverse-engineering an off-substrate asset (the ad-hoc / off-scope lane)

> **Status**: v0 — **NAMED + proven once** (Red Dog), 2026-06-14 (`../plans/2026-06-14_outlier_showcase_red_dog.md` Phase 2). The companion mode to forward-deployment: how an InfraSure analyst reasons about a climate-risk asset that is **NOT in the MCP substrate**. **Lean by design** — it stays a method doc, not a packaged resource, until a **second** outlier uses it (then consider formalizing/generalizing). Worked example: `../extra/reddog_bottom_up_report_2026-06.md`.

## 1 · The mode — forward-deployment vs reverse-engineering

```text
FORWARD-DEPLOYMENT (the core lab)             REVERSE-ENGINEERING (this playbook)
substrate-up: which (family × driver) cells   outlier-down: a specific off-substrate asset matters (showcase/pilot),
  fit our data + our client book                so demonstrate what the METHOD can do
grounded in the InfraSure MCP                  grounded in PUBLIC RESEARCH + the model + our resources
moat = curated data + reasoning               moat = the reasoning DISCIPLINE + a reusable method (NOT data)
```

**The grounding-mode insight this rests on**: the MCP is **top-down / competitive** grounding (rank a fleet, "you vs X across 15K plants"); **resources + the model + research** are **bottom-up** grounding (a single asset). On *any* bottom-up the MCP is anyway limited; an off-substrate outlier is just the extreme (≈ zero MCP) — which makes it the cleanest demonstration of the bottom-up mode.

## 2 · The grounding stance (honest — non-negotiable)

```text
GROUNDS ON   named public sources (research) + the model's current capability + our resource files
NOT          the public MCP · NOT model-gpr · NOT InfraSure proprietary data
FITS         the existing data_map: an `external`-DOMINANT read. The discipline is UNCHANGED — every material claim →
             named source + access date + confidence + fact|projection label; blocked_claims still block; gate still gates.
LABEL        always present it as RESEARCH-GROUNDED. Never as MCP / model-gpr / substrate-grounded product.
```

The A/B that keeps it honest: a vanilla LLM + web can write *a* narrative on the asset. So the value is **(1) the grounding/gate discipline, (2) the reusable method, (3) the framing we bring** — not data. If those three aren't present, don't ship it.

## 3 · The playbook (the steps — a guided-reasoning program, docs not engine)

```text
1. CLASSIFY     is the asset off-substrate? what CLASS is it (off-grid/remote · cold-region/Arctic · coastal · …)?
2. ASSEMBLE     build the exposure profile asset-by-asset from PUBLIC sources (there is no registry) —
                power source, logistics/resupply window, foundations, water, the class hazard stack
3. APPLY        the class hazard taxonomy + citable FRAMEWORKS + a realized PRECEDENT (§4)
4. GROUND       every claim → named source + date + confidence + fact|projection
5. NAME GAPS    the undisclosed asset-level numbers ARE findings (days-of-autonomy, dam factor-of-safety,
                foundation engineering, asset-level financials) — never fill a gap with a guess
6. FRAME        the decision (for an existing asset: the ADAPTATION lever + the economics it collides with)
7. GATE         block what we can't model — no $ EAL/PML, no return-periods, no plant-level forecast, no single-cause
8. RENDER       (post-gate only) the artifact, leading with OUR distinctive framing (for energy assets: the
                energy + logistics exposure), honesty-labelled research-grounded
```

## 4 · Defining the class (so the method generalizes)

A worked outlier should abstract to a **class**, so the next one is cheap. The first class (from Red Dog):

```text
CLASS: remote, off-grid, cold-region / Arctic INDUSTRIAL asset
  TWO coupled traits: (1) islanded on a diesel/HFO microgrid · (2) one climate-sensitive seasonal logistics window
  HAZARD STACK: permafrost (foundation bearing-capacity + watershed chemistry) · a wetter Arctic (water containment)
                · coastal erosion · freeze-thaw · tundra wildfire
  FRAMEWORKS (citable): IPCC AR6 WG2 CCP6 (Polar) · Hjort 2018 (pan-Arctic infra; "for an existing asset, ADAPTATION
                not decarbonization is the lever") · AMAP/SWIPA · Rantanen 2022 (~4× warming, models under-state it)
  PRECEDENT (realized): Norilsk 2020 — a diesel tank on thaw-weakened piles → ~21,000 t spill, ~$2B (the geometry, realized)
```

For a **new** outlier (a copper mine, a port, a remote data center): re-run steps 1–8, swapping the class hazard stack + frameworks + a class-relevant precedent. Reuse the *structure*, not Red Dog's specifics.

## 5 · What it composes

```text
this playbook (the mode)  +  the `_method` primitives (screen/rank/score · non-stationarity · EVT — `../../resources/_method/`)
  +  the CLOUD SKILL (deep public research)  +  the MODEL's capability
  +  (minimal) the MCP — only for a competitive/peer overlay if any in-substrate asset is comparable (often none)
```

## 6 · Scope guards

```text
1. TAGGED EXCEPTION — the off-scope / research-grounded lane, clearly labelled; NOT a pivot of the substrate core.
2. HONESTY — research-grounded, never presented as substrate / MCP / model-gpr product.
3. DON'T DUPLICATE prior work — be ADDITIVE (current · our framing · generalizable · gap-honest) or don't ship.
4. DON'T OVER-QUANTIFY — gaps are findings, not guesses; the model-gpr-class numbers stay blocked.
5. REUSABLE METHOD = the anti-drift guard; keep the META lean — formalize a standalone "ad-hoc framework" only
   after a SECOND outlier proves the pattern (don't build the meta ahead of evidence).
```

## 7 · Worked example — Red Dog Mine

`../extra/reddog_bottom_up_report_2026-06.md` (the report) + `../discussion/2026-06-14_outlier_method_red_dog.md` (the discussion + full sourced evidence). It applied steps 1–8 to the Arctic-industrial class, led with the **energy-logistics chokepoint**, corrected the existing deck's stale points, and named its gaps as findings.

---

**See also**: `../plans/2026-06-14_outlier_showcase_red_dog.md` (the plan) · `../discussion/2026-06-14_outlier_method_red_dog.md` (the discussion) · `workflow_recipes.md` (the recipe shape this playbook follows) · `data_map.md` (the `external` input-job this leans on) · `analysis_families.md` (the families a substrate read uses; this read is off-substrate) · `../use_cases.md` (the bottom-up/top-down buckets this refines) · `../principles.md` (P2 content-downstream · P6 references-inform) · `../../resources/_method/README.md` (the primitives it composes).
