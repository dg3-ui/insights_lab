# Knowledge — Severe Hail Exposure For Solar Assets (cited mechanism library)

> **Status**: draft 2026-06-14. The stable "why" for `hail_solar`. Live geography/event state comes from NOAA SPC + the InfraSure `hazards` news category (pulled per test, dated). Cite everything; this never substitutes for substrate grounding.

## 1 · The mechanism

```text
severe hail (≳ 1–2 in / golf-ball+) over a solar array
   → impact energy exceeds module front-glass / cell tolerance
   → cracked cells · shattered front glass · micro-cracks → immediate output loss + latent degradation
   → array-level availability drop until panels are inspected / replaced (weeks–months)
```

Two physical modifiers carry most of the variance — and are where the **(driver × mechanism)** detail lives:

- **Module exposure angle.** A horizontal/low-tilt panel takes hail face-on (worst case). **Single-axis trackers can "hail-stow"** — rotate to a steep angle (~60°) to deflect hail and shrink the impact footprint. Whether a site stows, and how fast, is the single biggest controllable factor. (Fighting Jays is single-axis-tracking c-Si — the stow question is live there.)
- **Module construction.** Thin (2.0 mm) front glass and large-format cells are more hail-vulnerable than thick-glass / hail-rated modules. c-Si dominates utility solar.

## 2 · Robustness & attribution

```text
mechanism (hail damages c-Si arrays)        ROBUST — physical, well-documented (insurance-loss literature)
geography (where damaging hail concentrates) ROBUST — SPC climatology is stable
a realized event hit asset X                FACTUAL when corroborated (multi-source news + substrate)
the forward PROBABILITY at a given site      LOW skill from climatology alone — needs a hail model (blocked here)
climate TREND in hail severity/frequency     CONTESTED — low-to-medium attribution; never assert a trend as settled
```

**Non-stationarity** (standard climate/weather caveat): hail climatology is an odds-shift on a shifting baseline, not a stationary return-period — never state a return-period from a historical record alone.

## 3 · State / event basis

- **Geography**: NOAA Storm Prediction Center (SPC) severe-hail climatology — the **southern Great Plains / Texas is the US hail maximum**. SPC storm reports give dated realized events.
- **Realized events (in-substrate)**: the InfraSure `hazards` news category (`subcategory = hail | hailstorm`) carries `details_json` — `hazard_type`, `affected_area`, `operational_impact`, `affected_mw`, `event_date`, sometimes a qualitative `damage_estimate`. **Verify** each (the classifier has false positives — e.g. a "hails decree" regulatory article).

## 4 · Region / asset-class crosswalk

```text
hail × SOLAR (this resource)   c-Si module/glass damage; tracker hail-stow is the mitigation lever
hail × wind turbine            blade leading-edge erosion (different mechanism → a different resource)
hail × gas / thermal           minimal (different resource) — illustrates why asset-class forks the mechanism
geography                      ERCOT/Texas + the southern Plains carry the bulk of US utility-solar hail exposure
```

## 5 · Canonical realized case (the worked anchor)

**Fighting Jays Solar (EIA 62945, Fort Bend County TX, 227.5 MW AC, single-axis c-Si, CIP-owned).** A mid-March-2024 severe hailstorm damaged the array (multiple sources: PV Tech, Houston Chronicle, Fox News; InfraSure `hazards`/`hail`). The damage is **observable in the substrate generation series** — see `examples/applied_insight_001.md` for the CF figures and the disciplined claim.

## 6 · Citations

```text
NOAA SPC severe-hail climatology + storm reports            https://www.spc.noaa.gov/
InfraSure hazards news (subcategory=hail) — Fighting Jays    PV Tech (2024-03 / 2025-01), Houston Chronicle (2024-03)
utility-solar hail loss mechanism + hail-stow                industry/insurance literature (e.g. kWh Analytics, VDE, RETC)
```

---

**See also**: `data_requirements.md` (where to pull the geography + event state) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the peril-field standard) · `.learning/` (foundational hazard/insurance notes).
