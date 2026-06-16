---
description: Render a VALIDATED studio brief / applied insight into a deliverable (blog · report · email) with grounded charts/maps — the Layer-3 content engine, post-gate
argument-hint: <path to a gated insight — a test_run applied-insight OR a studio brief, e.g. studio/brookfield_standard_solar/hail.md> [format: html|docx | output: blog|report|email]
---

You are running **`/render`** — the Layer-3 content engine (`../../docs/architecture.md` Layer 3). It turns a **validated, gated insight** into a deliverable: prose in the house voice + brand, with **grounded charts/maps**. It is a **thin conductor** — it points at the canon, it does not restate it.

**Two paths in, same conductor.** The insight can come **straight from the gate** — the **baseline**: a `test_run` / applied-insight object produced by a methodology package + the MCP, **no studio needed** (this is the default, and the whole point — MCP + a package alone yields something useful). **Or** from a `studio/<subject>/<phenomenon>.md` **brief** — the **selective** lane, which adds the §2 grounded hook + §3 creative dressing on top. `/render` handles both; most renders are baseline.

## THE FRAME — the layers are stepping-stones, not a checklist (`../../docs/principles.md` P6)

Read this before anything else. Everything in `resources/` you load here — `_principles/voice`, `_style/brand` + `output_contracts`, `_craft/plot_generation`, `_reference` exemplars — is a **reference, a stepping-stone, NEVER a constraint or an obligation to satisfy.** Use a layer when it improves THIS deliverable; **deviate, restructure, or improve on top when you can do better** — bring your own analytical angle, a sharper structure, the latest information, a point of view the template didn't anticipate. Depth and shape **scale to the topic** — a one-number email and a flagship report do not get the same treatment. Do **not** "fill every section / use every layer" — that is the anti-pattern P6 forbids.

**The only hard floor is the claim-discipline** (it does not flex): grounding + `source_ref`/`as_of`, `blocked_claims`, the gate, confidence as **posture not grade**. Everything above that floor is yours to improve. *Tell yourself, out loud, at the start: here is the scaffold and the grounding — improve on it.*

## GATE PRECONDITION (P2 — refuse otherwise)

`/render` renders **only a validated insight** — one that passed the gate (`../../docs/process/test_protocol.md`; `../../docs/principles.md` P2). If the target has no gated insight (a scaffold, a blocked read, an un-gated draft), **stop**: there is nothing to render. A rendering is never the source of truth.

## STEP 0 — RESOLVE + RE-GROUND

- Parse `$ARGUMENTS`: the source path — a gated **applied-insight** (a `test_run`, the baseline) **or** a **studio brief**; optional `format` (html default · docx), `output` (blog | report | email — else take the source's declared type), and `audience` (internal | client | public — else read the source's `audience` meta-tag; **default to the client-safe cut**: strip on unless `internal` is explicit). `audience` does not change the gate verdict — only what surfaces (STEP 4).
- Open the source. Confirm the insight is **gated** (passed the test_protocol gate; not a scaffold/blocked). Read the **single-source confidence record** — the three axes (the applied-insight's `confidence`, or a studio brief's §1). If it's a **studio brief**, also read its §2 comparison + §3 creative (the amplification the lane adds); a **baseline** insight has neither, and that is expected.
- **Re-ground freshness** (`../../studio/README.md`): substrate numbers are dated snapshots — re-fetch the named entities against the live InfraSure MCP, confirm currency, reconcile drift **before** any number ships externally.

## STEP 1 — LOAD THE LAYERS (P6-flexibly — points, doesn't script)

Pull in only what improves the piece, at the depth the topic warrants:
- `../../resources/_principles/voice.md` — house voice + the no-AI-tells rules (always; phrasing hygiene is cheap at draft).
- `../../resources/_style/output_contracts.md` — the envelope for the chosen output (blog/report/email); a **light envelope, not a cage**.
- `../../resources/_style/brand.md` — Part A design language (binds as *intent*) → render for the target via Part B (HTML/DOCX). Confidence on the face = **posture + event + settledness, never the cap grade** (`../../docs/method/confidence_model.md` §3).
- `../../resources/_craft/plot_generation.md` — **if the piece carries a chart/map** (see STEP 3).
- `../../resources/_reference/` — form exemplars (form, never facts; quarantined from grounding).

## STEP 2 — RENDER THE PROSE

