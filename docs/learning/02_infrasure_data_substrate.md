# 02 - InfraSure Data Substrate

> **Purpose**: explain what InfraSure data actually contains, where it comes from, and which of it can *ground* a claim versus only *frame* or *route* it.
>
> **Grounded in**: the live `get_plant(57993)` record (Desert Sunlight 300) and `aggregate` output, 2026-06-05.

## Core Idea

InfraSure's moat is not that the model can write. The moat is that the model can reason over **structured, multi-source, pre-resolved** data per entity. A vanilla LLM can describe ENSO. Only a model wired to this substrate can say *which* assets, owned by *whom*, sold to *which offtaker*, with *what* generation history, sit in the exposed region.

```text
generic LLM            : strong language, weak grounding
InfraSure + methodology: same language, plus 13+ structured channels per record
```

Four of those channels (assets, ownership, news facts, offtakers) are wired into MCP today. The rest are the growth path — see `01_mcp_basics.md` on the expandable surface.

## Where The Data Comes From

The tools do not scrape live. They read a **curated, versioned pipeline**. Knowing the pipeline tells you why every result carries an `as_of` date and why some fields are null:

```text
RAW SOURCES                      ZONES                        SERVING
EIA-860/860M, generation   ┐
GEM (ownership chains)     │
Wikidata / Wikipedia       │     data/base/                  JSON export
USPVDB / USWTDB (panels)   ├──>  asset_master.parquet  ──>   + Postgres   ──> MCP tools ──> Claude
PUDL / FERC (financial)    │     data/dimensions/            (Neon)            (_meta.as_of)
eGRID (emissions)          │     ownership, engineering,
LBNL + 7 ISOs (queue)      │     generation, financial,
FERC EQR (offtakers)       ┘     pricing, regions, news…

EXTERNAL (not in substrate): NOAA CPC ENSO state, ONI, seasonal outlooks  ← the methodology supplies these
```

Implication for insights: the substrate grounds *who/where/how-much/owned-by-whom*. It does **not** contain the ENSO state itself — that is an **external input** the methodology brings in (see `docs/04_context_and_data_map.md`).

## Substrate Areas And Scale

| Area | Tool entry point | Scale | What it can ground |
|---|---|---|---|
| Plants + generators | `search_plants`, `get_plant` | ~15.5K / ~29.7K | location, fuel, capacity, status, vintage |
| Interconnection queue | `search_projects`, `get_project` | ~9.8K | development-stage assets, COD, milestones |
| Ownership + companies | `get_plant.ownership`, `plants_by_owner` | 4-layer chains | owner / operator / parent / UBO |
| Offtakers + PPAs | `get_plant.offtakers` | FERC EQR-derived | counterparty, contract term, rate |
| Generation + CF | `get_plant.generation` | monthly series | output, seasonal capacity factor |
| Engineering | `get_plant.generators[].solar/thermal` | per-generator | tilt, tracking, module type, min-load |
| Financial | `get_plant.financial` | FERC + LBNL + OEDI | LCOE, PPA price, capex |
| Emissions | `get_plant.emissions` | eGRID | CO2/NOx/SO2 lb/MWh |
| Pricing / grid | `get_plant.grid` | node crosswalk | LMP node, hub, ISO, voltage |
| News + resolved facts | `search_news`, `get_news_extracted`, `find_by_extracted_fact` | ~57K articles | events + cited developer/EPC/PPA/buyer facts |
| Descriptive context | `get_plant.context` | LLM + Wikipedia | framing only (see below) |

`aggregate` rolls these up. Real call, 2026-06-05 — total solar nameplate by state:

```text
aggregate(entity="plants", group_by="state", metric="total_capacity", filter={fuel:"SUN"})
  TX 70,349 MW   CA 36,843 MW   FL 14,620 MW   GA 9,765 MW   AZ 9,489 MW ...
```

That one call sizes the ENSO-exposed solar fleet per state without fetching a single plant.

## Anatomy Of A Plant Record

`get_plant(57993)` → Desert Sunlight 300 (Riverside County, CA). The blob is grouped — learn the groups, not the 200 fields:

```text
get_plant(57993)
├── identity      plant_id 57993 · slug · "Desert Sunlight 300, LLC" · status Operating · operating_year 2013
├── scale         total_capacity_mw 313.7 · n_generators 11 · primary_fuel SUN
├── grid          iso "caiso" · lmp_node "DSRTSN_2_DS2BX2-APND" · hub "TH_SP15_GEN-APND" · 230 kV
├── regions       iso_rto CAISO · ba CISO · nerc WECC · match_flag "matched"
├── ownership      ← see "routes" below
│     chain: Clearway Energy → Clearway Energy Group (54.9%) → TotalEnergies (50%) → BlackRock (6.1%) → Vanguard (8.7%)
│     operator (utility_eia_name): "NextEra Energy Desert Sunlight 300, LLC"   ← owner ≠ operator
├── generators    11 × Solar Photovoltaic, each: { p_axis "fixed-tilt", thin_film_cdte "Y", tilt 22.5°, p_cap_dc 399, ... }
├── generation    monthly { period, mwh, capacity_factor } · latest_annual_cf 0.242   ← the ENSO-relevant signal
├── financial     lbnl_solar + oedi_solar_value · ppa_price 160.95 $/MWh · lcoe 101.41 (2014)
├── offtakers     top: Pacific Gas & Electric · 28 contracts · energy_ppa_escalating · to 2039-12-16
├── emissions     null (zero-emission solar)
├── context       description {text, model "gemini-2.0-flash", generated_at} · links [EIA, Wikidata, GEM]
└── nearby/similar pre-computed neighbor + peer lists (Haversine / capacity match)
```

