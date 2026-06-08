# Reference Corpus — Exemplars, Not Sources

> **Status**: v0 reference library, 2026-06-05.
>
> **Purpose**: hold external exemplars of *how good infrastructure/energy insight reads* — competitor insight notes, analyst briefings, strong industry LinkedIn posts — so the rendering layer and the eval suite have a "what good looks like" reference. This folder underscores (`_reference`) sorts above the domain folders and is **never** a methodology resource.

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

The trap to avoid: ingesting a competitor note and parroting its *assertions* instead of its *form*. Extract the structure; discard the claims. (`08_design_principles.md` P2: content is downstream of validated insight; this corpus feeds rendering, never grounding.)

## What It Feeds

```text
exemplar corpus ─┬─► RENDERING layer (Layer 3): how a blog / email / card / post should read
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
└── README.md      # this file (the quarantine rule)
                   # exemplars land here as they are collected
```

---

**See also**: `docs/08_design_principles.md` (P2: content downstream of insight), `docs/learning/02_infrasure_data_substrate.md` (grounds / frames / routes), `docs/02_analysis_catalog.md` (the families a strong rendering should still respect).
