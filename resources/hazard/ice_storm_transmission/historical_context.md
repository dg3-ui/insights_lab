# Historical Context — Ice Storm Exposure For Transmission, Wind, and Delivery-Dependent Assets

> **Status**: draft 2026-06-29. The dated realized-event record behind `ice_storm_transmission`. Regional facts + cited public record, **not** per-span / per-plant damage claims. ⚠ **Reconciliation note**: align section headers with the established `historical_context.md` house format if it differs. Generation-side freeze (gas wellhead/pipeline) is `../extreme_cold_winter_storm/` — do not double-count.

## Realized events (dated record)

| Date | Location | What happened (public record) | Mechanism tie-in |
|---|---|---|---|
| Jan 1998 | Northeast US / Quebec / Ontario | **Great Ice Storm of 1998** — catastrophic ice accretion collapsed hundreds of transmission towers and thousands of distribution structures (Hydro-Québec grid hit hardest); weeks-long outages for millions. The textbook ice-load transmission-failure case. | (A) ice-load → conductor/tower mechanical failure |
| Dec 2007 | Oklahoma / Great Plains | **December 2007 ice storm** — one of the most destructive on record for the South-Central grid; ~1.5M+ customers lost power as ice downed T&D across the OK corridor (the test-001 geography; anchor Wagon Wheel Wind, EIA 69224, Logan Co). | (A) transmission ice-load · (C) delivery stranding |
| Jan 2009 | Mid-South (KY/AR/MO) | **January 2009 ice storm** — widespread transmission/distribution failure and prolonged outages across the Mid-South ice belt. | (A) ice-load failure · (C) delivery stranding |

## What the substrate carries about these

The substrate grounds **ice-belt exposure** (plant lat/lon, county within the NOAA/SPIA freezing-rain belt), the **resolved fleet + delivery corridor**, and **ownership** (test 001: AEP/SWEPCO owns both Wagon Wheel and regional transmission — the delivery-corridor hook). It does **not** carry conductor/tower ice-load ratings or line geometry, so a per-span failure cannot be claimed; monthly CF cannot isolate an ice-storm outage from the winter seasonal minimum. The hazard lives on the **wires** — the loss is often grid-side, and a healthy generator can be stranded behind a downed line with no physical-damage signal.

## How history informs the exposure read

History shows the **belt** (where damaging ice storms concentrate) and the **delivery-infrastructure** character of the loss (1998 was a transmission-tower-collapse event, not a generation-equipment event). It does **not** yield a per-span return-period (needs an ice-load model + line ratings). Freezing-rain frequency trends are contested; treat any poleward-shift signal as directional. Keep the boundary with `extreme_cold_winter_storm` (generation-side freeze) clean.

## Citations

```text
Great Ice Storm of 1998 (transmission collapse)            Environment Canada / NWS / Hydro-Québec post-event records
December 2007 Oklahoma ice storm                           NWS / OK utility (OG&E, PSO) restoration records
January 2009 Mid-South ice storm                           NWS / DOE outage reports
NOAA NWS freezing-rain climatology + SPIA Ice Index        https://www.weather.gov/ · https://www.spia-index.com/
InfraSure substrate (test 001, 2026-06-29)                 search_plants(wind, OK) → Wagon Wheel Wind 69224 (Logan Co), AEP/SWEPCO
```

---

**See also**: `knowledge.md` §5 · `examples/applied_insight_001.md` (the validated Wagon Wheel insight) · `../extreme_cold_winter_storm/historical_context.md` (the generation-side freeze sibling).
