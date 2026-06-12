# Brand — How An InfraSure Document Looks

> **Status**: v0.1, 2026-06-12 (Phase 2 deliverable; D3 of the active plan, font set refined by owner decision 2026-06-12 — **Inter-primary**).
>
> **Provenance**: vendored from the live infrasure.ai web app — `renewablesinfo_org/web/src/app/globals.css` (OKLCH tokens), `layout.tsx` (font loading), `src/lib/brand.ts` + `fuel-colors.ts`, pulled 2026-06-11. **The web app remains the source of truth**; this file is the projection rendered documents use. Re-sync when the site theme changes (a version bump here = staleness signal, `docs/03`).
>
> **Scope**: rendered outputs only (HTML artifacts, DOCX exports). Loads **post-gate** (`docs/04` Activation Boundary).

## §1 · Type — Inter-led

**Owner decision (2026-06-12): the primary family for insight documents is `Inter` — one family, varied within.** Hierarchy comes from weight, size, and optical sizing, not from switching families. (`Fraunces`, the site's display serif, stays a **marketing-site** face — not used in insight documents.)

| Role | Face | Spec |
|---|---|---|
| Title | Inter | 600 · 28–34px · `letter-spacing -0.02em` · `opsz` 32 |
| Section heading | Inter | 600 · 18–20px · `-0.01em` |
| Body | Inter | 400 (450 for emphasis-weight body) · 15–16px · line-height 1.6 |
| Dek / standfirst | Inter | 400 · 18px · muted color |
| Caption · meta · footer | Inter | 400 · 12.5–13px · muted color |
| Label / kicker | Inter | 500 · 11px · UPPERCASE · `+0.08em` tracking |
| Data: IDs · `as_of` · code · table numerics | JetBrains Mono | 400–500 · 12.5–13px |

**Delivery (HTML artifact)**: Google Fonts link — `Inter:opsz,wght@14..32,400..700` + `JetBrains Mono:wght@400;500`. **Degradation stack (mandatory in every rendering)**: `Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif` and `"JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace` — if a sandbox blocks the font fetch, the document degrades to the system grotesque, never to a serif default. (Artifact-sandbox font limits are an R7 ledger detail, not a prompt workaround.) **DOCX export**: same faces named; fidelity depends on recipient-installed fonts — the fallback stack is embedded in the style definitions.

## §2 · Palette (OKLCH canonical, hex fallback)

| Token | Light | Dark | Hex (light) | Use |
|---|---|---|---|---|
| `--fg` | `oklch(0.145 0 0)` | `oklch(0.985 0 0)` | `#0a0a0a` | text |
| `--bg` | `oklch(1 0 0)` | `oklch(0.145 0 0)` | `#ffffff` | page |
| `--muted-fg` | `oklch(0.556 0 0)` | `oklch(0.708 0 0)` | `#737373` | deks, captions, meta |
| `--muted-bg` | `oklch(0.97 0 0)` | `oklch(0.205 0 0)` | `#f5f5f5` | summary/callout fills |
| `--border` | `oklch(0.922 0 0)` | `oklch(1 0 0 / 10%)` | `#e5e5e5` | rules, boxes, figures |
| `--brand-green` | `oklch(0.72 0.18 155)` | `oklch(0.74 0.18 155)` | `#00c470` | accents, links, the kicker |
| `--brand-amber` | `oklch(0.78 0.15 75)` | `oklch(0.80 0.15 75)` | `#efa831` | secondary accent, watch-items |

Accent discipline: **green and amber are accents, not paint** — kickers, links, callout left-borders, chart series. Body stays near-black on white (or the inverse). Never set body text in brand colors.

**Chart / fuel colors** (per-series; every series still needs its `source_ref` — `docs/04`):

```text
fuel:   solar #efa30f · wind #00a7dd · hydro #00bec7 · bess #00bc7b ·
        nuclear #886de9 · gas #6b727e · coal #5b5449
charts: 1 #f54900 · 2 #009689 · 3 #104e64 · 4 #ffb900 · 5 #fe9a00   (light-mode slots)
```

## §3 · Logo

Assets in [`brand_assets/`](brand_assets/): `lockup-on-light.svg` · `lockup-on-dark.svg` (full wordmark lockups — DOCX headers, covers) · `icon.svg` (the mark alone — amber ring · green bolt · slate grid).

- **HTML artifact header**: inline `icon.svg` at 28–32px + wordmark text — "InfraSure" Inter 600 + "Insights" Inter 400 muted (self-contained; artifacts cannot load local files).
- Never recolor, stretch, or put the mark on a busy background; clear space ≥ the mark's ring width.
- **Entity deep-links** (the product-demo move, `_reference/exemplars/grid_status_rabbit_hill.md` lesson 4): entity mentions and figures link to their infrasure.ai pages where they exist. The canonical URL route is **not yet documented here** — confirm against the web app (`renewablesinfo_org/web/src/app/`) before shipping links; until then link the domain, never a guessed path.

## §4 · Document Anatomy (the "proper format")

Every rendered document carries these bones — header and footer are **not optional**:

```text
┌ HEADER ──────────────────────────────────────────────────────────────┐
│ [icon + InfraSure Insights]              [KICKER: reader topic]     │  ← 1px border-bottom
├ TITLE BLOCK ─────────────────────────────────────────────────────────┤
│ Title (Inter 600) · dek (muted) · meta line (date · scope · as_of    │
│ register — JetBrains Mono)                                           │
├ SUMMARY BOX (blog/brief) ────────────────────────────────────────────┤
│ muted fill · radius 10px · 3–4 terse takeaways · calibration cue     │
├ BODY ────────────────────────────────────────────────────────────────┤
│ sections per the output contract; entity tables; callouts            │
│ ┌ FIGURE ────────────────────────────┐                               │
│ │ chart / image                      │ ← 1px --border · radius 10px  │
│ │────────────────────────────────────│                               │
│ │ caption BELOW: what it shows ·     │ ← 12.5px muted · source +     │
│ │ source · as_of                     │   as_of are MANDATORY         │
│ └────────────────────────────────────┘                               │
├ CAVEAT BOX ──────────────────────────────────────────────────────────┤
│ amber left-border · the honest caveat: what is still resolving /     │
│ what would change the read (confident, never a "what we are NOT      │
│ saying" negation list)                                               │
└ FOOTER ──────────────────────────────────────────────────────────────┘
  1px border-top · sources + as_of register · calibrated descriptor ·
  "InfraSure Insights · infrasure.ai" · generated date
```

Rules: **every figure is bordered with its caption below it** (description under the image — never above, never floating); the caption names source + `as_of`; radius 10px (`--radius: 0.625rem`) and `shadow-sm` everywhere a box lifts; generous whitespace (24px section gaps) — density lives in tables, not in cramped text. **Confidence (public):** the summary's calibration cue and the footer's calibrated descriptor state the *posture* ("a forward, directional read"), never a pejorative "LOW" badge; the caveat box carries a real caveat, not a disclaimer of what we won't say (`output_contracts.md` §3, the public-vs-internal note). **Kicker:** reader-facing topic ("ENSO" · "California Solar"), never the internal bucket name.

**DOCX delivery (build note, 2026-06-12).** Three things the first ENSO render got wrong and fixed: (1) **name a guaranteed sans** (Calibri/Carlito or Arial) in the DOCX style defaults — naming "Inter" *alone* makes LibreOffice substitute a **serif**, which breaks the house look; the Inter→system fallback must be explicit for the DOCX path, not just HTML. (2) Carry the lockup + page number in a real Word **running header/footer**, not an in-body band (the reference-doc pattern). (3) Rasterize the logo SVG → PNG for embedding (`../_craft/plot_generation.md` §6).

## §5 · What This File Is Not

Not a methodology input: brand never grounds, frames, or routes a claim (FORM job, `docs/04`). Not a per-document override surface: a rendering that needs to deviate is a contract-cell change (version-bumped), not an inline exception.

---

**See also**: `output_contracts.md` (which cell uses which anatomy), `brand_assets/artifact_skeleton.html` (this file as working CSS), `../_principles/voice.md` (the prose these bones carry), `../../docs/09_mcp_roadmap.md` R6/R7 (serving brand assets / a render tool — the roadmap), `../README.md` (the underscore rule).
