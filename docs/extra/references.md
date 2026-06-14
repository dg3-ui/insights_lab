# Architecture Reference Repositories

> **Status**
> First-pass landscape scan, created 2026-06-14. This file is for architectural learning only: these inputs frame how to package, serve, validate, and operate analyst methods. They do not ground InfraSure energy-infrastructure claims. Star and fork counts are point-in-time GitHub API values from 2026-06-14 and will drift.

## Selection Lens

| Keep if | Why it matters for InfraSure Insights |
|---|---|
| Official / firm-backed public repo | Better signal on enterprise architecture, governance, and repeatable packaging. |
| Packaged domain methods, not only toy prompts | InfraSure is building analyst methodology, not demo chatbots. |
| Clear separation of method, tools, runtime, and output | Matches the stable-method / swappable-execution principle. |
| Grounded data access pattern | Supports the moat: structured evidence, citations, and source-ref discipline. |
| Validation or governance layer | Maps to gates, blocked claims, test runs, and MCP gap ledgers. |

## Read Order

```text
1. anthropics/financial-services       # closest structural analog
2. anthropics/knowledge-work-plugins   # sibling pattern for role/workflow plugins
3. anthropics/skills                   # skill packaging and progressive disclosure
4. anthropics/claude-plugins-official  # plugin structure and marketplace conventions
5. openai/openai-agents-python         # runtime handoffs / tracing / guardrail vocabulary
6. microsoft/agent-framework           # production multi-agent workflow architecture
7. google/adk-python + adk-samples     # agent development kit and sample-agent organization
8. AWS data-exploration/platform refs  # data platform and governed runtime patterns
```

## Primary Analog

