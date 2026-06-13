# Reference Corpus — Exemplars, Not Sources

> **Status**: populated v0.1, 2026-06-12 (plan Phase 4) — 3 Grid Status exemplars + 1 prompt exemplar; **open for intake** (see Pending Intake).
>
> **Purpose**: hold external exemplars of *how good infrastructure/energy insight reads* — Grid Status blogs, Substack grid-studies, competitor insight notes, analyst briefings, strong industry LinkedIn posts — so the rendering layer and the eval suite have a "what good looks like" reference. This folder underscores (`_reference`) sorts above the domain folders and is **never** a methodology resource.
>
> **Two reference kinds** (both quarantined the same way):
> - **`exemplars/`** — pieces whose *form* we imitate (structure, hook, caveat style).
> - **`prompts/`** — the *messaging that traveled with the references* and produced good output (prompting moves, `../../docs/principles.md` P3 process data); each entry maps its moves to the shared layer that absorbed them.

## The One Rule: Form, Not Facts

```text
THIS CORPUS TEACHES          THIS CORPUS NEVER SUPPLIES
─────────────────            ──────────────────────────
format · structure           a fact · a number · a claim
framing · rhetorical moves   a source_ref
what resonates in-industry   grounding of any kind
length / tone for an audience
```

A competitor's insight can show us *how to say it well*. It can **never** be the source behind one of our claims. Every grounded claim still traces to the InfraSure substrate + a named external source (`docs/learning/02_infrasure_data_substrate.md`). This is the same `grounds / frames / routes` discipline applied to outside material — a reference exemplar **frames** style only.

The trap to avoid: ingesting a competitor note and parroting its *assertions* instead of its *form*. Extract the structure; discard the claims. (`../../docs/principles.md` P2: content is downstream of validated insight; this corpus feeds rendering, never grounding.)

## What It Feeds

```text
exemplar corpus ─┬─► RENDERING layer (Layer 3): the _style output contracts cite specific
                 │     exemplar lessons per cell; /render composes them (blog/brief/email/post)
                 ├─► the RUBRIC's style criteria (format · presentability) — _principles/rubric.md
                 └─► EVAL suite: a "good output" yardstick for examples/ + test_runs/
                 ✗ NOT the grounding layer — quarantined from any claim's source_ref
```

## How To Add An Exemplar

```text
1. Save the source (or a faithful excerpt) + provenance: who · where · when · URL.
2. Note WHY it is here — the specific form lesson (structure, hook, caveat style, actor framing).
3. Strip or clearly mark any factual claims so they are never mistaken for grounded inputs.
4. Mind provenance/PII — especially for individual LinkedIn authors; store an excerpt + link, not scrapes.
```

## Contents

```text
resources/_reference/
├── README.md                              # this file (the quarantine rule + intake)
├── exemplars/
│   ├── grid_status_curtailment.md         # the phenomenon-explainer form (top_down blog)
│   ├── grid_status_4cp_storage.md         # the seasonal-mechanism data piece (+ header-personality dose)
│   └── grid_status_rabbit_hill.md         # event → mechanics → named asset (the bucket-2→1 drill)
└── prompts/
    └── blog_messaging_001.md              # the messaging that cracked top-down, moves mapped to layers
```

## Pending Intake (owner-provided; not a blocker — logged so it isn't lost)

| Awaiting | From | Lands as |
|---|---|---|
| Detailed reference list: websites · LinkedIn accounts · Substack accounts | Divy (promised 2026-06-12, "I'll do that later") | `exemplars/` entries via the 4-step protocol below |
| The strongest day-one internal top-down output | Divy / Daniel's project | an internal exemplar (it is our own gated work, so its facts stay valid — but it files here for *form*) |
| 1–2 Substack grid-study pieces | owner list or curated search | `exemplars/` entries, tagged Market Context / Event Translation |
| The authored bottom-up exemplar | plan Phase 5 (iterate-and-compare) | `exemplars/` + fills the §5/§6 contract cells |

---

**See also**: `../../docs/principles.md` (P2: content downstream of insight), `docs/learning/02_infrasure_data_substrate.md` (grounds / frames / routes), `../../docs/method/analysis_families.md` (the families a strong rendering should still respect).
