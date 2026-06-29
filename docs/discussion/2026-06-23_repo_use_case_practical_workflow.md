# Discussion — Repo use case + practical workflow

> **Status**: **RECOVERED**, opened 2026-06-23 — regenerated from the archived Codex thread titled `Explain repo use case` (`019ef55c-9f5b-70e2-a5e5-aca041cc9e85`). This is a recap/discussion note, not canon by itself.

## 1 · What this repo is for

This repo is the **InfraSure analyst methodology layer**. It is not the app, data pipeline, or data warehouse. The InfraSure substrate already exists through MCP/data tools; this repo tells an LLM **how to reason over that data** so the output becomes a grounded infrastructure insight instead of generic energy commentary.

For bottom-up use cases, the starting point is a **client, portfolio, asset, region, or account**:

```text
For this specific portfolio, what exposure, risk, opportunity, or constraint
should the owner / investor / lender / offtaker care about?
```

The moat is:

```text
InfraSure data       = what is true
methodology package = how to reason
human gate          = what is responsible to claim
render layer        = how to communicate it
```

## 2 · Bottom-up flow

```text
CLIENT / PORTFOLIO / ASSET
          |
          v
resolve the actual entities
plants · projects · owners · offtakers · regions
          |
          v
choose / load methodology
ENSO · hail · heat · hurricane wind · offtaker concentration · etc.
          |
          v
retrieve before drafting
InfraSure MCP data + dated external source where needed
          |
          v
assemble applied insight
condition + scope + mechanism + evidence + confidence + caveat + actor relevance
          |
          v
GATE
allowed claims? blocked claims? confidence capped? caveats present?
          |
     +----+----+
     |         |
  blocked   validated
     |         |
     v         v
 no render   report / email / platform note
             optional studio pass for high-value pieces
```

The product is usually not the first answer. The valuable output is the refined, gated read after entity resolution, evidence checks, caveats, and actor relevance are forced into the claim.

## 3 · Practical workflow with MCP connected

```text
1. Pick the use case
   "Analyze this client / portfolio / site against this phenomenon."

2. Pick the methodology resource
   e.g. el_nino_enso, hail_solar, extreme_heat_derate,
   hurricane_high_wind_wind, offtaker_concentration.

3. Load the method into the MCP-enabled LLM
   resource prompt_projection.md
   + resource.yml / data_requirements.md as needed
   + resources/_principles/ for rubric + voice.

4. Retrieve before drafting
   Resolve assets, owners, offtakers, locations, capacity, etc.
   Use MCP tools first. Add dated external sources only where needed.

5. Draft the applied insight
   claim + scope + mechanism + evidence + confidence + caveat + actor relevance.

6. Gate it
   Check blocked_claims, confidence cap, source_refs, as_of dates, caveats.
   Iterate until it is defensible.

7. Save the transcript / resolve the run
   The raw chat is process data.
   The resolved output becomes a test_run or applied-insight artifact.

8. Render only after the gate
   /render <gated-insight-path> report docx client
   or
   /render studio/<subject>/<phenomenon>.md report html
```

## 4 · Where `/render` and references fit

`/render` is **not** the first step. It is the **post-gate** step. It should consume a validated applied insight or a studio brief that was built from one.

```text
BASELINE PATH
  gated test_run / applied insight
        |
        v
  /render -> blog / report / email

STUDIO PATH
  gated insight
        |
        v
  studio/<subject>/<phenomenon>.md brief
        |
        v
  /render -> higher-polish blog / report / email
```

Files in `resources/_reference/`, including `resources/_reference/internal/blog/enso_ca_solar_2026-06.md`, are **form exemplars**, not grounding. They can guide shape, voice, structure, and polish. Their numbers must be re-grounded live before use.

```text
wrong:
  open _reference/internal/blog/enso_ca_solar_2026-06.md
  -> treat it as factual input
  -> render from it directly

right:
  use that file as a form reference only
  -> re-fetch live MCP numbers
  -> build/gate the new insight
  -> then render
```

## 5 · Example bottom-up shape

```text
Subject:
  Brookfield / Standard Solar portfolio

Question:
  Is this portfolio materially exposed to El Nino, hail, extreme heat, etc.?

Method:
  load the relevant resource package

Grounding:
  resolve plants, capacity, geography, owner/offtaker context, hazard/weather overlap

Insight:
  "This portfolio is more / less exposed than the naive assumption,
   because the actual asset distribution shows X."

Output:
  internal read first
  then client report or email subset
```

## 6 · Working rule

The order is:

```text
specific client / portfolio context
  -> methodology package
  -> MCP retrieval
  -> gated insight
  -> optional studio brief
  -> render
```

Not:

```text
reference artifact
  -> pretty output
  -> retrofitted grounding
```

The core use case is to turn specific infrastructure context into **grounded, caveated, client-relevant decision intelligence**. Not content first. Not outreach first. Insight first, gate second, render third.

---

**See also**: `README.md` (what a discussion is) · `2026-06-14_bottom_up_output_workshop.md` (bottom-up output + studio lane) · `../architecture.md` (layers and gate) · `../process/commands.md` (`/render` design) · `../process/test_protocol.md` (manual loop) · `../../resources/_reference/internal/blog/enso_ca_solar_2026-06.md` (form exemplar, not grounding) · `../../resources/weather_and_climate/el_nino_enso/` (validated resource package).
