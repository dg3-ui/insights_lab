# Resources — Methodology Registry

> **Status**: v0 registry, updated 2026-06-15 — **5 resources across 3 live domains** (weather_and_climate · hazard · commercial); the Registry table below is current. (Shared layers added 2026-06-12 per `docs/plans/2026-06-11_layered_reference_v1.md`; the 4 hazard/commercial/weather resources per `docs/plans/2026-06-13_knowledge_base_expansion_v1.md`.)
>
> **Purpose**: index every methodology resource by **domain · family · actor**, define how new resources are placed, and define the **shared layers** (underscore folders) every resource composes with. This is the `resources/` analog of the Learning vault's `_tag_taxonomy.md` + Maps of Content.

## Organizing Model

Two axes, one folder path:

```text
FOLDER PATH                     = domain   ← the one axis resources SHARE machinery on
                                            (external sources, region crosswalks, caveats)
TAGS (resource.yml.taxonomy)    = family · drivers · actors
                                            ← every other axis a resource is findable by
```

A resource lives in exactly one **domain** folder and is *tagged* with its family/actors, so it is reachable along several axes without being duplicated. Same discipline as the knowledge base: a domain-first tree with a faceted tag layer on top. We group folders by **driver** (not by analysis family, not by analyst persona) because the driver is what neighboring resources actually reuse — NOAA sources, region resolution, mechanism caveats.

**Grain — what counts as ONE resource** (`../docs/plans/2026-06-13_knowledge_base_expansion_v1.md` D6): a resource is the **(driver × physical-mechanism) cell**. The *folder* stays driver-grouped (shared retrieval machinery), but the *resource identity* is the **mechanism** — because the mechanism is what drives `blocked_claims` + `confidence_rules` (the moat). **Asset-class and actor are facets, not forks**; a resource splits **only when the physical mechanism genuinely differs** — and for `hazard` that fires **by default** (hail×solar-panel ≠ hail×gas-turbine ≠ wildfire×transmission-ignition). This keeps the catalog at *dozens, not hundreds*: cross-resource jobs (Screen / Evaluate / Mitigate · top-down / bottom-up) compose resources in a **recipe** (`../docs/method/workflow_recipes.md`), they do not fork the catalog.

```text
resources/
├── README.md                  # this registry
├── templates/                 # package skeleton (/new-resource copies these) — NOT a package, not indexed
├── _principles/               # shared layer: rubric · voice · altitude (loads at draft + render)
├── _style/                    # shared layer: brand kit · output contracts (loads at render, post-gate)
├── _craft/                    # shared layer: analytic plot generation (loads at render, post-gate)
├── _reference/                # shared layer: exemplar corpus (form, not facts) — feeds rendering + eval, NOT grounding
├── _method/                   # shared layer: reusable analytic + finance/insurance/math primitives (pre-gate; NEVER grounds)
├── weather_and_climate/       # domain (driver-grouped)
│   ├── el_nino_enso/          # package = METHOD ONLY: resource.md/.yml/prompt_projection.md/examples/test_runs
│   └── extreme_heat_derate/   # heat × solar thermal derate
├── hazard/                    # domain (driver-grouped)
│   ├── hail_solar/            # the flagship (hail × solar PV)
│   └── hurricane_high_wind_wind/
└── commercial/                # domain (driver-grouped)
    └── offtaker_concentration/
```

**The underscore rule.** A leading-underscore folder is a **shared cross-cutting layer, not a package**: no `resource.yml`, no slug, exempt from `folder == slug`, excluded from any publish scan / discovery index (`../docs/method/discovery_spec.md` §3), and registered in the Shared Layers table below — not in the resource Registry. Shared layers sort above the domain folders and are **composed at session time** (the same doctrine as persona views: a view, not a storage axis). Packages carry ONLY the method — voice, rubric, brand, output contracts, plot craft, and exemplars are never restated inside a package.

## Shared Layers

| Layer | Role | Feeds | Stage | Status |
|---|---|---|---|---|
| [`_principles/`](_principles/) | judging rubric · voice · altitude · anti-microprompting · show-don't-flaunt | the checkpoint's scoring · every drafting session | draft + render | ✅ v0.2 |
| [`_style/`](_style/) | brand kit (Inter-primary) · output contracts (blog/report/email) · artifact skeleton | rendering only | post-gate | ✅ v0.2 |
| [`_craft/`](_craft/) | analytic plot generation — selection by question · blocked plots · grounded-plot rules · spatial fallback | rendering only | post-gate | ✅ v0.2 |
| [`_reference/`](_reference/) | exemplar corpus — form, not facts | rendering + eval, **never** grounding | post-gate | README only; populates in plan Phase 4 |
| [`_method/`](_method/) | reusable analytic primitives (screen·rank·segment·score) + finance/insurance/math method (damage funcs · DSCR · EVT) | recipes **call** them; resources **cite** the reasoning skeleton | draft (pre-gate) | ✅ v0 seed |

Quarantine: shared-layer material **never grounds a claim** — it is never a valid `source_ref` (`../docs/method/data_map.md`). `_principles` and `_method` load **before** the gate (they guide voice + reasoning); `_style` · `_craft` · `_reference` load **post-gate** (rendering). None ever grounds a claim.

