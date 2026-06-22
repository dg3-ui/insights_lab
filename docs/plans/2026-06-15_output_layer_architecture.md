# Plan — The Output-Layer Architecture (foundation + render + triage)

> **Status**: ACTIVE, opened 2026-06-15. Supersedes the studio scaffold in `2026-06-14_studio_and_bottom_up.md` (which stood studio up as flat briefs); this plan makes the output layer **scalable** — a confidence foundation, a subject-keyed render layer, and a separate triage layer. Owner-blessed 2026-06-15 ("do this end to end correctly").
>
> **Why now**: a 4-lens design review (2026-06-14) flagged the flat-file studio as not-yet-scalable: confidence conflated into one axis, the grade sitting on the rendered face, no single source of truth, triage implied but unbuilt, "Anten" keyed as an account it can't resolve to. The owner chose to build the **right long-term shape** rather than patch. This plan is that shape.

## The decision (what "right at scale" means here)

The output layer is a **foundation + three layers**. The load-bearing move is that **confidence is three axes, only one is a grade, and the grade never reaches the rendered face**.

```text
FOUNDATION — THE CONFIDENCE MODEL            docs/method/confidence_model.md  (NEW canon)
  three orthogonal axes, each grounded:
    · CALIBRATION CAP    how hard we may assert THIS claim (weakest input)   → INTERNAL grade
    · EVENT LIKELIHOOD   the world's probability (NOAA 63%), sourced          → ON OUTPUT
    · MATERIALITY        exposed-share × class-severity band; a BAND not a $   → INTERNAL
  on output: POSTURE (a register-translation of the cap) + the event number + a SETTLEDNESS signal.
  the cap grade + materiality + the triage verdict stay INTERNAL (render-internal ≠ host-private).

LAYER 1 — RENDER OUTPUTS            studio/<subject>/<phenomenon>.md
  subject = an entity OR a region/corridor (handles the unresolvable "Anten" → a corridor)
  each phenomenon file SELF-CONTAINED + cloud-attachable · §1 gate-record = SINGLE SOURCE OF TRUTH
  for the three axes (per-part allowed) · posture on output · folder-per-subject is the scalable norm.

LAYER 2 — TRIAGE / PRIORITIZATION   studio/_triage.md   (ONE internal board, never attached)
  derives from the §1 gate-records: rank subject×phenomenon by cap + materiality → ACT / WATCH / NOISE.
  a prioritization capability, not a render artifact; never re-types a grade (links each §1).

LAYER 3 — GALLERY                   resources/_reference/internal/{blog|report|email}/
  validated phenomenon files promote as FORM exemplars (unchanged; form, never facts).
```

## The correctness invariants (baked in, not deferred)

```text
· single source of truth     the three axes live in §1; output posture + triage BOTH derive (no two-copy drift)
· materiality has a basis     exposed-share × class-severity band; a band, never a $; tie-breaker NOT override
· three-axis confidence       written into confidence_model.md canon FIRST, then encoded (P1: sharpen, then build)
· subject-keyed, not account  an unresolvable entity becomes a region/corridor subject, honestly
· triage is its own layer      the act/watch/noise dial is one cross-subject board, not scattered per-folder READMEs
· the arcs survive            folding preserves Brookfield's reversal + the storm-surge refusal-to-fake (diff-checked)
· render-internal ≠ host-private   a private repo never excuses a grade on a client-facing render
```

## Build phases (this plan)

| # | Phase | Deliverable | State |
|---|---|---|---|
| 1 | Foundation | `docs/method/confidence_model.md` (three-axis canon + posture map + settledness signal + materiality basis) | — |
| 2 | Bind the canon | `resource_standard.md` Confidence Rules reframed to the three axes; point to the model | — |
| 3 | Render layer | fold to `studio/<subject>/<phenomenon>.md`; Brookfield→`brookfield_standard_solar/el_nino_enso.md`; Anten→`galveston_ship_channel_surge/storm_surge.md`; new confidence representation; §1 as single source | — |
| 4 | Triage layer | `studio/_triage.md` — one derived cross-subject board | — |
| 5 | Template + README | `_brief_template.md` (subject/phenomenon, per-part, single-source); `studio/README.md` (the four-part architecture + the render-internal/host-private guard) | — |
| 6 | Bind the contracts | `output_contracts.md` §3/§5, `brand.md` §A4, `voice.md` §5, `rubric.md` criterion 4 — refs to the model + the settledness signal | — |
| 7 | Verify | adversarial multi-lens pass (foundation holds · single-source respected · no leaked grade · arcs preserved · cross-refs consistent) | — |

## The confidence representation (the owner-blessed shape)

```text
ON OUTPUT, "Confidence: LOW" is replaced by two honest things + one forward signal:
  · POSTURE    "a forward, directional read — watch, don't act yet"   (register-translation of the cap)
  · EVENT      the sourced likelihood (NOAA 63% very-strong El Niño)   (a real number, not our self-grade)
  · SIGNAL     a 5-segment SETTLEDNESS bar: fills as the driver firms (63%→90%), forward not self-doubt.
               never "1/5 = we're unsure"; it reads "the read firms as the season resolves."
the cap grade (High/Med/Low/Blocked), the materiality band, and the triage verdict NEVER render.
```

---

**See also**: `docs/method/confidence_model.md` (the foundation this plan builds) · `docs/discussion/2026-06-14_bottom_up_output_workshop.md` (the thinking) · `2026-06-14_studio_and_bottom_up.md` (the scaffold this supersedes) · `studio/README.md` (the layer it documents) · `docs/principles.md` P7 (calibration is posture) · `resources/_principles/rubric.md` criterion 4 (the cap the model enforces).
