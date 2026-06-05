# Research 02 — Agentic Analytical Systems (2025-2026)

> Status: research complete. For reference only — our agent operates on a structured substrate, not open web. Many open-web patterns don't transfer.

## TL;DR

The 2025-2026 frontier converged on **planner → isolated subagents → synthesis → separate citation pass**, with end-to-end RL on long-horizon trajectories the only thing closing GAIA-style benchmarks. Dominant failure mode: **intermediate-step hallucination invisible to end-to-end eval** — bad plans, fabricated citations, silent scope drift accumulate inside multi-hop trajectories that look fine at the output. For a structured-substrate agent like ours the open-web playbook is mostly reference: we don't need breadth-first search; we need a planner decomposing against a known schema, deterministic tool-call retrieval, a methodology-grounding step, and per-claim provenance back to dimension rows. The bar to beat is "comprehensive but unauditable" — where every shipped deep-research product is stuck.

## Systems Investigated

- **OpenAI Deep Research** — single-agent RL-finetuned o3, 5-30 min/query, SOTA GAIA.
- **Anthropic Research (multi-agent)** — lead Opus plans, 3-5 Sonnet subagents parallel, separate citation pass. +90.2% over single-agent Opus internally; ~15× token cost.
- **Gemini Deep Research** — user-approved plan, async task manager for graceful failure recovery, 1M synthesis context, multi-pass self-critique.
- **Perplexity Deep Research** — agentic RAG loop, dozens of searches, 2-4 min, 100-300 sources, live process view.
- **Claude Code** — single-threaded master loop (`nO`), flat history, while-loop on tool-calls, Task tool spawns isolated subagents.
- **Devin (Cognition)** — VM-isolated; Devin's Brain + structured notes; 67% PR-merge; senior at understanding, junior at execution.
- **Anthropic "Building Effective Agents"** — five patterns: prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer.
- **ReAct / Reflexion / Self-RAG** — Thought-Action-Observation loop; verbal-reinforcement memory; reflection-token-driven adaptive retrieval.
- **MAST taxonomy** — 14 failure modes, 41-86.7% failure rates in production MAS.
- **Spider 2.0** — frontier models solve 10-17% of enterprise text-to-SQL vs 86% on Spider 1.0; nested schemas 27%→10%.
- **Eval/observability** — LangSmith (LangChain-native), Braintrust (eval-first, CI gates), Phoenix (OpenTelemetry, OSS).

## Architecture Patterns That Emerged

### Pattern 1: Plan → Execute → Synthesize → Cite, as four separate passes
**Where seen:** Anthropic Research, Gemini, OpenAI, all production deep-research.
**What it does:** Planner decomposes & saves a plan; executors run sub-queries (often parallel); separate synthesis call composes the artifact; **citation is a fourth deterministic pass**, not inline.
**For us:** **ADOPT**.
**Why:** Mirrors how an analyst thinks and is the only structure where intermediate quality is inspectable. Citation is split out specifically because inline citation lets the model fabricate references.

### Pattern 2: Orchestrator + isolated subagents with structured-output contracts
**Where seen:** Anthropic multi-agent research, Claude Code Task tool, LangGraph subagents, Devin 2.0.
**What it does:** Parent ships a minimal context package per child (task, policies, artifacts); child runs in fresh context; child returns **structured summary**, not raw thoughts. Anthropic's contract: objective + output format + tools + clear boundaries.
**For us:** **ADAPT** — useful for per-dimension parallelism (one subagent per substrate dim: generation, financial, news, regional), only with typed schemas, only when sub-tasks are independent. MAST data: 79% of MAS failures are spec ambiguity / coordination breakdown.
**Why:** ~15× chat token cost. Worth it for long-form briefs, lethal for interactive queries. Sparingly + deterministic contracts only.

### Pattern 3: Single-threaded master loop with flat history
**Where seen:** Claude Code (`nO`), OpenAI Deep Research single-agent, Devin's Brain.
**What it does:** `while(tool_calls_present): step()`, flat history, no competing personas. Subagents only via explicit Task tool, not as default.
**For us:** **ADOPT for the main loop**.
**Why:** Lower coordination overhead, single explainable trace, easier to audit. Anthropic principle: transparency of planning steps > parallel capability for high-stakes output.

