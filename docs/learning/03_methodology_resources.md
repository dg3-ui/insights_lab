# 03 - Methodology Resources

> **Purpose**: explain what a contributor is actually building — a *control surface* for analysis — its required parts, and how it reads end-to-end, traced against the real ENSO resource and live data.
>
> **Grounded in**: `resources/weather_and_climate/el_nino_enso/` + live MCP output, 2026-06-05. The canonical field standard is `docs/03_methodology_resource_standard.md`; this doc teaches it.

## What A Methodology Resource Does

A methodology resource tells the model, for one analytical question:

- what question it may answer (and what it may not)
- what data to retrieve, and from where
- which reasoning steps to follow, in order
- which claims are allowed, and which are blocked
- when to downgrade confidence
- which caveats must always appear
- who the result is for

```text
It is NOT an essay about a topic.
It IS a control surface that constrains how the model reasons and what it may assert.
```

The difference matters: an essay makes the model *fluent*; a resource makes the model *disciplined and auditable*. V0 is a bet that discipline — not fluency — is what turns InfraSure data into defensible intelligence.

## Three Forms Of One Resource

Each resource exists in three coupled forms. They are not duplicates; they are projections of the same method at different altitudes:

```text
resource.md          resource.yml             prompt_projection.md
(human canon)         (machine-structured)     (session-strict subset)
- full reasoning      - enforceable fields      - what Claude sees in a test
- the "why"           - identity, scope,        - role + task + rules + format
- review reference      inputs, claims, conf.   - no background prose
        \                    |                        /
         \                   |                       /
          ----> one method, audited at the altitude each reader needs
```

`resource.md` is what a reviewer reads. `resource.yml` is what a future engine enforces. `prompt_projection.md` is what runs in the manual test (taught in `04_prompt_projection.md`).

## The Resource Contract

Every resource must define these fields. Learn *why each exists* — the "why" is what stops the model from drifting:

| Field | What it pins down | Why it exists |
|---|---|---|
| `identity` | slug, version, status, review date | makes the method citable + versionable |
| `question_grammar` | the exact questions allowed / blocked | stops scope creep into commentary |
| `scope` | entity types, fuels, regions, lifecycle, actors | bounds the fan-out |
| `substrate_inputs` | InfraSure fields that ground claims | forces grounding, not memory |
| `external_inputs` | non-platform causal state (e.g. NOAA ENSO) | names what the substrate can't supply |
| `descriptive_context` | framing-only inputs | quarantines "sounds-true" prose |
| `actor_context` | owner / offtaker / investor | routes the insight without distorting it |
| `procedure` | ordered reasoning steps | makes the path reproducible + reviewable |
| `allowed_claims` | claim types permitted | the ceiling on assertion |
| `blocked_claims` | claims forbidden | the explicit floor — the most valuable field |
| `confidence_rules` | when to keep / downgrade / block | conservative by construction |
| `caveats` | mandatory caveats per claim type | uncertainty is never silent |
| `actor_relevance` | who cares + which rendering | feeds activation later, after validation |
| `staleness_signals` | what forces a re-review | keeps the method honest over time |

`blocked_claims` does the heaviest lifting. A resource with vague "allowed" language but sharp "blocked" language still produces safe output; the reverse does not.

## The Claim Grammar

Every material claim a resource emits must decompose into seven slots:

```text
condition + scoped entity set + mechanism + evidence + confidence + caveat + actor relevance
```

Filled with **real** values from the live CA-solar query (2026-06-05):

```yaml
condition:   "Forecast / current ENSO state per the external source used in the test"
scope:       "Operating CA solar >= 50 MW — e.g. Topaz Solar Farm (57695, 585.9 MW),
              Desert Sunlight 300 (57993, 313.7 MW), Darden I–IV (646.4 MW each)"
mechanism:   "ENSO-associated winter cloud/precipitation tendency may shift seasonal irradiance"
evidence:
  external:  "NOAA CPC ENSO status / ONI  (name + vintage, supplied in test)"
  substrate: "get_plant.generation monthly CF (summer ~0.38 / winter ~0.13);
              capacity, lat/lon, regions.iso_rto=CAISO"
confidence:  low            # external-forecast-dependent + regional teleconnection is noisy
caveat:      "Directional exposure only; not a plant-level production or LMP forecast"
actor_relevance: "Owners (Clearway, BHE, Intersect) + offtaker PG&E should monitor
                  seasonal generation variance and revenue sensitivity"
```

Every slot points to something retrievable or to a named external source. A slot you cannot fill is a confidence downgrade — or a `blocked` claim.

## Worked Walkthrough — The ENSO Resource End To End

How a contributor actually traces the resource against the tools:

```text
1. question_grammar  -> "which CA solar assets are directionally exposed to ENSO?"  (allowed)
                        NOT "what LMP will ENSO cause?"                              (blocked)

2. external_inputs   -> fetch NOAA CPC ENSO state + vintage   (the methodology's job, not the substrate's)

3. scope + substrate -> search_plants(fuel="solar", state="CA", minMw=50)
                        ⚠ NOT iso="CAISO" — that filter returns [] (see 01_mcp_basics, live gap)

4. drill             -> get_plant(57993) for capacity, regions.iso_rto, generation CF, owner, offtaker

5. procedure         -> state mechanism + claim type (directional, not causal)
                        filter to material operating assets
                        attach owner/offtaker for actor relevance

6. claim grammar     -> assemble the 7 slots above

7. confidence + block-> downgrade to LOW (external forecast dependence)
                        BLOCK any exact LMP or plant-level output number
```

The walkthrough is the resource doing its job: at step 3 it catches a tool gap, at step 7 it refuses an overclaim. Both are the control surface working.

## V0 Quality Bar

A v0 resource passes when a reviewer can answer all of these from the resource alone:

```text
[ ] What is the exact question? (and the exact non-questions?)
[ ] What input data is needed — and is each labeled substrate / external / descriptive / actor?
[ ] What is the mechanism, and is its claim type named (directional / statistical / causal)?
[ ] What may the model claim?
[ ] What must the model NOT claim?
[ ] What confidence applies, and is it conservative (no upgrade past the weakest input)?
[ ] Which caveats are mandatory?
[ ] Who should care, and via which rendering?
```

If any box is unanswerable, the resource is not done — regardless of how well it reads.

## How This Scales Past V0

The resource is the seed of the production architecture, not a throwaway:

```text
v0 resource.yml  ->  retrieval planner   (which tools, in what order — step 3 above)
                 ->  validation gates     (confidence_rules + blocked_claims, enforced)
                 ->  trace capture        (the 7 slots become a stored insight object)
                 ->  tool roadmap         (every logged tool gap → a new MCP capability)
```

So writing a tight resource now is also writing the spec for what the platform retrieves, refuses, and grows into later. The methodology leads; the engine and the expanding MCP surface follow.

---

**Next**: `04_prompt_projection.md` — how the resource collapses into the strict, pasteable surface the model sees in a test.
