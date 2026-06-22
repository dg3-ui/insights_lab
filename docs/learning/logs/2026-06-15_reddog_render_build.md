# Log — Red Dog report render build (2026-06-15)

> **Status**: process-capture (`../../principles.md` P3). A `/render` of the Red Dog bottom-up read to a Teck-facing **report · docx**. Captured because the first pass shipped text-only slop and had to be rebuilt against the studio brief.

## The headline lesson

**A report/blog render that ships as text-only is a FAIL, even when every claim is faithfully preserved.** The first DOCX was clean, on-brand, and claim-perfect, and it was still the wrong deliverable: no hero visual, no grounded charts, the data trapped in monospace ASCII boxes. It read like an internal working doc, not something you hand to a counterparty. Fidelity is the floor, not the bar. The render contract (STEP 3) and `_craft` §5 both say *the model is the renderer* and *produce the §3 visuals* — skipping that is the single biggest miss.

**Second lesson: render the studio brief, not the bare prose file.** The prose report (`../../extra/reddog_bottom_up_report_2026-06.md`) is the un-amplified §1 record. The shareable deliverable is specified in `studio/red_dog_mine/arctic_climate_risk.md` §3 — the hook, the two hero visuals, the punchline, the posture line, the forward door. Rendering the prose file alone is why the visuals went missing. The report's own line-3 banner now redirects there; honor it.

## Fail → fix pairs (each routed to its home)

```text
FAIL (first pass)                                  FIX → where it now lives
─────────────────────────────────────             ───────────────────────────────────────
text-only render; no hero, no charts               build the §3 hero visuals + grounded     → render.md STEP 3 (made
  (ASCII boxes copied as monospace)                  charts; the model authors them            non-optional); _craft §5
rendered the bare prose file                       render the STUDIO BRIEF when one exists   → render.md STEP 0
  → §3 visual specs never seen                        (it carries the §3 hero-visual specs)
ASCII data boxes shipped verbatim                  styled 2-col tables (asset screen, the    → (craft habit) tables/figures
                                                     decision frame, the gaps, sources)         beat monospace for share-out
no posture / calibration cue on the face           posture line + ~4× event likelihood in    → brand §A4, output_contracts §3
                                                     the summary; grade stays internal
no forward-door caveat box                          amber caveat box: phenomenon caveat +     → brand §A4, voice §5 (P7)
                                                     "the per-asset layer is where we go deeper"
```

## What carried over correctly (keep doing)

```text
· prose font named a GUARANTEED SANS (Arial) for the DOCX path — never serif (brand §B2, the ENSO lesson held)
· running header (rasterized lockup PNG) + kicker + footer; figure = bordered, caption-below w/ source + as_of
· every chart plotted ONLY numbers already in the gated read, captioned to the report's own sources
· zinc guidance drawn as a LABELED RANGE (projection), not a continued line — no extrapolated tail (_craft §2/§3)
· "research-grounded; not InfraSure MCP / model-gpr" label preserved verbatim; cap grade + materiality stayed internal
```

## Tool-env correction (feeds `../../status/mcp_gaps.md` R7/R10)

`render.md` STEP 3 asserts "this sandbox has no matplotlib (verified 2026-06-15)". **Not true in this session** — matplotlib 3.10.9 is present and produced the four charts as PNGs; `cairosvg` rasterized the hand-authored hero SVGs. The env note was stale and nearly cost the charts. Inline-SVG remains primary for HTML; for **DOCX**, matplotlib-PNG + cairosvg-from-SVG is the reliable raster path.

**The three `render.md` edits below are staged, not applied** — `.claude/commands/render.md` is a protected path this session (the operator applies the patch in `render_command.patch.md`, beside this log):
1. STEP 0 — *if a studio brief exists for a bare prose read, render the brief* (it carries the §3 visual specs).
2. STEP 3 — *a report/blog render that ships text-only is a FAIL*; the §3 hero visuals + grounded charts are non-optional, the model authors them.
3. STEP 3 — correct the stale "no matplotlib" note (matplotlib + cairosvg available; PNG is the reliable DOCX raster path, inline-SVG primary for HTML).

## See also

`../../process/commands.md` (the `/render` design), `../../../resources/_craft/plot_generation.md` (the plot-as-claims rules these charts obey), `../../../studio/red_dog_mine/arctic_climate_risk.md` (the brief that specified the visuals), `2026-06-12_enso_render_build.md` (the prior render build + the serif/posture lessons this one reused).
