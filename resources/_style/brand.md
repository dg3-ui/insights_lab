# Brand — How An InfraSure Document Looks

> **Status**: v0.2, 2026-06-14 — **restructured so the brand is format-agnostic**: design **INTENT** (Part A, binds) is separated from per-format **DELIVERY** (Part B, swappable), so the same brand renders to DOCX, HTML, or a future format without forcing any one of them (P1 applied to brand; P6 framing). Was v0.1, 2026-06-12 (Inter-primary, owner decision).
>
> **Provenance**: vendored from the live infrasure.ai web app — `renewablesinfo_org/web/src/app/globals.css` (OKLCH tokens), `layout.tsx` (font loading), `src/lib/brand.ts` + `fuel-colors.ts`, pulled 2026-06-11. **The web app remains the source of truth**; this file is the projection rendered documents use. Re-sync when the site theme changes (a version bump here = staleness signal, `../../docs/method/resource_standard.md`).
>
> **Scope**: rendered outputs only; loads **post-gate** (`../../docs/method/data_map.md` Activation Boundary). Brand never grounds, frames, or routes a claim (FORM job — §C).

## How to read this file (intent vs delivery — matters, because this composes into the prompt)

```text
PART A · THE DESIGN LANGUAGE    the brand INTENT — format-agnostic, and it BINDS (stay on-brand):
                                type roles · palette · the document's bones · accent discipline
PART B · DELIVERY (per format)  HOW to render the intent for a target — SWAPPABLE notes (HTML · DOCX · …);
                                the format mechanics (CSS values, Word styles) live HERE, never in Part A
```

**The brand is Part A.** Render it appropriately for whatever format you're asked for — **adapt the *expression*, keep the *intent*** (P1: stable design language / swappable format · P6: the intent guides, you render it well; no format is forced). A prompt that carries this file should read "here is the design language; render it for [DOCX / HTML / …]," never "emit HTML with these exact CSS values."

## PART A · The Design Language  (format-agnostic · binds)

### A1 · Type — Inter-led

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

(The **font files + fallback stack** differ by format — see Part B. The intent is: Inter for prose, JetBrains Mono for data, hierarchy by weight/size.)

### A2 · Palette (OKLCH canonical · hex fallback)

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

**Chart / fuel colors** (per-series; every series still needs its `source_ref` — `../../docs/method/data_map.md`):

```text
fuel:   solar #efa30f · wind #00a7dd · hydro #00bec7 · bess #00bc7b ·
        nuclear #886de9 · gas #6b727e · coal #5b5449
charts: 1 #f54900 · 2 #009689 · 3 #104e64 · 4 #ffb900 · 5 #fe9a00   (light-mode slots)
```

### A3 · Logo

Assets in [`brand_assets/`](brand_assets/): `lockup-on-light.svg` · `lockup-on-dark.svg` (full wordmark lockups) · `icon.svg` (the mark alone — amber ring · green bolt · slate grid).

- Never recolor, stretch, or put the mark on a busy background; clear space ≥ the mark's ring width.
- **Entity deep-links** (the product-demo move, `_reference/exemplars/grid_status_rabbit_hill.md` lesson 4): entity mentions and figures link to their infrasure.ai pages where they exist. The canonical URL route is **not yet documented here** — confirm against the web app (`renewablesinfo_org/web/src/app/`) before shipping links; until then link the domain, never a guessed path.

(How the logo is *embedded* — inline SVG vs rasterized PNG vs running-header — differs by format; see Part B.)

### A4 · Document Anatomy — the bones (the "proper format")

Every rendered document carries these bones — **header and footer are not optional**:

