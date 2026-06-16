# Handoff — Output-Layer Architecture (2026-06-15)

> **Status**: COMPLETE (`origin/main` @ `7721b86`). The bridge to the next session. Read this first. (See the **Addendum** at the bottom — the baseline-first reframe + the discovery clarification landed after this handoff was first drafted.)

## 60-second summary (10 bullets)

1. Built the **scalable output-layer architecture** for `studio/` (owner: "do the right thing for the long term, not patches").
2. **Confidence is now three axes** — calibration cap (internal grade) · event likelihood (sourced, on output) · materiality (band, internal, tie-breaker). Canon: `docs/method/confidence_model.md`. On the rendered face: **posture + event + settledness; the grade never renders.**
3. **Studio folded** to `studio/<subject>/<phenomenon>.md`; each §1 gate-record is the single source of truth. Subjects: `brookfield_standard_solar/` (account) + `galveston_ship_channel_surge/` (corridor — the honest home for the unresolvable "Anten").
4. **Triage layer** — `studio/_triage.md`: one internal board, cap × materiality → ACT/WATCH/NOISE, never rendered.
5. **Two new phenomena grounded live** (MCP, 2026-06-15): `hail.md` (0 MW in the US hail maximum) + `extreme_heat.md` (NOISE — a modest derate muted by fixed-price PPAs). **Offtaker = BLOCKED** (offtakers field null; gap R13). A multi-phenomenon **subject guide** (`brookfield_standard_solar/README.md`).
6. **`direction` (top_down/bottom_up) is a meta-tag, not a folder**; subject = a scope ladder (account→region→market).
7. **Origination norm**: studio-first for the OUTPUT artifact (the insight is still gated upstream, P2); bottom_up before top_down.
8. **P6 sharpened** — references inform the *analysis*, not just form; the model is the renderer (writes its own SVG/HTML/generators); only the claim-discipline binds. The differentiator.
9. **`/render` built** (`.claude/commands/render.md`, Tier-2, P6-first) + demoed with a real **hail US statebin map** (`studio/brookfield_standard_solar/_renders/hail_us_statebin.html`).
10. **Front-door docs synced** (architecture.md, CLAUDE.md, docs/README, use_cases, +6 more) — verified no stale labels remain.

## Files the next session should read first

```text
docs/method/confidence_model.md          THE foundation — the 3 axes, posture, materiality, render-internal
studio/README.md                          the output-layer architecture (foundation→render→triage→gallery)
studio/_triage.md                          the cross-subject board + the binding-cap rule
studio/brookfield_standard_solar/README.md the subject-guide pattern (the 4-phenomenon matrix)
.claude/commands/render.md                 the /render conductor (P6-first; the model is the renderer)
docs/principles.md  P6 (+ P7)              the discipline that governs all of the above
docs/plans/2026-06-15_output_layer_architecture.md   the plan-of-record
```

## Verify current state

```bash
git -C insights_lab log --oneline -10       # af394d7 → 7721b86
git -C insights_lab status -sb              # should be clean, up to date with origin/main
open studio/brookfield_standard_solar/_renders/hail_us_statebin.html   # the demo map (browser)
# residual-drift check (should be clean in live canon):
grep -rniE 'direction ?[x×] ?audience ?[x×] ?format|blog/brief/email/post|P1[–-]P5' --include="*.md" . | grep -vE 'docs/plans/|node_modules'
```

## NEXT ACTION (start here)

The architecture is built, verified, and pushed. The open work, in priority order:

