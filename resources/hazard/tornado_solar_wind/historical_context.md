# Historical Context — Tornado Exposure For Solar, Wind, and Substation Assets

> **Status**: draft 2026-06-29. The dated realized-event record behind `tornado_solar_wind`. Regional facts + cited public record, **not** per-plant damage claims. ⚠ **Reconciliation note**: align section headers with the established `historical_context.md` house format if it differs.

## Realized events (dated record)

| Date | Location | What happened (public record) | Mechanism tie-in |
|---|---|---|---|
| Apr 25–28, 2011 | Southeast / Dixie Alley | **2011 Super Outbreak** — one of the largest tornado outbreaks on record (~360 tornadoes), catastrophic damage across AL/MS/TN incl. widespread transmission/substation destruction. | extreme wind + debris → outright structural destruction (mechanism, regional) |
| May 20, 2013 | Moore, OK | **Moore EF5 tornado** — a violent tornado through the Southern Plains corridor (the test-001 geography). Illustrates the corridor's realized severity. | narrow-path total-loss severity in the OK corridor |
| Recurring | Southern Plains (OK/KS/TX) | NOAA SPC documents the Southern Plains as a global tornado-touchdown maximum; utility-scale wind + solar buildout (e.g. the OK fleet — Traverse 63479, Wagon Wheel 69224) places growing nameplate inside the corridor. | corridor exposure — areal climatology, not a per-asset strike rate |

## What the substrate carries about these

The substrate grounds **corridor exposure** (plant lat/lon, county within the SPC touchdown-density band) and the **resolved fleet**, but does **not** carry sub-plant geometry (which rows/turbines) or a per-asset strike probability. Asset-specific destruction records (a tornado crossing a specific array/turbine string) are **case-by-case in the public record** and are not asserted from the substrate — the disciplined claim is geographic intersection risk plus the catastrophic-but-localized framing.

## How history informs the exposure read

A tornado path is a few hundred meters wide: history shows the corridor's **severity** (total loss where a path crosses an asset) but the annual probability of any single asset being struck is **low**. History is therefore evidence that the corridor is high-severity, **not** a basis for annualizing a total loss across a fleet's nameplate. Tornado-frequency/intensity trends are weakly attributable; treat any trend (e.g. a debated eastward Dixie-Alley shift) as directional only.

## Citations

```text
2011 Super Outbreak (Apr 2011)                             NOAA SPC / NWS storm survey records
Moore, OK EF5 (May 20, 2013)                               NWS Norman damage survey
NOAA SPC tornado touchdown-density climatology             https://www.spc.noaa.gov/
InfraSure substrate (test 001, 2026-06-29)                 search_plants(wind, OK) → Traverse 63479 (Custer Co), corridor fleet
```

---

**See also**: `knowledge.md` §5 · `examples/applied_insight_001.md` (the validated Traverse insight) · `data_requirements.md` (gaps) · `../hurricane_high_wind_wind/historical_context.md` (the wide-field wind sibling — the contrast).
