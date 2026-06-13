# Status — Capabilities & Open Decisions

> **Status**: VOLATILE — the platform-capability build state + the open architectural decisions. This is the churn-prone half of the P1 seam, deliberately pulled OUT of `../architecture.md` so the architecture stays timeless canon and just points here. The other two status ledgers are `mcp_gaps.md` (tool-surface gaps) and `commands.md` (command build state); active working plans are in `../plans/`.
>
> **Updated**: 2026-06-13.

## Where V0 Stands

```text
   V0 PROVES ONE THESIS, manually:
      IF Claude has (1) MCP tools (2) one methodology resource (3) a clear prompt projection
      THEN it can draft one grounded applied insight (refs · confidence · caveats · actor).

   STATUS LADDER:
     [✅] data tools (MCP) live            [✅] source repo + taxonomy registry
     [✅] ENSO skill authored (SKILL.md)   [✅] Test Run 001 — PASS (with logged gaps)
     [✅] shared layers built (_principles · _style · _craft · _reference — layered-reference plan Ph1-4)
     [◑ ] bottom-up cracked — layered-reference plan Phase 5
     [◑ ] find_methodology discovery — spec'd (../method/discovery_spec.md), not built
     [☐ ] publish step · [☐ ] eval harness — design only (paused; eat PROCESS data first)
```

The active build is governed by the working plans, not this table — see `../plans/`. This ladder is the snapshot; the plans are the currency.

## Capability Build Status

| Capability | Status | Next |
|---|---|---|
| Data tools (MCP) | ✅ live | wire the `iso` filter (gap R1) / add region resolution |
| Source repo + taxonomy registry | ✅ built | — |
| One validated skill (ENSO) | ✅ test 001 PASS | — |
| Shared layers (`_principles`/`_style`/`_craft`/`_reference`) | ✅ built (v0.2) | bottom-up cells fill in plan Phase 5 |
| Skill **format** (`SKILL.md` from a package) | ✅ ENSO authored | generalize: a build script that compiles `SKILL.md` from any package |
| Discovery tool (`find_methodology`) | ◑ spec'd (`../method/discovery_spec.md`) | implement as an MCP tool over the registry index |
| Publish step (repo → served) | ☐ design | minimal: a build script that emits skill bundles + a registry index |
| Eval harness (examples/test_runs → CI) | ☐ design | turn golden outputs into pass/fail checks |

## Boundaries & Non-Goals (v0)

- No autonomous outreach — activation always follows a passed validation gate (human-in-the-loop outreach emails are the *first* output, but still post-gate).
- No raw-folder serving — only the published skill + registry are served.
- No production agent/orchestrator yet — v0 stays manual (MCP-ready, not MCP-integrated).
- No quantitative forecasts where the method only supports direction.
- No auth/authz in v0 — assumes a single trusted internal session; per-user credentials, catalog gating, external-access scoping are post-v0.

## After V0 — the two tracks

```text
validated insight object
        ├── in-house architecture track  → publish step · discovery · enforced gates · trace capture · persistence
        └── activation / outreach track   → renderings (report · vlog · email); BUILD report/vlog
                                            first (feedback loop), email last
```

Every tool gap logged during testing (like the `iso` filter) is an input to the in-house track's roadmap — see `mcp_gaps.md`.

## Open Decisions

1. **Delivery format** — RESOLVED 2026-06-05 toward **MCP-served** for v0: author in the Agent-Skill (`SKILL.md`) *format*, deliver by serving the body via the InfraSure MCP (`get_methodology`), so `find_methodology` is the authoritative discovery path. Native-Skill install is a valid alternative deployment, not combined with the served model. See `../architecture.md` §6 + `../method/discovery_spec.md` §1.
2. **Where discovery lives**: an InfraSure MCP tool vs a separate catalog service.
3. **State freshness enforcement**: how a skill guarantees the external state (NOAA) was pulled within an acceptable window before it renders. (Ledger R4 proposes a `get_external_state` tool that closes this.)
4. **Skill versioning & coherence**: how `resource.yml.version` + eval suite gate a re-publish, and how one publish stamps every derived artifact (skill bundle, registry entry, gate set) with that version. Make publish atomic per resource; have `get_methodology` + the insight trace echo the version.
5. **Discovery index at scale**: flat tag rank with one skill today; revisit before ~15–20 skills. (a) a controlled `drivers` vocabulary + alias map vs fuzzy matching — `../method/discovery_spec.md` §7 adopts an alias map as the v0 middle, still open; (b) RESOLVED 2026-06-05 → ranked top-N, never silent auto-bind (`discovery_spec.md` §4/§6); (c) RESOLVED → tie-break `exact-driver > family > actor > text`, epsilon-gated (`discovery_spec.md` §5).
6. **Canonical slug** — RESOLVED 2026-06-05: `el_nino_enso` (folder == `identity.slug`); descriptive "exposure" lives in `title` + the `family` tag. Remaining: publish asserts `folder == slug` for package folders (underscore shared layers excluded — `discovery_spec.md` §3, `resources/README.md`); revisit if one phenomenon ever needs multiple family-skills (see #5).
7. **Catalog maintainership & deprecation**: who owns the served catalog and approves a publish, and how a skill is marked deprecated so it stops surfacing in `find_methodology`.

---

**See also**: `../architecture.md` (the canon this is the volatile companion to), `mcp_gaps.md` + `commands.md` (the other status ledgers), `../plans/` (the active working plans — the real currency), `../method/discovery_spec.md` (the discovery contract several open decisions concern).
