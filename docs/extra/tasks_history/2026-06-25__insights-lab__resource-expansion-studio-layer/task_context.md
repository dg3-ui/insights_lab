# Task Context — Resource Expansion + Studio Layer Planning

> **Date**: 2026-06-25
> **Session type**: Methodology catalog expansion + the missing studio-orchestration layer

---

## Objective

Expand the InfraSure Insights methodology catalog from 7 to 10 resources, add a verified historical-context layer across all packages, and identify the next major missing layer: **studio orchestration** — the logic for how validated insights get composed into deliverables (blogs, reports, risk briefs) across multiple crossing dimensions (domain, risk appetite, asset class, actor).

---

## Background

The lab had 7 resources at session start (`el_nino_enso`, `extreme_heat_derate`, `hail_solar`, `hurricane_high_wind_wind`, `offtaker_concentration`, `wildfire` draft, `extreme_cold_winter_storm` draft). The catalog needed to grow, and each new resource now requires a `historical_context.md` — a deep-researched, citation-verified event ledger — which adds meaningful depth but also meaningful verification work per package.

Separately, the `studio/` layer (Layer 3 output) exists structurally but lacks the **orchestration logic** for *which* resources to compose for which deliverable type and actor. That is the next major build.

---

## What We Did

### 1. Added `drought_low_hydro` (weather_and_climate)
- Drought / low-snowpack / low-streamflow × hydropower
- 9 files including PENDING test 001 (California / CAISO hydro ≥ 50 MW)
- New gaps: R21 (plant-to-basin/reservoir linkage), R22 (hydro operations surface), R23 (fuel taxonomy alias)

### 2. Added `hurricane_coastal_flood` (hazard)
- Storm-surge / coastal-flood × energy assets (distinct from riverine)
- Full package: mechanism, FEMA/NHC/SLOSH data stack, component crosswalk
- New gaps: R24 (coastal component elevation), R25 (served surge/inundation overlay)

### 3. Added `historical_context.md` layer across ALL 9 packages
- Template-driven; deep-research workflow + citation verification per file
- 73 citations checked; 70 verified exact; 3 corrected:
  - `extreme_cold_winter_storm`: dead NERC .aspx → working FERC/NERC 2011 PDF
  - `hail_solar`: Midway Solar ">$75M" → ~$70M (consensus, corroborated)
  - `drought_low_hydro`: WAF-blocked CRS link → everycrsreport.com mirror
- Raw deep-research output archived to `archive/historical_context_research/` (outside `resources/`)

### 4. Cleanup
- Deleted `_writetest` (empty stray)
- Moved `extreme-cold-historical-context.{md,json}` from repo root to `archive/historical_context_research/`
- Held back `docs/extra/InfraSure-Customer-Tracker.xlsx` from git (customer list; should stay local or go to gitignore)

### 5. Added `riverine_flood` (hazard) — 10th package
- Inland river corridor / floodplain × energy assets (distinct from `hurricane_coastal_flood`)
- Knowledge layer: 5 hazard sub-types, FEMA AE/AO taxonomy, asset crosswalk, non-stationarity
- `historical_context.md`: 5 deep-researched, citation-verified events:
  - 2019 Missouri-Mississippi (Cooper Nuclear NOUE + WAPA hydro surplus + Offutt AFB)
  - 2011 Missouri River (Fort Calhoun 478 MW / 2.5 yr offline / $180M recommission)
  - 1993 Great Midwest Flood (Des Moines 40K customers; Callaway nuclear operated)
  - 2008 Iowa Flood (Cedar Rapids $225M Alliant damage; Prairie Creek $152M)
  - 2010 Nashville Flood (3 NES substations; TVA $9M substation relocation)
  - Pattern 3 (hydro surplus from extreme inflow) is non-obvious and explicitly documented
- New gaps: R26 (plant-to-HUC/river-reach linkage), R27 (FEMA riverine zone join per plant)

### 6. Registry + gap ledger
- `resources/README.md`: 7 → 10 resources; all new rows + domain table updated
- `docs/status/mcp_gaps.md`: R21–R27 added (priority table + body entries)

### 7. Commits (all pushed to main)
- `8406148` — catalog 9 + historical_context layer + R21–R25
- `ec57698` — docs + studio refresh
- `3088e4e` — riverine_flood (10th package) + R26–R27

---

## Files Created / Modified

### Created (new packages)
```
resources/weather_and_climate/drought_low_hydro/   (9 files)
resources/hazard/hurricane_coastal_flood/          (9 files + historical_context.md)
resources/hazard/riverine_flood/                   (10 files incl. historical_context.md)
archive/historical_context_research/README.md
archive/historical_context_research/extreme-cold-historical-context.{md,json}
```

### Modified (existing packages — historical_context.md added)
```
resources/weather_and_climate/el_nino_enso/historical_context.md      (new)
resources/weather_and_climate/extreme_heat_derate/historical_context.md (new)
resources/hazard/wildfire/historical_context.md                        (new)
resources/hazard/extreme_cold_winter_storm/historical_context.md       (new, 3 citation fixes)
resources/hazard/hail_solar/historical_context.md                      (new, $75M→$70M fix)
resources/commercial/offtaker_concentration/historical_context.md      (new)
```

### Modified (wiring)
```
resources/README.md           (7→10 resources; registry rows; domain table)
docs/status/mcp_gaps.md       (R21–R27 added)
```

---

## Current Status

| Item | Status |
|---|---|
| Catalog size | **10 resources** across 3 domains |
| Test 001 passed | el_nino_enso, extreme_heat_derate, hail_solar, hurricane_high_wind_wind, offtaker_concentration (5/10) |
| Test 001 PENDING | wildfire, extreme_cold_winter_storm, drought_low_hydro, hurricane_coastal_flood, riverine_flood (5/10) |
| historical_context layer | ✅ exists in all 10 packages, citation-verified |
| MCP gaps logged | R1–R27 (27 entries) |
| Studio orchestration logic | ❌ missing — see Next Steps |
| InfraSure-Customer-Tracker.xlsx | ⚠️ uncommitted; add to .gitignore or move out |

---

## Next Steps (in priority order)

1. **Studio orchestration layer** — the most important missing piece (see `decisions.md` + `handoff.md`)
2. `wind_drought` resource (weather_and_climate — next in the catalog queue)
3. A 2nd `commercial` resource (merchant/re-contracting exposure or curtailment/interconnection cost)
4. Run test 001 on PENDING resources when studio logic is ready (gate is intentional)
5. Resolve `InfraSure-Customer-Tracker.xlsx` (gitignore or move)
