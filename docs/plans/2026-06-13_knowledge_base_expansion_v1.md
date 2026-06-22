# Plan — Knowledge-Base Expansion v1 (the authored-intelligence scaffold + the first hazard-led resource wave)

> **Status**: **COMPLETE** — Phases 0–4 ✅ done (2026-06-14). The authored-intelligence scaffold (recipe layer + `_method` + maturity fields) is built; Wave-1 = **5 validated resources** across all 3 pillars (ENSO · hail · heat · hurricane/wind · offtaker), each test 001 PASS; and **one recipe is proven** end-to-end (`../method/workflow_recipes.md` §7). Kept in `plans/` (not yet moved to `done/`) because it is densely cross-referenced by the resource packages + ledger — it archives to `done/` when its successor (Wave-2 / near-queue) opens and the links are reconciled in one pass. Activated 2026-06-14 after `done/2026-06-13_docs_reorg.md`. Born from two resolved discussions (`../discussion/2026-06-13_expanding_the_knowledge_base.md` + `../discussion/2026-06-13_architecture_lessons_anthropic_fs.md`) and an adversarial verification pass (faithfulness · canon-consistency · grain-soundness), then re-prioritized 2026-06-14 to the product's true spine (hazard-led).
>
> **What InfraSure is** (the frame this plan serves, now canon in `../architecture.md` §1): a **climate & weather risk-analytics platform for energy infrastructure**. The resource spine is three pillars that resolve into dollars:
>
> ```text
> (HAZARD × asset-class)   hail×solar · wildfire×transmission/battery · hurricane/wind×wind · flood×solar
> (WEATHER × asset-class)  ENSO×solar · heat-derate×(solar/gas/battery) · drought×hydro
> (COMMERCIAL)             offtaker / PPA / insurance — the $ layer the other two RESOLVE INTO
>                          e.g. hail → a solar fleet's panels → a hail-insurance dollar claim
> ```
>
> **Center of gravity**: resource expansion, step by step, **hazard-led**. Phases 0–1 are cheap-docs preamble (the scaffold every resource inherits); Phases 2–3 are the bulk (author + manually test resources); Phase 4 exercises one recipe. If scaffold work balloons, cut it.

## 1 · What This Plan Does

Turn the one validated resource (`el_nino_enso`) into a small, grounded, hazard-led catalog that matches the live product — without category sprawl, ungroundable resources, or building a runtime. It (a) names the **authored-intelligence scaffold** (recipe layer + `_method` primitives, docs-only), (b) adds sequencing metadata that keeps expansion grounding-led, then (c) authors and manually tests **4 new resources** spanning the three pillars, and (d) proves the recipe layer on one end-to-end run.

```text
PHASE 0  settle canon (reframe · L0/L2 + no-code rail · no-finance · frozen families · grain)   cheap-docs   ✅ DONE
PHASE 1  author the scaffold (recipe layer named · _method/ layer · templates/ · maturity fields) cheap-docs   ✅ DONE
PHASE 2  grain freeze applied + Wave-1 slate committed + the FLAGSHIP resource (hail_solar)        moderate     ✅ DONE
PHASE 3  Wave-1 breadth: +heat×solar +hurricane/wind×wind +offtaker (3 pillars exercised)          heavy        ✅ DONE
PHASE 4  exercise ONE recipe end-to-end (screen a solar fleet: hail → exposure → insurance $)       moderate     ✅ DONE
         ───────────────────────── PLAN COMPLETE (Phases 0–4 ✅) ─────────────────────────
```

## 2 · Settled Decisions (committed up front — the contract)

These resolve both discussions' open questions and the adversarial findings; a change is a versioned amendment, not a drift (P5).

