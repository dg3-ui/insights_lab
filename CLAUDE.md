# CLAUDE.md — InfraSure Insights (methodology lab)

**InfraSure Insights** is the **methodology / reasoning layer** above the InfraSure data substrate — the curated US energy-infrastructure platform (~15.5K plants, ~29.7K generators, ~9.8K queue projects, ~57K classified news articles; brand **InfraSure**, `www.infrasure.ai`). The substrate and its read-only MCP/data tools already exist. This repo adds the second surface: packaged, discoverable methodology that tells a model *how an InfraSure analyst reasons* — what to retrieve, how to reason, what NOT to claim, how to score confidence. The moat is **grounding, not fluency**.

**Where this sits (naming, so sessions don't get confused):**
- `~/code/personal/renewablesinfo_org` — the **platform repo** (`riorg` package + Next.js web app + the data pipeline that the MCP tools serve). The data lives there.
- `~/code/personal/renewablesinfo` — the **lab repo** (experiments). `insights_lab/` is one lab project inside it. **You are here.**
- This repo is **methodology only** — no data pipeline, no app, no build CLI (yet). It is "MCP-ready, not MCP-integrated" (`docs/01_scope_v0.md`).

**Status**: v0. One validated skill (`el_nino_enso`, test 001 PASS). The publish step, discovery tool, and eval harness are designed but not built — deliberately paused (see `TODO`-equivalent in `docs/06_architecture.md` §11).

## How To Work Here

There is **no build system**. The operational loop is the manual MCP/Claude test, and it is a **loop, not a one-shot** (`08_design_principles.md` P4):

```text
1. Load/paste resources/<domain>/<skill>/prompt_projection.md (+ knowledge.md, data_requirements.md).
2. Give a narrow test question (one region · one asset class). NOT "write an article about X".
3. Make the model identify required data BEFORE drafting; let it call the InfraSure MCP tools.
4. Review every claim against source refs + the resource's blocked_claims.
5. ITERATE — enrich, re-scope, challenge. The loop is the product, not overhead.
6. SAVE THE FULL TRANSCRIPT (raw source) — not just the final output.
7. Resolve it into test_runs/test_run_NNN.md (accepted/rejected claims, failures, fixes).
8. Log learning in docs/learning/logs/ and any tool gap in docs/09_mcp_roadmap.md.
```

Full protocol: `docs/05_mcp_test_protocol.md`. Onboarding fundamentals: `docs/learning/`.

## The MCP Feedback Loop (standing instruction)

**The MCP surface is a floor, not a ceiling.** As you author or test, you *will* hit "this call / field / filter would be super useful." When you do:

```text
DON'T treat a gap as a dead end and silently work around it.
DO   log it to docs/09_mcp_roadmap.md in the gap · workaround · roadmap form,
     then use the workaround to keep moving.
```

This is not optional housekeeping — a model has no memory between sessions, so `docs/09_mcp_roadmap.md` *is* the persistent back-of-mind for the tool surface. Each entry is a roadmap input that grows the platform from 12 tools toward 13 (`learning/01_mcp_basics.md`, `06_architecture.md` §11). The ledger is **data**; this instruction is what keeps it fed (`08` P3).

## Architecture

Four layers, repo → served → runtime → output (full diagram: `docs/06_architecture.md`):

```text
LAYER 0  SOURCE      this repo: authored, versioned methodology packages
LAYER 1  SERVED      InfraSure MCP (data tools, live) + skill catalog (one skill per package)
LAYER 2  RUNTIME     a Claude session: discover → load → ground → assemble → GATE  (a LOOP, w/ human checkpoint)
LAYER 3  OUTPUT      the content engine: blog · email · card · post — renderings of a VALIDATED insight only
```

The load-bearing seam is `resource.yml` (taxonomy → discovery, prompt sections → the served method, confidence_rules + blocked_claims → the gates). Keep the **methodology layer stable** and the **execution layer (model, orchestration, delivery, phrasing) swappable** — that is how the project absorbs LLM advances without rebuilding (`08` P1).

## Key Conventions

- **House doc style.** Every doc opens with a `> **Status**` blockquote, reasons in ASCII diagrams + tight tables, stays terse and grounded, and ends with a `See also` footer. Match it.
- **Ground or downgrade.** A claim with no tool result / named source is commentary, not an insight. Cross every material number to a structured field.
- **Label every input's job** before citing it: *grounds* (capacity, CF, PPA) · *frames* (descriptions, Wikipedia — never proof) · *routes* (owner, offtaker) · *external* (NOAA) · *logic* (crosswalks). (`learning/02`.)
- **The claim grammar**: condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance. A slot you can't fill is a downgrade or a blocked claim.
- **Content is downstream of validated insight** — always insight → gate → render, never the reverse (`08` P2).
- **Naming.** Package/slug is `snake_case` (`el_nino_enso`); the published Skill `name` is `kebab-case` (`el-nino-enso`). Folder name MUST equal `resource.yml.identity.slug`.
- **One domain folder + faceted tags.** A resource lives in one driver-grouped `domain/` folder, tagged with family · drivers · actors (`resources/README.md`).
- **`resources/_reference/` is form, not facts** — competitor/LinkedIn exemplars feed rendering + eval, quarantined from any claim's grounding.

## Don'ts

- **No blocked claims**: never emit an exact `$/MWh` or LMP from ENSO alone, never a plant-level production forecast without a model, never causal language where the evidence is directional.
- **No outreach/content before the gate passes** — a rendering is never the source of truth.
- **No unscoped scans** ("all US solar") — one region, one asset class per test.
- **No new MCP tools / agents / orchestrators / DB schemas in v0** — log the gap instead (`docs/09_mcp_roadmap.md`).
- **No `code/`, `scripts/`, or `data/` folders** until there is real implementation that belongs there (`README.md`).
- **Don't trust tool labels** — verify the entity you got is the one you wanted (the `get_plant` docstring mislabels 56051 as Topaz; it is a gas peaker).

## Docs Index

| Doc | What |
|-----|------|
| `README.md` | Repo map, read order, working rules, current task |
| `docs/00_project_brief.md` | What InfraSure Insights is + why (the moat) |
| `docs/01_scope_v0.md` | The exact v0 deliverable, what's out of scope, the after-V0 split |
| `docs/02_analysis_catalog.md` | The 7 analysis families (v0 = Exposure) |
| `docs/03_methodology_resource_standard.md` | The resource contract every package must meet |
| `docs/04_context_and_data_map.md` | Input taxonomy: substrate / external / descriptive / actor |
| `docs/05_mcp_test_protocol.md` | How to run the manual test; session capture + extraction; failure taxonomy |
| `docs/06_architecture.md` | The 4 layers, request lifecycle, terminology, gates, roadmap |
| `docs/07_discovery_spec.md` | `find_methodology` / `get_methodology` contract |
| `docs/08_design_principles.md` | Stable vs volatile · content downstream · process-data laws · iteration · no-mush |
| `docs/09_mcp_roadmap.md` | **The MCP feedback ledger** — log tool gaps/ideas here |
| `docs/learning/` | Onboarding: MCP basics, the substrate, methodology resources, prompt projection |
| `resources/README.md` | Methodology registry (domain · family · actor) |
| `resources/_reference/` | Exemplar corpus (form, not facts) |
| `resources/weather_and_climate/el_nino_enso/` | The first validated skill |
| `AGENTS.md` | The lean, vendor-neutral cut of this file |

## Read Order

```text
new contributor:  README.md → docs/01 → docs/learning/ (01→04) → resources/weather_and_climate/el_nino_enso/
senior reviewer:  README.md → docs/00 → docs/01 → docs/02 → docs/06 → docs/07 → docs/08
```
