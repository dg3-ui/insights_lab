# CLAUDE.md — InfraSure Insights (methodology lab)

**InfraSure Insights** is the **methodology / reasoning layer** above the InfraSure data substrate — the curated US energy-infrastructure platform (~15.5K plants, ~29.7K generators, ~9.8K queue projects, ~57K classified news articles; brand **InfraSure**, `www.infrasure.ai`). The substrate and its read-only MCP/data tools already exist. This repo adds the second surface: packaged, discoverable methodology that tells a model *how an InfraSure analyst reasons* — what to retrieve, how to reason, what NOT to claim, how to score confidence. The moat is **grounding, not fluency**.

**Where this sits (naming, so sessions don't get confused):**
- `~/code/personal/renewablesinfo_org` — the **platform repo** (`riorg` package + Next.js web app + the data pipeline that the MCP tools serve). The data lives there.
- `~/code/personal/renewablesinfo` — the **lab repo** (experiments). `insights_lab/` is one lab project inside it. **You are here.**
- This repo is **methodology only** — no data pipeline, no app, no build CLI (yet). It is "MCP-ready, not MCP-integrated" (`docs/use_cases.md`).

**Status**: v0. One validated skill (`el_nino_enso`, test 001 PASS). The publish step, discovery tool, and eval harness are designed but not built — deliberately paused (see `TODO`-equivalent in `docs/status/capabilities.md`).

## How To Work Here

There is **no build system**. The operational loop is the manual MCP/Claude test, and it is a **loop, not a one-shot** (`docs/principles.md` P4):

```text
1. Load/paste resources/<domain>/<skill>/prompt_projection.md (+ knowledge.md, data_requirements.md).
2. Give a narrow test question (one region · one asset class). NOT "write an article about X".
3. Make the model identify required data BEFORE drafting; let it call the InfraSure MCP tools.
4. Review every claim against source refs + the resource's blocked_claims.
5. ITERATE — enrich, re-scope, challenge. The loop is the product, not overhead.
6. SAVE THE FULL TRANSCRIPT (raw source) — not just the final output.
7. Resolve it into test_runs/test_run_NNN.md (accepted/rejected claims, failures, fixes).
8. Log learning in docs/learning/logs/ and any tool gap in docs/status/mcp_gaps.md.
```

Full protocol: `docs/process/test_protocol.md`. Onboarding fundamentals: `docs/learning/`.

This loop is packaged as slash commands (thin conductors over the canon, not restatements — `docs/process/commands.md`): **`/new-resource`** (author), **`/test-resource`** (run the test loop on an existing slug), **`/extract`** (resolve a saved transcript into a `test_run` + ledger/learning), and Tier-2 **`/render`** (render a gated studio brief → blog/report/email + grounded charts/maps; the model generates the artifact itself, P6). Tier-2 `/gate-check` and `/recap` are planned.

## The MCP Feedback Loop (standing instruction)

**The MCP surface is a floor, not a ceiling.** As you author or test, you *will* hit "this call / field / filter would be super useful." When you do:

```text
DON'T treat a gap as a dead end and silently work around it.
DO   log it to docs/status/mcp_gaps.md in the gap · workaround · roadmap form,
     then use the workaround to keep moving.
```

This is not optional housekeeping — a model has no memory between sessions, so `docs/status/mcp_gaps.md` *is* the persistent back-of-mind for the tool surface. Each entry is a roadmap input that grows the platform from 12 tools toward 13 (`learning/01_mcp_basics.md`, `docs/status/capabilities.md`). The ledger is **data**; this instruction is what keeps it fed (`principles.md` P3).

## Architecture

Four layers, repo → served → runtime → output (full diagram: `docs/architecture.md`):

```text
LAYER 0  SOURCE      this repo: authored, versioned methodology packages
LAYER 1  SERVED      InfraSure MCP (data tools, live) + skill catalog (one skill per package)
LAYER 2  RUNTIME     a Claude session: discover → load → ground → assemble → GATE  (a LOOP, w/ human checkpoint)
LAYER 3  OUTPUT      render a VALIDATED insight → blog · report · email via /render. BASELINE (default, NO studio): gated insight → /render — MCP + a methodology package alone is useful. SELECTIVE lane: studio/ — captured briefs (studio/<subject>/<phenomenon>.md, §1 = single source of truth; subject = scope ladder; direction = meta-tag) + _triage (internal) + gallery; most outputs skip it (the accuracy/home-run pass). posture on the face, the cap grade never renders (confidence_model)
```

The load-bearing seam is `resource.yml` (taxonomy → discovery, prompt sections → the served method, confidence_rules + blocked_claims → the gates). Keep the **methodology layer stable** and the **execution layer (model, orchestration, delivery, phrasing) swappable** — that is how the project absorbs LLM advances without rebuilding (`principles.md` P1).

## Key Conventions

- **House doc style.** Every doc opens with a `> **Status**` blockquote, reasons in ASCII diagrams + tight tables, stays terse and grounded, and ends with a `See also` footer. Match it.
- **Ground or downgrade.** A claim with no tool result / named source is commentary, not an insight. Cross every material number to a structured field.
- **Label every input's job** before citing it: *grounds* (capacity, CF, PPA) · *frames* (descriptions, Wikipedia — never proof) · *routes* (owner, offtaker) · *external* (NOAA) · *logic* (crosswalks) · *form* (`resources/_*` — shapes the rendering, never grounding). (`learning/02`.)
- **The claim grammar**: condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance. A slot you can't fill is a downgrade or a blocked claim.
- **Content is downstream of validated insight** — always insight → gate → render, never the reverse (`principles.md` P2). **Baseline output needs no studio**: a gated insight (MCP + a methodology package) renders directly via `/render`. `studio/` is the **selective** lane on top — when a piece goes through it, the brief originates there (studio-first; bottom_up before top_down) before render/gallery; it never originates the insight, which is always gated upstream (`studio/README.md`).
- **Re-ground on use.** Substrate numbers in any rendered/studio artifact are dated MCP snapshots — re-fetch the named entities against the live MCP and reconcile drift before any number ships externally (`studio/README.md`).
- **Confidence is three axes, not one** (`docs/method/confidence_model.md`): calibration cap (internal grade, weakest input) · event likelihood (sourced, on output) · materiality (band, internal). On a rendered face: posture + event + settledness; the cap grade never renders. References inform, don't bind — they shape the *analysis*, not just the form, and the model improves on top (`principles.md` P6).
- **Naming.** Package/slug is `snake_case` (`el_nino_enso`); the published Skill `name` is `kebab-case` (`el-nino-enso`). Folder name MUST equal `resource.yml.identity.slug`.
- **One domain folder + faceted tags.** A resource lives in one driver-grouped `domain/` folder, tagged with family · drivers · actors (`resources/README.md`).
- **`_`-prefixed `resources/` folders are shared layers, not packages** — no `resource.yml`/slug, composed at session time: `_principles` (rubric · voice) loads at draft; `_style` · `_craft` · `_reference` load post-gate only. Packages carry ONLY the method (`resources/README.md`, the underscore rule).
- **`resources/_reference/` is form, not facts** — competitor/LinkedIn exemplars feed rendering + eval, quarantined from any claim's grounding.

## Don'ts

- **No blocked claims**: never emit an exact `$/MWh` or LMP from ENSO alone, never a plant-level production forecast without a model, never causal language where the evidence is directional.
- **No outreach/content before the gate passes** — a rendering is never the source of truth.
- **No unscoped scans** ("all US solar") — one region, one asset class per test.
- **No new MCP tools / agents / orchestrators / DB schemas in v0** — log the gap instead (`docs/status/mcp_gaps.md`).
- **No `code/`, `scripts/`, or `data/` folders** until there is real implementation that belongs there (`README.md`).
- **Don't trust tool labels** — verify the entity you got is the one you wanted (the `get_plant` docstring mislabels 56051 as Topaz; it is a gas peaker).

## Docs Index

Docs are grouped by job (folder = job), with the stable/volatile seam as a folder boundary (P1). Full front-door map + per-audience read order: `docs/README.md`.

| Doc | Job |
|-----|-----|
| `docs/architecture.md` | **The front door** — what it is, the end-to-end flow (Mermaid + ASCII), the 4 layers, terminology, the gate |
| `docs/principles.md` | The discipline (P1–P7): stable vs volatile · content downstream · process-data laws · iteration · no-mush · references-inform-not-bind/the-model-improves-on-top (P6) · calibration-as-posture (P7) |
| `docs/use_cases.md` | The 2 buckets × audience (Pillar 3) + the V0 scope contract + the validation method + the activation boundary |
| `docs/method/` | The "how to reason & build" contract: `analysis_families` · `resource_standard` · `confidence_model` (the 3-axis canon) · `data_map` (source_ref owner) · `discovery_spec` |
| `docs/process/` | The loop: `test_protocol` (manual test, capture, failure taxonomy, feedback intake) · `commands` (the toolchain design) |
| `docs/status/` | **Volatile hub**: `capabilities` (build status + open decisions) · `mcp_gaps` (tool-gap ledger) · `commands` (registry) |
| `docs/plans/` | The active working plans (the real currency of "what's next") |
| `docs/learning/` | Onboarding fundamentals: MCP basics · substrate · methodology resources · prompt projection |
| `studio/` | **Layer 3 output layer** — subject/phenomenon render briefs (§1 = single source of truth; subject = scope ladder, direction = meta-tag) · `_triage.md` (internal ACT/WATCH/NOISE board) · subject guides; post-gate, rendered via `/render`. `studio/README.md` is its front door |
| `resources/README.md` | The package + shared-layer registry (domain · family · actor + the underscore rule) |
| `resources/_reference/` | Exemplar corpus (form, not facts) |
| `resources/weather_and_climate/el_nino_enso/` | The first validated skill |
| `README.md` / `AGENTS.md` | Repo map + working rules / the lean vendor-neutral cut of this file |

## Read Order

```text
new contributor:  README.md → docs/architecture.md → docs/learning/ (01→04) → resources/weather_and_climate/el_nino_enso/
senior reviewer:  docs/architecture.md → docs/principles.md → docs/use_cases.md → docs/method/ → docs/status/
```
