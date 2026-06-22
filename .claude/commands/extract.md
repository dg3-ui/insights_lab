---
description: Resolve a saved test transcript into the reusable record — test_run extraction, learning log, and MCP ledger entries. The "resolve" half of "save the chat".
argument-hint: <path to saved transcript> [slug, if not inferable]
---

You are **resolving a raw test transcript into reusable process data**: **$ARGUMENTS**

A saved transcript is **raw source**; the value is the **extraction** (`../../docs/principles.md` P3, `../../docs/process/test_protocol.md` "Session Capture & Extraction"). A pile of un-extracted transcripts is a swamp, not an asset. This command turns one transcript into the things that sharpen the next resource. It conducts `../../docs/process/test_protocol.md`; follow it, do not duplicate it.

## STEP 0 — LOAD

- Read the transcript at the given path. Identify the resource it belongs to (`resources/<domain>/<slug>/`); if not inferable, ask.
- Read the resource's `prompt_projection.md` + `blocked_claims` so you can judge what happened against the contract.

## STEP 1 — EXTRACT (only what is actually in the transcript — do not invent)

```text
PROMPTING MOVES    what the human said/did that ENRICHED the output (the redirections that worked)
ENRICHMENT DELTAS  one-shot draft → final: what changed, and WHY it got better
FAIL→FIX PAIRS     each overclaim/miss caught → the rule (blocked_claim / projection line) that should catch it next time
TOOL GAPS          empty results / unwired filters / missing fields hit during the run
```

## STEP 2 — WRITE THE RESOLVED RECORD

- Create/update `resources/<domain>/<slug>/test_runs/test_run_NNN.md` (from `templates/mcp_test_run.template.md`): accepted / rejected / downgraded claims, failures by the `../../docs/process/test_protocol.md` taxonomy, **a link to the raw transcript**, and the **extracted yield** (the four buckets above).

## STEP 3 — FEED THE LOOPS

- **Tool gaps →** append each to `../../docs/status/mcp_gaps.md` in `gap · workaround · roadmap` form (note a repeat rather than duplicating).
- **Fail→fix pairs →** each is (a) a candidate `prompt_projection.md` / `blocked_claims` edit, and (b) a candidate **eval case** for the future eval harness. Note them as such.
- **Learning →** log unclear/confusing/missing-context notes under `docs/learning/logs/`.

## Guardrails (`../../docs/principles.md`)

- **Model-agnostic by design** (P1): the outputs are prompts, evals, and process — never model-training data.
- **Resolve, don't restate**: extract the signal; do not transcribe the whole chat into the record.
- **Faithful**: every extracted item must trace to a real moment in the transcript. If unsure, mark it `?` rather than inventing.

**Deliverable**: a resolved `test_run_NNN.md` (linked to its raw transcript) + ledger/learning entries + a short list of proposed projection edits and eval cases. This is the process data that makes the next `/new-resource` and `/test-resource` sharper.
