# 02 — Methodology brief shape (schema v0)

> **Status**: v0 draft, 2026-05-31. Adapted from the schema proposed in [`research/03_methodology_traditions.md`](research/03_methodology_traditions.md), hardened with the predicted stress points from the El Niño brief ([`05_first_methodology_brief/`](05_first_methodology_brief/)). Expected to flex with the first brief — see "What's expected to change" at the end.
>
> **Authority**: this schema specifies the data model for a methodology brief. Writers don't argue with it; they author content into it. If the schema doesn't fit, that's a schema-revision conversation, not a writer-improvisation conversation.

## Reading guide

- Every field is annotated with one of:
  - **[validated]** — proven against an actual brief or research thread; load-bearing.
  - **[candidate]** — added speculatively from El Niño prediction or research thread synthesis. To be confirmed or removed during the first brief.
  - **[TBD]** — included as a placeholder; concrete shape resolves with the first brief.
- The schema is YAML in the canonical form. Rendering pipelines (web pages, downloadable PDFs, prompt projections for the agent) read this YAML; humans rarely look at the raw form.

---

## The schema (v0)

```yaml
# methodology_brief.schema.yml — v0
# Schema is the source of truth. brief.md files declare data against this schema.

# ── Identity (immutable after first publish) ──────────────────────────────
slug: <kebab-case-slug>                       # [validated] URL slug, never changes after publish
brief_id: <MB-NNNN>                           # [validated] numeric persistent ID
title: <full title>                           # [validated]
short_title: <chip/breadcrumb title>          # [validated]
kind: methodology_brief                       # [validated] vs. applied_insight

# ── Versioning (two clocks: live + snapshot) ──────────────────────────────
version: <semver>                             # [validated] major = breaking re-interpretation
                                              # minor = added scope or claims
                                              # patch = corrections that don't change conclusions
current_snapshot: <YYYY-QN>                   # [validated] latest immutable edition
snapshots:                                    # [validated] all archived editions
  - id: <YYYY-QN>
    published: <date>
    snapshot_url: /insights/methodology/<slug>/<YYYY-QN>
    changed_from_previous: <bool>             # [candidate] true if content differs from prior snapshot
last_reviewed: <date>                         # [validated]
withdrawn: false                              # [candidate] for takedowns; URL still resolves with notice

# ── Subject matter (controlled vocabulary) ────────────────────────────────
topics:                                       # [validated] DefinedTerm-style
  - <namespace>:<term>                        # e.g., fuel:natural_gas, lifecycle:repower, climate:el_nino
keywords: [<freeform>, <freeform>, ...]       # [validated] non-controlled, for search

# ── Scope (what entities the methodology applies to) ──────────────────────
scope:
  entity_types:                               # [validated]
    - plant | generator | project | region
  fuel_filter: [<EIA fuel codes>]             # [validated] empty = any
  capacity_filter:                            # [validated]
    min_mw: <number | null>
    max_mw: <number | null>
  lifecycle_phase:                            # [validated]
    - operating | construction | queue | retiring
  regions:                                    # [candidate — El Niño force-add]
    - { type: ba_id, values: [...] }          # substrate region types
    - { type: iso_rto, values: [...] }
    - { type: nerc, values: [...] }
    - { type: ensoclimate_region, values: [...] }   # external region types
    - { type: noaa_cpc_region, values: [...] }
    # Each region type declares whether it's substrate-resolvable or external-only.
    # Schema enforces that external-only regions must crosswalk to substrate entities at applied-insight render time.
  actors:                                     # [candidate — gridstatus + decision-grounded discussion]
    # Who reads applied insights produced from this methodology, and what decision are they making?
    # role enum is OPEN — capital-stack actors are common examples, not the universe.
    # Some methodology briefs will produce framings for actors not on this list (researchers, public, etc.).
    - role: insurer | lender | equity | developer | asset_manager | operator | researcher | policy | public | other
      decision_class: <free text — the specific decision this actor is making>
      confidence_floor: low | medium | high      # minimum confidence publishable to this actor
      framing_notes: <optional — how the same methodology output is reframed for this actor>
    # Multiple actor entries are normal — the same methodology often produces different framings
    # for different actors (e.g., insurer reads "tail risk", lender reads "covenant stress",
    # equity reads "long-run cashflow distribution") from one underlying analytical computation.

# ── Substrate inputs (typed pointers — the moat) ──────────────────────────
substrate_inputs:                             # [validated]
  - dim: <dimension_name>                     # e.g., engineering_subsystem, generation, financial, news
    fields: [<field_name>, ...]
    required: <bool>
    aggregation: <none | trailing_n | annual_sum | latest>
    fallback:                                 # optional; what to use if field is null
      source: <fallback_source>
      scenario: <fallback_scenario>

# ── External inputs (non-substrate sources) ───────────────────────────────
# [candidate — El Niño force-add]
external_inputs:
  - source: <source_id>                       # e.g., NOAA_CPC_ENSO, NREL_ATB
    vintage_clock: <weekly | monthly | quarterly | annual | triggered>
    fields: [<field_name>, ...]
    refresh_lag_tolerance: <duration>         # how stale can this be before applied insight should re-run?
    fallback:
      source: <fallback_source>
      treatment: <use_last_known | hold_claim | downgrade_confidence>
    license: <text>                           # provenance + licensing for external data

# ── Analytical procedure (Diátaxis: segmented) ────────────────────────────
procedure:
  reference:                                  # [validated] bare facts — no prose
    outputs:                                  # [candidate — vector, not scalar]
      - name: <output_name>
        unit: <unit>
        sign_convention: <text>
        claim_type:                           # [candidate — El Niño force-add]
          - mechanistic | statistical | scenario_based | correlational
        confidence: <low | medium | high>     # per-output, not per-brief
    horizon: <duration | null>                # [validated]
    discount_rate_default: <number | null>    # if applicable
    temporal_scale:                           # [candidate — El Niño force-add]
      <single_point | multi_year_cycle | seasonal | event_triggered>
      # how the methodology relates to time independent of the snapshot cadence
  
  explanation: |                              # [validated] Diátaxis: the worldview, prose
    <The analytical story. Why does this work? What does this NOT cover?
    Where are the boundaries of the framework? Honest about limits.>

  how_to:                                     # [validated] Diátaxis: executable recipe
    - step: <step_name>
      purpose: <one_line>
      inputs: [<which substrate_inputs or external_inputs feed this step>]
      operation:                              # [candidate — runnable?]
        type: <query | formula | model | external_lookup>
        spec: <SQL template | math | code snippet | API call>
      outputs: [<which procedure.reference.outputs this contributes to>]
      claim_type: <inherits from output, or overrides>

# ── Worked examples (back-edges to applied insights) ──────────────────────
worked_examples:                              # [validated]
  - title: <text>
    applied_insight_slug: <slug>
    entity_filter: <inline filter for clarity>
    notes: <what this example demonstrates about the methodology>

# ── Citation & lineage ────────────────────────────────────────────────────
citation:
  authors:                                    # [validated] team handle v1
    - "InfraSure.ai Research"
  first_published: <date>
  reviewer: <internal_id>                     # internal metadata, not public
  doi: <null | string>
  cite_as: <auto-derived from structured fields>

lineage:                                      # [validated]
  extends: [<other_brief_slug>, ...]
  depends_on: [<other_brief_slug>, ...]
  supersedes: [<other_brief_slug>, ...]
  cites_data:                                 # internal substrate or external data
    - source: <source_id>
      vintage: <text>
      role: <primary | corroborating | parameter>
  cites_external:                             # outside literature
    - type: <paper | dataset | regulation | other>
      title: <text>
      url: <url>
      role: <theoretical_basis | empirical_support | counterpoint>

# ── Validity & staleness ──────────────────────────────────────────────────
validity:                                     # [validated]
  asserted_window:
    start: <date>
    end: <date | null>                        # null = open-ended
  expected_review_cadence:                    # [validated]
    <quarterly | annual | triggered | event_driven>
  staleness_signals:                          # [validated]
    - source: <source_id>
      event: <schema_change | new_edition | revision | structural_change>
    - internal: <named_internal_event>
      severity: <low | medium | high>
  temporal_scale: <field present at procedure.reference; replicated here for query speed>
  confidence:                                 # [validated]
    overall: <low | medium | high>
    per_claim_type:                           # [candidate]
      mechanistic: <low | medium | high>
      statistical: <low | medium | high>
      scenario_based: <low | medium | high>
      correlational: <low | medium | high>
    caveats:                                  # [validated]
      - <explicit prose caveat>

# ── Surfacing (where this brief earns its keep) ───────────────────────────
surfacing:                                    # [validated]
  applies_to_pages:
    - surface: <plant_page | project_page | portfolio_page | region_page | global_index>
      condition: <expression evaluable against entity attributes>
  applied_insights:                           # [validated] computed reverse edge
    - <applied_insight_slug>
```

