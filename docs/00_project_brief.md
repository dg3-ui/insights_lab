# 00 - Project Brief

> **Status**: v0 brief, updated 2026-06-08 — the **single overview** of the project (goal · architecture · scope · principles), drawn. V0 validated (Test 001 PASS); methodology layer hardened.
>
> **Audience**: seniors reviewing the direction and juniors executing the first resource package.
>
> **Grounded in**: live InfraSure MCP output, 2026-06-05 — the real entities below are pulled, not invented.
>
> **How to read this**: this is the one place that describes the whole project. It *summarizes and points*; the deep docs own the detail — scope (`01`), architecture (`06`), principles (`08`).

## 0 · What We're Building (3 pillars)

At the highest level the project is three things — two foundations and the agent that combines them:

```text
  PILLAR 1 · MCP           PILLAR 2 · REFERENCE / KB      PILLAR 3 · COMBINED AGENT
  data tools               methodology + knowledge         1 + 2 + agentic architecture
  "what is true"           "how to reason"                 "a useful tool for TEAM + CLIENT"
  ✅ built                 ✅ initial build                 ◀── the big open work
        │                        │                               │
        └──── REFINE + VALIDATE ──┘                              DEFINE THE USE CASE
                (rigorous testing)                                (two buckets — see 11)
```

Pillars 1 and 2 are built and now in **refine + validate** (prove the curated tool/reference beats a vanilla query). Pillar 3 is the open work — its use-case shape (two buckets × two audiences) is detailed in `11_use_cases.md`, and the whole-project panorama lives in `01_scope_v0.md`. The rest of this brief is the methodology layer that spans Pillars 2 → 3.

## 1 · The Goal — add the second surface (the moat)

InfraSure Insights is the **methodology / reasoning layer** above InfraSure's asset, ownership, offtaker, news, generation, and context substrate. It should not produce generic market commentary — it should produce infrastructure decision intelligence. The platform already has data access (the MCP tools). The missing layer is a methodology-backed analyst: a structured resource that tells the model what to retrieve, how to reason, what *not* to claim, and how to score confidence. **The moat is grounding, not fluency.**

```text
        InfraSure has ONE surface today.  This project adds the SECOND.

   ┌──────────────────────────┐              ┌──────────────────────────┐
   │   axis 1: DATA            │              │   axis 2: METHODOLOGY     │
   │   "what is true"          │              │   "how to reason"         │
   │   search_plants·get_plant │              │   el_nino_enso · (drought │
   │   aggregate·find_by_fact  │              │    wildfire·curtailment…) │
   │   ✅ LIVE TODAY           │              │   ◀── THIS REPO           │
   └────────────┬─────────────┘              └────────────┬─────────────┘
                └──────────────┬──────────────────────────┘
                               ▼
            "here is the data, AND here is how an
             InfraSure analyst reasons over it"   ──►   THE MOAT
                               │                         (a vanilla LLM
                               ▼                          copies NEITHER)
   grounded condition + scoped entities + mechanism + source refs
     + confidence/caveats + actor relevance   =   an InfraSure Insight
                               │
        commentary ✗  "El Niño may affect US electricity markets."
        insight    ✓  "El Niño Watch DJF 26-27 → wetter CA winter →
                       downside to winter solar CF across CA ≥50MW fleet
                       (Topaz 57695, Desert Sunlight 57993); owners
                       Clearway/BHE + offtaker PG&E should watch; LOW
                       confidence; no $/MWh claim."
```

## 2 · The Architecture — repo → served → runtime → output

Four layers. The runtime is a **loop with a human checkpoint**; the output (the content engine) renders only *after* the gate. Full detail: `06_architecture.md`.

```text
LAYER 0  SOURCE     this repo: authored, versioned methodology packages
   │                  resource.yml · prompt_projection · knowledge.md · examples/ + test_runs/
   ▼  publish (repo is SOURCE, not the served thing)
LAYER 1  SERVED     InfraSure MCP (DATA tools, live)  +  skill catalog (one skill per package)
   │                  find_methodology / get_methodology  ◀── discovery via resource.yml.taxonomy
   ▼
LAYER 2  RUNTIME    a Claude session = the "agent":  discover → load → ground → assemble → GATE
   │                  ▲___________ human checkpoint (enrich · re-scope · challenge) ___________│  (a LOOP)
   ▼  validated insight object
LAYER 3  OUTPUT     the CONTENT ENGINE: blog · brief · email · post — per the _style output
                      contract (direction × audience × format; resources/_style/)
                      = renderings of a VALIDATED insight, never before the gate (08 P2)
```

The substrate (~15.5K plants · ~29.7K generators · ~9.8K queue projects · ~57K news articles) and its **12 read-only MCP tools** exist today — an *expandable floor*, not a fixed surface (`learning/01`). `resource.yml` is the load-bearing seam: taxonomy → discovery, prompt sections → the served method, confidence_rules + blocked_claims → the gates.

## 3 · Why It Matters — the actors (grounded)

InfraSure's core users need decision-grade risk intelligence. Grounded against one real CAISO solar asset — **Desert Sunlight 300** (plant `57993`, 313.7 MW, Riverside County; owner Clearway Energy; offtaker Pacific Gas & Electric):

| Actor | Question | Insight job | Real hook on this asset |
|---|---|---|---|
| Owner / operator | What action does this asset need? | Surface exposure, operating relevance, resilience levers | Clearway: winter-irradiance variance on a ~0.24 capacity-factor asset |
| Investor | What changes the downside / terminal-value case? | Conditions → risk concentration + portfolio implications | TotalEnergies / BlackRock up the chain: CA-solar concentration |
| Lender | Does this asset stay financeable under stress? | Physical/market stress → credit, covenant, monitoring | $160.95/MWh PG&E PPA to 2039 — revenue-stress sensitivity |
| Offtaker / counterparty | Which linked assets or regions matter to us? | Power-supply exposure → commercial relationships | PG&E holds 28 contracts on this single asset |

