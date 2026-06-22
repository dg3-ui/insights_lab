# Methodology Resource - El Niño / ENSO Exposure

> **Status**: v0 resource, deepened 2026-06-05.
>
> **Resource slug**: `el_nino_enso` (Skill `name`: `el-nino-enso`).
>
> **Purpose**: guide a model through **directional exposure** analysis connecting ENSO state/forecast to renewable assets, regions, owners, offtakers, and actor relevance — disciplined, source-grounded, and caveated.

This file is the **method** (the control surface). It sits on two companions:
- `knowledge.md` — the **mechanism library** (what ENSO is, how it teleconnects, rated by robustness, cited).
- `data_requirements.md` — the **input map** (what to retrieve, from which tool, and what to do when it is missing).

## 1. Question Grammar

Allowed:

```text
Which assets, regions, owners, or offtakers are directionally exposed to the current or forecast ENSO state?
Through what mechanism are they exposed?
What can InfraSure claim with confidence, and what must remain caveated?
Who should monitor the exposure, and why?
```

Not allowed:

```text
What exact LMP impact will ENSO cause?
What exact plant-level generation loss will occur?
Which accounts should receive an outreach email before the insight is validated?
```

## 2. Scope

| Scope Type | V0 Value |
|---|---|
| Entity types | plant, generator, company/owner, offtaker where available |
| Technologies | solar first; wind/hydro optional context only |
| Region / market | one selected market or region per test |
| Lifecycle phase | operating assets first |
| Actors | owner/operator, investor, lender, offtaker |

Recommended first test: **CAISO solar ≥ 50 MW**, resolved via `state="CA"` (the `iso` filter is unwired — see §5).

## 3. Mechanism

Full detail lives in `knowledge.md` (§4–§6). The conservative v0 chain:

```text
ENSO state / forecast (NOAA CPC — pulled live)
  -> regional weather/irradiance tendency (knowledge.md teleconnection table, rated by robustness)
  -> affected solar asset or fleet scope (substrate)
  -> owner / offtaker / portfolio exposure (substrate)
  -> caveated revenue/operating relevance
```

For California solar specifically: **El Niño → wetter/cloudier CA winters → lower winter POA irradiance → lower winter capacity factor** on an already-low winter baseline. This is a **probabilistic, odds-shifting** mechanism — name the claim type as *directional*, never causal/quantitative. (See the 2022-23 counter-example in `knowledge.md` §5 for why.)

## 4. Required Inputs

| Input | Type | Required? | Source / tool |
|---|---|---|---|
| ENSO state / forecast (+ Alert status, strength) | external | **required** | NOAA CPC / IRI (pull live) — `knowledge.md` §3, §8 |
| Teleconnection mechanism + robustness | knowledge | **required** | `knowledge.md` §4–§6 |
| Plant locations, fuel/technology | substrate | **required** | `search_plants` → `get_plant` |
| Capacity, operating status | substrate | **required** | `search_plants` (`minMw`, status) |
| Owner / company context | substrate / actor | recommended | `get_plant.ownership`, `plants_by_owner` |
| Offtaker / PPA context | actor | optional | `get_plant.offtakers` |
| Generation / capacity factor | substrate | optional | `get_plant.generation` (seasonal CF) |
| Pricing / revenue context | substrate | optional | `get_plant.grid` / `financial` (caveated only) |
| Descriptive plant/company context | descriptive | optional | `get_plant.context` (frames only — never grounds) |

## 5. Procedure

```text
1. Pull the ENSO STATE live from NOAA CPC (phase, Alert status, DJF forecast, strength). Cite it with the access date.
2. State the regional mechanism + its robustness from knowledge.md; name the claim type (directional / statistical / causal).
3. Select one region/market + one asset class for the test.
4. Retrieve substrate for assets in scope:
     search_plants(fuel="solar", state="CA", minMw=50)
     ⚠ NOT iso="CAISO" — that filter returns []; scope by state, confirm per-plant via get_plant.regions.iso_rto
5. Filter to material operating assets (recommended ≥ 50 MW).
6. Drill (get_plant) for capacity, seasonal CF, owner, offtaker. Retrieve owner/company + optional offtaker context.
7. Draft the claim: condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance.
8. Cap confidence at the weakest link (knowledge.md §6). Block or downgrade any claim that exceeds the evidence.
```

## 6. Allowed Claims

- Directional exposure claims for a scoped asset set.
- Mechanism statements linking ENSO to regional weather/irradiance/demand tendencies, **cited** to `knowledge.md` / NOAA and qualified by robustness.
- Asset, owner, offtaker, or portfolio relevance grounded in InfraSure substrate.
- Caveated revenue/operating implications, clearly marked directional.
- Monitoring recommendations for owners, investors, lenders, or offtakers.

## 7. Blocked Claims

- Exact LMP forecasts from ENSO alone.
- Exact plant-level generation forecasts without plant-level resource/weather modeling.
- National conclusions from one regional test.
- Claims based only on generic climate commentary or on descriptive context (e.g. the Gemini plant description).
- Outreach copy before the applied insight is validated.
- Causal language where the evidence supports only correlation or directional exposure.

## 8. Confidence Rules

| Confidence | Rule |
|---|---|
| High | Narrow mechanism, current source, resolved scope, no downstream forecast — **rarely reachable for ENSO** |
| Medium | Regional tendency + asset scope credible but one input/crosswalk imperfect |
| Low | Scenario/forecast-dependent, directional, noisy teleconnection — **the ENSO default** |
| Blocked | ENSO source missing/stale, scope unresolved, or a precise market/plant forecast is requested |

Strength uncertainty alone (e.g. "El Niño likely but weak/moderate/strong TBD") caps the claim before scope is even resolved. See `knowledge.md` §6.

## 9. Required Caveats

- Directional exposure is not a plant-level production forecast.
- ENSO teleconnections are probabilistic and vary by region, season, and event strength.
- Any single winter can defy the composite (2022-23: wet La Niña CA winter).
- Market-price effects depend on demand, hydro, congestion, marginal generation, and market structure.
- Asset-level relevance depends on owner, offtaker, contract, and operating context.

## 10. Actor Relevance

| Actor | Why They Care | Rendering |
|---|---|---|
| Owner / operator | Monitor seasonal operating variance + asset concentration | platform card, account note |
| Investor | Portfolio concentration + downside sensitivity | platform card, portfolio note |
| Lender | Operational/revenue stress signals for financed assets (DSCR sensitivity to a low-generation winter) | account note |
| Offtaker | Exposure in linked supply assets where PPA context exists | account note, informative email draft (post-validation) |

## 11. Staleness Signals

- NOAA/CPC ENSO status or Alert level changes (Watch → Advisory, phase flip).
- Seasonal outlook / strength probabilities shift materially.
- New plant/generator/owner/offtaker data lands.
- Region crosswalk changes, or the `iso` filter gets wired (retire the `state` workaround).
- Pricing or generation substrate gains a better source for the scoped region.

## 12. Review Notes

The first manual test (`test_runs/test_run_001.md`) checks whether: the prompt projection is strict enough; existing MCP tools resolve the scoped assets/actors; external ENSO handling is clear; the model avoids overclaiming market/plant-level impacts; and the applied-insight thin contract is sufficient for review. Results from that run feed back into this file, `knowledge.md`, and the projection.
