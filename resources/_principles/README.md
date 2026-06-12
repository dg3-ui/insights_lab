# _principles — How We Judge & Speak

> **Status**: v0.2, 2026-06-12 (v0.1 Phase 1 · v0.2 adds `voice.md` §5 show-don't-flaunt — California-build feedback intake).
>
> **Role**: the shared **judging and voice layer** — the canonical output rubric, the bounded self-critique rules, and the house voice/altitude discipline. Cross-cutting: applies to every phenomenon package (ENSO, drought, grid studies…), which is why it lives here and not inside any of them.
>
> **Not a package**: no `resource.yml`, no slug, never indexed for discovery (`docs/07` §3). It is a shared layer per the underscore rule in `resources/README.md`.

## Stage Placement

```text
loads at DRAFT/TEST                      stays loaded through RENDER
  voice + altitude shape the insight       the rubric scores the final artifact
  stage-1 self-critique (skeleton only)    stage-2 self-critique (contract cell)
```

`_principles` is the only shared layer loaded **before** the gate. `_style` / `_craft` / `_reference` load **post-gate only** (`docs/04` Activation Boundary). Loading this layer is part of the pre-test checklist (`docs/05`).

## Contents

| File | What it owns |
|---|---|
| [`rubric.md`](rubric.md) | The 5 judging criteria · pass/flag/fail scoring · the two-stage, style-only self-critique bounds · where scores are recorded |
| [`voice.md`](voice.md) | House voice · humanization rules (no m-dashes, no AI tells) · altitude ("smartfulness") · the anti-microprompting doctrine |

## What This Layer Feeds

```text
rubric.md  ──► the human checkpoint's scoring step (docs/05 flow) ──► test_run records
           ──► /gate-check (when built, docs/10) — the INDEPENDENT accuracy judge
voice.md   ──► every drafting session (loaded with the projection)
           ──► every rendering (the humanization rules bind output prose)
```

What it must **never** do: override a package's `blocked_claims` / `confidence_rules` / `caveats` (those stay per-resource, `docs/03`), or ground a claim (this layer is FORM/logic, not evidence — `docs/04`).

## Versioning

The version in the Status line is bumped on any material change; test runs record which version they composed (`templates/mcp_test_run.template.md`). A version change here is a staleness signal for resources validated against the old one (`docs/03`).

---

**See also**: `../README.md` (the underscore-layer rule + Shared Layers table), `../../docs/05_mcp_test_protocol.md` (where the rubric scores land), `../../docs/08_design_principles.md` (P2/P4 — the gate order and the loop this layer serves), `../../docs/plans/2026-06-11_layered_reference_v1.md` (D1/D2/D6 — the decisions this layer implements).
