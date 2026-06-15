# Studio Brief — <Title>

> **Location**: a brief lives at `studio/<subject>/<phenomenon>.md` (subject = an entity OR a region/corridor; phenomenon = the driver, matching a resource slug). The paths below assume that depth (`../../`).
>
> **Subject**: <entity or region/corridor> · **Phenomenon**: <driver, e.g. el_nino_enso> (`../../resources/<domain>/<slug>/`)
>
> **Output type**: <blog | report | email> · **As of**: <YYYY-MM-DD> · **Audience**: <internal | client | public> · **Grounding**: <MCP-grounded | research-grounded (label it)>
>
> *(This header blockquote is **internal metadata — strip on render**: the Location/Subject/Grounding lines carry toolchain taxonomy, not reader copy.)*
>
> **A cloud-attachable brief**: attach this + `../../resources/_style/brand.md` + `../../resources/_principles/voice.md` (+ `_craft` if charts) → render for the target format. **Post-gate only** — this brief dresses a *validated* insight (the three guards, `../README.md`).
>
> ⚠ **GROUNDING FRESHNESS — re-ground on use.** Substrate figures are a dated **MCP snapshot** (see As-of); the upstream `renewablesinfo_org` platform fetch may not have been re-run. **Before any external use — and whenever this brief is loaded as a skill in a live Claude session — re-fetch the named entities against the live InfraSure MCP, confirm the platform data is current, and reconcile any drift.** The methodology is stable; the numbers are perishable (`../README.md`).

## 1 · The validated insight (the gated content — grounds everything · SINGLE SOURCE OF TRUTH)

`<the claim grammar from the test_run / applied-insight: claim · scope · mechanism · source_refs (each with as_of) ·
 caveats · actor relevance · review trace. OR a pointer to the gated test_run. Nothing here may exceed what the gate passed.>`

**Calibration — the three axes (`../../docs/method/confidence_model.md`).** This block is the **single source of truth**; the output posture (§3) and the triage ranking (`../_triage.md`) *derive* from it and never re-state a grade. Split per-part where the claim has parts (`confidence_model.md` §6).

| Axis | Value | Basis |
|---|---|---|
| **Calibration cap** (internal) | `<High / Medium / Low / Blocked — per part if needed>` | `<the weakest required input; nothing here raises it>` |
| **Event likelihood** (on output) | `<the sourced external probability, e.g. NOAA 63% — or a season frame>` | `<named source + as_of; NOT our self-grade>` |
| **Materiality** (internal) | `<negligible / modest / meaningful / severe>` | `<exposed-share (substrate count) × class-severity band (peril resource financial_materiality); never a $>` |

`<ON OUTPUT: posture (the cap → a register phrase) + the event number + a settledness bar (▰▰▰▱▱) where a firming
 forecast exists. The cap grade + the materiality band stay INTERNAL — render-internal regardless of repo visibility.>`

## 2 · The comparison (the moat + the hook)

`<the MCP-grounded comparison — "this portfolio vs its peers / vs last year, over the next 12 months" — with the entity
 IDs + the tool that produced it + as_of. This is the home-run engine: the thing a vanilla LLM can't produce, and the
 attention-grabber. GROUNDED, not invented (guard 3).>`

## 3 · Creative & Activation (the cherry — bounded by the guards)

```text
HERO VISUAL    <the ONE chart/image that lands the read — usually the grounded comparison. _craft rules apply
               (every series a source_ref + as_of); the visual SAYS nothing the gated insight doesn't.>
PUNCHLINE/HOOK <the headline that grabs — lands on FRAMING, never on inflating a claim (guard 2). Catchy title, honest number.>
COMPARISON     <how the §2 comparison is framed for impact ("better/worse positioned than X") — grounded.>
CONFIDENCE     <on the rendered face: POSTURE + the EVENT likelihood + the SETTLEDNESS bar where it applies.
               NO "CONFIDENCE: LOW" badge; the cap grade + materiality band are internal (confidence_model.md §3).>
FORWARD DOOR   <a scope boundary reframed as a door to the deeper InfraSure layer — "the per-asset modeling is where
               InfraSure goes deeper, talk to the team." Never "we don't model that" (P7).>
CHANNEL NOTES  <how it flexes: blog title vs report subject-line vs email one-liner. Send stays human-in-the-loop (post-gate).>
```

## 4 · Render notes

```text
COMPOSE     brand.md Part A (design language) → rendered for the target format via Part B (HTML / DOCX / …) ·
            voice.md (the prose) · _craft (grounded charts)  ·  output_contracts.md (the <type> envelope)
GATE        renders ONLY this validated insight; every number traces to §1's source_refs (P2).
            Confidence display per confidence_model.md §3 — posture + event + settledness, never the "LOW" badge.
GUARDS      gate-upstream · creative≠overclaim · grounded-hook (../README.md §guards).
```

## 5 · Gaps / next

`<what's still resolving · which form exemplar to promote toward in ../../resources/_reference/internal/ if this lands>`
