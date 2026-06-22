# 04 - Prompt Projection

> **Purpose**: explain how a methodology resource collapses into the strict, pasteable surface the model sees in a manual test — its anatomy, what it includes and excludes, and the failure modes it must prevent.
>
> **Grounded in**: `resources/weather_and_climate/el_nino_enso/prompt_projection.md` + the live first-call trace, 2026-06-05.

## Definition

A prompt projection is the **condensed, stricter** form of a methodology resource — the operational cut that runs in a Claude/MCP session. It is shorter than the full resource and tighter than an ordinary prompt.

```text
full resource (resource.md + resource.yml)   ← canon, the "why", the audit reference
        |  project: keep the operational rules, drop the prose
        v
prompt_projection.md                          ← what the model actually receives
        |
        v
Claude/MCP session  ->  applied-insight draft
```

## Why Project At All?

Two reasons, both practical:

| Reason | Without projection | With projection |
|---|---|---|
| **Context economy** | the full repo competes for attention | one focused instruction surface |
| **Strictness** | background prose invites elaboration | terse rules invite compliance |

`resource.yml` even declares the cut explicitly — its `prompt_projection` block lists `include_in_prompt` (question grammar, scope, procedure, allowed/blocked claims, confidence rules, output format) and `exclude_from_prompt` (long background prose, full repo context, email/outreach instructions). The projection is not a summary you improvise; it is a **specified subset**.

## Anatomy Of The ENSO Projection

The real `prompt_projection.md` has eight parts. Each maps to a job:

```text
SECTION                  JOB IT DOES
----------------------   ---------------------------------------------
Role                     "act as an InfraSure Insights analyst"  → sets stance, not persona fluff
Task + scope             one directional insight, "CAISO solar ≥ 50 MW"  → bounds the work
Required reasoning steps  identify ENSO state → mechanism → retrieve → filter → claim  → forces order
Required inputs          external ENSO + plant list + capacity + owner…  → makes retrieval explicit
Allowed claims           directional exposure, mechanism, actor relevance  → the ceiling
Blocked claims           exact LMP, plant-level forecast, outreach copy   → the floor
Confidence rules         high/medium/low/blocked decision table           → conservative by default
Output format            Claim · Scope · Mechanism · Source Refs · Confidence · Caveats · Actor · Gaps
```

The output format is doing quiet work: by **requiring a Source Refs section and a Confidence line**, it makes an ungrounded or over-confident answer structurally obvious in review.

## What A Projection Includes / Avoids

```text
INCLUDE                          AVOID
-------------------------        --------------------------------
role + stance                    long background / motivation prose
the one scoped task              "write an article about ENSO"
ordered reasoning steps          open-ended "tell me about…"
required input categories        instructions needing unavailable data
allowed + blocked claims         exact forecasts the method blocks
confidence rules                 email / outreach copy
a rigid output format            anything that needs the full repo to interpret
```

## Failure Modes A Projection Must Prevent

The test pass/fail criteria (`../process/test_protocol.md`) are really a list of failures the projection exists to stop. For each, the line that prevents it:

| Failure | What it looks like | Projection guardrail |
|---|---|---|
| Generic commentary | "ENSO may affect markets" — no entities | Required inputs + "retrieve substrate data" step |
| Skipped retrieval | confident prose, zero `plant_id`s | "identify required data before drafting" + Source Refs section |
| Overclaim | "LMP will rise $8/MWh" | Blocked claims: exact LMP from ENSO alone |
| Plant-level forecast | "this plant loses 12 GWh" | Blocked claims: no plant-level forecast w/o modeling |
| Missing caveats | directional claim stated as fact | Mandatory Caveats section |
| Jump to outreach | drafts an email | Blocked claims: no outreach before validation |
| Unscoped scan | "all US solar" | Task scope: one region, one asset class |

If a test fails one of these, the fix is usually a **prompt gap** — tighten the projection — not a model failure.

## A Real First-Call Trace

What a *good* first move looks like under this projection, with the live tools (2026-06-05):

```text
GOOD                                                    WHY
search_plants(fuel="solar", state="CA", minMw=50)  ->   resolves the real fleet (8 plants)
cite _meta.as_of = "2026-06-05"                    ->   vintage attached
get_plant(57993) for CF + owner + offtaker         ->   drill for grounding
"ENSO state pending external source (NOAA CPC)"    ->   names the external dependency, doesn't invent it

BAD                                                     DIAGNOSIS
search_plants(iso="CAISO")  -> [] then gives up    ->   didn't fall back to state= (knowable gap)
"California has ~37 GW of solar…" with no IDs       ->   skipped retrieval → prompt gap
"Expect ~5% winter generation loss"                ->   overclaim → blocked-claims line too weak
```

Note the first BAD line: a well-written projection would *pre-empt* it by telling the model the ISO filter is unreliable and to scope by `state`. That is the projection absorbing a known tool gap so the test doesn't stall on it.

## Review Rule

```text
If the prompt projection cannot be pasted into a fresh Claude/MCP session — with no other repo
files loaded — and still produce a scoped, grounded, caveated draft, it is too dependent on
surrounding documentation. Tighten it until it stands alone.
```

A projection that needs the repo to make sense has failed its one job.

---

**Back to**: `README.md` (read order) · **then run**: `resources/weather_and_climate/el_nino_enso/test_runs/test_run_001.md` and log what the projection let through — that test is what turns these four docs from theory into evidence.
