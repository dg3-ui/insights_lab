# Learning Track

> **Status**: v0 onboarding track, deepened 2026-06-05.
>
> **Purpose**: help contributors learn the concepts needed to build and test methodology resources — grounded in real InfraSure tool output, not abstraction — without turning learning notes into deliverables.

Learning lives under `docs/learning/` so the top-level repo stays scalable for future `code/`, `scripts/`, or `data/` folders when real implementation work begins.

## What Each Doc Delivers

| Doc | The question it answers | Grounded in |
|---|---|---|
| `00_fundamentals_map.md` | What is this whole project — goal, architecture, scope, fundamentals — at a glance? | the visual on-ramp: every concept drawn in ASCII, pointing into the prose docs |
| `01_mcp_basics.md` | What are the InfraSure tools, what do they return, and how do I verify Claude used them? | live 12-tool surface, real `search_plants` / `get_plant` I/O |
| `02_infrasure_data_substrate.md` | What does the data contain, and which of it can *ground* a claim vs. only *frame* or *route* it? | real `get_plant(57993)` record + `aggregate` output |
| `03_methodology_resources.md` | What am I building — and why does each field of the resource contract exist? | the ENSO resource, traced end-to-end |
| `04_prompt_projection.md` | How does a resource become the strict surface the model sees in a test? | the ENSO `prompt_projection.md` anatomy |

## Read Order

```text
00_fundamentals_map.md          <- start here: the whole project, drawn
  -> 01_mcp_basics.md
  -> 02_infrasure_data_substrate.md
  -> 03_methodology_resources.md
  -> 04_prompt_projection.md
  -> logs/
```

Each doc ends by pointing to the next; `04` points you to the first real test.

## Two Themes That Run Through All Four

```text
1. Ground or downgrade.   A claim with no tool result / named source is commentary, not an insight.
2. The MCP is a floor.    The 12 tools are the v0 starting surface — every gap you hit is a
                          roadmap input for the next tool/field, not a dead end. Log it.
```

## What To Log

Use `logs/` to record, after each test:

- what was unclear or confusing
- which MCP/data tools were useful — and which **gaps** you hit (with a workaround + a roadmap line)
- what data was missing, and whether it blocked or downgraded a claim
- where the methodology resource was too vague
- where Claude overclaimed, skipped caveats, or skipped retrieval
- what should change in the resource or projection before the next test

Logs are not polished essays. They are feedback loops for improving the resource, the test protocol, and the platform's tool surface.

## Learning Is Not The Deliverable

These four docs make you *able* to do the v0 work. The v0 work itself is: a methodology resource + a prompt projection + **one manual MCP/Claude test** + an applied-insight draft + a logged set of gaps. When in doubt, go run `resources/weather_and_climate/el_nino_enso/test_runs/test_run_001.md` — the test is what turns this track from theory into evidence.
