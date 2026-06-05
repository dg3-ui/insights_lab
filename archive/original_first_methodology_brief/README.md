# 05 — First methodology brief: El Niño & US energy infrastructure

> **Status**: scaffold only, 2026-05-31. The crucible — chosen specifically because it stress-tests the framework along multiple axes simultaneously.
>
> **Why this topic was picked first** (user's stated reasoning + analyst expansion):
> 1. **Region as a type choice** — ENSO state interacts differently with CAISO / ERCOT / SPP / MISO / Southeast.
> 2. **Multi-output, multi-dimension methodology** — outputs a causal chain (climate → solar irradiance → solar generation → demand → LMP), not a scalar. Forces the schema to handle vector outputs.
> 3. **External data with its own vintage clock** — NOAA CPC indices, monthly outlooks, seasonal forecasts. Forces "external grounding" as a first-class concept.
> 4. **Climate region as a substrate dimension we don't yet carry** — forces either a new dimension OR a generalizable "non-substrate region grounding" pattern.
> 5. **Multi-year temporal periodicity vs. our quarterly snapshot cadence** — forces a real reconciliation between methodology validity and applied-insight refresh.
> 6. **Mechanism + correlation declared honestly** — solar irradiance effects are mechanistic; LMP effects are mixed (mechanistic via cooling load, correlational via market structure). Forces a `claim_type` taxonomy.
> 7. **The fan-out problem in concrete form** — methodology applies to thousands of plants. Forces the parameterized-insight-vs-stored-insight call.

## Files

- `brief.md` — the methodology brief itself, structured per `02_methodology_brief_shape.md`. **Empty stub** at the moment; user supplies domain knowledge, agent structures it.
- `data_inputs.md` — concrete substrate joins required, gaps in current substrate, external sources needed. **To be added if the resource needs a separate input inventory.**
- `what_we_learned.md` — running log of what writing this brief revealed about the framework. Populated during iteration; folds back into `02_methodology_brief_shape.md` revisions.

## How this brief gets written

This brief now feeds the [`../methodology_registry/`](../methodology_registry/) work. The immediate goal is not a polished publication; it is the first methodology resource that can be tested with MCP + Claude.

1. User dumps domain knowledge into `brief.md` in any shape (prose, bullets, equations, references).
2. We structure it against the methodology-brief schema and the methodology-registry resource contract.
3. We produce a prompt projection that Claude can use alongside MCP data tools.
4. We run one applied-insight test scoped to one asset, region, company, or offtaker.
5. Whenever the schema doesn't fit, we either flex the schema or adjust the brief's framing. Each flex gets logged in `what_we_learned.md`.
6. When the brief/resource/test loop is coherent, we decide whether the registry is ready for a second methodology or a small in-house architecture prototype.

This is **not** a finished publication. It's an architectural test. The brief might never ship in this form — that's fine.

## What we expect to discover (predictions to test)

- The `output_metric` field probably needs to become `outputs[]` — a vector of derived quantities, each typed.
- The `scope` block probably needs a `regions[]` field that accepts both substrate region types (BA, ISO, NERC, RC) and external region types (ENSO climate region, NOAA CPC region, drought monitor region) with explicit type discrimination.
- The `substrate_inputs` field probably needs an `external_inputs[]` sibling for non-substrate data sources, with their own vintage / refresh / fallback policy.
- `procedure.reference` probably needs a `claim_types` field declaring per-output-quantity which kind of inference it is (mechanistic / statistical / scenario-based).
- `validity` probably needs a `temporal_scale` field — quarterly snapshot doesn't capture "this methodology spans multi-year climate cycles."
- The applied-insight `kind` may need to support parameterized templates that render per-entity on demand, in addition to fully-materialized per-entity insights.

If even half of these surface, this brief did its job.
