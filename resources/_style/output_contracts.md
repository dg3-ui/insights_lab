# Output Contracts — direction × audience × format

> **Status**: v0.1, 2026-06-12 (Phase 2 deliverable; D7/D11 of the active plan). Filled: 2 cells + 1 variant. Stubs fill in Phase 5.
>
> **What a contract is**: the **envelope** a rendering must fit — length band · tone · rendering target · what NOT to include · the gate guard. **Inner structure flexes by analysis family and granularity** (D11): the method package and family-tagged exemplars resolve the inside; the cell fixes the outside. No microprompting (`_principles/voice.md` §4).
>
> **THE GATE PRECONDITION — stamped on every cell, no exceptions**: a contract renders **only a validated insight** — one that has passed the `../../docs/process/test_protocol.md` gate with its `review_trace` complete. Rendering before the gate is the `../../docs/principles.md` P2 violation; `/render` must refuse it.

## §1 · The Key

```text
direction:  top_down (phenomenon → assets)  ·  bottom_up (asset/portfolio → phenomenon)
            — the ../../docs/method/analysis_families.md §Exposure axis verbatim; one axis across analysis_families/use_cases/_style
audience:   internal  ·  client (a named account)  ·  public
format:     report  ·  vlog  ·  email      ← the three output TYPES (a set, not a sequence)
```

**The three outputs:**
- **report** — the specialized, rich, long-form analysis (internal, client, or public; a *public* report is what gets published as a blog post). The RICH format.
- **vlog** — a narrated version of a report (script + delivery). Also rich.
- **email** — a terse, targeted distillation for a named lead. The LEAN format.

(Old vocabulary maps in: "brief" = a short report · "blog" = a public report · "post"/`platform_card` = a delivery *channel* for a report, not a separate output type · `account_note`/`portfolio_note` = a client report · `informative_email_draft` = **email**.)

**Build order ≠ delivery order** (do not conflate — this is the load-bearing distinction):

```text
BUILD ORDER (how we develop + validate the engine)
   report / vlog  FIRST   ──►  email  LAST
   the RICH formats create the richest feedback loop: iterating a report or vlog shows
   whether the insight is deep and well-grounded. You cannot judge insight-richness from a
   terse email, so email is the WRONG place to start the loop — it is the final, distilled
   output, built once the engine is proven on the rich formats.

DELIVERY ORDER (which output ships when, to whom)
   a SEPARATE business question, NOT settled here, and NOT the build order — do not conflate.
```

**Declaring**: the session names its tuple at test/render start — one line, e.g. `contract: top_down × internal × report`. Naming the tuple is a pre-test checklist item (`../../docs/process/test_protocol.md`); *loading* this file stays post-gate.

## §2 · The Matrix

Columns are ordered by **build priority** (report/vlog first, email last — §1); they are output *types*, not a delivery sequence.

| direction × audience | report | vlog | email |
|---|---|---|---|
| **top_down × public** | **§3 FILLED** (public report; publishable as a blog post) | variant of §3 (narrated) | ✗ (no un-gated mass email; client-only) |
| **top_down × internal** | **§4 FILLED** (internal report) | **§4 vlog variant** | — |
| **bottom_up × internal** | **§5 STUB** (fills Phase 5 — the feedback-loop anchor) | variant of §5 | — |
| **bottom_up × client** | client report (feeds §6) | variant | **§6 STUB** (the lean distillation — built LAST) |

Unlisted combinations derive from the nearest filled cell under the same envelope rules; if none fits, that is a new cell (version-bumped), not an improvisation.

## §3 · `top_down × public × report` — FILLED (the cracked structure; a public report, publishable as a blog post)

What made the day-one top-down work, codified: references + structure (the Grid Status form — `_reference/exemplars/`; the messaging that produced it — `_reference/prompts/blog_messaging_001.md`).

| Envelope | Value |
|---|---|
| Rendering | HTML artifact (`brand_assets/artifact_skeleton.html`); DOCX export on request |
| Display | topic kicker (one word, above the title: "ENSO" · "Solar") · date posted, Day Month Year ("12 June 2026") · estimated read time |
| Length | 800–1,400 words · 1–2 grounded charts |
| Tone | `voice.md` §1–§2 — analyst-direct, human, zero AI tells; section heads may carry personality, the prose under them stays precise (4CP exemplar, lesson 2) |
| Gate guard | **validated insight only**; every number in the piece traces to the insight's `source_refs` |

Structure (the moves, in order):

```text
0 DISPLAY    topic kicker · date (Day Month Year) · read time   (the title block, brand.md §4)
1 TITLE      catchy via rhetorical device (alliteration · idiom · tension · a number) —
   + DEK     playful words, honest numbers: hyperbole NEVER lands on a claim (voice.md §3)
             dek = informative subtitle, 1–2 sentences: what the piece covers + why now
             "El Niño Is Coming for California's Winter Solar. Here's Who Is Exposed."
2 SUMMARY    3–4 takeaway bullets + a CALIBRATION CUE   (the TL;DR box, brand.md §4)
             (posture: forward · directional) — NEVER a pejorative "LOW confidence" stamp
3 CONDITION  what changed — the external state, dated;  NOAA El Niño Watch, ~96% DJF, as_of
             + ≤1 background paragraph (frames, never grounds)
4 EXPOSED    WHO / WHERE — named entities, IDs, MW,     the entity table + the spatial figure;
             owners, region                             granularity per scope
5 MECHANISM  one breath, first-principles PROSE         condition → irradiance → the already-low
                                                         winter the fleet can least afford to lose
5a HISTORY   the historical-anchor move: dated past     each episode carries its own source ref;
             episodes as evidence where they exist      history is evidence, not decoration
6 CHART(s)   grounded series, FLEET/REGION scope for    (_craft rules); spatial when geography IS
             top-down (NEVER a single-plant chart),     the story; charts + entity mentions DEEP-LINK
             caption+source+as_of below                 to infrasure.ai pages where they exist
7 CAVEAT     the honest caveat, woven or ONE box: what  CONFIDENT, NOT a "we are not saying X"
             is still resolving + what would change     negation list (if we wouldn't say it, we
             the read                                    just don't); amber left-border, brand §4
8 WATCH      forward hook — what resolves when          strength firms over summer/fall
9 CONCLUDE   zoom out: why these insights matter —      no triumphant summary; the curtailment
   + FOOTER  then sources + as_of register · brand line exemplar's close (lesson 6) + brand.md §4
```

