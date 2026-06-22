# The Confidence Model — Three Axes, One Posture

> **Status**: v0, 2026-06-15 (`../plans/2026-06-15_output_layer_architecture.md` Phase 1). The canonical confidence model for InfraSure Insights. **Confidence is not one number.** It is three orthogonal axes; only one is a *grade*, and that grade never reaches the rendered face.
>
> **Why this is its own doc**: the model is referenced by `resource_standard.md` (the cap ladder), `../../resources/_principles/rubric.md` (criterion 4), `../../resources/_style/output_contracts.md` (the public display), `../../resources/_style/brand.md` (§A4 the widget), `../../resources/_principles/voice.md` (§5 posture), and `../../studio/_triage.md` (the ranking). One foundation, many bindings — so it lives in one place, and they all point here (P1: a stable methodology layer the execution layer reads).

## §1 · The three axes

A claim about a weather/hazard exposure carries **three independent measures**. Conflating them into a single "Confidence: LOW" is the error this model exists to fix.

| Axis | The question it answers | Grounded by | Where it lives |
|---|---|---|---|
| **CALIBRATION CAP** | How hard may we assert *this* claim? | the **weakest required input** (`resource_standard.md` Confidence Rules) | **internal** grade |
| **EVENT LIKELIHOOD** | How probable is the driving condition in the world? | a **named external source** (NOAA 63% very-strong El Niño) | **on output** |
| **MATERIALITY** | If the condition bites, how big is the stake? | **exposed-share × class-severity band** (§4) | **internal** |

They move independently. The Brookfield ENSO read makes this concrete:

```text
EVENT LIKELIHOOD   63% very-strong El Niño (NOAA)        — NOT low. a firm, sourced odds-shift.
CALIBRATION CAP    LOW (directional)                     — noisy teleconnection + no production model.
MATERIALITY        modest (~23% of MW exposed, diversified) — the stake is small BY DESIGN.
```

"Confidence: LOW" would have flattened all three into "not worth your time." The truth is sharper: a **likely** event, a **directional** claim, a **small** stake. Three facts, three axes.

## §2 · The CAP ladder (the only graded axis)

The calibration cap is the existing `resource_standard.md` ladder, now named as one axis of three. It is the **firewall** — what `blocked_claims` and `confidence_rules` enforce.

```text
HIGH      mechanism strong · scope resolved · refs current · claim narrow
MEDIUM    mechanism credible · one input / crosswalk / comparison imperfect
LOW       directional · scenario-based · depends on external forecasts or noisy teleconnection
BLOCKED   required input missing · source stale · scope unresolved · claim exceeds allowed logic → REFUSED upstream
```

**The cap is set by the weakest required input and nothing raises it** — not a high event-likelihood, not a severe stake. A 63%-likely event with a severe stake is still a LOW-cap claim if the mechanism is a noisy teleconnection with no model behind it. This is the discipline the other two axes must never erode.

## §3 · What renders vs what stays internal

```text
ON OUTPUT (render-public)              INTERNAL (render-internal)
  POSTURE  (cap → a register phrase)     the CAP GRADE (High/Med/Low/Blocked)
  EVENT LIKELIHOOD (sourced number)      the MATERIALITY band
  SETTLEDNESS SIGNAL (§5)                the TRIAGE verdict (act/watch/noise)
```

