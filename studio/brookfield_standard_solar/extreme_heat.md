# Studio Brief — Solar's Most Over-Weighted Peril, Right-Sized for a Fixed-Price Book

> **Subject**: Brookfield / Standard Solar (account) · **Phenomenon**: extreme-heat thermal derate (`../../resources/weather_and_climate/extreme_heat_derate/`)
>
> **Output type**: report · **As of**: 2026-06-15 · **Audience**: internal (Brookfield/Standard Solar account team; render path also client) · **Grounding**: MCP-grounded (InfraSure substrate — monthly CF, construction, PPA price) + research-grounded heat state (NOAA CPC) + cited PV physics
>
> **A cloud-attachable brief**: attach this + `../../resources/_style/brand.md` + `../../resources/_principles/voice.md` (+ `_craft` if charts) → render for the target format. **Post-gate only** — this brief dresses a *validated* insight (the three guards, `../README.md`).
>
> ⚠ **GROUNDING FRESHNESS — re-ground on use.** Substrate figures are a dated **MCP snapshot** (get_plant pulls 2026-06-15); the `renewablesinfo_org` platform fetch may not have been re-run, and the **NOAA CPC summer outlook must be re-pulled** (the one cited here is a 2026-06-14 snapshot). **Before any external use — and whenever this brief is loaded as a skill in a live session — re-fetch the named entities + the temperature outlook, confirm currency, and reconcile drift** (`../README.md`).

## 1 · The validated insight (the gated content — grounds everything · SINGLE SOURCE OF TRUTH)

**Condition.** Extreme heat lowers PV output through the **temperature coefficient of power**: under high irradiance, c-Si cell temperature runs tens of °C above ambient (NOCT 40–48 °C), and every °C above the 25 °C STC rating costs roughly **−0.3 % to −0.45 %/°C** (`../../resources/weather_and_climate/extreme_heat_derate/knowledge.md` §1). NOAA CPC's summer-2026 (JJA) outlook leans **above-normal, with the highest confidence in the West** — where this book's hot-climate plants sit (snapshot accessed 2026-06-14; **re-pull before use**).

**The defining discipline (do not get this wrong — `knowledge.md` §2).** The de-rate is a **second-order, intra-day, peak-hour** efficiency effect — **not** a capacity-factor collapse. It is **invisible at monthly resolution**: summer monthly CF is HIGH (irradiance-dominated), and reading a heat signal off monthly CF is an explicit blocked error. City of Gallup (62406) proves it: summer CF peaks at **~0.35 (Jun)** against a winter trough of **~0.10–0.15 (Dec–Jan)** — summer is ~2.5–3× winter, the *opposite* of "heat drags summer down." (The slight Jul–Aug softening below the June peak is **consistent with the NM summer-monsoon cloud cover, not attributable to heat** — single-cause is refused.)

**Scoped entities.** The heat-exposed slice is the book's **hot, low-elevation interior** — concentrated in **CA (Kern County, ~20.4 MW) and NM (~43 MW)**, ~18% of MW. Two grounded data points (`get_plant`, as_of 2026-06-15):

| Plant | EIA | State / county | MW | Construction | Heat-relevant read |
|---|---|---|---|---|---|
| **City of Gallup Solar** | 62406 | NM / McKinley | 8 | **single-axis c-Si** | summer CF ~0.35; **fixed PPA $44.08/MWh**; high desert (~6,500 ft) *moderates* cell temp |
| **Nachtigall 1836-WD** | 67747 | CA / Kern (CAISO) | 4.6 | **fixed-tilt** (per description) | online Dec-2024, no usable CF yet; low-elevation San Joaquin valley heat is the hotter case |

**Mechanism + why it matters (cite — `knowledge.md` §1, §4).** high ambient → cell temp ≫ 25 °C STC → efficiency falls at the temp coefficient → a **modest few-% shave concentrated in the hottest afternoon hours**, compounded by inverter/BOS thermal derating. The de-rate matters *more than its size* only where it coincides with a **peak price/demand window** that the asset's revenue actually captures — i.e. a **merchant or shaped/peak PPA** book.

**Claim.** Standard Solar's heat exposure is **directional, modest, and — for this book — the least material of its perils**. The physical de-rate is real but second-order and confined to the hot CA/NM interior (~18% of MW), and its one materiality amplifier (peak-hour revenue coincidence) is **muted by the book's fixed-price contract structure**: the substrate confirms a **fixed $44.08/MWh PPA** on Gallup (62406), the community-solar signature, which does not capture peak-hour scarcity value. A fixed-price community-solar book in the West therefore feels heat as a quiet efficiency factor, not a revenue event. This is an odds-shift exposure, not a production or revenue forecast.

**Source references** (each: type · source · scope · field · as_of · role):

