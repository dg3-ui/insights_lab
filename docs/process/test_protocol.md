# MCP Test Protocol

> **Status**: v0 protocol, deepened 2026-06-05.
>
> **Purpose**: define how to test a methodology resource manually with Claude and existing InfraSure MCP/data tools.
>
> **Companion**: `docs/learning/01_mcp_basics.md` (the tool surface), `04_prompt_projection.md` (the surface under test), and `resources/_principles/rubric.md` (the scoring layer the checkpoint applies).

## Test Goal

The test asks:

```text
When Claude has both:
  1. InfraSure MCP/data tools
  2. a methodology resource prompt projection

can it produce:
  a useful, grounded applied-insight draft?
```

This is not a production agent test. It is a resource-shape test.

## Pre-Test Checklist

Before running a test, confirm:

- `resource.md` explains the method
- `resource.yml` has structured fields
- `data_requirements.md` names required inputs
- `prompt_projection.md` is concise and pasteable
- `examples/applied_insight_001.md` shows the target output shape
- `resources/_principles/` (rubric + voice) is loaded alongside the projection — the only shared layer loaded before the gate (`_style`/`_craft`/`_reference` are post-gate, render-side)
- the output type is **declared** — `blog` / `report` / `email` (`resources/_style/output_contracts.md` §1), optionally tagged with the descriptive meta-tags `direction` (top_down/bottom_up) and `audience` (*naming* it at test start, not loading `_style`)
- the test question is scoped to one region, asset set, company, or offtaker

## Manual Test Flow

```text
1.  Open Claude with InfraSure MCP/data tools available.
2.  Load or paste prompt_projection.md (+ resources/_principles/ — rubric and voice).
3.  Provide the test question.
4.  Ask Claude to identify required data/tools before drafting.
5.  Let Claude retrieve data using available tools.
6.  Ask Claude to draft the applied insight.
7.  Review each claim against source refs and methodology rules.
8.  ITERATE — enrich, re-scope, or challenge; a one-shot draft is rarely the product (see below).
9.  SELF-CRITIQUE, stage 1 (≤2 passes, style only): the model checks the draft against the
    9-section skeleton — structure conformance, not prose polish. Accuracy is NEVER self-judged
    (resources/_principles/rubric.md §2); the human at step 7 stays the accuracy judge.
10. SCORE THE RUBRIC — the human records pass/flag/fail on the 5 criteria (rubric.md §1).
    Render-stage criteria (format-vs-contract, presentability) are fully scored only post-gate.
11. Save the FULL transcript (raw source, INCLUDING the critique turns), not just the final output.
12. Record the resolved result in test_runs/test_run_NNN.md.
13. Record learning in docs/learning/logs/.
```

**Iteration is expected, not a failure** (`../principles.md` P4). The first draft is a draft. The enrichment that makes an insight useful happens in the loop, and the human checkpoint in that loop is the product, not overhead. Do not treat "it needed three turns" as a defect — treat the turns as the most valuable thing the test produced.

## A Real First-Call Trace (2026-06-05)

What a *good* first move looks like vs. a failing one, against the live tools:

```text
GOOD                                                  WHY
search_plants(fuel="solar", state="CA", minMw=50) ->  resolves the real fleet (Topaz 57695, Desert Sunlight 57993…)
cite _meta.as_of = "2026-06-05"                   ->  vintage attached to every grounded claim
get_plant(57993) for CF + owner + offtaker        ->  drills for grounding (CF 0.24, PG&E, Clearway)
"ENSO state pending NOAA CPC (external)"          ->  names the external dependency, does not invent it

BAD                                                   DIAGNOSIS (failure type below)
search_plants(iso="CAISO") -> [] then gives up    ->  MCP/tool gap not worked around (use state=CA)
"California has ~37 GW of solar…" with no IDs      ->  skipped retrieval -> prompt gap
"Expect ~5% winter generation loss"               ->  overclaim -> blocked-claims rule too weak
```

## Required Test Question Shape

Use a narrow question:

```text
Using the El Niño / ENSO exposure methodology, identify a directional
exposure insight for [one region/market] [one asset class or portfolio].
Include source refs, confidence, caveats, and actor relevance.
```

Good first test:

```text
Using the ENSO exposure methodology, draft a directional exposure insight
for CAISO solar assets >= 50 MW. Focus on affected assets/owners, mechanism,
confidence, caveats, and who should monitor it.
```

Avoid:

