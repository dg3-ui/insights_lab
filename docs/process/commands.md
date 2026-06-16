# Commands — The Toolchain That Cranks the Loop

> **Status**: command-design canon, 2026-06-13 (was `10_command_roadmap`; the volatile build-status registry split out to `../status/commands.md`).
>
> **Purpose**: the command/skill toolchain that makes the resource lifecycle + the two feedback loops **crank-able** — each stage that today happens by hand inside a session becomes a thin, repeatable conductor over the canon. This doc owns the *design* (what the stages are, the rule every command obeys); the *build status* of each command lives in `../status/commands.md`.

## The Lifecycle (each stage is a command)

```text
   AUTHOR ───► TEST ───► RESOLVE ───► GATE ───► RENDER          (+ maintain)
  /new-resource /test-resource /extract  /gate-check /render

   feedback loops these commands feed:
     TEST ─► RESOLVE   = the PROCESS loop   (transcript → test_run + extraction)   principles.md P3
     any stage ─► the ledger = the TOOL-SURFACE loop  (gap · workaround · roadmap)  learning/01
     out-of-loop feedback ─► /intake-feedback  (triage → routed homes + log)        process/test_protocol.md §intake
```

The canon each command conducts is `method/` + `process/` + `principles.md`; the current per-command status is `../status/commands.md`.

## Why Tier 1 First

`/test-resource` + `/extract` complete the **iteration-and-process-data loop** — the thing the lab cares most about (`../principles.md` P3/P4) — and pair naturally with `/new-resource` to give `author → test → resolve` as one crank. `/extract` is specifically the *missing half* of "save the chat": without it, transcripts accumulate unresolved (the swamp P3 warns against).

## Tier 2 — `/render` is built; `/gate-check` is next

- **`/render`** (BUILT — `.claude/commands/render.md`) is the **content engine** (`../architecture.md` Layer 3): a **P6-first thin conductor** that renders a **gated studio brief → blog / report / email + grounded charts/maps**, where the model generates the artifact itself (its own SVG/HTML/generator — `_craft`). It consumes the render-side shared layers — `_style` (brand + the three-output contract), `_craft` (grounded plots/maps), `_reference` (form, not facts) — treats them as **stepping-stones not a checklist** (P6), and refuses to render where no validated insight exists upstream (`../principles.md` P2).
- **`/gate-check`** (the remaining Tier-2 item) patches a known weakness: `../architecture.md` §7 admits the v0 gate is *self-policing* (the same session that drafts also judges). Running validation as a separate command in a fresh context is the cheapest way to get an *independent* check without building production enforcement. It is also where the rubric's **accuracy** criterion is judged independently (`../../resources/_principles/rubric.md` §2 — style self-critique stays in-session; accuracy never).

## Design Rule (so the toolchain doesn't become rigidity)

```text
every command is a THIN CONDUCTOR over the canon — it points, it does not restate
                  MODEL-AGNOSTIC — improves prompts/evals/process, never bets on one model (P1)
                  ENDS AT A HUMAN CHECKPOINT — where judgment matters, it stops (P4)
```

Commands are the right home for workflow meta-tools. `/render` and `/gate-check` are the two that could later graduate into installable **skills** for reuse across repos.

---

**See also**: `.claude/commands/` (the commands themselves), `../status/commands.md` (per-command build status), `test_protocol.md` (what `/test-resource` + `/extract` conduct), `../principles.md` (P3/P4 the loop commands serve), `../status/mcp_gaps.md` (the tool-surface ledger), `../architecture.md` §7 (the gate + content engine Tier 2 targets).
