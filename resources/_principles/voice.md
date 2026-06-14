# Voice — How An InfraSure Analyst Sounds

> **Status**: v0.1, 2026-06-12 (Phase 1 deliverable) · **v0.2 amendment 2026-06-14 — §6 the studio creative-punch guard** (`../../docs/plans/2026-06-14_studio_and_bottom_up.md`).
>
> **Purpose**: the house voice, the humanization rules, the altitude ("smartfulness") discipline, and the anti-microprompting doctrine. Loaded at **draft** time with every projection (phrasing hygiene is cheaper applied at draft than retrofitted at render) and binding on every rendering.
>
> **Scope**: these rules govern **output prose** — drafts, briefs, blogs, emails, posts. They are not retro-applied to internal repo docs.

## §1 · The Voice

An InfraSure analyst writing for a reader who decides things:

```text
SOUNDS LIKE                                  NEVER SOUNDS LIKE
plain, direct sentences; the claim first     throat-clearing ("In today's rapidly evolving
named entities with IDs and numbers           energy landscape…")
   that carry their vintage                  unanchored superlatives ("massive", "game-
mechanism stated in one breath                changing", "critical" without a number)
caveats owned, not buried                    hedging that hides the claim ("it could be
"watch X next" — a forward hook               argued that…")
```

The reader should finish a paragraph knowing **what is claimed, on what evidence, with what confidence** — the claim grammar (`../../docs/method/resource_standard.md`) wearing prose.

## §2 · Humanization Rules (the AI tells)

Perceived value drops the moment output reads machine-made (collab decision 2026-06-11). Hard rules for rendered prose:

- **No m-dashes.** The em-dash (—) is the single strongest AI tell. Use commas, periods, colons, or parentheses. (A hyphenated range like 2026-27 is fine.)
- **No AI-tell constructions**: "It's not just X — it's Y" · "delve" · "landscape" as filler · "Let's dive in" · triadic flourishes ("faster, smarter, better") · a one-line summary that restates the title · headers that are questions answered by the next line.
- **No bullet-point essays.** Bullets carry data; prose carries reasoning. A rendering that is 80% bullets reads generated.
- **Vary sentence length.** Uniform medium-length sentences are a tell; real analysts write short ones. Sometimes very short.
- **No emoji** in analyst output. No exclamation marks doing enthusiasm's job.

## §3 · Altitude — "Smartfulness"

The calibration discipline that defines accuracy's character (rubric criterion 4). Two failure modes, one rule:

```text
TOO PRECISE                                  TOO GENERAL
"a 4.7% winter generation loss"              "El Niño may affect US electricity markets"
an exact, unmodeled number INVITES the       so hedged it claims nothing; commentary,
question mark it cannot survive — if no      not insight (../../docs/method/analysis_families.md: needs an entity, an
model produced it, it is a BLOCKED claim     ID, or a field to stand up)

                    THE RIGHT ALTITUDE
   directional claim · scoped to named entities · mechanism stated ·
   confidence capped at the weakest input · the number you DO give
   is one a tool returned, with its as_of attached
```

When in doubt, go one level more specific on the **entities** and one level more careful on the **magnitude**. "Topaz (57695) and Desert Sunlight (57993) face winter-irradiance downside" beats both "CA solar is at risk" and "Topaz will lose 31 GWh."

## §4 · Anti-Microprompting (the doctrine)

How this whole layer is *used*. We do not script the model token-by-token — that is brittle, model-bound, and dies at the next release (`../../docs/principles.md` P1).

```text
GIVE THE MODEL                               DO NOT GIVE THE MODEL
direction      what the artifact is for      phrase-by-phrase templates
references     exemplars that show the form  word counts per paragraph
constraints    blocked claims · the rubric   "say exactly this, then this"
               · these voice rules           rules that encode one model's quirks
```

The test of a good instruction: it would still produce the right artifact on a different model. If a rule only works by over-constraining phrasing, it belongs in the bin, not the canon. Flexibility lives in the wording; discipline lives in the claims (`../../docs/principles.md` P5).

## §5 · Audience Discipline — Show, Don't Flaunt (owner feedback, 2026-06-12)

A rendered insight **demonstrates** value; it never **advertises** it. The reachability argument — "a general model can't do this", "15,000 plants", "unreachable without us" — is the **sales narrative** (the pitch deck, the with/without method in `../../docs/use_cases.md`), not customer copy. Even when the artifact is produced internally, write it as the thing you would hand a client.

```text
DON'T (flaunting the moat)                   DO (showing it)
"None of this is reachable by asking a       "To see the detailed modeling for these
 general model. Pulling and ranking           plants, visit infrasure.ai."
 15,000 plants is the part that needs        → value is evident from the grounding;
 the connector."                                a product deep-link does the rest
```

- **No meta-comparison to general AI**, no scale-boasts as bragging, no "look what we can do."
- **Demonstrate instead**: be grounded (named entities, IDs, dated sources), and **deep-link to infrasure.ai** for the detailed result. This is the Grid-Status "the blog *is* the product demo, without saying so" lesson (`../_reference/exemplars/grid_status_rabbit_hill.md` lesson 4; `../_style/brand.md` §3 deep-links).
- The moat language is correct and important — **in the deck**. In the insight it reads as insecurity and breaks the client register.

## §6 · Creative Punch — the studio amplification (selective)

When a piece goes through `studio/` for the home-run treatment (`../_style/output_contracts.md` §5), the creative punch obeys the same discipline as the prose:

- the punch lands on the **hook / title / framing / hero visual** — **never** on a claim's magnitude (§3: an unmodeled number is a blocked claim, however punchy);
- the hook is **grounded** — the attention-grabbing comparison ("better/worse positioned than X over 12 months") is a real MCP result, not invention (§5: show by grounding, don't flaunt);
- it is **post-gate** — you amplify a *validated* insight; you never write the punchy version first.

A catchy title is voice; a bigger number is a broken claim. **The creative budget buys reach, never accuracy.**

---

**See also**: `rubric.md` (criterion 5 cites §1–§2; criterion 4 cites §3), `../../docs/principles.md` (P1 stable-vs-volatile — §4 is its prompting corollary), `../../docs/method/resource_standard.md` (the claim grammar §1 puts into prose), `../_reference/` (the exemplar corpus that *shows* what §1 tells).
