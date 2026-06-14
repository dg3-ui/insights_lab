# Design Principles

> **Status**: v0 governing principles, 2026-06-05 · **amended 2026-06-14** (P1 corollary: authored scaffold vs runtime intelligence + the no-code rail; P6 asymmetry guard — `plans/2026-06-13_knowledge_base_expansion_v1.md` Phase 0).
>
> **Audience**: anyone authoring resources, building the engine, or deciding what to freeze vs. leave open.
>
> **In one line**: stay flexible where the tooling moves fast, stay rigid where the discipline is the moat — and never confuse the two.

## Why This File Exists

The other docs say *what* to build. This one says *what must not move* and *what must stay swappable* — so the project can absorb fast-moving LLM/agent advances without rebuilding, and without dissolving into mush. Every principle below is a constraint we accept on purpose. If a future decision violates one, that is the signal to stop and re-reason, not to quietly route around it.

```text
GATE 0: For any new capability — which layer does it touch?
        stable (methodology) ──► hold the line, version it carefully
        volatile (execution) ──► keep it swappable, expect it to change
```

## Principle 1 — Two Layers: Stable Methodology, Volatile Execution

The fastest way to lose to the next model release is to entangle *what a defensible insight is* with *which engine produced it*. Separate them, and let only one side move.

```text
STABLE  (the methodology layer)              VOLATILE (the execution layer)
─ slow-moving · versioned · the moat ─       ─ fast-moving · swappable · commodity ─
the claim grammar (7 slots)                  the model (Opus / Sonnet / next)
ground-or-downgrade                          the orchestration (manual → agentic)
blocked_claims discipline                    the delivery format (MCP-served / native skill)
the taxonomy (domain·family·driver·actor)    the exact prompt phrasing
"content is downstream of insight" (P2)      the retrieval plumbing
confidence-capped-at-weakest-input
```

The payoff is the answer to "how do we ride LLM progress?": **you do not keep the methodology loose — you keep it tight and hot-swap the engine underneath it.** A better model does not change what a grounded, caveated insight is; it just executes the same discipline more cheaply and more reliably. Volatility lives in the engine, never in the standard.

`resource.yml` is the seam between the layers: it encodes the stable contract (taxonomy, confidence_rules, blocked_claims) so the volatile engine can be rebuilt around it without touching the discipline.

**Corollary — the intelligence is the model's job; we author the scaffold.** InfraSure is an intelligence system (`architecture.md` §1), and "intelligence" splits along this same seam. The **authored scaffold** — recipes, `_method` primitives, the family map, the claim/Q&A grammar — is **stable / L0**: methodology a model *reads*. The **planning + synthesis** that turns a question into a grounded insight (decompose → retrieve → rank → drill → synthesize) is **volatile / L2 = the model's job** (the table above already lists *the orchestration, manual → agentic* as volatile). So a recipe or `_method` artifact is **a docs/spec the model READS, never an engine we BUILD** — no `code/`, no `scripts/`, no planner/orchestrator in v0. "Build the intelligent system" must always resolve to "author the scaffold that makes the model reason like an InfraSure analyst," or it has frozen intelligence into the swappable layer.

## Principle 2 — Content Is Downstream of Validated Insight

The moat is grounding, not fluency (`architecture.md`). A generic LLM already writes well. The moment the rendering layer is allowed to pull the methodology toward "make this read well," the moat is gone and we have rebuilt a content farm.

```text
ALWAYS this order — no exceptions:

   grounded retrieval ─► assembled insight ─► VALIDATION GATE ─► render
                                                  │
        blog · email · card · LinkedIn post ◀─────┘   (a rendering, never a source)
```

A blog, a curated outreach email, an Ask answer, a LinkedIn post — these are all *renderings of the same validated insight object*, differing only in audience and length. A blog is a useful first rendering precisely because many smaller renderings derive from it. But the blog is a **forcing function and an output, never the origin**. If a claim cannot survive the gate, no amount of good writing rescues it; it does not get rendered.

## Principle 3 — Process Data Obeys the Same Laws as Asset Data

We already solved "how to make raw inputs trustworthy" in the data layer. Apply the same pattern to the *process* of producing insights (the saved sessions — see `process/test_protocol.md`).

```text
ASSET DATA  (already built)               PROCESS DATA  (the sessions we save)
raw: EIA · GEM · ~57K news                raw: full chat transcripts (intern · reviewer · agent)
   │ resolve                                 │ extract
   ▼                                         ▼
resolved facts (find_by_extracted_fact)   prompting moves · enrichment deltas · fail→fix pairs
   │ serve the resolution, not the raw       │ serve the extraction, not the raw
   ▼                                         ▼
grounds a claim                           sharpens prompt_projection + the eval suite
```

Three rules carry over unchanged:

