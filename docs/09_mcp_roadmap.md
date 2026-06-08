# 09 - MCP Roadmap Ledger

> **Status**: living ledger, opened 2026-06-05.
>
> **Purpose**: the persistent home for "this MCP call / field / filter would be super useful" — the agent's back-of-mind for the tool surface. Every gap or idea hit while authoring or testing a resource lands here, so the *expandable floor* (`learning/01`) actually accumulates instead of evaporating at the end of a session.
>
> **This is data, not instruction.** The *instruction* to log here lives in `CLAUDE.md` / `AGENTS.md`; this file is the resolved ledger it feeds (`08_design_principles.md` P3).

## Why This File Exists

A model has no memory between sessions. An MCP gap noticed today is gone tomorrow unless it is written down. This ledger is the tool-surface analog of what `test_runs/` extraction is to the methodology: **resolved feedback that grows the platform** (`06_architecture.md` §11 tool roadmap). Each entry is also a roadmap input for the post-V0 in-house track (`01_scope_v0.md`).

## How To Add An Entry

Every entry has the three-part shape from `learning/01_mcp_basics.md` + `05_mcp_test_protocol.md`, plus where it was observed and a status:

```text
gap/idea:   what the surface can't do, or what would help
workaround: what kept the session moving (or "none yet")
roadmap:    the concrete tool / field / filter to build
observed:   the session / doc where it surfaced (+ date)
status:     open · proposed · building · shipped · wontfix
kind:       tool gap · field/coverage gap · new tool · filter · external-state
```

Keep entries terse. A recurring entry is a signal to prioritize it; note the repeat rather than duplicating.

## Ledger

### R1 — `search_plants(iso=…)` filter is unwired

```text
gap:        search_plants(fuel=solar, iso="CAISO", minMw=50) -> []  (empty; even iso alone returns [])
            yet get_plant(57993).regions.iso_rto = CAISO exists per-plant — the data is there, the filter isn't.
workaround: scope by state="CA" (CA ≈ CAISO, minus LADWP/SMUD/IID), then confirm each plant's
            regions.iso_rto via get_plant.
roadmap:    wire the search_plants ISO filter to the existing per-plant region join, OR add a
            resolve_region tool. This single fix turns the surface from 12 tools toward 13.
observed:   learning/01_mcp_basics.md + test_run_001 (2026-06-05)
status:     open      kind: filter
```

### R2 — No fleet-level seasonal-CF rollup

```text
idea:       ENSO (and any Exposure-family) insight wants the seasonal capacity-factor baseline for a
            *fleet*, not one drilled plant. Today the only CF evidence is get_plant on a single asset.
workaround: drill one representative plant (e.g. 57993) and caveat that it is illustrative, not fleet-wide.
roadmap:    an aggregate-style call returning monthly/seasonal CF distribution across a scoped fleet
            (e.g. aggregate(entity=plants, metric=seasonal_cf, group_by=month, filter={state,fuel,minMw})).
observed:   test_run_001 next-fixes (2026-06-05)
status:     open      kind: new tool
```

### R3 — `developer` (and other resolved facts) null on queue rows

```text
gap:        search_projects rows return developer: null across DARDEN / UMBRIEL / WINGTIP etc. —
            so Development-Risk + Portfolio actor-routing has no actor to route to.
workaround: omit actor relevance where absent; do NOT infer a developer. Flag as a context gap.
roadmap:    extend resolved-fact coverage onto queue projects (find_by_extracted_fact over projects),
            or expose a coverage flag so the agent knows when routing is simply unavailable.
observed:   02_analysis_catalog.md (Development Risk) (2026-06-05)
status:     open      kind: field/coverage gap
```

### R4 — No served external-state call (NOAA ENSO etc.)

```text
idea:       the external causal state (NOAA CPC ENSO / ONI) is fetched ad hoc via WebFetch each test,
            with no enforced freshness. The methodology supplies it; nothing serves it with an as_of.
workaround: WebFetch the NOAA discussion live and hand-stamp the as_of in the insight.
roadmap:    a get_external_state(driver) MCP tool that returns the current state + as_of + source URL,
            cached with a freshness window. Closes architecture Open Decision 3 (state-freshness gate).
observed:   architecture §9 Open Decision 3 + test_run_001 (2026-06-05)
status:     proposed  kind: new tool / external-state
```

### R5 — No coverage / introspection call

```text
idea:       the agent cannot cheaply ask "what fraction of this scoped fleet has offtaker / financial /
            generation data?" — so it can't decide *up front* whether to downgrade for missing context.
workaround: drill plants until a pattern is obvious; expensive and ad hoc.
roadmap:    a coverage(entity, fields, filter) call returning fill-rates per field over a scope, so the
            confidence-cap-for-missing-context rule (08 P-data / confidence_rules) can fire deterministically.
observed:   inferred from 04_context_and_data_map + confidence_rules discipline (2026-06-05)
status:     open      kind: new tool / introspection
```

---

**See also**: `learning/01_mcp_basics.md` (the floor-not-ceiling thesis + the gap-log format), `05_mcp_test_protocol.md` (the failure taxonomy each gap maps to), `06_architecture.md` §11 (the tool roadmap these entries feed), `08_design_principles.md` P3 (why this is resolved data, not instruction), `CLAUDE.md` (the standing instruction to log here).
