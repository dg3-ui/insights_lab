# 00 - Fundamentals Map (the visual on-ramp)

> **Status**: visual on-ramp, 2026-06-08.
>
> **Purpose**: the whole project in one place, drawn rather than described — the goal, the architecture, the scope, the fundamentals, the principles, and the two feedback loops. Read this first; it points into the prose docs for depth. ASCII is the medium on purpose: the shapes are the understanding.
>
> **Reads before**: `01_mcp_basics.md` → `02_infrasure_data_substrate.md` → `03_methodology_resources.md` → `04_prompt_projection.md`.

## 1 · THE GOAL — add the second surface

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
        commentary ✗  "El Niño may affect power markets."
        insight    ✓  "El Niño Watch DJF → wetter CA winter → downside to
                       winter solar CF across CA ≥50MW (Topaz 57695,
                       Desert Sunlight 57993); owners + PG&E watch;
                       LOW confidence; no $/MWh."
```

## 2 · THE ARCHITECTURE — four layers, repo → served → runtime → output

```text
LAYER 0  SOURCE     this repo: authored, versioned methodology packages
   │                  resource.yml · prompt_projection · knowledge.md · examples/ + test_runs/
   ▼  publish (repo is SOURCE, not the served thing)
LAYER 1  SERVED     InfraSure MCP (DATA tools, live)  +  skill catalog (one skill per package)
   │                  find_methodology / get_methodology  ◀── discovery via resource.yml.taxonomy
   ▼
LAYER 2  RUNTIME    a Claude session = the "agent":  discover → load → ground → assemble → GATE
   │                  (a LOOP with a human checkpoint — see §3)
   ▼  validated insight object
LAYER 3  OUTPUT     the CONTENT ENGINE: blog · email · card · post
                      = renderings of a VALIDATED insight, never before the gate (08 P2)
```

```text
   resource.yml is the load-bearing seam — ONE file drives THREE things:
        taxonomy ───────────► discovery   (which skill)
        prompt sections ────► the served method   (how to reason)
        confidence_rules + blocked_claims ──► the gates   (what to refuse)
```

## 3 · THE RUNTIME IS A LOOP, NOT A LINE

```text
   discover → load → ground → assemble → GATE ──pass──► validated insight ──► render
                       ▲                    │
                       └─── human checkpoint┘──fail──► BLOCKED
                          (enrich·re-scope·challenge·approve)   (empty scope / stale NOAA / overclaim)

   one-shot draft = a DRAFT.   the enrichment happens in the loop.
   the human checkpoint is the product — "more hands, more dimension", not overhead.   (08 P4)
```

## 4 · SCOPE & STATUS — narrow on purpose

```text
   ┌─────────── INSIDE V0 ───────────┬─────────── OUTSIDE V0 ───────────┐
   │ one ENSO methodology package    │ production agent / orchestrator   │
   │ one prompt projection           │ API integration / DB schema       │
   │ ONE manual MCP/Claude test      │ automated batch / email           │
   │ one applied-insight draft       │ new MCP tools (unless gap proven)  │
   │ one learning / gap log          │ exact LMP / $/MWh · national scans │
   │ "MCP-READY" ───────────────────►│ "MCP-INTEGRATED"                  │
   └─────────────────────────────────┴───────────────────────────────────┘

   STATUS LADDER (2026-06-08):
     [✅] data tools (MCP) live
     [✅] source repo + taxonomy registry
     [✅] ENSO skill authored (SKILL.md) · Test Run 001 PASS   ◀── YOU ARE HERE
     [◑ ] find_methodology discovery tool — spec'd, not built
     [☐ ] publish step (repo → served) — design only
     [☐ ] eval harness (examples → CI) — design only  (paused on purpose: must eat PROCESS data, §7)
                       │
                       ▼  after V0 the path SPLITS:
         in-house architecture track  ·  activation / content track
