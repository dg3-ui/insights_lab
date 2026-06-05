# 01 - MCP Basics

> **Purpose**: give a contributor enough MCP context to run the v0 manual test against the *real* InfraSure tool surface — and to treat that surface as a starting point we expand, not a fixed boundary.
>
> **Grounded in**: live InfraSure MCP output, 2026-06-05. Every call and response shown below is real, not invented.

## Working Definition

MCP (Model Context Protocol) gives the model tools it can call mid-conversation. For InfraSure Insights it is the **data-access layer**: it lets Claude retrieve curated platform data instead of reasoning from generic, undated training memory.

```text
Claude WITHOUT MCP
  -> answers from general model memory
  -> no entity IDs, no source, no as-of date
  -> cannot be grounded or audited

Claude WITH InfraSure MCP
  -> calls InfraSure data tools
  -> returns real plant_ids, capacities, owners, dates
  -> claims can carry a source_ref and a vintage
```

Grounding is the entire point. An applied insight is only as defensible as the tool result behind it. If a claim has no tool result, it is commentary, not an InfraSure Insight.

## The InfraSure MCP Surface (Today)

The current surface is **12 read-only tools** over the public platform — ~15,500 operating plants, ~29,700 generators, ~9,800 queue projects, ~57K classified news articles. Read them by job, not alphabetically:

| Group | Tools | Returns | ENSO v0 use |
|---|---|---|---|
| **Discover** | `search_plants`, `search_projects`, `plants_by_owner`, `nearby_plants` | slim entity rows (id + slug + headline fields) | resolve the asset set in scope |
| **Drill** | `get_plant`, `get_project`, `compare_entities` | full JSONB blob per entity | pull capacity, region, owner, generation |
| **Roll up** | `aggregate`, `get_aggregate_news_stats` | grouped counts / capacity sums | size the fleet by state / fuel / ISO |
| **News + facts** | `search_news`, `get_news_extracted` | classified articles / resolved facts | corroborating event context |
| **Differentiator** | `find_by_extracted_fact` | reverse lookup: every entity where a resolved fact = value | "every plant where developer = X" |

The **discover → drill** pattern is the spine of almost every session:

```text
search_plants(...)  ->  returns plant_id + slug
        |
        v
get_plant(plant_id) ->  returns the full record you reason over
```

`find_by_extracted_fact` is the one tool with no public-data equivalent: it reverse-looks-up the resolution layer (developer, EPC, PPA terms, buyer/seller, milestones) that InfraSure derives from news. Treat it as the "what makes us different" tool.

## Anatomy Of A Real Call

Resolving large California solar — the v0 asset set:

```text
search_plants(fuel="solar", state="CA", minMw=50, limit=8)
```

returns slim rows (real, 2026-06-05):

```text
plant_id  name                MW     county           canonical_owner
57695     Topaz Solar Farm    585.9  San Luis Obispo  BHE Solar LLC
68607     Pelicans Jaw Hybrid 678.5  Kern             Pelicans Jaw Solar
69661-4   Darden I–IV Solar   646.4  Fresno           Intersect USA, LLC
69956     Sanborn Hybrid 3    578.0  Kern             Terra-Gen
64633     Rexford Solar Farm  540.0  Tulare           Avantus
...
_meta: { as_of: "2026-06-05", source: "InfraSure" }
```

Notice two things on **every** call:

- Each row carries a `plant_id` (pass to `get_plant`) and a `slug` (the public URL fragment). These are how you cite the claim.
- The `_meta.as_of` envelope is your **vintage**. Every grounded claim inherits that date; write it into the `source_ref`.

## The Surface Is The Floor, Not The Ceiling

**Do not treat the MCP as a fixed thing.** The 12 tools are the *initial* surface — the v0 floor. The product vision is a tool surface that **grows as methodology resources reveal what analysts actually need to retrieve**. That changes how you read a tool gap:

```text
fixed-surface mindset          expandable-surface mindset (ours)
---------------------          ---------------------------------
"the tool can't do X"          "X is the next tool/field/filter to build"
gap = dead end                 gap = roadmap input
work around it silently        log it as a tool gap, then work around it
```

So a contributor's job during a test is not only to produce an insight — it is to **map the delta between what the methodology needs and what the surface currently exposes**. That delta is the deliverable that grows the platform.

## A Real Tool Gap (Live, 2026-06-05)

The ENSO resource recommends the scope "CAISO solar ≥ 50 MW." The obvious first call fails:

```text
search_plants(fuel="solar", iso="CAISO", minMw=50)   ->  data: []   (empty!)
search_plants(iso="CAISO", limit=5)                  ->  data: []   (empty even alone)
search_plants(fuel="solar", state="CA",  minMw=50)   ->  8 real plants  ✅
```

Yet `get_plant` on any of those CA plants returns rich ISO data:

```text
get_plant(57993).regions.iso_rto = { code: "CAISO", name: "CALIFORNIA INDEPENDENT SYSTEM OPERATOR" }
get_plant(57993).grid.iso        = "caiso"
```

So the per-plant ISO/region data **exists**; the `search_plants(iso=...)` *filter* just isn't wired to it. This is the expandable-surface thesis made concrete:

- **Today's workaround**: resolve the CAISO fleet via `state="CA"` (a close proxy — CA is overwhelmingly CAISO territory, with a few municipal balancing authorities like LADWP, SMUD, and IID outside it), then confirm each plant's ISO using the per-plant `regions.iso_rto` field from `get_plant`.
- **Roadmap signal to log**: "wire the `search_plants` ISO filter to the existing per-plant region join (or add a `resolve_region` tool)." That single line, captured in a test log, is exactly the kind of input that turns the surface from 12 tools into 13.

## Verify That Claude Actually Used The Tools

A model can *narrate* tool use without doing it. During review, separate grounded from generic:

| Signal | Grounded | Generic (reject) |
|---|---|---|
| Entity IDs | cites real `plant_id` / `slug` | names plants with no IDs |
| Numbers | match a tool result (585.9 MW) | round, "about 500 MW", unattributed |
| Vintage | carries an `as_of` date | none, or a training-era date |
| Source | InfraSure tool or named external | "it is well known that…" |

**Verify, do not trust the labels either.** The `get_plant` docstring says "56051 = Topaz Solar." It is not — `56051` is **THUMS, a 57 MW gas peaker**; Topaz Solar Farm is `57695`. Tool descriptions can be stale; confirm the entity you got is the entity you wanted before you build a claim on it.

## Logging Tool Gaps

Every gap goes into the test record (`resources/<topic>/test_runs/`) under the **MCP/tool gap** row of the failure taxonomy (see `docs/05_mcp_test_protocol.md`). A good gap log has three parts:

```text
gap:        search_plants(iso="CAISO") returns [] — ISO filter not wired
workaround: used state="CA" + per-plant regions.iso_rto confirmation
roadmap:    wire ISO filter to region join, or add resolve_region tool
```

The workaround keeps the test moving; the roadmap line is what feeds the expandable surface.

## V0 Rule

Do **not** build MCP integration, new tools, or an agent in v0. The v0 loop is manual:

```text
prompt_projection.md
  -> Claude/MCP session (these 12 tools)
  -> manual tool use, verified
  -> applied-insight draft
  -> test log  (insight + tool gaps + roadmap signals)
```

You are not allowed to *build* the next tool yet. You **are** expected to discover and document what it should be.

---

**Next**: `02_infrasure_data_substrate.md` — what the data behind these tools actually contains, and which of it can ground a claim vs. only frame or route it.
