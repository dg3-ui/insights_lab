# Log — ENSO blog render build (2026-06-12)

> **Status**: process-capture (`docs/08` P3), the `/extract` step this ad-hoc build skipped.
>
> **What**: built a `top_down × public × blog` rendering for El Niño × California solar (`InfraSure_ENSO_California_Solar.docx`), grounded live via the InfraSure MCP and shaped by the reference. Captured here because it was built by hand, not through `/test-resource` + `/extract`, so the fail→fix pairs had no `test_run`.

## The headline lesson

Building **ad hoc** (reference not loaded up front, no gate checkpoint) is exactly why the first two drafts were slop. Loading `_style`/`_principles`/`_craft` *before* drafting, and pausing at the human gate, is what caught every fix below. This is `docs/08` P4 (the loop is the product) earning its place.

## Fail → fix pairs (each routed to its home)

```text
FAIL (first drafts)                                FIX → where it now lives
─────────────────────────────────────             ───────────────────────────────────────
confidence shown as "LOW (directional)" badge      posture, not a pejorative badge        → _style/output_contracts §3,
  + "we make no production/revenue forecast"          (public); explicit label internal     brand §4 (calibration cue)
"WHAT WE ARE NOT SAYING" negation box              a confident caveat (what's resolving)  → output_contracts §3, brand §4
single-plant CF chart in a top-down piece          fleet/region figures only              → output_contracts §3 (move 6)
no map (punted twice)                              statebin tile-grid CONUS map           → _craft §6 (spatial fallback)
internal label "TOP-DOWN EXPOSURE BRIEF"           reader-facing kicker ("ENSO")          → output_contracts §3 not-include
title was a cryptic pun ("Cloudy, With a...")      title carries the message              → voice §3 / contract move 1
DOCX rendered SERIF (named "Inter" only)           name a guaranteed sans (Calibri/Arial) → brand §4 DOCX delivery note
in-body header band, no page footer                running Word header/footer + logo      → brand §4 DOCX delivery note
"none of this is reachable by a general model…"    show, don't flaunt: deep-link to       → voice §5, output_contracts §3
  + "15,000 plants" as a boast                       infrasure.ai; moat stays in the deck    (owner feedback)
```

## MCP gaps hit (logged to docs/09)

`R8` county aggregation · `R9` owner-name parent canonicalization · `R10` served geometry for a real map · `R11` news corpus has no climate/weather lane. The choropleth limit (`R10` + `R7` render tool) is why the map is a schematic tile-grid for now.

## Keep (worked)

Live MCP grounding (CA 36.8 GW, 153 plants ≥50 MW, owner ranking, Desert Sunlight 9-yr CF record) with `as_of` on every number; the NOAA external state dated and strength-uncertain (not inflated); the brand letterhead from the vendored lockup.

---

**See also**: `../../09_mcp_roadmap.md` (R8–R11), `../../../resources/_principles/voice.md` §5 (show, don't flaunt), `../../../resources/_style/output_contracts.md` §3, `../../05_mcp_test_protocol.md` (the capture this stands in for), `../../08_design_principles.md` P3/P4.
