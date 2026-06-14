# Output Contracts — blog · report · email

> **Status**: v0.2, 2026-06-13 (revamped to the three-output model; the earlier direction×audience×format matrix was over-built — simplified to the three output *types*).
>
> **What a contract is**: a light **envelope** for an output — roughly its length, tone, the shape readers expect, what NOT to include, and the gate guard. It is **not a template to satisfy** and not a cage: it is inspiration the model uses when it helps and sets aside when it doesn't (`../../docs/principles.md` P6). The inside flexes by phenomenon, scope, and the model's judgment; the envelope just keeps the outside coherent and on-brand.
>
> **THE GATE PRECONDITION — on every output, no exceptions**: a contract renders **only a validated insight** — one that passed the `../../docs/process/test_protocol.md` gate with its `review_trace` complete. Rendering before the gate is the `../../docs/principles.md` P2 violation; `/render` must refuse it.

## §1 · The Three Outputs

```text
blog    top-down, generic-but-useful information — broad, public-facing
report  the SAME format family as a blog, but targeted to a specific
        portfolio / client / region / purpose
email   a condensed SUBSET of either a blog or a report
```

The relationships are the whole model:

- **blog ↔ report overlap in nature.** Same format, same structural moves; the only difference is *generic* (blog) vs *targeted* (report). A report is "a blog, scoped to one portfolio / client / region / purpose."
- **email is a subset of both.** It is the distillation — one claim, one number, one watch-line — pulled from a blog or a report.

**Meta-tags** describe any given piece without multiplying output types: `direction` (top_down / bottom_up — the `../../docs/method/analysis_families.md` §Exposure axis), `audience` (internal / client / public), plus phenomenon and domain. A blog tends top-down/public; a report tends targeted (a specific book, account, or region). These are descriptors, not new formats.

**Build order ≠ delivery order:**

```text
BUILD ORDER (how we develop + validate the engine)
   blog / report  FIRST   ──►  email  LAST
   the rich pair create the richest feedback loop — iterating a blog or report shows whether
   the insight is deep and well-grounded. You cannot judge insight-richness from a terse email,
   so email is the WRONG place to start; it is the final, distilled output once the rich one is proven.

DELIVERY ORDER (which output ships when, to whom)
   a SEPARATE business question, NOT settled here, NOT the build order — do not conflate.
```

## §2 · Blog — top-down, generic (the cracked structure)

The validated form, codified from what worked (the InfraSure ENSO / CA-solar piece — see the internal golden output in `../_reference/internal/blog/`; external form from `../_reference/exemplars/`). Use these moves when they help; drop any that don't (P6).

| Envelope | Value |
|---|---|
| Rendering | HTML artifact (`brand_assets/artifact_skeleton.html`); DOCX export on request |
| Display | topic kicker (one word, above the title: "ENSO" · "Solar") · date posted, Day Month Year · estimated read time |
| Length | ~800–1,400 words · 1–2 grounded charts |
| Tone | `voice.md` §1–§2 — analyst-direct, human, zero AI tells; section heads may carry personality, the prose under them stays precise |
| Gate guard | **validated insight only**; every number traces to the insight's `source_refs` |

Structural moves (a guide, not a checklist — P6):

```text
0 DISPLAY    topic kicker · date · read time   (the title block, brand.md §4)
1 TITLE+DEK  catchy via a rhetorical device; honest numbers (hyperbole never lands on a claim, voice.md §3)
             dek = informative subtitle: what the piece covers + why now
2 SUMMARY    3–4 takeaway bullets + a calibration cue (posture, not a pejorative "LOW" stamp)
3 CONDITION  what changed — the external state, dated + ≤1 background paragraph (frames, never grounds)
4 EXPOSED    WHO / WHERE — named entities, IDs, MW, owners, region (the entity table + spatial figure)
5 MECHANISM  one breath, first-principles prose
5a HISTORY   dated past episodes as evidence where they exist (each cites its own source ref)
6 CHART(s)   grounded series, fleet/region scope for top-down; caption + source + as_of below (_craft rules)
7 CAVEAT     the honest caveat (what is still resolving), confident — not a "we are not saying X" negation list
8 WATCH      forward hook — what resolves when
9 CONCLUDE   zoom out: why it matters; no triumphant summary + FOOTER (sources + as_of register + brand line)
```

Not-include: price/LMP forecasts · plant-level production forecasts · outreach CTAs · unscoped national claims · exemplar-derived facts · **internal-taxonomy labels** (the artifact is reader-facing; the kicker names a topic, never our categorization) · **moat / meta-pitch language** ("unreachable without a general model", "15,000 plants" as a boast) — that is the sales narrative (`../../docs/use_cases.md`), not reader copy (`../_principles/voice.md` §5: show, don't flaunt; demonstrate by grounding + a product deep-link to infrasure.ai).

**Confidence display, public vs internal.** A public/broad blog conveys calibration as *analytical posture* ("a forward, directional read"), carried by precise grounding and the honest caveat — **not** a self-deprecating "Confidence: LOW" badge or a "we make no forecast" disclaimer. A targeted report for an internal/expert reader may keep the explicit confidence line — the decider wants the label. The gate's LOW/directional verdict underneath is unchanged (`../_principles/rubric.md` criterion 4); only its surfacing differs by audience.

## §3 · Report — a blog, scoped to a specific portfolio / client / region / purpose

Same format family and structural moves as the blog (§2); the difference is **targeting**. A report answers "what does this mean for **this** portfolio / account / region?" rather than the market broadly, so it leads with the specific entities and narrows the mechanism + caveats to them.

- **Tags it tends to carry**: `bottom_up` (asset/portfolio-anchored) and/or `client` audience — but a region- or purpose-scoped report can be a narrowed top-down too.
- **Reuses the blog's moves**, scoped: the entity section is the *target's* assets; the chart is the target's exposure; the caveat is what's unresolved *for them*.
- **Anti-target** (decided): *not a generic plant profile* (available elsewhere, adds nothing), and *no unmodeled "X% loss" figures* — it is an exposure read (mechanism on the target's baseline, actor relevance, caveats), not a forecast.
- **Status**: we have a validated **blog** example, not yet a **report** example — the report form gets cracked alongside the bottom-up work (`../../docs/plans/2026-06-11_layered_reference_v1.md` Phase 5). Build it before its email distillation.

## §4 · Email — the condensed subset

The terse output: a distillation of a validated **blog or report** (§2/§3), not a thing built from scratch. Because it is a subset, it is **built last** — the rich piece must crack the feedback loop first; you can't tell from an email whether the underlying insight is deep.

**GATE PRECONDITION (doubly so): renders only a validated insight, for a named account, after human review of the rendering itself — no send automation, ever** (`../../docs/use_cases.md` activation boundary). Envelope: short (~120–250 words) · one claim, one number with `as_of`, one watch line · DOCX/email-body export from the same brand kit.

---

**See also**: `brand.md` (the anatomy every output renders into), `../_principles/rubric.md` (criterion 1 judges the declared output; criterion-5 voice), `../_principles/voice.md` §4 + `../../docs/principles.md` P6 (these contracts inform, they don't bind), `../_reference/` (external form exemplars + internal golden outputs that *show* the form), `../../docs/use_cases.md` (the buckets these serve).
