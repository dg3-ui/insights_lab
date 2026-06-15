# studio/_triage — The Prioritization Board (internal · never rendered)

> **Status**: v0, opened 2026-06-15 (`../docs/plans/2026-06-15_output_layer_architecture.md` Layer 2). The **one** cross-subject prioritization surface for the output layer. It answers a different question than any single brief: *across everything we've gated, what deserves attention first?*
>
> **Render-internal, always** (`../docs/method/confidence_model.md` §7). This board carries the **cap grade**, the **materiality band**, and the **triage verdict** — none of which ever appear on a rendered artifact. It is **never attached** to a cloud render. Its being in a (private) repo is irrelevant: render-internal is a content rule, not an infra setting.
>
> **Derived, never authored twice.** Every value here is *read* from a phenomenon file's §1 gate-record (the single source of truth). The board re-states nothing; it links each row to its §1. If a §1 changes, the board is re-derived, not edited in parallel.

## How a verdict is set

The board ranks by the two **internal** axes (cap + materiality); the **event likelihood** is context, not a ranker.

```text
                 MATERIALITY (the stake — exposed-share × class-severity band)
                 negligible          modest            meaningful / severe
CAP   high   │   NOISE (log)         WATCH             ACT   (firm finding, real stake → do something now)
(firm)       │
      medium │   NOISE               WATCH             ACT / WATCH
      low    │   NOISE               WATCH (low)       WATCH (high — surface first among low-cap reads)
(direct.)    │
      blocked│   — never reaches the board (refused at the gate) —
```

```text
ACT     a firm-cap finding with a meaningful+ stake → a decider should act now (diligence, harden, weather-normalize)
WATCH   a low/directional-cap read with a real stake, OR a firming event → monitor; revisit as the signal resolves
NOISE   negligible stake, or a low-cap read with nothing material behind it → logged, not surfaced
```

Materiality is the **tie-breaker among low-cap reads** (a severe-stake LOW outranks a modest-stake LOW in the WATCH queue), never an override of the cap (`confidence_model.md` §4). A **medium-high** cap reads with the medium row → **ACT / WATCH** (a hard fact — a count, a co-location — firms it toward ACT; a soft inference toward WATCH). Per-part claims take their **binding (lowest) cap** for the **headline** verdict — a composite read is never promoted by its strongest part; a higher-cap part that stands alone (a hard fact) earns its **own co-equal row** with its own verdict (`confidence_model.md` §6).

## The board

Direction is a meta-tag (scope: `account` → `region` → `market`); all current rows are `bottom_up` (no top-down market piece grounded yet).

| Subject | Scope · dir | Phenomenon (facet) | Cap | Materiality | Event likelihood | Verdict | §1 source |
|---|---|---|---|---|---|---|---|
| Galveston Bay / Ship Channel corridor | region · bottom_up | storm surge — co-location *(stand-alone fact)* | medium-high | **meaningful–severe** (~3.7 GW in one surge cell) | NOAA 2026 below-normal | **ACT / WATCH** — a hard count; diligence/harden the concentration | [galveston_ship_channel_surge/storm_surge.md](galveston_ship_channel_surge/storm_surge.md) §1 |
| Galveston Bay / Ship Channel corridor | region · bottom_up | storm surge — forward season *(headline)* | **low** (binding) | **meaningful–severe** | NOAA 2026 below-normal — "it only takes one" | **WATCH (high)** — surface first among low-cap reads | [galveston_ship_channel_surge/storm_surge.md](galveston_ship_channel_surge/storm_surge.md) §1 |
| Brookfield / Standard Solar | account · bottom_up | severe hail | **low** (directional) | **meaningful** (0 MW in the US hail maximum; ~6% CO + ~41% MN/IL/NM) | climatological — *none in the SPC maximum* | **WATCH (high)** — hail outranks ENSO on severity; confirm hail-stow / deductible on CO + MN/IL | [brookfield_standard_solar/hail.md](brookfield_standard_solar/hail.md) §1 |
| Brookfield / Standard Solar | account · bottom_up | el_nino / ENSO | **low** (binding) | **modest** (~23% of MW, diversified) | 63% very-strong El Niño (firming) | **WATCH (low)** — reassuring; weather-normalize the 83.8 MW SW belt only | [brookfield_standard_solar/el_nino_enso.md](brookfield_standard_solar/el_nino_enso.md) §1 |
| Brookfield / Standard Solar | account · bottom_up | extreme-heat derate | **low** (directional) | **low** (modest derate, muted by fixed-price PPAs) | NOAA JJA above-normal (West) | **NOISE** — logged; real physics, immaterial to this fixed-price book; no action beyond O&M | [brookfield_standard_solar/extreme_heat.md](brookfield_standard_solar/extreme_heat.md) §1 |

*(Galveston's §1 records three per-part caps — co-location `medium-high` · simultaneous-hit `medium` · forward `low`. The board shows the stand-alone fact and the binding headline; the `medium` simultaneous-hit is the mechanism bridge between them, not a separate verdict.)*

**Reading the board (2026-06-15).** Five reads. Four carry a **low cap** and are ordered purely by **materiality**: Galveston's forward surge (meaningful–severe, 3.7 GW in one cell) → Standard Solar's **hail** (meaningful — hail physically breaks panels, high class-severity, even spread across CO/MN/IL) → **ENSO** (modest — a mild winter-CF nudge, diversified) → **extreme heat**, which bottoms out at **NOISE** (real physics, but a modest derate whose peak-hour sting is muted by fixed-price PPAs — logged, not surfaced). So within the *same* account, **hail > ENSO > heat** by severity alone, not exposed share. Above all four sits Galveston's co-location count, a hard medium-high-cap fact that earns its **own ACT/WATCH row** (diligence the concentration) without promoting its subject's low-cap headline. Standard Solar's **offtaker concentration** was triaged too but is **BLOCKED** (`offtakers` null book-wide) so it earns **no row** — blocked never reaches the board (mcp_gap R13). That is the rule working: materiality orders attention, a stand-alone firm fact gets its own row, blocked stays off — and none of it ever lifts the binding cap (`../../docs/method/confidence_model.md` §4, §6).

---

**See also**: `../docs/method/confidence_model.md` (the three axes this board reads; §3 single-source, §4 materiality, §7 render-internal) · `_brief_template.md` §1 (the gate-record each row derives from) · `README.md` (the layer this completes) · `../docs/plans/2026-06-15_output_layer_architecture.md` (Layer 2).
