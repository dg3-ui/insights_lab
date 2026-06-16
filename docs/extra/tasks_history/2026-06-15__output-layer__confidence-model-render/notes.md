# Notes — Implementation, MCP, Verification, Metrics (2026-06-15)

> **Status**: the detailed record — how it was built, what was pulled live, how it was verified.

## Commits (this session, on `main`)

```text
af394d7  Output-layer architecture: 3-axis confidence model + subject-keyed studio + triage
9c191ba  Standard Solar guide: ground extreme-heat (NOISE) + resolve offtaker (blocked)
7953c4c  studio: top_down/bottom_up as a meta-tag + scope ladder (not a folder split)
ce628f3  studio: origination norm — studio-first for outputs; bottom_up before top_down
649a170  P6 sharpened: references inform the ANALYSIS too — guide, don't force (incl. studio)
33735f1  Build /render (P6-first conductor) + demo the maps gap closed with a real artifact
a7322bd  render/_craft: make explicit that the MODEL generates the artifact (P1/P6 applied)
d326654  docs sync: front-door architecture/flow docs absorb the 2026-06-15 build
```

## MCP grounding (live InfraSure tools, as_of 2026-06-15)

```text
plants_by_owner("Standard Solar", fuel=solar, limit=200)
  → 127 plants / 355.3 MW (the ENSO brief saw 129 / 362.3 — DRIFT between pulls, the freshness point).
  by-state (jq on the saved tool-result): IL 17/59.1 · MN 40/44.4 · NM 9/43.0 · VA 9/39.2 · MD 11/28.1 ·
  CA 8/20.4 · CO 8/20.4 · ID 1/20 · ... · TX/OK/KS/NE/SD = 0 (the hail-maximum finding).

get_plant(62406)  City of Gallup Solar, NM, single-axis c-Si, 8 MW
  → monthly CF: summer ~0.35 (Jun) vs winter ~0.10–0.15 (Dec/Jan) — summer CF is HIGH (the heat discipline);
    financial.ppa_price_per_mwh = $44.08 (a FIXED PPA — mutes the heat peak-revenue sting); offtakers = null.
get_plant(67747)  Nachtigall 1836-WD, CA Kern, fixed-tilt, 4.6 MW
  → online Dec-2024, no usable CF yet; offtakers = null. Confirms MIXED construction (62406 single-axis / 67747 fixed-tilt).
```

**MCP-gap finding (R13, sharpened).** `get_plant.offtakers` is null book-wide, BUT the PPA *price* is sometimes recoverable from `financial.ppa_price_per_mwh` (Gallup $44.08) — a fixed-vs-merchant *structure* signal, not the counterparty. Logged in `docs/status/mcp_gaps.md` R13. (R14 geometry-seeded query + R12 hazard peril model also referenced by the new briefs.)

## Rendering (the demo map)

```text
generator: /tmp/gen_hail_map.py   (Python, STDLIB ONLY — no matplotlib; kept transient, NOT committed)
output:    studio/brookfield_standard_solar/_renders/hail_us_statebin.html   (committed artifact)
technique: _craft §6 statebin tile-grid — each state a rounded SVG rect on a fixed (row,col) grid,
           shaded by SPC hail climatology (deep-red maximum column = TX/OK/KS/NE/SD), Standard Solar
           plants as MW-scaled green dots. Self-contained HTML + inline SVG (brand B1 shell).
verify:    ASCII grid eyeball (reads as US: West-left, NE-top-right; 0 dots in the maximum) +
           tag-balance well-formedness (51 tiles, 19 dots, balanced; expat XML parser is broken in
           this py3.14 build, so used regex tag-counting instead).
```

**Sandbox constraint (verified 2026-06-15):** no `matplotlib`, no `geopandas`, no `kaleido`. So HTML + hand-authored inline SVG is THE reliable render path; the `_craft` §5 matplotlib-PNG fallback needs matplotlib installed. Recorded in `_craft` §6 + `render.md`.

## Verification (4 workflows — adversarial + audit)

```text
wf w...  (4-lens adversarial)   foundation coherence · single-source/no-drift · no-leaked-grade · arcs-preserved
   → FOUND: triage led Galveston with ACT off the highest cap (violated binding-cap rule); materiality cited a
     hazard-only field (ungrounded for ENSO); architecture.md front door still single-axis; el_nino_enso.yml seam
     stale; triage verdict missing from brand/output_contracts never-render lists; Galveston "two parts" vs 3 caps;
     em-dash in a rendered punchline; "noise" colliding with the triage NOISE verdict; template glyph inconsistency.
   → ALL reconciled (see decisions #3, #6).
wf w...  (2-lens confirmation)  triage-logic-now-consistent · cross-doc-consistency → CLEAN (1 nit: a footer gloss, fixed).
wf w...  (5-agent audit)        architecture.md · CLAUDE.md · docs/README · use_cases + a grep sweep
   → FOUND: Layer-3 drift across the front-door docs (the output half); use_cases cited as owner of the
     "activation boundary" but the section didn't exist (dead reference, 5 files); /render still "planned" in
     commands.md; old "direction × audience × format" / "blog/brief/email/post" / "P1–P5" labels lingering.
   → ALL reconciled (the docs-sync commit d326654).
```

**Blocked-claim discipline checks (greps, all clean):** hail.md + extreme_heat.md scanned for `$`/EAL/PML/return-period/`%/MWh`/"will lose" → every hit is a *refusal* or a legitimate substrate value (the $44.08 PPA price, the exposed-share %), never an asserted blocked claim. The heat brief's specific trap (reading heat off monthly CF) is explicitly disciplined (summer CF shown HIGH; Jul/Aug softening attributed to NM monsoon, not heat).

## Metrics

```text
8 commits · ~30 files created/modified · 4 workflows (≈620k subagent tokens) · 2 live get_plant + 1 plants_by_owner pull
studio: 2 subjects · 4 phenomenon briefs (3 gated-draft + 1 corridor) · 1 subject guide · 1 triage board · 1 rendered map
new canon: confidence_model.md · /render command · the 2026-06-15 plan
```

## Key insights / lessons

1. **The three-axis split is the unlock.** Once cap/event/materiality are separated, the honest output writes itself (posture + the real event number) and the triage ranks correctly (hail > ENSO on *severity*, not exposed share).
2. **Materiality must be grounded, not asserted** — the verification caught that the basis cited a hazard-only field; the fix (weather resources read knowledge.md sensitivity) is what makes the model honest for its anchor resource.
3. **The discipline spread of verdicts is the proof the system works** — one ACT/WATCH (Galveston co-location), one WATCH-high (hail), one WATCH-low (ENSO), one NOISE (heat), one BLOCKED (offtaker). A system that rubber-stamps everything ACT/WATCH isn't triaging.
4. **"Build for scale, not patches" + P6 are the same thread** — the model is the trusted engine; the structure is a stepping-stone; that reaches all the way down to *how the pixels get made* (the model writes its own SVG).
5. **Freshness is real** — the book drifted between two pulls in one session; "re-ground on use" isn't theoretical.
6. **The honest move beats the impressive one** — "Anten" → a grounded corridor; offtaker → a logged gap, not a fabricated "low"; heat → NOISE (the least material peril), not an inflated risk.
