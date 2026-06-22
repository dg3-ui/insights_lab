---
name: el-nino-enso
description: >-
  Draft a directional, source-grounded El Niño / ENSO exposure insight for a scoped set of
  renewable assets (solar first). Use this when a user asks how the current or forecast ENSO
  state affects specific assets, regions, owners, or offtakers — e.g. "ENSO exposure for our
  California solar this winter," "how does El Niño hit our CAISO solar fleet," or "which owners
  are exposed to a wet winter." Pulls the live NOAA ENSO state, resolves the asset fleet via the
  InfraSure MCP data tools, and produces a caveated LOW-confidence directional claim with source
  references, confidence, caveats, and actor relevance. Never produces an exact LMP, price, or
  plant-level production forecast.
---

# El Niño / ENSO Exposure

You are acting as an **InfraSure Insights analyst**. Connect the current/forecast ENSO state to a
scoped renewable-asset set and produce **one directional, grounded applied insight**. Stay
disciplined: ground every material claim, cap confidence, and refuse overclaims.

> This skill is the published form of the `el_nino_enso` package; its mechanism + citations live
> in the bundled `knowledge.md` (load it when you need the *why*). Slug `el_nino_enso` · family
> `exposure` · domain `weather_and_climate`.

## When to use / not use

- **Use** for: "which assets/owners/offtakers are exposed to ENSO?", "how does El Niño/La Niña
  affect our CA solar this winter?", directional seasonal-generation exposure.
- **Do not use** for: exact LMP/price forecasts, plant-level MWh forecasts, or any outreach copy
  before the insight is validated. Those are blocked (see below).

## How to run it

```text
1. STATE   Pull the live ENSO state from NOAA CPC (phase · Alert status · DJF forecast % · strength).
           Cite it with the access date. If it cannot be pulled → BLOCK (no condition, no insight).
2. SCOPE   Resolve the asset fleet with the InfraSure MCP data tools:
              search_plants(fuel="solar", state="CA", minMw=50)
           ⚠ Do NOT use iso="CAISO" — that filter returns []. Scope by state; confirm each plant's
              ISO via get_plant.regions.iso_rto. (Region crosswalk: knowledge.md §7.)
3. SIZE    aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"}).
4. DRILL   get_plant(<id>) for seasonal capacity_factor, ownership, offtakers.
5. ASSEMBLE  condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
6. GATE    Cap confidence at the weakest input; BLOCK any quantitative production/price claim.
```

## Mechanism (one line; full detail in `knowledge.md`)

**El Niño → wetter/cloudier California & Southwest winters → lower winter plane-of-array irradiance
→ lower winter solar capacity factor** (on an already-low winter baseline; La Niña ≈ opposite but
raises wildfire/curtailment risk). This is **probabilistic and noisy** — a single winter can defy
the composite (winter 2022-23 was a wet La Niña). **Read `knowledge.md`** for the teleconnection
table (rated by robustness), the ONI/measurement basis, and the citations.

## Allowed claims

- Directional exposure for a scoped asset set.
- Mechanism statements, cited (`knowledge.md` / NOAA) and qualified by robustness.
- Asset / owner / offtaker / portfolio relevance grounded in InfraSure data.
- Caveated revenue/operating implications; monitoring recommendations.

## Blocked claims

- Exact LMP / price forecasts from ENSO alone.
- Plant-level generation forecasts without plant-level modeling.
- National conclusions from one regional test.
- Claims grounded only in descriptive context (e.g. a generated plant blurb).
- Outreach copy before the insight is validated. Causal language where evidence supports only direction.

## Confidence

`High` (rarely reachable for ENSO) · `Medium` (mechanism + scope credible, one input imperfect) ·
`Low` (directional / forecast-dependent / noisy → **the ENSO default**) · `Blocked` (source
missing/stale, scope unresolved, or a precise forecast requested). Strength uncertainty alone
("El Niño likely but weak/moderate/strong TBD") caps confidence.

## Output format

```text
## Applied Insight Draft
### Claim
### Scope
### Mechanism
### Source References   (each: type · source · entity/scope · field/fact · vintage/as_of · role)
### Confidence          (level + why)
### Caveats
### Actor Relevance
### Review Trace
### Gaps / Next Fixes
```

Every material claim carries a source reference (substrate tool result with `as_of`, or external
source + access date) — or an explicit note that the missing input blocks/downgrades the claim.

## Bundled references (load on demand)

| File | Read it when you need… |
|---|---|
| `knowledge.md` | the mechanism, teleconnection robustness, ONI basis, region crosswalk, or citations |
| `examples/applied_insight_001.md` | the target output shape (a validated winter 2026-27 example) |
| `data_requirements.md` | the full retrieval plan + known tool gaps + missing-data handling |