```text
┌ HEADER ──────────────────────────────────────────────────────────────┐
│ [icon + InfraSure Insights]              [KICKER: reader topic]     │  ← rule below
├ TITLE BLOCK ─────────────────────────────────────────────────────────┤
│ Title (Inter 600) · dek (muted) · meta line (date · scope · as_of    │
│ register — JetBrains Mono)                                           │
├ SUMMARY BOX (blog/report) ───────────────────────────────────────────┤
│ muted fill · lifted box · 3–4 terse takeaways · calibration cue      │
├ BODY ────────────────────────────────────────────────────────────────┤
│ sections per the output contract; entity tables; callouts            │
│ ┌ FIGURE ────────────────────────────┐                               │
│ │ chart / image                      │ ← bordered, lifted box        │
│ │────────────────────────────────────│                               │
│ │ caption BELOW: what it shows ·     │ ← muted · source + as_of      │
│ │ source · as_of                     │   are MANDATORY               │
│ └────────────────────────────────────┘                               │
├ CAVEAT BOX ──────────────────────────────────────────────────────────┤
│ amber left-border · the honest caveat: what is still resolving /     │
│ what would change the read (confident, never a "what we are NOT      │
│ saying" negation list)                                               │
└ FOOTER ──────────────────────────────────────────────────────────────┘
  rule above · sources + as_of register · calibrated descriptor ·
  "InfraSure Insights · infrasure.ai" · generated date
```

Intent rules (format-agnostic): **every figure is bordered with its caption below it** (description under the image — never above, never floating); the caption names source + `as_of`; boxes are **lifted** (rounded corners + a subtle shadow — the exact radius/shadow are a Part-B delivery detail); **generous whitespace** (density lives in tables, not cramped text). **Confidence (public):** the summary's calibration cue and the footer's descriptor state the *posture* ("a forward, directional read"), never a pejorative "LOW" badge; the caveat box carries a real caveat, not a disclaimer (`output_contracts.md` §3, public-vs-internal). **Kicker:** reader-facing topic ("ENSO" · "California Solar"), never the internal bucket name.

## PART B · Delivery  (per format · swappable · render Part A for the target)

### B1 · HTML artifact

- **Fonts**: Google Fonts link — `Inter:opsz,wght@14..32,400..700` + `JetBrains Mono:wght@400;500`. **Degradation stack (mandatory)**: `Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif` and `"JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, Consolas, monospace` — if a sandbox blocks the font fetch, degrade to the system grotesque, **never** to a serif (R7 ledger detail).
- **Boxes**: `radius 10px` (`--radius: 0.625rem`) + `shadow-sm` wherever a box lifts (the A4 "lifted box" intent, in CSS).
- **Header**: inline `icon.svg` at 28–32px + wordmark text — self-contained (artifacts cannot load local files).
- **Working CSS**: `brand_assets/artifact_skeleton.html` is Part A rendered as HTML/CSS — the canonical B1 artifact.

### B2 · DOCX export

Three fixes the first ENSO render needed (2026-06-12):
1. **Name a guaranteed sans** (Calibri/Carlito or Arial) in the DOCX style defaults — naming "Inter" *alone* makes LibreOffice substitute a **serif**, breaking the house look; the Inter→system fallback must be **explicit** for the DOCX path (not just HTML).
2. Carry the lockup + page number in a real Word **running header/footer**, not an in-body band.
3. **Rasterize** the logo SVG → PNG for embedding (`../_craft/plot_generation.md` §6).

Faces named: the same A1 roles; fidelity depends on recipient-installed fonts (the fallback is embedded in the style definitions). "Lifted boxes" → table-cell shading / borders, since DOCX has no `shadow-sm`.

### B3 · Other formats (PDF · slides · platform card · …)

Not yet needed — **add a delivery note when one first is.** Render the Part-A intent appropriately for the target (PDF ≈ the B1 CSS to print; slides = the type/palette/bones adapted to a deck; a platform card = the bones at card scale). The intent is the constant; the note captures only that format's mechanics. (Roadmap: a served render/export tool — `../../docs/status/mcp_gaps.md` R7.)

## §C · What This File Is / Is Not

- **Not a methodology input**: brand never grounds, frames, or routes a claim (FORM job, `../../docs/method/data_map.md`).
- **What is stable vs adaptable** (the P6 point): the **design language (Part A)** is stable + **versioned** — a change to the type system, palette, or document bones is a version bump here (a staleness signal). But **rendering that intent for a given format (Part B) is expected adaptation, not a deviation to police** — choosing the DOCX vs HTML expression is the model's job. The thing that must not drift is the *design language*; the *format mechanics* are meant to flex per target.

---

**See also**: `output_contracts.md` (which output uses these bones), `brand_assets/artifact_skeleton.html` (Part A as working HTML/CSS — a B1 artifact), `../_principles/voice.md` (the prose these bones carry), `../../docs/status/mcp_gaps.md` R6/R7 (serving brand assets / a render tool — the roadmap), `../README.md` (the underscore rule).
