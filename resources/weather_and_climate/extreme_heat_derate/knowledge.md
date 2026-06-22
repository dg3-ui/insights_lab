# Knowledge — Extreme-Heat Thermal Derate For Solar Assets (cited mechanism library)

> **Status**: draft 2026-06-14. The stable "why" for `extreme_heat_derate`. Live temperature STATE comes from NOAA/CPC (pulled per test, dated); the mechanism magnitude is stable PV physics (cited). This file supplies the *mechanism* + *caveat* slots of a claim — it never substitutes for retrieving asset data. Sibling weather resource: `../el_nino_enso/knowledge.md` (same NOAA-pull + directional-LOW discipline).

## 0 · The three layers (orientation)

```text
DATA       who / where / how much   →  MCP substrate (search_plants, get_plant)        [retrieve, cite as_of]
KNOWLEDGE  why / how the mechanism  →  THIS FILE + cited PV-physics sources             [reason, cite source]
STATE      what is happening now    →  NOAA CPC seasonal temperature outlook            [external, has a clock]
```

A good thermal-derate claim needs all three. The mechanism is stable physics (§1, cited §6); the live STATE (is this a hot-summer lean?) must be pulled fresh every test (§3).

## 1 · The mechanism

```text
high ambient temperature (hot summer afternoon)
   → PV CELL temperature rises well ABOVE 25 °C STC (cells run hotter than ambient under high irradiance)
   → module conversion efficiency falls at the temperature coefficient of power (~ -0.3 to -0.45 %/°C)
   → a MODEST per-panel output de-rate, CONCENTRATED in the hottest afternoon hours
   → inverter / balance-of-system (BOS) thermal derating compounds it (inverters clip / derate when hot)
```

Three physics anchors carry the variance — and the discipline:

- **STC vs reality.** Nameplate is rated at **Standard Test Conditions: 25 °C cell temperature**. In the field, under high irradiance, **cell temperature runs tens of °C above ambient** (NOCT — nominal operating cell temperature — is typically **40–48 °C** at only 800 W/m² and 20 °C ambient). So a 40 °C Texas afternoon can put cells well above 60 °C — every °C above 25 °C costs power at the temperature coefficient.
- **The temperature coefficient of power** for crystalline-silicon (c-Si) modules is roughly **−0.3 % to −0.45 % /°C** (some modules to −0.5 %/°C). This is the magnitude ceiling: the effect is **real but second-order** — a de-rate of a few percent on the hottest panels in the hottest hours, **not** a halving of output.
- **Inverter / BOS thermal derating** compounds the cell effect: inverters and transformers reduce rated output or clip when their own temperatures climb, which also peaks in the afternoon heat.

## 2 · Robustness & attribution — the HONESTY section (this caps the claim)

This is the single most important section in this file. The de-rate is **real physics** but **easy to over-claim**.

```text
mechanism (heat lowers PV efficiency)              ROBUST — physical, well-documented (the temperature coefficient)
the de-rate is MODEST + intra-day                  ROBUST — a few % on the hottest hours, NOT a CF collapse
the de-rate COINCIDES with the ERCOT summer peak   ROBUST + this is the WHY-IT-MATTERS (peak-hour value)
"summer monthly CF is LOW because of heat"          FALSE — summer monthly CF is HIGH (irradiance-dominated). DO NOT.
the exact %/MWh de-rate at plant X                  NOT groundable here — needs a plant-level cell-temp/thermal model (blocked)
climate TREND in heat frequency/severity            DIRECTIONAL — non-stationarity caps it; never a stationary return-period
```

**The defining trap — do NOT read heat off monthly CF.** Utility-scale PV monthly capacity factor is **dominated by irradiance and day length**, so **summer monthly CF is HIGH, not low** (see §5, real data). The thermal de-rate is an **intra-day efficiency** effect: it shaves the *peak* of the daily curve on hot afternoons — it does **not** pull the *monthly average* down below the irradiance baseline. A model that "sees low winter CF and high summer CF" and infers "heat must not matter / heat helps" has the mechanism exactly backwards. **The honest claim is: summer CF is high BECAUSE of irradiance, AND the heat de-rate quietly shaves the most valuable peak hours within those high-CF months.** Confidence is therefore **LOW**, magnitude **MODEST**, the claim **directional + peak-hour-scoped**.

**Non-stationarity** (standard climate/weather caveat): a hot-summer outlook is an **odds-shift on a shifting baseline**, not a stationary return-period — never state a frequency/return-period from a historical record alone.

## 3 · State / condition basis (pull live)

