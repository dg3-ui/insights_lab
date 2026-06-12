# _craft — How Analytics Are Drawn

> **Status**: v0.2, 2026-06-12 (v0.1 Phase 3 · v0.2 adds §6 statebin spatial fallback + the chart-scope-follows-direction rule — California-build feedback intake).
>
> **Role**: the shared **analytic-plot layer** — chart selection by question, the blocked-plot gates, and the craft defaults. Cross-cutting: every rendering that carries a figure draws it through this layer.
>
> **Stage placement**: loads at **RENDER only, post-gate** (`docs/04` Activation Boundary). A chart is a set of claims; claims are gated before they are drawn.
>
> **Not a package**: no `resource.yml`, no slug (`resources/README.md`, the underscore rule).

## Contents

| File | What it owns |
|---|---|
| [`plot_generation.md`](plot_generation.md) | Question → chart-family selection (keyed to `docs/02` families) · the uncertainty gate (model-backed only) · blocked plots · perception + brand defaults · the spec-first runtime |

## The One Rule

**A plot is a set of claims**: every plotted series carries its own `source_ref` + `as_of`; every figure is bordered with its caption below (what it shows · source · `as_of`); no chart says more than the gated insight it renders. Brand values are cited from `../_style/brand.md`, never copied.

## Versioning

Version in the Status line; test runs record the composed version; a bump is a staleness signal for dependents (`docs/03`). The knowledge source (the Learning-vault visualization guide) may grow independently — this layer re-syncs deliberately, not automatically.

---

**See also**: `../README.md` (Shared Layers table), `../_style/brand.md` (palette + figure anatomy), `../_principles/rubric.md` (criterion 4 binds charts too), `../../docs/09_mcp_roadmap.md` R7 (the render-tool roadmap charts ride on).