One record already spans **six independent sources** (EIA, GEM, Wikidata, LBNL, FERC EQR, OEDI) reconciled into one object. That reconciliation is the substrate's value.

## Three Kinds Of Context — Grounds / Frames / Routes

Not every field can support a claim. Classify each before you cite it:

```text
GROUNDS a claim        FRAMES the entity            ROUTES the insight
(material evidence)     (explanation only)           (who should care)
-------------------     -------------------          -------------------
capacity 313.7 MW       context.description (LLM!)   ownership: Clearway / TotalEnergies
CF 0.242 monthly        Wikipedia summary            offtaker: PG&E (28 contracts)
PPA $160.95/MWh         external links               operator: NextEra
lat/lon, ISO, node      "ranks 6th largest…"         investor: BlackRock / Vanguard
```

**The trap**: `context.description` reads like fact but is **Gemini-generated prose** (`model: "google/gemini-2.0-flash-001"`). It is framing, never proof. A claim grounded only in a generated description is a **blocked claim** (see `docs/03_methodology_resource_standard.md`). Cross every material number back to a structured field.

## The Resolution Layer (The Differentiator)

`get_news_extracted` and `find_by_extracted_fact` expose facts InfraSure *resolved* from many articles — each with a source, a date, a confidence, and a support count. Real call, 2026-06-05:

```text
find_by_extracted_fact(field="developer", value="primergy solar")
  plant 63352 · Primergy Solar · conf 0.95 · 3 articles · POWER Magazine (2024-07-18)
  plant 66625 · Primergy Solar · conf 0.90 · 1 article  · Business Wire (2023-11-28)
  plant 66391 · Primergy Solar · conf 0.80 · 1 article  · PV Tech (2024-10-18)
```

This is grounding *and* its own audit trail: value + source URL + as_of + confidence. No other public energy source exposes this reverse lookup. When a methodology needs "every asset where developer / buyer / PPA-type = X," this is the channel.

## The ENSO-Relevant Signal In Real Data

Solar generation is seasonal, and the substrate already holds the baseline. Desert Sunlight 300 monthly capacity factor:

```text
        Jan   Feb   Mar   Apr   May   Jun   Jul   Aug   Sep   Oct   Nov   Dec
2018   0.14  0.22  0.23  0.30  0.35  0.39  0.33  0.33  0.32  0.24  0.17  0.13
2023   0.20  0.19  0.15  0.26  0.29  0.30  0.29  0.27  0.27  0.26  0.22  0.18
              ^^^^^^^^^^ low Q1 — wet CA winter (atmospheric rivers)
summer peak ≈ 0.38   winter trough ≈ 0.13     (irradiance-driven, robust)
```

What this teaches about grounding ENSO claims:

- The **seasonal shape** (summer high, winter low) is robust and groundable — it is irradiance, not weather noise.
- **Year-to-year winter deviations** (e.g., the depressed Q1 2023, a very wet CA winter) are where a climate-regime signal *could* show up — but attributing a specific winter's dip to ENSO is a **causal claim the methodology blocks**. The data shows the *where to look*; it does not prove the *why*.
- This is exactly why the ENSO resource caps output at **directional exposure**: substrate gives you the asset + its seasonal baseline; ENSO is an external perturbation whose link must stay caveated until controlled analysis exists.

## What The Substrate Does Not Contain (Today)

| Want | Status | Action |
|---|---|---|
| ENSO state / ONI / seasonal outlook | external, not in substrate | methodology supplies it as an **external input** |
| `search_plants(iso=…)` filter | data exists per-plant, filter not wired | use `state`, confirm via `get_plant.regions` — log the gap |
| Plant-level irradiance / weather model | not present | block plant-level production forecasts |
| Offtaker context for every plant | FERC EQR coverage is partial | omit actor relevance where absent, don't invent |

A missing field is not a defect to hide — it is a **confidence downgrade or a roadmap signal**. Name it.

## Contributor Rule

When writing a methodology resource, label **every** input by job:

```text
substrate input   -> grounds the claim       (capacity, CF, owner, node)
external input    -> supplies causal state    (NOAA ENSO)
descriptive       -> frames only              (LLM description, Wikipedia)
actor context     -> routes / activates       (offtaker, owner, investor)
logic / crosswalk -> converts inputs to claims (thresholds, region map, confidence rules)
form              -> shapes the rendering     (resources/_* — exemplars, brand, contracts, plot
                                               rules; never grounds; post-gate except _principles)
```

If you cannot say which job a field does, you cannot yet cite it.

---

**Next**: `03_methodology_resources.md` — how these inputs get assembled into a control surface that constrains the model.
