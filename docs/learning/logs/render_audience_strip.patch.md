# Staged patch — `render.md` audience switch + strip guard

> **Status**: ✅ **APPLIED 2026-06-16** — both edits are now live in `.claude/commands/render.md` (applied directly; the repo is private and `render.md` is maintained in-session, so the protected-path staging wasn't needed). Kept as the record of the change. Companion to `2026-06-16_audience_strip_internal_vs_external.md`. Two edits: parse `audience` in STEP 0, add an AUDIENCE-STRIP guard in STEP 4. Thin-conductor only — points to the canon, restates nothing.

## Edit 1 — STEP 0, the `$ARGUMENTS` parse (add audience)

**ANCHOR (current):**

```
- Parse `$ARGUMENTS`: the source path — a gated **applied-insight** (a `test_run`, the baseline) **or** a **studio brief**; optional `format` (html default · docx) and `output` (blog | report | email — else take the source's declared type).
```

**REPLACE WITH:**

```
- Parse `$ARGUMENTS`: the source path — a gated **applied-insight** (a `test_run`, the baseline) **or** a **studio brief**; optional `format` (html default · docx), `output` (blog | report | email — else take the source's declared type), and `audience` (internal | client | public — else read the source's `audience` meta-tag; **default to the client-safe cut**: strip on unless `internal` is explicit). `audience` does not change the gate verdict — only what surfaces (STEP 4).
```

## Edit 2 — STEP 4, add the AUDIENCE-STRIP guard (insert directly ABOVE the Render-internal bullet)

**ANCHOR (insert before this existing line):**

```
- **Render-internal** (`confidence_model.md` §7): the cap **grade**, the **materiality band**, the **triage verdict** never appear on the rendered face — independent of repo visibility.
```

**INSERT (new bullet, immediately above the anchor):**

```
- **Audience strip** (`../../resources/_principles/voice.md` §5 / P7 · `../../resources/_style/output_contracts.md` §2). One gated insight, two faces — the verdict is identical, the surfacing is not. For a **client/public** render, strip the internal-only tells: direction/substrate **meta-tags** (`bottom_up`, `off-substrate`); **grounding-provenance labels** ("research-grounded · not MCP · not model-gpr" — method-talk, not reader copy); **capability/moat sections** ("What InfraSure adds here"); and **internal-artifact critiques** ("the deck missed X" → reframe to the asset). For an **internal/expert** render these may stay (the provenance label is useful, the cap line is allowed per `confidence_model.md` §3a). The rule is **audience-conditional, never "always strip"** — provenance honesty internally becomes a capability-confession on a client face (P7). Phenomenon caveats + the forward door stay on every face.
```

## Apply / verify

```text
1. Make the two edits above in .claude/commands/render.md.
2. Sanity: STEP 0 now parses `audience`; STEP 4 lists the strip ABOVE the render-internal (confidence) bullet.
3. Re-run a client render (e.g. studio/red_dog_mine/arctic_climate_risk.md report docx audience=client)
   and confirm none of the strip-list tells appear on the face; an internal render keeps them.
```

## See also

`2026-06-16_audience_strip_internal_vs_external.md` (the lesson + the full strip table), `render_command.patch.md` (the prior staged render.md edits — same convention), `../../process/commands.md` (the `/render` design).
