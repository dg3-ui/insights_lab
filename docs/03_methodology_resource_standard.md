# 03 - Methodology Resource Standard

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
data_requirements.md input map (see docs/04)
prompt_projection.md pasteable session surface (see docs/learning/04)
examples/            target + validated applied-insight shapes
test_runs/           manual validation records
```

The Markdown file is for humans. The YAML file is for structured operation. The prompt projection is the minimal instruction surface for Claude/MCP testing.

## Resource Contract

Every resource must define:

```text
methodology_resource
├── identity
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
| `staleness_signals` | Data or external events that force review |

`blocked_claims` carries the most weight: a resource with sharp "blocked" rules produces safe output even when the "allowed" language is loose. The reverse is not true.

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

Each material claim should carry at least one `source_ref` (taxonomy in `docs/04`). Filled example:

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

Use conservative confidence. Do not upgrade confidence beyond what the weakest required input supports.

| Confidence | Use When |
|---|---|
| High | Mechanism is strong, scope is resolved, source refs are current, and the claim is narrow |
| Medium | Mechanism is credible but one input, crosswalk, or comparison is imperfect |
| Low | Claim is directional, scenario-based, or depends on external forecasts / incomplete context |
| Blocked | Required input is missing, source is stale, entity scope is unresolved, or claim exceeds allowed logic |

The ENSO claim above is `low` because its weakest input — an external seasonal forecast plus a noisy regional teleconnection — caps it there, regardless of how clean the asset scope is.

## Blocked Claim Examples

Do not allow:

- exact LMP forecasts from ENSO alone
- plant-level production forecasts without plant-level weather/resource data
- account/outreach claims before the insight claim is valid
- claims grounded only in descriptive context (e.g. the Gemini-generated plant description — see `docs/04`)
- broad national conclusions from one regional test
- causal language where the resource only supports correlation or directional exposure

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
