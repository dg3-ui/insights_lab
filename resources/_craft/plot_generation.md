# Plot Generation — Analytics That Obey the Claim Grammar

> **Status**: v0.1, 2026-06-12 (Phase 3 deliverable of the active plan).
>
> **Purpose**: the operational skill for producing analytical charts in InfraSure renderings — what chart answers what question, what may never be plotted, and the craft defaults that make a chart read in seconds.
>
> **Knowledge companion**: the full theory (perception science, color, the agentic pipeline) lives in the Learning vault — `.learning/Data Analytics/data_visualization/data_visualization_complete_guide.md`. This file is its terse, gated projection; cite the vault, don't restate it.
>
> **Scope**: loads at **RENDER only, post-gate** (`../../docs/method/data_map.md`). Brand values come from `../_style/brand.md` §2 — cite, never copy.

## §0 · The One Rule

**A plot is a set of claims.** Every plotted series obeys the claim grammar exactly as prose does:

```text
per series:   a source_ref (substrate | external) + as_of        — no ref, no plot
per figure:   bordered · caption BELOW · caption names what it shows + source + as_of
                                                                   (brand.md §A4, mandatory)
per chart:    says NOTHING the gated insight does not say — a chart that implies a
              forecast, a magnitude, or a causal link the insight blocked is itself blocked
```

The figure caption is the chart's citation line. A reader must be able to audit any plotted number back to a tool result or a dated external source, same as any claim (`../../docs/method/resource_standard.md`, `../../docs/method/data_map.md`).

## §1 · Selection — Question First, Never Chart First