- **Source, not served.** A raw transcript is source of truth, never the deliverable — exactly as we never bolt the raw `weather_and_climate/` folder onto MCP (`architecture.md` §2).
- **Resolve or it is a swamp.** A pile of unprocessed transcripts is as low-signal as a pile of unread news articles. The value is the extraction step, planned from day one (manual at first is fine).
- **Floor, not ceiling.** A gap surfaced mid-session (a missing tool, a vague rule) is a roadmap input, logged — not a dead end (`learning/01`).

"Fine-tuning the workflow" means improving **prompts, evals, and process** — model-agnostic assets that survive the next release. It explicitly does **not** mean fine-tuning a base model (that would be a Principle 1 violation: training on model X, obsoleted by model X+1).

## Principle 4 — Iteration Is Expected, Not a Failure

A one-shot output is a *draft*, not the product. The enrichment happens in the loop, and the human checkpoint in that loop is not overhead — it is the product. "Augment humans, give them more hands" *is* the iteration loop made first-class.

```text
discover → load → ground → assemble → GATE
              ▲                          │
              └──── human checkpoint ◀────┘
                 (enrich · re-scope · challenge · approve)
```

So the architecture's runtime is a loop, not a line (`architecture.md` §3, Layer 2), and the eval suite must be able to consume *iteration traces*, not only static golden outputs.

## Principle 5 — Flexibility Is Not an Excuse for Non-Commitment

"LLMs move fast, stay flexible" is correct and has a failure mode: using it to never fix anything, which produces a project that cannot be measured because nothing is stable enough to test. Flexibility is disciplined, not loose:

```text
flexible (good)                          loose (failure)
─────────────────                        ─────────────────
volatile layer stays swappable           nothing is ever fixed
stable layer is committed + versioned    the standard drifts per session
gaps are logged + roadmapped             gaps are silently worked around
decisions are made, then revisited       decisions are deferred forever
```

If you cannot say which layer a change touches (P1) or which job an input does (`learning/02`: grounds / frames / routes), you are not yet ready to commit it — but the answer is to *resolve that*, not to leave it open indefinitely.

## Principle 6 — References Inform, They Don't Bind (preserve the model's creativity)

A reference — an external exemplar in `resources/_reference/`, an internal golden output, a baked-in structural cue — exists for **one job: to improve the output**. It is never ground truth, and it is never a constraint. The model's own creativity, design judgment, adaptability, and current knowledge are a genuine advantage; a reference must *sharpen* that intuition, never *replace* or *cage* it.

```text
A reference EARNS its place only by making the output better.
   it helps the output            → use it
   it doesn't help                → drop it; do NOT force-fit a reference
   the model's instinct is better → trust the instinct

   a small, well-placed cue can have outsized POSITIVE impact (e.g. the InfraSure
   ENSO / CA-solar prompts) — but that is because it helped, not because it was required.
   the same cue forced where it doesn't fit makes the output worse.
```

This is the deliberate counterweight to "bake references in so quality is automatic" (the `_reference` corpus, the `_style` contracts): bake them in as **available inspiration**, never as a rule the model must satisfy. Slavishly following the reference folder produces flatter, worse output than a model trusted to reason — and it throws away the exact thing an LLM is good at (creativity, design, the latest information, adaptability).

What stays binding is the **discipline** — grounding, `blocked_claims`, the gate, the claim grammar — never the *form* a reference happens to show. This is P1's volatile layer seen from the inside (the model is the swappable, *trusted* layer, so we don't shackle it), the anti-microprompting doctrine (`../resources/_principles/voice.md` §4) applied to references, and the floor-not-ceiling rule applied to form. **This one does not get walked back.**

**The asymmetry guard.** Borrow *form and packaging* from external references (a competitor's structure, a big-firm repo's layering); **never trade the gate for a reference's thinner guardrails.** A richer-scale repo can be ahead on packaging and still behind on the evidence discipline that is our moat — borrowing its shape must never dilute `blocked_claims`, `confidence_rules`, or the gate.

## How To Use These Principles

```text
adding a capability   -> P1: which layer? freeze or keep swappable accordingly
writing a rendering   -> P2: is there a validated insight upstream of it? if not, stop
saving a session      -> P3: capture raw, but plan the extraction; serve the resolution
reviewing an output   -> P4: is this a draft or did the loop run? evals must see the loop
facing an open call    -> P5: decide and version it, or name exactly what blocks the decision
using a reference     -> P6: does it improve THIS output? if not, drop it — never force-fit; trust the model
```

---

**See also**: `architecture.md` (the moat = grounding), `use_cases.md` (the after-V0 activation split that P2 governs), `process/test_protocol.md` (where P3/P4 are operationalized), `architecture.md` (the stable/volatile seam + the runtime loop), `resources/_reference/` (the exemplar corpus P2 feeds, quarantined from grounding).