```

## 5 · THE FUNDAMENTALS — the rules under everything

```text
   RULE A · every field does ONE job — label it before you cite it
     GROUNDS (evidence)        FRAMES (explanation only)     ROUTES (who cares)
     capacity·CF·PPA·node      context.description ⚠·Wiki    owner·offtaker·operator
        + EXTERNAL (NOAA causal state)   + LOGIC (crosswalks/thresholds)
     ⚠ context.description READS like fact but is LLM prose → grounding on it = BLOCKED

   RULE B · every material claim = 7 slots; a slot you can't fill = downgrade or block
     condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance

   RULE C · a resource is a CONTROL SURFACE, not an essay
     allowed_claims = the ceiling      blocked_claims = the floor  ◀── heaviest lifting
     essay → fluent (drifts)           resource → disciplined + auditable (refuses)

   RULE D · the MCP surface is a FLOOR, not a ceiling
     gap = roadmap input, logged (gap·workaround·roadmap → docs/09)   not a dead end
```

## 6 · THE FIVE DESIGN PRINCIPLES (docs/08)

```text
   P1  STABLE methodology  |  VOLATILE execution      ride LLM progress by swapping the
       claim grammar, gates |  model, orchestration,    ENGINE, not the discipline
       taxonomy, blocked    |  delivery, phrasing
   P2  CONTENT downstream of validated insight         insight → gate → render, always
   P3  PROCESS data obeys the same laws as ASSET data  raw transcript → resolve → reuse
   P4  ITERATION is expected, not a failure            the loop (and its human) is the product
   P5  FLEXIBILITY is not an excuse for non-commitment  fix the stable layer so it's measurable
```

## 7 · THE TWO FEEDBACK LOOPS — how the platform grows

```text
   Both loops are the same move: raw → RESOLVE → a reusable asset that grows the platform.

   METHODOLOGY loop                          TOOL-SURFACE loop
   ────────────────                          ─────────────────
   full chat transcript (raw)                "this call/field would help" (raw notice)
        │ extract                                 │ log (gap·workaround·roadmap)
        ▼                                         ▼
   test_runs/test_run_NNN.md                 docs/09_mcp_roadmap.md  (the ledger)
   + prompting moves · fail→fix pairs              + R1 iso filter · R2 fleet-CF · R4 NOAA tool …
        │ sharpens                                │ feeds
        ▼                                         ▼
   prompt_projection + eval suite            the expandable MCP surface (12 → 13 tools)

   (model-agnostic by design — survives the next model release; 08 P1+P3)
```

## 8 · THE REFERENCE CORPUS — form, not facts

```text
   resources/_reference/   competitor insights · analyst briefings · industry LinkedIn posts
        ├─► RENDERING layer: how a blog/email/card/post should READ
        ├─► EVAL: a "what good looks like" yardstick
        └─► ✗ NOT grounding — never the source behind a claim   (extract the FORM, discard the claims)
```

## 9 · WHERE TO GO NEXT (the doc map)

```text
   THIS FILE (visual)
      ├─ why + what ........ docs/00_project_brief.md · docs/01_scope_v0.md
      ├─ the families ...... docs/02_analysis_catalog.md   (v0 = Exposure)
      ├─ the contract ...... docs/03_methodology_resource_standard.md
      ├─ the inputs ........ docs/04_context_and_data_map.md
      ├─ how to test ....... docs/05_mcp_test_protocol.md   (+ session capture / extraction)
      ├─ the 4 layers ...... docs/06_architecture.md
      ├─ discovery ......... docs/07_discovery_spec.md
      ├─ the principles .... docs/08_design_principles.md
      ├─ the tool ledger ... docs/09_mcp_roadmap.md
      ├─ fundamentals ...... learning/01 → 02 → 03 → 04
      └─ the first skill ... resources/weather_and_climate/el_nino_enso/
```

---

**See also**: `README.md` (read order + working rules), `docs/06_architecture.md` (the layers in prose), `docs/08_design_principles.md` (the principles in full), `docs/09_mcp_roadmap.md` (the live ledger). Then run the first test: `resources/weather_and_climate/el_nino_enso/test_runs/test_run_001.md`.
