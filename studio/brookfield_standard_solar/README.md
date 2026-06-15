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
| **Extreme-heat derate** | [`extreme_heat_derate`](../../resources/weather_and_climate/extreme_heat_derate/) | SW belt + summer peak; PV temperature-coefficient derate | *queued* | *queued* | — | scaffold ↓ |
| **Offtaker concentration** | [`offtaker_concentration`](../../resources/commercial/offtaker_concentration/) | community-solar subscriber base + any merchant tail | *queued* | *queued* | — | scaffold ↓ |

**Reading the matrix.** **Hail outranks ENSO** for this book — not because more MW are exposed (both are diversified, low-cap, directional) but because hail's **class-severity is high** (it physically breaks panels; it is solar's costliest insurance peril) while ENSO is a mild seasonal CF nudge. That is the materiality axis doing its only job: ordering two low-cap reads. Neither is an ACT — the spread keeps both at WATCH (`../../docs/method/confidence_model.md` §4).

## Scaffolded phenomena (rationale only — NOT yet grounded, do not assert)

These belong on the book but have **not** been run through the test loop. The rationale is groundable from the book profile; **the numbers are not written until each is grounded + gated** (P2 — studio is post-gate; this section is a queue, not a claim).

```text
EXTREME-HEAT DERATE (extreme_heat_derate)
  WHY it matters   PV output derates with cell temperature (negative temp-coefficient); the SW belt + summer
                   peak is where it bites. RELATED to ENSO (both act on solar CF) but opposite season — heat is
                   a summer-peak derate, ENSO a winter-irradiance shift. A fuller seasonal read pairs the two.
  TO GROUND        plants_by_owner state split (already have) → SW-belt + high-summer-irradiance subset →
                   get_plant monthly CF to see the summer derate signature → cap LOW (no production model),
                   materiality likely MODEST (derate is real but well-understood and modest vs hail).
  EXPECTED POSTURE reassuring-to-neutral: a known, modest, well-characterized loss — not a catastrophe peril.

OFFTAKER CONCENTRATION (offtaker_concentration)
  WHY it matters   the commercial overlay: who buys the output. A community-solar book is MANY small subscriber
                   contracts → concentration is likely LOW by design (the opposite of a merchant-exposed book).
  TO GROUND        the substrate offtakers field was NULL on the assets checked (ENSO brief Gaps) → this needs an
                   owner-level offtake/contract rollup (mcp_gap candidate) OR external contract disclosure.
                   Until then offtaker concentration is UNRESOLVED, not "low" — record the gap, do not assert.
  EXPECTED POSTURE likely reassuring (diversified subscriber base), but BLOCKED until the offtake data resolves.
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