- Render the gated insight into the chosen output, scoped + structured as the topic calls for (the model's judgment, per the FRAME). Posture not grade; the **forward door** replaces any scope-confession (P7). Lead with its sharpest grounded point — the §2 comparison if it's a studio brief, else the insight's own strongest grounded hook.
- Every material number traces to a `source_ref` with `as_of`. Nothing exceeds what the gate passed.

## STEP 3 — PRODUCE THE GROUNDED VISUALS (`_craft`)

If the insight (or a studio brief's §3) calls for a hero visual (or one would help), make it real — spec-first, then draw (`_craft` §5):
- **YOU are the renderer — use your full generation capability (P1/P6 applied to the artifact).** Don't wait for a render tool or a library. **Produce the artifact yourself**: hand-author the inline SVG, write the HTML/CSS directly, or write a small **stdlib generator (Python/JS) and run it** — whatever yields the best-crafted result. A missing library (no matplotlib in this sandbox) is **never a blocker**; the model's own ability to write clean SVG/HTML/code IS the renderer. **Max-utilise it**: correct encodings, the brand palette, a figure that reads in seconds — a genuinely well-made visual, not a stub. Keep a one-off generator **transient** (e.g. `/tmp`) and commit only the rendered **artifact** (the deliverable), not the scaffolding (`CLAUDE.md` no-scripts rail) — unless a generator becomes a reused render helper, which then earns its place.
- **A plot is a set of claims** (`_craft` §0): every series a `source_ref` + `as_of`; bordered figure; caption BELOW names what-it-shows + source + as_of; the chart says nothing the gated insight doesn't (no forecast curve, no unmodeled magnitude — `_craft` §2/§3).
- **Primary path = HTML + inline SVG** in the brand figure slot (`_craft` §5; `brand.md` B1 `artifact_skeleton.html`). **This sandbox has no matplotlib/geopandas/kaleido** (verified 2026-06-15) — so the **HTML/inline-SVG path is the reliable one**; the matplotlib-PNG fallback is unavailable here (a render-env constraint, `../../docs/status/mcp_gaps.md` R7/R10).
- **Maps**: the MCP serves no geometry yet (R10) — use the **statebin tile-grid schematic** (`_craft` §6: each state a rounded square on a fixed grid, filled by the metric, focus state in amber), as hand-authored inline SVG; caption it as a schematic. Use a map **only if geography IS the story**; else a sorted bar is faster (`_craft` §1).

## STEP 4 — GATE + GUARDS BEFORE SHIP

- **Audience strip** (`../../resources/_principles/voice.md` §5 / P7 · `../../resources/_style/output_contracts.md` §2). One gated insight, two faces — the verdict is identical, the surfacing is not. For a **client/public** render, strip the internal-only tells: direction/substrate **meta-tags** (`bottom_up`, `off-substrate`); **grounding-provenance labels** ("research-grounded · not MCP · not model-gpr" — method-talk, not reader copy); **capability/moat sections** ("What InfraSure adds here"); and **internal-artifact critiques** ("the deck missed X" → reframe to the asset). For an **internal/expert** render these may stay (the provenance label is useful, the cap line is allowed per `confidence_model.md` §3a). The rule is **audience-conditional, never "always strip"** — provenance honesty internally becomes a capability-confession on a client face (P7). Phenomenon caveats + the forward door stay on every face.
- **Render-internal** (`confidence_model.md` §7): the cap **grade**, the **materiality band**, the **triage verdict** never appear on the rendered face — independent of repo visibility.
- **Blocked claims/plots** refused (`blocked_claims`; `_craft` §3). **The three guards** (`../../studio/README.md` — they govern any render, doubly in the studio lane): gate-upstream · creative≠overclaim · grounded-hook.
- **No outreach/send automation** — a render is reviewed by a human before any external use (`../../docs/use_cases.md` activation boundary).

---

**Deliverable**: a rendered artifact (HTML default; DOCX on request) carrying the validated insight, the house voice + brand, and grounded visuals — posture on the face, the grade internal, every number traceable. If a tool/render limit bites (no geometry, no matplotlib), log it to `../../docs/status/mcp_gaps.md` and ship the on-canon fallback.

**Reminder (P6)**: the canon you loaded is a stepping-stone. If your judgment produced a better structure, angle, or visual than any layer suggested, that is the command working as intended — the discipline is the floor, the creativity is the point.
