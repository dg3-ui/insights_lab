---
description: Run the manual MCP/Claude test loop on an existing methodology resource — the standalone version of /new-resource Phase 5
argument-hint: <slug> [optional narrow question, e.g. "CAISO solar >=50MW this winter"]
---

You are running a **manual MCP test** on an existing InfraSure Insight resource: **$ARGUMENTS**

This is the lab's heartbeat — the discover→ground→assemble→GATE loop, exercised on its own (not as part of authoring). It is a **loop, not a one-shot** (`../../docs/process/test_protocol.md`, `../../docs/principles.md` P4). It conducts `../../docs/process/test_protocol.md`; follow it, do not duplicate it.

## STEP 0 — RESOLVE THE TARGET

- Parse `$ARGUMENTS`: first token = resource **slug**; the rest (if any) = the narrow test question.
- Open `resources/<domain>/<slug>/` and load: `prompt_projection.md`, `knowledge.md`, `data_requirements.md`. If the slug is unknown, list the `resources/README.md` registry and ask which one.
- If no question was given, propose one in the `../../docs/process/test_protocol.md` shape: **one region · one asset class**. Never a national/all-asset scan.

## STEP 1 — PRE-TEST CHECKLIST (`../../docs/process/test_protocol.md`)

- `prompt_projection.md` is concise and pasteable · `data_requirements.md` names the inputs · the question is narrow. If a piece is missing, fix the resource first (or fall back to `/new-resource`).

## STEP 2 — RUN (retrieve before drafting)

- Load the projection. Make the model **identify required data BEFORE drafting**.
- Pull the **external state live** (NOAA-equivalent for this driver) with a date; call the **InfraSure MCP tools live** for the scope. Cite real ids + `_meta.as_of` — no invented numbers.
- Draft the applied insight against the projection's output format.

## STEP 3 — ITERATE (the loop is the product)

- Enrich, re-scope, challenge. A one-shot draft is a draft. The human checkpoint in this loop *is* the product, not overhead (`../../docs/principles.md` P4).

## STEP 4 — SAVE THE RAW TRANSCRIPT

- Save the **full transcript** (every turn, tool calls, dead ends) as raw source to `resources/<domain>/<slug>/test_runs/transcripts/<run>.md` (`../../docs/principles.md` P3). This is the source `/extract` later resolves.

---

**STOP — human checkpoint.** A human reviews the draft + transcript before it is recorded as a pass. Do not self-certify and move on.

---

## STEP 5 — RECORD (resolve into the test run)

- Scaffold the next `test_runs/test_run_NNN.md` from `templates/mcp_test_run.template.md`. Record: loaded files (incl. composed shared-layer versions) · tools/data used · accepted claims · rejected/downgraded claims · failures by the `../../docs/process/test_protocol.md` taxonomy · rubric scores + self-critique delta (`resources/_principles/rubric.md`) · next fixes · link to the raw transcript.
- (For the deep extraction — prompting moves, enrichment deltas, fail→fix pairs — run **`/extract`** on the saved transcript.)

## STEP 6 — CLOSE THE LOOPS

- Any empty result / unwired filter / missing field ⇒ a tool gap: log it to `../../docs/status/mcp_gaps.md` (`gap · workaround · roadmap`), use the workaround, keep moving.
- Log learning under `docs/learning/logs/`.

## Guardrails (`../../docs/principles.md` + `CLAUDE.md` don'ts)

- **Ground or downgrade.** Review every claim against `blocked_claims` + the gate: source ref + `as_of` present? confidence capped at the weakest input? caveats attached? **no `$/MWh`/LMP from a driver alone, no plant-level forecast without a model, no causal-where-directional.**
- One region / one asset class. No **un-gated** rendering here — a contract rendering of a *gated* insight is `/render`'s job, after the gate (`../../docs/process/test_protocol.md` Avoid list, `../../docs/principles.md` P2). Don't trust tool labels — verify the entity is the one you wanted.

**Deliverable**: a saved transcript + a filled `test_run_NNN.md`, with gaps logged and learning recorded. To turn the transcript into reusable process data, run `/extract`.