| # | Decision | Resolution | Status |
|---|---|---|---|
| D1 | **Product framing** | InfraSure is a **climate & weather risk-analytics platform for energy infrastructure** — an **intelligence system whose reasoning is evidence-disciplined**; the gate is the **firewall, not the purpose**. The spine = (hazard × asset) + (weather × asset) + commercial → dollars. | ✅ in `architecture.md` §1 |
| D2 | **L0 scaffold vs L2 orchestration** | Authored **scaffold** (recipes, `_method`, family map, grammar) = **STABLE/L0**. Planning+synthesis **orchestration** = **VOLATILE/L2 = the model's job**. | ✅ in `principles.md` P1 corollary |
| D3 | **No-code rail** (bound, not implicit) | A recipe / `_method` artifact is a **docs/spec the model READS, never an engine we BUILD**. No `code/`, `scripts/`, `agent.yaml`, orchestrator. Explicit acceptance criterion on every phase that touches them. | ✅ in `principles.md` P1 corollary |
| D4 | **No `finance` domain** | Five domains stand (`weather_and_climate · hazard · market · policy · commercial`); finance/insurance/math → **`_method/`** shared layer. | ✅ recorded in `resources/README.md` |
| D5 | **7 families frozen** for this expansion | Author against the existing families; don't reconcile against the vault's analytical-mode taxonomy now. | logged |
| D6 | **Grain = the (driver × MECHANISM) cell** | Mechanism is the real key (drives `blocked_claims`/`confidence_rules` — the moat); driver is the **folder** grouping (shared retrieval machinery); asset-class & actor are **facets**; a split fires whenever the mechanism differs — for `hazard` that is **by default** (hail×solar ≠ hail×gas ≠ wildfire×transmission). | ✅ recorded in `resources/README.md`; Organizing-Model edit in Phase 2 |
| D7 | **Second resource class** | (1) driver-keyed methodology packages in the domain tree; (2) non-driver **`_method` primitives** (damage functions, DSCR, EVT, insurance/materiality) that recipes **CALL** but never ground. Gives the vertical hazard→…→$ chain something to compose. | Phase 1 |
| D8 | **Recipe layer = named docs concept** | `{ job · ordered resources · `_method` primitives called · checkpoint · gate · render target }`. Name now; no catalog; exercise one in Phase 4. | Phase 1 |
| D9 | **Maturity + peril fields** | `grounding_maturity` (`substrate-only \| model-not-wired \| needs-data`) + `data_maturity` (H/M/L) set the confidence ceiling + build order. Peril-CSV columns become the `resource.yml` shape for peril resources. Non-stationarity → standard `confidence_rule` for climate. | Phase 1 |
| D10 | **Grounding-led, with the hazard exposure/loss split** | Sequence by *what the public MCP can ground today*. **Hazard EXPOSURE + EVENT-TRANSLATION are groundable now** (substrate + the `hazards` news category + one footprint feed → **directional**); **hazard LOSS/$** (EAL, PML, modeled peril-risk, insurance pricing) is **model-gpr** → ship directional, **log the gap**, quantify in a later wave. Apply the GATE-1 vanilla-LLM A/B before authoring each. | live rule |
| D11 | **Defer / reject discipline** | DEFER (validation checklist · publish/sync · marketplace index · Wave-2 model-gpr wiring) with explicit triggers. REJECT (three-tier taxonomy · managed runtime · subagents · partner connectors · artifact-first telos · thin guardrails · **planner runtime**) recorded once, not relitigated. | live rule |

## 3 · The Phase Ladder

Each phase: **goal · deliverables · canon amendments · acceptance · status**. No later-phase *deliverable* lands before the active phase closes; the sanctioned parallel exception is **raw-material gathering** (peril CSVs, candidate research, exemplar collection).

### Phase 0 — Settle canon  ·  `cheap-docs`  ·  **status: ✅ DONE (2026-06-14)**

> **Goal**: land the decision-resolving, versioned canon amendments (D1–D6) so no later phase carries an open or canon-conflicting decision.

```text
LANDED THIS PHASE
  ✅ architecture.md §1 — the climate-&-weather-risk product framing + gate-as-firewall reframe (Status bumped)
  ✅ principles.md P1   — the L0(scaffold,stable)/L2(orchestration,volatile) corollary + the no-code rail (Status bumped)
  ✅ principles.md P6   — the asymmetry guard ("borrow form/packaging; never trade the gate for thinner guardrails")
  ✅ resources/README.md — recorded D4 (no finance domain) + D6 (grain = driver×mechanism cell)
  ✅ both discussion docs — Status → RESOLVED-INTO-PLAN, pointing here
  ✅ done/ discipline established; docs_reorg plan closed + archived to done/; this plan activated
ACCEPTANCE (met): the canon docs carry the reframe + L0/L2 + no-code rail with bumped Status; D4/D6 recorded;
                  discussions resolved-into-plan. No folders, no resources touched.
```

### Phase 1 — Author the scaffold  ·  `cheap-docs`  ·  **status: ✅ DONE (2026-06-14)**

