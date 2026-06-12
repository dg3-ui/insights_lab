# Resources — Methodology Registry

> **Status**: v0 registry, updated 2026-06-12 (shared layers added per `docs/plans/2026-06-11_layered_reference_v1.md`).
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

```text
resources/
├── README.md                  # this registry
├── _principles/               # shared layer: rubric · voice · altitude (loads at draft + render)
├── _style/                    # shared layer: brand kit · output contracts (loads at render, post-gate)
├── _craft/                    # shared layer: analytic plot generation (loads at render, post-gate)
├── _reference/                # shared layer: exemplar corpus (form, not facts) — feeds rendering + eval, NOT grounding
└── weather_and_climate/       # domain (driver-grouped)
    └── el_nino_enso/          # package = METHOD ONLY: resource.md/.yml/prompt_projection.md/examples/test_runs
```

**The underscore rule.** A leading-underscore folder is a **shared cross-cutting layer, not a package**: no `resource.yml`, no slug, exempt from `folder == slug`, excluded from any publish scan / discovery index (`docs/07` §3), and registered in the Shared Layers table below — not in the resource Registry. Shared layers sort above the domain folders and are **composed at session time** (the same doctrine as persona views: a view, not a storage axis). Packages carry ONLY the method — voice, rubric, brand, output contracts, plot craft, and exemplars are never restated inside a package.

## Shared Layers

| Layer | Role | Feeds | Stage | Status |
|---|---|---|---|---|
| [`_principles/`](_principles/) | judging rubric · voice · altitude · anti-microprompting · show-don't-flaunt | the checkpoint's scoring · every drafting session | draft + render | ✅ v0.2 |
| [`_style/`](_style/) | brand kit (Inter-primary) · output contracts (direction × audience × format) · artifact skeleton | rendering only | post-gate | ✅ v0.2 |
| [`_craft/`](_craft/) | analytic plot generation — selection by question · blocked plots · grounded-plot rules · spatial fallback | rendering only | post-gate | ✅ v0.2 |
| [`_reference/`](_reference/) | exemplar corpus — form, not facts | rendering + eval, **never** grounding | post-gate | README only; populates in plan Phase 4 |

Quarantine: shared-layer material **never grounds a claim** — it is never a valid `source_ref` (`docs/04`). `_principles` is the only layer loaded before the gate.

## Planned Domains

Materialize a **domain** folder when its **first** resource lands — not before (keep `resources/` from becoming a flat pile). Shared `_` layers follow the same discipline against their own ladder: each materializes when its phase in the active plan lands.

| Domain | External driver | Shared machinery | Example resources |
|---|---|---|---|
| `weather_and_climate` ✅ | climate regimes + weather | NOAA CPC / ONI, irradiance, region crosswalk | el_nino_enso · (drought · heat_wave · wind_drought) |
| `hazard` | physical peril | FEMA / USGS, damage logic, footprint | wildfire_exposure · hurricane_wind · flood |
| `market` | grid / market structure | LMP nodes, curtailment, congestion | curtailment_exposure · congestion |
| `policy` | regulatory / policy change | dockets, permitting, IRA | permitting_delay · interconnection_rule |
| `commercial` | counterparty / contract | FERC EQR, ownership, PPA | offtaker_concentration |

Persona views (e.g. a "climate scientist" agent) are **composed at runtime** by loading a domain's resources + their tags — persona is a view, not a storage axis.

## Registry

| Resource | Domain | Family (docs/02) | Actors | Status |
|---|---|---|---|---|
| [el_nino_enso](weather_and_climate/el_nino_enso/) | `weather_and_climate` | Exposure | owner · investor · lender · offtaker | manual test 001 PASS · status `draft` (not default-indexed until eval-gated → `active`, see `docs/07`) |

## Tag Vocabulary

```text
domain  (folder):   weather_and_climate · hazard · market · policy · commercial
family  (docs/02):  exposure · performance · commercial · development_risk ·
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
3. Meet the contract in docs/03_methodology_resource_standard.md.
4. Fill resource.yml.taxonomy and add a row to the Registry above.
5. Run docs/05_mcp_test_protocol.md; log gaps (tool gaps → the MCP roadmap).
```

See `docs/02_analysis_catalog.md` for family definitions and `docs/learning/` for onboarding.
