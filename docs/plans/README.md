# docs/plans — Phased Execution Plans

> **Status**: opened 2026-06-11 — the home for multi-phase execution plans that are too big for the README "Current Task" line.
>
> **Rule**: one **ACTIVE** plan at a time (others may be **PAUSED** — started, set down to let a more urgent plan run — or **QUEUED** — opened as a stub, not started). A plan is a *working doc*: its phase ladder is updated as phases complete, and the ACTIVE one is what the README "Current Task" routes to. When a plan is done or superseded, mark it and leave it in place as the record; do not rewrite history.

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
| [2026-06-13_docs_reorg.md](2026-06-13_docs_reorg.md) — reorganize `docs/` into purpose-folders along the P1 seam; `architecture.md` as the front door | 2026-06-13 | **ACTIVE** |
| [2026-06-11_layered_reference_v1.md](2026-06-11_layered_reference_v1.md) — restructure `resources/` into shared layers (_principles · _style · _craft · _reference) + output contracts + rubric | 2026-06-11 | **PAUSED** behind the reorg — Phases 1–4 ✅ · Phase 5 (crack bottom-up) next |

---

**See also**: `../../README.md` (Current Task points here while a plan is active), `../principles.md` (P5 — commit, then revisit), `../process/commands.md` (the command lifecycle plans operate inside).