---

## Companion: how applied insights reference this brief

This is a preview — full spec lives in `03_applied_insight_shape.md` (after this schema stabilizes). The link is:

```yaml
# applied_insight.schema.yml — preview only
kind: applied_insight
slug: <applied_insight_slug>
cadence: periodic | event_triggered           # [candidate — gridstatus + memo discussion]
                                              # periodic = rendered on a schedule from a stable methodology
                                              # event_triggered = fires when a defined event happens
                                              #   (e.g., new LBNL edition, ENSO state change, hurricane path forecast)
target_actor:                                 # [candidate] which actor entry from the methodology brief
                                              # this applied insight is framed for
  role: <role from methodology.scope.actors[].role>
  decision_class: <inherited from methodology.scope.actors[].decision_class>
methodology_refs:                             # MUST point to a brief snapshot, not the live URL
  - brief_slug: <methodology_brief_slug>
    snapshot_id: <YYYY-QN>
    role: <primary | corroborating>
scope:
  # subset of the methodology brief's scope, resolved to concrete entity IDs
  entity_ids: [<resolved at insight build time>]
  region_resolution:                          # how the external regions in the brief's scope were mapped
    - external_type: ensoclimate_region
      external_value: <text>
      resolved_substrate_entities: [<plant_id>, ...]
claims:
  - claim_id: <local_identifier>
    text: <prose claim>
    tuple_refs:                               # the substrate grounding from principle 3
      - { dim: <dim>, entity_id: <id>, column: <col>, value: <value>, vintage: <date> }
    methodology_ref: <which procedure.reference.outputs this implements>
    confidence: <inherited from brief; can be downgraded, never upgraded>
```

