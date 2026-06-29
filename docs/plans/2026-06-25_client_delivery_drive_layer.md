# Plan — Client Delivery Drive Layer

> **Status**: IN PROGRESS, opened 2026-06-25. Build the business-development handoff layer described in `../client_delivery_flow.md`: Google Drive taxonomy, sheet-separated client profile shape, agent-created profile process, and Drive-promotion QA. `.research_lab` is linked as the starting profile-generation reference, the customer tracker is staged under `../client_delivery/_inputs/`, and AIG Project Finance Group is the first pilot; still blocked on the external deep-research output and final Drive naming details.
>
> **Why now**: the lab can already create methodology-backed insights and render client-ready artifacts. The missing operational layer is where those artifacts live for senior-led business development and how client context shapes what gets created.

## 1. Decision

```text
client-centric   bottom-up, client/account anchored
climate-centric  top-down, phenomenon/signal anchored
```

The Drive layer is the delivery handoff. It does not replace the repo, studio, source refs, or the human gate.

## 2. Phase Ladder

| # | Phase | Deliverable | Status |
|---|---|---|---|
| 0 | Inputs | client Excel + `.research_lab` / profile-generation reference mapped | done |
| 1 | Taxonomy | local client-delivery workspace + final Drive naming convention | in progress |
| 2 | Profile Contract | deep `Client Profile` schema: team-curated + agent-created + strategy views | in progress |
| 3 | Pilot | one client folder populated with profile + one collateral lane | in progress |
| 4 | QA Gate | Drive-promotion checklist for reports, vlogs, presentations, emails | queued |
| 5 | Scale | repeatable process for remaining target clients and climate folders | queued |

## 3. Phase Details

### Phase 0 — Inputs

Received locally:

```text
client profile Excel / workbook
.research_lab profile-generation reference
```

Still needed from owner:

```text
any additional cross-reference folder or system beyond `.research_lab`
target Google Drive parent folder
preferred client-folder naming convention
```

Acceptance: inputs are available locally or described well enough to map without guessing.

Current known reference:

```text
.research_lab -> /Users/divy/code/personal/renewablesinfo_com/research_lab
../client_delivery/_inputs/InfraSure-Customer-Tracker.xlsx
```

Use it narrowly for the customer-profile lane: company/entity profiles, team input, `/profile` process, PMF synthesis outputs, and the decision-to-artifact diagnostic. Do not pull the full research lab into this repo's operating model.

### Phase 1 — Taxonomy

Settle the Drive structure:

```text
InfraSure sites/
  client-centric/<client_name>/
  climate-centric/<phenomenon>/
```

Decide whether client folders include only senior-ready artifacts or whether they also carry `draft/` and `approved/` subfolders. Default recommendation: Drive is senior-ready; drafts stay in repo/studio until promoted.

Acceptance: the folder contract can be followed by another contributor without asking where an artifact belongs.

Local workspace now exists:

```text
../client_delivery/
  _inputs/
  clients/
  process/
```

Remaining Phase-1 decision: final Drive naming convention and whether Drive holds only approved material or also a visible `draft/` lane. Default remains: Drive is senior-ready; drafts stay in repo/studio until promoted.

### Phase 2 — Profile Contract

Define the `Client Profile` artifact:

```text
team-curated profile:
  category, follow-up, core fit, use case, pitch angle, product readiness,
  blocking features, stage, owner, contacts, next step, notes

agent-created profile:
  public company intelligence only: company map, verticals, product/service lines,
  asset/geography surface, counterparties, workflows, public team map,
  latest updates, evidence ledger, intelligence gaps

strategy / opportunity sheet:
  combines team-curated relationship context + agent-created profile + product
  readiness into account strategy, collateral direction, and next action
```

Seed the agent-created view from the research-lab profile method. Do not adapt it into pitch language inside the profile:

```text
research lab       broad entity / market / competitor profile style
client delivery    public agent-created profile sheet
strategy sheet     later internal synthesis and collateral routing
```

Acceptance: profile fields are complete enough to understand the entity without importing team relationship assumptions, and every generated field has review status.

Profile artifacts landed:

```text
../client_delivery/clients/_template/client_profile.md
../client_delivery/process/deep_client_research_playbook.md
```

Remaining Phase-2 work: fill the template with the first pilot client and check whether any tracker fields need to become required profile fields.

### Phase 3 — Pilot

Populate one client folder end to end:

```text
client profile
one gated/rendered artifact
one senior-ready email template or notes file
QA checklist applied
owner / next-step recorded
```

Acceptance: a senior can open the folder and understand the client, the fit, the collateral, and the next action without reading this repo.

Pilot started:

```text
../client_delivery/clients/aig_project_finance_group/
  client_profile.md
  deep_research_prompt.md
```

This pilot deliberately starts with a prompt pack. The first test is whether a web-enabled deep-research run can produce a DOCX-quality **agent-created AIG profile** without collapsing into a shallow company summary or an account-strategy memo.

### Phase 4 — QA Gate

Codify the promotion checklist from `../client_delivery_flow.md`:

```text
insight gate passed
numbers re-grounded
audience strip applied
design QA passed
client profile checked
senior owner named
no send automation
```

Acceptance: no artifact enters Drive unless it is suitable for direct senior review and possible client use.

### Phase 5 — Scale

Apply the structure across the active target list and start climate-centric folders for reusable top-down materials.

Acceptance: target clients have folders, profiles are initialized, and climate-centric material can be linked into client-specific follow-ups.

## 4. Scope Guards

```text
1. Drive is the handoff layer, not the claim source.
2. Client profile context routes and frames; it does not ground material claims.
3. Agent-curated profiles are reviewed aids, not authoritative relationship truth.
4. Anything client/public-facing is re-grounded and audience-stripped before Drive promotion.
5. Actual outreach remains senior-owned and human-in-the-loop.
6. Do not build a Drive automation or CRM integration until the manual taxonomy works.
```

---

**See also**: `../client_delivery_flow.md` (canon flow) · `../client_delivery/README.md` (local workspace) · `../client_delivery/process/deep_client_research_playbook.md` (deep profile process) · `../use_cases.md` (bottom-up/top-down and activation boundary) · `../../studio/README.md` (render briefs) · `../process/commands.md` (`/render`) · `../status/mcp_gaps.md` (platform gaps that may block collateral quality).
