# Client Delivery Flow

> **Status**: v0 canon, opened 2026-06-25. The business-development handoff layer that sits after a gated InfraSure insight and its render. This document defines the Google Drive operating model, the client-profile role, and the quality bar for anything that becomes senior/customer-ready collateral.
>
> **Purpose**: close the missing layer between `insights_lab` output and senior-led client communication. The repo creates grounded insights and rendered artifacts; the business-development layer organizes those artifacts by client or climate signal so the senior team can use them without reconstructing context.

## 1. What This Adds

The existing lab flow ends at a gated insight or rendered artifact. The missing operational layer is the business-development handoff:

```text
methodology package + MCP retrieval
        |
        v
gated insight
        |
        v
/render or studio brief
        |
        v
client-readiness QA
        |
        v
Google Drive handoff
        |
        v
senior-owned client communication
```

This is **not** a new source of truth for claims. It is the delivery surface where a finished, reviewed artifact is organized against a client, phenomenon, contact owner, and next step.

```text
repo / studio     working source, methodology, test records, render drafts
Google Drive      senior-ready collateral and business-development context
CRM / senior team live relationship state, contact judgment, send decision
```

## 2. The Drive Shape

The Drive home is planned under the business-development channel:

```text
InfraSure sites/
  client-centric/          bottom-up: account, client, portfolio, site
    <client_name>/
      Client Profile       team-curated + agent-created + strategy sheets
      vlogs/
      reports/
      presentations/
      email_templates
  climate-centric/         top-down: driver, phenomenon, market signal
    enso/
    hail/
    extreme_heat/
    hurricane_high_wind/
    ...
```

**Client-centric** is bottom-up. The anchor is a named company, portfolio, account, site, lender, investor, or offtaker. The question is: what should this specific relationship care about, and what collateral would help a senior conversation?

**Climate-centric** is top-down. The anchor is a climate/weather/hazard/commercial signal. The question is: what does this phenomenon affect, which clients should hear about it, and which bottom-up drills should it trigger?

## 3. Client Folder Contract

Each client folder should start with one `Client Profile` artifact. The final file type can be a Google Sheet / Excel workbook or a Google Doc, but it must preserve distinct views:

| View | Owner | Job | Status |
|---|---|---|---|
| **Team-curated profile** | senior / BD team | relationship truth: category, fit, stage, owner, contacts, next step | authoritative for outreach context |
| **Agent-created profile** | research workflow | public company intelligence: structure, business lines, products, assets, workflows, counterparties, latest updates, evidence gaps | generated aid, reviewed before use |
| **Strategy / opportunity sheet** | internal synthesis owner | combines team context + agent profile + product reality into account strategy and collateral direction | downstream; not part of public profile |

The team-curated profile should carry fields such as:

```text
customer category
follow-up schedule
core fit
primary use case
pitch angle
product readiness
blocking features
stage
business owner
key contacts
next step
notes / relationship context
```

The agent-created profile has a different job. It is broader, more research-heavy, and public-source-based: company map, business verticals, products, assets, counterparties, workflows, leadership, latest updates, peer set, evidence ledger, and intelligence gaps. It must **not** include pitch angle, product readiness, blockers, owner, next step, NDA status, outreach copy, or "how InfraSure helps." Those belong in the separate strategy / opportunity sheet.

The local working area for turning the tracker into deep profiles is `client_delivery/`:

```text
client_delivery/_inputs/      local tracker workbooks; ignored by git
client_delivery/clients/      one folder per selected client
client_delivery/process/      deep profile playbook and checklist
```

The current tracker is `client_delivery/_inputs/InfraSure-Customer-Tracker.xlsx`. It contains the active customer pipeline, demo schedule, roadmap blockers, partnerships, old pipeline context, and dropdown lists. It is an intake source, not a grounding source.

### Research lab reference

The local symlink `.research_lab` points to `/Users/divy/code/personal/renewablesinfo_com/research_lab`. That project is broader than this repo: it covers market research, competitors, product-opportunity discovery, contracts, risks, and PMF synthesis. For this client-delivery lane, use only the pieces that help create the **agent-created profile** first. The decision-to-artifact bridge is a later strategy step.

Useful subsets:

```text
.research_lab/00_engine.md
.research_lab/02_workflow_command_index.md
.research_lab/team_input/
.research_lab/us_power_market_workflow_research/company_profiles/
.research_lab/product_opportunity_maps/candidates/
```

