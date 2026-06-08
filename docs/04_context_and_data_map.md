# 04 - Context And Data Map

> **Status**: v0 map, deepened 2026-06-05.
>
> **Purpose**: distinguish the data and context layers a methodology resource can use.
>
> **Companion**: `docs/learning/02_infrasure_data_substrate.md` walks a real `get_plant` record field-by-field; this file defines the layer taxonomy.

## Core Principle

Not all context grounds claims.

```text
grounding data
  supports material claims

descriptive context
  helps explain the entity

actor context
  helps route and activate the insight
```

The methodology resource should name each input by job. If you cannot say which job a field does, you cannot yet cite it.

## Input Layers

| Layer | Examples (real fields, 2026-06-05) | Job |
|---|---|---|
| Grounding substrate | `total_capacity_mw` 313.7 · `generation.capacity_factor` 0.24 · `grid.lmp_node` · `ownership.chain` | Supports material claims |
| Descriptive context | `context.description` (Gemini-generated) · Wikipedia summary · external links | Frames the entity; does **not** validate a claim alone |
| Foundational knowledge | `.learning/` shared vault (→ `~/Desktop/Learning`): risk · weather/climate · electricity-market · project-finance notes | Backs the cited **mechanism** (`knowledge.md`) — the stable *why*; cite it, it is **not** live state |
| External methodology input | NOAA CPC ENSO status · ONI · seasonal outlooks · climate-region definitions | Supplies non-platform causal / scenario **state** (live — has a freshness clock) |
| Actor context | `ownership` (Clearway → TotalEnergies) · `offtakers` (PG&E, 28 contracts) · developer | Determines who should care + how it renders |
| Logic layer | thresholds (≥50 MW) · region crosswalk · confidence rules · caveat rules | Converts inputs into claims |

**The descriptive-context trap**: `get_plant(57993).context.description` reads like fact but carries `model: "google/gemini-2.0-flash-001"` — it is generated prose. Framing only. A claim grounded solely in it is a **blocked claim** (`docs/03`).

## InfraSure Substrate

V0 should use existing data tools and platform context where available. It should not rebuild the platform data pipeline. Substrate areas, with their MCP entry points and rough scale:

| Area | Tool entry point | Scale |
|---|---|---|
| Plants + generators | `search_plants`, `get_plant` | ~15.5K / ~29.7K |
| Interconnection projects | `search_projects`, `get_project` | ~9.8K |
| Ownership + companies | `get_plant.ownership`, `plants_by_owner` | 4-layer chains |
| Offtakers + PPAs | `get_plant.offtakers` | FERC EQR-derived (partial) |
| Generation + capacity factor | `get_plant.generation` | monthly series |
| Engineering + components | `get_plant.generators[].solar/thermal` | per-generator |
| Pricing / node crosswalk | `get_plant.grid` | LMP node, hub, ISO |
| Financial | `get_plant.financial` | FERC + LBNL + OEDI |
| News facts + extracted events | `search_news`, `get_news_extracted`, `find_by_extracted_fact` | ~57K articles |
| Descriptive context | `get_plant.context` | LLM + Wikipedia (framing) |

Note projects carry their own substrate (`search_projects` returns `technology`, `total_mw`, `status`, `region`); the modern CA queue is multi-GW Solar+Battery (DARDEN `CAISO-1949`, 2,365 MW). The generated engineering substrate catalog in the platform repo is a useful *map* of technical fields and hazards — it is not a task for the insights contributor to regenerate or modify.

## ENSO V0 Data Need

The first resource should separate its inputs like this:

```text
external ENSO state
  -> NOAA CPC / ONI / seasonal outlook          (NOT in substrate — methodology supplies it)

region resolution
  -> climate region to state / ISO / BA / plant scope
  -> ⚠ resolve via state=CA today; search_plants(iso=…) is unwired (see learning/01)

asset substrate
  -> plant location, fuel, capacity, operating status, owner/company   (search_plants → get_plant)

performance / market context
  -> generation, capacity factor, pricing or revenue context where available   (get_plant.generation/grid/financial)

actor context
  -> owner, offtaker, developer, lender/investor relevance   (get_plant.ownership/offtakers)
```

## Source Reference Standard

For v0, every material claim should reference one of:

- an InfraSure substrate source or tool result
- an external source name and vintage/date
- a clearly marked missing input that blocks or downgrades the claim

Minimum source reference shape:

```yaml
source_ref:
  source_type: substrate | external | descriptive | actor_context
  source_name: string
  entity_scope: string
  field_or_fact: string
  vintage_or_accessed_at: string
  role: primary | corroborating | framing | activation
```

Two filled examples (real, 2026-06-05):

```yaml
# grounding
- source_type: substrate
  source_name: "InfraSure get_plant"
  entity_scope: "plant 57993 (Desert Sunlight 300)"
  field_or_fact: "generation.monthly capacity_factor (summer ≈0.38 / winter ≈0.13)"
  vintage_or_accessed_at: "2026-06-05"
  role: primary
# external (the input the substrate cannot supply)
- source_type: external
  source_name: "NOAA CPC ENSO status / ONI"
  entity_scope: "ENSO state for the test winter"
  field_or_fact: "ENSO phase + seasonal outlook"
  vintage_or_accessed_at: "<date pulled during the test>"
  role: primary
```

The `vintage_or_accessed_at` for any substrate ref is the `_meta.as_of` envelope every tool returns. Never drop it — it is what makes the claim auditable later.

## Activation Boundary

Actor/account context matters, but it should not change the analytical method.

```text
methodology resource
  -> validates the insight claim

contacts / account context
  -> routes and renders the validated insight
```

Do not write email copy before the applied insight has passed review.
