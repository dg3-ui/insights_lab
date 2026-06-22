# MCP Test Run 001 — ENSO Exposure V0

> **Status**: COMPLETE — first manual MCP/Claude test.
>
> **Date**: 2026-06-05 · **Tester**: Claude (Opus 4.8) + Divy, live InfraSure MCP session.
>
> **Decision**: **PASS (with logged gaps)** — the resource shape guided a grounded, caveated, source-referenced applied insight without a custom in-house agent.

## Test Question

```text
Using the El Niño / ENSO exposure methodology, draft a directional exposure insight for
CAISO solar assets ≥ 50 MW. Focus on scoped assets/owners, mechanism, source refs,
confidence, caveats, and actor relevance.
```

## Loaded Files

- `prompt_projection.md` (operational cut)
- `knowledge.md` (mechanism + sources)
- `data_requirements.md` (input map)

## Tools / Data Used

| Tool / source | Call | Result |
|---|---|---|
| NOAA CPC (WebFetch) | ENSO Diagnostic Discussion | **El Niño Watch**; ENSO-neutral now; Niño-3.4 +0.4 °C; **~96% El Niño DJF 2026-27**; strength uncertain (no category > 37%) |
| `search_plants` | `fuel=solar, iso="CAISO", minMw=50` | **`[]` — EMPTY** (tool gap) |
| `search_plants` | `fuel=solar, state="CA", minMw=50` | 8 plants (Topaz 57695, Pelicans Jaw 68607, Darden I–IV 69661-4, Sanborn 69956, Rexford 64633) ✅ |
| `aggregate` | plants · group_by=state · total_capacity · `{fuel:SUN}` | CA solar **36,843 MW** |
| `get_plant` | `57993` (Desert Sunlight 300) | CF summer ~0.38 / winter ~0.13; owner Clearway → TotalEnergies; offtaker PG&E (28 contracts, PPA $160.95/MWh) |

## Output Summary

Produced `examples/applied_insight_001.md` — a **directional, LOW-confidence** exposure insight: El Niño Watch for DJF 2026-27 → wetter/cloudier CA winter tendency → downside to an already-low winter solar CF across the CA ≥50 MW fleet. All material claims carry a source ref + as-of; no quantitative production/price claims made.

## Accepted Claims

| Claim | Why accepted | Source ref |
|---|---|---|
| El Niño likely for DJF 2026-27 | grounded external forecast | NOAA CPC, 2026-06-05 |
| CA solar fleet ≥50 MW resolved | grounded substrate | `aggregate` + `search_plants`, 2026-06-05 |
| Directional winter-CF downside | mechanism cited, capped LOW | `knowledge.md` + `get_plant(57993)` CF |

## Rejected / Downgraded Claims

| Claim | Issue | Action |
|---|---|---|
| Any MWh / % generation loss | no plant-level model | **blocked** |
| Any $/MWh or LMP effect | outside allowed claims | **blocked** |
| ISO-based scoping (`iso="CAISO"`) | filter returns `[]` | **downgraded** to `state="CA"` + per-plant `regions.iso_rto` |
| "El Niño will reduce output" (causal) | evidence is directional | reworded to probabilistic/directional |

## Failures Found

| Type | Description | Next fix |
|---|---|---|
| **MCP/tool gap** | `search_plants(iso="CAISO")` → `[]` though per-plant ISO exists in `get_plant.regions` | wire ISO filter to the region join, or add `resolve_region` tool |
| **External-data limit** | ENSO strength not yet forecastable (occurrence only) | re-pull as forecasts sharpen; keep confidence LOW |
| **Method** | none — blocked claims held; confidence stayed conservative | — |
| **Prompt** | none — projection forced retrieval + the `state=` fallback + source refs | — |

## Decision

```text
PASS (with logged gaps).

The methodology resource (resource.md + knowledge.md + prompt_projection.md) successfully guided
Claude + the existing InfraSure MCP tools + a live NOAA pull to one grounded, caveated,
source-referenced directional insight — and it correctly BLOCKED the quantitative overclaims.
This validates the v0 resource SHAPE without building a custom agent.
```

## Next Fixes

- **Roadmap (MCP)**: wire the `search_plants` ISO filter / add region resolution — the one real tool gap.
- Add a **fleet-level seasonal-CF rollup** so generation evidence isn't a single drilled plant.
- Keep the ENSO state fresh (re-pull as DJF approaches and strength resolves).
- Consider a sibling **La Niña** resource (drought / wildfire / curtailment side of `weather_and_climate`).
- `knowledge.md` strength-uncertainty + 2022-23 counter-example handling proved adequate — keep.
