# 00 - Project Brief

> **Status**: v0 brief, deepened 2026-06-05.
>
> **Audience**: seniors reviewing the direction and juniors executing the first resource package.
>
> **Grounded in**: live InfraSure MCP output, 2026-06-05 — the real entities below are pulled, not invented.

## What InfraSure Insights Is

InfraSure Insights is the analysis layer above InfraSure's asset, company, offtaker, news, engineering, generation, pricing, and context substrate.

It should not produce generic market commentary. It should produce infrastructure decision intelligence:

```text
grounded condition
  + specific asset / region / company / offtaker scope
  + explicit mechanism
  + source references
  + confidence and caveats
  + actor relevance
  =
InfraSure Insight
```

The current platform already has useful data access through MCP/data tools. The missing layer is a methodology-backed analyst: a structured resource that tells the model what to retrieve, how to reason, what not to claim, and how to explain confidence.

## Where The Layer Sits

```text
[ raw sources ]   EIA · GEM · Wikidata · USPVDB/USWTDB · PUDL/FERC · eGRID · LBNL · FERC EQR
       |
       v
[ InfraSure substrate ]   ~15.5K plants · ~29.7K generators · ~9.8K queue projects · ~57K news articles
       |
       v
[ MCP / data tools ]   12 read-only tools today — an EXPANDABLE FLOOR, not a fixed surface (learning/01)
       |
       v
[ methodology resource ]  ◀── THIS PROJECT: what to retrieve · how to reason · what NOT to claim · how to score confidence
       |
       v
[ InfraSure Insight ]   grounded · caveated · source-referenced · actor-routed
       |
       ├──> platform card / Ask answer
       └──> account note / informative email     (activation — ONLY after the claim is validated)
```

The substrate and the tools exist. The methodology layer is what turns "Claude can query InfraSure" into "Claude reasons like a disciplined InfraSure analyst."

## Why This Matters

InfraSure's core users need decision-grade risk intelligence. Grounded against one real CAISO solar asset — **Desert Sunlight 300** (plant `57993`, 313.7 MW, Riverside County; owner Clearway Energy; offtaker Pacific Gas & Electric):

| Actor | Question | Insight job | Real hook on this asset |
|---|---|---|---|
| Owner / operator | What action does this asset need? | Surface exposure, operating relevance, resilience levers, monitoring | Clearway: winter-irradiance variance on a ~0.24 capacity-factor asset |
| Investor | What changes the downside or terminal-value case? | Translate conditions into risk concentration + portfolio implications | TotalEnergies / BlackRock up the ownership chain: CA-solar concentration |
| Lender | Does this asset remain financeable under stress? | Translate physical/market stress into credit, covenant, monitoring | $160.95/MWh PG&E PPA running to 2039 — revenue-stress sensitivity |
| Offtaker / counterparty | Which linked assets or regions matter to us? | Connect power-supply exposure to commercial relationships | PG&E holds 28 contracts on this single asset |

The insight becomes most useful when it can later feed activation:

```text
validated insight object
        ├── platform card / Ask answer
        └── account note / informative email
```

Outreach is not the source of truth. It is a **rendering** of a validated insight.

## V0 Thesis

V0 tests one narrow thesis:

```text
If Claude has:
  1. InfraSure MCP/data tools
  2. one operational methodology resource
  3. a clear prompt projection

then it should be able to draft:
  one grounded applied insight
  with source refs, confidence, caveats, and actor relevance.
```

If that works manually, later work can split into two paths:

```text
validated insight object
        ├── in-house insight architecture
        └── activation / outreach workflow
```

## First Topic

The first resource is **El Niño / ENSO exposure** because it stress-tests the methodology layer:

- external data inputs with their own freshness clocks (NOAA CPC ENSO state / ONI — *not* in the substrate)
- region crosswalks from climate geography to InfraSure entities
- asset fan-out across plants, portfolios, owners, and offtakers
- mixed claim types: mechanistic, statistical, correlational, and scenario-based
- actor-specific relevance for owners, investors, lenders, and offtakers

The v0 resource should not try to forecast exact LMP impacts. The clean first chain is:

```text
ENSO state / forecast
  -> regional weather or irradiance tendency
  -> affected asset or regional fleet
  -> owner / offtaker / portfolio exposure
  -> caveated market or revenue implication
```

Already grounded in the substrate (2026-06-05): CA solar totals **36,843 MW** (`aggregate`); the operating ≥ 50 MW fleet includes Topaz Solar Farm (`57695`, 585.9 MW), Desert Sunlight 300 (`57993`), and Darden I–IV (646 MW each). The seasonal capacity-factor baseline ENSO would perturb is already retrievable per plant (summer ≈ 0.38, winter ≈ 0.13). See `02_analysis_catalog.md` (Exposure family) and `docs/learning/02_infrasure_data_substrate.md`.

## What V0 Proves

V0 is successful if a new contributor can:

1. Understand what InfraSure Insights is.
2. Build or improve the ENSO methodology resource.
3. Produce a prompt projection.
4. Run one manual Claude/MCP test.
5. Record what worked, what failed, and what must change before scaling.

## Read Next

```text
docs/01_scope_v0.md                  -> the exact v0 deliverable and what is out of scope
docs/02_analysis_catalog.md          -> the family this resource belongs to (Exposure)
docs/03_methodology_resource_standard.md -> what every resource must contain
docs/learning/                       -> onboarding: MCP, substrate, resources, projection
```
