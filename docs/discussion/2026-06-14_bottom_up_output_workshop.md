# Discussion — The Output Half: bottom-up reports + the output workshop + a first-class creative layer

> **Status**: **OPEN**, opened 2026-06-14 — a **draft to argue with**, not a decision. The lab is crossing from the half we've built (**grounding / methodology**) into the half we haven't (**output / activation**). Trigger: the meeting's two **bottom-up** deliverables (Anten · Brookfield/Standard Solar) + the owner's insight that a *home-run* bottom-up needs a **creative layer** (visuals, marketing punch) we haven't made first-class.
>
> **The headline**: this is **not a teardown** — it's the lab maturing into Layer 3, which the architecture reserved and the **paused `layered_reference_v1` Phase 5 ("crack bottom-up")** already named. Appendable. The one seam we cross is the **gate**, and it was drawn on day one.

## 1 · The reframe — we're building the output half, on schedule

```text
BUILT (the grounding half)                         NEW (the output half — this)
resources · MCP grounding · _method · recipes      bottom-up REPORTS · the output workshop · the creative layer
the GATE (insight is validated)                    RENDERINGS of validated insight (post-gate)
"is it true + defensible?"                         "does it LAND + is it a home run?"
        └────────────────── the seam = the GATE (insight → gate → render) ──────────────────┘
```

Two anchors already exist, so this is additive: **Layer 3 (the content engine)** in `../architecture.md` (we just never built it — renders got dumped ad hoc in `../extra/`), and **`../plans/2026-06-11_layered_reference_v1.md` Phase 5 = "crack bottom-up"** (PAUSED, waiting). `../../resources/_style/output_contracts.md §3` already defines **report = a blog scoped to a portfolio/client/region** — that *is* bottom-up.

**Scope of `studio` (owner refinement, 2026-06-14)** — `studio` is a **selective amplification lane — the *cherry on top*, NOT a mandatory stage.** It spans use-case types (top-down blogs · in-substrate *and* off-substrate bottom-up · even the standard resource-+-MCP → output); **bottom-up is just where we start.** Many outputs stay on the **baseline path** (gated insight → render) with **no** studio creative pass; studio is **opt-in for the pieces that must land as home runs.** So studio is a *capability, not a pipeline gate* — and that selectivity is itself a guard against content-farm drift (you only spend the creative budget where it earns a home run).

## 2 · Two bottom-up modes (both valid, both served by this)

```text
IN-SUBSTRATE bottom-up   Anten (ports → storm-surge/hurricane) · Brookfield/Standard Solar (solar → 12-mo El Niño)
  → MCP + resources + the COMPETITIVE COMPARISON ("your portfolio vs peers over 12 months")   ← the meeting's deliverable
OFF-SUBSTRATE bottom-up  Red Dog (Arctic mine) → research + the outlier playbook (`../method/outlier_playbook.md`)
```

**The bottom-up MOAT (and the home-run hook) is the same thing**: the **MCP-powered comparison**. A vanilla LLM can't rank a named portfolio against peers across the 15K-plant substrate — and that grounded comparison *is* the marketing punch ("you're better/worse positioned than X"). The creative layer **amplifies a grounded comparison; it never manufactures one** (§6).

## 3 · What's already supported vs. genuinely new

```text
ALREADY SUPPORTED (reuse, don't reinvent)
  report shape            output_contracts.md §3      prose punch        _principles/voice.md
  grounded visuals        _craft/plot_generation.md   the look           _style/brand.md (Part A intent / Part B delivery)
  golden-output archive   _reference/internal/{blog,report,email}/  ← the REPORT slot is EMPTY, waiting for the first bottom-up

GENUINELY NEW (the real gap the owner named)
  a first-class CREATIVE & ACTIVATION layer — the hero-visual concept · the marketing punchline · the channel framing ·
  "what makes this a home run." We have prose-voice + grounded-craft, but no captured CREATIVE IDEATION per piece.
  THAT is the gap between "accurate grounded report" and "home run."
```

## 4 · The output home (the workshop) + the lifecycle

```text
A dedicated OUTPUT folder at the REPO ROOT (NOT inside docs/ — docs/ is stable methodology; outputs are volatile
Layer-3 renderings, and mixing them blurs the one seam that matters). We've outgrown docs/extra/ as the dump
(ENSO blog · Red Dog report · soon Anten + Brookfield). CLAUDE.md's "no folders until real implementation" is
satisfied — real outputs ARE the implementation.   Name: **studio/**  (owner pick, 2026-06-14).

LIFECYCLE:   studio/ (draft · iterate · carry the creative ideas — the WORKSHOP)
                │ when validated + we like it
                ▼
             _reference/internal/{report}/  (the curated form ARCHIVE — the MUSEUM, reused for form)
```

Each workshop file is a **self-contained brief**: the gated insight + the MCP comparison + a *Creative & Activation* section + pointers to brand/voice/craft — so it is **cloud-attachable** for rendering (attach the brief + the format-agnostic `_style`/`voice`/`_craft` → render), exactly the flow we set up with `brand.md` v0.2.

