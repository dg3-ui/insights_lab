# What writing this brief revealed about the framework

> Running log. Each entry: what we tried, what didn't fit, what we changed in the schema.

## Predictions made in `README.md` (test these as we go)

- [ ] `output_metric` becomes `outputs[]` — vector of derived quantities, each typed
- [ ] `scope.regions[]` accepts substrate region types AND external region types with type discrimination
- [ ] `external_inputs[]` is a sibling of `substrate_inputs[]` with own vintage/refresh/fallback policy
- [ ] `procedure.reference.claim_types` declares per-output-quantity which inference kind (mechanistic / statistical / scenario-based)
- [ ] `validity.temporal_scale` field — quarterly snapshot doesn't capture multi-year climate cycles
- [ ] Applied-insight `kind` supports parameterized templates rendered per-entity on demand, alongside fully-materialized per-entity insights

## Findings log

(Empty — populated during iteration)