---

## What's expected to change (predictions to test)

Drawn from the El Niño stress-test predictions ([`05_first_methodology_brief/README.md`](05_first_methodology_brief/README.md)):

| Schema piece | Current status | Prediction | Resolution path |
|---|---|---|---|
| `procedure.reference.outputs[]` (vs. single `output_metric`) | candidate | Confirms — El Niño has 4-6 outputs in the causal chain | When confirmed, mark validated and update `01_principles.md` if it changes commitment 1's framing |
| `scope.regions[]` with type discrimination (substrate + external) | candidate | Confirms — El Niño needs ENSO climate regions, NOAA CPC regions | Confirm; then audit other dimensions to find sibling external region types |
| `external_inputs[]` (sibling to `substrate_inputs[]`) | candidate | Confirms — NOAA CPC indices, seasonal outlooks | Confirm; document the fallback policy patterns that emerge |
| `procedure.reference.outputs[].claim_type` | candidate | Confirms — mechanistic for irradiance, statistical for demand, correlational for LMP | Confirm; settle the `claim_type` taxonomy (4 values feels right; may compress to 3) |
| `validity.temporal_scale` | candidate | Confirms — multi-year ENSO cycle doesn't fit quarterly snapshot semantics | Confirm; check whether thermal-repower or queue-lifecycle briefs need same field |
| Applied-insight `kind`: stored vs. parameterized | TBD | El Niño forces the call — parameterized template that renders per-plant on demand is the right answer for fan-out methodologies | Lock the decision; update principles commitment 2 if needed |
| `procedure.how_to.operation.type: query` runnability | TBD | Aspirational answer (runnable SQL/Python). El Niño is too complex for runnable-from-day-1; we accept pseudo-code with declared inputs/outputs for v1 | Lock the v1 standard at "structured pseudo-code with typed I/O"; defer fully-runnable to a future principle |
| `surfacing.applies_to_pages.condition` DSL | TBD | El Niño needs a condition language richer than YAML literals (e.g., "plant in scope where current ENSO state ≠ neutral") | Sketch a minimal expression language; defer full design to when we have 3 briefs |
| `scope.actors[]` (open role enum + decision_class + confidence_floor) | candidate | Confirms — El Niño produces different framings for insurer / lender / equity / developer / operator / researcher; same math, different applied-insight renders | Confirm role enum is open; settle whether `confidence_floor` per actor is realistic or premature optimization |
| Applied insight `cadence: periodic \| event_triggered` | candidate | Confirms — El Niño has both periodic (quarterly seasonal-outlook render) and event-triggered (ENSO state change) applied insights | Confirm; document how `validity_window` semantics differ between the two cadences |
| Applied insight `target_actor` (links back to methodology `scope.actors[]`) | candidate | Confirms — distinct applied insights for distinct actors from one methodology | Confirm; settle whether one applied insight can target multiple actors or always exactly one |

