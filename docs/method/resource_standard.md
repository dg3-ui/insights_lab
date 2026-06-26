# Methodology Resource Standard

> **Status**: v0 standard, deepened 2026-06-05.
>
> **Purpose**: define what every methodology resource must contain so it can guide a model, support review, and later scale into production architecture.
>
> **Companion**: `docs/learning/03_methodology_resources.md` *teaches* this contract; this file *is* the contract.

## Resource Package

Each methodology resource package should contain:

```text
resource.md          human-readable method
resource.yml         structured operational fields
data_requirements.md input map (see data_map.md)
prompt_projection.md pasteable session surface (see docs/learning/04)
historical_context.md cited event ledger (frames/external; informs method, never grounds scoped assets)
examples/            target + validated applied-insight shapes
test_runs/           manual validation records
```

The Markdown file is for humans. The YAML file is for structured operation. The prompt projection is the minimal instruction surface for Claude/MCP testing. `historical_context.md` is the deep event-history layer: it sharpens the mechanism, materiality band, confidence cap, and blocked-claim discipline, but it is **never** a substitute for live substrate grounding in an applied insight.

## Resource Contract

Every resource must define:

```text
methodology_resource
├── identity
├── maturity            (grounding_maturity · data_maturity)
├── question_grammar
├── scope
├── inputs            (substrate_inputs · external_inputs · descriptive_context · actor_context)
├── region_resolution
├── procedure
├── allowed_claims
├── blocked_claims
├── confidence_rules
├── caveats
├── actor_relevance
├── staleness_signals
└── prompt_projection
```

## Required Fields

| Field | What It Means |
|---|---|
| `identity` | Slug, title, version, status, owner, and review date |
| `maturity` | `grounding_maturity` + `data_maturity` — set the confidence ceiling + the build order (defined in *Maturity, Peril & Stationarity* below) |
| `question_grammar` | The exact questions this resource is allowed to answer |
| `scope` | Entity types, fuels, regions, lifecycle phases, and actors |
| `substrate_inputs` | InfraSure data/tool inputs needed for grounding |
| `external_inputs` | Non-platform sources needed for causal or scenario state |
| `descriptive_context` | Background context useful for explanation but not claim grounding |
| `actor_context` | Owner, developer, offtaker, company, or account context for relevance |
| `procedure` | Ordered reasoning steps and expected intermediate outputs |
| `allowed_claims` | Claim types the resource may produce |
| `blocked_claims` | Claims the resource must not make |
| `confidence_rules` | When to keep, downgrade, or block a claim |
| `caveats` | Required caveats by claim type |
| `actor_relevance` | Who cares, why, and which rendering uses it |
| `staleness_signals` | Data or external events that force review — including a version change in a shared `resources/_*` layer the resource was validated against (`resources/README.md`, Shared Layers) |

`blocked_claims` carries the most weight: a resource with sharp "blocked" rules produces safe output even when the "allowed" language is loose. The reverse is not true.

## Maturity, Peril & Stationarity Fields

> Added 2026-06-14 (`../plans/2026-06-13_knowledge_base_expansion_v1.md` Phase 1) — three additions that keep expansion grounding-led and make peril authoring repeatable.

### Maturity (every resource)

Two facets in `resource.yml.maturity`. They **do not categorize** (not discovery tags); they set the **confidence ceiling** and the **build order**:

| Field | Values | Meaning |
|---|---|---|
| `grounding_maturity` | `substrate-only` \| `model-not-wired` \| `needs-data` | Can the public MCP + one named feed ground a defensible claim **today**? `substrate-only` → ship now (directional). `model-not-wired` → the quantified claim lives in `model-gpr`; ship the **directional** claim now + **log the gap** (`../status/mcp_gaps.md`). `needs-data` → defer. |
| `data_maturity` | `H` \| `M` \| `L` | Substrate coverage for this resource's scope; sparse coverage caps confidence and forces *omit-don't-infer*. |

