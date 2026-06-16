# tasks_history — Session Handoff Records

> **Status**: README added 2026-06-15 (the folder predates it — the first entry is `2026-06-05__insights-lab__repo-readiness/`). Per-session task documentation, in the format from `.cursor/commands/PROMPT_CREATE_TASK_DOCS.md`: one folder per substantial session, four files (context · decisions · notes · handoff). The **handoff** is the bridge to the next session/model. (Earlier entries may use a lighter heading style; the four-file intent is the constant.)

## Folder convention

```text
docs/extra/tasks_history/YYYY-MM-DD__area__short-slug/
  ├── task_context.md   objective · background · problems · what we built · files touched · status · next
  ├── decisions.md      one section per design decision: Decision + Rationale (the WHY, not just the what)
  ├── notes.md          implementation detail · commands/MCP calls · verification · metrics · key insights
  └── handoff.md        MOST IMPORTANT — 10-bullet 60-second summary + an explicit next-action roadmap
```

`area` examples for this repo: `output-layer` · `studio` · `resources` · `confidence` · `docs` · `commands` · `method`. Slug = 2–4 words naming the specific work. Date format `YYYY-MM-DD`.

## How this relates to the other session records (don't duplicate)

```text
test_runs/<resource>/      VALIDATION records — a gated test of one resource (pass/fail, accepted/rejected claims)
docs/learning/logs/        DISTILLED learnings — prompting moves, fail→fix pairs (the P3 extraction)
docs/plans/                the active WORKING plans (what's next), archived to plans/done/ when complete
tasks_history/ (this)      the full SESSION HANDOFF — context + decisions + the next-action roadmap for a model switch
```

A session that produced a validated insight still writes its `test_run`; a session that moved the architecture writes a `tasks_history` entry. They are complementary: `test_runs` prove a claim, `tasks_history` carries the working context across a context-window or model switch.

---

**See also**: `.cursor/commands/PROMPT_CREATE_TASK_DOCS.md` (the format spec) · `../../process/test_protocol.md` (the validation records) · `../../learning/logs/` (distilled learnings) · `../../plans/` (active plans).