> **Goal**: materialize the minimal STABLE scaffold the resource waves inherit — recipe layer named (no engine), `_method/` layer stood up, the package **`templates/`** the `/new-resource` command assumes, and maturity/peril fields added to the standard. All docs; the model reads it, nothing executes it.

**✅ Landed (2026-06-14)**: `docs/method/workflow_recipes.md` (recipe layer named + the no-code rail) · `resources/_method/README.md` (the seeded screen/rank/segment/score skeleton + non-driver primitive stubs + the two-class admission) · `resources/templates/` (README + 8 templates — fixes the `/new-resource` gap, now carries maturity/peril fields) · `resource_standard.md` (maturity + peril-field standard + non-stationarity rule) · `resources/README.md` (tree + Shared Layers `_method` row + quarantine/two-class note) · `docs/README.md` index + dangling-link fixes from archiving the reorg plan.

```text
DELIVERABLES
  · NAME the recipe layer in docs (new docs/method/workflow_recipes.md, NOT a runtime) with the in-doc acceptance
      line "recipe = docs/spec, never a planner/orchestrator; no code/, no scripts/". Name only — NO catalog.
  · MATERIALIZE resources/_method/ (underscore rule: no resource.yml, excluded from discovery, quarantined from
      grounding). Seed: the screen/rank/segment/score skeleton lifted from ENSO's "Required reasoning steps"; a STUB
      home for non-driver method (damage functions, insurance/materiality, DSCR, EVT). Register in Shared Layers.
  · ADMIT the two-resource-class distinction (D7) in resources/_method/README.md + resources/README.md.
  · CREATE resources/templates/ — the package skeleton /new-resource Phase 1 assumes but that doesn't exist today
      (resource.md/.yml · knowledge.md · prompt_projection.md · data_requirements.md · SKILL.md · examples/ · test_runs/),
      distilled from the el_nino_enso package. Fixes the command/repo gap; standardizes every future package.
  · AMEND resource_standard.md: grounding_maturity + data_maturity (D9); the peril-field standard (predictability ·
      key-datasets · climate-attribution-confidence · financial-materiality · insurance-treatment); non-stationarity rule.
CANON AMENDMENTS:  new docs/method/workflow_recipes.md · new resources/_method/README.md · new resources/templates/
                   · resource_standard.md · resources/README.md (Shared Layers + two-class)
ACCEPTANCE:        recipe layer named with the no-code line; _method/ exists, registered, seeded + two-class admitted;
                   templates/ exists; resource_standard carries maturity + peril + non-stationarity.
                   NO recipe authored, NO _method math beyond stubs, NO resource authored.
```

### Phase 2 — Grain freeze applied + Wave-1 slate + the FLAGSHIP (`hail_solar`)  ·  `moderate`  ·  **status: ✅ DONE (2026-06-14)**

> **Goal**: begin the center of gravity with the **flagship of the live product** — author + manually test the hail×solar resource, which is the strongest-grounded resource available (the Texas Fighting Jays event is in the substrate) and exercises the most new machinery (hazards-news + a footprint feed + the maturity/peril fields + a `_method` call).

**✅ Landed (2026-06-14)**: grain re-key applied to `resources/README.md` §Organizing Model · Wave-1 slate committed (§4) · **`resources/hazard/hail_solar/`** authored (9 files: resource.yml/.md · knowledge · prompt_projection · data_requirements · SKILL · examples/applied_insight_001 · test_runs/test_run_001 · README) · **live MCP test 001 PASS** (the hail impact is *observable in the generation CF*: Aug 2023 0.37 → Aug 2024 0.15 → Aug 2025 0.33; $ layer correctly blocked) · `hazard/` domain materialized · Registry row added · gaps logged (R1 ERCOT repeat · new R12 hazard peril-model). The reusable hazard pattern (substrate + hazards-news + VERIFY → directional, log the $ gap) is proven for `hurricane_high_wind_wind`.

