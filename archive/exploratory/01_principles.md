# 01 — Analysis principles

> **Status**: draft v0, 2026-05-31. Graduates to `business/principles/analysis.md` (or equivalent) at the same authority level as the existing scalability / SEO / UI principles once the user signs off.
>
> **Why a principles file at all**: the insights layer is a new system at a new altitude. Every code-level decision we make over the next year compounds against (or with) the assumptions encoded here. The earlier the principles are explicit, the fewer "should we…?" arguments we relitigate later. Mirror of how `docs/principles/ui_design.md`, `docs/principles/scalability.md`, etc. have served the platform side.
>
> **Authority**: these principles override implementation convenience. If a principle and a shortcut conflict, the principle wins and we figure out a different shortcut. If a principle is wrong, we change the principle deliberately and log the change — we don't quietly drift past it.

---

## I. The eight structural commitments

These are the load-bearing architectural decisions for the insights system. They came out of [`00_research_synthesis.md`](00_research_synthesis.md), each justified by at least two of the three research threads (platforms / agentic systems / methodology traditions). Flipping any one of these forces a redesign of multiple downstream pieces.

### 1. The atomic unit is the structured analytical statement, not the report.

A "report" or "brief" is a *rendering* over a set of statements. The unit of value is the typed claim — scoped to entities + time window + dimension — with provenance into the substrate.

**What this rejects**: the PDF-report-as-product pattern (Wood Mac, BNEF, S&P, RAND). Decays the moment underlying data shifts; not queryable by an LLM; can't be subset to one plant; dies on author turnover.

**What this commits us to**: every methodology brief and every applied insight is a first-class data row, not a markdown file in a folder. Rendering surfaces (cards, pages, downloadable PDFs) are projections.

### 2. Two content types, joined by typed reference.

**Methodology briefs** — reusable analytical worldviews. Evergreen with versioned revisions.
**Applied insights** — specific, scoped, time-bound analytical statements. Cite a methodology brief by `slug + snapshot_id`.

**What this rejects**: one content type with a `kind` flag. Looks simpler in the data model; produces messy product surfaces because the lifecycles, audiences, and update cadences are different.

**What this commits us to**: methodology before applied, always. No applied insight ships without a methodology brief it instantiates. The brief is the worldview; the applied insight is the worldview's application to a scope.

### 3. Substrate grounding is at the claim level, not the document level.

Every analytical claim carries a `(dimension, entity_id, column, value, vintage)` tuple back to the substrate. If a claim can't produce a tuple, it doesn't ship.

**What this rejects**: document-level tagging (Bloomberg RMS, Wood Mac Lens, BNEF). Tells you which report mentions Vistra; doesn't tell you which analytical claim about Vistra is still valid against today's data.

**What this commits us to**: per-dimension typed retrieval tools (not vector RAG, not text-to-SQL — Spider 2.0 confirms text-to-SQL collapses on real enterprise schemas). The agent names what it wants; the tool returns rows with provenance.

### 4. Two clocks: live view + immutable snapshots.

Methodology briefs have a live URL showing the freshest synthesis. They also have periodic immutable snapshots at fixed cadence dates. **Applied insights cite snapshots, never the live brief.**

**What this rejects**: single-version mutable briefs (citations break on every revision) and write-once-immutable briefs (drift to staleness, never sharpened).

**What this commits us to**: quarterly snapshot cadence (aligned with our existing data refresh cadence — EIA-860M / queue / FERC). A snapshot fires for every brief every quarter even if unchanged; the `unchanged` flag is part of the snapshot metadata. Predictable citation anchors > storage thrift.

### 5. Typed edges, not implicit references.

Inter-brief relationships are typed first-class edges: `extends`, `depends_on`, `supersedes`, `cites_data`, `cites_external`. Reverse edges (`used_by_applied_insights`, `referenced_by_briefs`) are computed at build time.

**What this rejects**: prose-embedded references that require grep to maintain. Wikidata and Schema.org both made this commitment 20 years ago. We don't get to relearn it.

**What this commits us to**: a small graph layer in the data model. Trivial cost; large payoff (mass-update propagation, dependency rendering, staleness fan-out when a data source refreshes).

### 6. Single-threaded master loop for the agent; fan-out only when justified.

