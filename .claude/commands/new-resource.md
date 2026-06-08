---
description: Author a new InfraSure Insight methodology resource — the generalized ENSO-creation process
argument-hint: <topic or question, e.g. "drought exposure for hydro" or "offtaker concentration risk">
---

You are authoring a **new InfraSure Insight methodology resource** for: **$ARGUMENTS**

This is the repeatable, turn-the-crank version of how `el_nino_enso` was built. It is the **ENGINE** of the lab's dual strategy:

```text
INPUTS                                   ENGINE (this command)            OUTPUT
.learning/        foundational knowledge   PHASE 0 frame                   resources/<domain>/<slug>/
external source   live state (NOAA-like)   PHASE 1 scaffold                 a complete, grounded,
InfraSure MCP     real asset grounding     PHASE 2 knowledge                manually-tested, registered
resources/_reference   form, not facts     PHASE 3 method                   methodology package
docs/02·03·04·08  the method canon         PHASE 4 ground · 5 test-loop      (= the el_nino_enso analog)
templates/        the scaffold             PHASE 6 publish · 7 register
```

**Read before you start** (this command orchestrates the canon — follow it, do not duplicate it):
`docs/03` (the contract every package meets) · `docs/02` (the 7 families) · `docs/04` (input taxonomy: grounds/frames/routes/external/logic) · `docs/05` (the test protocol) · `docs/08` (the 5 principles — load-bearing) · `resources/README.md` (registry + taxonomy) · `CLAUDE.md` (conventions + the working loop). Your worked exemplar is `resources/weather_and_climate/el_nino_enso/` — mirror its file set and rigor.

---

## PHASE 0 — FRAME (does this resource deserve to exist?)

- Write the **atomic question** in the `docs/02` grammar. Reject it if it is market commentary — *could it be written without any InfraSure entity, id, or field?* Then it is not a resource.
- Pick the **analysis family** (`docs/02`: exposure · performance · commercial · development_risk · portfolio_strategy · market_context · event_translation).
- Pick the **driver + domain**. Reuse an existing `domain/` folder if the driver fits; create a new domain only for a genuinely new external driver (`resources/README.md`).
- Decide the **slug** (`snake_case`) and Skill **name** (`kebab-case`). Folder name MUST equal `resource.yml.identity.slug`.
- **P1 check** (`docs/08`): name what is *stable* here (the claim grammar, blocked_claims, taxonomy) vs *volatile* (model, phrasing, plumbing). You are authoring the stable layer.

## PHASE 1 — SCAFFOLD (clean copy of the full template set)

- Copy `templates/` into `resources/<domain>/<slug>/`, renaming to the package files:

```text
methodology_resource.template.md   → resource.md
methodology_resource.template.yml  → resource.yml
knowledge.template.md              → knowledge.md
prompt_projection.template.md      → prompt_projection.md
data_requirements.template.md      → data_requirements.md
skill.template.md                  → SKILL.md          (UPPERCASE in the package root)
applied_insight.template.md        → examples/applied_insight_001.md
mcp_test_run.template.md           → test_runs/test_run_001.md
```

- Fill `resource.yml` **identity** + **taxonomy** (`domain · family · drivers · actors`) + `knowledge_ref: knowledge.md`.
- Every section in those templates carries `<placeholder>` guidance. If one is unclear, the filled-in `el_nino_enso` package is your reference.

## PHASE 2 — KNOWLEDGE (the cited mechanism library → `knowledge.md`)

- **Foundational basics** come from `.learning/` (the shared vault — risk, weather/climate, electricity-market, project-finance notes). **Live state** comes from the external source for this driver (NOAA-equivalent), pulled fresh with a date.
- State the mechanism and **rate its robustness**; mark each input's job (`docs/04`): *grounds* vs *frames* vs *routes* vs *external* vs *logic*. Cite everything. A current-state value must always carry the date it was pulled.

## PHASE 3 — METHOD (the control surface → `resource.md` + `prompt_projection.md` + `data_requirements.md`)

- Meet `docs/03`: question_grammar · scope · procedure (the **real tool sequence**) · allowed_claims · **blocked_claims** · confidence_rules (cap at the weakest input) · required caveats · actor_relevance · staleness_signals.
- The **claim grammar** (`CLAUDE.md`): condition + scoped entities + mechanism + evidence + confidence + caveat + actor relevance. A slot you cannot fill is a downgrade or a blocked claim.
- `data_requirements.md`: the retrieval plan (which MCP tools, in what order) + known tool gaps + missing-data handling.

## PHASE 4 — GROUND IN REALITY (no invented examples)

- Exercise the **InfraSure MCP data tools live** for the scope, and pull the **external state live**. Fill `examples/applied_insight_001.md` with **real** ids / numbers / `as_of` — never placeholders.
- Hit an empty result or an unwired filter? That is a tool gap: **log it to `docs/09_mcp_roadmap.md`** (`gap · workaround · roadmap`), then use the workaround (e.g. a `state=` proxy) and keep moving.

## PHASE 5 — TEST LOOP (it is a loop, not one-shot — `docs/05`, `docs/08` P4)

- Run the manual MCP/Claude test on **one narrow question** (one region · one asset class). Make the model identify required data **before** drafting. Then **iterate** — enrich, re-scope, challenge. The loop and its human checkpoint *are* the product.
- **Save the full transcript** (raw source — `docs/08` P3), then resolve it into `test_runs/test_run_001.md`: accepted / rejected claims, failures by taxonomy, fixes. **Extract** the prompting moves + fail→fix pairs (this is the process data that sharpens the next resource).
- Review every claim against `blocked_claims` and the gate: source ref present? confidence capped? caveats attached? **no `$/MWh`, no plant-level forecast, no causal-where-directional**?

## PHASE 6 — PUBLISH THE SKILL (→ `SKILL.md`)

- Frontmatter: `name` (kebab) + `description` (**what it does AND when to use it** — this is the discovery match-text, ≤1024 chars). Body = the method. Bundled refs = `knowledge.md`, the example, `data_requirements.md` (`docs/07`).
- Optional: hand to Anthropic's **skill-creator** to optimize the description for triggering + run eval/variance. Our domain rubric = the gate above; skill-creator supplies the generic runner.

## PHASE 7 — REGISTER + LOG (close the loop)

- Add a row to the `resources/README.md` registry. Assert **folder == slug**.
- `status` stays **`draft`** until the eval suite passes → then `active` (`docs/07` publish-eligibility; a draft skill is not default-indexed).
- Ensure every MCP gap hit is in `docs/09`, and learning is logged under `docs/learning/logs/`.

---

## Guardrails (always — `docs/08` + `CLAUDE.md` don'ts)

- **Methodology stable, execution swappable** (P1). **Content is downstream of a validated insight** — never render before the gate (P2).
- **Ground or downgrade.** Conservative confidence. Block overclaims: exact `$/MWh`/LMP from a driver alone, plant-level forecasts without a model, national conclusions from one region, causal language where evidence is only directional.
- **One region / one asset class** per test — no unscoped scans.
- **No new MCP tools / agents / orchestrators / DB / `code/` in v0** — log the gap to `docs/09` instead.
- Don't trust tool labels — verify the entity you got is the one you wanted.

**Deliverable**: a complete `resources/<domain>/<slug>/` package — the analog of a finished candidate — grounded, manually tested (transcript saved + resolved), registered, and gap-logged. When in doubt, diff your package against `resources/weather_and_climate/el_nino_enso/`.
