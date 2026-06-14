V# Discussion — Architecture Lessons from `anthropics/financial-services` (adopt · adapt · defer · reject)

> **Status**: **RESOLVED-INTO-PLAN** (`../plans/2026-06-13_knowledge_base_expansion_v1.md`), 2026-06-14 — opened 2026-06-13, **deepened 2026-06-13** with the *intelligence-layer reframe* (§2); its verdicts now live in the plan (kept here as the record of *why*). Grounded in a direct read of the cloned repo (`.financial-services`) — verified counts, a real `SKILL.md`, the `market-researcher` agent prompt — **and** a direct re-read of our own system (`architecture.md`, `principles.md`, `method/analysis_families.md`, `method/discovery_spec.md`, the ENSO `prompt_projection.md`).
>
> **The question**: we stepped outside the lab to study how a big-firm, high-signal repo packages analyst methodology. `anthropics/financial-services` is the closest structural analog. **What is right for us to adopt, what is not, and why — then what to do now vs. defer.**
>
> **The frame that governs the whole doc** (`../principles.md` P6): this repo is a **reference, not a mandate**. It earns a borrow only by making InfraSure better. Where our instinct is already sharper, we keep ours. We are not behind and copying up; we are mining a richer-scale repo for the few patterns that transfer.
>
> **Companion**: `2026-06-13_expanding_the_knowledge_base.md` (the KB-expansion discussion). Several conclusions here feed directly into its §3 (domain tree) and §4 (grain).

## 1 · What the repo actually is (verified, not paraphrased)

`anthropics/financial-services` packages financial-analyst work as **installable Claude plugins + deployable managed-agent cookbooks**. The load-bearing pattern:

```text
source method  ──►  packaged plugin  ──►  optional headless managed-agent wrapper  ──►  human-reviewed output
   (SKILL.md)        (vertical/agent)        (agent.yaml + subagents)                    (artifact)
```

Verified local shape:

| Surface | Count | What it is |
|---|---:|---|
| Vertical plugins | 7 | `financial-analysis`, `equity-research`, `investment-banking`, `private-equity`, `wealth-management`, `fund-admin`, `operations` — skill **source** grouped by business line |
| Vertical source skills | 55 | `SKILL.md` folders (e.g. `3-statement-model`, `comps-analysis`, `dcf-model`, `pptx-author`) |
| Agent plugins | 10 | workflow agents (`market-researcher`, `pitch-agent`, `valuation-reviewer`) that **sequence** named skills |
| Managed-agent cookbooks | 10 | headless wrappers: `agent.yaml` + `subagents/*.yaml` + `steering-examples.json` |
| Subagents | 30 | scoped leaf workers (`sector-reader`, `comps-spreader`, `note-writer`) |
| MCP connectors | 12 | centralized in the core `financial-analysis` vertical's `.mcp.json` |
| Validation | `scripts/check.py` | parses manifests, resolves refs, checks bundled-skill drift |

## 2 · The bigger reframe — InfraSure is an intelligence system; the gate is its firewall

The deepest lesson of this exercise was **not** about the other repo. It was a correction to how we describe *ourselves*.

```text
THE REDUCTION TO REJECT                       THE TRUE FRAME
─────────────────────                         ──────────────
"InfraSure is an evidence /                   "InfraSure is an INTELLIGENCE / analytics system
 claim-validation system"                      whose reasoning is evidence-disciplined."
the gate IS the product                        the gate is the FIREWALL, not the purpose —
                                               it keeps the intelligence from becoming fluent mush
```

**Our own docs already lean to the true frame** — so the gap the deep-dive worried about is *narrower* than "we are missing an intelligence layer." Evidence, from a direct re-read:

```text
analysis_families.md  →  "define the kinds of INTELLIGENCE InfraSure Insights should support"
architecture.md §1    →  the moat is "how an InfraSure analyst REASONS over the data"
architecture.md §4    →  an entire section titled "The Runtime Is a Loop, Not a Line"  ← this IS the intelligence layer
prompt_projection.md  →  "Required reasoning steps": pull state → mechanism → resolve → filter/drill → assemble → cap
                          (a reasoning PROGRAM — already authored, for one driver/one family)
analysis_families.md  →  "Common Q&A Grammar" (7 questions): what changed → scope → mechanism → confident? →
                          directional? → who cares → watch next  (a generic DECOMPOSITION template, already here)
```