**Rule**: a resource's confidence ceiling never exceeds what `grounding_maturity` supports — a `model-not-wired` resource must **not** emit the quantified claim its model would (EAL, forward LMP, DSCR); it ships the directional claim and logs the gap.

### Peril-field standard (hazard / peril resources)

A peril resource's `resource.yml` adopts the vault's hazard-CSV columns, so peril authoring is a CSV-row → package transform:

| Field | Meaning |
|---|---|
| `predictability` | Lead-time skill of the hazard (forecastable vs sudden-onset). |
| `key_datasets` | The named external footprint/event feed(s) — e.g. NOAA-SPC hail, NHC track, NIFC fire perimeter. |
| `climate_attribution_confidence` | Strength of the climate-change trend signal (caps trend claims). |
| `financial_materiality` | Typical $ severity to the asset class — a **tie-breaker, never the grounding**. |
| `insurance_treatment` | How the peril is carried/excluded in cover — the bridge to the commercial $ layer. |

The hazard **EXPOSURE + EVENT-TRANSLATION** claim is groundable today (substrate + the `hazards` news category + one feed → **directional**); the hazard **LOSS / $** (EAL, PML, insurance pricing) is `model-gpr` → set `grounding_maturity: model-not-wired`, log the gap. Hazard news carries **classifier noise** (false positives) — a peril resource's `procedure` **must include a VERIFY step** (`CLAUDE.md` "don't trust tool labels").

### Non-stationarity (climate / weather resources)

Every weather/climate resource carries a standard `confidence_rule`: **climate non-stationarity caps trend claims.** A historical teleconnection or baseline (an ENSO composite, a hail climatology) is an odds-shift on a *shifting* baseline, not a stationary law — never assert a stationary return-period from a historical record alone.

## Historical Context Layer

> Added 2026-06-25 — the event-history layer for resources where past events materially teach the method.

`historical_context.md` is recommended for any package whose mechanism is clarified by real events (hazards, weather/climate drivers, commercial failures, market disruptions). It is **in-package methodology**, not a shared reference layer: the file belongs with the resource because it explains that resource's event grammar, mechanism traps, and claim boundaries.

Role discipline:

```text
historical_context.md = frames + external evidence
  -> informs mechanism, materiality, confidence caps, caveats, blocked claims
  -> supplies cited historical analogs and recurrence patterns
  -> NEVER grounds scoped assets in a new applied insight
  -> every number must be named-source + dated, and re-grounded before use
```

Each event entry should state:

```text
name + dates + geography / market / ISO
what happened (cited)
mechanism illustrated (links back to knowledge.md)
magnitude / impact (energy, reliability, $ only where authoritatively reported)
asset / actor relevance
what this event DOES and DOES NOT license as a claim
```

If a historical-context event lacks a source for a number, omit the number. If an event only loosely resembles the scoped asset class, label it as analogy, not grounding.

## Applied-Insight Thin Contract

An applied insight produced from a resource must contain:

```text
applied_insight
├── claim
├── scope
├── methodology_reference
├── source_refs
├── confidence
├── caveats
├── actor_relevance
└── review_trace
```

It does not need to be a production database object in v0. It does need to be structured enough for review and two renderings:

```text
resource.yml (the method)
      |
      v
applied_insight (the thin object above)
      ├──> platform card / Ask answer
      └──> account note / informative email   (only after review_trace passes)
```

## Claim Grammar

Use this grammar for material claims:

```text
condition
  + scoped entity set
  + mechanism
  + evidence
  + confidence
  + caveat
  + actor relevance
  =
applied insight claim
```

Worked example, grounded in real entities (`get_plant`/`aggregate`, 2026-06-05):

