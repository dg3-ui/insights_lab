# Learning — three render-polish rules from the Standard Solar account DOCX

> **Status**: 2026-06-17. Three defects surfaced on the first client-safe **Brookfield / Standard Solar** multi-peril DOCX (`../../../studio/brookfield_standard_solar/_renders/Standard_Solar_Weather_Hazard_Exposure.docx`). Each is now canon so the next render inherits it. Owner feedback, treated as standing rules (not one-off fixes).

## The three lessons

```text
DEFECT (this render)                         RULE (now canon)                                  HOME
last page held ~4 lines over a sea of        no paginated file ends on a near-empty page;       brand.md B2 #4 ·
  whitespace                                   tail → prior page, or last page ≥ half full;       render.md STEP 4
                                               render to PDF + eyeball the last page              (staged patch)
capacity/CF plots showed exact-looking       any displayed number / CF / share is a             principles.md P7 ·
  numbers with no precision caveat             DIRECTIONAL SCREEN: approximate, not a site/        _craft §4 ·
                                               portfolio model; note it + route detail to          render.md STEP 4
                                               the InfraSure team (forward door on the numbers)    (staged patch)
sources/as_of register set upright, same     the sources / as_of register renders in ITALIC      brand.md §A4
  weight as body copy                          (muted), apparatus set apart from the argument
```

## Why each is a rule, not a one-off

- **Pagination is a render-time check, invisible until paginated.** The orphan page does not exist in the markup; it appears only after the DOCX/PDF lays out. So the discipline is procedural: *render to PDF and look at the last page* before shipping, then tighten spacing / figure sizes / keep-with-next, or balance content. Generalises to any paginated format (PDF, slides).
- **The numbers-note is P7 made concrete.** We already say "scope is a forward door, never a confession." The new edge: an **exact-looking number or a capacity/CF chart** is itself a scope statement — it implies a site-level rigor the fleet screen did not claim. The standing "approximate, directional; contact InfraSure for asset/portfolio detail" note both keeps us honest about precision (`voice.md` §3 false-precision) **and** deflects point-precision questions into the real deeper capability (the owner's stated goal: *reduce direct point questions to InfraSure*). Word it true for observed-history series too, not only modeled ones.
- **Italic sources** is a small brand convention with a real job: the citation apparatus should read as apparatus, distinct from the body argument.

## A fourth, added the same day — P8 (the value-forward close)

Owner feedback in the same review: outputs lack a **curiosity-driven, value-forward ending**, and the reassurance language risks **flattening a concentration finding into "safe."** Added as **Principle 8** — explicitly as a **P6-style smart guide, not a constraint** (the existing output is good; this sharpens, never formularizes; *no* bolted-on CTA on every section). Two halves at different firmness: the **accuracy half** (never render "0 in the maximum / diversified" as low risk; name the residual — e.g. ~47% of the book sits in real hail country even with none in the SPC maximum; a state outside the maximum is not zero at county/cell level) is close to the claim-floor; the **conversion half** (turn the residual into curiosity + a concrete next step: mitigation cost, per-asset risk, revenue/DSCR) is judgment, landed once with a light touch. Threaded into `voice.md` §7 and `output_contracts.md` §2 (moves 8/9). The example that named it: "~24% El Niño exposure (or ~47% in hail country) is **not** a small number" — it is the hook, not a reason to look away.

## A pagination follow-on — connectedness, not just the last page

The first pass fixed the orphan *last* page but left two mid-document break defects (caught on review): a **heading stranded at a page foot** with its body on the next page, and a **figure split from its caption** across a page break (plus a footer page-number that lost its right-alignment). Lesson: the pagination rule is about **visual connectedness at every break**, not only the final page. Mechanically in DOCX this means `keepNext` on every heading **and on any label that introduces a table/figure/list**, `cantSplit` on figures (image+caption), callout boxes, and table rows, and a real right tab (`TabStopType.RIGHT`) so header/footer fields hold their position. `brand.md` B2 #4 was sharpened to say so. Eyeball **every** page break in the PDF, not just the last page.

## Applied

Canon edits live: `principles.md` P7 + **P8** + how-to-use + status; `brand.md` §A4 (italic sources) and B2 #4 (pagination); `_craft` §4 (numbers screen-note); `voice.md` §7 (the close); `output_contracts.md` §2 (close moves). `render.md` STEP-4 additions staged in `render_pagination_numbers_note.patch.md` (protected path this session). The Standard Solar DOCX was re-rendered against the pagination/numbers/italic fixes, then given a light P8 pass (name the hail residual; one sharpened curious value-forward close; no per-section CTAs).

## See also

`render_pagination_numbers_note.patch.md` (the staged command edit), `../../principles.md` P7, `../../../resources/_style/brand.md` (§A4 · B2), `../../../resources/_craft/plot_generation.md` §4, `2026-06-16_audience_strip_internal_vs_external.md` (the prior render-feedback lesson, same shape).
