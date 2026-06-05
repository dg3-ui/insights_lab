# InfraSure Insights

> **Status**: v0 staging workspace, 2026-06-05.
>
> **Purpose**: create methodology-backed insight resources that let an MCP-enabled LLM use InfraSure data tools like a focused analyst.
>
> **V0 outcome**: one El Nino / ENSO exposure methodology package, one prompt projection, one data-requirements map, one manual MCP/Claude test run, one applied-insight draft, and one learning/gap log.

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
├── docs/
│   ├── 00_project_brief.md
│   ├── 01_scope_v0.md
│   ├── 02_analysis_catalog.md
│   ├── 03_methodology_resource_standard.md
│   ├── 04_context_and_data_map.md
│   ├── 05_mcp_test_protocol.md
│   ├── 06_architecture.md
│   ├── 07_discovery_spec.md
│   └── learning/
├── resources/
│   ├── README.md               # methodology registry (domain · family · actor)
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
docs/learning/README.md
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
- Keep the method analytical; outreach is a rendering after the claim is valid.
- Use manual MCP/Claude testing before building code.
- Log failures as method gaps, tool/data gaps, external-source gaps, or orchestration gaps.
- Keep learning material under `docs/learning/`.
- Move old exploratory material to `archive/` instead of mixing it with execution docs.

## Current Task

Complete the V0 El Nino / ENSO package and run the first manual MCP/Claude test. The first test should answer whether the current methodology-resource shape is strong enough to guide a grounded InfraSure Insight without a custom in-house agent.