## 5 · The Creative & Activation layer (the new bit)

A captured section in each worked example (concrete so it isn't vague):

```text
CREATIVE & ACTIVATION
  hero visual     the ONE chart/image that lands the read (the grounded comparison, usually) — _craft rules apply
  punchline/hook  the headline that grabs — bounded by §6 guard 2 (catchy framing, NEVER an inflated claim)
  comparison      the MCP-grounded "vs peers / vs last year" framing that is both the moat and the hook
  channel notes   how it flexes by output: blog title vs report subject-line vs email one-liner
```

**Sequencing (prove-then-formalize, as always)**: capture the creative layer **per-example first** (it's specific — Anten's hurricane punch ≠ Brookfield's El-Niño-competitive hook); abstract the **reusable hook/visual patterns into `_craft` (or a new `_creative` layer) only after a few examples** prove the patterns. Don't build the shared creative layer ahead of evidence.

## 6 · The three accuracy guards (the moat's blast radius — non-negotiable)

This is where the lab is *most* tempted to drift from grounding-moat to content-farm. A "marketing punchline" folder without these would erode the exact moat we built.

```text
1. THE GATE STAYS UPSTREAM (P2)   the workshop holds RENDERINGS of VALIDATED insight + its creative dress — never the
                                  origin. Order is immutable: insight → GATE → render → creative. "Write the punchy
                                  version first" is the failure mode.
2. CREATIVE ≠ OVERCLAIM (the moat) the punch lands on the HOOK / title / framing / visual — NEVER on inflating a claim
                                  (voice.md §3: hyperbole never lands on a claim). No $/MWh, no causal-where-directional,
                                  the calibrated posture survives. FORM (quarantined from grounding) + bounded by
                                  blocked_claims. A catchy TITLE yes; a bigger NUMBER never.
3. THE HOOK IS GROUNDED            the home-run line ("you vs X") is an MCP comparison — real data, not invention. The
                                  creative layer AMPLIFIES a grounded comparison; it never manufactures one.
```

With these three: pieces that land *and* are defensible. Without them: how we lose the moat. They are first-class rules, not footnotes.

## 7 · The honest caution

It's not "don't" — it's that **the creative layer is the highest-drift-risk thing we've added.** Everything before it (resources, the gate, blocked_claims) was *grounding* discipline; this is the first layer whose job is to *persuade*. Done with §6's guards it's a force multiplier (home runs that survive scrutiny); done loose it's the content-farm we explicitly aren't. So the guards are the price of admission, and the reusable-method/prove-then-formalize discipline is the anti-sprawl rail.

## 8 · Decisions for you (before this becomes a plan)

1. **The output home** — name **settled: `studio/`** (repo-root, owner pick 2026-06-14). Still open: the **workshop → `_reference/internal/` gallery** lifecycle (promote-when-validated). *(Recommend the lifecycle as described.)*
2. **The creative layer** — per-example first, abstract reusable patterns into `_craft`/a new `_creative` layer only after a few examples? *(Recommend yes — prove-then-formalize.)*
3. **The three accuracy guards** (§6) — adopt as first-class rules (likely a short addition to `voice.md`/`output_contracts.md` + the workshop README)? *(Recommend yes — they're the moat guard.)*
4. **The first two worked examples** — **Anten** (ports → storm-surge/hurricane) + **Brookfield/Standard Solar** (solar → 12-mo El Niño + the competitive comparison), the meeting's deliverables, as the home-run proofs. Agree these two, in this order?
5. **Relationship to Phase 5** — reactivate/supersede the paused `layered_reference_v1` Phase 5 (bottom-up), enriched with the workshop + creative layer — or keep them separate? *(Recommend reactivate-and-enrich; it's the same work.)*
6. **Scope of the creative layer's "marketing"** — how far toward outreach/marketing do we go in the lab vs leave to the activation/business side? (The lab should stop at the *gated insight + creative brief*; actual send/outreach stays post-gate, human-in-the-loop — `use_cases.md` activation boundary.) Agree?

Pick any to start, or push back. When these settle, this becomes a plan (the workshop + the guards + Anten/Brookfield as the first home-run examples) in `../plans/` — and it's the natural successor to the paused Phase 5.

---

**See also**: `2026-06-14_outlier_method_red_dog.md` (the off-substrate bottom-up mode — the sibling) · `README.md` (what a discussion is) · `../architecture.md` (Layer 3 — the output surface this builds) · `../use_cases.md` (the bottom-up/top-down buckets + the activation boundary) · `../../resources/_style/output_contracts.md` §3 (the report contract) · `../../resources/_style/brand.md` (the format-agnostic look) · `../../resources/_principles/voice.md` (prose punch + "hyperbole never on a claim") · `../../resources/_craft/plot_generation.md` (grounded visuals) · `../../resources/_reference/internal/` (the golden-output gallery the workshop promotes into) · `../plans/2026-06-11_layered_reference_v1.md` Phase 5 (the paused bottom-up phase this reactivates) · `../principles.md` (P2 content-downstream · P6 references-inform).