```text
DELIVERABLES
  · APPLY D6 to resources/README.md §Organizing Model (grain = driver×mechanism cell; mechanism the key, driver
      the folder grouping; for hazard the asset-class split fires by default; persona/actor a facet).
  · COMMIT the Wave-1 slate (§4) as a settled sub-decision here.
  · AUTHOR resource #2: hail_solar (hazard · Exposure + Event-Translation · solar) via /new-resource. Materialize
      the hazard/ domain folder on this first resource. grounding_maturity = substrate-only (directional).
      Grounds on: search_news(category=hazards, query="hail") → hazard_type·affected_area·operational_impact·
      affected_mw·event_date (worked example: Fighting Jays, plant 62945, ERCOT, CIP-owned); get_plant geometry/
      owner; search_plants(fuel=SUN,state)+nearby_plants for footprint; external NOAA-SPC hail feed (live, dated).
      BLOCKED (log the gap): modeled hail return-period/swath risk (external model) + EAL/PML/$ damage/insurance
      pricing (model-gpr). Method MUST include a VERIFY step — the hazards classifier has false positives.
  · RUN the manual loop (test_protocol.md); save the FULL transcript; resolve into test_runs/; log gaps to mcp_gaps.md.
      Add the Registry row.
CANON AMENDMENTS:  resources/README.md (Organizing Model — grain); new hazard/ domain folder; Registry row
ACCEPTANCE:        grain re-keyed + frozen; Wave-1 slate committed; hail_solar authored, manually tested
                   (PASS or logged fail→fix), test_run saved, Registry + gaps updated. New scaffold fields +
                   ≥1 _method primitive used by a real resource; the hazards-news verify step proven.
```

### Phase 3 — Wave-1 breadth: +`extreme_heat_derate` +`hurricane_high_wind_wind` +`offtaker_concentration`  ·  `heavy`  ·  **status: ✅ DONE (2026-06-14)**

> **Goal**: complete Wave-1 so all **three pillars** are exercised across solar + wind + the commercial layer — heterogeneous resources the recipe (Phase 4) can compose.

**✅ Landed (2026-06-14)** — authored + live-tested via the `wave1-breadth-author` workflow (3 parallel agents, each grounded against the MCP, each test 001 PASS):
- **`extreme_heat_derate`** (weather × solar · `substrate-only`) — anchor Aktina Solar (64927); resisted the over-magnitude trap (used the *high* summer CF to **bound** the claim down, LOW by design, reframed as ERCOT peak-coincidence).
- **`hurricane_high_wind_wind`** (hazard × wind · **`model-not-wired`**) — TX = #1 wind (49.7 GW); Beryl/Matagorda corridor; the honest finding: **no separable Beryl signal in the CF** (2024-07 CF = the no-storm 2021-07 lull) → capped MEDIUM, blocked CF-attribution, split cut-out vs damage; VERIFY caught hazards-news links to nuclear/hydro/gas, not wind.
- **`offtaker_concentration`** (commercial · first **FACTUAL** resource) — Amazon book (≥12 entities, 5 verified) vs the merchant TX tail; found `offtakers` array null (grounds on `news_extracted.buyer`), confirmed R9 live, caught a cross-tagged `deal_value_usd`.