The insight-production agent runs Claude Code's pattern: while-loop on tool-calls, flat history, transparent trace. Subagent fan-out (Anthropic's +90.2%-at-15×-cost pattern) is reserved for full-brief production with independent sub-dimensions — not for interactive queries.

**What this rejects**: multi-agent-by-default architectures. MAST taxonomy data: 79% of production MAS failures are spec ambiguity + coordination breakdown, not model capability.

**What this commits us to**: every agent run produces an inspectable trace. Subagent calls happen via an explicit typed Task contract (objective + output schema + tool list + scope), not free-text delegation.

### 7. Staleness is machine-readable, not editorial vibes.

Every methodology brief carries `last_reviewed`, `expected_review_cadence`, and `staleness_signals` (events that trigger review — `new LBNL Queued Up edition`, `FERC EQR schema change`, `capacity market reform`, `ENSO state change`). Every applied insight carries `validity_window` and the vintage of every substrate input it consumed.

**What this rejects**: the think-tank failure mode where 2018 frameworks linger on the site in 2026. None of the incumbent platforms does this well.

**What this commits us to**: a scheduled job that reads staleness signals against the data refresh log and produces a review queue. Connects to the existing `/refresh-*` cadence work — when the foundation refresh fires, the review queue gets populated mechanically.

### 8. Editorial confidence is declared, not implied.

Every brief and every applied insight carries an explicit confidence level (`low / medium / high`) with caveats. **Lowest publishable confidence is `low`, provided caveats are explicit and substrate grounding holds.**

**What this rejects**: confidence-implied-by-tone (incumbent norm). Users can't programmatically filter for what they trust.

**What this commits us to**: a discipline of caveat writing — "this claim assumes X, breaks if Y, doesn't account for Z." Editorial review checks caveat completeness, not whether the claim is "right enough to publish." Honesty about uncertainty is a feature, not a hedge.

---

## II. The four risk principles

These are the long-tail traps. Each is phrased as "what we will not do" so the discipline is unambiguous.

### 9. Substrate grounding is the publication gate.

**If an insight could be written from public data alone, we don't publish it.** Every published insight must be hard to produce without InfraSure.ai's specific substrate. Editorial review's first question is: "what does this claim require that a generic energy analyst couldn't get?" If the honest answer is "nothing," it doesn't ship.

This is the moat in its operational form. It's also the gate that prevents the platform from drifting into a weak content site.

### 10. LLM-led authoring, human-reviewed.

LLMs are categorically better than humans at cross-dimensional synthesis at our substrate's scale. We embrace this. The human's role is:
- **Editorial judgment**: is the framing fair? Are the caveats honest? Does the claim land?
- **Taste**: is this the right thing to say at all, given what we've already published?
- **Catch failures the agent can't see**: silent scope drift, mechanistic claims masquerading as statistical, over-confident phrasing on a low-confidence claim.

The human is **not** rewriting prose for prose's sake. If the LLM produced a sentence that says the right thing in OK words, we ship it. Editorial polish is the lowest-leverage activity in this system and we will not optimize for it.

### 11. Maintenance is part of authoring; a brief without lifecycle metadata isn't finished.

A methodology brief that doesn't declare staleness signals is incomplete. An applied insight that doesn't stamp every substrate input with vintage is incomplete. "Finished" includes the lifecycle. No "we'll add the metadata later" — later doesn't happen and the unmaintained brief is what tarnishes the platform.

### 12. The agent's trace is part of the deliverable.

Every published insight ships with a structured trace of the agent run that produced it: plan, retrievals, sub-syntheses, citation pass. The trace is consumer-facing in a "view methodology trace" UI affordance, not just internal logging. **If the trace is embarrassing, the insight isn't ready to publish.** This is how we enforce intermediate quality — the failure mode "looks good at end-to-end eval, garbage in the middle" doesn't survive a visible trace.

---

## III. Editorial section

### Confidence policy

- **High** — multiple substrate dimensions corroborate the claim; mechanistic basis is well-established; no significant caveats. (Example: "Plant X's nameplate capacity is 540 MW per EIA-860 Q2 2026." Substrate-grounded fact.)
- **Medium** — claim has solid analytical basis but depends on inferences from substrate (e.g., capacity-factor regression on 5 years of generation data) or on external data with known uncertainty.
- **Low** — claim is directionally supported but has significant uncertainty (forecasts, scenario-based reasoning, claims about unknown actor behavior). Publishable with explicit caveats.