Not-include: price/LMP forecasts · plant-level production forecasts · outreach CTAs · unscoped national claims · exemplar-derived facts · **internal-taxonomy labels** (the bucket name, "top-down exposure brief" — the artifact is reader-facing; the kicker names a topic, never our categorization) · **moat / meta-pitch language** ("unreachable without a general model", "15,000 plants" as a boast) — that is the sales narrative (`../../docs/use_cases.md`), not reader copy (`../_principles/voice.md` §5: show, don't flaunt). Family/granularity notes: exposure pieces lead with the entity table + the spatial view; event-translation pieces lead with the event (the Rabbit Hill drill trajectory — `_reference/exemplars/grid_status_rabbit_hill.md`); single-region scope keeps one table, multi-region gets one per region — depth flexes, the moves do not.

**Show value, don't announce it (owner feedback, 2026-06-12).** Where a draft is tempted to brag about reach ("none of this is reachable by a general model"), the client/public cell instead carries a **product deep-link** — e.g. "the detailed modeling for these plants is at infrasure.ai" (move 6, the Grid-Status product-demo move; `brand.md` §3 deep-links). The grounding proves the value; the link routes the reader to the platform; the moat argument stays in the deck (`../_principles/voice.md` §5).

**Confidence display, public vs internal (added 2026-06-12, owner feedback).** A public rendering conveys calibration as *analytical posture* ("a forward, directional read on the season ahead"), carried by precise grounding and the honest caveat. It does **not** print a self-deprecating "Confidence: LOW" badge or a "we make no forecast" disclaimer: both undercut the work and InfraSure's image, and neither is the purpose of the piece. The discipline (no magnitude, no $/MWh, no plant-level forecast) is honored by *not writing those claims*, plus the caveat that names what is still resolving. The **internal report (§4) keeps the explicit confidence line** — the decider needs the label; the public reader needs the posture. The gate's LOW/directional verdict underneath is unchanged (`../_principles/rubric.md` criterion 4); only its surfacing differs by audience.

## §4 · `top_down × internal × report` — FILLED (short internal report)

| Envelope | Value |
|---|---|
| Rendering | markdown-first (it IS the insight, condensed); HTML artifact optional |
| Length | 300–600 words, tables over prose |
| Tone | terse analyst register; caveats inline, not performative |
| Gate guard | **validated insight only** |

Structure: claim (one paragraph) → scope table (entities · IDs · MW) → mechanism (one line) → confidence + caveats (the table from the insight) → actor relevance → watch next. It is the 9-section skeleton compressed for a reader who decides — nothing added, only condensed.

**Vlog variant (the internal narration script)**: ~60–90 seconds spoken (≈150–220 words) · spoken register (numbers rounded as said aloud: "about thirty-seven gigawatts") · structure: hook → condition → who's exposed → the one caveat that matters → watch line · no charts; sources land on an end-card list. The video itself is out of scope; the contract covers the script.

## §5 · `bottom_up × internal × report` — STUB (fills Phase 5 — the feedback-loop anchor, built FIRST)

Anchor: **one asset or one portfolio** → its exposure to the phenomenon. This is the **rich** bottom-up output, and it is built **first** (per §1 build order) — it is where the bottom-up feedback loop actually cracks (you can see whether the insight is deep). Envelope (provisional): markdown · 300–600 words · the asset's numbers from the substrate with `as_of`. **Anti-target (already decided)**: *not a generic plant profile* (available elsewhere, adds nothing) and *no unmodeled "X% loss" figures* — exposure read: mechanism on THIS asset's seasonal baseline, actor relevance, caveats. Filled by the Phase-5 iterate-and-compare runs; until then this cell does not render.

## §6 · `bottom_up × client × email` — STUB (built LAST — the lean distillation of §5's report)

The terse client output. **Built last, not first** (§1 build order): it is a distillation of the validated bottom-up *report* (§5), so the report must crack the feedback loop before this is meaningful. **GATE PRECONDITION (doubly so): renders only a validated insight, for a named account, after human review of the rendering itself — no send automation, ever** (`../../docs/use_cases.md` activation track). Envelope (provisional): short (120–250 words) · one claim, one number with `as_of`, one watch line · DOCX/email-body export from the same brand kit.

---

**See also**: `brand.md` (the anatomy every cell renders into), `../_principles/rubric.md` (criterion 1 judges against the declared cell; stage-2 self-critique checks it), `../_reference/` (the exemplars that teach each cell's form — Phase 4), `templates/output_contract.template.md` (adding a cell), `../../docs/use_cases.md` (the bucket × audience grid this operationalizes).
