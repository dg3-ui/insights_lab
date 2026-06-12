# Plan — Layered Reference v1: shared layers · output contracts · the rubric

> **Status**: **ACTIVE**, opened 2026-06-11 — **Phases 1–4 CLOSED 2026-06-12** (1: probe passed · 2: renders verified on-brand · 3: forecast-fan refusal verified · 4: corpus populated [3 Grid Status exemplars + 1 prompt exemplar, two reference *kinds* established], unprompted-structure render + non-ENSO smoke both passed; **corpus stays open for intake** — owner's website/LinkedIn/Substack list lands later, ledgered in `_reference/README.md` Pending Intake). Next: Phase 5 (crack bottom-up — the Divy × Daniel iterate-and-compare). Adversarially reviewed (3 lenses) 2026-06-11; findings folded in.
>
> **Owner**: Divy. Collaborator: Daniel (bottom-up iterations, Phase 5).
>
> **What it is**: the restructure of `resources/` from "one phenomenon package carries everything" to **shared cross-cutting layers + method-only packages**, plus the three capabilities the iteration loop proved we need: **typed output contracts** (direction × audience × format), a **brand/styling kit**, and a **canonical judging rubric** with a bounded self-critique pass.
>
> **Presentation cut (2026-06-12, 2pm)**: the deadline does not wait for phase closure. **DRAFT-marked** versions of `rubric.md` + `voice.md` (Phase 1) and `brand.md` + the `top_down` blog cell (Phase 2) may land ahead of their phases as a one-time exception; tonight's bottom-up iterations are scored against the draft rubric. Each phase still **closes** serially afterward — closure = acceptance met **and** that phase's canon amendments landed.
>
> **What follows this plan**: the **client-specific Prashant & Ross lead-gen work** (collab-thread decision 2026-06-11). The `bottom_up × client` cells and the D3 DOCX export contract are deliberately designed as its on-ramp.
>
> **Grounded in**: the Daniel collab thread (decisions of 2026-06-09/11), test run 001 (PASS), and a full canon sweep + 3-critic adversarial review (2026-06-11) across `docs/00–11`, `resources/`, the `el_nino_enso` package, `templates/`, commands, and agent files. Brand values pulled from the live infrasure.ai web app (`renewablesinfo_org/web`).
>
> **How to read it**: §1 decisions are settled — do not re-litigate per phase. §4 is the ladder; execute **one phase at a time**, land each phase's canon amendments with it, close the phase, then start the next. One standing exception: **raw-material gathering is a parallel human track** (Phase 5 iterations, exemplar collection) — only *deliverables* wait for their phase.

## 0 · Why — what the iteration loop taught (2026-06-09 → 11)

The manual loop (MCP on cloud + the ENSO folder in a claude.ai project + prompting) produced its first real outputs, and the review against them taught four things:

```text
1  QUALITY = REFERENCES + STRUCTURE   top-down cracked the moment it had reference
                                      blogs (Grid Status) + structural cues. Fix: bake
                                      them into the reference so quality is automatic.
2  THE OUTPUT IS NEVER TYPED          no session declares direction · audience · format,
                                      so the model defaults to one shape. The matrix in
                                      docs/11 exists on paper; nothing operationalizes it.
3  EVERYTHING NEW IS CROSS-CUTTING    rubric · voice · brand · plot craft · exemplars apply
                                      to ENSO, grid studies, drought — all of it. None of it
                                      belongs inside a phenomenon package.
4  BOTTOM-UP IS A MISSING-EXEMPLAR    the weak bottom-up output was a generic plant profile.
   PROBLEM, NOT A STYLE PROBLEM       top-down had Grid Status to imitate; bottom-up has no
                                      exemplar anywhere — it must be AUTHORED (Phase 5).
```

And one standing discipline: **no microprompting**. We give the model direction, references, and constraints — not token-level scripts. That is `08` P1 made operational: the methodology stays tight; the phrasing stays free.

## 1 · Settled Decisions

| # | Decision | Detail |
|---|---|---|
| **D1** | **The rubric is 5 criteria, with a pinned scoring shape** | `format · relevancy · usefulness · accuracy (with calibration — "smartfulness" — as its defining clause) · presentability`. Matches the 2026-06-11 collab decision. Scoring shape: **each criterion scored `pass / flag / fail` per artifact** (simple enough for two humans to apply independently). The rubric is a **scoring layer on top of** the binary pass/fail gate in `docs/05` — never a replacement for it. Accuracy-with-calibration *cites* the existing machinery (`03` confidence rules, `blocked_claims`, `02` Q&A grammar Q4/Q5); it does not restate or compete with it. The rubric also does not replace the **with/without proof-of-value method** (`11` §Validation) or the three-bucket prompting framework: rubric = "is this artifact good"; with/without = "is it unreachable without us"; bucket #3 = the testing lens. All three coexist, said explicitly in `rubric.md`. |
| **D2** | **Self-critique is bounded, split, and two-stage** | The model may run **1–2 self-critique iterations, style criteria only; accuracy is never self-judged** — it is reviewed claim-by-claim against source refs by the human checkpoint (later: independent `/gate-check`; the `06` §9 self-policing weakness is fixed by *independence*, not more self-review). Two stages, because `_style` only loads post-gate (D6): **pre-gate** self-critique checks *skeleton conformance only* (the 9-section insight structure — not prose polish; polishing an ungated draft is exactly the P2 pull we refuse); **post-gate** self-critique checks the render against its contract cell (format + presentability proper). All critique turns are saved in the transcript. |
| **D3** | **Rendering: HTML artifact canonical, DOCX as export contract** | **Refined 2026-06-12 (owner): Inter is the primary family** for insight documents — hierarchy via weight/size/optical-size *within* Inter; JetBrains Mono for data; Fraunces stays a marketing-site face, not used in documents. The styled rendering is an **HTML artifact** (brand fonts/palette/logo, renders inline in claude.ai during the loop). Font delivery inside the artifact sandbox is an **execution assumption to verify in Phase 2** — `brand.md` must name the mechanism (CDN link vs vendored) *and* the degradation fallback stack; if in-sandbox fidelity fails, that detail lands on ledger R7, not in styling prompts. **DOCX** is a named **export contract** for account-facing deliverables (BD handoff for the Prashant & Ross successor work; font fidelity depends on recipient — derived from the same brand kit, never a second styling truth). Markdown remains the **gate-stage** format: the applied-insight draft is and stays a markdown object; styling happens only at render. |
| **D4** | **Four shared layers, underscore-prefixed; packages keep ONLY the method** | `resources/_principles/` (rubric · voice · altitude) · `_style/` (brand kit · output contracts) · `_craft/` (plot generation) · `_reference/` (exemplar corpus, exists). The `_` prefix is generalized from `_reference/` precedent: **non-domain, non-package shared layer** — no `resource.yml`, no slug, exempt from `folder == slug`, excluded from the publish scan (`07` §3 — amendment lands in **Phase 1**, with the rule itself), registered in a separate Shared Layers table in `resources/README.md`, never a `SkillIndexRecord`. |
| **D5** | **Composition is session-level, not bundled** | A session composes `phenomenon method + _principles (+ post-gate: _style contract + _craft + _reference)`. Published skills stay self-contained (`07` §8: bundled paths are relative to the slug folder — no `../../_style/`). This mirrors the existing doctrine: *"persona is a view, not a storage axis"* (`resources/README.md`) — so is a styled output. |
| **D6** | **Stage placement** | `_principles` loads at **draft/test and stays loaded through render** (voice and altitude shape the insight; the rubric — a `_principles` artifact — is applied at the post-gate score; phrasing hygiene is cheaper applied at draft than retrofitted at render — a decision, not an accident). `_style`, `_craft`, `_reference` load at **render only, post-gate** (`_reference` additionally feeds **eval**). "Output contract declared" at test start means **naming the `(direction, audience, format)` tuple** — not loading `_style`. The `docs/05` Avoid-list and the `test-resource` guardrail are **reworded together (Phase 1)** to ban *un-gated* rendering specifically — the gate order `insight → gate → render` (`08` P2) is stamped as a precondition on **every** output contract. |
| **D7** | **One format vocabulary** | Canonical format enum: **`blog · brief · email · post`**. Contract key: `direction(top_down|bottom_up) × audience(internal|client|public) × format`. Direction reuses the `02` §Exposure axis wording. Audience **refines** `11`'s two-level layer (customer/public → `client | public`) — `11` is amended to carry the split (Phase 2). Mappings: `account_note`/`portfolio_note` → **brief** · `informative_email_draft` → **email** · `platform_card`/Ask answer → **platform rendering, post-v0** (stays on the roadmap; `actor_relevance` entries keep it as `platform (post-v0)`, not a contract cell) · **vlog** (`01`/`11` "internal vlog", the Thursday-deliverable shape) → **a narration-script variant of the `top_down × internal × brief` cell** (the video itself stays out of scope). `10`'s `/render` row ("blog/email/card/post"), `06` Layer 3, `00` §2, and the CLAUDE.md/AGENTS.md Layer-3 lines are amended to match (Phase 2). |
| **D8** | **FORM joins the input-job labels** | The label rule ("label every input's job before citing it") gains **FORM — shapes the rendering; never grounds, frames, or routes a claim** (no ordinal — the label lists differ in length across files). `_reference`/`_style`/`_craft` material is never a valid `source_ref` (any type, any role). A claim grounded in an exemplar is a **blocked claim**, same severity as the descriptive-context trap (`04`). |
| **D9** | **Versioning, lightweight** | Each shared layer carries `version` in its README Status line. A test run records the shared-layer versions it composed (new template fields). A shared-layer change is a staleness signal for dependent resources (`03` note) — no `resource.yml` schema change in v1. |
| **D10** | **No code, no new tools — log instead** | Everything ships prompt/spec/asset-level inside `resources/` (an `.html` skeleton and vendored logo SVGs are brand **assets**, not `code/`). Executable rendering/export tooling and MCP-served brand assets are **ledger entries** (`09` R6/R7), not v1 builds. |
| **D11** | **A contract cell is an envelope, not a straitjacket** | A cell fixes the envelope: length band · tone · rendering target · gate guard · what NOT to include. **Inner structure flexes by analysis family and granularity** (one asset vs portfolio vs fleet), resolved by the method package + family-tagged exemplars — that's the no-microprompting discipline applied to formats. The contract template carries a `family/granularity notes` field for exactly this. |

## 2 · Target Architecture

```text
resources/
├── README.md                 registry: domains table + NEW Shared Layers table + underscore rule
├── _principles/              HOW WE JUDGE & SPEAK          loads at DRAFT + RENDER
│   ├── README.md             role · version · feeds
│   ├── rubric.md             the 5 criteria · pass/flag/fail scoring · the D2 two-stage
│   │                         self-critique bounds · relation to with/without validation (D1)
│   └── voice.md              house voice · humanization (no m-dashes, no AI tells) ·
│                             anti-microprompting doctrine · altitude ("smartfulness") rules
├── _style/                   HOW IT LOOKS & SHIPS          loads at RENDER only (post-gate)
│   ├── README.md             role · version · feeds
│   ├── brand.md              fonts (Fraunces/Inter/JetBrains Mono) + delivery mechanism &
│   │                         fallback stack (D3) · palette (brand green/amber, fuel-type
│   │                         chart colors) · logo usage · provenance (web app, dated)
│   ├── brand_assets/         vendored lockup SVGs + artifact skeleton .html
│   └── output_contracts.md   the direction × audience × format matrix; per cell: envelope
│                             (D11) + family/granularity notes + rendering target +
│                             GATE PRECONDITION stamped on every cell
├── _craft/                   HOW ANALYTICS ARE DRAWN       loads at RENDER only (post-gate)
│   ├── README.md             role · version · feeds
│   └── plot_generation.md    chart-type selection by analysis family · brand palette inherited
│                             from _style · grounded-plot rules (source_ref + as_of per series) ·
│                             blocked plots (no forecast $/MWh, no plant-level forecast curves)
├── _reference/               WHAT GOOD LOOKS LIKE          feeds RENDER + EVAL only (exists)
│   └── (populated: Grid Status · Substack grid-studies · authored bottom-up exemplar)
└── weather_and_climate/
    └── el_nino_enso/         METHOD ONLY — what to retrieve · how to reason · what to claim ·
                              what to refuse  (persona/format boilerplate re-pointed to layers)
```

```text
THE COMPOSED SESSION (runtime view — extends 06 Layer 2. Layer 0 gains non-package shared
folders and the 0→1 publish scan gains an underscore exclusion; Layer 1/serving is unchanged.)

  DRAFT/TEST:   method (prompt_projection + knowledge) + _principles ──► applied-insight draft
                contract tuple DECLARED (named, not loaded — D6)           (markdown, 9-section)
                loop: enrich · re-scope · challenge (08 P4)                       │
                self-critique stage 1: skeleton conformance only (D2)             │
  GATE:         human checkpoint — claim-by-claim vs source refs + blocked_claims │
                                                                                  ▼
  RENDER:       + _style contract(direction × audience × format) + _craft + _reference
                self-critique stage 2: render vs contract cell (1–2 iterations, D2)
                rubric scored, all 5 criteria, pass/flag/fail ──► recorded in the test_run
                ──► HTML artifact (canonical) · DOCX export (account-facing) · markdown (internal)
```

## 3 · What Must Not Move (guardrails carried from the sweep)

- **`blocked_claims`, `confidence_rules`, `caveats` stay per-resource** (`03`): the rubric never centrally overrides them; the ENSO cap ("DIRECTIONAL, LOW … Never a number", `knowledge.md` §6) binds `_craft` too — no chart may plot what a claim may not say.
- **Gate before render, on every branch**: every output contract carries the `(only after review_trace passes)` guard verbatim; `/render` (when built) refuses ungated input (`10`).
- **The projection stays minimal** (`03`: "the minimal instruction surface") — shared layers compose at session time, never inline into `prompt_projection.md`.
- **`_reference` quarantine is load-bearing for Phase 4**: Grid Status / Substack material is full of real grid numbers — intake step 3 ("strip or clearly mark any factual claims") is executed per exemplar, and `02`'s bar is untouched: exemplar **form** is welcome; exemplar **topics** still need an InfraSure entity/ID/field to stand up.
- **The test stays a resource-shape test** (`05`): the style criteria are *fully* judged only on the post-gate render; pre-gate critique is skeleton-conformance only (D2) — the rubric does not convert the protocol into a content-pipeline test.
- **No `code/`/`scripts/`/`data/`, no new MCP tools, no publish step** — unchanged v0 pauses; gaps go to `09`.

## 4 · The Phase Ladder

| Phase | Name | Delivers | Status |
|---|---|---|---|
| 1 | Foundation: underscore rule + `_principles` | rubric · voice · shared-layer conventions + protocol/command hooks | ✅ 2026-06-12 |
| 2 | `_style`: brand kit + output contracts | brand.md · assets · contract matrix · D7 vocabulary lands canon-wide · R6/R7 | ✅ 2026-06-12 |
| 3 | `_craft`: the plot skill | plot_generation.md + plot quarantine clauses | ✅ 2026-06-12 |
| 4 | Populate `_reference` | Grid Status + Substack exemplars, annotated + non-ENSO smoke check | ✅ 2026-06-12 (open intake: owner's list pending) |
| 5 | Crack bottom-up | authored bottom-up exemplar + filled bottom-up contract cells + DOCX smoke | ☐ |
| 6a | Rewire: package + command/canon lockstep | el_nino_enso re-pointing · remaining lockstep · doc-audit pass | ☐ |
| 6b | Revalidate: the composed test run | composed run PASS · rubric scored · extracted | ☐ |

### Phase 1 — Foundation: the underscore rule + `_principles/`

**Goal**: the judging and voice layer exists; the registry and discovery spec know what a shared layer *is*; the test protocol knows where rubric scores land.

Deliverables:
- `resources/_principles/README.md` — role, version, what it feeds, stage placement (D6).
- `resources/_principles/rubric.md` — the 5 criteria (D1), each defined by **citation into existing canon** (accuracy-with-calibration ← `03` confidence ladder + `blocked_claims` + `02` grammar Q4/Q5; relevancy/usefulness ← Q6; format/presentability ← render-stage, explicitly **subordinate** to `03`'s "If any item fails, the resource is not ready — however well it reads"). Pass/flag/fail scoring shape. The D2 two-stage self-critique bounds (1–2 iterations, style only, stage 1 = skeleton conformance, stage 2 = contract conformance, turns saved). The D1 reconciliation: rubric vs with/without validation vs prompting-bucket #3.
- `resources/_principles/voice.md` — house voice; humanization rules (**no m-dashes**, no AI-tell constructions); altitude/"smartfulness" (no false precision — an exact unmodeled number invites the question mark it can't survive; no generic mush — `08` P5); the anti-microprompting doctrine (direction + references + constraints, never scripts).

Canon amendments (land with this phase):
- `resources/README.md` — generalize the `_reference` sentence into the **underscore-folder rule**; add the **Shared Layers table** (Layer · Role · Feeds · Status — separate from the resource registry, which keeps its Domain/Family/Actors columns); scope "materialize on first resource" to domains; draw the new tree.
- `docs/07_discovery_spec.md` §3 + `docs/06_architecture.md` §8/§13 #6 — the publish scan **excludes `_`-prefixed folders** and the `folder == slug` assertion applies to packages only (lands here because the rule lands here, per D4; 06's publish-assertion language gets the same one-line exclusion so the two specs never disagree).
- `docs/03_methodology_resource_standard.md` staleness_signals — one line: a composed shared-layer version change is a staleness signal for dependent resources (D9; lands with the template's D9 fields).
- `docs/05_mcp_test_protocol.md` — pre-test checklist gains "shared layers loaded"; flow inserts the **stage-1** self-critique + rubric-scoring steps **between claim review and transcript save**; **pass/fail stays the gate, rubric is scoring on top**; failure taxonomy gains two rows (`style/contract gap`, `craft/plot gap`); Avoid-list reworded to ban **un-gated** rendering specifically. *(The "output contract declared" checklist line moves to Phase 2 — it must not land before contracts exist.)*
- `.claude/commands/test-resource.md` — the guardrail line reworded in lockstep with the `docs/05` Avoid-list (thin-conductor doctrine: a command may not contradict the canon it conducts for five phases).
- `templates/mcp_test_run.template.md` — lockstep: 5-criteria score fields, self-critique delta, composed shared-layer versions (D9). *(The "declared contract" field moves to Phase 2.)*
- `docs/04_context_and_data_map.md` — add the **FORM** job (D8) to the input-layer table + the source-ref quarantine sentence; generalize the activation boundary from "email copy" to "any contract format" pre-gate.
- `docs/00_project_brief.md` §4 RULE A + `docs/learning/02` — the label list gains FORM (the teaching home moves in lockstep with the rule).
- `CLAUDE.md` + `AGENTS.md` — label-rule gains FORM; underscore convention + composition rule added (mirrored, per AGENTS lockstep).

Acceptance (concrete probe): in a fresh session loaded with `_principles` + the ENSO projection, asking (a) which criteria it may self-critique and at which stage, (b) which it must never self-judge, (c) where scores are recorded — yields answers matching `rubric.md`'s D2 bounds and the template's score fields, with no other prompting.

### Phase 2 — `_style/`: brand kit + output contracts

**Goal**: a declared `(direction, audience, format)` resolves to one contract cell that fixes the envelope (D11) — and the rendering carries the brand. The D7 vocabulary lands **everywhere it appears**, in one phase.

Deliverables:
- `resources/_style/brand.md` — fonts + roles (Fraunces display / Inter body / JetBrains Mono data-mono), **font delivery mechanism + degradation fallback stack** (D3), palette (brand green `oklch(0.72 0.18 155)`, amber `oklch(0.78 0.15 75)`, the fuel-type chart colors, light/dark), logo usage (lockup variants), box/radius idiom — **provenance stamped**: pulled from `renewablesinfo_org/web` (`globals.css`, `layout.tsx`, `brand.ts`), dated 2026-06-11; the web app remains the source of truth, this file is the vendored projection.
- `resources/_style/brand_assets/` — lockup SVGs (on-light/on-dark) + `artifact_skeleton.html` (the canonical HTML-artifact shell: fonts per the D3 mechanism, palette vars, header with lockup, source-attribution footer).
- `resources/_style/output_contracts.md` — the matrix (D7), cells as envelopes (D11) with `family/granularity notes`. Filled now: **top_down × public × blog** (codify exactly what cracked: catchy title · subtitle · summary block · the 4–5 structural moves real blogs make · grounded-chart slots), **top_down × internal × brief** (+ the **vlog narration-script** variant, D7), **bottom_up × internal × brief** (stub, marked "fills in Phase 5"), **bottom_up × client × email** (stub + the post-gate precondition in bold — the P&R on-ramp). Every cell: gate precondition · rendering target (D3) · length band · what NOT to include.
- `templates/output_contract.template.md` — so future cells are added in one shape.

Canon amendments:
- `docs/05` pre-test checklist + `templates/mcp_test_run.template.md` — the deferred "output contract declared (tuple named)" line and "declared contract" field land now, with the artifact they describe.
- `docs/09_mcp_roadmap.md` — append **R6** (brand/logo assets not served via MCP; workaround: vendored in `_style/`; roadmap: serve brand kit as MCP resources) and **R7** (no rendering/export tool — HTML artifact hand-rolled per session, DOCX exported manually; any in-sandbox font-fidelity limit recorded here; roadmap: a render/export tool) in the six-field form.
- **D7 vocabulary sweep, one pass**: `docs/10` `/render` row (formats + conducted canon gains `_style`/`_craft`; `/gate-check` row gains `_principles` + the D2 split) · `docs/06` Layer 3 list + §4 sequence-diagram tail + §10 mapping · `docs/00` §2 content-engine line · `CLAUDE.md`/`AGENTS.md` Layer-3 lines.
- `docs/11_use_cases.md` — audience layer refined (customer/public → `client | public`); the contract matrix cited as the operationalization of the bucket × audience grid; a one-line cross-ref distinguishing the rubric (artifact quality, `_principles`) from §Validation's with/without method (moat proof — D1); **the test-001 direction reconciliation**: 001 was a phenomenon→fleet scan = *top-down* by `11`'s own definitions, while `01`/`11` label V0 "Bucket 1 bottom-up" — amend the wording (001 re-classified top_down; the bottom-up slice is what Phase 5 completes).
- `docs/01_scope_v0.md` — the V0-slice parenthetical + After-V0 activation-track vocabulary updated to point at this plan (the boundary "top-down/customer renderings are post-V0" is superseded *by this plan, deliberately* — silence is not).
- `docs/02_analysis_catalog.md` — §Exposure direction parenthetical cited as the contract's direction key (one shared axis across 02/11/_style).

Acceptance: test 001's ENSO insight re-rendered through `top_down × internal × brief` and the blog cell produces on-brand HTML artifacts with zero manual styling prompts, **and the artifact demonstrably renders the three brand fonts (or brand.md's named fallback stack)**.

### Phase 3 — `_craft/`: the plot-generation skill

**Goal**: an analytic chart is a first-class, *grounded* rendering element — never decoration, never an ungated claim.

Deliverables:
- `resources/_craft/README.md` + `plot_generation.md` — chart-type selection guide keyed by analysis family (`02` idiom: each entry carries a "Claim type" line stating what is blocked); brand palette + fuel-type colors inherited from `_style` (cite, don't copy); **grounded-plot rules**: every plotted series carries a `source_ref` (substrate|external) with `as_of` — a plot is a set of claims and obeys the claim grammar; **blocked plots** mirror blocked claims (no forecast $/MWh, no plant-level production forecast curves, no exemplar-derived data); runtime guidance for HTML-artifact charts (inline SVG/recharts-style) and analysis-tool fallbacks.
- Incorporate the user-supplied plot material when it arrives (named input; the skill ships without blocking on it).

Canon amendments: `docs/03` blocked-claim examples gain a form-layer entry (no chart of an ungrounded number); `docs/04` source-ref section notes plots inherit the per-series discipline.

Acceptance: a test render produces one chart whose every series traces to a tool result with `as_of`, in brand colors, and refuses a requested forecast-price chart.

### Phase 4 — Populate `_reference/`

**Goal**: top-down quality is automatic because the form corpus rides in the reference, not in manual prompts.

Deliverables: 3–6 exemplars (Grid Status blogs; 1–2 Substack grid-studies; the strongest day-one top-down output as an internal exemplar) — each through the existing 4-step intake (provenance who·where·when·URL · the **specific form lesson** · claims stripped/marked · excerpt+link, no scrapes), tagged with the analysis family it exercises and the contract cell it exemplifies.

Canon amendments: `_reference/README.md` purpose/contents/feeds updated (rubric + `_style` named as consumers; "✗ NOT the grounding layer" verbatim); `docs/02` "What This Rules Out" gains the one-line form-vs-topic distinction.

Acceptance: a top-down blog render with the corpus loaded needs **no** structural instructions in the prompt, and no exemplar fact appears in any `source_ref`. **Plus the non-ENSO smoke check**: a structural outline (form only — no claims, no method package) for a grid-study-style blog, produced from the shared layers + corpus alone, confirming the layers carry no ENSO-shaped assumptions.

### Phase 5 — Crack bottom-up

**Goal**: the missing exemplar exists, authored by us; the bottom-up contract cells stop being stubs.

Method (the same move that cracked top-down, run deliberately): Divy and Daniel **independently generate iterations** of the bottom-up read (one asset / one portfolio, ENSO), score each against the rubric, extract what worked into (a) an authored bottom-up exemplar in `_reference/` and (b) the filled `bottom_up × internal × brief` and `bottom_up × client × email` cells. The anti-target is explicit: **not a generic plant profile** (available elsewhere, not backed by method) and **no unmodeled "X% loss" figures** — exposure read, mechanism, actor relevance, caveats. (Iteration *capture* may run from day one as the standing parallel human track; the cells land here.)

Acceptance: a bottom-up output that **passes the `docs/05` gate** AND both authors independently score **pass on all 5 criteria**, produced from the contract + exemplar with no manual structural prompting — **plus one DOCX export smoke-test** of the client-facing cell (the P&R on-ramp ships tested, or its limits land on R7).

### Phase 6a — Rewire: package + remaining lockstep

**Goal**: the first package composes the layers; every doc and command that still describes the pre-layer reality stops doing so.

Deliverables:
- Package edits: persona line → cites `_principles/voice.md`; `## Output format` sections (projection + SKILL.md) keep the 9-section **insight** skeleton and gain the one-line "rendering is downstream via `_style`" note; `resource.yml` — `include_in_prompt` "output format" → contract reference, `exclude_from_prompt` "email drafting instructions" → "rendering instructions load only post-gate via `_style`" (as written it forbids ever loading the email contract); `actor_relevance[].renderings` re-keyed to D7 (`account_note`→brief, `informative_email_draft`→email, `platform_card`→`platform (post-v0)`); SKILL.md bundled-references table notes session-level composition (D5); package README files-table updated.
- `examples/applied_insight_001.md` — **grandfathered** as the pre-composition baseline (like test 001); the composed run's output (6b) becomes `examples/applied_insight_002.md` and SKILL.md's "target output shape" pointer moves to it.
- Command/canon lockstep (remainder): `new-resource` (engine diagram + read-list + Phase-3/4 wording) · `extract` (rubric-findings bucket + "candidate `_principles`/`_style` edits" feed target) · `test-resource` STEP 2 ("projection's output format" → insight skeleton vs. contract distinction) · **`docs/10` full registry status sweep** (`/recap` ✅-but-missing → restore or correct, *and* `/test-resource`/`/extract` ◑-but-built → built; reconcile README.md repo map + CLAUDE.md command list in the same pass) · `docs/07` §8 session-composition note · `docs/06` Layer 2 composed-session note + §9 cross-ref to the D2 split · `docs/03` Resource Package composition rule + the two-renderings paragraph → contract matrix · `docs/learning/03` + `docs/learning/04` companions (the projection-anatomy table, the `exclude_from_prompt` quote, and the "no other repo files loaded" review rule gain the session-composition carve-out) · repo `README.md` (map · read order · working rules).

Acceptance: a doc-audit pass over the contributor read path (README → 01 → learning → package) finds **zero** pre-layer descriptions.

### Phase 6b — Revalidate: the composed test run

**Goal**: the PASS baseline is re-earned under composition.

Deliverables: **the composed test run** — this *is* the "second ENSO test run done the new way" the README already calls for: contract tuple declared, full transcript saved (both self-critique stages in it), gate passed, rubric scored, resolved via `/extract` into `test_run_00N` + learning log + any new `09` entries; output promoted to `examples/applied_insight_002.md` (per 6a). Test 001 stays as the pre-composition baseline record.

Acceptance: the composed run PASSes the gate and is rubric-scored and extracted; the run's record carries the composed shared-layer versions (D9).

## 5 · Sequencing Notes

- **The presentation cut (see Status block)** is the deadline exception (the parallel gathering track below is the other sanctioned one): DRAFT rubric/voice/brand/blog-cell artifacts may exist before their phases close, because the 2026-06-12 2pm presentation and tonight's scoring need them. Phase *closure* — canon amendments + acceptance — still happens serially afterward; the DRAFT mark comes off at closure.
- **Raw-material gathering is a standing parallel human track** (also in the header rule): Phase 5 iteration capture and Phase 4 exemplar collection may run from day one; only their *deliverables* wait for their phase.
- Phase 6 was split (6a/6b) so the ladder can close incrementally: rewiring is a doc session; revalidation is a live MCP session. Rewiring before the layers stabilize would churn the only validated artifact we have — hence last.
- **After this plan**: the client-specific Prashant & Ross lead-gen work (its own plan; the `bottom_up × client` cells, DOCX export, and the actor-relevance routing are its designed on-ramp).

---

**See also**: `README.md` (this folder's rules), `../11_use_cases.md` (the bucket × audience grid the contracts operationalize), `../08_design_principles.md` (P1/P2/P4/P5 — the constraints this plan executes inside), `../06_architecture.md` §9 (the self-policing weakness D2 respects), `../05_mcp_test_protocol.md` (the loop every phase's outputs run through), `../09_mcp_roadmap.md` (R6/R7 land in Phase 2).
