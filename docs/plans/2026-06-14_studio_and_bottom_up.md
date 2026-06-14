# Plan — `studio/` (the output half) + the first bottom-up home-run examples

> **Status**: **ACTIVE**, opened 2026-06-14 — **Phases 1–2 ✅** (studio/ stood up + guards baked; the 2 home-run briefs drafted, **for owner review**). Phase 3 deferred (its ≥2-example trigger is now met — revisit). Promoted from `../discussion/2026-06-14_bottom_up_output_workshop.md`. The lab's **output half**: stand up the **`studio/`** workshop + the **creative & activation layer** (with the moat guards), and produce the first **bottom-up** home-run examples. **Supersedes/enriches** `2026-06-11_layered_reference_v1.md` **Phase 5** ("crack bottom-up").
>
> **`studio` is a selective amplification lane — the *cherry on top*, not a mandatory stage** (owner, 2026-06-14): most outputs stay on the baseline path (gated insight → render); studio is opt-in for the pieces that must land as home runs, across all use-case types.

## 1 · What this is

```text
ONE effort → TWO things:
  (a) THE WORKSHOP + GUARDS    studio/ (the output home) + the creative & activation layer + the 3 moat guards
  (b) THE FIRST HOME RUNS      Anten + Brookfield/Standard Solar — in-substrate bottom-up, MCP comparison + creative layer
SEAM: the GATE. studio holds RENDERINGS of VALIDATED insight + their creative dress — never the origin (P2).
MOAT (bottom-up): the MCP-powered COMPARISON ("you vs peers over 12 months") — the grounded thing a vanilla LLM can't
  do, and the marketing hook. The creative layer AMPLIFIES a grounded comparison; it never manufactures one.
```

## 2 · Settled decisions (from the discussion §8)

| # | Decision | Resolution |
|---|---|---|
| D1 | **Output home** | **`studio/`** at repo root (owner pick). Lifecycle: `studio/` (draft + creative) → promote validated/liked ones to `_reference/internal/` (the form gallery) |
| D2 | **studio scope** | a **selective amplification lane** (the cherry) — opt-in, cross-use-case; **not** a mandatory stage; the baseline (gated insight → render) stands alone |
| D3 | **Creative layer** | capture **per-example first**; abstract reusable hook/visual patterns into `_craft` (or a new `_creative` layer) **only after** a few examples prove them (prove-then-formalize) |
| D4 | **The 3 accuracy guards** (first-class) | **gate stays upstream** (P2) · **creative ≠ overclaim** (punch on the hook/title/visual, never the number; `voice.md` §3) · **the hook is grounded** (the MCP comparison is real, not invented) |
| D5 | **First examples** | **Anten** (ports → storm-surge/hurricane) + **Brookfield/Standard Solar** (solar → 12-mo El Niño + the competitive comparison) — the meeting's deliverables, as the home-run proofs |
| D6 | **Phase 5** | this **supersedes/enriches** `2026-06-11_layered_reference_v1.md` Phase 5 (bottom-up) — same work, now with studio + the creative layer |
| D7 | **Where marketing stops** | the lab produces the **gated insight + the creative brief**; actual send/outreach stays **post-gate, human-in-the-loop** (`../use_cases.md` activation boundary) — studio does not automate distribution |

## 3 · The build (lean)

### Phase 1 — stand up `studio/` + bake the guards  ·  `cheap-docs`  ·  **status: ✅ DONE (2026-06-14)**

**✅ Landed**: `studio/README.md` (what studio is — the selective cherry · the lifecycle · the 3 guards) + `studio/_brief_template.md` (the cloud-attachable brief: §1 gated insight · §2 the MCP comparison · §3 Creative & Activation · §4 render notes — the guards inline) + the **3 guards baked into the form layers** (`_style/output_contracts.md` §5 + `_principles/voice.md` §6, both versioned). The baseline path is untouched; studio is the opt-in cherry.

```text
DELIVERABLES
  · studio/README.md — what studio IS (the selective cherry · the lifecycle · the brief template) + the 3 guards (D4)
  · the BRIEF TEMPLATE — a self-contained, cloud-attachable output brief:
      gated insight (+ source_refs) · the MCP comparison · a "Creative & Activation" section
      (hero visual · punchline/hook · comparison framing · channel notes) · pointers to brand/voice/craft
  · bake the 3 guards as first-class rules — a short add to _principles/voice.md + _style/output_contracts.md
    (so the guards travel with the form layers, not just this plan)
ACCEPTANCE  studio/ exists with the brief template + lifecycle; the 3 guards are first-class in the form layers;
            an output brief is cloud-attachable (attach brief + format-agnostic brand/voice/craft → render).
            NO example built yet.
```

