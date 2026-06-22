# Log — audience is a render switch: the internal-vs-external strip (2026-06-16)

> **Status**: process-capture (`../../principles.md` P3). A `/render` of the Red Dog read shipped **internal-framed** first, then had to be re-cut for an **external** reader. The lesson: *audience* is a first-class render input, and the internal-only tells need one enumerated home. Staged edits for `render.md` live beside this log in `render_audience_strip.patch.md` (protected path — operator applies).

## The headline lesson

**One gated insight, two faces. The gate verdict never changes; the surfacing does.** The first Red Dog DOCX was correct and on-brand but written for *us* — it carried the internal scaffolding onto a page meant for a counterparty. The fix was not new analysis; it was a **strip pass keyed to audience**. That switch was implicit (scattered across `voice.md` §5, `output_contracts.md` §2, `confidence_model.md` §7) and absent from the one place that conducts the render, so it got skipped.

```text
SAME gated insight ──► internal render   keeps: provenance label · per-claim fact/projection · direction tags · (expert) cap line
                  └──► client/public     strips them → posture + grounding + forward door only
```

## The strip list (codify once; `render.md` STEP 4 points here)

```text
TELL (internal-only)                         INTERNAL   CLIENT/PUBLIC   HOME
──────────────────────────────────────────   ────────   ─────────────   ─────────────────────
direction / substrate meta-tags              keep       STRIP           output_contracts §2 not-include
  (bottom_up · off-substrate)                                             (internal-taxonomy labels)
grounding-provenance labels                  keep       STRIP           voice §5 (P7) — provenance is
  ("research-grounded · not MCP · not gpr")                              method-talk, not reader copy
capability / moat sections                    n/a        STRIP           voice §5 (show-don't-flaunt),
  ("What InfraSure adds here")                                           output_contracts §2 not-include
internal-artifact critiques                   keep       STRIP/REFRAME   voice §5 — reframe to the asset,
  ("the framing the LT-Risk deck missed")                                not "their deck was wrong"
cap grade · materiality band · triage         (expert    NEVER           confidence_model §7
                                               cap line                  (already render-internal)
                                               optional)
```

**Nuance that bit us (don't lose it):** for the *internal* Red Dog render, keeping "not MCP / not model-gpr" was logged **correct** (`2026-06-15_reddog_render_build.md`). So the rule is **audience-conditional**, never "always strip." Internal honesty label = useful provenance; the same label on a client face = a capability-confession (P7).

## Fail → fix (this session)

```text
FAIL (first external pass)                         FIX → where it lives
─────────────────────────────────────────────     ─────────────────────────────────────────
shipped the internal cut to an external reader     audience parse + strip pass        → render.md STEP 0 + 4 (patch)
"bottom_up / off-substrate" on the meta line       drop direction/substrate tags      → output_contracts §2
"not MCP, not model-gpr" on the face               drop provenance label (client)     → voice §5 (P7)
"What InfraSure adds here" section                 cut the capability/moat section    → voice §5 / output_contracts §2
"the LT-Risk deck missed…" asides                  reframe to the asset, not the deck → voice §5
```

## What stays true regardless of audience (the floor)

```text
· the gate verdict + claim grammar + blocked_claims — identical on both faces (only surfacing differs)
· every material number traces to source_ref + as_of
· posture renders (cap grade internal); confidence is three axes (confidence_model)
· no send/outreach automation — a human reviews any render before external use (use_cases activation boundary)
```

## The staged `render.md` edits (see `render_audience_strip.patch.md`)

```text
STEP 0  parse an `audience` arg (internal | client | public); else read the source's audience
        meta-tag; DEFAULT to the client-safe cut (strip on, unless internal is explicit).
STEP 4  add an AUDIENCE-STRIP guard: for client/public, run the strip list above; for internal,
        the provenance label + per-claim labels + (optional) cap line may stay. Thin conductor —
        points to voice §5 / output_contracts §2 / confidence_model §7, restates nothing.
```

## See also

`../../../resources/_principles/voice.md` §5 (show-don't-flaunt · forward door · P7), `../../../resources/_style/output_contracts.md` §2 (not-include list), `../../method/confidence_model.md` §7 (render-internal axes), `../../../.claude/commands/render.md` (the conductor these edits land in), `2026-06-15_reddog_render_build.md` (the internal render whose provenance label was correctly kept — the nuance this log preserves).
