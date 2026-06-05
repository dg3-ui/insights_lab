# Task Context - InfraSure Insights Repo Readiness

## Objective

Convert the current `.lab/insights_lab` ideation workspace into a clean, team-ready staging repo for InfraSure Insights.

The target was an execution-first structure where seniors can review the vision quickly and juniors can see exactly what to produce for v0.

## Background

The Insights Lab started as an exploratory folder with research synthesis, methodology-shape thinking, an initial methodology registry, and an El Nino scaffold. The thinking was useful, but the active folder shape was not ready to hand to a team.

The desired v0 deliverable was:

```text
El Nino / ENSO exposure methodology resource
  + prompt projection
  + data requirements map
  + one manual MCP/Claude test run
  + applied-insight draft
  + learning/logged gaps
```

The important boundary was that v0 should be **MCP-ready**, not MCP-integrated. No production agent, code, database schema, or outreach automation should be built until a manual MCP/Claude test proves the resource shape.

## Problems Encountered

1. The original folder mixed ideation, scope, research, and resource scaffold files at the same level.
2. `initial_scope.md` carried valuable vision and deliverable thinking, but also folder-architecture details that made it less usable as a team scope.
3. The analysis-family content was important but needed a clear canonical home.
4. Learning/onboarding needed to be visible without becoming a top-level folder that would crowd future `code/`, `scripts/`, or `data/` folders.
5. Neighboring lab/platform docs still pointed to the old `methodology_registry/` path after the refactor.

## What We Fixed

1. Replaced the Insights Lab README with an execution-facing entry point.
2. Created a minimal scalable live tree:

   ```text
   insights_lab/
   ├── README.md
   ├── docs/
   ├── resources/
   ├── templates/
   └── archive/
   ```

3. Promoted the old methodology-registry scope into `docs/01_scope_v0.md`.
4. Added execution docs:
   - `docs/00_project_brief.md`
   - `docs/01_scope_v0.md`
   - `docs/02_analysis_catalog.md`
   - `docs/03_methodology_resource_standard.md`
   - `docs/04_context_and_data_map.md`
   - `docs/05_mcp_test_protocol.md`
5. Added onboarding under `docs/learning/`.
6. Added the first ENSO resource package under `resources/el_nino_enso/`.
7. Added reusable templates under `templates/`.
8. Archived old exploratory files under `archive/`.
9. Updated live cross-links in:
   - `.lab/README.md`
   - `.lab/contacts/planning/README.md`
   - `.lab/contacts/planning/companies_dimension/README.md`
   - `riorg/dimensions/context/README.md`

## Files Touched

### Created

- `.lab/insights_lab/docs/00_project_brief.md`
- `.lab/insights_lab/docs/01_scope_v0.md`
- `.lab/insights_lab/docs/02_analysis_catalog.md`
- `.lab/insights_lab/docs/03_methodology_resource_standard.md`
- `.lab/insights_lab/docs/04_context_and_data_map.md`
- `.lab/insights_lab/docs/05_mcp_test_protocol.md`
- `.lab/insights_lab/docs/learning/README.md`
- `.lab/insights_lab/docs/learning/01_mcp_basics.md`
- `.lab/insights_lab/docs/learning/02_infrasure_data_substrate.md`
- `.lab/insights_lab/docs/learning/03_methodology_resources.md`
- `.lab/insights_lab/docs/learning/04_prompt_projection.md`
- `.lab/insights_lab/docs/learning/logs/README.md`
- `.lab/insights_lab/docs/learning/logs/2026-06-05_repo_readiness.md`
- `.lab/insights_lab/resources/el_nino_enso/README.md`
- `.lab/insights_lab/resources/el_nino_enso/resource.md`
- `.lab/insights_lab/resources/el_nino_enso/resource.yml`
- `.lab/insights_lab/resources/el_nino_enso/data_requirements.md`
- `.lab/insights_lab/resources/el_nino_enso/prompt_projection.md`
- `.lab/insights_lab/resources/el_nino_enso/examples/applied_insight_001.md`
- `.lab/insights_lab/resources/el_nino_enso/test_runs/test_run_001.md`
- `.lab/insights_lab/templates/methodology_resource.template.md`
- `.lab/insights_lab/templates/methodology_resource.template.yml`
- `.lab/insights_lab/templates/applied_insight.template.md`
- `.lab/insights_lab/templates/mcp_test_run.template.md`
- `.lab/insights_lab/templates/learning_log.template.md`

### Modified

- `.lab/insights_lab/README.md`
- `.lab/README.md`
- `.lab/contacts/planning/README.md`
- `.lab/contacts/planning/companies_dimension/README.md`
- `riorg/dimensions/context/README.md`

### Archived / Moved

Old exploratory files were moved under:

- `.lab/insights_lab/archive/exploratory/`
- `.lab/insights_lab/archive/original_methodology_registry/`
- `.lab/insights_lab/archive/original_first_methodology_brief/`
- `.lab/insights_lab/archive/research/`

## Current Status

- [x] Live Insights Lab tree is repo-ready.
- [x] Scope clearly says v0 is resource + manual MCP/Claude test, not direct integration.
- [x] Learning track lives under `docs/learning/`.
- [x] ENSO resource package is seeded.
- [x] Templates are available for future resources and test runs.
- [x] Old exploratory files are preserved in `archive/`.
- [x] Live stale links to `methodology_registry/` were updated.
- [ ] First actual manual Claude/MCP test still needs to run.

## Next Steps

1. Read `README.md` and `docs/01_scope_v0.md` as the new contributor entry point.
2. Run the planned test in `resources/el_nino_enso/test_runs/test_run_001.md`.
3. Replace placeholder rows in `examples/applied_insight_001.md` with source-backed output from the test.
4. Add a real learning log under `docs/learning/logs/`.
5. Use test failures to improve `resource.md`, `resource.yml`, `data_requirements.md`, and `prompt_projection.md`.

