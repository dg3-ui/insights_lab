# 10 - Command Roadmap

> **Status**: living roadmap, opened 2026-06-08.
>
> **Purpose**: the command/skill toolchain that makes the resource lifecycle + the two feedback loops **crank-able** — each stage that today happens by hand inside a session becomes a thin, repeatable conductor over the canon. This is the "turn the crank" layer; the canon (`docs/02–09`) is what each command conducts.

## The Lifecycle (each stage is a command)

```text
   AUTHOR ───► TEST ───► RESOLVE ───► GATE ───► RENDER          (+ maintain)
  /new-resource /test-resource /extract  /gate-check /render
     ✅ built     ◑ next       ◑ next     ☐ tier 2   ☐ tier 2

   feedback loops these commands feed:
     TEST ─► RESOLVE   = the PROCESS loop   (transcript → test_run + extraction)   docs/08 P3
     any stage ─► docs/09 ledger = the TOOL-SURFACE loop  (gap · workaround · roadmap)  learning/01
```

Today the chain has its first link (`/new-resource`) and a meta tool (`/recap`). The rest of the chain — turning a resource into a *validated, resolved, rendered* output — is the build path.

## The Registry

```text
TIER   COMMAND          STAGE      WHAT IT DOES (thin conductor over →)              STATUS
────   ───────────────  ─────────  ───────────────────────────────────────────────  ──────
 0     /recap           (meta)     ASCII structural recap + honest friction          ✅ built
 0     /new-resource    AUTHOR     author a methodology package (the ENSO engine)     ✅ built  (docs/02·03·04·05·08)
 1     /test-resource   TEST       run the manual MCP test loop on an existing slug   ◑ next   (docs/05 · P4)
 1     /extract         RESOLVE    transcript → test_run + extraction + ledger        ◑ next   (docs/05 capture · P3)
 1     /log-gap         (loop)     one-line append to docs/09 from anywhere           ☐ cheap  (docs/09)
 1     /intake-feedback (loop)     triage out-of-loop feedback → routed homes + log    ☐ cheap  (docs/05 §intake · template)
 2     /gate-check      GATE       INDEPENDENT validate vs contract + blocked_claims  ☐ tier2  (docs/03·06 §9·_principles)
 2     /render          RENDER     validated insight → blog/brief/email/post per      ☐ tier2  (docs/06 L3 · P2 · _style
                                   the _style contract (direction×audience×format)              · _craft · _reference)
 3     /eval-resource   EVAL       run examples/test_runs + fail→fix as pass/fail      ☐ later  (paused; eat process data first)
 3     /find-methodology DISCOVER  rank resources by taxonomy for a query             ☐ later  (revisit ~10 skills; 07)
 3     /sync-docs       MAINTAIN   house-style + cross-ref + registry consistency      ☐ later  (when drift is real)
```

## Why Tier 1 First

`/test-resource` + `/extract` complete the **iteration-and-process-data loop** — the thing the lab cares most about (`docs/08` P3/P4) — and pair naturally with `/new-resource` to give `author → test → resolve` as one crank. `/extract` is specifically the *missing half* of "save the chat": without it, transcripts accumulate unresolved (the swamp P3 warns against).

## Why Tier 2 Matters (but later)

- **`/gate-check`** patches a known weakness: `docs/06` §9 admits the v0 gate is *self-policing* (the same session that drafts also judges). Running validation as a separate command in a fresh context is the cheapest way to get an *independent* check without building production enforcement. It is also where the rubric's **accuracy** criterion is judged independently (`resources/_principles/rubric.md` §2 — style self-critique stays in-session; accuracy never).
- **`/render`** is the **content engine** end goal (`docs/06` Layer 3) — and the first real consumer of the render-side shared layers: `_style` (brand + the output-contract matrix), `_craft` (grounded plots), `_reference` (form, not facts). It must refuse to render where no validated insight exists upstream (`docs/08` P2).

## Design Rule (so the toolchain doesn't become rigidity)

```text
every command is a THIN CONDUCTOR over the canon — it points, it does not restate
                  MODEL-AGNOSTIC — improves prompts/evals/process, never bets on one model (P1)
                  ENDS AT A HUMAN CHECKPOINT — where judgment matters, it stops (P4)
```

Commands are the right home for workflow meta-tools. `/render` and `/gate-check` are the two that could later graduate into installable **skills** for reuse across repos.

---

**See also**: `.claude/commands/` (the commands themselves), `docs/05_mcp_test_protocol.md` (what `/test-resource` + `/extract` conduct), `docs/08_design_principles.md` (P3/P4 the loop commands serve), `docs/09_mcp_roadmap.md` (the tool-surface ledger), `docs/06_architecture.md` §9 + Layer 3 (the gate + content engine Tier 2 targets).
