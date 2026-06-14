# docs/plans — Phased Execution Plans

> **Status**: opened 2026-06-11 — the home for multi-phase execution plans that are too big for the README "Current Task" line.
>
> **Rule**: one **ACTIVE** plan at a time (others may be **PAUSED** — started, set down to let a more urgent plan run — or **QUEUED** — opened as a stub, not started). A plan is a *working doc*: its phase ladder is updated as phases complete, and the ACTIVE one is what the README "Current Task" routes to. When a plan is **done** or **superseded**, mark its final status and **move the file into [`done/`](done/)** — a relocation, not a rewrite; the file is preserved verbatim as the record and the index keeps a pointer. So the top-level `plans/` only ever shows **live** work (ACTIVE · QUEUED · PAUSED); `done/` is the archive.

## How A Plan Works Here

```text
plan = decisions (settled up front) + phase ladder (executed ONE AT A TIME)
   each phase: goal · deliverables · canon amendments · acceptance · status
   a phase is DONE when its acceptance line is met and its canon edits landed
   no later-phase DELIVERABLE lands before the active phase closes (08 P5:
   decide and version it — flexibility is not non-commitment)
   two sanctioned exceptions, declared IN the plan, never improvised:
     · raw-material gathering (human iterations, exemplar collection) may run
       in parallel — only deliverables wait for their phase
     · a hard external deadline may pull DRAFT-marked artifacts forward; the
       DRAFT mark comes off only at the owning phase's closure
```

Plans follow house doc style (`Status` blockquote · ASCII + tight tables · `See also` footer). There is no plan template in `templates/` — deliberately; a plan is reasoning, not a fill-in form.

**Where plans come from**: a plan is born when work is structural — including an accepted feedback item too big to patch inline (`../process/test_protocol.md` §Feedback Intake, step 5: new layer, new contract cell, new decision, re-sequencing → a plan here, never an ad-hoc edit). Small accepted feedback routes directly to its home with an intake record in `docs/learning/logs/`.

## Index

| Plan | Opened | Status |
|---|---|---|
| [2026-06-14_studio_and_bottom_up.md](2026-06-14_studio_and_bottom_up.md) — the **output half**: stand up `studio/` + the creative & activation layer (with the moat guards) + the first bottom-up home-run examples (Anten · Brookfield) | 2026-06-14 | **ACTIVE** — Phases 1–2 ✅ (studio + 2 home-run briefs, for review) · Phase 3 deferred (trigger met) |
| [2026-06-14_outlier_showcase_red_dog.md](2026-06-14_outlier_showcase_red_dog.md) — the off-substrate / reverse-engineering lane: the Red Dog bottom-up report (worked proof) + the reusable outlier method | 2026-06-14 | **DONE** (Phases 1–2 ✅, 2026-06-14) — report drafted (owner review pending) + outlier playbook; archives to `done/` at supersession |
| [2026-06-13_knowledge_base_expansion_v1.md](2026-06-13_knowledge_base_expansion_v1.md) — the authored-intelligence scaffold (recipe layer + `_method`) + the first hazard-led resource wave (hail×solar · heat×solar · hurricane/wind×wind · offtaker) | 2026-06-13 | **DONE** (Phases 0–4 ✅, 2026-06-14) — scaffold + 5 resources + 1 proven recipe; archives to `done/` at supersession |
| [2026-06-11_layered_reference_v1.md](2026-06-11_layered_reference_v1.md) — restructure `resources/` into shared layers (_principles · _style · _craft · _reference) + output contracts + rubric | 2026-06-11 | **PAUSED** — Phases 1–4 ✅ · Phase 5 (bottom-up) **superseded by** `2026-06-14_studio_and_bottom_up.md` |

Completed plans are archived in [`done/`](done/).

---

**See also**: `../../README.md` (Current Task points here while a plan is active), `../principles.md` (P5 — commit, then revisit), `../process/commands.md` (the command lifecycle plans operate inside).
