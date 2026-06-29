# Sea Level Rise & Storm Surge Exposure For Coastal Thermal, Nuclear, and Grid Assets — Method (human-readable)

> **Status**: draft 2026-06-29. The human-readable companion to `resource.yml` (the structured contract) and `prompt_projection.md` (the session surface). Contract: `../../docs/method/resource_standard.md`. Sibling hazard resources: `../hurricane_high_wind_wind/` (the WIND side of a coastal storm), `../flooding_multi_asset/`, `../hail_solar/`, `../extreme_cold_winter_storm/`, `../wildfire/`.

## What it answers (and what it refuses)

```text
ANSWERS   which coastal thermal/nuclear/substation/offshore-wind-landfall assets sit at tidewater ·
          the TWO timescales (chronic SLR raising the baseline + eroding the cooling-intake design basis vs
          acute surge inundating the switchyard/intake during a storm) · what a realized surge meant regionally ·
          who should plan, monitor, or harden
REFUSES   exact $ loss / EAL / decommissioning cost / payout · the year a site is permanently inundated · forward
          surge probability · inundation depth (site elevation not in substrate) · single-cause CF attribution ·
          outreach before the gate
```

## Scope

Coastal nuclear + gas (thermal) + transmission (substation) + offshore-wind landfall infrastructure (utility-scale ≥ ~50 MW) · one region/market per test (test 001 = Gulf Coast / Texas tidewater) · operating + queue (siting/elevation) · actors: owner-operator · investor · lender · developer.

## Mechanism — TWO timescales (cite `knowledge.md`; do not re-derive)

```text
(CHRONIC) SEA LEVEL RISE — BASELINE CREEP, decades horizon
    relative SLR (global rise + local vertical land motion) raises the mean water level
    → more frequent nuisance / tidal flooding of low-lying equipment
    → erosion of the cooling-intake + switchyard DESIGN FLOOD BASIS the plant was built to
    A PLANNING-HORIZON risk — largely uninsurable creep, not a claim event.

(ACUTE) STORM SURGE — EVENT INUNDATION, hours horizon
    a tropical / extratropical storm pushes a surge above the tide
    → inundation of the switchyard / cooling intake / pump house → outage + damage
    An EVENT — NHC-forecastable during a storm; insurable under coastal flood / surge sub-limits.
```

The two share a geography but have completely different financial logic and time horizons — **do not conflate them**. Both are governed by **site elevation relative to the water surface**, which the substrate does not carry. This resource is the WATER side of a coastal storm; the WIND side lives in `hurricane_high_wind_wind` — cross-reference, do not double-count.

## Procedure (the real tool sequence)

```text
1. hazard state:  NOAA tide-gauge SLR rate (chronic) + NHC SLOSH / FEMA VE zone (acute) AND/OR search_news(category=hazards, query="storm surge")  → VERIFY each
2. scope:         search_plants(fuel="nuclear"/"gas", state="TX", minMw=50)   ⚠ NOT iso= → []; scope by state; filter to tidewater
3. footprint:     get_plant geometry/county + nearby_plants                    → other tidewater assets in the reach
4. context only:  get_plant.generation                                        → ⚠ largely irrelevant for the chronic horizon; cannot resolve an acute surge; state this
5. actor:         get_plant.ownership                                         → owner chain + portfolio tidewater accumulation
6. draft:         assemble the claim grammar; cap confidence; block the $ / inundation-year / surge-probability / depth / single-cause claims
```

## Allowed vs blocked claims

```text
ALLOWED  directional SLR + surge exposure · the chronic/acute distinction (cited) · tidewater cooling-siting
         concentration · realized surge → coastal reach (regional fact) · owner/portfolio tidewater accumulation ·
         mitigation (sea wall, intake redesign, switchyard elevation, relocation planning) recs
BLOCKED  exact $ / EAL / decommissioning / payout · inundation YEAR · forward surge probability · inundation DEPTH ·
         single-cause CF · national-from-regional · outreach-before-gate
```

## Confidence + caveats

Confidence is **per-claim-part**: the *chronic SLR rate at the nearest gauge* and the *mechanism + tidewater exposure* reach **Medium** (NOAA/NHC/FEMA + resolved scope); a *realized surge near a scoped asset* is **factual as a regional event**; any *CF read* is **Low/blocked**. **High is not reachable** on the substrate alone (would need verified site elevation + a served SLR/surge model to claim a depth or a year).

Required caveats: chronic vs acute kept distinct (different horizons + financial logic); exposure driven by site elevation (not in substrate); this is the WATER side (wind = hurricane resource, don't double-count); chronic SLR is uninsurable creep not a claim event; CF is irrelevant/blocked; $ + decommissioning not modeled (model-gpr).

## Actor relevance

Owner (long-horizon adaptation: sea wall, intake redesign, switchyard elevation; cooling design-basis review; decommissioning-timeline implications) · investor (portfolio tidewater accumulation; chronic SLR as stranded-asset / residual-value risk; coastal-insurance tightening) · lender (SLR horizon can exceed debt tenor — directional; coastal-zone + surge-insurance adequacy) · developer (coastal siting + design flood basis + intake/switchyard elevation, incl. offshore-wind landfall infra).

---

**See also**: `resource.yml` · `knowledge.md` (the cited "why" + chronic/acute mechanisms + tidewater-siting + surge anchors) · `prompt_projection.md` · `data_requirements.md` · `../hurricane_high_wind_wind/` (the WIND side) · `../flooding_multi_asset/` · sibling hazard resources.