**Not publishable**: claims where the agent cannot ground at least one substrate tuple; claims where confidence is "low" but the agent hasn't surfaced caveats.

### The five-question editorial filter

Every insight must answer all five questions before publish. Failing question 3 or 4 means the piece is content marketing, not insight, and doesn't ship.

1. **Who** is the reader of this insight (which actor — see `scope.actors[]` on the methodology brief)?
2. **What decision** are they currently making (or considering)?
3. **What would they decide without this insight?**
4. **What does our insight let them decide differently?**
5. **Is the marginal decision-quality improvement worth their time to read?**

This is the operational test that enforces principle 9 (substrate grounding as gate). Substrate grounding makes the insight *defensible*; the five-question filter makes the insight *useful*. Both are required.

**Example application (gridstatus.io blog post critique)** — "Net Load Ramps: Texas vs California" is technically accurate and well-written. It fails questions 3 and 4: a plant operator, financier, developer, or trader reading it would not change a decision they were making. They would close the tab and continue with what they were doing. The piece reads as marketing because the editorial filter that would have caught this isn't applied. Our gate.

**Caveat on the filter** — utility is the test; marketing is a downstream effect. We are not against insights that happen to build the platform's reputation. We are against insights that exist *primarily* for that purpose. Real users whose decisions our insights enable will become evangelists; that's good marketing. Writing for marketing impact first and hoping utility falls out is the trap.

### Attribution model

For v1: team handle (`InfraSure.ai Research`) on every brief and applied insight. Internal metadata records the human reviewer's identity for audit trail; does not surface publicly.

Revisit when we have a real research team with named experts. Individual attribution then becomes a tool for trust-building, not a vanity surface.

### Review chain

- **Methodology brief, new**: must be reviewed by user (or designated senior reviewer) before first publish.
- **Methodology brief, revision**: reviewer of the previous version, plus the user if the revision is semver-major.
- **Applied insight**: methodology brief author or senior intern review. Higher-confidence claims have lighter review touch; low-confidence claims with high-impact framing get the heaviest touch.
- **Trace inspection** on every insight pre-publish, regardless of reviewer level. If the trace is sloppy, the insight goes back.

### Takedown vs. revision

- **Revision** (default): something changed; update the brief, bump the snapshot, log the change in `lineage.supersedes`.
- **Takedown** (rare): claim was wrong in a way that revision can't repair. Brief gets a `withdrawn: true` flag with an explanation; the URL still resolves (citations don't break) but renders a withdrawal notice. Applied insights that cite a withdrawn brief get a banner.

### What an intern can publish without senior sign-off

- **Applied insights** instantiating an existing reviewed methodology brief, confidence: medium or high, that touch < N entities (TBD).
- **Methodology brief revisions** at semver-patch level (typo fix, citation update, no analytical change).

Anything else requires senior review. The cost of a bad publish is too high relative to the cost of waiting a day.

---

## IV. Process for evolving these principles

These principles are not load-bearing because they're written down — they're load-bearing because we hold the line on them. When the principles need to change:

1. **Propose** the change in a PR-style discussion (probably a section in `what_we_learned.md` of whichever brief surfaced the friction).
2. **Argue** what specifically forced the change. Avoid "this would be easier if…" — work backwards from a concrete failure that the principle prevented us from addressing.
3. **Decide** explicitly. User has final call.
4. **Log** the change in this file with a date and the brief that caused it.

The first revision is expected from the El Niño brief (predictions in [`05_first_methodology_brief/what_we_learned.md`](05_first_methodology_brief/what_we_learned.md)). Anticipate updates to commitment 3 (substrate grounding now needs to handle external grounding) and commitment 7 (staleness signals may need a `temporal_scale` field).

---

## V. Where this file goes

- **For now**: lives in `~/code/personal/renewablesinfo/insights_lab/01_principles.md`.
- **When user signs off**: copied (or graduated) to `business/principles/analysis.md` at the same authority as scalability / SEO / UI principles. At that point this lab file becomes a working copy and the `business/` copy becomes canonical.

Until graduation, this file is the canonical source.
