# InfraSure Insights

> **Status**: v0 staging workspace, 2026-06-08.
>
> **Purpose**: create methodology-backed insight resources that let an MCP-enabled LLM use InfraSure data tools like a focused analyst.
>
> **V0 outcome**: one El Nino / ENSO exposure methodology package, one prompt projection, one data-requirements map, one manual MCP/Claude test run (001 PASS), one applied-insight draft, and one learning/gap log.
>
> **Since 001 PASS** the methodology layer was hardened (not extended into code): governing principles (`docs/principles.md`), a living MCP feedback ledger (`docs/status/mcp_gaps.md`), agent instructions (`CLAUDE.md` / `AGENTS.md`), and a quarantined exemplar corpus (`resources/_reference/`); the project brief (`docs/architecture.md`) was made the single visual overview of the whole project. The publish step, discovery tool, and eval harness remain deliberately paused.

InfraSure Insights is not a news pipeline and not a generic content project. It is an applied intelligence layer:

```text
MCP data tools
  +
methodology-backed analyst
  =
grounded InfraSure insight

grounded insight
  +
contacts / account context
  =
standardized activation and outreach
```

V0 does not build the production insight agent. V0 proves that a structured methodology resource can guide Claude plus existing InfraSure MCP/data tools toward a useful, caveated, source-grounded applied insight.

---

## Repository Map

```text
insights_lab/
├── README.md
├── CLAUDE.md                   # agent instructions (full) — how to work here, conventions, don'ts
├── AGENTS.md                   # agent instructions (lean, vendor-neutral cut of CLAUDE.md)
├── .claude/commands/           # slash commands: /new-resource · /test-resource · /extract · /render  (TRACKED — travels on clone)
├── .cursor/commands/           # the same commands for Cursor (tracked copies — keep in sync with .claude/commands/)
├── docs/                       # grouped by job; folder = job, canon vs volatile = folder boundary (P1)
│   ├── README.md               # the docs index + per-audience read order
│   ├── architecture.md         # THE front door — flow (Mermaid+ASCII), 4 layers, terminology, the gate
│   ├── principles.md           # the discipline (P1–P7): stable/volatile · content downstream · no-mush · references-inform-not-bind (P6) · posture (P7)
│   ├── use_cases.md            # the 2 buckets × audience (Pillar 3) + the V0 scope contract + validation
│   ├── method/                 # the contract: analysis_families · resource_standard · confidence_model (3-axis) · data_map · discovery_spec
│   ├── process/                # the loop: test_protocol · commands (toolchain design)
│   ├── status/                 # VOLATILE hub: capabilities · mcp_gaps (ledger) · commands (registry)
│   ├── plans/                  # the active working plans
│   └── learning/               # onboarding fundamentals (01–04) + session logs
├── resources/
│   ├── README.md               # methodology registry (domain · family · actor)
│   ├── _principles · _style · _craft · _reference · _method   # shared layers (composed at session time)
│   └── weather_and_climate · hazard · commercial             # domain folders; e.g. el_nino_enso · hail_solar · offtaker_concentration
├── studio/                     # LAYER 3 output layer: <subject>/<phenomenon>.md briefs · _triage board · subject guides (post-gate · /render)
├── templates/
└── archive/
```

This is a minimal scalable structure. Do not add `code/`, `scripts/`, or `data/` until there is real implementation work that belongs in those folders.

**Running the commands after a clone.** The slash commands are **tracked** (`.claude/commands/` for Claude Code · `.cursor/commands/` for Cursor) — a clone includes them. Open the repo in **Claude Code or Cursor** and invoke them (`/render`, `/new-resource`, `/test-resource`, `/extract`). What each does + how to invoke (args, sequences) is **`docs/process/commands.md`** (the operator's quick-reference); each command file is its own full guide. They're **thin conductors over the canon**, so even without the tool you can follow a command file's steps by hand. `.claude/commands/` is the source of truth; `.cursor/commands/` mirrors it (keep the two in sync when editing).

## Read Order

(The canonical per-audience read order lives in `docs/README.md`; the short version:)

```text
senior reviewer:   docs/architecture.md -> docs/principles.md -> docs/use_cases.md -> docs/method/ -> docs/status/
junior contributor: docs/architecture.md -> docs/method/resource_standard.md -> docs/method/data_map.md
                    -> docs/process/test_protocol.md -> resources/weather_and_climate/el_nino_enso/ -> templates/
onboarding:        docs/architecture.md (start here) -> docs/learning/ (README -> 01 -> 02 -> 03 -> 04)
```

## V0 Deliverable

The first resource is:

```text
El Nino / ENSO exposure
  -> renewable assets
  -> one region or market
  -> actor relevance
```

The required output package is:

```text
resources/weather_and_climate/el_nino_enso/
├── README.md
├── resource.md
├── resource.yml
├── data_requirements.md
├── prompt_projection.md
├── examples/
│   └── applied_insight_001.md
└── test_runs/
    └── test_run_001.md
```

Success means the resource can be pasted or loaded into a Claude/MCP session and produce one structured applied-insight draft with source references, confidence, caveats, and actor relevance.

## Working Rules

- Start from methodology, not topic enthusiasm.
- Treat data access as grounding, not decoration.
- Keep the method analytical; **content/outreach is a rendering of a validated insight, never the source of truth** (`docs/principles.md` P2).
- Use manual MCP/Claude testing before building code — and treat it as a **loop**: a one-shot draft is a draft, iteration is expected (`docs/principles.md` P4).
- **Save the full transcript** of each test (raw source), then resolve it into a `test_run` (`docs/process/test_protocol.md`).
- Log failures as method gaps, tool/data gaps, external-source gaps, or orchestration gaps; **log every MCP tool gap/idea in `docs/status/mcp_gaps.md`** (the surface is a floor, not a ceiling).
- Keep the **methodology layer stable** and the **execution layer swappable** — absorb LLM advances by swapping the engine, not the discipline (`docs/principles.md` P1).
- Keep learning material under `docs/learning/`; keep outside exemplars in `resources/_reference/` (form, not facts).
- Move old exploratory material to `archive/` instead of mixing it with execution docs.

## Current Task

V0 is validated (Test Run 001 PASS); the methodology layer is hardened (principles in `docs/principles.md`, the MCP ledger in `docs/status/mcp_gaps.md`, the command toolchain in `docs/process/commands.md`), and the shared resource layers (`_principles` · `_style` · `_craft` · `_reference`) are built.

The latest work is the **outlier / reverse-engineering lane** (`docs/plans/2026-06-14_outlier_showcase_red_dog.md`, **complete**) — a research-grounded bottom-up **Red Dog Mine** report (`docs/extra/reddog_bottom_up_report_2026-06.md`, pending owner review) + the reusable **outlier playbook** (`docs/method/outlier_playbook.md`) for off-substrate ad-hoc requests. Before it, the **knowledge-base expansion** completed (`docs/plans/2026-06-13_knowledge_base_expansion_v1.md`, Phases 0–4 ✅: the authored-intelligence scaffold + 5 validated resources across hazard/weather/commercial + one proven recipe). Likely next: **Wave-2** (wire model-gpr for the $/EAL layer) · the **near-queue** resources (wildfire×transmission · drought · flood) · or a 2nd outlier. Done: the **docs reorganization** (`docs/plans/done/2026-06-13_docs_reorg.md`). Paused: the **layered-reference restructure** at Phase 5 (`docs/plans/2026-06-11_layered_reference_v1.md` — crack bottom-up). The publish step, discovery tool, and eval harness stay paused. The current build status lives in `docs/status/capabilities.md`.