- national all-asset scans
- exact LMP forecasts
- **un-gated rendering** — email/blog/post copy before the insight passes the gate (a declared
  contract rendering of a *gated* insight is `/render`'s job, not banned — `../principles.md` P2)
- unbounded "write an article" prompts (an article is a post-gate rendering, never the test ask)

## Pass / Fail Criteria

Pass means:

- the model identifies required inputs before drafting
- the output has a scoped claim
- source refs are present (with `as_of`)
- confidence is declared
- caveats are attached to uncertain claims
- actor relevance is present
- the output does not exceed allowed claims

Fail means:

- the output is generic commentary
- claims are unsupported
- the model skips data retrieval
- confidence is absent or inflated
- caveats are missing
- the output jumps directly to outreach copy
- the resource does not constrain the model's reasoning

**The rubric sits on top, never instead.** This binary pass/fail is the gate. The 5-criteria rubric (`resources/_principles/rubric.md` — format · relevancy · usefulness · accuracy-with-calibration · presentability, scored pass/flag/fail) is a per-run scoring layer recorded in the test record; a good rubric score never overrides a gate fail.

## Failure Taxonomy

Log every failure as one of the following. The right-hand column is a real or concrete example to calibrate against:

| Failure Type | Meaning | Concrete example |
|---|---|---|
| Methodology gap | The resource did not explain how to reason or what to block | model gave a causal ENSO→price claim the method should have blocked |
| MCP/tool gap | The needed data was not available through current tools | `search_plants(iso="CAISO")` returns `[]` (data exists per-plant; filter unwired) |
| External-data gap | NOAA or another external source was missing, stale, or unresolved | no dated ENSO/ONI value pulled for the test winter |
| Context gap | Actor, offtaker, company, or descriptive context was missing | queue rows return `developer: null` (DARDEN, UMBRIEL…) — no actor to route to |
| Prompt gap | The prompt projection was too broad, vague, or verbose | model wrote prose with no `plant_id`s — projection didn't force retrieval |
| Review gap | The output could not be judged because refs/confidence/caveats were unclear | a claim with no `source_ref` or `as_of` to check against |
| Style/contract gap | The output ignored its declared shape or the voice rules | draft missing skeleton sections; rendered output off-contract (wrong structure/length/tone); AI-tell prose (`resources/_principles/voice.md`) |
| Craft/plot gap | A chart violated the grounded-plot rules | a plotted series with no `source_ref`/`as_of`; a chart of a blocked quantity (forecast $/MWh) |

**MCP/tool gaps are roadmap inputs, not dead ends** (see `docs/learning/01_mcp_basics.md`). Log them in three parts so they feed the expandable tool surface:

```text
gap:        search_plants(iso="CAISO") returns [] — ISO filter not wired
workaround: used state="CA" + per-plant regions.iso_rto confirmation
roadmap:    wire ISO filter to the region join, or add a resolve_region tool
```

## Session Capture & Extraction (The Process Is Data)

A test produces two things, and they are not the same artifact. The transcript is **raw source**; the test record is the **resolved extraction**. Treat them with the same discipline the data layer applies to news vs. resolved facts (`../principles.md` P3).

```text
RAW SOURCE                                RESOLVED EXTRACTION
the full chat transcript                  what we actually reuse
(every turn: prompts, tool calls,    ──►  · prompting moves that enriched the output
 retries, dead ends, redirections)        · enrichment deltas (one-shot → final, what changed + why)
                                          · fail→fix pairs (overclaim caught → the rule that should catch it)
   │ kept as source, never served            │ feeds prompt_projection edits + the eval suite
   ▼                                          ▼
test_runs/transcripts/<run>.md            test_runs/test_run_NNN.md  (+ docs/learning/logs/)
```

Three rules:

- **Save the whole chat, every experiment** — the intern's, the reviewer's, the agent's. The raw transcript is cheap to keep and impossible to reconstruct later.
- **Resolve it, or it is a swamp.** A folder of transcripts nobody extracts from is as useless as unread news. The extraction step (manual at first) is where the value is.
- **Extraction targets are model-agnostic.** Prompting moves, eval cases, and rule fixes survive the next model release; that is the point (`principles.md` P1). "Fine-tuning the workflow" = improving prompts/evals/process, not training a model.

The extracted `fail→fix` pairs map straight onto the Failure Taxonomy below: each becomes a concrete row, and each row that recurs is a candidate eval case.

## Feedback Intake (suggestions from outside the loop)

Feedback also arrives from **outside** the `/test-resource → /extract` loop — a build in another chat window, a colleague's review, owner notes. It is neither silently applied nor silently dropped; it runs the intake:

```text
1 CAPTURE    the feedback verbatim (or the source transcript) — raw source, kept (P3)
2 TRIAGE     every item gets a verdict: accept · reject · defer · already-covered — WITH a reason.
             Not every suggestion is useful; a reasoned REJECT is a first-class outcome, recorded.
3 ROUTE      each accepted item to exactly ONE home:
               voice / altitude        → resources/_principles/
               envelope / brand        → resources/_style/        (contract cells · brand.md)
               charts                  → resources/_craft/
               form lesson / prompt    → resources/_reference/    (exemplars/ · prompts/)
               tool gap                → ../status/mcp_gaps.md  (gap · workaround · roadmap)
               method / claims         → the package (resource.yml · blocked_claims)
               process / protocol      → test_protocol.md (this file) · commands
4 RECORD     the triage table → docs/learning/logs/<date>_<source>_intake.md
             (template: templates/feedback_intake.template.md)
5 ESCALATE   an accepted item that is STRUCTURAL — a new layer, a new contract cell, a new
             decision, a re-sequencing — is NOT patched inline: it becomes a plan in docs/plans/
             (or an amendment to the active plan's ladder). Small fixes route directly; structure
             goes through a plan. When in doubt: if it changes a §1 decision or adds a folder,
             it is a plan.
```

Three rules make this stick: **no canon edit without an intake record** (the record is what turns feedback into process data instead of drift — P3/P5); a batch that arrives as a *finished diff* (another session already edited the repo) gets its intake record **retroactively**, same table, plus a consistency cross-check for drift the edits left behind (skeletons, examples, sibling layers); and every feedback-driven edit **bumps the touched layer's version** and trips the staleness signal for dependents (`../method/resource_standard.md`).

## Test Record

Each test record should include:

- test title and date
- test owner
- loaded files
- question asked
- tools/data used
- applied-insight output
- accepted claims
- rejected or downgraded claims
- failures found (by type above)
- rubric scores (the 5 criteria, pass/flag/fail — `resources/_principles/rubric.md`)
- self-critique delta (what the bounded style pass changed; ≤2 iterations)
- composed shared-layer versions (e.g. `_principles v0.1`)
- next fixes
- link to the raw transcript (the source this record resolves)
- extracted prompting moves / enrichment deltas / fail→fix pairs (the reusable yield)

The template is `templates/mcp_test_run.template.md`; the first record to fill is `resources/weather_and_climate/el_nino_enso/test_runs/test_run_001.md`. That single run is what converts this whole `docs/` set from specification into evidence.
