# Historical Context — Sea Level Rise & Storm Surge Exposure For Coastal Thermal, Nuclear, and Grid Assets

> **Status**: draft 2026-06-29. The dated realized-event record behind `sea_level_rise_surge`. Regional facts + cited public record, **not** per-plant damage claims. ⚠ **Reconciliation note**: align section headers with the established `historical_context.md` house format if it differs. This is the WATER side; the WIND side is `../hurricane_high_wind_wind/`.

## Realized events (dated record)

| Date | Location | What happened (public record) | Mechanism tie-in |
|---|---|---|---|
| Oct 2012 | NY / NJ tidewater | **Superstorm Sandy** — storm surge inundated coastal substations and switchyards; Oyster Creek (NJ) declared an alert as water rose at its intake; widespread coastal-grid outages. The textbook ACUTE-surge case. | (ACUTE) surge inundation of switchyard / intake |
| Aug 2005 | Gulf Coast (LA/MS) | **Hurricane Katrina** — surge devastated Gulf Coast electrical infrastructure incl. coastal substations and tidewater generation. | (ACUTE) surge inundation, Gulf Coast |
| Chronic / ongoing | SE Florida (e.g. Turkey Point) + Gulf tidewater | Documented chronic **sea-level-rise + saltwater-intrusion** concern at tidewater nuclear/thermal siting; rising baseline erodes the cooling-intake design flood basis over the planning horizon. The test-001 anchor (South Texas Project, EIA 6251, Matagorda Co) is this siting class. | (CHRONIC) SLR baseline creep → design-basis erosion |

## What the substrate carries about these

The substrate grounds **tidewater exposure** (plant lat/lon, coastal county) and the **resolved coastal fleet**, but does **not** carry site elevation, the design flood basis, or a per-site inundation depth/year. Test 001 (2026-06-29) isolated South Texas Project (6251) as the coastal anchor by county/lat-lon, distinguishing it from inland TX nuclear (Comanche Peak 6145). Monthly CF is irrelevant for the chronic horizon and cannot resolve an acute surge.

## How history informs the exposure read

The two timescales carry different historical logic. **Acute** events (Sandy, Katrina) are dated, insurable, and establish the surge envelope for a reach. **Chronic** SLR is a *rising baseline* — among the best-attributed climate signals — so a historical design flood basis is **optimistic**, not stationary; the exposure grows over decades. Neither yields a per-site depth or inundation year without a model + site elevation (see `data_requirements.md` gaps). Keep the two distinct; do not double-count the wind side (`../hurricane_high_wind_wind/`).

## Citations

```text
Superstorm Sandy coastal grid + Oyster Creek alert (2012)  FEMA / DOE / NRC event reports
Hurricane Katrina Gulf infrastructure (2005)               DOE / FEMA post-event reports
Sea-level-rise + tidewater-nuclear siting (chronic)        NOAA tide-gauge SLR trends · NRC / EPRI coastal-siting literature
InfraSure substrate (test 001, 2026-06-29)                 search_plants(nuclear, TX) → South Texas Project 6251 (Matagorda Co)
```

---

**See also**: `knowledge.md` §5 · `examples/applied_insight_001.md` (the validated South Texas Project insight) · `../hurricane_high_wind_wind/historical_context.md` (the WIND side) · `../flooding_multi_asset/historical_context.md` (the inland/riverine sibling).