So the planning / decompose / retrieve-in-order / rank / synthesize loop is **present** — it just lives inside one resource's prompt and has **no name above the resource.**

### The distinction that prevents the mistake — authored scaffold (L0) vs runtime intelligence (L2)

"Intelligence" is two different things, and only one of them is the lab's to build:

```text
(a) AUTHORED intelligence SCAFFOLD     recipes · decomposition templates · screen/rank/segment
    L0 · STABLE · the moat             _method primitives · the family map · the Q&A grammar
                                       → THIS is what the lab authors. THIS is the genuine gap
                                         (recipes + factored-out method primitives are un-named).

(b) RUNTIME intelligence               the actual planning + synthesis a Claude session performs
    L2 · VOLATILE · the model's job    → NOT a thing we hard-code. The MODEL is the intelligence,
                                         scaffolded by (a). Building a bespoke "planner" engine
                                         freezes intelligence into the swappable layer.
```

**The P1 guardrail (load-bearing).** `principles.md` P1 lists, verbatim, under the **VOLATILE / swappable** column: *"the orchestration (manual → agentic)."* So a bespoke planner-orchestrator-runtime is, by our own constitution, the part we keep swappable — **not** the part we build and freeze. The temptation "let's build the intelligent system" must resolve to "let's author the scaffold that makes the model reason like an InfraSure analyst," or it violates P1.

```text
THE BRIDGE:  a RECIPE is authored methodology (a, L0/stable) that GUIDES the model's runtime
             reasoning (b, L2/volatile) — read by the model, not executed by an engine we wrote.
             That is how we get "scalable intelligence" without a planner that the next model obsoletes.
```

## 3 · The asymmetry (a corollary of §2)

The reframe explains *why* the borrow from financial-services is lopsided. They are **ahead of us on some axes and behind us on the one that is our moat** — and the moat is exactly the evidence-discipline firewall that protects the intelligence.

```text
financial-services is AHEAD on              InfraSure Insights is AHEAD on
──────────────────────────────              ──────────────────────────────
packaging at scale (55 skills, 7 verticals)  epistemic discipline
workflow composition (agent → skills)        blocked_claims · confidence_rules · the GATE
runtime wrappers (managed agents, subagents)  grounds / frames / routes (input-job labels)
tool/artifact procedures (drive Excel, PPTX) "ground or downgrade", the claim grammar
```

Two pieces of direct evidence from the repo:

- A real `SKILL.md` (`3-statement-model`) is a **procedural/tool skill** — *which cell to fill, what hex to use, when to recalc*. It teaches a model to operate a tool, not what it may and may not claim.
- `market-researcher`'s guardrails, in full, are: *"cite every number / mark `[UNSOURCED]` / stop for review / no distribution."* That is the **entire** epistemic layer. It has **no** equivalent of our `blocked_claims`, `confidence_rules`, downgrade rules, or input-job labels.

```text
THE TRAP:  copying their structure to "look more like a real firm's repo" could water down
           the layer where WE are already ahead. Their thin guardrails are a sign of a
           DIFFERENT product (artifact-centric, tool-integrated), not a better one.
THE RULE:  borrow their COMPOSITION + PACKAGING discipline. Never trade our gate for theirs.
```

## 4 · The core call — adopt / adapt / defer / reject

Every pattern in the repo, with a verdict and the reason. This is the heart of the discussion.

```text
ADOPT  = take it, it sharpens us, cheap         DEFER  = real, but not our bottleneck — trigger-gated
ADAPT  = borrow the shape, change the content   REJECT = wrong for us (scale artifact or anti-moat)
```

