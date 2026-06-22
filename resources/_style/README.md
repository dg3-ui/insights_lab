# _style — How It Looks & Ships

> **Status**: v0.2, 2026-06-12 (v0.1 Phase 2 · v0.2: public-vs-internal confidence display, honest-caveat box, moat language banned from copy, DOCX delivery notes, skeleton slots aligned — California-build feedback intake).
>
> **Role**: the shared **rendering layer** — the brand kit and the typed output contracts. Cross-cutting: every phenomenon package renders through this layer; none restates it.
>
> **Stage placement**: loads at **RENDER only, post-gate** (`../../docs/method/data_map.md` Activation Boundary). The one pre-gate touch: the session *names* its output type (blog/report/email) at test start — naming, not loading.
>
> **Not a package**: no `resource.yml`, no slug, excluded from discovery (`resources/README.md`, the underscore rule).

## Contents

| File | What it owns |
|---|---|
| [`brand.md`](brand.md) | Type (Inter-primary), palette (OKLCH + hex), logo usage, the document anatomy (header · figure-with-caption-below · caveat box · footer) |
| [`output_contracts.md`](output_contracts.md) | The three-output model (blog/report/email) — envelopes, gate guards, the public-vs-internal confidence display; direction/audience are meta-tags |
| [`brand_assets/`](brand_assets/) | `lockup-on-light/dark.svg` · `icon.svg` (vendored from the web app) · `artifact_skeleton.html` (the canonical HTML shell) |
| [`examples/`](examples/) | Render exemplars — validated insights rendered through a cell (form demonstrations, not new claims) |

## The One Rule

**A rendering is a projection of a validated insight — never a source of truth, never produced before the gate** (`../../docs/principles.md` P2). This layer changes how an insight *looks*; it may never change what it *claims*. Brand material never grounds a claim (FORM job, `../../docs/method/data_map.md`).

## Versioning

Version in the Status line; bumped on any envelope/brand change. Test runs record the composed version; a bump is a staleness signal for resources validated against the old one (`../../docs/method/resource_standard.md`). The web app is the brand source of truth — re-sync `brand.md` when the site theme changes.

---

**See also**: `../README.md` (Shared Layers table), `../_principles/` (the voice the renderings carry; the rubric that scores them), `../../docs/architecture.md` Layer 3 (the content engine this implements), `../../docs/status/mcp_gaps.md` R6/R7 (the serving roadmap).