---

## Open design tensions (not yet decided)

1. **Snapshot every brief every quarter, even unchanged?** Principle 4 currently says yes. The `snapshots[].changed_from_previous` flag captures the metadata. Storage cost is trivial; citation predictability wins. Confirmed unless someone surfaces an objection.
2. **`claim_type` taxonomy size.** 4 values (mechanistic / statistical / scenario_based / correlational) feels right. Could compress correlational into statistical (correlation is just a kind of statistical inference). El Niño's LMP claims are the test case — they're correlational with mechanistic substrate, which is a hard typing call. Defer until we author them.
3. **External-region crosswalk: build time vs. query time?** When an applied insight cites a brief scoped to `ensoclimate_region: North_American_Monsoon`, do we resolve to plant_ids at insight build time (denormalized, fast) or query time (always current, slow)? My lean: build time for the canonical applied-insight render, query time for ad-hoc filters. Worth a separate small spec.
4. **Versioning of the schema itself.** This document is `v0`. When the El Niño brief forces the candidate fields to validated, we go to `v1`. When a brief forces a breaking structural change (e.g., claim shape rethought), we go to `v2`. The schema's own version lives in a header in each brief file (`methodology_brief_schema_version: v1`) so old briefs can be migrated mechanically.
5. **The relationship to `the_ontology/grounding/`.** The Signal ontology already has `event_type`, `risk_factors`, etc. Our methodology brief schema overlaps these in spots (`topics`, some `claim_type` values). When does a methodology brief defer to the ontology? When does it extend it? Open question; probably resolved by treating the ontology as a controlled vocabulary that briefs reference, not duplicate.
6. **Analytical coherence with the platform's other model outputs.** When an applied insight cites e.g. "plant 3470 expected annual loss" or "ERCOT capacity payment forecast" or "CAISO solar capacity factor distribution", that quantity may also exist as an output of the platform's hazard / financial / generation modeling layer. If the insight cites a value that differs from what the platform itself displays elsewhere for that same plant + same time window, the system is incoherent — exactly the failure mode the architecture exists to prevent. Open question: should the agent's substrate retrieval tools have read access to platform-modeling-layer active outputs (not just raw substrate), and refuse to ship an insight whose claimed quantity disagrees with the platform's existing model output for that quantity? My lean: yes, but this is a `04_agent_architecture.md` design call; flagging here so it doesn't get lost.

---

## How this schema gets revised

Same process as the principles file:
1. **Author into the current schema** — if it doesn't fit, log the friction in the relevant brief's `what_we_learned.md`.
2. **Argue the change** when one is needed. Always from a concrete failure case (a real brief couldn't be written), never from "this would be cleaner."
3. **Decide.** User has final call on breaking changes; analyst can ship semver-minor additions with explanation.
4. **Migrate** existing briefs mechanically if a breaking change ships. Schema version field on every brief makes this trivial.

The first major test arrives when the El Niño brief is authored end-to-end. Expect the candidate fields above to either land as validated or get redesigned. Either outcome is success — the point of the crucible is to force the schema to face real content.