| # | Pattern in the repo | Verdict | Why |
|---|---|---|---|
| A | **One method source → many wrappers** (the whole spine) | **ADOPT** (already do) | This *is* our P1 (stable method / swappable execution), now confirmed by a 55-skill repo. Free validation; keep doing it. |
| B | **Method-skill vs workflow-agent split** (skill = one method; `market-researcher` = a recipe sequencing 5 skills) | **ADOPT (new)** | The one genuinely new structural idea — names the **authored-intelligence scaffold** (§2a) we have in docs but not in the model. See §5. Docs-only, cheap, sharpens the grain question. |
| C | **External docs are untrusted DATA, never instructions** | **ADOPT** (already do) | We already enforce this (`grounds/frames/routes`; `_reference` = form-not-facts). Their phrasing is crisp; worth quoting. Confirmation, not change. |
| D | **Scope the ask first → named steps in sequence → stop for human review** | **ADOPT** (already do) | This is our loop-with-checkpoint + the gate. The *"scope first"* move belongs in the recipe layer (§5) explicitly. |
| E | **`SKILL.md` frontmatter = `name` + trigger-rich `description`** (progressive disclosure: the right skill loads on the right phrasing) | **ADAPT** | We have the discovery mechanism (`resource.yml` taxonomy); borrow the *craft* of a trigger-rich description for the discovery tool. Not the file format. |
| F | **Centralized data connectors; packages stay method-only** (`.mcp.json` lives in the core vertical, not in each skill) | **ADAPT** (already lean this way) | Confirms: never embed connector/tool config in a resource. Our version = one MCP substrate + log gaps in `mcp_gaps.md`. Keep packages pure method. |
| G | **A `_method/`-style home for cross-cutting depth** (their verticals share skills; we'd share math/finance/insurance **+ the screen/rank/decompose primitives of §2a**) | **ADAPT** | Already proposed in the KB discussion (§3.1). The repo confirms shared method belongs in a quarantined layer, not duplicated per-resource. This is also the home for the **factored-out reasoning primitives** (§6). |
| H | **Validation script (`check.py`): schema, ref-resolution, drift** | **DEFER** | Real and worth it — but as a **written invariant checklist first** (no build system, per v0). The actual script triggers when there's a 2nd/3rd resource to check against. |
| I | **`SKILL.md` export / publish contract + `sync-agent-skills.py`** (source skill → portable bundle) | **DEFER** | Solving *portability*; our bottleneck is *grounding*. Trigger: ~3–5 validated resources, or a real publish need. Defining it now pulls focus to packaging mechanics. |
| J | **`marketplace.json` discovery index** | **DEFER** | We have `discovery_spec` designed, not built. Pointless to index 1 resource. Trigger: >1 resource worth discovering. |
| K | **Three-tier plugin taxonomy** (vertical / agent / partner-built) | **REJECT (for now)** | A **scale artifact** for 55 skills + 7 verticals + 2 partners. At 1 validated resource, importing it is cargo-culting. Our one-domain-folder + faceted-tags is the right grain for our scale. |
| L | **Managed-agent cookbooks / headless runtime** (`agent.yaml`, `steering-examples.json`) | **REJECT (for now)** | v0 is methodology-only. This is the runtime wrapper — explicitly out of scope until validated resources exist. |
| M | **Subagent decomposition** (separate scoped retriever / verifier / writer agents) | **REJECT (for now)** | Multi-agent choreography; v0 forbids it. A single session loop is arguably *better* for epistemic coherence — the gate sees the whole chain. Revisit only if a real bottleneck appears. |
| N | **Partner connector marketplace** (LSEG, S&P plugins) | **REJECT** | We have a curated substrate. Adding connector surface area is the *opposite* of our "log the gap, don't bolt on a tool" discipline. |
| O | **Artifact-centric telos** (their agents optimize for producing the note/deck) | **REJECT (actively)** | Directly against P2 (content downstream of validated insight). Their `market-researcher`'s *purpose* is the artifact; ours is the validated claim, which is *then* rendered. Do not import the artifact-first orientation. |
| P | **Thin guardrails as sufficient** ("cite every number / `[UNSOURCED]`") | **REJECT** | Our gate is richer (blocked_claims, confidence_rules, downgrades). Adopting theirs would be a downgrade. Keep ours. |
| Q | **A bespoke planner / orchestrator RUNTIME** (read §2 first) | **REJECT (P1)** | Tempting after seeing their agent runtime, but P1 names "orchestration (manual → agentic)" as the **volatile/swappable** layer. The intelligence is the model's job (§2b); we author the *scaffold* (recipes + `_method` primitives), never a planner engine that the next model obsoletes. |

## 5 · The idea worth promoting — the recipe layer (the authored-intelligence scaffold)

The repo separates two things our model currently **fuses into the single word "resource"**:

```text
financial-services            what it is                      InfraSure today
──────────────────            ──────────                      ───────────────
skill (comps-analysis)        ONE analytical method           = our RESOURCE (family × driver)  ✅ have it
agent (market-researcher)     a RECIPE that sequences          = Screen / Evaluate / Mitigate
                              skills for a job                   + bucket-1 / bucket-2
                                                                 — described in docs, NOT modelled as a thing
```

This is the concrete form of the §2a **authored-intelligence scaffold**. A recipe is the named layer above the resource; the `_method/` primitives (decompose, screen, rank, segment, score) are its reusable parts.

Why this matters for the KB-expansion discussion's **#1 hurdle (grain)**:

```text
A resource stays DRIVER-KEYED and small  ──because──►  the cross-resource orchestration
(ENSO, drought, congestion; actor/asset                lives ONE LAYER UP, in a recipe —
 as facets — never split per job/actor)                not by splitting resources per job or actor.

   → this is the cleanest argument yet for "dozens of resources, not hundreds."
   → Screen / Evaluate / Mitigate and bucket-1/bucket-2 become NAMED recipes that COMPOSE resources,
     instead of pressure to fork the resource catalog.
```

**Proposal**: name the **recipe layer** in docs (not code). A recipe is a *guided reasoning program*, read by the model:

```text
recipe = { job · ordered resources it composes · the _method primitives it calls ·
           the human checkpoint · the gate · the render target }
   e.g.  screen_weather_to_cashflow_risk:
         resolve scope → select drivers/resources → fan out across the fleet (aggregate/plants_by_owner)
         → score exposure·materiality·confidence (_method) → drill the top cases (get_plant)
         → assemble validated insight objects → GATE → render only after the gate
```

It is the InfraSure analog of an agent-plugin **minus the runtime** (§4 row Q): authored guidance (L0/stable), executed by the model (L2/volatile). Docs-only, cheap, and it resolves a real ambiguity in the taxonomy. *Open question in §8.*

## 6 · Honest scorecard of "what's underdeveloped" + the sequencing reality

The deep-dive listed seven "missing" capabilities. Graded against what's actually in the repo, they are **not equal** — and naming the difference stops us from over-building:

| Claimed gap | Honest verdict | What it actually needs |
|---|---|---|
| **reusable workflow recipes** | **REAL GAP** (the headline) | name the recipe layer (§5) — docs |
| **multi-method composition** | **REAL GAP, but conceptual** | impossible to exercise with 1 resource; needs the recipe layer + ≥2 resources |
| **cross-resource reasoning** | **NOT YET POSSIBLE** | needs ≥2–3 resources first; don't build ahead of it |
| **planning / task decomposition** | **PRESENT-BUT-UNFACTORED** | the Q&A grammar + per-resource "required reasoning steps" already do it; lift the generic skeleton up — and remember it's mostly the model's job (§2b) |
| **scalable fleet analytics** | **PRESENT-BUT-UNFACTORED** | data primitives exist (`aggregate`, `plants_by_owner`, `compare_entities`); lift "screen + rank a fleet" into a `_method` primitive any resource inherits |
| **ranking / screening / prioritization** | **PARTIAL** | `confidence_rules` + the materiality tie-break are seeds; factor into a `_method` scoring primitive |
| **analytic memory from prior runs** | **SCOPE-CREEP RISK — DEFER** | P3 already gives process-data memory (human-readable). Machine-reusable memory is a volatile-layer runtime feature; not the bottleneck |

**The sequencing reality nobody said out loud**: we have **one** resource.

```text
NAME the recipe layer + the _method primitives NOW   cheap · docs-only · resolves the grain question  ✅
BUILD a recipe catalog / planner NOW                 NO — that builds the composition layer over a
                                                     near-empty method layer (the same mistake as
                                                     building the publisher before there are skills).

CORRECT ORDER:  name recipe + _method (docs) → add 2–3 resources across different families
                → THEN the recipe layer has something to compose and the catalog earns itself.
```

## 7 · Prioritization — usefulness × timing

Two separate axes. *Usefulness* = how much the learning changes our thinking. *Timing* = when to act.

```text
                 SO USEFUL (changes thinking)            NOT THAT USEFUL (noise / scale artifact)
              ┌────────────────────────────────────┬──────────────────────────────────────────┐
   DO NOW     │ • intelligence reframe + L0/L2 (§2)  │ • (nothing — don't act on low-signal items)│
              │ • recipe layer + _method (B,G,§5)    │                                            │
              │ • the asymmetry / moat guard (§3)    │                                            │
              │ • confirm P1/P2/untrusted-docs (A,C,D)│                                            │
              ├────────────────────────────────────┼──────────────────────────────────────────┤
   DEFER /    │ • validation invariant CHECKLIST (H) │ • marketplace.json (J)                     │
   TRIGGER-   │ • trigger-rich discovery descriptions│ • SKILL.md export + sync (I)               │
   GATED      │   (E)                                │ • managed-agent runtime (L) · analytic mem │
              ├────────────────────────────────────┼──────────────────────────────────────────┤
   DON'T /    │ (n/a)                                │ • three-tier taxonomy (K) · subagents (M)  │
   REJECT     │                                      │ • partners (N) · artifact-telos (O)        │
              │                                      │ • thin guards (P) · planner runtime (Q)    │
              └────────────────────────────────────┴──────────────────────────────────────────┘
```

**The single most useful takeaway**: the **intelligence reframe + the L0/L2 distinction** (§2) — it corrects how we describe the product *and* installs the guardrail (P1) that keeps "build the intelligent system" from becoming "build a planner."
**The most useful structural idea**: the **recipe layer + `_method` primitives** (§5) — the concrete form of the authored scaffold, and it sharpens the grain question in the other discussion.
**The most useful *negative***: the **asymmetry** (§3) — knowing we're ahead on epistemics stops us from copying structure that would dilute the moat.
**The least useful**: the broader landscape scan in `../extra/references.md` (OpenAI/MS/Google/AWS frameworks) — fine as a "we looked around" record, but those are runtime-orchestration repos; nothing there transfers until we have a runtime, which is far off.

## 8 · Decisions for you (what we iterate on)

1. **Intelligence reframe as canon** (§2): adopt the one-liner — *"InfraSure is an intelligence system; the gate is its firewall, not its purpose"* — into `architecture.md` / `principles.md`? *(I recommend yes — it stops the reduction from recurring.)*
2. **The L0/L2 guardrail** (§2, row Q): make explicit in `principles.md` P1 that the *recipe/scaffold is stable (L0)* while *orchestration/planning is volatile (L2, the model's job)* — so "build the intelligent system" never quietly becomes "build a planner"?
3. **Recipe layer** (§5): name a **workflow-recipe** layer in docs (composes resources for Screen/Evaluate/Mitigate + the two buckets), and fold its conclusion into the KB discussion's §4 grain answer? *(Recommend yes — docs-only, cheap.)*
4. **`_method` primitives** (§5/§6): lift decompose / screen / rank / score out of the ENSO prompt into reusable `_method/` primitives — now (docs), or when resource #2 forces it?
5. **Sequencing** (§6): agree the order is *name recipe + `_method` (now) → add 2–3 resources across families → then build the catalog* — not a catalog/planner first?
6. **Asymmetry as canon** (§3): worth a one-liner — *"borrow form/packaging from references; never trade the gate for a reference's thinner guardrails"* — or leave it here?
7. **Validation checklist** (H) / **discovery description craft** (E): now, or at resource #2 / when discovery is built?
8. **The defers / rejects** (I, J, L / K, M, N, O, P, Q): agree, or is any one worth reconsidering at our stage?

Pick any to start, or push back on a verdict — the §4 table is meant to be argued with. When these settle: the **reframe + recipe + `_method`** decisions become small canon amendments **and a plan** (`docs/plans/`); the **defer** rows become trigger-tagged entries; the **reject** rows are recorded here so we don't relitigate them every time the repo tempts us.

---

**See also**: `2026-06-13_expanding_the_knowledge_base.md` (the companion KB discussion this feeds — §3 domain tree, §4 grain) · `README.md` (what a discussion is) · `../principles.md` (P1 stable/volatile + the orchestration-is-volatile line · P2 content downstream · P6 references inform, don't bind) · `../architecture.md` (§1 "how the analyst reasons" · §4 "the runtime is a loop") · `../method/analysis_families.md` (the 7 families + the "Common Q&A Grammar" decomposition template a recipe composes) · `../../resources/weather_and_climate/el_nino_enso/prompt_projection.md` (the per-resource "required reasoning steps" — the scaffold to factor up) · `../../resources/README.md` (the spine the recipe layer sits above) · `../status/mcp_gaps.md` (where the "log the gap, don't add a tool" discipline lives) · `../extra/references.md` (the broader landscape scan) · `.financial-services/learning/architecture_map.md` (the verified repo map this builds on).
