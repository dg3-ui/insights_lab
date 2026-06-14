# Internal Reference — Our Own Outputs We Like

> **Status**: opened 2026-06-13. The **internal** wing of `_reference/` — validated outputs *we* produced and liked, kept as a growing reference for improvement. Distinct from the **external** wing (`../exemplars/`, `../prompts/`), which holds others' work as form-only exemplars.

## What This Is (and isn't)

This is a gallery of **our own golden outputs** — real, gated pieces that exemplify the qualities we want (structure, voice, brand, grounding, the right altitude) all at once. Unlike the external exemplars, these *also* demonstrate correct grounding and discipline, because they're our validated work.

But the **same two rules apply to both wings:**

1. **Re-ground facts live.** Even our own past output's numbers are dated. Never cite a number *from here* — re-pull it. These teach **form and quality**, never live facts.
2. **A reference informs, it doesn't bind** (`../../../docs/principles.md` P6). These are *inspiration*, not templates to satisfy. Use a quality from one when it improves the output; if it doesn't, drop it. A new piece does not have to look like the gallery — it has to be good and grounded. The gallery is a floor for ideas, never a cage.

## Three Categories (= the three output types)

```text
internal/
├── blog/     top-down, generic-but-useful pieces        (e.g. enso_ca_solar_2026-06)
├── report/   a blog scoped to a portfolio/client/region/purpose   (none yet — cracked in Phase 5)
└── email/    the condensed subset of a blog or report            (none yet — built last)
```

Each artifact is paired with a **metadata sidecar** (`<name>.md`) so the gallery *teaches*, not just stores.

## Metadata Schema (the sidecar)

```yaml
title:         <the piece's title>
output_type:   blog | report | email
tags:          { direction: top_down|bottom_up, audience: internal|client|public, phenomenon: …, domain: … }
provenance:    where it came from (which iteration / test_run / session) + date
grounding:     validated · data as_of <date>   (facts are dated — re-ground live, never cite from here)
exemplifies:   [ the qualities worth borrowing — what makes this one good ]
still_improve: [ what we did NOT love yet — the gap, so the gallery captures the lesson, not just the win ]
```

## How It Feeds Improvement

```text
internal gallery ─┬─► the RUBRIC (_principles): "what good looks like" anchors for scoring
                  ├─► the OUTPUT CONTRACTS (_style): concrete filled examples each output points to
                  └─► a future EVAL harness: golden outputs to check new work against
   ✗ never the grounding layer — re-ground facts live (same quarantine as the external wing)
```

## Scale note (decide later, not now)

At a handful of files, committing binaries (`.docx`, `.pptx`) into git is fine. As this grows toward dozens, revisit whether the gallery stores the binary or a markdown transcript + a link/export — to avoid repo bloat. Not a blocker today.

---

**See also**: `../README.md` (the reference corpus + its two rules), `../../_style/output_contracts.md` (the three outputs this gallery exemplifies), `../../../docs/principles.md` P6 (references inform, don't bind), `../../_principles/rubric.md` (what the gallery anchors).
