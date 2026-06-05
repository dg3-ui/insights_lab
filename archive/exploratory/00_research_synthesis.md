# 00 — Research synthesis

> Status: synthesis complete 2026-05-31. Reads the three research threads ([`research/01_platforms.md`](research/01_platforms.md) / [`research/02_agentic_systems.md`](research/02_agentic_systems.md) / [`research/03_methodology_traditions.md`](research/03_methodology_traditions.md)) as one. The structural decisions here become the spine of [`01_principles.md`](01_principles.md), [`02_methodology_brief_shape.md`](02_methodology_brief_shape.md), and `04_agent_architecture.md` (forthcoming).

## Executive framing

The three threads converge on a single thesis: **every mature analytical tradition treats either the substrate or the methodology as structured — but never both at once**. RAND/Brookings/RFF have structured methodology with prose substrate. CIM/OEO have a typed substrate with no methodology layer. NREL ATB has typed parameters with prose-narrative applied analysis. Wood Mac and BNEF have entity registries that don't bind to the analytical claims in their PDFs. Stratechery and Money Stuff prove that framework × entity stream is the leverage shape, but it's executed manually by a single voice. Deep-research agents (OpenAI / Anthropic / Gemini / Perplexity) produce comprehensive prose with intermediate hallucinations that are invisible to end-to-end eval.

The wedge: **typed methodology over a typed substrate, with claim-level grounding**. That's a category none of these systems is positioned to ship without dismantling its current architecture. We're not yet committed to a PDF/seat economic model or to open-web-search agentic architecture, so we can build it.

### The shape of the opportunity, visualised

```
                  STRUCTURED SUBSTRATE
                          ▲
                          │
        CIM / OEO ────────┤
        (typed assets,    │
         no methodology)  │
                          │      ★ InfraSure.ai Insights
                          │      (typed methodology
                          │       OVER typed substrate
                          │       with claim-level grounding)
                          │
                          │
       Wood Mac / BNEF ───┤
       (entity registry,  │
        loose narrative)  │
                          │
        NREL ATB ─────────┤
        (typed params,    │
         prose applied)   │
                          │                              RAND / Brookings
                          ├──────────────────────────────  (structured methodology,
                          │                                  prose substrate)
                          │
                          │                              Stratechery / Money Stuff
                          │                              (manual framework × entity)
                          ▼
                  UNSTRUCTURED NARRATIVE
                          ◄───────────────────────────────────────────►
                          NO METHODOLOGY                STRUCTURED METHODOLOGY
                          LAYER                         LAYER
```

Each existing platform sits in one of three quadrants. None occupy the top-right. That's where we build.

---

## Eight structural commitments

These are the load-bearing decisions. Each is justified by at least two of the three research threads. If we flip one of these, the whole architecture shifts.

---

### 1. The atomic unit is the structured analytical statement, not the report.

A "report" or "brief" is one possible rendering over a set of statements. The unit of value is the typed claim, scoped to entities + time window + dimension, with citations into the substrate.

**Why** — The dominant industry failure mode is PDF-as-atomic-unit (Wood Mac, BNEF, S&P, RAND): can't be re-grounded when underlying data changes, can't be queried by an LLM, can't be subset to one plant, dies on author turnover.

**What it forces** — A first-class data model for "insight" and "methodology brief" (not just markdown files). Render targets (cards, pages, downloadable PDFs) become *projections* of the structured data, not the canonical store.

#### Example: what "atomic unit" actually means

What we're rejecting — the report shape (~24-page PDF "Q2 2026 ERCOT Thermal Outlook"):

> *"…NRG's W.A. Parish station, the largest fossil generation facility in Texas, remains well-positioned in the current capacity market environment. With ERCOT capacity payments holding above $70/kW-month and natural gas prices stabilising in the $3.50-$4.00/MMBtu range, our base case sees the plant maintaining merchant economics through 2030. Repower optionality has come back into focus as gas turbine OEMs report extended lead times…"*

What we're adopting — the statement shape (a row in a structured store):