### Pattern 4: Methodology / skill retrieval before synthesis
**Where seen:** AgentAda (skill lookup), DataSage (external-knowledge retrieval), Self-RAG (retrieval as learned reflex), semantic-layer SQL agents.
**What it does:** Before answering, retrieve a curated **methodology artifact** (technique, formula, pattern) that constrains synthesis.
**For us:** **ADOPT — central to design**.
**Why:** This is our differentiator. Grounding in methodology briefs (capacity-factor norms, queue conversion rates, LCOE composition, BA congestion patterns) turns "comprehensive-looking" into "actually correct." Without it the agent emits generic plausible prose.

### Pattern 5: Deterministic typed tool calls over the substrate, not vector RAG
**Where seen:** Claude Code's regex `GrepTool` over vectors; enterprise text-to-SQL agents collapse on nested schemas (10% success).
**For us:** **ADOPT**.
**Why:** Our substrate is a known schema (15K plants × ~100 cols, dimension parquets). Named retrieval tools (`get_plants_in_region`, `get_generation_for_plant`) beat vector RAG because the agent can name what it wants. Vector RAG is for unstructured corpora; ours isn't.

### Pattern 6: Evaluator-optimizer with explicit 4-track stopping
**Where seen:** Gemini "multiple passes of self-critique", Anthropic evaluator-optimizer, Reflexion verbal-reinforcement, CaRT ("know when you know enough").
**What it does:** Second model scores draft against criteria; loop continues until criteria met OR budget exhausted OR repetition detected.
**For us:** **ADOPT, bounded**.
**Why:** Termination is hard (CaRT: LLMs overshoot or undershoot). Need four parallel stop tracks: (1) goal — methodology checklist satisfied; (2) resource — iter/token/$ cap; (3) pathology — same retrieval twice = stop; (4) eval-gate — provenance check on every numeric claim.

## Failure Modes

1. **Intermediate hallucination invisible to end-to-end eval.** Misleading plans and fabricated mid-trajectory facts are silent at output ("Why Your DR Agent Fails", arxiv 2601.22984). **Mitigation:** every numeric claim carries a `(dimension, entity_id, column, value)` tuple back to substrate. No tuple → strip the claim.

2. **Citation hallucination at scale.** Ansari 2026: 100 fabricated citations across 53 NeurIPS papers; 66% pure fabrication, 27% partial-attribute corruption. Perplexity DR itself still cites incorrectly. **Mitigation:** citations are deterministic — emitted by the retrieval tool, not by the LLM. LLM only references retrieved IDs.

3. **Scope drift in multi-hop trajectories.** Entity scope quietly broadens between steps ("ERCOT solar" → "ERCOT renewables") because latter has more results. **Mitigation:** scope is a typed object re-passed verbatim to every sub-step.

4. **Multi-agent coordination collapse (MAST).** 79% of production MAS failures are spec ambiguity + unstructured coordination — subagents duplicate work, skip verification. **Mitigation:** typed validated schemas on every intermediate handoff. No free-text intermediates.

5. **Premature stopping / runaway loops.** ReAct stuck repeating; CaRT shows LLMs can't natively recognize "enough." **Mitigation:** explicit per-sub-q iteration budget + methodology-required-facts checklist before synthesis fires.

Bonus: the **text-to-SQL cliff** (Spider 2.0: 10-17% success, nested-schema collapse) is the strongest argument against "let the agent write SQL against the warehouse." Per-dimension typed tool functions are the right abstraction.

## Architecture Sketch For Our Insight Agent

