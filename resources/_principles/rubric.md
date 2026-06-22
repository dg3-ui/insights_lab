# The Rubric — Five Criteria, One Gate

> **Status**: v0.1, 2026-06-12 (Phase 1 deliverable; decision D1/D2 of the active plan).
>
> **Purpose**: the canonical judging rubric for every InfraSure Insights output, and the bounded self-critique rules. Fixed by the 2026-06-11 collab decision (five criteria) — do not re-derive per session.
>
> **What it is NOT**: the rubric is a **scoring layer on top of** the binary pass/fail gate in `../../docs/process/test_protocol.md` — never a replacement for it. An artifact can score well and still fail the gate; the gate wins.

## §1 · The Five Criteria

Score each criterion **`pass / flag / fail`** per artifact. Definitions point into existing canon — the rubric cites the machinery, it does not restate or compete with it.

| # | Criterion | The question | Defined by |
|---|---|---|---|
| 1 | **format** | Does the artifact match its declared shape? Pre-gate: the 9-section applied-insight skeleton (Claim · Scope · Mechanism · Source References · Confidence · Caveats · Actor Relevance · Review Trace · Gaps). Post-gate: the output-contract cell it was rendered under (`resources/_style/`, Phase 2+). | the package's `prompt_projection.md` output format · `_style/output_contracts.md` |
| 2 | **relevancy** | Is it about the declared scope — named entities, IDs, fields — and does it answer the question asked? "If the answer needs no InfraSure entity, ID, or field to stand up, it is commentary." | `../../docs/method/analysis_families.md` Core Position + Q&A grammar Q1–Q3 |
| 3 | **usefulness** | Would the named actor *do* something with it — watch, monitor, re-check, ask? Decision intelligence, not description. | `../../docs/method/analysis_families.md` Q&A grammar Q6–Q7 · the package's `actor_relevance` |
| 4 | **accuracy** (with calibration — **"smartfulness"**) | Is every material claim grounded with a `source_ref` + vintage, the **calibration cap** set by the weakest input (one of three axes — event-likelihood and materiality are the others, and neither raises the cap, `../../docs/method/confidence_model.md`), blocked claims refused — **and is the altitude right**: no false precision (an exact, unmodeled number invites the question mark it cannot survive) and no generic mush (a claim so hedged it says nothing). Calibration *is* the defining clause of accuracy here, not a sixth criterion. | `../../docs/method/confidence_model.md` (the three axes) · `../../docs/method/resource_standard.md` Confidence Rules + Blocked Claim Examples · the package's `blocked_claims` · `../../docs/method/analysis_families.md` Q4–Q5 |
| 5 | **presentability** | Does it reflect well on InfraSure's image — house voice, human prose, no AI tells, on-brand when rendered? **Subordinate to substance**: `../../docs/method/resource_standard.md` — "If any item fails, the resource is not ready — however well it reads." | `voice.md` · `_style/brand.md` (Phase 2+) |

## §2 · Self-Critique — Bounded, Split, Two-Stage

The drafting model may critique its own work, inside hard bounds:

```text
WHAT IT MAY SELF-JUDGE                      WHAT IT MUST NEVER SELF-JUDGE
style criteria: format · presentability     accuracy (criterion 4) — reviewed claim-by-claim
(relevancy/usefulness as a sanity check)    against source refs by the HUMAN checkpoint
                                            (later: the independent /gate-check, ../../docs/process/commands.md).
max 1–2 critique iterations per stage       The drafter is never its own accuracy judge —
ALL critique turns saved in the transcript  that is the architecture.md §7 self-policing weakness, and
                                            it is fixed by independence, not more self-review.
```

Two stages, because `_style` loads only post-gate:

```text
STAGE 1 · pre-gate (drafting session)        STAGE 2 · post-gate (render)
checks SKELETON CONFORMANCE only:            checks the render against its declared
all 9 sections present, claims carry         output-contract cell: structure, length
refs/confidence/caveats slots                band, tone, brand, what-not-to-include
NOT prose polish — polishing an ungated      full format + presentability judgment
draft is the P2 pull we refuse (../../docs/principles.md)     happens HERE, not before the gate
```

## §3 · Where Scores Land

Rubric scores are recorded **per run** by the human at the checkpoint, in the test record (`templates/mcp_test_run.template.md` → Rubric Scores table + Self-Critique Delta), alongside — never instead of — the `../../docs/process/test_protocol.md` pass/fail decision. Recurring `flag`/`fail` rows are extraction targets: they feed `voice.md`/`_style` edits and the eval suite, same as fail→fix pairs (`../../docs/process/test_protocol.md` Session Capture).

## §4 · What The Rubric Is Not

Three evaluation instruments coexist; do not conflate them:

```text
THE RUBRIC (this file)      "is this artifact good?"            scores one output
WITH/WITHOUT VALIDATION     "is it unreachable without us?"     proves the moat (../../docs/use_cases.md §Validation)
PROMPTING BUCKET #3         "does the prompt engineering hold?" a testing lens (../../docs/use_cases.md §Reconciliation)
```

And the rubric never overrides a package's `blocked_claims`, `confidence_rules`, or `caveats` — those stay per-resource (`../../docs/method/resource_standard.md`); criterion 4 *enforces* them, it does not re-legislate them.

---

**See also**: `voice.md` (criterion 5's source), `README.md` (stage placement + versioning), `../../docs/process/test_protocol.md` (the gate this scores on top of; the flow step that applies it), `../../docs/method/resource_standard.md` (the confidence ladder + blocked-claim floor criterion 4 cites), `../../docs/method/analysis_families.md` (the Q&A grammar behind criteria 2–4).
