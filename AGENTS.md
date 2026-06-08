# AGENTS.md — InfraSure Insights (methodology lab)

**InfraSure Insights** is the **methodology / reasoning layer** above the InfraSure data substrate (the curated US energy-infrastructure platform served via read-only MCP/data tools; brand **InfraSure**, `www.infrasure.ai`). The data and tools already exist; this repo adds packaged, discoverable methodology that tells a model *how an InfraSure analyst reasons* — what to retrieve, how to reason, what NOT to claim, how to score confidence. **The moat is grounding, not fluency.**

**Where this sits:** `~/code/personal/renewablesinfo_org` = the platform repo (`riorg` package + web app + data pipeline). `~/code/personal/renewablesinfo` = the lab repo; `insights_lab/` is one lab project inside it — **you are here**. This repo is methodology only: no data pipeline, no app, no build CLI. It is "MCP-ready, not MCP-integrated."

**Status**: v0. One validated skill (`el_nino_enso`, test 001 PASS); publish step / discovery tool / eval harness designed but deliberately not yet built.

> This is the lean cut. The fuller operational version is **`CLAUDE.md`** — read it for the full how-to-work loop, architecture diagram, and docs index.

## How To Work Here

No build system — the loop is the manual MCP/Claude test, and it is a **loop, not a one-shot**:

```text
load prompt_projection → narrow question → retrieve before drafting → review vs blocked_claims
  → ITERATE (enrich/re-scope) → SAVE THE FULL TRANSCRIPT → resolve into test_runs/ → log gaps
```

Full protocol: `docs/05_mcp_test_protocol.md`. Fundamentals: `docs/learning/`.

## The MCP Feedback Loop (standing instruction)

The MCP surface is a **floor, not a ceiling**. Whenever you hit "this call / field / filter would be useful," **log it to `docs/09_mcp_roadmap.md`** in the `gap · workaround · roadmap` form, then use the workaround to keep moving. A model has no cross-session memory, so that ledger *is* the persistent back-of-mind for the tool surface. Don't silently route around gaps — capture them; each is a roadmap input that grows the platform.

## Key Conventions

- **Ground or downgrade** — no tool result / named source ⇒ commentary, not an insight.
- **Label every input's job**: grounds · frames (never proof) · routes · external · logic (`learning/02`).
- **Claim grammar**: condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance.
- **Content is downstream of validated insight**: insight → gate → render, never the reverse (`08` P2).
- **Stable methodology, swappable execution** — absorb LLM advances by swapping the engine, not the discipline (`08` P1).
- **Naming**: slug/folder `snake_case` (`el_nino_enso`) = `resource.yml.identity.slug`; published Skill `name` `kebab-case` (`el-nino-enso`).
- **House doc style**: `> **Status**` header, ASCII diagrams, terse tables, `See also` footer.
- **`resources/_reference/` is form, not facts** — exemplars feed rendering + eval, never grounding.

## Don'ts

- No exact `$/MWh` / LMP from ENSO alone; no plant-level production forecast without a model; no causal language where evidence is directional.
- No outreach/content before the validation gate passes.
- No unscoped "all US solar" scans — one region, one asset class.
- No new MCP tools / agents / orchestrators / DB schemas / `code/`+`scripts/`+`data/` folders in v0 — log the gap instead.
- Don't trust tool labels — verify the entity is the one you wanted.

## Docs Index

`README.md` (map + read order) · `docs/00` brief · `docs/01` scope · `docs/02` analysis families · `docs/03` resource standard · `docs/04` data map · `docs/05` test protocol · `docs/06` architecture · `docs/07` discovery spec · `docs/08` design principles · `docs/09` **MCP roadmap ledger** · `docs/learning/` onboarding · `resources/README.md` registry · `resources/_reference/` exemplars · `resources/weather_and_climate/el_nino_enso/` first skill · `CLAUDE.md` full version.
