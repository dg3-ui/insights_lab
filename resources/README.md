# Resources — Methodology Registry

> **Status**: v0 registry, 2026-06-05.
>
> **Purpose**: index every methodology resource by **domain · family · actor**, and define how new resources are placed. This is the `resources/` analog of the Learning vault's `_tag_taxonomy.md` + Maps of Content.

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
└── weather_and_climate/       # domain (driver-grouped)
    └── el_nino_enso/          # self-contained package: resource.md/.yml/prompt_projection.md/examples/test_runs
```

## Planned Domains

Materialize a domain folder when its **first** resource lands — not before (keep `resources/` from becoming a flat pile).

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

```text
1. Pick the domain (driver). Reuse an existing folder; create one only for a genuinely new driver.
2. Copy templates/ into resources/<domain>/<slug>/.
3. Meet the contract in docs/03_methodology_resource_standard.md.
4. Fill resource.yml.taxonomy and add a row to the Registry above.
5. Run docs/05_mcp_test_protocol.md; log gaps (tool gaps → the MCP roadmap).
```

See `docs/02_analysis_catalog.md` for family definitions and `docs/learning/` for onboarding.