The most damaging mistake is starting with the chart type (vault §12 #1). Classify the question, then pick from the family. Mapped to the analysis families (`../../docs/method/analysis_families.md`):

| The question sounds like | Chart family | First picks | Claim type (what's blocked) |
|---|---|---|---|
| "how do these compare / rank?" | Comparison · Ranking | sorted bar (desc) · lollipop · dumbbell (two periods) | observed values only; never invented rankings |
| "how did X change?" (Exposure baseline, Performance) | Trend | line · multi-line ≤5 series · seasonal paired bar | observed history only; **no extrapolated tail** on the line |
| "what's the seasonal shape?" (Exposure) | Trend/seasonal | monthly CF line · summer-vs-winter paired bar | the baseline a driver perturbs — never the perturbed forecast |
| "how spread / concentrated?" (Portfolio Strategy) | Distribution | histogram · box by group · concentration bar | distribution of *substrate* values; no synthetic spreads |
| "is X related to Y?" (Market Context) | Relationship | scatter (≤2 encodings + label) | correlation shown ≠ causation claimed — caption must match the insight's caveat |
| "what's the mix / share?" (Portfolio) | Composition | stacked bar ≤4 cats · treemap for many · waffle | shares of a *resolved* total; pie only 2–3 cats with one dominant |
| "where?" (any family) | Spatial | symbol map (magnitude) · choropleth (rate) | **only if geography IS the story** — else a sorted bar is faster (vault §12 #10) |
| "what's the event timeline?" (Event Translation) | Annotated trend | line + dated call-outs · reference lines | each annotation cites its article/`as_of` |
| "what's the range of outcomes?" (any) | Uncertainty | band · fan · exceedance curve | **MODEL-BACKED ONLY** — see §2, the sharpest gate in this file |

## §2 · The Uncertainty Family — Allowed Only With a Model

The vault (§14) rightly calls uncertainty views high-value — *for teams that have forecasting models*. We mostly do not, yet. The gate:

```text
ALLOWED   a band / fan / exceedance chart whose distribution a NAMED MODEL produced,
          with the model as the source_ref and the confidence level labeled on the band
BLOCKED   any forecast band drawn from a driver + intuition: an "ENSO price impact" fan,
          a "winter generation loss" band, a single-point forecast styled as data
```

If the insight's confidence is LOW/directional, the honest chart is the **baseline** (the seasonal CF the driver perturbs) plus a *text* annotation of direction — never a drawn forecast curve. Drawing the curve manufactures precision the gate already refused (`_principles/voice.md` §3).

## §3 · Blocked Plots (mirrors blocked claims)

- **No forecast `$/MWh` / LMP chart from a driver alone** — and no plant-level production-forecast curve without a plant-level model (`../../docs/method/resource_standard.md` blocked claims, the ENSO cap: "Never a number").
- **No chart from `_reference` exemplar data** — exemplars are form, never data (`../../docs/method/data_map.md` quarantine).
- **No undated series** — a series whose `as_of` is unknown does not render.
- **No truncated bar baselines** (bars start at zero), **no dual y-axes** (use small multiples; if unavoidable, disclose the scaling in the caption), **no 3D**, **no pie beyond 3 categories**, **no rainbow ramps on sequential data**, **no area/bubble size as the primary magnitude encoding** (vault §7, §12).
- **No extrapolated line tails** — observed history ends where the data ends; the future is text, not ink.

## §4 · Craft Defaults (perception + brand)

- **Chart scope follows the piece's direction** (owner feedback, 2026-06-12): a **top-down** piece leads with fleet/region-scope figures (capacity, counts, owner concentration via `aggregate`) — never a single-plant chart presented as the fleet read. Where the tool surface can't produce the fleet series yet (seasonal-CF rollup: R2 · county: R8), a single-plant series may appear only as a **labeled exemplar inset** ("one plant's baseline, exemplifying the pattern"), and the gap stays logged. **Bottom-up** pieces are single-asset by nature.
- **Position and length carry the message** — they decode most accurately (vault §2, Cleveland & McGill). Color groups or highlights; it never encodes precise values.
- **≤5 series per chart**; more → small multiples with shared scales.
- **Direct labels at line/bar ends; legends are a last resort.** Sort categorical bars by value.
- **Aspect**: wide (≥2:1) for time series — bank slopes toward ~45°; squarer for distributions.
- **Color** (all values from `_style/brand.md` §2): categorical = the **fuel-type colors** (solar `--color-fuel-solar` etc.); highlight pattern = focus series in brand green, context series in muted gray; sequential = single-hue ramp of brand green; diverging = **blue ↔ amber** around a neutral mid (CVD-safe; avoids red-green). Red is reserved for risk/loss semantics. Never rely on color alone — pair with line style, position, or label.
- **Annotation is storytelling**: name every reference line and threshold ("fleet median", "≥50 MW cut"); date every event call-out.
- **Every figure gets alt text** (chart type · scope · the one takeaway) — accessibility, and it doubles as the caption draft.
- **Declutter by default**: minimal gridlines, no box, no shadow; the data-ink discipline (vault §2) matches the house no-mush rule.

## §5 · Runtime — Spec First, Then Draw

Think in a **chart spec before any drawing** (the vault §10 pipeline, collapsed to one session):

```text
1 QUESTION   the single question this chart answers (if you can't say it, no chart)
2 FAMILY     from §1 — intent, not chart-type preference
3 SERIES     each with: tool call / external source · as_of · units
4 ENCODING   x · y · color · label — position/length first (§4)
5 GATE CHECK §2/§3 — is anything here a blocked plot? does the chart exceed the insight?
6 DRAW       HTML artifact → inline SVG in the figure slot of artifact_skeleton.html
             analysis-tool fallback → matplotlib PNG, same palette, embedded
7 CAPTION    below the figure: what it shows · source · as_of  (+ alt text)
```

Pre-ship checklist (the vault §8 list, compressed): units on axes · zero-baseline bars · ≤5 series · sorted categories · consistent colors with every other figure in the document · readable at the rendered size · the title states the takeaway, not the topic.

## §6 · Spatial Fallback — A Map Without Geo Libraries (2026-06-12)

A "where" view often wants a US map, but the sandbox has **no Chrome (kaleido), no geopandas, and (verified 2026-06-15) no matplotlib** either, and the MCP serves no geometry yet (`../../docs/status/mcp_gaps.md` R10). So the **hand-authored inline-SVG path is the reliable one** here (the §5 matplotlib-PNG fallback needs matplotlib installed) — worked end-to-end on the hail statebin map (`../../studio/brookfield_standard_solar/_renders/hail_us_statebin.html`, via `/render`). The self-contained technique:

```text
STATEBIN TILE-GRID   each state = one rounded square on a fixed (row,col) grid (matplotlib
                     FancyBboxPatch). Fill by the metric (single-hue green ramp, §4); the
                     focus state in amber; outline the region of interest. RENDER + EYEBALL
                     before shipping — verify it reads as the US (West left, NE top-right).
WHEN A BAR IS BETTER if the message is rank/scale, a sorted bar (§4) is faster and exact;
                     use the map only when geography itself IS the message (the region hit).
LOGO / SVG ASSETS    rasterize brand SVGs to PNG with `sharp` (svg → png at density ~400) to
                     embed in a DOCX header/PPT; artifacts/LibreOffice handle PNG reliably.
```

This is a *fallback*, not the target: when the render tool + served geometry land (`../../docs/status/mcp_gaps.md` R7/R10), the same grounded series drops into a true choropleth. Caption it as a schematic ("each tile is a state").

---

**See also**: `README.md` (stage placement + versioning), `../_style/brand.md` §2/§4 (palette + the figure anatomy), `../_principles/voice.md` §3 (altitude — why drawn precision is false precision), `../../docs/method/analysis_families.md` (the families §1 keys on), `../../docs/method/data_map.md` (the per-series source_ref rule), `.learning/Data Analytics/data_visualization/data_visualization_complete_guide.md` (the full theory).