```
INPUTS: insight_topic + scope{geo,tech,vintage} + methodology_brief_id
   |
   v
PLANNER (1 call)  -> ordered sub-qs, each tagged w/ dimensions + brief sections
   |
   v
METHODOLOGY LOOKUP  -> briefs/{id}.md => required_facts checklist + formulas + caveats
   |
   v
ORCHESTRATOR (single-threaded master loop):
   for sub_q in plan:
     SCOPE-GROUND   -> resolve scope to typed entity_id set
     RETRIEVE       -> typed tools: get_plants / get_generation / get_financial
                                     get_news_facts / get_regional_context / get_queue
                       -> rows w/ row-level provenance
     SUB-SYNTHESIZE -> claim ::= (text, tuple_ref+)
     SELF-CHECK     -> 4-track stop: goal | resource | pathology | provenance-gate
   |
   v
FINAL SYNTHESIS    -> compose narrative; re-validate brief checklist at whole-insight level
   |
   v
CITATION PASS      -> deterministic; inject tuple_refs as inline substrate cites;
                       emit scope manifest (exact entity_ids this insight applies to)
   |
   v
OUTPUT: markdown insight + scope manifest + brief ref + human-review queue entry
```

Starting point, not final. Open decisions below.

## Open Questions

1. **Methodology briefs: data or prompts?** First-class substrate rows (queryable, versioned, citable) vs. prompt-template fragments. First-class is more auditable but adds substrate complexity.

2. **Scope fan-out granularity.** Same methodology over 2,400 ERCOT solar projects → 2,400 applied insights, or one parameterized insight rendered per project? Economic question, not just architectural.

3. **Subagent fan-out yes/no?** Anthropic's +90.2% / 15× cost is real, but Claude Code's single-thread bet won on debuggability. Probably yes for full briefs, no for interactive — need to draw the line explicitly.

4. **Eval substrate.** Human-authored golden insights per methodology, or scoring on substrate-claim-grounding rate? Both? The deep-research literature doesn't have an answer.

5. **Stopping when the substrate itself is sparse.** Retrieved 4 rows for a 200-plant region — "done" or "needs more digging"? Pathology detection alone won't catch a real but thin answer.

## Sources

- OpenAI Deep Research — https://openai.com/index/introducing-deep-research/
- Anthropic Building Effective Agents — https://www.anthropic.com/research/building-effective-agents
- Anthropic Multi-Agent Research System — https://www.anthropic.com/engineering/multi-agent-research-system
- Anthropic Effective Context Engineering — https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Anthropic Citations API — https://claude.com/blog/introducing-citations-api
- Anthropic "think" tool — https://www.anthropic.com/engineering/claude-think-tool
- Cognition Devin 2025 Review — https://cognition.ai/blog/devin-annual-performance-review-2025
- Claude Code master loop (PromptLayer) — https://blog.promptlayer.com/claude-code-behind-the-scenes-of-the-master-agent-loop/
- Claude Code architecture (ZenML) — https://www.zenml.io/llmops-database/claude-code-agent-architecture-single-threaded-master-loop-for-autonomous-coding
- Gemini Deep Research — https://gemini.google/overview/deep-research/
- Gemini DR API — https://ai.google.dev/gemini-api/docs/deep-research
- Perplexity DR review — https://www.secondtalent.com/resources/perplexity-deep-research-review/
- Perplexity pipeline — https://ziptie.dev/blog/how-perplexity-ai-answers-work/
- ReAct — https://arxiv.org/pdf/2210.03629
- Reflexion — https://arxiv.org/abs/2303.11366
- Self-RAG — https://arxiv.org/abs/2310.11511
- MAST taxonomy — https://arxiv.org/abs/2503.13657
- Why Your DR Agent Fails — https://arxiv.org/html/2601.22984v1
- Reference hallucinations in commercial LLMs — https://arxiv.org/html/2604.03173v1
- Spider 2.0 — https://spider2-sql.github.io/
- ReFoRCE — https://arxiv.org/pdf/2502.00675
- CaRT — https://arxiv.org/pdf/2510.08517
- Anatomy of Termination — https://towardsai.net/p/machine-learning/when-should-an-agent-stop-the-anatomy-of-termination
- AgentAda — https://arxiv.org/pdf/2504.07421
- DataSage — https://arxiv.org/pdf/2511.14299
- Data-to-Dashboard — https://arxiv.org/html/2505.23695v1
- Braintrust eval platforms 2025 — https://www.braintrust.dev/articles/best-llm-evaluation-platforms-2025
- Agenta observability platforms 2025 — https://agenta.ai/blog/top-llm-observability-platforms
