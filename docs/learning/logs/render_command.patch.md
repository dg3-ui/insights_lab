# Staged patch — `.claude/commands/render.md` (apply by hand)

> Captured 2026-06-15 from the Red Dog render build (`2026-06-15_reddog_render_build.md`). The command file is a protected path in the cowork session, so these three edits are staged here for an operator to apply. Each is a thin-conductor tweak, not new canon.

## 1 · STEP 0 — render the brief, not the bare prose file

In **STEP 0 — RESOLVE + RE-GROUND**, after the first bullet (`Parse $ARGUMENTS ...`), add:

```text
- If the target is a bare prose read AND a studio brief exists for it, render the BRIEF. A brief
  carries the §3 hero-visual specs, hook, punchline, posture line, and forward door; the prose file
  is the un-amplified §1 record only. Rendering the prose alone is how the visuals go missing
  (docs/learning/logs/2026-06-15_reddog_render_build.md). Follow any redirect banner the read carries.
```

## 2 · STEP 3 — text-only is a FAIL; visuals are non-optional

At the top of **STEP 3 — PRODUCE THE GROUNDED VISUALS**, before the first bullet, add:

```text
- A report/blog render that ships TEXT-ONLY is a FAIL — even when every claim is faithfully preserved.
  Claim-fidelity is the floor, not the bar. If the source (or its studio brief §3) names a hero visual
  or any figure would help, BUILD IT. ASCII/data boxes from the read become styled tables or real charts,
  not copied monospace. The model is the renderer (P1/P6) — no waiting on a tool.
```

## 3 · STEP 3 — correct the stale matplotlib note

Replace the parenthetical in the "Primary path" bullet:

- **Old**: "This sandbox has no matplotlib/geopandas/kaleido (verified 2026-06-15) — so the HTML/inline-SVG path is the reliable one; the matplotlib-PNG fallback is unavailable here ..."
- **New**: "Inline-SVG is primary for **HTML**. For **DOCX**, matplotlib (3.10.9, verified present 2026-06-15) renders charts to PNG and `cairosvg` rasterizes hand-authored hero SVGs — the reliable raster path for embedding. (geopandas/kaleido still absent — statebin fallback for maps, `_craft` §6.)"

## Why

`render.md` already *says* the model is the renderer and to produce the §3 visuals — the first Red Dog pass still shipped text-only. These edits make the visual step impossible to skip, point the conductor at the brief that holds the specs, and stop the stale env note from scaring off the charts.