```json
{
  "insight_id": "AI-014-wa-parish-repower-2026Q2",
  "claim": "W.A. Parish (plant_id 3470) repower NPV is $145M at 8.5% discount over 20yr horizon",
  "claim_type": "scenario_based",
  "confidence": "medium",
  "tuple_refs": [
    {"dim": "engineering_generator", "entity_id": 3470, "column": "heat_rate_btu_per_kwh", "value": 9847, "vintage": "2024-Annual"},
    {"dim": "financial", "entity_id": "ERCOT", "column": "capacity_payment_per_kw_month", "value": 73, "vintage": "2026-Q1"},
    {"dim": "engineering_subsystem", "entity_id": 3470, "column": "prime_mover", "value": "ST", "vintage": "2024-Annual"}
  ],
  "scope": {"entity_ids": [3470], "iso": "ERCOT"},
  "methodology_ref": {"brief_slug": "thermal-repower-npv", "snapshot_id": "2026-Q2"},
  "valid_until": "2026-09-30",
  "caveats": ["Assumes single-axis retrofit, not full repower", "Capacity payment forecast is mechanical, not auction-derived"]
}
```

Same analytical content. But the statement form is queryable ("find me all repower NPV claims > $100M in ERCOT, valid as-of today"), subsettable ("show only the WA Parish claim on its plant page"), auditable (every input has a vintage stamp), and renderable in any output surface. The PDF can't do any of those.

---

### 2. Two content types, joined by `methodology_refs`.

**Methodology briefs** (reusable worldviews; evergreen with revisions) and **applied insights** (specific, scoped, time-bound) are first-class peer types. Applied insights reference methodology briefs by slug + snapshot ID.

**Why** — NREL ATB / EIA AEO / BNEF Tier 1 / RAND all validate methodology-as-separable-citable-artifact as a real pattern. But their applied work is prose. Our applied insights are structured objects that explicitly declare which methodology they instantiate.

**What it forces** — Methodology comes first in the build order. We cannot produce trustworthy applied insights without the methodology spine in place.

#### Example: the two types side by side

A **methodology brief** is a worldview. It does not name any specific plant:

```yaml
slug: thermal-repower-npv
brief_id: MB-0007
kind: methodology_brief
short_title: "Thermal Repower NPV"
scope:
  entity_types: [plant, generator]
  fuel_filter: [NG, BIT, SUB, LIG, DFO, RFO]
  capacity_filter: { min_mw: 50 }
procedure:
  reference:
    outputs:
      - { name: repower_npv_usd, unit: USD, sign_convention: "positive = attractive" }
    horizon_years: 20
    discount_rate_default: 0.085
  explanation: |
    Repower NPV is the spread between (capacity payment + energy margin
    under a new heat rate) and the capex of the retrofit, after netting
    residual book value of the existing asset...
```

An **applied insight** instantiates that worldview on a concrete scope. It cites the brief snapshot:

```yaml
slug: wa-parish-repower-2026Q2
insight_id: AI-014
kind: applied_insight
methodology_refs:
  - { brief_slug: thermal-repower-npv, snapshot_id: 2026-Q2, role: primary }
scope:
  entity_ids: [3470]
  iso: ERCOT
claims:
  - claim_id: c1
    text: "W.A. Parish repower NPV is $145M"
    tuple_refs: [...]   # see commitment 3
    confidence: medium
```

Note: the methodology brief is **abstract** (no plant IDs). The applied insight is **concrete** (specific plant + specific vintage). They live in separate tables, joined by `methodology_refs`. Different lifecycles: the brief evolves slowly through revisions (semver), the applied insight has a fixed publication date and a defined `valid_until`.

---

### 3. Substrate grounding is at the *claim* level, not the document level.

Every analytical claim carries a `(dimension, entity_id, column, value, vintage)` tuple back to the substrate. Citations are emitted by the retrieval tool, not by the LLM.

**Why (1)** — Three of the four agentic-system failure modes (intermediate hallucination, citation hallucination, scope drift) collapse if every claim must point back to a substrate row. The fourth (premature stopping) becomes detectable because "no tuple yet" = "keep digging."

**Why (2)** — This is the structural moat. Bloomberg RMS / Wood Mac Lens / BNEF can tag a *report* to an entity. Almost no one tags a *claim* to an entity. To get there they'd have to rebuild their authoring stack.