Historical material can also be used as a diagnostic when it helps answer: what entity is this, what does it do, which workflows does it run, and what has changed? Treat that as scaffolding, not final truth.

Do not import the research lab wholesale. It is a reference and profile-generation aid. Anything that becomes client-facing still needs the InfraSure insight gate, current sources, audience stripping, and senior review.

## 4. What Can Enter Drive

Drive is not the scratchpad. It is the senior-ready handoff layer.

Before an artifact enters a client folder or climate folder, it must pass this bar:

```text
1. Insight gate passed: source_refs, caveats, blocked_claims, confidence posture.
2. Numbers re-grounded: live MCP / external state refreshed and as_of recorded.
3. Audience strip done: no internal tags, cap grade, materiality band, triage verdict, or method-talk on a client/public face.
4. Design QA done: figures, captions, sources, pagination, visual connectedness, no text-only report when visuals are called for.
5. Client context checked: profile fit, pitch angle, stage, owner, next step.
6. Senior owner named: a human owns whether and how it is used.
```

This rule is intentionally stricter than "rendered." A rendered file can still be wrong for Drive if it is internally framed, stale, visually unfinished, or not matched to the client context.

## 5. Repo vs Drive Boundary

The repo remains the source for methodology and process:

```text
resources/       how to reason by driver x mechanism
test_runs/       validation records
docs/status/     MCP gaps and build state
studio/          selective render briefs and home-run working artifacts
docs/learning/   process lessons
```

Drive is the business-development delivery surface:

```text
client profile       relationship and fit context
client collateral    reports, vlogs, presentations, email templates
climate collateral   top-down assets reusable across clients
senior handoff       what to use, with whom, and next action
```

Client profile material can **route** and **frame** a deliverable. It does not **ground** an infrastructure claim. If an output says a client owns a plant, has a PPA, faces hail exposure, or should care about a risk, that claim still needs InfraSure substrate, named external sources, or a documented missing-input downgrade.

## 6. Operating Loop

### Bottom-up: client-centric

```text
senior team profile
  -> choose target client / relationship need
  -> agent-created profile adds public company intelligence
  -> separate strategy sheet combines public profile + relationship context
  -> select resources / recipes
  -> retrieve before drafting
  -> gate insight
  -> render report / vlog / email template
  -> client-readiness QA
  -> place in client-centric/<client_name>/
  -> senior-owned follow-up
```

### Top-down: climate-centric

```text
climate / hazard / commercial signal
  -> choose methodology resource
  -> top-down scan
  -> gated market / phenomenon read
  -> render climate-centric artifact
  -> identify affected clients
  -> create bottom-up client adaptations where useful
  -> senior-owned follow-up
```

The two folders should feed each other. A climate-centric ENSO piece can identify candidate clients; a client-centric Brookfield / Standard Solar read can later improve the general ENSO playbook.

## 7. Quality Standard

The quality bar is deliberately high because the folder is meant to reduce senior-team friction, not create another review burden:

```text
no hidden internal labels
no stale substrate numbers
no unsupported claims
no over-precise model-free dollars / MWh / losses
no unreviewed agent assumptions
no rough design artifacts
no orphaned page tails or split figures in paginated exports
no generic collateral where a client profile should have shaped the angle
```

The target state is simple: a senior should be able to open a client folder, understand the relationship context, find the most relevant collateral, and decide whether to send or adapt it without reverse-engineering the analysis.

## 8. Open Inputs

The local input baseline is now available. Remaining setup inputs:

```text
received:
  client-profile Excel / workbook
  .research_lab profile-generation reference

still needed:
  agreed Drive naming convention for client folders
  first pilot client folder
  final QA checklist for Drive promotion
```

Those build steps are tracked in `plans/2026-06-25_client_delivery_drive_layer.md`.

---

**See also**: `architecture.md` (methodology to output stack) · `client_delivery/README.md` (local client-delivery workspace) · `client_delivery/process/deep_client_research_playbook.md` (deep profile process) · `use_cases.md` (bottom-up/top-down and activation boundary) · `principles.md` P2/P7/P8 (content downstream, posture, value-forward close) · `../studio/README.md` (selective output lane) · `resources/_style/output_contracts.md` (blog/report/email envelopes) · `resources/_principles/voice.md` (client-facing register) · `plans/2026-06-25_client_delivery_drive_layer.md` (next build steps).
