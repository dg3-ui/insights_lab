# El Nino / ENSO Exposure Resource

> **Status**: v0 resource package scaffold, 2026-06-05.
>
> **Purpose**: create the first InfraSure Insights methodology resource and validate it manually with Claude + existing MCP/data tools.
>
> **Domain**: `weather_and_climate` (driver-grouped). Family: Exposure (`../../../docs/method/analysis_families.md`). Registry: `resources/README.md`.

## Resource Scope

```text
El Nino / ENSO exposure
  -> renewable assets
  -> one region or market
  -> actor relevance
```

This resource tests whether a climate-regime signal can be translated into a grounded InfraSure insight about assets, owners, offtakers, or portfolios.

The first test should stay narrow. Recommended first scope:

```text
CAISO solar assets >= 50 MW
```

If CAISO data/tool access is insufficient, use another region/market that the MCP tools can resolve cleanly.

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | **Published skill** — the loadable Claude Agent Skill (frontmatter `name`+`description` + method body + bundled refs) |
| `resource.md` | Human-readable methodology (the method) |
| `resource.yml` | Structured operational fields + taxonomy |
| `knowledge.md` | **Domain reference** — ENSO mechanism, measurement, teleconnections by region (cited) |
| `historical_context.md` | historical ENSO event context and teleconnection caveats; context only, never grounding |
| `data_requirements.md` | Data/tool/source inventory + known gaps |
| `prompt_projection.md` | Pasteable Claude/MCP instruction surface |
| `examples/applied_insight_001.md` | **Validated** applied insight (winter 2026-27, from test 001) |
| `test_runs/test_run_001.md` | Manual test record — **PASS** (2026-06-05) |

## V0 Rule

This resource is **MCP-ready**, not MCP-integrated.

```text
resource package
  -> prompt projection
  -> manual Claude/MCP session
  -> applied-insight draft
  -> logged gaps
```

Do not write production code or automate outreach from this package.