| Repo | Signal | Why it is relevant | Study angle |
|---|---:|---|---|
| [anthropics/financial-services](https://github.com/anthropics/financial-services) | 31,035 stars / 4,400 forks | Public, firm-built package of finance analyst workflows. Same method ships as Claude plugin and Managed Agent template. Local clone: `.financial-services`. | How to split vertical skills, workflow agents, managed-agent wrappers, MCP connectors, validation scripts, and human-signoff guardrails. |

Local shape worth studying:

```text
financial-services/
  .claude-plugin/marketplace.json
  plugins/
    vertical-plugins/      # source skills, commands, connector config
    agent-plugins/         # self-contained workflow agents with bundled skills
    partner-built/         # partner data-provider plugins
  managed-agent-cookbooks/ # headless wrappers: agent.yaml, subagents, steering examples
  scripts/                 # check, validate, skill sync, deploy/orchestrate
```

## Direct Comparables

| Repo | Signal | Why it is relevant | Study angle |
|---|---:|---|---|
| [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) | 20,560 stars / 2,428 forks | Anthropic sibling repo for role/team/company plugins. It explicitly bundles skills, connectors, slash commands, and sub-agents by job function. | Compare role-centric packaging with InfraSure's resource-centric packages. |
| [anthropics/skills](https://github.com/anthropics/skills) | 150,318 stars / 17,744 forks | Public repository for Agent Skills. Strongest current reference for portable skill folder structure. | How much of `resources/<domain>/<slug>/` can later emit or map to a standard skill. |
| [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) | 30,057 stars / 3,246 forks | Official Anthropic-managed directory of Claude Code plugins. Shows plugin conventions and marketplace structure. | Plugin packaging rules, trust boundaries, and discovery surface. |
| [Agent Skills overview](https://agentskills.io/home) | standard / docs | Describes skills as lightweight folders containing `SKILL.md`, plus optional scripts, references, templates, and assets. | Progressive disclosure and package portability. |
| [Model Context Protocol intro](https://modelcontextprotocol.io/docs/getting-started/intro) | standard / docs | Defines MCP as the open standard for connecting AI apps to data sources, tools, and workflows. | Keep InfraSure's MCP surface separate from methodology packages; log tool gaps instead of hiding them. |

## Runtime / Orchestration Comparables

| Repo | Signal | Why it is relevant | Study angle |
|---|---:|---|---|
| [openai/openai-agents-python](https://github.com/openai/openai-agents-python) | 27,130 stars / 4,189 forks | Official OpenAI multi-agent workflow framework. | Borrow vocabulary for handoffs, guardrails, tracing, and evaluation without adopting runtime complexity in v0. |
| [microsoft/agent-framework](https://github.com/microsoft/agent-framework) | 11,313 stars / 1,897 forks | Microsoft framework for building, orchestrating, and deploying AI agents and multi-agent workflows across Python and .NET. | Production workflow primitives, state, checkpointing, enterprise concerns. |
| [microsoft/semantic-kernel](https://github.com/microsoft/semantic-kernel) | 28,115 stars / 4,646 forks | Mature Microsoft SDK for model-agnostic agent and app orchestration. | Historical enterprise patterns; use `agent-framework` as the forward-looking reference. |
| [google/adk-python](https://github.com/google/adk-python) | 20,097 stars / 3,560 forks | Google's code-first toolkit for building, evaluating, and deploying agents. | How Google organizes agent runtime, evaluation, deployment, and docs. |
| [google/adk-samples](https://github.com/google/adk-samples) | 9,652 stars / 2,667 forks | Ready-to-use agents built on ADK, from simple bots to complex multi-agent workflows. | Sample-agent directory structure and reusable patterns. |
| [microsoft/ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) | 67,157 stars / 22,162 forks | High-signal curriculum repo, not a product architecture. | Vocabulary and onboarding sequence only. |

## Data / Analytics Platform Comparables

| Repo | Signal | Why it is relevant | Study angle |
|---|---:|---|---|
| [aws-samples/sample-agentic-platform](https://github.com/aws-samples/sample-agentic-platform) | 96 stars / 44 forks | AWS sample of an agentic platform with shared core library, gateway services, and agents across frameworks. Lower adoption, but architecture-focused. | Platform boundaries: core, gateway, agent implementations, deployment options. |
| [aws-solutions-library-samples/guidance-for-agentic-data-exploration-on-aws](https://github.com/aws-solutions-library-samples/guidance-for-agentic-data-exploration-on-aws) | 14 stars / 6 forks | AWS guidance for data fragmentation: agent team automates discovery, connection, and analysis across siloed systems. | Data-discovery workflow and source-connection patterns. |
| [aws-samples/sample-agentic-value-accelerator](https://github.com/aws-samples/sample-agentic-value-accelerator) | 28 stars / 6 forks | AWS financial-services platform for planning, building, operating, securing, and governing AI systems. | Governance/control-plane ideas; adoption signal is still early. |
| [Google-Cloud-AI/agent-platform](https://github.com/Google-Cloud-AI/agent-platform) | 204 stars / 36 forks | Curated Gemini Enterprise Agent Platform samples and tutorials. | Enterprise platform onboarding and sample catalog organization. |
| [i-am-bee/beeai-framework](https://github.com/i-am-bee/beeai-framework) | 3,291 stars / 449 forks | Linux Foundation / BeeAI ecosystem framework for production-ready Python and TypeScript agents. | Governance, workflow events, telemetry, and multi-agent reliability patterns. |

## Broader References

| Repo | Signal | Keep / defer |
|---|---:|---|
| [openai/openai-cookbook](https://github.com/openai/openai-cookbook) | 74,145 stars / 12,549 forks | Keep for examples, not architecture. It is a cookbook, not a methodology packaging system. |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 34,659 stars / 5,822 forks | Useful runtime reference for stateful workflows; not big-firm official. Defer until InfraSure needs runtime orchestration. |
| [langchain-ai/open_deep_research](https://github.com/langchain-ai/open_deep_research) | 11,695 stars / 1,668 forks | Useful research-agent example; not as close to domain-method packaging as Anthropic's repos. |
| [microsoft/autogen](https://github.com/microsoft/autogen) | high historical signal | Defer. Public search result notes maintenance mode and points forward to Microsoft Agent Framework. |

## Transfer Questions

| Question | Why it matters |
|---|---|
| Should every InfraSure `resource.yml` be able to emit a future `SKILL.md`? | Keeps methodology portable without committing to a runtime now. |
| Should we introduce a vertical/domain layer separate from individual resources? | Anthropic separates vertical skill source from workflow agent bundle. InfraSure currently has domain folders plus shared `_` layers. |
| What becomes the validation equivalent of `scripts/check.py`? | We need checks for `resource.yml`, blocked claims, source-ref grammar, prompt projection, and transcript/test-run linkage. |
| What is the "managed-agent wrapper" analog for InfraSure? | Likely future only: a served skill catalog / MCP-ready loader, not a v0 orchestrator. |
| How do we encode human approval checkpoints? | Anthropic agents stop after key artifacts; InfraSure's equivalent is gate before render. |

## Do Not Import Yet

| Pattern | Reason |
|---|---|
| Full multi-agent runtime | v0 is methodology only; orchestration belongs after validated resources exist. |
| Partner connector marketplace | InfraSure already has a curated data substrate; log MCP gaps before adding surface area. |
| Content generation first | Keep insight -> gate -> render. Reference repos may optimize artifact production; InfraSure should optimize grounded claims first. |
| Generic "all data" scans | Violates scoped-entity discipline. Use one region, one asset class, one analytic family. |

## See also

- [Architecture](../architecture.md)
- [Principles](../principles.md)
- [MCP gaps](../status/mcp_gaps.md)
- [Resource standard](../method/resource_standard.md)
- Local study clone: [.financial-services](../../.financial-services)
