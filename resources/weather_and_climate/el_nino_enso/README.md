# El Nino / ENSO Exposure Resource

> **Status**: v0 resource package scaffold, 2026-06-05.
>
> **Purpose**: create the first InfraSure Insights methodology resource and validate it manually with Claude + existing MCP/data tools.
>
> **Domain**: `weather_and_climate` (driver-grouped). Family: Exposure (`docs/02`). Registry: `resources/README.md`.

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
| `resource.md` | Human-readable methodology |
| `resource.yml` | Structured operational fields |
| `data_requirements.md` | Data/tool/source inventory |
| `prompt_projection.md` | Pasteable Claude/MCP instruction surface |
| `examples/applied_insight_001.md` | Target applied-insight shape |
| `test_runs/test_run_001.md` | Manual test record |

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

