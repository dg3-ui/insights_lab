# Task Context — Output-Layer Architecture: Confidence Model, Studio, /render

> **Status**: COMPLETE (pushed to `origin/main`, commits `af394d7` → `d326654`). 2026-06-15. Area: output-layer. The studio briefs are **gated drafts pending the owner checkpoint** (not yet client-shipped).

## Objective

Build the **scalable output-layer architecture** for InfraSure Insights — owner-directed: *"do tight things for a scalable system, not small patch fixes; whatever's right for the long term."* Stand up a confidence foundation, a subject-keyed render layer, a triage layer, and the `/render` conductor — then make the front-door docs reflect it.

## Background

The output half (`studio/`) existed only as **flat briefs** (2026-06-14). A 4-lens design review flagged it as not-yet-scalable: confidence was conflated into one axis, the grade sat on the rendered face, there was no single source of truth, triage was implied but unbuilt, and an unresolvable entity ("Anten") was keyed as an account it couldn't resolve to. The owner chose to build the **right long-term shape** rather than patch.

## Problems we were solving

1. **"Confidence: LOW" miscommunicates** — it reads as *low quality* when it means *we're not asserting a number you'd hold us to*. Three different things (the event's probability, our calibration cap, the stake) were collapsed into one badge.
2. **The grade leaked onto the rendered (client-facing) face.**
3. **No single source of truth** — a grade restated in multiple places drifts.
4. **No prioritization surface** — nothing ranked "across everything we've gated, what matters first?"
5. **An unresolvable entity** ("Anten") had no honest home.
6. **Maps/plots were specced in prose but never produced** — no render conductor.
7. **Over-constraining the model** — the owner's core concern: don't curtail the model's capability with rigid templates; guide, don't force.
8. **Doc drift** — the front-door architecture/flow docs still taught the pre-session output model.

## What we built (in order)

1. **Confidence foundation** — `docs/method/confidence_model.md` (NEW): confidence is **three axes** — calibration cap (internal grade) · event likelihood (sourced, on output) · materiality (exposed-share × class-severity band, internal, tie-breaker). Posture + event + settledness render; the grade never does. Per-part confidence; `render-internal ≠ host-private`.
2. **Render layer** — folded `studio/` to `studio/<subject>/<phenomenon>.md`; each §1 gate-record is the single source of truth. Brookfield/Standard Solar (account) + Galveston Bay corridor (region — the honest home for "Anten").
3. **Triage layer** — `studio/_triage.md`: one internal cross-subject board, cap × materiality → ACT/WATCH/NOISE, never rendered.
4. **New phenomena, MCP-grounded** — `hail.md` (0 MW in the US hail maximum; CO/MN/IL/NM exposure) and `extreme_heat.md` (a modest derate, NOISE for a fixed-price book) on the Brookfield subject; **offtaker confirmed BLOCKED** (R13). A multi-phenomenon **subject guide** (`brookfield_standard_solar/README.md`).
5. **Direction + scope ladder** — `direction` (top_down/bottom_up) is a **meta-tag, not a folder**; subject = a scope ladder (account → region → market/fleet).
6. **Origination norm** — studio-first for the OUTPUT artifact (the insight is still gated upstream); bottom_up before top_down.
7. **P6 sharpened** — references inform the *analysis*, not just form; covers studio; the differentiator; **the model is the renderer** (writes its own SVG/HTML/generators).
8. **`/render` built** — `.claude/commands/render.md` (Tier-2): a P6-first thin conductor, gated brief → blog/report/email + grounded charts/maps. Demoed with a real **hail US statebin map** (HTML+SVG).
9. **Docs sync** — front-door architecture/flow docs (architecture.md, CLAUDE.md, docs/README, use_cases, commands, test_protocol, README, AGENTS, resources READMEs) updated to reflect all of the above.

## Files touched

```text
CREATED
  docs/method/confidence_model.md                         the 3-axis keystone
  docs/plans/2026-06-15_output_layer_architecture.md      the architecture record
  studio/_triage.md                                       the cross-subject triage board
  studio/brookfield_standard_solar/{README,el_nino_enso,hail,extreme_heat}.md
  studio/galveston_ship_channel_surge/storm_surge.md      (folded from anten_ports.md)
  studio/brookfield_standard_solar/_renders/hail_us_statebin.html   the demo map artifact
  .claude/commands/render.md                              the /render conductor
  docs/extra/tasks_history/** (this)
MODIFIED (method/principles/contracts)
  docs/method/resource_standard.md (Confidence Rules → 3 axes + materiality basis)
  docs/principles.md (P6 sharpened) · resources/_principles/{voice,rubric}.md
  resources/_style/{output_contracts,brand,README}.md · resources/_craft/plot_generation.md
  resources/weather_and_climate/el_nino_enso/resource.yml (confidence_rules annotated; v0.0.2)
  docs/status/{commands,mcp_gaps}.md
MODIFIED (front-door docs sync)
  docs/architecture.md · CLAUDE.md · docs/README.md · docs/use_cases.md
  docs/process/{commands,test_protocol}.md · README.md · AGENTS.md
  resources/README.md · resources/_reference/README.md
DELETED
  studio/brookfield_standard_solar.md · studio/anten_ports.md (folded) · studio.zip (stray)
```

## Current status (acceptance)

- [x] Confidence model is canon + bound across resource_standard, rubric, output_contracts, brand, voice, architecture, the resource seam, docs README.
- [x] Studio = foundation + render + triage + gallery; subject-keyed; direction as meta-tag.
- [x] Two new phenomena MCP-grounded (hail, heat); offtaker honestly blocked (R13).
- [x] `/render` built + demoed with a real map; the model-is-renderer principle explicit.
- [x] Front-door docs synced + verified (no stale labels; all six reference confidence_model/studio/render).
- [x] Verified by 4 workflows (2 adversarial + 1 confirmation + 1 audit); all findings reconciled.
- [ ] **Owner checkpoint** on the 4 studio briefs (gated drafts) — not yet done.
- [ ] **Re-ground** before any external use (numbers are 2026-06-15 MCP snapshots).

## Next steps

See `handoff.md` → Next action. In short: owner-review the briefs; render the remaining hero visuals via `/render`; resolve the offtaker gap (R13); consider a first top_down market piece; build `/gate-check`.
