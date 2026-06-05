# Methodology Brief — El Niño & US Energy Infrastructure

> **STATUS: STUB.** This file is a scaffold. The user supplies domain knowledge; the analyst structures it against the schema in [`02_methodology_brief_shape.md`](../02_methodology_brief_shape.md) (forthcoming).
>
> Empty sections below are placeholders. Fill in any order; the schema will be argued against the content as it lands.

---

## YAML metadata (top of file in final form — placeholder here)

```yaml
# To be filled in.
# Schema reference: ../02_methodology_brief_shape.md
slug: el-nino-us-energy-infrastructure
brief_id: MB-0001
title: "El Niño / ENSO state effects on US energy infrastructure: irradiance, demand, and LMP"
short_title: "El Niño & US Energy"
kind: methodology_brief
version: "0.0.1-draft"
# ... rest TBD
```

---

## Reference (Diátaxis: bare facts)

What this brief claims, in the most compressed form possible.

**Outputs (vector — TBD how the schema handles this):**

- [ ] **Solar irradiance shift** by climate region under El Niño / La Niña / Neutral ENSO states (W/m², or % vs neutral)
- [ ] **Solar generation impact** per plant — derived from irradiance shift × plant geometry × tracking type
- [ ] **Demand pattern shift** — by climate region; cooling load Δ, heating load Δ, peak timing Δ
- [ ] **LMP impact** — by ISO/BA; magnitude + sign + congestion implications
- [ ] **(Open) Hydro generation impact** — Pacific Northwest, California, Southwest reservoir storage
- [ ] **(Open) Wind generation impact** — jet stream / ENSO interactions

**Time scale:** valid across full ENSO cycles (2-7 years). Quarterly snapshot of the *applied* layer, not the methodology.

**Confidence:** TBD per output — declared per `claim_type`.

---

## Explanation (Diátaxis: the worldview)

The analytical story. Why does ENSO state affect US energy infrastructure, and what's the causal chain?

[USER TO POPULATE — what you know about teleconnections, regional asymmetries, the LMP-via-demand pathway, the historical record]

---

## How-to (Diátaxis: executable procedure)

How an applied insight produced from this methodology actually works. As runnable as we can make it.

### Step 1 — Determine current / forecast ENSO state

External data source: NOAA CPC.

[Procedure TBD]

### Step 2 — Resolve climate regions to substrate entities

This is the new pattern: external regions → substrate entities.

[Procedure TBD]

### Step 3 — Compute irradiance shift per region

[Procedure TBD]

### Step 4 — Roll up to solar generation impact per plant

Substrate join: `engineering_subsystem` (PV vs CSP, tracking type) × `regions` crosswalk × plant location.

[Procedure TBD]

### Step 5 — Compute demand shift per ISO/BA

[Procedure TBD]

### Step 6 — Translate demand + supply shifts to LMP impact

This step has a `claim_type: correlational` flag — LMP formation depends on market structure, marginal generator, congestion patterns.

[Procedure TBD]

---

## Substrate inputs (typed pointers — the moat)

```yaml
# To be filled in. Predicted shape:
substrate_inputs:
  - dim: engineering_subsystem
    fields: [...]
  - dim: generation
    fields: [annual_net_generation_mwh, capacity_factor_monthly]
  - dim: regions
    fields: [iso_rto, ba_code, latitude, longitude]
  - dim: financial / pricing
    fields: [lmp_node, lmp_hourly]  # via lab repo pricing crosswalk

external_inputs:
  - source: NOAA_CPC_ENSO
    vintage_clock: weekly
    fields: [oni, mei_v2]
    fallback: { ... }
  - source: NOAA_CPC_seasonal_outlook
    vintage_clock: monthly
  # etc.
```

---

## Worked examples (applied insights that consume this brief)

To be populated. Examples expected:

1. **"El Niño 2026-2027 forecast — projected impact on CAISO solar fleet"** — applied to all CA solar plants ≥ 50 MW
2. **"ENSO Neutral state — what to expect for ERCOT Q3 2026 LMP"** — applied to ERCOT pricing nodes

---

## Citation & lineage

```yaml
# TBD
```

---

## Validity & staleness

```yaml
# Predicted shape:
validity:
  asserted_window: { start: 1950-01-01, end: null }   # ENSO record goes back this far
  expected_review_cadence: triggered                   # not date-based
  staleness_signals:
    - { source: NOAA_CPC, event: methodology_change }
    - { internal: new_climate_region_dimension_landed, severity: high }
    - { external: ipcc_report_release, severity: medium }
  temporal_scale: multi_year_cycle   # NEW FIELD — to argue with the schema
  confidence:
    overall: medium
    per_claim_type:
      mechanistic: high           # irradiance physics is solid
      statistical: medium         # historical demand correlations
      scenario_based: low         # forecast-conditional claims
```

---

## Surfacing

Where this brief earns its keep on the platform once shipped.

- **Plant page** — for solar plants in ENSO-sensitive climate regions, surface "Related insight: current ENSO state impact" card
- **Region/BA page** — if/when built, hero treatment for the seasonal applied insight
- **Ask pi** — retrievable when user asks about weather impact, capacity factor variance, LMP volatility
- **/insights index** — global filter by topic = `climate`, dimension = `weather`

---

## Notes from drafting (folds into `what_we_learned.md` when shape stabilizes)

[Running log to be populated as we go]