### Phase 2 — the first home-run examples (Anten · Brookfield/Standard Solar)  ·  `moderate–heavy`  ·  **status: ✅ DONE (drafted 2026-06-14, for owner review)**

**✅ Landed (2026-06-14)** — built in parallel via the `studio-phase2-examples` workflow; both held the 3 guards (gate-upstream · creative≠overclaim · grounded-hook):
- **`studio/brookfield_standard_solar.md`** — the substrate **overturned** the brief's premise (Standard Solar is a DG/community-solar book — 129 plants, 2.81 MW each, only ~23% in the El-Niño-sensitive Southwest), and the agent let the data win: the *reversal is the hook* ("a strong El Niño is coming; most of this book won't feel it"). The MCP comparison (plant-count peer class) is grounded; magnitude withheld; gate PASS. A clean home run.
- **`studio/anten_ports.md`** — **"Anten" was unresolvable** as a named company (the agent refused to substitute a near-name — disclosed as a finding) → pivoted to a *grounded* **Galveston Bay / Houston Ship Channel** surge-corridor read (~3.7 GW ERCOT gas in one ~3.4 km cell via `nearby_plants`). Proves the **COASTAL** outlier class; the $/EAL/forward-probability all blocked.

New MCP gaps logged: **R14** (geometry-seeded nearby query) · **R15** (elevation/surge/flood-zone field) · R13 extended. **Two findings for the owner**: (1) Anten needs its real identity (or rename the brief to the Galveston coastal read); (2) Anten is the **2nd outlier after Red Dog → the `outlier_playbook` formalize-trigger is now met** (a decision, not done).

```text
DELIVERABLES
  · Brookfield/Standard Solar — in-substrate bottom-up: resolve the fleet (plants_by_owner / search_plants), build the
    COMPETITIVE COMPARISON (the moat + hook), the 12-mo El Niño exposure read (compose the el_nino_enso resource), gate,
    + the Creative & Activation layer → a render-ready brief in studio/.
  · Anten — ports acquisition: FIRST check the substrate footprint (ports may be partly OFF-substrate → a hybrid using
    the outlier playbook for the ports piece + MCP for any in-substrate energy assets); storm-surge/hurricane exposure;
    gate; creative layer → a brief in studio/.
  · every claim sourced + gated; the comparison MCP-grounded; the punch on the hook never the number (D4); honesty intact.
ACCEPTANCE  two render-ready bottom-up briefs in studio/, each a home run AND defensible (the comparison grounded, the
            guards held); the best promoted toward _reference/internal/report/. The studio pattern proven on 2 examples.
```

### Phase 3 — abstract the reusable creative patterns  ·  **status: ☐ DEFERRED (trigger: ≥2–3 examples done)**

```text
Lift the recurring hook/visual patterns from the examples into _craft (or a new _creative layer). Don't build ahead of
the examples — prove-then-formalize (D3).
```

## 4 · Scope guards

```text
1. THE 3 ACCURACY GUARDS (D4) apply to every studio piece: gate-upstream · creative≠overclaim · grounded-hook.
2. STUDIO IS SELECTIVE (D2) — the cherry, not a gate; don't route every output through it; the baseline path stands.
3. DON'T REBUILD THE BASELINE — studio composes the EXISTING form layers (_style/voice/_craft/_reference); it adds the
   creative-ideation capture, not a parallel rendering stack.
4. MARKETING STOPS AT THE BRIEF (D7) — no send/distribution automation; activation stays human-in-the-loop, post-gate.
5. PROVE-THEN-FORMALIZE — the shared creative layer (Phase 3) waits for the examples to prove the patterns.
```

---

**See also**: `../discussion/2026-06-14_bottom_up_output_workshop.md` (the discussion this resolves) · `README.md` (plan lifecycle) · `2026-06-11_layered_reference_v1.md` Phase 5 (the paused bottom-up phase this supersedes) · `../architecture.md` (Layer 3) · `../use_cases.md` (bottom-up/top-down + the activation boundary) · `../../resources/_style/output_contracts.md` (the report contract) · `../../resources/_style/brand.md` (format-agnostic look) · `../../resources/_principles/voice.md` (prose punch + "hyperbole never on a claim") · `../../resources/_craft/plot_generation.md` (grounded visuals) · `../../resources/_reference/internal/` (the gallery studio promotes into).