**What it forces** — Per-dimension typed retrieval tools (not vector RAG, not text-to-SQL). The agent names what it wants (`get_generation_for_plant(plant_id, vintage)`); the tool returns rows with provenance. Spider 2.0's text-to-SQL cliff (10-17% success on real enterprise schemas) is the empirical argument against the alternative.

#### Example: claim with vs. without grounding

Ungrounded (what an LLM produces by default):

> *"W.A. Parish has strong repower economics in the current ERCOT capacity market."*

Could be true. Could be plausible-sounding fiction. The reader has no way to check.

Grounded (what our system requires):

> *"W.A. Parish (plant_id 3470) has a measured heat rate of 9,847 BTU/kWh `[engineering_generator.heat_rate_btu_per_kwh @ 2024-Annual]`, well above class average of ~7,200, and operates in an ERCOT capacity market clearing at $73/kW-month `[financial.capacity_payment_per_kw_month @ 2026-Q1]`. Under the [thermal-repower-npv@2026-Q2] methodology, projected NPV is $145M at the 8.5% default discount rate."*

Every quantitative claim points to a substrate row with a known vintage. If 2025-Annual data lands and the heat rate updates to 9,720, the system can mechanically detect that this insight's underlying input has shifted and flag it for review. The reader can audit any individual claim.

**What this rules out**: vector RAG for our use case. Vector RAG is for "find passages similar to my question" — appropriate when the corpus is unstructured. Our corpus is *known schema* (15K plants × ~100 cols, dimension parquets). The agent should name the columns it wants, not vector-search for them.

---

### 4. Two clocks: live view + immutable snapshots.

Methodology briefs have (a) a live URL that always shows the freshest synthesis and (b) periodic snapshots at fixed cadence dates. Applied insights cite snapshot IDs, never the live brief.

**Why** — Stanford Encyclopedia of Philosophy and arXiv both solved this in the 1990s-2000s. Applied insights have a fixed publication date and shouldn't drift in meaning when the methodology beneath them is sharpened later. Citation breakage is what kills knowledge bases at scale.

**What it forces** — A versioning subsystem. Quarterly snapshots aligns naturally with EIA-860M / queue refresh cadence.

#### Example: the two-clocks pattern in action

```
LIVE BRIEF (always-current URL: /insights/methodology/thermal-repower-npv):
    v0.5──●──v0.6──●──v0.7────●─v0.8──●──v0.9──────●─v1.0──●──v1.1──────>
         (sharpened over time as we learn from applied insights, errata, etc.)


SNAPSHOTS (immutable, fixed cadence — Q1 / Q2 / Q3 / Q4):
    │             │             │             │             │
   2026-Q1     2026-Q2       2026-Q3       2026-Q4       2027-Q1
   captures    captures      captures      captures      captures
   v0.6        v0.8          v0.9          v1.0          v1.1
   (immutable) (immutable)   (immutable)   (immutable)   (immutable)


APPLIED INSIGHT published 2026-04-12 (Q2):
    methodology_refs: [{brief_slug: thermal-repower-npv, snapshot_id: 2026-Q2}]
                                                                  └────────┐
                                                                           │
                                                                           ▼
    Even when the live brief evolves to v1.0 in Q4, this insight
    still cites 2026-Q2 — meaning the audit trail stays stable
    even as the methodology gets sharpened.
```

A reader visiting the applied insight clicks through to `/insights/methodology/thermal-repower-npv/2026-Q2` and sees exactly the methodology the insight was authored against. Click "current version" → routes to the live brief at `/insights/methodology/thermal-repower-npv` and sees the latest. Audit trail preserved without freezing the methodology.

---

### 5. Typed edges, not implicit references.

Inter-brief relationships are typed first-class edges: `extends`, `depends_on`, `supersedes`, `cites_data`, `cites_external`. Plus computed reverse edges (`used_by_applied_insights`).

**Why** — When we sharpen a methodology, we need to know what depends on it. Either we have a typed graph or we have a grep problem. Wikidata and Schema.org both made this commitment 15 years ago; we don't get to learn it again.

**What it forces** — A staging step in the build pipeline that computes reverse edges. Trivial cost; large surface payoff.

