# InfraSure Insights

> **Status**: v0 staging workspace, 2026-06-08.
>
> **Purpose**: create methodology-backed insight resources that let an MCP-enabled LLM use InfraSure data tools like a focused analyst.
>
> **V0 outcome**: one El Nino / ENSO exposure methodology package, one prompt projection, one data-requirements map, one manual MCP/Claude test run (001 PASS), one applied-insight draft, and one learning/gap log.
>
> **Since 001 PASS** the methodology layer was hardened (not extended into code): governing principles (`docs/08`), a living MCP feedback ledger (`docs/09`), a visual fundamentals map (`docs/learning/00`), agent instructions (`CLAUDE.md` / `AGENTS.md`), and a quarantined exemplar corpus (`resources/_reference/`). The publish step, discovery tool, and eval harness remain deliberately paused.

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
├── docs/
│   ├── 00_project_brief.md
│   ├── 01_scope_v0.md
│   ├── 02_analysis_catalog.md
│   ├── 03_methodology_resource_standard.md
│   ├── 04_context_and_data_map.md
│   ├── 05_mcp_test_protocol.md
│   ├── 06_architecture.md
│   ├── 07_discovery_spec.md
│   ├── 08_design_principles.md # what stays stable vs swappable; content downstream of insight
│   ├── 09_mcp_roadmap.md       # living ledger: log MCP tool gaps/ideas here
│   └── learning/
├── resources/
│   ├── README.md               # methodology registry (domain · family · actor)
│   ├── _reference/             # exemplar corpus (form, not facts) — quarantined from grounding
│   └── weather_and_climate/    # domain folder (driver-grouped)
│       └── el_nino_enso/
├── templates/
└── archive/
```

This is a minimal scalable structure. Do not add `code/`, `scripts/`, or `data/` until there is real implementation work that belongs in those folders.

## Read Order

For a senior reviewer:

```text
README.md
  -> docs/00_project_brief.md
  -> docs/01_scope_v0.md
  -> docs/02_analysis_catalog.md
  -> docs/06_architecture.md
  -> docs/07_discovery_spec.md
  -> docs/08_design_principles.md
```

For a junior contributor:

```text
README.md
  -> docs/01_scope_v0.md
  -> docs/03_methodology_resource_standard.md
  -> docs/04_context_and_data_map.md
  -> docs/05_mcp_test_protocol.md
  -> resources/weather_and_climate/el_nino_enso/README.md
  -> templates/
```

For onboarding:

```text
docs/learning/00_fundamentals_map.md      <- the whole project, drawn (visual on-ramp)
  -> docs/learning/README.md
  -> docs/learning/01_mcp_basics.md
  -> docs/learning/02_infrasure_data_substrate.md
  -> docs/learning/03_methodology_resources.md
  -> docs/learning/04_prompt_projection.md
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
- Keep the method analytical; **content/outreach is a rendering of a validated insight, never the source of truth** (`docs/08` P2).
- Use manual MCP/Claude testing before building code — and treat it as a **loop**: a one-shot draft is a draft, iteration is expected (`docs/08` P4).
- **Save the full transcript** of each test (raw source), then resolve it into a `test_run` (`docs/05`).
- Log failures as method gaps, tool/data gaps, external-source gaps, or orchestration gaps; **log every MCP tool gap/idea in `docs/09_mcp_roadmap.md`** (the surface is a floor, not a ceiling).
- Keep the **methodology layer stable** and the **execution layer swappable** — absorb LLM advances by swapping the engine, not the discipline (`docs/08` P1).
- Keep learning material under `docs/learning/`; keep outside exemplars in `resources/_reference/` (form, not facts).
- Move old exploratory material to `archive/` instead of mixing it with execution docs.

## Current Task

V0 is validated (Test Run 001 PASS) and the methodology layer is hardened with principles (`08`), the MCP ledger (`09`), the fundamentals map (`learning/00`), and agent files. The next concrete move is a **second ENSO test run done the new way** — save the full transcript, then resolve it into a `test_run` + extract the prompting moves / fail→fix pairs — to produce the first piece of *process data*. The publish step, discovery tool, and eval harness stay paused until that process loop has been exercised at least once.