Registry rows added · `commercial` domain materialized + `hazard`/`weather_and_climate` extended · gaps logged (R1 wind repeat · R9 live · R12 extended · new **R13** offtaker grounding). All three held the discipline (per-part confidence · blocked the model-gpr $ · omit-don't-infer).

```text
DELIVERABLES
  · AUTHOR #3 extreme_heat_derate (weather · Exposure · solar; thermal de-rate). grounding_maturity = substrate-only,
      WEATHER-DIRECTIONAL like ENSO (NOAA temp + asset thermal characteristics) — NOT a news-event resource (heat news
      is thin/noisy). BLOCKED: plant-level output forecast (no model). [extensible to gas/battery later — scope to solar now.]
  · AUTHOR #4 hurricane_high_wind_wind (hazard · Exposure + Event-Translation · wind). Reuses the hazard/ folder +
      the hazards-news + footprint-feed machinery hail_solar built. grounding_maturity = substrate-only directional;
      external feed = NHC track / wind field. BLOCKED: modeled wind-loss + $ (model-gpr).
  · AUTHOR #5 offtaker_concentration (commercial · Commercial · factual). Materialize the commercial/ folder.
      grounding_maturity = substrate-only; leans on find_by_extracted_fact (the "DIFFERENTIATOR"). First FACTUAL
      (non-directional) resource — tests resolved-fact confidence + partial-coverage / omit-don't-infer caveats.
  · Each: GATE-1 vanilla-LLM A/B BEFORE authoring; manual loop; transcript → test_runs/; log gaps; Registry row;
      confirm the frozen grain (driver×mechanism, actor as facet).
CANON AMENDMENTS:  new commercial/ domain folder; Registry rows
ACCEPTANCE:        validated resources = ENSO + hail_solar + heat + hurricane/wind + offtaker (4 new), spanning all
                   3 pillars and ≥3 domains; each with a saved test_run + Registry row; gaps ledgered. Precondition
                   for a recipe (≥2 heterogeneous composable resources) is met.
```

### Phase 4 — Exercise ONE recipe end-to-end  ·  `moderate`  ·  **status: ✅ DONE (2026-06-14)**

> **Goal**: with the hazard resources existing, author and manually run ONE recipe to PROVE the recipe layer — and test the hardest grain claim: does composing driver-keyed resources express the job, including whether the **vertical** hazard → exposure → **insurance $** leg composes via the non-driver `_method` primitives (D7)? Still docs-only.

**✅ Landed (2026-06-14)** — authored + ran `screen_solar_hail_to_insurance_exposure` end-to-end as a manual loop (`../method/workflow_recipes.md` §7). **Verdict: the recipe layer + the two-resource-class model (D7) HOLD.** The parallel fan-out composed cleanly (hail_solar + extreme_heat_derate scored the same TX fleet — no forking); the vertical insurance-$ leg — *the grain-verification's predicted sharp edge* — **composed via the `_method insurance_materiality` primitive** (class (2) gave it a legitimate home), running directional with the $ correctly **blocked** to model-gpr. Honest limitation logged: the `_method` primitives are stubs, so the vertical scoring is qualitative — the recipe is the forcing function that defines their contract. No catalog, no engine, no code (P1 held).

```text
DELIVERABLES
  · AUTHOR one recipe in docs: screen_solar_hail_to_insurance_exposure — compose hail_solar (+ heat) as the PARALLEL
      fan-out across a solar fleet, and CALL the _method insurance/materiality primitive for the VERTICAL $ leg
      (directional — the modeled-$ stays the logged model-gpr gap). Deliberate test of grain-finding #2.
  · RUN it as a single manual Claude-session loop (resolve scope → select resources → fan out across the fleet →
      score exposure/materiality/confidence via _method → drill top cases → assemble → GATE → render post-gate).
      Save the full transcript.
  · RESOLVE into a test_run; capture: did it compose? parallel fan-out work? did the vertical/$ leg find a _method
      primitive to call, or hit a gap? Log gaps. Reconcile to the grain freeze (composes / partial / breaks-here-logged).
      Add the recipe as the first worked example. NO catalog.
CANON AMENDMENTS:  docs/method/workflow_recipes.md (first worked example); recipe test_run
ACCEPTANCE:        one recipe authored + run end-to-end with a saved transcript + resolved test_run; a clear verdict
                   on the vertical $ chain; gaps ledgered. No catalog, no engine, no code.
```

## 4 · Wave-1 Slate (committed in Phase 2)

Hazard-led, three pillars, solar + wind; none depends on a model-gpr-only field for its *core* claim (the $ layer is logged + directional).

| # | Slug | Pillar · Domain · Family | Driver × mechanism | grounding | Grounds on (verified) / what stays blocked |
|---|---|---|---|---|---|
| 2 | **hail_solar** | HAZARD · `hazard` · Exposure+Event | hail × solar-panel/tracker damage | substrate-only | `search_news(category=hazards)` (679 hazard arts; **Fighting Jays** plant 62945, affected_mw·damage·event_date) · `get_plant` geometry/owner · `nearby_plants` · NOAA-SPC hail feed. **Blocked**: modeled hail risk (feed) · EAL/$/insurance pricing (model-gpr) |
| 3 | **extreme_heat_derate** | WEATHER · `weather_and_climate` · Exposure | extreme heat × thermal de-rate (solar) | substrate-only | NOAA temp + `get_plant.generation` CF baseline + thermal characteristics — ENSO-style directional. **Blocked**: plant-level output forecast |
| 4 | **hurricane_high_wind_wind** | HAZARD · `hazard` · Exposure+Event | hurricane / high wind × wind-turbine load | substrate-only | reuses hail's hazards-news + footprint machinery · `search_plants(fuel=WND)` · NHC track/wind-field feed. **Blocked**: modeled wind-loss + $ (model-gpr) |
| 5 | **offtaker_concentration** | COMMERCIAL · `commercial` · Commercial | offtaker / PPA counterparty concentration | substrate-only | `find_by_extracted_fact` (buyer·ppa_type·ppa_price) — the "DIFFERENTIATOR" · `get_plant.offtakers` · `plants_by_owner`+`aggregate`. **Blocked**: forward $/MWh re-contracting (model-gpr) |

**Near queue (Wave-1.5 / 2)**: `wildfire×transmission/battery` (2nd strong hazard — also richly grounded: PSPS, the Irving Storage battery case) · `drought_low_hydro` (weather×hydro) · `hurricane_coastal_flood` (needs a flood feed) · `queue_delay_risk` (still valid; not core to the climate-risk spine). **Wave-2** (wire model-gpr): the modeled-$ / EAL / insurance-pricing upgrade across the hazard resources.

## 5 · Scope Guards (the rails — apply every phase)

```text
1. CENTER OF GRAVITY = resources, HAZARD-LED. Phases 0–1 are cheap-docs preamble; if they balloon, cut them.
2. NO `finance` domain (D4). Finance/insurance/math = `_method/` content.
3. Recipe layer + `_method` are DOCS the model READS — never an engine/planner/orchestrator/code (D3, P1).
4. Grain = (driver × MECHANISM) cell (D6). For hazard the asset-class split fires by DEFAULT; don't under-count.
5. The vertical hazard→exposure→$ chain composes from NON-driver `_method` primitives (D7), not a driver resource.
6. Don't author a recipe / run one before ≥2 heterogeneous resources exist (Phase 4 gated on Phase 3).
7. Grounding-led (D10): hazard EXPOSURE/EVENT ships directional now; hazard LOSS/$ is model-gpr → log the gap,
   never assume the field. Apply the GATE-1 vanilla-LLM A/B BEFORE authoring each.
8. HAZARD-NEWS HAS CLASSIFIER NOISE (a "hails decree" reg article and a boiler explosion both mis-tagged) — every
   hazard resource's method MUST include a VERIFY step (CLAUDE.md "don't trust tool labels").
9. HEAT is a WEATHER-DIRECTIONAL resource (NOAA temp + de-rate), NOT a news-event one — heat news is thin/noisy.
10. DATACENTERS likely sit in a SEPARATE substrate (not the generation-plant MCP) — grounding-check before any
    datacenter resource; do not assume the public MCP covers them.
11. No unscoped scans in any test (one region · one asset class); save the FULL transcript, then resolve to a test_run.
12. DEFER rows stay deferred with triggers; REJECT rows recorded once, not relitigated (D11).
13. Canon edits are VERSIONED amendments (Status bump, P5) landing WITH their owning phase — one at a time.
14. Every MCP friction point → mcp_gaps.md (gap · workaround · roadmap) before working around it.
```

## 6 · What This Plan Does NOT Touch (recorded once)

```text
DEFER (trigger-gated, P5):   validation invariant checklist (trigger: 2nd/3rd resource) · trigger-rich discovery
                             descriptions (trigger: discovery tool built) · publish/sync + marketplace index
                             (trigger: >1 discoverable resource) · Wave-2 model-gpr wiring (trigger: the modeled-$
                             / EAL / insurance-pricing upgrade on the hazard resources)
REJECT (do-not-relitigate):  three-tier plugin taxonomy · managed-agent runtime · subagent choreography ·
                             partner connectors · artifact-first telos · thin guardrails · planner/orchestrator runtime
```

---

**See also**: `README.md` (the lifecycle + the live index) · `done/2026-06-13_docs_reorg.md` (the plan whose closure freed this one) · `../discussion/2026-06-13_expanding_the_knowledge_base.md` + `../discussion/2026-06-13_architecture_lessons_anthropic_fs.md` (the two discussions this resolves) · `../architecture.md` §1 (the product framing this serves) · `../principles.md` (P1 corollary + P6 asymmetry guard, landed in Phase 0) · `../method/resource_standard.md` (the contract Phase 1 amends) · `../method/analysis_families.md` (the frozen 7 families) · `../../resources/README.md` (the spine + Shared Layers Phase 1 extends) · `../../.claude/commands/new-resource.md` (the per-resource engine Phases 2–3 run) · `../status/mcp_gaps.md` (the gap ledger every phase feeds).