```yaml
condition: "Forecast El Niño conditions for the winter the test is run in (per NOAA CPC)"
scope: "CAISO solar plants >= 50 MW — e.g. Topaz Solar Farm (57695, 585.9 MW),
        Desert Sunlight 300 (57993, 313.7 MW); resolved via state=CA (iso filter is unwired)"
mechanism: "ENSO-associated winter cloud/precipitation tendency may shift seasonal irradiance"
evidence:
  external: "NOAA CPC ENSO status / seasonal outlook (name + date)"
  substrate: "get_plant.generation monthly CF (summer ≈0.38 / winter ≈0.13); capacity; regions.iso_rto=CAISO"
confidence: low
caveat: "Directional exposure; not a plant-level production forecast; SW teleconnection is noisy"
actor_relevance: "Owner (Clearway/BHE) and offtaker (PG&E) should monitor seasonal generation variance"
```

Each material claim should carry at least one `source_ref` (taxonomy in `data_map.md`). Filled example:

```yaml
source_ref:
  source_type: substrate
  source_name: "InfraSure get_plant"
  entity_scope: "plant 57993 (Desert Sunlight 300)"
  field_or_fact: "generation.monthly capacity_factor"
  vintage_or_accessed_at: "2026-06-05"   # the _meta.as_of envelope
  role: primary
```

## Confidence Rules

> **Confidence is three axes, not one** (`confidence_model.md`). The ladder below is the **CALIBRATION CAP** — the only *graded* axis, and the firewall `blocked_claims` enforces. The other two axes — **event likelihood** (the world's sourced probability) and **materiality** (the stake) — are *not* graded here and *never raise the cap*. This section owns the cap; the model owns how all three render.

Use conservative confidence. **The cap is set by the weakest required input, and nothing raises it** — not a high event-likelihood, not a severe stake.

| Calibration cap | Use When |
|---|---|
| High | Mechanism is strong, scope is resolved, source refs are current, and the claim is narrow |
| Medium | Mechanism is credible but one input, crosswalk, or comparison is imperfect |
| Low | Claim is directional, scenario-based, or depends on external forecasts / incomplete context |
| Blocked | Required input is missing, source is stale, entity scope is unresolved, or claim exceeds allowed logic |

The ENSO claim above is `low` because its weakest input — an external seasonal forecast plus a noisy regional teleconnection — caps it there, regardless of how clean the asset scope is, **how likely the El Niño (63%), or how large the exposed book**.

**Materiality basis (the second internal axis).** When a resource ranks *how big the stake is*, ground it as **exposed-share × class-severity band** — the exposed-share is a substrate count (the % of the subject's MW/plants in the exposed bucket); the class-severity band is read from the resource's own canon, **never a $** (a $ is a `model-gpr` output, blocked here): for a **hazard/peril** resource it is the `financial_materiality` field above; for a **weather/climate** resource it is the documented (driver × asset-class) sensitivity in `knowledge.md` (e.g. the ENSO CA/SW DJF teleconnection robustness). If the cell has no documented severity band, materiality is `unknown` — a logged gap, not an asserted band. Materiality is a **tie-breaker** (it orders which low-cap reads to surface first), never an **override** (it never lifts the cap). Full model + the render/internal split: `confidence_model.md`.

## Blocked Claim Examples

Do not allow:

- exact LMP forecasts from ENSO alone
- plant-level production forecasts without plant-level weather/resource data
- account/outreach claims before the insight claim is valid
- claims grounded only in descriptive context (e.g. the Gemini-generated plant description — see `data_map.md`)
- broad national conclusions from one regional test
- causal language where the resource only supports correlation or directional exposure
- **charts of any of the above** — a plot is a set of claims; a series with no `source_ref`/`as_of`, a drawn forecast curve with no model, or a chart from exemplar data is the same blocked claim in ink (`resources/_craft/plot_generation.md`)

## Review Checklist

Before a resource passes v0 review:

- the resource can state what it answers and what it does not answer
- all inputs are named and categorized (substrate / external / descriptive / actor)
- reasoning steps are ordered
- allowed and blocked claims are explicit
- confidence and caveat rules are explicit
- actor relevance is present but does not distort the method
- the prompt projection is concise enough for a manual Claude/MCP test

If any item fails, the resource is not ready — however well it reads.
