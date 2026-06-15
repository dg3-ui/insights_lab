# studio/ — The Output Layer (Layer 3 · where validated insight becomes a home run)

> **Status**: v0.2, 2026-06-15 — restructured into a **scalable output layer**: a confidence foundation, a subject-keyed render layer, and a separate triage layer (`../docs/plans/2026-06-15_output_layer_architecture.md`). Was v0 flat briefs (2026-06-14). The lab's **output half**: where a **validated, gated** insight gets the *home-run treatment* and is rendered into a deliverable.
>
> **What loads here is post-gate.** studio holds **renderings of validated insight + their creative dress** — never the origin (`../docs/principles.md` P2).

## The architecture — a foundation + three layers

```text
FOUNDATION   ../docs/method/confidence_model.md   the three axes every brief records in §1
             CALIBRATION CAP (internal grade) · EVENT LIKELIHOOD (on output) · MATERIALITY (internal band)
             on the rendered face: POSTURE + the event number + a SETTLEDNESS bar. the grade never renders.

LAYER 1  RENDER   studio/<subject>/<phenomenon>.md
         subject = an entity (Brookfield/Standard Solar) OR a region/corridor (Galveston surge corridor — used
         when the entity is unresolvable). phenomenon = the driver, matching a resource slug (el_nino_enso).
         each phenomenon file is SELF-CONTAINED + cloud-attachable; its §1 is the SINGLE SOURCE OF TRUTH.

LAYER 2  TRIAGE   studio/_triage.md   ONE internal board, never attached
         derives from the §1 gate-records → ranks subject×phenomenon by cap + materiality → ACT / WATCH / NOISE.
         a prioritization capability, not a render artifact. re-states no grade; links each §1.

LAYER 3  GALLERY  ../resources/_reference/internal/{blog|report|email}/
         validated phenomenon files promote as FORM exemplars (form, never facts).
```

## What studio is — and isn't

```text
studio IS    a SELECTIVE amplification lane — the CHERRY on top, not a mandatory stage.
             opt-in, for the pieces that must LAND as home runs. spans ALL use-case types
             (top-down blogs · in-substrate + off-substrate bottom-up · plain resource+MCP→output).
studio ISN'T a pipeline gate. MOST outputs stay on the BASELINE path (gated insight → render) with NO
             studio creative pass. You spend the creative budget only where it earns a home run.
```

## Subject-keying — entity OR region

A subject folder is keyed by **what the read is about**, which is usually an entity (an owner, an account) but is a **region/corridor** when the entity won't resolve. The Galveston corridor is the worked case: the commissioned entity ("Anten") did not resolve to any real company, so the subject is the **Galveston Bay / Ship Channel surge corridor** it would sit in — honest, grounded, and still a real read (`galveston_ship_channel_surge/storm_surge.md`; `../docs/method/confidence_model.md`). One subject folder holds many phenomena over time, and once it carries **≥2 phenomena it earns a subject-guide `README.md`** — an account profile + a ranked phenomenon matrix + the cross-resource map, which makes the folder behave like a per-account *skill*. `brookfield_standard_solar/` is the first (`el_nino_enso.md` + `hail.md`, with extreme-heat and offtaker scaffolded in its guide). That is the scalable grain: a subject becomes a guide as its phenomena accumulate.

## The single source of truth + render-internal

```text
§1 GATE-RECORD       each brief's §1 holds the three axes ONCE. output posture (§3) and the triage board both
                     DERIVE from it. a grade with one home does not drift; a grade in two places does.

RENDER-INTERNAL ≠ HOST-PRIVATE   (confidence_model.md §7 — two orthogonal axes, do not conflate)
   render-internal   the CAP GRADE · the MATERIALITY band · the TRIAGE verdict — NEVER on a rendered artifact
   host-private      the repo's git-remote visibility — an infra setting
   a private repo does NOT make it safe to print the grade on a client render. the grade stays off the
   rendered face regardless of where the file lives. a brief is designed to be handed to a client.
```

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
├── README.md                         this file
├── _brief_template.md                the output-brief template (the §1 three-axis gate-record + the guards inline)
├── _triage.md                        Layer 2 — the one internal prioritization board (derived; never rendered)
├── brookfield_standard_solar/        subject = account · MULTI-PHENOMENON (carries a subject-guide README)
│   ├── README.md                     the subject GUIDE — account profile + ranked phenomenon matrix + cross-resource map
│   ├── hail.md                       ✅ severe hail — 0 MW in the US hail maximum; ~6% CO Front Range + MN/IL/NM convective.
│   │                                    MORE material than ENSO (hail breaks panels) yet spread, not concentrated
│   └── el_nino_enso.md               ✅ home run — a DG/community-solar book only ~23% El-Niño-exposed; the data
│                                        OVERTURNED the "concentrated CA fleet" premise and the reversal IS the hook
└── galveston_ship_channel_surge/     subject = region/corridor (the unresolvable "Anten", keyed honestly)
    └── storm_surge.md                ✅ coastal chokepoint — ~3.7 GW of ERCOT gas inside one surge cell
                                         (nearby_plants(55327)); the 2nd outlier after Red Dog → the COASTAL class
```

---

**See also**: `../docs/method/confidence_model.md` (the foundation — the three axes, posture, materiality, render-internal) · `_triage.md` (Layer 2) · `../docs/plans/2026-06-15_output_layer_architecture.md` (the architecture) · `../docs/discussion/2026-06-14_bottom_up_output_workshop.md` (the thinking) · `../resources/_style/output_contracts.md` §5 (the studio guards in the form contract) · `../resources/_style/brand.md` (the format-agnostic look) · `../resources/_principles/voice.md` §6 (the creative-punch guard) · `../resources/_reference/internal/` (the gallery studio promotes into) · `../docs/architecture.md` (Layer 3) · `../docs/use_cases.md` (the activation boundary — send stays human-in-the-loop).