#### Example: the methodology graph for El Niño

```
                  [climate-fundamentals]
                          ▲
                          │ depends_on
                          │
        ┌─────────────────┴──────────────────────┐
        │                                         │
   [el-nino-impact-pathways] ─── extends ──→ [la-nina-impact-pathways]
        ▲       ▲                                 ▲
        │       │ depends_on                      │
        │       │                                 │ depends_on
        │       │                                 │
        │  [solar-irradiance-region-shift] ───────┘
        │              ▲
        │              │ cites_data
        │              │
        │      [NOAA_CPC_ENSO @ 2026-Q2]
        │
        │ extends
        │
  [enso-lmp-translation]
        ▲
        │ used_by_applied_insights (computed reverse edge)
        │
   [caiso-solar-fleet-el-nino-2026, ercot-q3-2026-lmp-outlook, ...]
```

When we sharpen `solar-irradiance-region-shift` to v0.8, the typed graph immediately tells us:
- `el-nino-impact-pathways` and `la-nina-impact-pathways` need review (both `depends_on`)
- Every applied insight using those briefs is flagged for re-validation
- A reader looking at `solar-irradiance-region-shift` sees, on the same page, every brief and every applied insight that builds on it

This is the difference between "grep the markdown for slug mentions" (fragile, slow, incomplete) and "query the edge table" (mechanical, fast, complete).

---

### 6. Agent architecture: plan → methodology-lookup → typed retrieval → sub-synthesize → final synthesis → citation pass.

