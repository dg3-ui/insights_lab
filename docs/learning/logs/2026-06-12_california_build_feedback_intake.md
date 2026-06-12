# Feedback Intake — California-solar build review (2026-06-12)

> **Status**: intake record (`docs/05` §Feedback Intake) — the **first** run of the procedure, retroactive.
>
> **Source**: owner test of the layered reference in a separate session (the `InfraSure_ENSO_California_Solar` build) + the owner's review feedback. Captured: that session's own log, `2026-06-12_enso_render_build.md` (the fail→fix table), and the owner's pasted summary.
>
> **Mode**: **pre-applied diff** — the source session edited the repo directly (voice §5 · contract §3 · brand §4 · craft §6 · R8–R11 · its log). This record is retroactive, plus the mandatory drift cross-check.

## Triage

| # | Suggestion (condensed) | Verdict | Reason | Routed to | Status |
|---|---|---|---|---|---|
| 1 | Show, don't flaunt — no moat/meta-pitch language in copy; deep-link instead | **accept** | client register; the moat argument is the deck's job | `_principles/voice.md` §5 · `_style/output_contracts.md` §3 | ✅ applied by source session, verified consistent |
| 2 | Public confidence as posture, not a pejorative LOW badge; explicit label stays internal | **accept** | calibration honored by *not writing* blocked claims + the honest caveat; the badge undercuts the work | contract §3 · brand §4 | ✅ applied, verified |
| 3 | Honest-caveat box (what's resolving), not a negation list, public-side | **accept** | a "we are not saying X" list reads as a disclaimer, not analysis | contract §3 move 7 · brand §4 | ✅ applied, verified |
| 4 | Top-down pieces: fleet/region figures, not a single-plant chart as the fleet read | **accept, with a reality clause** | correct — but R2/R8 block fleet CF/county series today; rule needs the exemplar-inset escape valve or it bans the only renderable mechanism figure | contract §3 move 6 (source session) + `_craft` §4 scope rule (this intake) | ✅ |
| 5 | Reader-facing kicker, never internal taxonomy ("TOP-DOWN EXPOSURE BRIEF") | **accept** | artifacts are reader-facing; bucket names are ours | contract §3 not-include | ✅ applied, verified |
| 6 | DOCX: guaranteed sans fallback · real running header/footer · rasterized logo | **accept** | the Inter→serif substitution trap is real; D3 said DOCX derives from the brand kit — now it says how | brand §4 DOCX note | ✅ applied, verified |
| 7 | Statebin tile-grid as the no-geo-libs map fallback | **accept** | honest schematic + "bar if rank is the message" guard included | `_craft` §6 | ✅ applied, verified |
| 8 | Four tool gaps: county rollup · owner canonicalization · served geometry · climate news lane | **accept** | all four are real floor-not-ceiling entries in correct form | docs/09 R8–R11 | ✅ applied, verified |
| 9 | Meta-lesson: ad-hoc builds (reference not loaded, no gate stop) produce slop | **already-covered** | this *is* docs/05 + 08 P4; value is the recorded evidence | the build log (kept) | ✅ |

Rejected: none in this batch (the owner pre-filtered well). The verdict column exists for the day that isn't true.

## Drift Cross-Check (what the pre-applied diff left behind)

| Drift found | Fix | Status |
|---|---|---|
| `artifact_skeleton.html` still hard-coded `CONFIDENCE: LOW` badge, "What we are not claiming" label, and the footer disclaimer the new rules ban public-side | slots parameterized public/internal (calibration cue · caveat label · calibrated descriptor) | ✅ |
| `_style/examples/*_001.html` (the Phase-2 acceptance renders) now violate three current conventions — future sessions could imitate them | `examples/README.md` grandfather note: records, not models; before/after pair completes at Phase 6b | ✅ |
| Contract's "never a single-plant chart" vs `_craft` §1's seasonal-CF row and the R2/R8 reality | `_craft` §4 chart-scope rule: top-down leads fleet/region; single-plant only as a **labeled exemplar inset** until R2/R8 ship | ✅ |
| No version bumps despite material layer changes (D9) | `_principles`/`_style`/`_craft` → v0.2; Shared Layers table updated | ✅ |

## Escalations

None — no new layer, cell, or §1-decision change; everything routed inline. (Had "public confidence display" required a new *audience* axis value or cell, it would have become a ladder amendment.)

## Version Bumps (D9)

| Layer | From → to | Why |
|---|---|---|
| `_principles` | v0.1 → v0.2 | voice §5 |
| `_style` | v0.1 → v0.2 | contract §3 (confidence display · caveat · not-include) · brand §4 (DOCX) · skeleton slots |
| `_craft` | v0.1 → v0.2 | §6 spatial fallback · §4 scope rule |

---

**See also**: `2026-06-12_enso_render_build.md` (the source session's fail→fix log this record wraps), `../../05_mcp_test_protocol.md` §Feedback Intake (the procedure, born from this batch), `../../../templates/feedback_intake.template.md`.