**Single source of truth.** The three axes are recorded **once**, in the **gate-record** — the applied-insight object on the baseline path (`resource_standard.md` Applied-Insight contract), or a studio brief's §1 when a piece goes through the studio lane (`../../studio/_brief_template.md`). The output's posture (and, for a studio read, the triage board's ranking) both **derive** from that record — neither re-states a grade. A grade that appears in two places drifts; a grade with one home does not.

### §3a · Posture — the register-translation of the cap

The cap is internal; what the reader sees is its **posture**. Translate, never badge:

| Cap (internal) | Posture (on output) |
|---|---|
| High | stated plainly, as fact with its source |
| Medium | "a well-grounded read; one input is still imperfect" |
| Low | "a forward, directional read — watch, don't act yet" |
| Blocked | nothing renders (refused at the gate) |

Never emit "Confidence: LOW" on a public/client face — it reads as *low quality* when it means *we are not asserting a number you'd hold us to* (`../principles.md` P7; `../../resources/_style/output_contracts.md` §3). An internal/expert reader who *wants* the grade may keep the explicit cap line — the surfacing differs by audience, the gate verdict underneath does not.

## §4 · Materiality — the grounded basis

Materiality answers "how big is the stake," and it must be **grounded**, not asserted. The basis:

```text
MATERIALITY  =  exposed-share   ×   class-severity band
                (substrate count) (a documented band on the resource — NEVER a $)

exposed-share    the % of the subject's MW / plants in the exposed bucket — a hard substrate count
                 (Standard Solar: ~23% of MW in the El-Niño-sensitive Southwest belt)
class-severity   how hard the driver hits this asset class — a qualitative band read from the
                 resource's own canon, NEVER a $, and grounded by resource type:
                   · HAZARD/peril resource → the `financial_materiality` field (`resource_standard.md`)
                   · WEATHER/climate resource → the documented (driver × asset-class) sensitivity in the
                     resource's knowledge.md (e.g. ENSO's CA/SW DJF teleconnection robustness, knowledge §4)
                 if the resource documents no severity band for the cell, materiality is `unknown` —
                 record it as a gap, do not assert a band.
```

The output is a **band**, never a dollar figure (a $ is a model output — `model-gpr`, a blocked claim in the lab):

```text
negligible   modest   meaningful   severe
```

**Materiality is a tie-breaker, never an override.** It orders *which* low-cap reads to surface first (a severe-stake LOW beats a negligible-stake LOW in the WATCH queue). It **never** raises the cap and never unblocks a blocked claim. A huge stake under a directional read is still a directional read — just one worth watching first.

## §5 · The settledness signal (the forward indicator)

On output, the calibration posture is paired with a **5-segment settledness bar**. It fills with how **settled the driving signal is** — driven by the *event-likelihood firming over time* (a forecast resolving from 63% toward 90% as the season arrives), **not** by our self-grade.

```text
SIGNAL  ▰▰▰▱▱   "settling — firms as the 2026-27 winter resolves"

  fills as     the external forecast firms (NOAA updates 63% → 70% → 90% …) and the window nears
  reads as     a FORWARD pointer: what to watch, when it resolves
  NEVER reads  "3/5 = we're 60% sure" — it is not our confidence, it is the world's settledness
```

This is the P7 move in a widget: a scope/uncertainty fact rendered as a *forward door* ("watch this firm up"), never as self-doubt ("we're unsure"). The bar tracks the **event-likelihood axis as it matures**, which is honest and external; the calibration cap behind it stays internal.

## §6 · Per-part confidence

A composite claim carries a cap **per part**. The Galveston surge read is the worked case — one claim, three parts, three caps:

```text
the corridor co-locates fuel + grid + generation on one plain     CAP: medium-high
a major-hurricane surge would hit the cluster simultaneously       CAP: medium
forward, this-season risk to the named assets                      CAP: low / directional
```

Each part renders its own posture. In **triage**, the subject's **headline verdict is set by the binding (lowest) cap** — so a composite read does not get promoted by its strongest part. A higher-cap part that stands on its own (a hard fact, like the Galveston co-location count) earns its **own co-equal row** with its own verdict; it is not folded into the headline row. So a subject can legitimately show two rows (e.g. an `ACT/WATCH` co-location row beside a `WATCH (high)` forward-risk row) — that is the expected shape, not an exception to the binding-cap rule.

## §7 · render-internal vs host-private (two orthogonal axes — do not conflate)

```text
RENDER-INTERNAL   not on the rendered artifact          the cap grade · materiality · the triage verdict
HOST-PRIVATE      not on a public git remote             the repo's visibility setting

ORTHOGONAL: a private repo does NOT make it safe to print the cap grade on a client render.
  render-internal is a CONTENT discipline (what the artifact says); host-private is an INFRA setting
  (where the file lives). The grade stays off the rendered face regardless of where the repo sits.
```

A studio brief lives in a (currently private) repo, but the brief is *designed to be handed to a client* — so the grade, the materiality band, and the triage verdict stay in the internal-only sections, never in the rendered output, independent of the remote's visibility.

## §8 · How it binds

```text
resource_standard.md   Confidence Rules — the CAP ladder (§2) lives there, now framed as one of three axes
rubric.md crit. 4      "smartfulness" judges the cap + altitude; materiality + event-likelihood are the other axes
output_contracts.md §3 the public display: posture + event + settledness, never the "LOW" badge
brand.md §A4           the caveat box + the settledness widget on the rendered face
voice.md §5            posture-not-confession, the P7 register
studio/_brief_template §1 the gate-record: the SINGLE source of truth for all three axes (per-part)
studio/_triage.md      the ranking: derives cap + materiality, never re-types them
```

---

**See also**: `../principles.md` P7 (calibration is posture and a forward door — the principle this model operationalizes) · `resource_standard.md` Confidence Rules (the cap ladder + the materiality basis: peril `financial_materiality` / weather `knowledge.md` sensitivity) · `../../resources/_style/output_contracts.md` §3 (public vs internal display) · `../../resources/_style/brand.md` §A4 (the widget) · `../../studio/README.md` (the layer that consumes this) · `../../studio/_triage.md` (the derived ranking).