Single-threaded master loop (Claude Code pattern) with four-track stopping: goal-met / resource-cap / pathology-detected / provenance-gate. Subagents (Anthropic's +90.2% pattern at 15× cost) only for full-brief production, not for interactive queries.

**Why** — This is the converged frontier pattern across OpenAI / Anthropic / Gemini / Perplexity Deep Research. The methodology-lookup step (AgentAda / DataSage / Self-RAG) is what turns "comprehensive-looking prose" into "actually correct" — and it's exactly what our methodology briefs are designed for.

**What it forces** — Methodology briefs aren't just human-readable documents; they're inputs to the agent's plan step.

#### Example: an agent trace producing one applied insight

```
=== RUN insight_2026Q2_wa_parish_repower ============================
[plan]            decompose("repower NPV for W.A. Parish station")
                  → 4 sub-questions, each tagged with required dimensions:
                    sub_q_1: heat rate + capacity        (engineering_*)
                    sub_q_2: ERCOT capacity payment      (financial, regions)
                    sub_q_3: fuel cost forecast          (financial, news)
                    sub_q_4: compute NPV, validate       (methodology brief)

[methodology_lookup]
                  load brief MB-0007 (thermal-repower-npv) @ snapshot 2026-Q2
                  → required facts checklist: 14 items
                  → output target: repower_npv_usd (scalar, USD)
                  → caveats baseline: 3 standard caveats

[retrieve sub_q_1]
                  tool: get_generator_engineering(plant_id=3470)
                  → 4 rows (one per generator unit)
                  → vintage: engineering_generator 2024-Annual
                  → claim materialised: heat_rate_btu_per_kwh = 9847

[retrieve sub_q_2]
                  tool: get_capacity_market(iso=ERCOT, horizon=20yr)
                  → vintage: financial 2026-Q1
                  → claim: capacity_payment_per_kw_month = 73

[retrieve sub_q_3]
                  tool: get_fuel_cost(state=TX, fuel=NG, horizon=20yr)
                  → vintage: financial 2026-Q1 + news facts 2026-Q2
                  → claim: fuel_cost_per_mmbtu projection $3.50-$4.00 base case

[sub_synthesize]  compose claim: "NPV $145M under base case"
                  attach tuple_refs: 6 (one per substrate row consumed)

[self_check]      goal-met: 14/14 ✓
                  resource: 8.2K tokens (cap 50K) ✓
                  pathology: no repeated retrievals ✓
                  provenance-gate: every numeric claim has tuple_ref ✓

[final_synthesize]  compose applied insight in publishable shape
[citation_pass]     attach 6 tuple_refs as inline cites; emit scope manifest
[done]              applied_insight_id = AI-014, queue for human review
```

The trace is **the deliverable**, not just internal logging. A reader on the published insight can click "View methodology trace" and see this exact run. If the trace is sloppy (e.g., a claim with no tuple_ref, premature stop, scope broadened mid-run), the insight doesn't ship — principle 12 in `01_principles.md`.

---

### 7. Staleness as machine-readable signals.

Every methodology brief carries `last_reviewed`, `expected_review_cadence`, and `staleness_signals` (events that trigger review). Every applied insight carries `validity_window` and the vintage of every substrate input it consumed.

**Why** — None of the incumbent platforms does this; their content drifts toward "2018 framework still on the site in 2026" decay. Wikidata qualifiers + FAIR provenance + arXiv versions all encode time-validity as data, not vibes.

**What it forces** — A scheduled job that reads staleness signals against the data refresh log and produces a review queue.

#### Example: staleness signals for the El Niño brief

```yaml
validity:
  expected_review_cadence: triggered    # not date-driven
  staleness_signals:
    - source: NOAA_CPC_ENSO
      event: state_change
      severity: high
      action: "Re-run all applied insights citing this brief; possibly downgrade
               confidence on cooling/heating demand claims if forecast changes."
    - source: LBNL_Queued_Up
      event: new_edition
      severity: medium
      action: "Audit scope.regions[].values for any new project IDs in the
               affected climate regions."
    - source: NREL_ATB
      event: new_edition
      severity: low
      action: "Refresh fuel-cost fallback parameters in substrate_inputs."
    - internal: capacity_market_reform
      severity: high
      action: "Methodology assumes single-axis market structure; reform invalidates."
  last_reviewed: 2026-05-31
```

When the foundation refresh pipeline fires (`/refresh-foundation`), the same pipeline now produces a `stale_briefs.json` summary: `LBNL_Queued_Up went 2024 → 2025 → review queue: [thermal-repower-npv (severity: medium), el-nino-impact-pathways (severity: medium), …]`. The system tells *us* what's stale. We don't have to remember.

---

### 8. Editorial confidence is declared, not implied.

Each brief and each applied insight carries an explicit confidence level (`low / medium / high`) with caveats. Editorial policy determines which levels are publishable.

**Why** — Incumbent platforms imply confidence through tone; readers can't programmatically filter for what they trust.

**What it forces** — A `01_principles.md` editorial section. Lean toward "low confidence is publishable IF caveats are explicit and underlying claims are still substrate-grounded".

#### Example: confidence levels in practice

| Confidence | What it means | Example claim | Publishable? |
|---|---|---|---|
| **high** | Multiple substrate dims corroborate; mechanistic basis well-established; no significant caveats | "Plant 3470 has nameplate 3,654 MW (`engineering_generator @ 2024-Annual`)" | ✓ |
| **medium** | Solid analytical basis but depends on inference from substrate or external data with known uncertainty | "Plant 3470 projected repower NPV is $145M at 8.5% discount over 20yr, base case" + 3 caveats on fuel cost / capacity payment / retrofit assumptions | ✓ |
| **low** | Directionally supported but significant uncertainty (forecasts, scenario-based reasoning, unknown actor behavior) | "Under a strong El Niño Q4 2026, CAISO solar fleet capacity factor likely drops 4-8 pp vs ENSO-neutral baseline" + caveats on irradiance attribution methodology, demand mix variability | ✓ (with explicit caveats) |
| **(unpublishable)** | No substrate tuple can be produced; or low confidence + no caveats surfaced | "ERCOT will see major restructuring this year" | ✗ — strip the claim |

Publishing low-confidence claims is fine. Publishing low-confidence claims **without surfacing why they're low confidence** is not. The discipline isn't conservatism, it's honesty about uncertainty.

---

## Where the threads explicitly disagree (and we have to pick)

These are real forks, not noise. Listing them with concrete instances so they don't get swept into the architecture without a deliberate call.

| Question | Source | The fork | Concrete instance | My initial lean |
|---|---|---|---|---|
| Snapshot cadence: fixed dates regardless of change vs. only on content change? | 03 | Fixed quarterly = predictable, generates "null" snapshots for unchanged briefs. Content-driven = leaner storage. | If `thermal-repower-npv` is unchanged from Q1 to Q2, do we still fire a 2026-Q2 snapshot? | **Fixed quarterly.** Citations need predictable anchors more than we need lean storage. Unchanged snapshots carry a `changed_from_previous: false` flag. |
| Methodology briefs as data rows vs. prompt templates? | 02 | Data = queryable, versioned, citable, but heavier substrate. Prompts = lighter but lose lifecycle properties. | Does the agent's plan step load the brief from a `methodology_briefs` table, or from a prompt template stored in the agent's repo? | **Data rows, with a derived prompt projection** for the agent. Same structured fields serve both — `procedure.how_to` blocks render into a system prompt fragment at runtime. |
| Subagent fan-out: yes or no? | 02 | Anthropic's +90.2% / 15× cost is real. Claude Code's single-thread win on debuggability is also real. | For the El Niño brief's 4-6 outputs (irradiance, solar gen, demand, LMP, …), do we spawn 4-6 parallel subagents? | **Yes for full-brief production with independent sub-dimensions, no for interactive Q&A.** El Niño's dimensions ARE independent (irradiance physics doesn't depend on LMP), so this is a fan-out case. |
| Scope fan-out: 2,400 insights per methodology or one parameterized insight rendered 2,400 ways? | 02 | 2,400 separate = each has own ID and lifecycle. One parameterized = leaner but render is computed, not stored. | The thermal repower methodology applies to ~1,200 NG plants ≥ 100 MW. Do we author 1,200 applied insights or one templated insight that renders per-plant on demand? | **One parameterized insight with per-entity render manifest.** The insight is the analytical statement + scope; the per-entity application is computed at request time. (This is also the structural answer to the "framework × entity stream" leverage shape — we don't author 1,200 essays.) |
| Eval: human-authored golden insights vs. substrate-claim-grounding rate? | 02 | Both useful, both expensive. | How do we know if the El Niño brief is producing trustworthy applied insights? Hand-authored "this is what the insight should look like" reference set, or mechanical "% of claims with tuple_refs"? | **Substrate-claim-grounding rate from day 1; golden insights from when we have ~10 published.** Grounding rate is mechanical and continuous; golden insights need a stock of real publications to author against. |
| Lowest publishable confidence? | 03 | Low-with-caveats vs. medium-or-higher only. | Can we publish "El Niño Q4 2026 forecast — CAISO solar fleet impact" as `low` confidence with 4 explicit caveats? | **Low-with-explicit-caveats publishable.** See commitment 8. The risk is over-conservatism that leaves directional analysis on the floor. |
| Author attribution model: team handle vs. individual names? | 03 | Team handle = scales, less personal accountability. Named = builds individual reputation. | Should the El Niño brief say `authors: ["InfraSure.ai Research"]` or `authors: ["divy@aamani.ai"]`? | **Team handle for v1** (`InfraSure.ai Research`), with individual reviewer name in metadata for audit trail. Revisit when we have a real research team. |

---

## The four risks I flagged earlier, reframed as principles

These came up in the very first discussion of the insights idea, before research. The research lets us state each as a principle-level commitment, ready for `01_principles.md`:

### Risk-principle 1: Substrate grounding is the gate, not the goal.

If an insight could be written from public data alone, we don't publish it.

**Violation example** — A LinkedIn-style think-piece: *"The future of US thermal generation depends on three factors: gas price stability, capacity market reform, and the speed of renewable buildout."* True. Publishable on any energy blog. **Doesn't ship on InfraSure.ai** — no substrate grounding, could be written by anyone, no marginal value over the rest of the internet.

**Pass example** — Same broad theme, properly grounded: *"Across the 1,224 NG plants ≥ 100 MW in our substrate, 312 (25.5%) have heat rates more than 1,500 BTU/kWh above their class average — measurable repower candidates totalling 184 GW. Of those, 89 sit in capacity markets where the current clearing price (`financial.capacity_payment @ 2026-Q1`) exceeds the methodology threshold for positive NPV."* — concrete, scoped, citable, and you can't write this without our substrate.

### Risk-principle 2: Methodology before applied, always.

No applied insight ships without a methodology brief it instantiates.

**Violation example** — An intern writes: "ERCOT Q3 2026 thermal repower opportunities" listing 15 candidate plants based on their own ad-hoc analysis. No methodology brief. Three months later the senior reviewer can't audit the analytical choices because they're embedded in prose with no separable methodology layer.

**Pass example** — Same intern writes the same applied insight, but cites `methodology_refs: [{brief_slug: thermal-repower-npv, snapshot_id: 2026-Q2}]`. The reviewer audits the brief once, then any applied insight using that brief inherits the audit. Methodology is the leverage; applied insights are the production line.

### Risk-principle 3: LLM-led, human-reviewed — and the human's role is editorial judgment, not authoring.

LLMs are categorically better than humans at cross-dimensional synthesis at this scale.

**Anti-pattern** — A reviewer rewrites every sentence of the LLM's draft for stylistic reasons. Slow, expensive, eats the cost advantage of LLM authoring, and doesn't actually improve the analytical content.

**Right pattern** — The reviewer reads the LLM draft and asks four questions: "Is the claim right? Are the caveats honest? Are mechanistic claims labeled as mechanistic and statistical claims as statistical? Is the scope honest?" If yes to all four, ship — even if the prose is awkward in spots. Editorial polish is the lowest-leverage activity in this system.

### Risk-principle 4: Maintenance is part of authoring; a brief without lifecycle metadata isn't finished.

A methodology brief without staleness signals + a refresh cadence + an asserted validity window is not a brief — it's a draft.

**Violation example** — Brief ships with the analytical content complete but `staleness_signals: []`. Six months later, NOAA CPC updates the ENSO index methodology, our brief is now silently wrong, nobody knows. **Unmaintained briefs tarnish the platform's credibility worse than the absence of the brief would have.**

**Pass example** — Brief ships with the analytical content + the four staleness signals from commitment 7's example. When CPC updates, our review queue automatically lists the brief. We either revalidate (and bump `last_reviewed`) or revise (and bump version + snapshot). Either way the platform's promise to readers stays intact.

---

## What we know vs. what's still open

**Settled enough to draft against:**

- The eight commitments above are load-bearing.
- The draft methodology brief schema in [`research/03_methodology_traditions.md`](research/03_methodology_traditions.md) is solid — adopted as the v0 starting point for [`02_methodology_brief_shape.md`](02_methodology_brief_shape.md). Open questions in that schema (snapshot cadence, runnable how-to, edge directionality) have my initial leans above; user can flip any of them.
- The agent architecture sketch in [`research/02_agentic_systems.md`](research/02_agentic_systems.md) is the v0 for `04_agent_architecture.md`. The four-track stopping criteria is non-negotiable; everything else can iterate.

**Open before we go further:**

- ~~**The first methodology brief topic.**~~ **Picked: El Niño & ENSO state effects on US energy infrastructure.** ([`05_first_methodology_brief/`](05_first_methodology_brief/))
- **The applied-insight shape.** Research thread 3 covers methodology brief in detail but only sketches applied insights. `03_applied_insight_shape.md` will need its own design pass once we have the methodology shape locked.
- **The principles file's editorial section.** Confidence policy, attribution model, what triggers a takedown vs. a revision, what an intern can publish without senior sign-off. Drafted in [`01_principles.md`](01_principles.md) section III; user to review.

## Recommended next moves

1. ~~**You pick the first methodology brief topic.**~~ ✓ El Niño picked.
2. **I draft [`01_principles.md`](01_principles.md)** ✓ shipped.
3. **I draft [`02_methodology_brief_shape.md`](02_methodology_brief_shape.md)** ✓ shipped as v0.
4. **You dump El Niño domain knowledge into [`05_first_methodology_brief/brief.md`](05_first_methodology_brief/brief.md)** — in any shape (prose, bullets, equations, references). I structure it against the schema; the schema flexes where it doesn't fit; learnings log to `what_we_learned.md`.
5. **`04_agent_architecture.md`** comes after we have one methodology brief — the brief informs what the agent's methodology-lookup step needs to consume.
6. **`03_applied_insight_shape.md`** comes after `02` is stable (probably co-stable with `04`).

That's the order. Everything else is downstream.
