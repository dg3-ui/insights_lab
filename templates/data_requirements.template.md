# Data Requirements — &lt;Driver&gt; &lt;Family&gt;

> **Status**: draft.
>
> **Purpose**: define exactly what the manual MCP/Claude test must retrieve (and from where), what is external, and what to do when an input is missing.
>
> **Companions**: `knowledge.md` (mechanism + sources), `resource.md` (method).

## Input Layers (by job — see `docs/04`)

```text
EXTERNAL     <driver> state/forecast    → <external source> (pull live)           knowledge.md §3, §8
FOUNDATIONAL mechanism + robustness     → knowledge.md (basics from .learning/)   (cite, don't re-derive)
SUBSTRATE    assets, capacity, region   → search_plants → get_plant               (grounds the claim)
SUBSTRATE    generation / CF / financial→ get_plant.<...>                          (asset baseline)
ACTOR        owner / offtaker           → get_plant.ownership / .offtakers         (routes the insight)
DESCRIPTIVE  plant blurb / Wikipedia    → get_plant.context                        (frames only — never grounds)
LOGIC        thresholds, region map     → <≥N MW, crosswalk>                       (converts inputs to claims)
```

## Required Inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| &lt;driver&gt; state / forecast | external | establish condition | source name, access date, phase/value |
| Mechanism + robustness | foundational | the *why* + confidence ceiling | cite `knowledge.md` |
| Region / market scope | substrate / logic | bound the test | one resolvable region |
| Plant / generator list | substrate | asset scope | operating assets in scope |
| Capacity | substrate | materiality | &lt;threshold&gt; |
| Owner / company | substrate / actor | actor relevance | name where available |

## External STATE — Where To Pull It

| Source | Use | URL |
|---|---|---|
| &lt;external source&gt; | current state + forecast | &lt;url&gt; |

## First-Test Retrieval Plan (the real call sequence)

```text
1. STATE:   pull <external> state → phase/value + date     (cite access date)
2. SCOPE:   search_plants(<filters>)                        → fleet rows   (⚠ note any unwired filter)
3. SIZE:    aggregate(...)                                  → fleet total
4. DRILL:   get_plant(<id>)                                 → baseline, region, ownership, offtakers
5. ACTOR:   get_plant.ownership / .offtakers                (or plants_by_owner for a portfolio view)
6. DRAFT:   assemble the claim; cap confidence; block quantitative claims
```

## Known Gaps (log to `docs/09`, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| &lt;tool/filter gap&gt; | &lt;what's missing&gt; | &lt;proxy&gt; | &lt;the fix to log&gt; |

## Missing-Data Handling

| Missing input | Required action |
|---|---|
| External state | **Block** — cannot establish the condition |
| Region unresolvable | downgrade, or switch to a resolvable region |
| Asset list unavailable | **Block** — no scoped entity set |
| Owner/company unavailable | asset-level claim only; actor relevance goes generic |
| Offtaker unavailable | omit offtaker relevance (do not infer) |
| Generation/pricing unavailable | keep revenue implications directional and caveated |