| Input | What it is | Where / use |
|---|---|---|
| **NOAA CPC seasonal temperature outlook** | probability lean toward above-/below-normal seasonal temperature | establishes the hot-summer CONDITION; pull at test time, cite the issue date |
| **NOAA CPC monthly + 6–10 / 8–14 day outlooks** | shorter-lead heat signals | sharpen a near-term claim; same dating discipline |

```text
┌─ SNAPSHOT (NOAA CPC, accessed 2026-06-14 — RE-PULL BEFORE ANY REAL USE) ───────────────────┐
│ Summer 2026 (JJA) seasonal outlook (issued ~mid-May 2026): much of the lower 48 LEANS       │
│ above-normal temperature, HIGHEST confidence in the West. South-central US / Texas is        │
│ inside the broad above-normal lean but NOT the highest-confidence region.                   │
│ → a CREDIBLE but MODEST hot-summer signal for ERCOT/TX → already caps the claim at LOW.      │
│ Source: NOAA CPC seasonal outlook + summary coverage, accessed 2026-06-14.                   │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

The modest, broad nature of the signal is itself analytically important: a "lean above normal, not the top-confidence region" outlook **caps confidence before any asset is named** — exactly as ENSO strength-uncertainty does (`../el_nino_enso/knowledge.md` §3).

## 4 · Why it matters MORE than its size — peak coincidence (the real point)

The de-rate is small, but **when** it lands is what makes it matter:

```text
hot summer afternoon  →  PV cell temp highest  →  thermal de-rate at its MAX
                      ↘                              (the few-% shave is concentrated HERE)
                       └ ERCOT demand + price at their SUMMER PEAK (A/C load) — the most valuable solar hours
   ⇒ the de-rate bites exactly when each MWh is worth the most (merchant / shaped-PPA exposure)
```

So the materiality argument is **not** "heat causes a big energy loss" — it is **"a modest de-rate concentrated in the highest-value hours."** That is the disciplined, defensible framing. ERCOT is the sharpest case in the US: summer-peaking, scarcity-priced, and the #1 solar fleet (§5).

## 5 · The substrate baseline this perturbs (real data — the honesty proof)

Utility-scale PV monthly CF in ERCOT/TX (Aktina Solar **64927**, 500 MW AC single-axis c-Si, Wharton County, ERCOT South). Most recent full year (2025), monthly capacity factor:

```text
winter trough ≈ 0.09–0.15  (Jan 0.094 · Dec 0.150)        summer peak ≈ 0.30  (Jun 0.296 · Jul 0.302 · Aug 0.307 · Sep 0.302)
```

**Summer CF is roughly 2–3× the winter trough** — irradiance-dominated, exactly as expected, and the *opposite* of "heat drags summer CF down." This is the cleanest possible argument for the §2 discipline: the heat de-rate lives **inside** those high-CF summer months as an intra-day, peak-hour efficiency shave — it is **invisible at monthly resolution**, so monthly CF must never be cited *as* the heat signal. (The Feb-2025 CF 0.009 dip is a winter-storm outage, not heat — a reminder that CF moves for many reasons, §2 single-cause caveat.)

## 6 · Region / asset-class crosswalk

```text
heat × c-Si SOLAR (this resource)   efficiency de-rate via the temperature coefficient; peak-hour-concentrated
heat × gas / thermal                capacity de-rate of the turbine (different mechanism → a different resource)
heat × transmission                 line ampacity / sag derating (different mechanism → a different resource)
heat × demand                       A/C load drives the ERCOT summer PEAK — the coincidence that makes §4 bite
geography                           ERCOT/TX = #1 US solar fleet AND a summer-peak, heat-prone market → sharpest case
```

## 7 · Sources (pull STATE live; cite mechanism)

| Source | Use | URL |
|---|---|---|
| NOAA CPC seasonal temperature outlook | the hot-summer CONDITION (above-normal lean) | https://www.cpc.ncep.noaa.gov/products/predictions/long_range/ |
| NOAA CPC 6–10 / 8–14 day + monthly outlooks | shorter-lead heat signals | https://www.cpc.ncep.noaa.gov/ |
| PV temperature coefficient / NOCT references | the mechanism magnitude (~ -0.3 to -0.45 %/°C; STC 25 °C; NOCT 40–48 °C) | PV-physics literature (e.g. PVEducation; Sandia/NREL module-temp work; IEC 61215 NMOT) |

**Citation rule**: every material claim cites either a substrate tool result (with `as_of`) or an external source name + access date. The mechanism magnitude is stable physics (cite §6); the *current temperature state* must always carry the date it was pulled.

---

**See also**: `data_requirements.md` (where to pull the temperature state + the substrate plan) · `resource.yml` (the structured contract) · `../../docs/method/resource_standard.md` (the non-stationarity rule) · `../el_nino_enso/` (the worked weather-resource reference + NOAA-pull discipline).
