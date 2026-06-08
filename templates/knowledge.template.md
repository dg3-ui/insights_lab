# Knowledge — &lt;Driver&gt; For &lt;Asset Scope&gt;

> **Status**: draft.
>
> **Purpose**: the **mechanism library** for &lt;driver&gt; analysis — what it is, how it is measured and where to pull it, how it teleconnects to US power-infrastructure conditions (rated by how trustworthy each link is), and how that maps to InfraSure entities. This is the **why/how** layer.
>
> **What this is NOT**: not the method (`resource.md`), not the data (the MCP substrate). Supplies the *mechanism* + *caveat* slots of a claim; the substrate supplies the *assets*; the external source supplies the *state*. Cite it — never let it substitute for retrieving asset data.

## 0. The Three Layers

```text
DATA       who / where / how much  → MCP substrate (search_plants, get_plant)        [retrieve · cite as_of]
KNOWLEDGE  why / how the mechanism  → THIS FILE + cited sources (+ .learning/ basics)  [reason · cite source]
STATE      what is happening now    → <external source> (pull at test time)            [external · has a clock]
```

## 1. What &lt;Driver&gt; Is

&lt;One paragraph: the phenomenon, its phases/regimes if any, what makes it predictable-with-lead-time (the reason it is analytically useful) and probabilistic (the reason claims stay directional).&gt;

## 2. Why It Matters For Power Infrastructure

```text
<driver> → regional weather/market/policy tendency → asset-relevant variable → revenue / risk implication
   e.g.  <driver state> → <regional effect> → <CF / demand / curtailment / outage> → <implication>
```

## 3. How It Is Measured (and where to pull it)

| Index / signal | What it is | Threshold / use |
|---|---|---|
| &lt;index&gt; | &lt;definition&gt; | &lt;threshold / episode rule&gt; |

**Pull the STATE live every test** — it has a freshness clock (§8). A clearly-dated snapshot may be quoted, but it goes stale; re-pull before any real use.

## 4. Teleconnections / Mechanism — rated by robustness

Effects are **probabilistic shifts in the odds**, not deterministic. Robustness varies by region/variable — treat the rating column as a **confidence ceiling**.

| Region / channel | Tendency | Robustness (High / Moderate / Low-noisy) | Power-infra relevance |
|---|---|---|---|
| &lt;region&gt; | &lt;tendency&gt; | &lt;rating&gt; | &lt;solar/wind/hydro/demand effect&gt; |

## 5. Asset-Specific Mechanism (&lt;focus technology&gt;)

&lt;How the driver moves this asset class's output/risk; the substrate baseline it perturbs (cite a real `get_plant` series); a real counter-example, if one exists, that shows why claims stay directional/LOW.&gt;

## 6. From Knowledge To Confidence (how this caps claims)

```text
forecast lead / strength    → caps at <LOW/MED>
teleconnection robustness   → caps at <best regional rating>
single-event noise          → any one event can defy the composite → caps at LOW
downstream modeling         → production / price not modeled here → BLOCK quantitative claims
─────────────────────────────────────────────────────────────────────────────────────
NET for <driver> → asset:   DIRECTIONAL, <LOW>. Never "High". Never a number.
```

## 7. Region / Scope Crosswalk (driver geography → InfraSure entity)

| &lt;Driver&gt; region | InfraSure scoping | Note (filter gaps?) |
|---|---|---|
| &lt;region&gt; | `state=` / `iso=` / `region=` | &lt;known filter caveats — log to docs/09&gt; |

## 8. Sources

- **Foundational basics (stable)** — `.learning/` (&lt;relevant vault folders, e.g. `Risk/`, `Electricity Market/`, `ML-DL/InfraSure_related/weather_climate`&gt;). Cite the note; this is the curated *why*, not live state.
- **Live state** — &lt;external source name + URL&gt;. Pull live; carry the access date.

| Source | Use | URL |
|---|---|---|
| &lt;external source&gt; | current state / forecast | &lt;url&gt; |

**Citation rule**: every material claim cites a substrate tool result (with `as_of`) or an external source + access date. The mechanism statements here are general domain knowledge (cite the sources above / `.learning/`); the *current state* must always carry the date it was pulled.

---

**See also**: `resource.md` (the method that consumes this), `docs/04_context_and_data_map.md` (input taxonomy), `docs/08_design_principles.md` (P2: content downstream of insight). Worked exemplar: `resources/weather_and_climate/el_nino_enso/knowledge.md`.
