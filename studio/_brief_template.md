# Studio Brief — <Title>

> **Output type**: <blog | report | email> · **As of**: <YYYY-MM-DD> · **Audience**: <internal | client | public> · **Grounding**: <MCP-grounded | research-grounded (label it)>
>
> **A cloud-attachable brief**: attach this + `../resources/_style/brand.md` + `../resources/_principles/voice.md` (+ `_craft` if charts) → render for the target format. **Post-gate only** — this brief dresses a *validated* insight (the three guards, `README.md`).

## 1 · The validated insight (the gated content — grounds everything)

`<the claim grammar from the test_run / applied-insight: claim · scope · mechanism · source_refs (each with as_of) ·
 confidence · caveats · actor relevance. OR a pointer to the gated test_run. Nothing here may exceed what the gate passed.>`

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
CHANNEL NOTES  <how it flexes: blog title vs report subject-line vs email one-liner. Send stays human-in-the-loop (post-gate).>
```

## 4 · Render notes

```text
COMPOSE     brand.md Part A (design language) → rendered for the target format via Part B (HTML / DOCX / …) ·
            voice.md (the prose) · _craft (grounded charts)  ·  output_contracts.md (the <type> envelope)
GATE        renders ONLY this validated insight; every number traces to §1's source_refs (P2).
GUARDS      gate-upstream · creative≠overclaim · grounded-hook (README §guards).
```

## 5 · Gaps / next

`<what's still resolving · which form exemplar to promote toward in _reference/internal/ if this lands>`