Outreach is **not** the source of truth — it is a **rendering** of a validated insight (`08` P2; the content engine is `06` Layer 3).

## 4 · How The Insight Is Produced And Protected

Four fundamentals (`learning/02`–`03`) and five principles (`08_design_principles.md`) hold it together:

```text
RULE A · every input does ONE job — label it before citing it
         GROUNDS (capacity·CF·PPA·node) · FRAMES (descriptions/Wiki — never proof) ·
         ROUTES (owner·offtaker) · EXTERNAL (NOAA causal state) · LOGIC (crosswalks) ·
         FORM (resources/_* style·exemplars — shapes the rendering, never grounding)
RULE B · every material claim = 7 slots:
         condition + scoped entities + mechanism + evidence + confidence + caveat + actor
         (a slot you can't fill = a downgrade or a blocked claim)
RULE C · a resource is a CONTROL SURFACE, not an essay
         allowed_claims = ceiling · blocked_claims = floor (the heaviest-lifting field)
RULE D · the MCP surface is a FLOOR, not a ceiling — a gap is a roadmap input (→ docs/09)

P1 stable methodology / swappable execution   P2 content downstream of a validated insight
P3 process data obeys the asset-data laws      P4 iteration is expected   P5 flexibility ≠ no commitment
```

Two feedback loops grow the platform each time the method is exercised:

```text
PROCESS loop   test transcript ─► resolve ─► test_run + extraction   (sharpens prompts/evals — 05 · 08 P3)
TOOL loop      "this call would help" ─► docs/09 ledger              (grows the 12-tool floor — learning/01)
```

The lifecycle is packaged as commands — `/new-resource` · `/test-resource` · `/extract` · `/recap` (`10_command_roadmap.md`).

## 5 · Scope & Status (V0)

```text
   V0 PROVES ONE THESIS, manually:
      IF Claude has (1) MCP tools (2) one methodology resource (3) a clear prompt projection
      THEN it can draft one grounded applied insight (refs · confidence · caveats · actor).

   ┌──────────── INSIDE V0 ────────────┬─────────── OUTSIDE V0 ───────────┐
   │ one ENSO methodology package      │ production agent / orchestrator   │
   │ one prompt projection             │ API integration / DB schema       │
   │ ONE manual MCP/Claude test        │ automated batch / email           │
   │ one applied-insight draft         │ new MCP tools (unless gap proven)  │
   │ one learning / gap log            │ exact LMP / $/MWh · national scans │
   │ "MCP-READY" ─────────────────────►│ "MCP-INTEGRATED"                  │
   └────────────────────────────────────┴───────────────────────────────────┘

   STATUS LADDER (2026-06-08):
     [✅] data tools (MCP) live          [✅] source repo + taxonomy registry
     [✅] ENSO skill authored (SKILL.md) [✅] Test Run 001 ── PASS (with logged gaps)  ◀ HERE
     [◑ ] find_methodology discovery ── spec'd, not built
     [☐ ] publish step · [☐ ] eval harness ── design only (paused; must eat PROCESS data first)
```

**Where things stand (2026-06-08):** V0 is validated — Test 001 PASS (the ENSO skill drafted a grounded, LOW-confidence, source-referenced directional insight and correctly *blocked* the quantitative overclaims). Since then the methodology layer was hardened — principles (`08`), the MCP ledger (`09`), the command toolchain (`10`), and agent files. The publish step, discovery tool, and eval harness remain **deliberately paused** until the test/extract loop has run across more cuts. Full scope + the after-V0 split: `01_scope_v0.md`.

## 6 · First Topic — ENSO

The first resource is **El Niño / ENSO exposure** because it stress-tests the methodology layer: external data with its own freshness clock (NOAA CPC ENSO state — *not* in the substrate), region crosswalks from climate geography to InfraSure entities, asset fan-out across plants/portfolios/owners/offtakers, mixed claim types, and actor-specific relevance. The clean v0 chain (no exact-LMP forecasting):

```text
ENSO state / forecast ─► regional irradiance tendency ─► affected asset / fleet
  ─► owner / offtaker / portfolio exposure ─► caveated, directional implication
```

Already grounded (2026-06-05): CA solar totals **36,843 MW** (`aggregate`); the operating ≥ 50 MW fleet includes Topaz Solar Farm (`57695`, 585.9 MW), Desert Sunlight 300 (`57993`), Darden I–IV (646 MW each). The seasonal capacity-factor baseline ENSO perturbs is retrievable per plant (summer ≈ 0.38, winter ≈ 0.13).

## Read Next

```text
docs/01_scope_v0.md                      -> the exact v0 deliverable + the after-V0 split
docs/02_analysis_catalog.md              -> the 7 analysis families (v0 = Exposure)
docs/03_methodology_resource_standard.md -> the contract every resource must meet
docs/06_architecture.md                  -> the 4 layers, the runtime loop, the content engine
docs/08_design_principles.md             -> the 5 principles (stable/volatile · content-downstream · …)
docs/09_mcp_roadmap.md                   -> the MCP feedback ledger (log tool gaps here)
docs/10_command_roadmap.md               -> the command toolchain (author -> test -> resolve -> gate -> render)
docs/11_use_cases.md                     -> the 2-bucket use cases (Pillar 3) + the validation method
docs/learning/                           -> onboarding: MCP basics, substrate, resources, prompt projection
```
