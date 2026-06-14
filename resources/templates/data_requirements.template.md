# Data Requirements — <Title>

> **Status**: draft <YYYY-MM-DD>. What the manual MCP/Claude test must retrieve, from where, and what to do when an input is missing. Worked reference: `../weather_and_climate/el_nino_enso/data_requirements.md`.

## Input layers (by job — `../../docs/method/data_map.md`)

```text
EXTERNAL    <driver/event state>      -> <named feed> (pull live, dated)        knowledge.md §3
KNOWLEDGE   mechanism + robustness    -> knowledge.md                          (cite, don't re-derive)
SUBSTRATE   assets, capacity, region  -> search_plants → get_plant             (grounds the claim)
ACTOR       owner / offtaker          -> get_plant.ownership / .offtakers      (routes the insight)
DESCRIPTIVE blurb / wikipedia         -> get_plant.context                     (frames only — never grounds)
LOGIC       thresholds, region map    -> <materiality cut, region crosswalk>   (converts inputs to claims)
```

## Required inputs

| Input | Type | Needed for | Minimum standard |
|---|---|---|---|
| `<driver/event state>` | external | establish the condition | source name + access date + `<the state fields>` |
| Mechanism + robustness | knowledge | the "why" + confidence ceiling | cite `knowledge.md` |
| Region / market scope | substrate / logic | bound the test | one resolvable region |
| Plant / generator list | substrate | asset scope | `<operating … in scope>` |
| Capacity | substrate | materiality | `<recommended threshold>` |
| Owner / company | substrate / actor | actor relevance | owner name where available |

## External state — where to pull it

| Source | Use | URL |
|---|---|---|
| `<named feed>` | `<the current state>` | `<URL>` |

Pull live each test; cite the access date. `<For hazards: also query the `hazards` news category and VERIFY the classification.>`

## Retrieval plan (the real call sequence)

```text
1. STATE:  <pull the external state / hazards news → the state fields>          (cite access date)
2. SCOPE:  search_plants(fuel="<...>", state="<...>", minMw=<...>)               → fleet rows  (VERIFY entities)
3. SIZE:   aggregate(entity="plants", group_by="<...>", metric="<...>", filter={...})
4. DRILL:  get_plant(<id>)  → <grounding fields: CF / geometry / ownership / offtakers>
5. DRAFT:  assemble the claim; cap confidence at the weakest link; block quantitative/$ claims
```

## Known gaps (log, then work around)

| Gap | Reality | Workaround | Roadmap |
|---|---|---|---|
| `<the gap>` | `<what's actually available>` | `<the proxy>` | `<the fix>` |

Also log each to `../../docs/status/mcp_gaps.md` (gap · workaround · roadmap).

## Missing-data handling

| Missing input | Required action |
|---|---|
| `<external state>` | **Block** — cannot establish the condition |
| Region unresolved | downgrade, or switch to a resolvable region |
| Asset list unavailable | **Block** — no scoped entity set |
| Owner / offtaker unavailable | asset-level claim only; do **not** infer the actor |
| Generation / pricing unavailable | keep implications directional + caveated |
