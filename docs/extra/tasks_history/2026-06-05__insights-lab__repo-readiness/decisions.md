# Decisions - InfraSure Insights Repo Readiness

## 1. Use Current Lab As The Staging Repo

### Decision

Refactor `.lab/insights_lab` directly into the clean staging structure instead of creating a separate standalone repo immediately.

### Rationale

The current lab already held the useful context and could become repo-ready with a controlled cleanup. This avoids splitting the work across two locations before the team handoff structure is stable.

## 2. Keep The Top-Level Structure Minimal

### Decision

Use only these live top-level folders:

```text
docs/
resources/
templates/
archive/
```

### Rationale

The repo should scale later into `code/`, `scripts/`, and `data/` only when actual implementation work exists. Creating those folders now would imply a build scope that v0 explicitly rejects.

## 3. Put Learning Under `docs/learning/`

### Decision

Learning material lives under `docs/learning/`, not as a top-level `learning/` folder.

### Rationale

The user wanted learning to be visible but not compete with future implementation folders. Keeping it under docs preserves the top-level structure for actual product/build surfaces.

## 4. Make V0 MCP-Ready, Not MCP-Integrated

### Decision

V0 creates a prompt projection and manual MCP/Claude test protocol. It does not build direct MCP integration, new MCP tools, a production agent, or an API orchestrator.

### Rationale

The first risk is methodology quality and tool-use discipline, not software architecture. Manual MCP/Claude testing is enough to validate whether the resource format can guide grounded insight production.

## 5. Treat ENSO Exposure As The First Resource

### Decision

The first resource remains:

```text
El Nino / ENSO exposure
  -> renewable assets
  -> one region or market
  -> actor relevance
```

### Rationale

ENSO forces the system to handle external inputs, region crosswalks, asset fan-out, confidence downgrades, and actor relevance. It is a strong test without requiring full production infrastructure.

## 6. Archive Instead Of Deleting Exploratory Material

### Decision

Old research, methodology-registry drafts, and first-brief scaffolds were moved into `archive/`.

### Rationale

The thinking remains valuable, but it should not distract a junior contributor from the execution path. Archive keeps the history available without making it part of the active read order.

