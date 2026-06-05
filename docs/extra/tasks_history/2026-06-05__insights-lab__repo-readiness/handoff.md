# Handoff - InfraSure Insights Repo Readiness

## 10-Bullet Summary

1. `.lab/insights_lab` was converted from ideation-heavy docs into a team-ready staging repo.
2. The live top-level structure is now `README.md`, `docs/`, `resources/`, `templates/`, and `archive/`.
3. The main entry point is `.lab/insights_lab/README.md`.
4. The v0 execution scope is `.lab/insights_lab/docs/01_scope_v0.md`.
5. The first deliverable is an El Nino / ENSO exposure methodology package plus one manual MCP/Claude test.
6. V0 is MCP-ready, not MCP-integrated: no production agent, code, database schema, or outreach automation.
7. The first resource package lives under `.lab/insights_lab/resources/el_nino_enso/`.
8. Learning/onboarding lives under `.lab/insights_lab/docs/learning/`.
9. Old exploratory docs were preserved in `.lab/insights_lab/archive/`.
10. The next session should run the first manual Claude/MCP test and replace placeholders with source-backed output.

## Files To Read First

```text
.lab/insights_lab/README.md
.lab/insights_lab/docs/00_project_brief.md
.lab/insights_lab/docs/01_scope_v0.md
.lab/insights_lab/docs/03_methodology_resource_standard.md
.lab/insights_lab/docs/04_context_and_data_map.md
.lab/insights_lab/docs/05_mcp_test_protocol.md
.lab/insights_lab/resources/el_nino_enso/README.md
.lab/insights_lab/resources/el_nino_enso/prompt_projection.md
.lab/insights_lab/resources/el_nino_enso/test_runs/test_run_001.md
```

## Files Touched

Key created files:

```text
.lab/insights_lab/docs/00_project_brief.md
.lab/insights_lab/docs/01_scope_v0.md
.lab/insights_lab/docs/02_analysis_catalog.md
.lab/insights_lab/docs/03_methodology_resource_standard.md
.lab/insights_lab/docs/04_context_and_data_map.md
.lab/insights_lab/docs/05_mcp_test_protocol.md
.lab/insights_lab/resources/el_nino_enso/resource.md
.lab/insights_lab/resources/el_nino_enso/resource.yml
.lab/insights_lab/resources/el_nino_enso/data_requirements.md
.lab/insights_lab/resources/el_nino_enso/prompt_projection.md
.lab/insights_lab/resources/el_nino_enso/examples/applied_insight_001.md
.lab/insights_lab/resources/el_nino_enso/test_runs/test_run_001.md
```

Cross-link updates:

```text
.lab/README.md
.lab/contacts/planning/README.md
.lab/contacts/planning/companies_dimension/README.md
riorg/dimensions/context/README.md
```

## Repro / Verification Commands

Show live tree excluding archive:

```bash
find .lab/insights_lab -path '.lab/insights_lab/archive' -prune -o -type f -print | sort
```

Check stale live references:

```bash
rg -n "methodology_registry|05_first_methodology_brief|00_research_synthesis|02_methodology_brief_shape" \
  .lab/README.md .lab/contacts riorg/dimensions/context/README.md \
  .lab/insights_lab/README.md .lab/insights_lab/docs .lab/insights_lab/resources .lab/insights_lab/templates
```

Check lab repo status:

```bash
git -C /Users/divy/code/personal/renewablesinfo status --short insights_lab contacts/planning/README.md contacts/planning/companies_dimension/README.md README.md
```

## Next Action Roadmap

### Phase A - Run First Manual MCP/Claude Test

1. Open Claude with InfraSure MCP/data tools available.
2. Load or paste `.lab/insights_lab/resources/el_nino_enso/prompt_projection.md`.
3. Use the test question from `.lab/insights_lab/resources/el_nino_enso/test_runs/test_run_001.md`.
4. Ask Claude to identify required data/tools before drafting.
5. Record tools and source results in `test_run_001.md`.

### Phase B - Replace Placeholder Output

1. Use the actual test output to update `resources/el_nino_enso/examples/applied_insight_001.md`.
2. Ensure the applied insight has claim, scope, source refs, confidence, caveats, actor relevance, and review trace.
3. Downgrade or block unsupported claims.

### Phase C - Improve The Resource

1. Update `resource.md` where Claude overclaimed or got confused.
2. Update `resource.yml` if structured fields were missing.
3. Update `data_requirements.md` if tool/source gaps were discovered.
4. Update `prompt_projection.md` if the prompt was too broad or too verbose.

### Phase D - Log Learning

1. Create a new log under `.lab/insights_lab/docs/learning/logs/`.
2. Use `.lab/insights_lab/templates/learning_log.template.md`.
3. Capture what was confusing, what tool gaps appeared, and what needs to change before the next test.

## Gotchas

- `.lab` points into `/Users/divy/code/personal/renewablesinfo`, so platform repo status does not show all lab changes.
- The generated platform substrate catalog is context only; do not hand-edit it for this task.
- Do not build MCP integration yet. The next step is a manual test.
- Do not write outreach copy before the applied insight is validated.

