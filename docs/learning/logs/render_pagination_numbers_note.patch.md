# Staged patch — `render.md` STEP 4: pagination hygiene + the numbers screen-note

> **Status**: ⏳ **STAGED 2026-06-17** — the two new STEP-4 ship-checks below could not be applied directly this session (`render.md` resolved to a protected path). The supporting canon they point to **is already live** (`../../resources/_style/brand.md` B2 item 4 · `../../resources/_craft/plot_generation.md` §4 · `../../docs/principles.md` P7). Apply these two bullets to `.claude/commands/render.md` (and the `.cursor` mirror) when the command is next editable. Companion to `2026-06-17_standard_solar_render_polish.md`. Thin-conductor only — points to the canon, restates nothing.

## Edit — STEP 4, add two ship-checks (insert directly BELOW the "No outreach/send automation" bullet)

**ANCHOR (insert after this existing line):**

```
- **No outreach/send automation** — a render is reviewed by a human before any external use (`../../docs/use_cases.md` activation boundary).
```

**INSERT (two new bullets, immediately below the anchor):**

```
- **Pagination & whitespace, on any paginated format** (`../../resources/_style/brand.md` B2). Don't ship a DOCX/PDF/deck that **ends on a near-empty page**; tighten or balance so the tail lands on the prior page, or the final page is **≥ half full**, and keep figures with their captions / heads with their first line. This only shows once paginated, so **render to PDF and eyeball the last page before shipping**.
- **Numbers carry the screen-note** (`../../resources/_craft/plot_generation.md` §4 · `../../docs/principles.md` P7). Wherever a capacity/CF/quantitative figure or an exact number appears, include the standing **"approximate, directional screen — contact the InfraSure team for asset/portfolio detail"** note. It manages the precision the plot implies and is the forward door on the numbers — load-bearing whenever the piece leans on capacity/CF plots.
```

## Apply / verify

```text
1. Add the two bullets above to .claude/commands/render.md (and .cursor/commands/render.md).
2. Sanity: STEP 4 now ends with pagination + numbers-note checks, after the no-send bullet.
3. Re-render any studio brief to DOCX; confirm (a) no orphan near-empty final page, (b) the
   capacity/CF figures carry the approximate/contact-InfraSure note.
```

## See also

`2026-06-17_standard_solar_render_polish.md` (the lesson), `render_audience_strip.patch.md` / `render_command.patch.md` (same staging convention), `../../resources/_style/brand.md` B2 (pagination rule), `../../resources/_craft/plot_generation.md` §4 (the numbers screen-note), `../../docs/principles.md` P7.
