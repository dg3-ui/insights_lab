# resources/_method — Reusable Analytic Primitives (shared layer; form/method, never grounding)

> **Status**: v0 **seed**, 2026-06-14 (`../../docs/plans/2026-06-13_knowledge_base_expansion_v1.md` Phase 1). A shared underscore layer: the home for cross-cutting **math / finance / insurance** method **and** the factored-out **reasoning primitives** that recipes call. Like every `_`-layer it is **quarantined from grounding** — it is **never** a valid `source_ref`.

## The underscore rule applies (`../README.md`)

`_method/` is a **shared layer, not a package**: no `resource.yml`, no slug, exempt from `folder == slug`, excluded from any publish scan / discovery index (`../../docs/method/discovery_spec.md` §3). It is **composed at session time**. It loads **before the gate** (it guides reasoning) but it **never grounds a claim** — every grounded claim still traces to the substrate + a named external source.

## The two resource classes (D7 — why this layer exists)

```text
(1) DRIVER-KEYED RESOURCES        methodology packages in the domain tree, keyed on (driver × mechanism)
    resources/<domain>/<slug>/    — hail_solar, el_nino_enso, hurricane_high_wind_wind, ...
                                    GROUND claims (substrate + named external feed).

(2) NON-DRIVER _method PRIMITIVES  here. damage functions, insurance/materiality, DSCR/CFADS, EVT.
    resources/_method/             Recipes CALL them for the VERTICAL legs of the hazard→…→$ chain
                                    that have no external driver. They NEVER ground a claim.
```

A recipe (`../../docs/method/workflow_recipes.md`) composes (1) as the parallel fan-out and calls (2) for the vertical/finance legs.

## What lives here

### A · The reasoning skeleton (seeded from `el_nino_enso`)

The generic decomposition every resource's `procedure` specializes — lifted from ENSO's "Required reasoning steps":

```text
1. RESOLVE external state      pull the live driver/event state (NOAA, footprint feed, hazards news) — cite the date
2. STATE mechanism + robustness name the claim type (directional vs factual); rate the mechanism's robustness
3. SCOPE                       one region · one asset class; resolve the asset set via the MCP
4. FILTER / RANK               keep material assets; rank by exposure · materiality · confidence  (screen / score)
5. DRILL                       get_plant the top cases for the grounding fields (CF, owner, offtaker, geometry)
6. ASSEMBLE                    the claim grammar: condition + scope + mechanism + evidence + confidence + caveat + actor
7. CAP                         confidence at the weakest input; block/downgrade beyond the evidence
```

Primitives, by name: **screen** (fan out + filter to material) · **rank** (order by a scored axis) · **segment** (group by geography/owner/vintage) · **score** (exposure · materiality · confidence — conservative, capped).

### B · Non-driver method primitives (STUBS — fill when a resource forces it, `../../docs/principles.md` P5)

| Primitive | Job | Grounding note | Status |
|---|---|---|---|
| `damage_functions` | hazard footprint → **directional** asset vulnerability by mechanism | the $ / EAL is `model-gpr` — directional only on the public MCP | stub |
| `insurance_materiality` | exposure → **directional** insurance / $ relevance (the commercial bridge) | pricing is `model-gpr` — never emit a premium/$ figure | stub |
| `dscr_cfads` | debt-service-coverage mechanics | DSCR is a `model-gpr` field — directional reasoning only | stub |
| `evt_statistics` | extreme-value / tail reasoning + uncertainty scoring | method only; never a stationary return-period from history alone | stub |

Stubs fill only when a resource needs the depth — do not build the math ahead of a resource that uses it.

## What it feeds (and never feeds)

```text
recipes (workflow_recipes.md)  ──CALL──►  _method primitives (esp. class B, the vertical legs)
resources                      ──CITE──►  the reasoning skeleton (A) when specializing their procedure
                               ✗ NEVER    a source_ref — _method grounds nothing (it is form/method, like _reference)
```

---

**See also**: `../README.md` (the underscore rule + the Shared Layers table + the two-class note) · `../../docs/method/workflow_recipes.md` (the recipes that call these primitives) · `../../docs/method/resource_standard.md` (the contract a driver-keyed resource's `procedure` meets) · `../../docs/method/data_map.md` (the `grounds / frames / routes` discipline this layer is quarantined from).