```text
1. external · NOAA CPC seasonal temperature outlook (JJA 2026) · above-normal lean, highest confidence in the West · accessed 2026-06-14 (RE-PULL) · STATE (the hot-summer condition)
2. external · PV temperature-coefficient / NOCT references (PVEducation, NREL/Sandia) · ~ -0.3 to -0.45 %/°C, STC 25 °C, NOCT 40–48 °C · stable physics · LOGIC (the de-rate magnitude ceiling)
3. substrate · InfraSure get_plant(62406) City of Gallup · single-axis c-Si, monthly CF (Jun ~0.35 / Dec ~0.10–0.15), fixed PPA $44.08/MWh, McKinley Co NM, PNM/WECC · as_of 2026-06-15 · GROUNDS (summer-CF baseline + fixed-price structure)
4. substrate · InfraSure get_plant(67747) Nachtigall 1836-WD · 4.6 MW fixed-tilt, Kern Co CA, CAISO; online Dec-2024 (no usable CF) · as_of 2026-06-15 · GROUNDS (CA Kern hot-valley data point + mixed construction)
5. substrate · InfraSure plants_by_owner state split · CA 20.4 MW + NM 43.0 MW = the hot-interior slice (~18% of 355.3 MW) · as_of 2026-06-15 · GROUNDS (the exposed share)
6. logic · extreme_heat_derate/knowledge.md §1–§5 + resource.yml · mechanism, the monthly-CF trap, peak-coincidence, the no-model/no-$ caps · cited · LOGIC (confidence ceiling + the discipline)
```

**Calibration — the three axes (`../../docs/method/confidence_model.md`).** Single source of truth; output posture and the triage ranking derive from it.