```text
PHASE A · OWNER CHECKPOINT (gates everything downstream)
  The 4 studio briefs are GATED DRAFTS "pending owner checkpoint" — the human-in-the-loop gate
  has NOT run. Owner reviews: brookfield_standard_solar/{el_nino_enso,hail,extreme_heat}.md +
  galveston_ship_channel_surge/storm_surge.md. Until then, nothing ships externally.

PHASE B · RENDER THE REMAINING HERO VISUALS (prove /render breadth)
  Only the hail map is rendered. Run /render on:
    · extreme_heat.md → the Gallup (62406) monthly-CF curve (summer HIGH, the discipline visual)
    · el_nino_enso.md → the 362 MW split into 3 ENSO-region buckets (the diversification bar)
  Same HTML/inline-SVG path (no matplotlib in sandbox); the model authors the artifact.

PHASE C · CLOSE THE OFFTAKER GAP (unblocks a phenomenon)
  Offtaker concentration is BLOCKED — get_plant.offtakers is null book-wide. Needs an owner-level
  offtake/counterparty rollup (mcp_gap R13) OR external contract disclosure. PPA *price* is partly
  recoverable (financial.ppa_price_per_mwh) but not the counterparty. Until R13, keep it blocked.

PHASE D · A FIRST TOP_DOWN MARKET PIECE (exercise the scope ladder)
  Generalize from the accumulated bottom_up reads → a market/fleet subject (e.g. studio/caiso_solar/
  el_nino_enso.md or us_solar/hail.md), tagged direction: top_down. The phenomenon links it to the
  account reads. (studio/README.md "subject-keying & direction".)

PHASE E · BUILD /gate-check (the remaining Tier-2 command)
  The independent-review conductor (architecture.md §7 self-policing weakness). Spec in
  docs/process/commands.md + status/commands.md.
```

## Critical context / gotchas (not obvious from code)

- **The grade never renders.** On any client-facing artifact: posture + event + settledness only. The cap grade, materiality band, and triage verdict are render-internal — *independent of repo visibility* (`confidence_model.md` §7).
- **Re-ground before shipping a number.** Substrate figures are dated MCP snapshots; the book already drifted 129→127 MW in one session. Re-fetch + reconcile (the freshness note in every brief/template/render).
- **The model is the renderer.** No matplotlib/geopandas in the sandbox — hand-author inline SVG or write a stdlib generator (keep it transient in `/tmp`; commit only the artifact). Maps = statebin schematic until served geometry lands (R7/R10).
- **P6 is load-bearing.** The resource layers are stepping-stones, not a checklist — guide the analysis, don't force it; the model improves on top. Only the claim-discipline binds. Don't "fill every section."
- **Triage binding-cap rule.** A composite read's headline = its *lowest* cap; a stand-alone higher-cap fact gets its own row (don't promote the headline off the strongest part).
- **Materiality is grounded + a tie-breaker** — never a $, never lifts the cap; weather resources read class-severity from `knowledge.md` sensitivity, hazard resources from `financial_materiality`.
- **Archived plan docs** (`docs/plans/done/`, `2026-06-11_layered_reference_v1.md`) carry superseded labels on purpose — don't "fix" them.

## Addendum (2026-06-15, after this handoff was first drafted — commit `7721b86`)

- **Baseline-first reframe (the important one).** Studio is the **SELECTIVE lane, not Layer 3 itself.** The **baseline** path is the default and needs no studio: a gated insight (MCP + a methodology package) renders directly via `/render` — *MCP + a package alone yields something useful*. Studio is the owner's opt-in accuracy/home-run lane; **most outputs skip it.** This corrected an over-centering from the docs-sync (architecture/CLAUDE/AGENTS/use_cases/docs-README had called Layer 3 "the studio output layer" — all reframed; verified clean).
- **`/render` renders a gated insight from EITHER path** — a `test_run` applied-insight (baseline, no studio) OR a studio brief (selective, adds the §2 hook + §3 creative). That's the tooling change that makes the baseline real. `confidence_model.md` §3 single-source decoupled (the applied-insight object on the baseline, or a brief's §1 in the lane).
- **Discovery/catalog checked (an open question this session):** the **registry is correct** — `resources/README.md` lists all 5 resources / 3 live domains (tree + Status trued up); every `resource.yml` carries the taxonomy discovery ranks on. The discovery **tool** (`find_methodology` / `get_methodology`) is **designed-not-built by intent** — the registry IS the index until ~10–20 skills (`discovery_spec.md` §1); not a gap. `discovery_spec` worked-example updated (5 skills, not 1).
- **Net for the next session:** PHASE A–E below are unchanged; just read Layer 3 as "baseline render + a selective studio lane," and remember `/render` accepts a bare gated insight (you don't need to author a studio brief to render).
