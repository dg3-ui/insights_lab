# Brookfield / Standard Solar — Multi-Phenomenon Exposure Guide

> **Status**: v0, 2026-06-15. The **subject index** for the Standard Solar account: one place that profiles the book and ranks the phenomena that drive risk to it, each linking to its gated brief. A subject folder earns a README once it carries **≥2 phenomena** (`../README.md`); this is the first to.
>
> **What this is.** Not a new claim — a **guide**. It composes the per-phenomenon briefs in this folder into an account-level read: *what is this book, which drivers matter to it, in what order, and where does each go deeper.* Loaded with the briefs + the shared layers, it behaves like a per-account **skill**: hand it to a Claude session and it knows how an InfraSure analyst reasons over THIS book.
>
> ⚠ **GROUNDING FRESHNESS — re-ground on use.** Every number here and in the briefs is a **dated MCP snapshot** (latest pull 2026-06-15); the upstream `renewablesinfo_org` platform fetch was not freshly re-run. The book size already drifted between pulls (129/362.3 MW → 127/355.3 MW). **Whenever this guide is loaded as a skill in a live Claude session, the first step is to re-fetch the book against the live InfraSure MCP** (`plants_by_owner("Standard Solar")` + `get_plant` on the named assets), confirm the platform data is current, and reconcile any drift before asserting a number externally. The methodology is stable; the figures are perishable.

## The book (the account profile — grounded, re-ground on use)

```text
Standard Solar — a Brookfield Renewable distributed-generation / community-solar developer-owner
  ~129 plants / ~362.3 MW   (127 / 355.3 MW solar-primary, 2026-06-15 filtered pull)
  ~2.81 MW per plant        ← the DG/community-solar signature: many small sites, not utility-scale
  geographic spread          IL · MN · NM · VA · MD · CA · CO · ID · NJ · DE · MA · ME · NY · RI · DC · PA · WI · OR · VT
```

**The book's structural defense is its spread.** 129 plants averaging 2.8 MW across ~19 states means no weather or hazard driver can *concentrate* on it the way it would on a few large utility-scale sites. That single fact recurs in every phenomenon below — it is why the reads come back "real but diversified" rather than "portfolio event."

## The phenomenon matrix (what drives risk to THIS book, ranked)

Ranked by the triage logic (cap × materiality, `../_triage.md`); the cap grade + materiality band are **internal**, shown here because this guide is an internal index.

| Phenomenon | Resource | Exposed slice (grounded) | Cap | Materiality | Verdict | Brief |
|---|---|---|---|---|---|---|
| **Severe hail** | [`hail_solar`](../../resources/hazard/hail_solar/) | **0 MW** in the US hail maximum; ~6% CO Front Range + ~41% MN/IL/NM convective | low (directional) | **meaningful** | **WATCH (high)** | [hail.md](hail.md) ✅ |
| **El Niño / ENSO** | [`el_nino_enso`](../../resources/weather_and_climate/el_nino_enso/) | ~23% of MW in the SW belt (CA/NM/AZ/NV/CO/UT) | low (directional) | **modest** | **WATCH (low)** | [el_nino_enso.md](el_nino_enso.md) ✅ |
| **Extreme-heat derate** | [`extreme_heat_derate`](../../resources/weather_and_climate/extreme_heat_derate/) | ~18% hot interior (CA Kern + NM); a modest intra-day peak-hour derate | low (directional) | **low** (muted by fixed-price PPAs) | **NOISE** (logged; no action beyond O&M) | [extreme_heat.md](extreme_heat.md) ✅ |
| **Offtaker concentration** | [`offtaker_concentration`](../../resources/commercial/offtaker_concentration/) | community-solar subscriber base; `offtakers` field null book-wide | **BLOCKED** | — | — (refused at gate) | scaffold ↓ (mcp_gap R13) |