| Axis | Value | Basis |
|---|---|---|
| **Calibration cap** (internal) | **LOW (directional)** | the resource default — a second-order effect with no plant-level cell-temp/thermal model (`extreme_heat_derate` confidence_rules "low"); the de-rate magnitude is blocked. |
| **Event likelihood** (on output) | **NOAA JJA above-normal lean, highest confidence in the West** (accessed 2026-06-14; re-pull) | a credible-but-modest, dated seasonal signal — caps confidence before any asset is named. |
| **Materiality** (internal) | **low** (below ENSO's *modest*) | exposed-share ~18% (CA/NM hot interior) × class-severity = **low for this book**: the de-rate is modest physics AND its peak-revenue amplifier is **muted by the fixed-price PPA** (Gallup $44.08/MWh) — no merchant/shaped exposure to capture the peak-hour sting. |

**On output**: posture *"a forward, directional read — solar's most over-weighted peril, correctly sized down for this book"* + the NOAA summer-outlook frame. A settledness bar applies only weakly (the JJA outlook is near-resolved as of mid-June). The cap grade and materiality band stay internal.

**Caveats** (`extreme_heat_derate` required caveats):

- This is a **second-order, modest, intra-day** efficiency effect concentrated in the hottest afternoon hours — **not** a capacity-factor collapse.
- **Summer monthly CF is HIGH** (irradiance-dominated); the heat de-rate does **not** show up as a monthly-CF drop, so monthly CF is not a heat signal. The Jul–Aug softening at Gallup is consistent with NM monsoon cloud, not heat.
- **No per-plant %/MWh de-rate, no $, no MWh impact** — these need a plant-level thermal model (`model-gpr`, blocked here). Directional only.
- The materiality muting rests on a **fixed-price structure confirmed on one asset** (Gallup); the book-wide offtake mix is otherwise unresolved (`offtakers` field null — see `offtaker_concentration` scaffold + mcp_gap R13). If any sites are merchant/shaped, their heat-at-peak exposure is higher.
- High-elevation NM (Gallup ~6,500 ft) runs cooler cells than its latitude implies; the hotter case is the low-elevation CA Kern valley. Construction is **mixed** (Gallup single-axis, Nachtigall fixed-tilt).
- Climate non-stationarity caps any trend claim: a hot-summer outlook is an odds-shift on a shifting baseline, not a stationary return-period.

**Actor relevance.** *Owner/operator:* heat is a thermal-aware-design + O&M factor (inverter sizing, ventilation), not a portfolio risk for this book; no special action beyond standard hot-weather O&M on the CA/NM sites. *Investor:* the least material of the book's perils — note it and move on; the fixed-price structure is the reason. *Lender:* P50/P90 generation assumptions already absorb a modest thermal derate; directional, immaterial to DSCR here. *Offtaker:* would matter on a shaped/peak PPA — not the community-solar fixed-price case.

**Review trace.** Checked vs `extreme_heat_derate` `blocked_claims`: no per-plant %/MWh de-rate (✓); no $/MWh impact (✓); no plant-level forecast (✓); no forward probability/return-period (✓); **no heat read off monthly CF** (✓ — explicitly disciplined, summer CF shown HIGH); no single-cause (✓ — Jul/Aug softening attributed to monsoon, not heat); not national-from-regional (✓). Every material number carries a substrate `source_ref` with as_of, or the NOAA/physics source. Cap LOW (no thermal model). **Gate: PASS (draft — pending owner checkpoint + a live re-ground per the freshness note).**

## 2 · The comparison (the moat + the hook)

The home-run move is **discipline as the differentiator**: a vanilla model, shown high summer CF, will say "heat doesn't hurt solar — summer output is highest" (the §2 trap, exactly backwards), or it will over-claim a big "heat loss." The grounded read does neither:

```text
WHAT A VANILLA MODEL SAYS          THE GROUNDED READ (InfraSure)
"summer CF is high, so heat helps"  Gallup (62406) summer CF ~0.35 IS high — but that is IRRADIANCE; the heat
                                    de-rate is an intra-day peak-hour shave, invisible at monthly resolution
"heat will cost X% of generation"   magnitude is blocked (no thermal model); the honest claim is directional
[no contract awareness]             the de-rate-at-peak only bites a MERCHANT/shaped book; Gallup's FIXED $44.08/MWh
                                    PPA mutes it — so heat is this book's LEAST material peril
```

The hook is the **right-sizing**: naming a real peril, refusing to inflate it, and grounding *why* it is small for this specific book (the fixed-price structure, a real substrate field). That calibration is the product — it is what a general model cannot do without the contract data and the discipline.

## 3 · Creative & Activation (the cherry — bounded by the guards)

```text
HERO VISUAL    Gallup's (62406) monthly CF curve (2018–2023) with the summer months HIGH (~0.35) and a one-line
               annotation: "summer CF is high (irradiance); the heat de-rate is the intra-day peak-hour shave you
               can't see at this resolution." A small side-note: "fixed PPA $44.08/MWh → the peak sting is muted."
               Every series a source_ref + as_of (_craft). The visual SAYS only what §1 gated.
PUNCHLINE/HOOK "Heat is solar's most over-weighted risk. For a fixed-price book, it's a footnote — here's why."
               (Catchy on the FRAMING — the right-sizing is the story. No number inflated; the de-rate magnitude
               is withheld, summer CF shown high. Guard 2 held.)
COMPARISON     "The de-rate bites at the afternoon peak. A merchant plant feels it in revenue; a fixed-$44/MWh
               community-solar plant doesn't. Standard Solar's contracts do the work." Grounded in the Gallup PPA price.
CONFIDENCE     On the rendered face: posture "a forward, directional read" + the NOAA summer-outlook frame. No
               "CONFIDENCE: LOW" badge; the cap grade + materiality band are internal (confidence_model.md §3).
FORWARD DOOR   "This is the directional read. The per-asset thermal modeling — cell-temp, inverter derate, the
               peak-hour $ at each site's actual contract — is where InfraSure goes deeper." (P7: a door, never
               "we run no thermal model.")
CHANNEL NOTES  report subject-line: "Extreme heat and the Standard Solar book — real physics, immaterial revenue, here's why."
               blog title (if generalized, scrub the account): "Why high summer CF doesn't mean heat is free."
               email one-liner (post-gate, human-reviewed, named account only): "Heat is solar's most over-weighted
                 peril; for this fixed-price book it's a modest intra-day derate, not a revenue event. No action beyond O&M."
               Send stays human-in-the-loop (post-gate, `../../docs/use_cases.md` activation boundary).
```

## 4 · Render notes

```text
COMPOSE     brand.md Part A (Inter, amber=solar accent, lifted boxes, bones) → target via Part B (HTML default;
            DOCX on request) · voice.md (claim-first, no m-dashes) · _craft (the Gallup CF curve, each series a
            source_ref + as_of) · output_contracts.md §3 (report envelope: lead with the discipline + the slice).
GATE        renders ONLY the §1 validated insight; every number traces to a §1 source_ref (P2). Confidence display
            (confidence_model.md §3): posture + the NOAA frame; no "LOW" badge. RE-GROUND before external use.
GUARDS      gate-upstream · creative≠overclaim (the de-rate magnitude is withheld; the punch is the right-sizing) ·
            grounded-hook (the $44.08 PPA + the high summer CF are real get_plant results). All three held.
```

## 5 · Gaps / next

```text
· FRESHNESS — figures are a 2026-06-15 MCP snapshot; the NOAA summer outlook is a 2026-06-14 snapshot. Re-ground + re-pull on use.
· OFFTAKE — the materiality muting rests on ONE confirmed fixed PPA (Gallup $44.08); the book-wide offtake mix is
  unresolved (offtakers field null). Resolving it (mcp_gap R13, owner-level offtake rollup) would confirm/qualify
  "heat is immaterial" across the whole book. Pairs directly with the offtaker_concentration phenomenon.
· CONSTRUCTION — mixed tracker/fixed (Gallup single-axis, Nachtigall fixed-tilt); a fuller get_plant pass on the
  CA/NM assets would sharpen both the heat (inverter/BOS) and the hail (hail-stow) reads.
· MATURITY — the per-plant %/MWh thermal de-rate is model-gpr (grounding_maturity: substrate-only). Directional ships
  now; the quantified layer is the forward door (mcp_gaps R12 — a served thermal model upgrades directional → quantitative).
· SEASONAL PAIR — read with el_nino_enso.md: ENSO is the winter-irradiance lever, heat the summer-derate lever — the
  two weather drivers bound the book's weather-normalized output band in opposite seasons (the guide's cross-resource map).
· FORM — if this lands, promote toward ../../resources/_reference/internal/report/ as the "right-sized peril / discipline-as-product" exemplar.
```
