# Historical Context — Flood Inundation Exposure For Thermal, Solar, Wind, and Grid Assets

> **Status**: draft 2026-06-29. The dated realized-event record behind `flooding_multi_asset` — the history the resource's exposure claims point back to. Regional facts + cited public record, **not** per-plant damage claims. ⚠ **Reconciliation note**: section structure follows the realized-event material in `knowledge.md` §5; align headers with the established `historical_context.md` house format (the sibling resources' 10th file) if it differs.

## Realized events (dated record)

| Date | Location | What happened (public record) | Mechanism tie-in |
|---|---|---|---|
| Aug 2017 | Gulf Coast / Houston–SE Texas | **Hurricane Harvey** — record rainfall, catastrophic riverine + urban flooding across the Texas Gulf Coast (FEMA DR-4332-TX). The test-001 anchor region (Sabine / Cedar Bayou tidewater thermal). | (A) switchyard inundation · (B) ground-level equipment · (C) cooling-intake — the multi-asset case |
| Jun 2011 | Fort Calhoun, NE (Missouri River) | **2011 Missouri River flood** — Fort Calhoun Nuclear Station was surrounded by floodwater for weeks; the plant was already off-line and remained shut, with flood barriers protecting safety systems. The textbook nuclear-flood-siting case. | (C) water-sited thermal / (A) switchyard — flood-defense design basis |
| Oct 2012 | NY / NJ tidewater | **Superstorm Sandy** — surge inundated low-lying coastal substations and switchyards. (Acute coastal-water overlap; the chronic/acute coastal framing lives in `../sea_level_rise_surge/`.) | (A) substation inundation — cross-ref coastal resource |

## What the substrate carries about these

The InfraSure substrate grounds **exposure geography** (plant lat/lon, county, cooling-water source) and sometimes **in-substrate hazards news** — but it does **not** carry a separable per-plant flood-damage signal. Test 001 (2026-06-29) confirmed this live: Sabine's (EIA 3459) monthly capacity factor **through Harvey** (Aug 2017 = 0.308, Sep 2017 = 0.306) is essentially **normal**, so the series cannot evidence the flood. `search_news(query="flood", state="TX")` returned `[]` that day — no in-substrate event article — so the Harvey leg rests on the public FEMA/NOAA record.

## How history informs the exposure read

History is **evidence of exposure**, not a forward probability. A FEMA flood zone or a past flood-of-record establishes that a geography floods; it does **not** yield a per-site return-period (that needs a flood model + site elevation, which the substrate lacks — see `data_requirements.md` known gaps). Non-stationarity applies: precipitation intensification and remapping shift the baseline, so a historical event is a directional anchor, not a stationary odds estimate.

## Citations

```text
Hurricane Harvey / FEMA DR-4332-TX (Aug 2017)              https://www.fema.gov/disaster/4332 · NOAA NWS Harvey record
2011 Missouri River flood / Fort Calhoun Nuclear Station   NRC event reports + USACE Missouri River flood record (2011)
Superstorm Sandy coastal infrastructure (Oct 2012)         FEMA / DOE post-event reports
InfraSure substrate (test 001, 2026-06-29)                 get_plant(3459) Sabine — CF through Harvey → normal
```

---

**See also**: `knowledge.md` §5 (the canonical case) · `examples/applied_insight_001.md` (the validated Sabine insight) · `data_requirements.md` (gaps) · `../sea_level_rise_surge/historical_context.md` (the coastal-water sibling).
