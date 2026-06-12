# Prompt Exemplar 001 — The Blog Messaging That Cracked Top-Down

> **Status**: intake 2026-06-12 · **prompt exemplar** — the second reference kind: not a piece to imitate, but the *messaging that traveled with the references* and produced the strong day-one top-down output (collab thread, 2026-06-09/11).
>
> **Provenance**: Divy, manual prompting during the first ENSO blog iterations (claude.ai project, June 2026). Captured verbatim below.
>
> **Why it is here**: process data (`docs/08` P3). The point of the layered reference is that these moves stop being manual — each move below is either **absorbed** into a shared layer (so no session needs to type it again) or marked **session-time** (legitimately per-run). When a future prompt works well, capture it here the same way.

## The Prompt (verbatim)

```text
Act as an industry expert on ENSO/solar energy writing a blog on this year's ENSO and its
impact on CAISO/CA solar power. Create a blog article with the above insights that:
Display:
1) Adds a catchy title (via alliteration, idiom, hyperbole, or some other rhetorical device)
2) Includes a longer, informative subtitle detailing the contents of your research and what
   the blog article will include (i.e: A look at the current state of three major hyperscale
   data center projects across the US, where they fit... - this subtitle will be completed and
   displayed under the title once the user clicks on the article)
3) Date posted (i.e 5 June 2026) Day Month Year Format
4) Estimated Read Time (10 minute read)
5) A one-word header above the title describing the energy type or topic that this will cover
   (i.e "ENSO" or "Solar")
Article Writing:
1) Experiment with your format but be sure to have an introductory paragraph with background
   on ENSO and solar
2) Include historical examples (of ENSO // Solar) where relevant events occurred (i.e your
   source references are based on these examples)
3) Generate relevant graphs and charts whenever statistics emerge
4) Concluding paragraph detailing the importance of our insights
For reference:
https://blog.gridstatus.io/tag/ercot/  Grid Status Exports  ERCOT - Grid Status Exports
```

## Where Each Move Lives Now

| Move (from the prompt) | Absorbed into | Note |
|---|---|---|
| "Act as an industry expert…" | `_principles/voice.md` §1 (the analyst voice) | persona line no longer typed per session |
| Catchy title via rhetorical device | blog cell move 1 (`_style/output_contracts.md` §3) | devices welcome in the *title*; **hyperbole never lands on a claim** (`voice.md` §3) — playful words, honest numbers |
| Longer, informative subtitle (what the piece covers) | blog cell move 1 (the dek spec) | the Grid Status dek pattern (see `../exemplars/`) |
| Date posted, Day Month Year | `_style` skeleton meta line | "12 June 2026" format |
| Estimated read time | `_style` skeleton meta line | computed from length band |
| One-word topic kicker above the title | `_style` skeleton title block | "ENSO" · "Solar" — distinct from the header's doc-type kicker |
| Intro paragraph with background | blog cell move 3 (condition + background) | background ≤ 1 paragraph; framed, never the grounding |
| Historical examples carrying the source refs | blog cell move 5a (NEW — the historical-anchor move) | each example cites its own dated source; history is evidence, not decoration |
| Charts whenever statistics emerge | `_craft/plot_generation.md` §0 + blog cell move 6 | already law: a chart at every statistic, grounded per series |
| Concluding paragraph on why the insights matter | blog cell move 8 | the zoom-out close (see curtailment exemplar lesson 6) |
| "For reference: gridstatus…" | this corpus (`../exemplars/`) | references ride in the reference layer, not in prompts |

**Still session-time (correctly)**: the topic and scope ("this year's ENSO · CAISO/CA solar"), the declared contract tuple, and any per-run emphasis. That is the anti-microprompting line (`voice.md` §4): direction + references + constraints are baked; the *ask* stays free.

---

**See also**: `../README.md` (intake protocol — prompt exemplars follow it too), `../../_style/output_contracts.md` §3 (the cell these moves landed in), `../../../docs/05_mcp_test_protocol.md` (Session Capture — where future prompting moves get extracted from transcripts).
