# Status — Command Registry (build state)

> **Status**: VOLATILE — the per-command build state. The command *design* (lifecycle, the thin-conductor rule) is canon in `../process/commands.md`; this is just what's built. Reconciled to `.claude/commands/` on 2026-06-13.

```text
TIER   COMMAND          STAGE      WHAT IT DOES (thin conductor over →)              STATUS
────   ───────────────  ─────────  ───────────────────────────────────────────────  ──────
 0     /new-resource    AUTHOR     author a methodology package (the ENSO engine)     ✅ built  (method/ + principles)
 1     /test-resource   TEST       run the manual MCP test loop on an existing slug   ✅ built  (process/test_protocol · P4)
 1     /extract         RESOLVE    transcript → test_run + extraction + ledger        ✅ built  (test_protocol capture · P3)
 0     /recap           (meta)     ASCII structural recap + honest friction          ☐ planned (no file yet)
 1     /log-gap         (loop)     one-line append to status/mcp_gaps from anywhere   ☐ cheap   (status/mcp_gaps)
 1     /intake-feedback (loop)     triage out-of-loop feedback → routed homes + log    ☐ cheap   (test_protocol §intake · template)
 2     /gate-check      GATE       INDEPENDENT validate vs contract + blocked_claims  ☐ tier2   (resource_standard · architecture §7 · _principles)
 2     /render          RENDER     gated studio brief → deliverable (blog/report/     ✅ built  (architecture L3 · P2 · P6
                                   email) + grounded charts/maps; P6-first                      · _style · _craft · confidence_model)
 3     /eval-resource   EVAL       run examples/test_runs + fail→fix as pass/fail      ☐ later   (paused; eat process data first)
 3     /find-methodology DISCOVER  rank resources by taxonomy for a query             ☐ later   (revisit ~10 skills; discovery_spec)
 3     /sync-docs       MAINTAIN   house-style + cross-ref + registry consistency      ☐ later   (when drift is real)
```

Status legend: ✅ built (file exists in `.claude/commands/`) · ◑ in progress · ☐ planned. **Reconciliation note (2026-06-13)**: the old registry marked `/recap` built and `/test-resource`+`/extract` "next"; the filesystem shows the reverse — corrected above.

---

**See also**: `../process/commands.md` (the design + the thin-conductor rule), `mcp_gaps.md` + `capabilities.md` (the other two status ledgers), `../plans/` (active working plans).
