# Decisions — Output-Layer Architecture (2026-06-15)

> **Status**: the design decisions made this session, with rationale. Canonical homes in parentheses.

## 1. Confidence is three orthogonal axes, not one number

**Decision.** Split confidence into **calibration cap** (how hard we may assert THIS claim — internal grade, set by the weakest input, *nothing raises it*) · **event likelihood** (the world's sourced probability, e.g. NOAA 63% — on output) · **materiality** (the stake — exposed-share × class-severity band — internal). (`docs/method/confidence_model.md`)

**Rationale.** "Confidence: LOW" collapsed three different facts and read as *low quality*. The truth is sharper: a *likely* event (not low) can carry a *directional* claim (low cap) about a *small or large* stake. Separating them lets us be honest on the rendered face (posture + the real event number) while keeping the grade internal.

## 2. render-internal ≠ host-private (two orthogonal axes)

**Decision.** The cap grade, the materiality band, and the triage verdict are **render-internal** — never on a rendered artifact — *independent of* whether the repo is host-private. (`confidence_model.md` §7)

**Rationale.** A private repo is an infra setting; what a client-facing artifact says is a content discipline. A brief is designed to be handed to a client, so the grade stays off the face regardless of where the file lives. Conflating the two would let "the repo is private" excuse a leaked grade.

## 3. Materiality is a tie-breaker, never an override; grounded by resource type

**Decision.** Materiality orders *which* low-cap reads to surface first; it **never** lifts the cap or unblocks a blocked claim. Basis = exposed-share (substrate count) × class-severity band, read from the resource's own canon — **never a $**: hazard resources use the `financial_materiality` field; weather/climate resources use the documented (driver × asset-class) sensitivity in `knowledge.md`; if undefined, materiality is `unknown` (a logged gap, not an asserted band). (`confidence_model.md` §4; fixed during verification — see notes)

**Rationale.** A huge stake under a directional read is still a directional read. And the original basis cited a `financial_materiality` field that only *hazard* resources have — ungrounded for ENSO (the anchor resource); extending it to weather resources closed the grounding gap the model claims to close.

## 4. Studio is keyed by SUBJECT on a scope ladder; direction is a meta-tag, NOT a folder

**Decision.** `studio/<subject>/<phenomenon>.md`, where subject is a **scope ladder** (account → region/corridor → market/fleet). `direction` (top_down/bottom_up) is a **meta-tag** in the header + a triage column, never a top-level folder split. (`studio/README.md`; owner-chosen via AskUserQuestion)

**Rationale.** A `top_down/ bottom_up/` folder split would add a second axis, bury subject folders, and — worst — sever the link that *the same phenomenon at two scopes is one insight* (a market blog + an account report). The phenomenon is that link. Consistent with `output_contracts.md` §1 ("direction is a descriptor, not a format"). An unresolvable entity ("Anten") becomes a region/corridor subject, honestly.

## 5. Single source of truth: the brief's §1 gate-record

**Decision.** The three axes live **once**, in the phenomenon file's §1. The rendered posture and the triage board both *derive* from it. (`confidence_model.md` §3)

**Rationale.** A grade with one home doesn't drift; a grade in two places does. The triage board links each §1 and re-states no grade.

## 6. Triage headline = the binding (lowest) cap; a stand-alone higher-cap part earns its own row

**Decision.** A composite read's headline verdict is set by its *lowest* cap (not promoted by its strongest part). A higher-cap part that stands alone (a hard fact, like the Galveston co-location count) gets its **own co-equal row**. (`confidence_model.md` §6; `studio/_triage.md`)

**Rationale.** Found during verification: the board led Galveston with ACT off its *highest* cap, contradicting the binding-cap rule. The fix keeps the rule honest while still surfacing a firm fact (the co-location is ACT/WATCH; the forward season is WATCH-high).

## 7. studio-first origination (for the OUTPUT), bottom_up before top_down

**Decision.** A studio brief is the **first output artifact** — created and iterated in studio before any render, gallery promotion, or publication. But the *insight* is still gated upstream (P2) — "origination" means the artifact, not the claim. Account/region (bottom_up) reads come first; a top_down market blog generalizes *from* accumulated bottom_up reads. (`studio/README.md`)

**Rationale.** Reconciles the owner's "studio-first" instinct with guard 1 (studio never originates an insight). The bottom_up-first order matches the build-order discipline (the rich, grounded reads create the feedback loop a generic blog distills from).

## 8. P6 governs the ANALYSIS, not just the form — and the model is the renderer

**Decision.** Sharpen P6: the resource layers (incl. studio briefs/template/guide + `_style`) are **stepping-stones, not a checklist**; the model may restructure, pick a different analytical angle, surface the latest info, and improve on top. The only hard floor is the claim-discipline. Applied to rendering: **the model generates the artifact itself** (hand-authored SVG/HTML, or a small stdlib generator) — a missing library is never a blocker. (`docs/principles.md` P6; `studio/README.md`; `.claude/commands/render.md`)

**Rationale.** The owner's core, repeated point: don't curtail the model's capability with rigid templates — guide, don't force; over-constraining misses what only the model can see. This openness (building *on top of* model capability) is framed as the differentiator, not a concession.

## 9. /render is a P6-first thin conductor; HTML/inline-SVG is the primary render path

**Decision.** `/render` (Tier-2, now built) renders a gated brief → deliverable + grounded charts/maps, opening with the stepping-stone frame. The **primary** draw path is HTML + hand-authored inline SVG (the matplotlib-PNG path is a fallback). (`.claude/commands/render.md`; `_craft` §5/§6)

**Rationale.** The thin-conductor rule ("point, don't restate"). And the sandbox has no matplotlib/geopandas/kaleido (verified) — so HTML/SVG is the reliable path; maps use the statebin tile-grid schematic until served geometry lands (R7/R10).

## 10. "Re-ground on use" freshness discipline

**Decision.** Substrate numbers in any studio/render artifact are **dated MCP snapshots**; re-fetch against the live MCP and reconcile drift before any number ships externally. Baked into the template, briefs, guide, and `/render`. (owner-raised; `studio/README.md`)

**Rationale.** The book size already drifted between two pulls (129/362.3 MW → 127/355.3 MW). Numbers are perishable; the methodology is stable. Made explicit at the point of use because a brief loaded later as a skill must re-ground first.

## 11. Establish `docs/extra/tasks_history/` (this record)

**Decision.** Adopt the `.cursor/commands/PROMPT_CREATE_TASK_DOCS.md` 4-file format for session handoff records, in `docs/extra/`, complementary to `test_runs/` (validation) and `learning/logs/` (distilled learnings).

**Rationale.** A model-switch / context-window bridge for a large multi-part session — the handoff is the value.
