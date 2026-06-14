# studio/ — The Output Workshop (Layer 3 · where insight becomes a home run)

> **Status**: v0, opened 2026-06-14 (`../docs/plans/2026-06-14_studio_and_bottom_up.md` Phase 1). The lab's **output half**: where a **validated, gated** insight gets the *home-run treatment* — a captured creative layer on top of grounded content — and is rendered into a deliverable.
>
> **What loads here is post-gate.** studio holds **renderings of validated insight + their creative dress** — never the origin (`../docs/principles.md` P2).

## What studio is — and isn't

```text
studio IS    a SELECTIVE amplification lane — the CHERRY on top, not a mandatory stage.
             opt-in, for the pieces that must LAND as home runs. spans ALL use-case types
             (top-down blogs · in-substrate + off-substrate bottom-up · plain resource+MCP→output).
studio ISN'T a pipeline gate. MOST outputs stay on the BASELINE path (gated insight → render) with NO
             studio creative pass. You spend the creative budget only where it earns a home run —
             that selectivity is itself a guard against content-farm drift.
```

## The lifecycle

```text
studio/<brief>.md   the WORKSHOP — draft · iterate · carry the creative ideas · cloud-attachable
       │ when validated + we like the form
       ▼
../resources/_reference/internal/{blog|report|email}/   the curated form ARCHIVE (the gallery), reused as a form exemplar
```

## The brief — a self-contained, cloud-attachable output

Each studio file is a brief (template: [`_brief_template.md`](_brief_template.md)) carrying: the **gated insight** (+ `source_refs`) · the **MCP comparison** (the moat + the hook) · a **Creative & Activation** section · pointers to the form layers. To render: attach the brief + the format-agnostic `_style/brand.md` + `_principles/voice.md` (+ `_craft` if charts) to a session → render for the target format (DOCX / HTML / …).

## The three guards (the moat's blast radius — non-negotiable)

The creative layer is the first thing in the lab whose job is to *persuade*, so it carries the heaviest discipline:

```text
1. GATE STAYS UPSTREAM (P2)    studio dresses a VALIDATED insight; it NEVER originates one.
                               order is immutable: insight → GATE → render → creative.
2. CREATIVE ≠ OVERCLAIM        the punch lands on the HOOK / title / framing / hero visual — NEVER on a claim's
                               magnitude (`../resources/_principles/voice.md` §3 + §6). A catchy title, yes; a bigger number, never.
3. THE HOOK IS GROUNDED        the home-run line (the comparison, "you vs peers over 12 months") is an MCP result —
                               real, not invented. The creative layer AMPLIFIES a grounded comparison, never manufactures one.
```

## Contents

```text
studio/
├── README.md                     this file
├── _brief_template.md            the output-brief template (the Creative & Activation section + the guards inline)
├── brookfield_standard_solar.md  ✅ home run — a DG/community-solar book only ~23% El-Niño-exposed; the data OVERTURNED
│                                    the brief's "concentrated CA fleet" premise and the reversal IS the hook (MCP comparison)
└── anten_ports.md                ✅ coastal storm-surge read — "Anten" was UNRESOLVABLE as a company, so built grounded on a
                                     real Galveston Bay / Houston Ship Channel gas cluster (~3.7 GW, nearby_plants). The 2nd
                                     outlier after Red Dog → the COASTAL energy-and-logistics chokepoint class.
```

---

**See also**: `../docs/plans/2026-06-14_studio_and_bottom_up.md` (the plan) · `../docs/discussion/2026-06-14_bottom_up_output_workshop.md` (the discussion + the thinking) · `../resources/_style/output_contracts.md` §5 (the studio guards in the form contract) · `../resources/_style/brand.md` (the format-agnostic look) · `../resources/_principles/voice.md` §6 (the creative-punch guard) · `../resources/_reference/internal/` (the gallery studio promotes into) · `../docs/architecture.md` (Layer 3) · `../docs/use_cases.md` (the activation boundary — send stays human-in-the-loop).