**Reading the matrix.** All three weather/hazard reads carry a **low directional cap** — so they are ordered purely by **materiality / class-severity**: **hail** (meaningful — it physically breaks panels, solar's costliest peril) → **ENSO** (modest — a mild winter-CF nudge) → **extreme heat** (low → **NOISE** — real physics, but a modest intra-day derate whose peak-hour revenue sting is *muted by the book's fixed-price PPAs*). That ordering is the materiality axis doing its only job; the geographic spread keeps even the top read at WATCH, never ACT (`../../docs/method/confidence_model.md` §4). **Offtaker concentration is BLOCKED, not low** — the `offtakers` field is null book-wide (a fixed PPA *price* surfaces on Gallup, but not the counterparty), so concentration cannot be sized until an owner-level offtake rollup exists. The honest output is a logged gap (mcp_gap R13), never a fabricated "low."

## Blocked / queued phenomena (NOT grounded — do not assert)

What belongs on the book but is not yet a gated brief. Offtaker concentration was run through the loop and came back **blocked** (the data gap below) — the honest outcome is a logged gap, not a brief. **No numbers until grounded + gated** (P2 — studio is post-gate; this is a queue + a gap log, not a claim).

```text
OFFTAKER CONCENTRATION (offtaker_concentration) — BLOCKED, gap confirmed 2026-06-15
  WHY it matters   the commercial overlay: who buys the output. A community-solar book is MANY small subscriber
                   contracts → concentration is likely LOW by design (the opposite of a merchant-exposed book).
  WHAT WE FOUND    get_plant.offtakers is NULL book-wide (re-confirmed on 62406 + 67747, 2026-06-15). A fixed PPA
                   PRICE does surface for some assets (Gallup 62406 = $44.08/MWh) — a fixed-vs-merchant STRUCTURE
                   signal — but NOT the counterparty identity, so concentration cannot be sized.
  STATUS           BLOCKED (refused at the gate): the concentration claim has no grounding. Logged as mcp_gap R13
                   (serve a first-class offtakers array + group_by=buyer on aggregate). DO NOT assert "low" — the
                   honest output is the gap. The fixed-price structure signal is used (carefully) by hail.md/heat.md.
  WHEN UNBLOCKED   an owner-level offtake/counterparty rollup (R13) OR external contract disclosure → then ground it.
```

## Cross-resource map (how the phenomena relate)

```text
                         act on SOLAR CAPACITY FACTOR (output)        a PHYSICAL-DAMAGE peril        a COMMERCIAL overlay
                         ─────────────────────────────────           ──────────────────────        ───────────────────
  el_nino_enso   ───►    winter irradiance shift (SW belt, DJF)
  extreme_heat   ───►    summer temp-derate (SW belt, JJA)            hail_solar  ───► panel        offtaker_concentration
       │                      └─ same asset class, opposite season         │            damage          ───► who buys output
       └──────────────── the book's GEOGRAPHIC SPREAD dampens all three ───┴──────────────────────────────────┘
                         (the recurring structural defense — many small plants, ~19 states)
```

- The two **weather** drivers (ENSO, heat) act on the *same* solar-CF mechanism in *opposite* seasons — read together they bound the book's weather-normalized output band.
- **Hail** is the odd one out: not a CF nudge but a catastrophic physical peril (hence higher materiality at a lower exposed share).
- **Offtaker concentration** is orthogonal — the commercial question layered on the physical reads.
- All four are dampened by the same thing: the book is spread thin by construction.

## How to use this guide (the skill note)

```text
1. RE-GROUND FIRST    re-fetch the book against the live MCP (freshness note); reconcile drift before any number ships.
2. PICK THE LENS       the matrix ranks the phenomena; lead with the highest-verdict one for the question asked.
3. STAY POST-GATE      the two ✅ briefs are gated drafts (pending owner checkpoint); the scaffolds are NOT claims —
                       ground + gate them through the test loop before they earn a brief.
4. RENDER INTERNAL ≠ HOST PRIVATE   the cap grade, materiality band, and triage verdict in this guide are internal;
                       a client render carries posture + the sourced frame only (confidence_model.md §3, §7).
```

---

**See also**: [hail.md](hail.md) · [el_nino_enso.md](el_nino_enso.md) (the gated briefs) · `../_triage.md` (the cross-subject board this feeds) · `../README.md` (the studio architecture + the subject-README rule) · `../../docs/method/confidence_model.md` (the three axes the matrix ranks by) · the four resources linked in the matrix.
