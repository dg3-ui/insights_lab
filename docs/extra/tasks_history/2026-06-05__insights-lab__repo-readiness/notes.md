# Notes - InfraSure Insights Repo Readiness

## Implementation Notes

The refactor started by inspecting:

- `.lab/insights_lab/README.md`
- `.lab/insights_lab/methodology_registry/initial_scope.md`
- `.lab/insights_lab/methodology_registry/00_analysis_catalog.md`
- `.lab/insights_lab/05_first_methodology_brief/`
- `docs/reference/workspace/engineering/substrate_catalog.generated.md`

The generated platform substrate catalog was used as context only. It reinforced that the insights contributor should understand what platform data can ground, but should not regenerate platform data as part of v0.

## Commands Used

Inspect current tree:

```bash
find .lab/insights_lab -maxdepth 4 -type f | sort
ls -la .lab/insights_lab
ls -la .lab/insights_lab/methodology_registry
ls -la .lab/insights_lab/05_first_methodology_brief
```

Create new folders:

```bash
mkdir -p .lab/insights_lab/docs/learning/logs \
  .lab/insights_lab/resources/el_nino_enso/examples \
  .lab/insights_lab/resources/el_nino_enso/test_runs \
  .lab/insights_lab/templates \
  .lab/insights_lab/archive/exploratory \
  .lab/insights_lab/archive/original_methodology_registry \
  .lab/insights_lab/archive/original_first_methodology_brief \
  .lab/insights_lab/archive/research
```

Archive old files:

```bash
mv .lab/insights_lab/00_research_synthesis.md .lab/insights_lab/archive/exploratory/
mv .lab/insights_lab/01_principles.md .lab/insights_lab/archive/exploratory/
mv .lab/insights_lab/02_methodology_brief_shape.md .lab/insights_lab/archive/exploratory/
mv .lab/insights_lab/methodology_registry/* .lab/insights_lab/archive/original_methodology_registry/
rmdir .lab/insights_lab/methodology_registry
mv .lab/insights_lab/05_first_methodology_brief/* .lab/insights_lab/archive/original_first_methodology_brief/
rmdir .lab/insights_lab/05_first_methodology_brief
mv .lab/insights_lab/research/* .lab/insights_lab/archive/research/
rmdir .lab/insights_lab/research
```

Verify live tree:

```bash
find .lab/insights_lab -path '.lab/insights_lab/archive' -prune -o -type f -print | sort
```

Check stale live references:

```bash
rg -n "methodology_registry|05_first_methodology_brief|00_research_synthesis|02_methodology_brief_shape" \
  .lab/README.md .lab/contacts riorg/dimensions/context/README.md \
  .lab/insights_lab/README.md .lab/insights_lab/docs .lab/insights_lab/resources .lab/insights_lab/templates
```

## Verification

Final live tree, excluding archive:

```text
.lab/insights_lab/README.md
.lab/insights_lab/docs/00_project_brief.md
.lab/insights_lab/docs/01_scope_v0.md
.lab/insights_lab/docs/02_analysis_catalog.md
.lab/insights_lab/docs/03_methodology_resource_standard.md
.lab/insights_lab/docs/04_context_and_data_map.md
.lab/insights_lab/docs/05_mcp_test_protocol.md
.lab/insights_lab/docs/learning/...
.lab/insights_lab/resources/el_nino_enso/...
.lab/insights_lab/templates/...
```

The stale-reference grep returned no live hits. Remaining old path references are only inside archived historical files.

## Key Insights

- The scope file needed to become a true v0 execution scope, not a mixed architecture proposal.
- The analysis catalog deserved its own canonical doc because it answers Gate 1: what kind of intelligence InfraSure should produce.
- The resource standard and MCP test protocol deserved separate docs because they answer Gate 2: what evidence and logic each method needs.
- Learning should be tracked, but learning is not the deliverable. The deliverable is resource + prompt projection + manual test + applied-insight draft.

## Remaining Issues

- No manual MCP/Claude test has been run yet.
- `resources/el_nino_enso/examples/applied_insight_001.md` is a target shape, not a validated output.
- `resources/el_nino_enso/test_runs/test_run_001.md` is planned and still needs to be filled after the test.
- Exact external ENSO source/vintage is not yet selected inside a real test run.

