# Studio Brief — The Peril That Breaks Panels, and the Bullseye This Book Sits Outside

> **Subject**: Brookfield / Standard Solar (account) · **Phenomenon**: severe hail (`../../resources/hazard/hail_solar/`) · **Direction**: bottom_up (account-targeted)
>
> **Output type**: report · **As of**: 2026-06-15 · **Audience**: internal (Brookfield/Standard Solar account team; render path also client) · **Grounding**: MCP-grounded (InfraSure substrate, state-level) + research-grounded hail climatology (NOAA SPC)
>
> **A cloud-attachable brief**: attach this + `../../resources/_style/brand.md` + `../../resources/_principles/voice.md` (+ `_craft` if charts) → render for the target format. **Post-gate only** — this brief dresses a *validated* insight (the three guards, `../README.md`).
>
> ⚠ **GROUNDING FRESHNESS — re-ground on use.** The substrate figures below come from an InfraSure MCP pull on **2026-06-15**; the upstream platform data fetch (`renewablesinfo_org` pipeline) was **not** freshly re-run for this brief. Concretely, the book size already drifted between pulls (the ENSO brief saw 129 plants / 362.3 MW; today's solar-filtered pull returns 127 / 355.3 MW). **Before any external use — and whenever this brief is loaded as a skill in a live Claude session — re-fetch the named entities against the live MCP (`plants_by_owner` / `get_plant` / `aggregate`), confirm the platform data is current, and reconcile any drift.** Treat these numbers as a dated snapshot, not a live source of truth (`../README.md` · `../../docs/method/data_map.md` `as_of`).

## 1 · The validated insight (the gated content — grounds everything · SINGLE SOURCE OF TRUTH)

**Condition.** Severe hail (≳1–2 in / golf-ball-plus) is the single largest cause of catastrophic insurance loss to utility-scale solar: impact energy past the module's front-glass tolerance cracks cells and shatters glass, dropping array availability for weeks-to-months until panels are inspected and replaced (`../../resources/hazard/hail_solar/knowledge.md` §1). NOAA SPC climatology puts the **US hail maximum in the southern Great Plains / Texas** — a stable geography, not a dated forecast (hail is sudden-onset; a forward site probability needs a hail model and is blocked here).

**Scoped entities — the finding.** Standard Solar's book has **zero plants in the SPC hail maximum** (TX · OK · KS · NE · SD = **0 plants, 0 MW**, `plants_by_owner` as_of 2026-06-15). Its hail exposure is *secondary and geographically spread*, and splits by hail climatology as follows:

| Hail-climatology bucket | States | Plants | MW | Share of book | Note |
|---|---|---|---|---|---|
| **The US hail maximum** | TX · OK · KS · NE · SD | **0** | **0** | **0%** | the book sits entirely outside the bullseye |
| **High secondary** (CO Front Range) | CO | 8 | 20.4 | ~6% | a genuine hail max; mostly 1.5 MW community-solar gardens (largest: Wheeler Gulch 69287, 9.9 MW, Garfield Co.) |
| **Moderate convective** (Upper Midwest + High Plains) | MN · IL · NM | 66 | 146.5 | ~41% | MN 40/44.4 · IL 17/59.1 · NM 9/43.0; severe-convective hail country, below the Plains maximum |
| **Lower** | VA · MD · CA · NJ · DE · MA · ME · NY · RI · DC · PA · ID · OR · WI · VT | 53 | ~188 | ~53% | eastern seaboard / West — limited hail climatology |

The book is, again, **many small plants** (the hail-state assets are almost all 1–5 MW community-solar gardens), so even the exposed share is spread across dozens of sites in several states, not concentrated.

**Mechanism (cite, do not re-derive — `knowledge.md` §1).** Severe hail → c-Si module front-glass / cell damage → immediate output loss + latent micro-crack degradation → array availability drop until inspection/replacement. The single biggest controllable factor is **module exposure angle: single-axis trackers can "hail-stow"** (rotate to ~60° to deflect hail); fixed-tilt low-angle arrays take hail face-on. **Construction is mixed** — a 2026-06-15 spot check found Gallup (62406) is **single-axis** (can hail-stow) while Nachtigall (67747) is **fixed-tilt** (cannot); the full book is unconfirmed (see Gaps). Where sites are fixed-tilt, the hail-stow mitigation is unavailable, which *raises* the per-site vulnerability.

**Claim.** Standard Solar's book carries **no exposure to the US hail maximum**; its severe-hail exposure is directional, secondary, and spread — a high-secondary slice on the CO Front Range (~6% of MW) plus a moderate convective slice across MN/IL/NM (~41%), with the rest in low-hail geography. Because hail is the **highest-severity** physical peril for solar (a leading insurance loss, often carried under a separate sub-limit / deductible — `hail_solar` `insurance_treatment`), this exposure is **more material than the book's ENSO exposure** (`el_nino_enso.md`) even though, like ENSO, it is geographically diversified rather than concentrated. This is an exposure geography, not a loss forecast.

**Source references** (each: type · source · scope · field · as_of · role):

```text
1. external · NOAA SPC severe-hail climatology + storm reports (spc.noaa.gov) · US hail maximum = southern Great Plains / Texas; CO Front Range a secondary max; Upper Midwest moderate convective · climatology (stable) · STATE (the hazard geography)
2. substrate · InfraSure plants_by_owner("Standard Solar", fuel=solar) · 127 plants / 355.3 MW; by state CO 8/20.4, MN 40/44.4, IL 17/59.1, NM 9/43.0, TX/OK/KS/NE/SD = 0 · as_of 2026-06-15 · GROUNDS (the hail-exposure split + the zero-in-maximum finding)
3. substrate · InfraSure plants_by_owner → largest CO asset · Wheeler Gulch Solar 69287, 9.9 MW, Garfield Co.; remaining CO = 1.5 MW community-solar gardens · as_of 2026-06-15 · GROUNDS (the small-plant profile)
4. logic · hail_solar/knowledge.md §1–§4 + resource.yml · hail→c-Si damage mechanism, tracker hail-stow lever, SPC geography, no-model/no-$ caps · cited · LOGIC (mechanism + confidence ceiling)
```

**Calibration — the three axes (`../../docs/method/confidence_model.md`).** This block is the **single source of truth**; output posture and the triage ranking *derive* from it.

| Axis | Value | Basis |
|---|---|---|
| **Calibration cap** (internal) | **LOW (directional)** | forward/probabilistic exposure without a hail model and no realized-event signal on these assets → `hail_solar` confidence_rules "low". The exposure *geography* is robust, but the forward site risk and any magnitude are not modeled. |
| **Event likelihood** (on output) | **climatological frame, not a forecast** — the book's states sit in *moderate* hail climatology; **none** in the SPC maximum | SPC climatology is stable; a forward annual probability / return-period at a site is **blocked** (needs a hail model). There is no single "%" here, unlike ENSO. |
| **Materiality** (internal) | **meaningful** (higher than ENSO's *modest*) | exposed-share (CO ~6% high + MN/IL/NM ~41% moderate) × class-severity = **high** (hail is a leading solar insurance loss, `hail_solar` `financial_materiality: high`). The high severity lifts materiality above ENSO's even though the share is spread; geographic diversification still dampens concentration. |

**On output**: posture *"a forward, directional read — the dangerous peril, but this book sits outside its bullseye"* + the climatological frame (zero MW in the hail maximum; CO the one real slice). **No settledness bar** — hail is sudden-onset/climatological, not a firming forecast (`confidence_model.md` §5). The cap grade and the materiality band stay internal.

**Caveats** (`hail_solar` required caveats):

- Exposure is **geographic, not a dated forecast** — hail is sudden-onset and climatologically concentrated; this read places the book in/out of the hail geography, it does not predict a hail season.
- **No dollar figure / EAL / PML / insurance payout** — hail $ severity is `model-gpr`, blocked here. The exposure is directional only.
- **No forward annual probability or return-period** from climatology alone (needs a hail model — blocked).
- The CO + MN/IL/NM figures are **state-level** placements, not a per-site footprint hit — county/geometry-level hail-cell overlay would sharpen them (MCP gap, see Gaps).
- **Tracker vs fixed-tilt is unresolved** for these community-solar sites; the hail-stow mitigation lever may or may not exist per asset (a `get_plant` drill or developer confirmation needed). If fixed-tilt, vulnerability is higher.
- No realized hail event is asserted for any Standard Solar asset; any future `hazards`-news hit must be **verified** (the classifier has false positives) before an event-translation claim.

**Actor relevance.** *Owner/operator (Standard Solar / Brookfield):* confirm hail-stow protocols where trackers exist and module hail-rating on the CO + MN/IL sites; check the hail **deductible / sub-limit** structure (hail is often separately carried). *Investor (Brookfield Renewable):* hail is the book's more-material physical peril than ENSO, but it is spread, not concentrated — no single-cell catastrophe like a Plains-maximum owner faces. *Lender:* a hail-driven multi-week outage on a financed CO/MN site is a directional DSCR stressor; spread across small sites it is not correlated. *Developer:* for queue-stage CO/Plains-adjacent sites, tracker hail-stow + hail-rated glass are the siting/design levers.

**Review trace.** Checked vs `hail_solar` `blocked_claims`: no $/EAL/PML/payout (✓ — magnitude withheld); no forward probability/return-period (✓ — climatological frame only); no plant-level generation forecast (✓); no single-cause attribution (✓ — no realized event claimed); not national-from-regional (✓ — scoped to this owner's book). Every material number carries a substrate `source_ref` with as_of, or the SPC climatology. Cap set by the weakest input (no hail model → LOW). **Gate: PASS (draft — pending owner checkpoint + a live re-ground per the freshness note).**

## 2 · The comparison (the moat + the hook)

The home-run engine is a **structural count** a vanilla model cannot make: it requires placing every plant in a book against the SPC hail geography. The grounded line:

```text
STANDARD SOLAR — SEVERE-HAIL PLACEMENT (plants_by_owner, as_of 2026-06-15)
  US hail MAXIMUM (TX·OK·KS·NE·SD)      0 plants     0 MW       ← the bullseye: empty
  CO Front Range (high secondary)        8 plants    20.4 MW     ~6%
  MN·IL·NM (moderate convective)        66 plants   146.5 MW    ~41%
  ────────────────────────────────────────────────────────────
  A Texas-heavy utility-scale solar owner would have its MW SITTING IN the maximum.
  Standard Solar has none there — its hail exposure is real but spread, and CO is the one slice to watch.
```

A vanilla model can say "hail damages solar." It cannot, in one pass, count a named owner's 127 plants across the SPC hail geography and report **zero in the maximum, ~6% on the CO Front Range, the rest spread**. That placement *is* the moat: the read is reassuring precisely because it is grounded in where the panels actually are. The honest framing is **concentration vs spread** (the book sits outside the bullseye), not "you vs peers over 12 months" — the count is the hook.

## 3 · Creative & Activation (the cherry — bounded by the guards)

```text
HERO VISUAL    A US map with the SPC severe-hail climatology shaded (the Plains/TX maximum hot, CO Front Range
               warm) and Standard Solar's plants pinned: visibly NONE in the red maximum, a cluster on the CO
               Front Range, scatter across MN/IL. One caption: "0 MW in the US hail maximum; ~6% on the CO Front
               Range · source: InfraSure plants_by_owner + NOAA SPC climatology · as_of 2026-06-15." The visual
               SAYS only what §1 gated: placement, not loss. (_craft: every pin a source_ref; no modeled-damage layer.)
PUNCHLINE/HOOK "The peril that actually breaks solar panels. This book sits outside its bullseye."
               (Catchy on the FRAMING — the zero-in-the-maximum placement is the story. No number inflated;
               the honest number is "0 MW in the hail maximum, ~6% on the CO Front Range." Guard 2 held.)
COMPARISON     "A Texas-heavy owner's megawatts sit in the hail maximum. Standard Solar's sit in Minnesota,
               Illinois, Maryland, Colorado. Same diversification that shrugs off El Nino keeps it off the
               hail bullseye too." Grounded in the state placement (§2, §1).
CONFIDENCE     On the rendered face: posture "a forward, directional read" + the climatological frame (zero in
               the maximum; CO the one slice). No "CONFIDENCE: LOW" badge; no settledness bar (sudden-onset, not
               a firming forecast); the cap grade + materiality band are internal (confidence_model.md §3, §5).
FORWARD DOOR   "This is the exposure geography. The per-asset hail-risk modeling — site footprint, module
               fragility, hail-stow status, loss and recovery — is where InfraSure goes deeper; the team takes
               the CO/MN slice there." (P7: scope as a door to a real capability, never "we run no hail model.")
CHANNEL NOTES  report subject-line: "Standard Solar and severe hail — zero MW in the maximum, the CO Front Range the one slice to watch."
               blog title (if generalized, scrub the account): "Where the panels are is the whole hail story."
               email one-liner (post-gate, human-reviewed, named account only): "Hail is solar's costliest peril;
                 the book has 0 MW in its maximum and ~6% on the CO Front Range. Confirm hail-stow / deductibles there."
               Send stays human-in-the-loop (post-gate, `../../docs/use_cases.md` activation boundary).
```

## 4 · Render notes

```text
COMPOSE     brand.md Part A (Inter type, amber=solar accent, lifted boxes, header+footer bones) → rendered for
            the target via Part B (HTML default; DOCX on request) · voice.md (claim-first, no m-dashes) ·
            _craft (the hail-climatology map + the placement bars, each series a source_ref + as_of) ·
            output_contracts.md §3 (report envelope: a blog scoped to one portfolio; lead with the placement).
GATE        renders ONLY the §1 validated insight; every number traces to a §1 source_ref (P2). Confidence
            display (confidence_model.md §3): posture + the climatological frame; no "LOW" badge, no fill-bar.
            The forward door replaces any scope-confession. RE-GROUND before external use (the freshness note).
GUARDS      gate-upstream · creative≠overclaim · grounded-hook (../README.md §guards). All three held — see §1 review trace.
```

## 5 · Gaps / next

```text
· RENDERED (2026-06-15, /render) — the hero map is realized at _renders/hail_us_statebin.html (statebin schematic,
  hand-authored inline SVG; matplotlib wasn't available in that render env, so HTML/SVG was the path — availability varies, _craft §6). Open in a
  browser to view; re-render on live re-ground. Proves the _craft §6 map fallback end-to-end.
· FRESHNESS — figures are a 2026-06-15 MCP snapshot; the platform fetch was not re-run. Re-ground on use (header note).
· MCP GAP — no county/geometry-seeded hail-cell overlay: placement is STATE-level; a "plants within an SPC hail
  footprint / county" query would sharpen CO + MN/IL to the actual hail cells. (Pairs with the geometry-aware
  aggregate gap, mcp_gaps R14.) Log if not already covered.
· DATA DRILL — construction is mixed (2026-06-15 spot check: Gallup 62406 single-axis, Nachtigall 67747 fixed-tilt);
  a fuller get_plant pass on the CO + larger MN/IL assets would map hail-stow availability across the exposed slice.
  Materially changes per-site vulnerability (fixed-tilt cannot hail-stow).
· MATURITY — hail $ LOSS / EAL is model-gpr (grounding_maturity: substrate-only). The directional exposure ships now;
  the quantified layer is the forward door (mcp_gaps R12 — a served hazard peril model upgrades directional → quantitative).
· FORM — if this lands, it is the first HAZARD-on-a-known-book brief (complements the ENSO weather read on the same
  subject); promote toward ../../resources/_reference/internal/report/ as the DG-book hazard-exposure exemplar.
```