**Two resource classes** (`_method/README.md`, plan D7): (1) **driver-keyed packages** in the domain tree that *ground* claims; (2) **non-driver `_method` primitives** (damage functions · DSCR · EVT · insurance/materiality) that recipes *call* for the vertical hazard→…→$ legs but that *never* ground. The discovery index (`../docs/method/discovery_spec.md`) sees only class (1).

## Planned Domains

Materialize a **domain** folder when its **first** resource lands — not before (keep `resources/` from becoming a flat pile). Shared `_` layers follow the same discipline against their own ladder: each materializes when its phase in the active plan lands.

> **Settled (KB-expansion plan, 2026-06-14)**: (1) **No `finance` domain** — the five domains below stand; finance / insurance / math methodology (DSCR/CFADS, EVT, copulas, parametric/basis-risk, damage functions) lives in the cross-cutting **`_method/`** shared layer (added in that plan's Phase 1), never a domain. (2) **Grain = the `(driver × mechanism)` cell** — folders stay driver-grouped (shared retrieval machinery), but *what counts as one resource* is the physical-mechanism cell (mechanism drives `blocked_claims`/`confidence_rules`, the moat); asset-class & actor are **facets**, and a split fires whenever the mechanism differs — for `hazard` that is **by default** (hail×solar ≠ hail×gas ≠ wildfire×transmission). The Organizing-Model wording is updated in that plan's Phase 2.

| Domain | External driver | Shared machinery | Example resources |
|---|---|---|---|
| `weather_and_climate` ✅ | climate regimes + weather | NOAA CPC / ONI, irradiance, region crosswalk | el_nino_enso ✅ · **extreme_heat_derate** ✅ · (drought · wind_drought) |
| `hazard` ✅ | physical peril | SPC / NHC / FEMA / USGS, hazards news, footprint | **hail_solar** ✅ · **hurricane_high_wind_wind** ✅ · (wildfire×transmission · flood) |
| `market` | grid / market structure | LMP nodes, curtailment, congestion | curtailment_exposure · congestion |
| `policy` | regulatory / policy change | dockets, permitting, IRA | permitting_delay · interconnection_rule |
| `commercial` ✅ | counterparty / contract | FERC EQR, ownership, resolved-buyer facts | **offtaker_concentration** ✅ |

Persona views (e.g. a "climate scientist" agent) are **composed at runtime** by loading a domain's resources + their tags — persona is a view, not a storage axis.

## Registry

| Resource | Domain | Family (../docs/method/analysis_families.md) | Actors | Status |
|---|---|---|---|---|
| [el_nino_enso](weather_and_climate/el_nino_enso/) | `weather_and_climate` | Exposure | owner · investor · lender · offtaker | manual test 001 PASS · status `draft` (not default-indexed until eval-gated → `active`, see `../docs/method/discovery_spec.md`) |
| [hail_solar](hazard/hail_solar/) | `hazard` | Exposure (+ Event-Translation) | owner · investor · lender · developer | manual test 001 PASS · status `draft` · grounding `substrate-only` (the $ / EAL layer is model-gpr — `../docs/status/mcp_gaps.md` R12) |
| [hurricane_high_wind_wind](hazard/hurricane_high_wind_wind/) | `hazard` | Exposure (+ Event-Translation) | owner · investor · lender · developer | manual test 001 PASS (directional) · status `draft` · grounding `model-not-wired` (no separable wind-damage signal in substrate; the $ / TC-model layer is model-gpr — `../docs/status/mcp_gaps.md` R12) |
| [extreme_heat_derate](weather_and_climate/extreme_heat_derate/) | `weather_and_climate` | Exposure | owner · investor · lender · offtaker | manual test 001 PASS · status `draft` · grounding `substrate-only` (the quantified %/MWh de-rate + $ layer is model-gpr — `../docs/status/mcp_gaps.md` R12) |
| [offtaker_concentration](commercial/offtaker_concentration/) | `commercial` | Commercial | owner · investor · lender | manual test 001 PASS · status `draft` · grounding `substrate-only` (the re-contracting/merchant $ + counterparty-credit layer is model-gpr) · first FACTUAL (non-directional) resource |

## Tag Vocabulary

```text
domain  (folder):   weather_and_climate · hazard · market · policy · commercial
family  (../docs/method/analysis_families.md):  exposure · performance · commercial · development_risk ·
                    portfolio_strategy · market_context · event_translation
actors:             owner_operator · investor · lender · offtaker · developer
drivers:            free-form leaf tags — enso, irradiance, wildfire, congestion, …
```

Declared per resource in `resource.yml`:

```yaml
taxonomy:
  domain: weather_and_climate
  family: exposure
  drivers: [enso, irradiance]
  actors:  [owner_operator, investor, lender, offtaker]
```

## Adding A Resource

**Fast path:** run `/new-resource <topic>` (`.claude/commands/new-resource.md`) — the guided, generalized ENSO-creation process. The steps below are what it automates; foundational knowledge for the mechanism layer (`knowledge.md`) comes from the `.learning/` shared vault (symlink → `~/Desktop/Learning`).

```text
1. Pick the domain (driver). Reuse an existing folder; create one only for a genuinely new driver.
2. Copy templates/ into resources/<domain>/<slug>/.
3. Meet the contract in ../docs/method/resource_standard.md.
4. Fill resource.yml.taxonomy and add a row to the Registry above.
5. Run ../docs/process/test_protocol.md; log gaps (tool gaps → the MCP roadmap).
```

See `../docs/method/analysis_families.md` for family definitions and `docs/learning/` for onboarding.
