# resources/templates — Package Skeleton (copied by `/new-resource`)

> **Status**: v0, 2026-06-14 (`../../docs/plans/2026-06-13_knowledge_base_expansion_v1.md` Phase 1). The clean placeholder set `/new-resource` Phase 1 copies into a new package. **Not a package itself** (no slug, not indexed). The filled, worked reference is [`../weather_and_climate/el_nino_enso/`](../weather_and_climate/el_nino_enso/).

## Files (template → package)

| Template | Copied to | Job |
|---|---|---|
| `methodology_resource.template.yml` | `resource.yml` | the structured seam (taxonomy→discovery · confidence_rules+blocked_claims→gates · maturity · prompt sections) |
| `methodology_resource.template.md` | `resource.md` | the human-readable method |
| `knowledge.template.md` | `knowledge.md` | the cited mechanism library (the stable "why") |
| `historical_context.template.md` | `historical_context.md` | deeply researched event ledger (frames/external; informs method, never grounds scoped assets) |
| `prompt_projection.template.md` | `prompt_projection.md` | the pasteable session surface |
| `data_requirements.template.md` | `data_requirements.md` | the retrieval plan + known gaps + missing-data handling |
| `skill.template.md` | `SKILL.md` | the published, loadable skill (frontmatter `name`+`description` + body) |
| `applied_insight.template.md` | `examples/applied_insight_001.md` | the target output shape |
| `mcp_test_run.template.md` | `test_runs/test_run_001.md` | the manual test record |

## How to use

```text
1. /new-resource <topic>  copies + renames these into resources/<domain>/<slug>/
2. Fill every <placeholder>; meet the contract in ../../docs/method/resource_standard.md
3. When a section is unclear, diff against the worked el_nino_enso package
```

Templates carry `<placeholder>` guidance, not facts — every fact a resource emits is grounded live (substrate + named external source), never copied from a template.

---

**See also**: `../../docs/method/resource_standard.md` (the contract these meet) · `../../.claude/commands/new-resource.md` (the engine that copies them) · `../weather_and_climate/el_nino_enso/` (the worked reference) · `../README.md` (the registry + underscore rule).
