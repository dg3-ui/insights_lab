# Plan — Docs Reorganization: purpose-folders along the P1 seam

> **Status**: **DONE** 2026-06-14 — every old→new move in §2 landed; the docs are in their new homes (`method/`, `process/`, `status/`, `architecture.md`, `principles.md`, `use_cases.md`). Opened 2026-06-13, branch `docs-reorg`. Archived to `done/`.
>
> **Owner**: Divy. **Why**: the docs are Divy's communication channel with the agent; the flat `00–11` sequence mixed stable canon with volatile roadmap, buried the architecture, and triplicated three "roadmaps." Decisions confirmed 2026-06-13 (purpose-folders · reorg + cheap corrections · architecture doc as front door).
>
> **Grounded in**: a 15-reader docs-cartography sweep (2026-06-13) — overlap matrix, stable/volatile classification, three-roadmaps diagnosis.
>
> **Scope (confirmed)**: structure + cheap corrections only. The Friday 2026-06-12 meeting minutes are an **external reference, not canon** — their specifics (positioning, competitor framing, backcast/forecast, multi-phenomenon, delivery ordering) are **not** embedded by this reorg and will be used only when the owner directs (owner correction, 2026-06-13: an earlier pass over-embedded them; that content was stripped back out).

## 1 · Target Tree (folder = job; canon vs volatile = folder boundary)

```text
docs/
├── README.md            index + per-audience read order (the only navigational front matter)
├── architecture.md      THE overview / front door — Mermaid + ASCII; absorbs 00 + 06 canon
├── principles.md        the P1–P5 + Rules A–D canon (was 08; promoted, sole owner of the discipline)
├── method/              the "how to reason & build" contract
│   ├── analysis_families.md   (was 02)
│   ├── resource_standard.md   (was 03)
│   ├── data_map.md            (was 04; sole owner of source_ref shape)
│   └── discovery_spec.md      (was 07)
├── process/             the operating loop
│   ├── test_protocol.md       (was 05)
│   └── commands.md            (was 10, the Lifecycle + Design Rule canon half)
├── use_cases.md         the bucket × audience canon (was 11 + the canon half of 01)
├── status/              THE volatile hub (the three roadmaps, detangled, co-located)
│   ├── capabilities.md        (was 06 §11 Build Status + §13 Open Decisions + 00 §5 / 01 status ladder)
│   ├── mcp_gaps.md            (was 09, unchanged in form)
│   └── commands.md            (was 10 Registry table; reconciled to the filesystem)
├── plans/               working plans (unchanged convention)
└── learning/            01–04 fundamentals (session logs relocated out → learning/logs stays but is not "fundamentals")
```

## 2 · File Map (old → new) + cross-ref targets

| Old (numbered) | New | Notes |
|---|---|---|
| `00_project_brief` | → `architecture.md` (+ panorama framing) | merged; the moat *panorama* lands here, moat-as-*discipline* stays in `principles.md` |
| `01_scope_v0` | → `use_cases.md` (canon) + `status/capabilities.md` (status ladder) | split; the "do not build" V0 boundary → a Scope section in `use_cases.md` |
| `02_analysis_catalog` | → `method/analysis_families.md` | move + retitle |
| `03_methodology_resource_standard` | → `method/resource_standard.md` | move; `source_ref` shape → point to `data_map.md` |
| `04_context_and_data_map` | → `method/data_map.md` | move; sole owner of `source_ref` |
| `05_mcp_test_protocol` | → `process/test_protocol.md` | move |
| `06_architecture` | → `architecture.md` (canon §§1-6,9) + `status/capabilities.md` (§11/§13) | merged/split; §7/§8 → point to `method/discovery_spec.md` |
| `07_discovery_spec` | → `method/discovery_spec.md` | move |
| `08_design_principles` | → `principles.md` | move + promote (P-numbers stay stable) |
| `09_mcp_roadmap` | → `status/mcp_gaps.md` | move (form unchanged) |
| `10_command_roadmap` | → `process/commands.md` (canon) + `status/commands.md` (registry) | split |
| `11_use_cases` | → `use_cases.md` | merged with 01's canon |

**Cross-ref rewrite (deterministic, applied to all `*.md` EXCEPT `archive/` + `docs/extra/tasks_history/`)**: full-path `docs/NN_*.md` and shorthand `` `NN` `` forms map per the table above. Section-number refs (`06 §9`, `06 §13`) become semantic (`architecture.md` gate · `status/capabilities.md` open decisions) since section numbers change. P-numbers (`principles.md P2`) are stable. Frozen historical records (`archive/`, `tasks_history/`) are **not** rewritten.

## 3 · Single-Owner Decisions (point, don't restate)

| Topic | Sole owner | Everyone else |
|---|---|---|
| moat-as-discipline | `principles.md` | one-line + link |
| moat panorama | `architecture.md` §thesis | — |
| 4-layer diagram | `architecture.md` | link (was re-drawn in 4 places) |
| P1–P5 principles | `principles.md` | cite `P#` inline |
| `source_ref` shape | `method/data_map.md` | `resource_standard.md` points |
| discovery contract | `method/discovery_spec.md` | `architecture.md` 1-para pointer |
| output matrix (blog/brief/email/post) | `resources/_style/output_contracts.md` | all docs point; **no doc enumerates formats** |
| underscore-folder rule | `resources/README.md` | child READMEs + `discovery_spec.md` point |
| substrate scale / 12-tool count | `learning/02` + `learning/01` | others link (stop hard-coding counts) |

## 4 · Cheap Corrections (in scope)

- **Output model + build-vs-delivery order** (owner direction, 2026-06-13): the three outputs are **blog · report · email** — blog = top-down/generic, report = the same format scoped to a specific portfolio/client/region/purpose (blog↔report overlap in nature), email = a condensed subset of either. (No "vlog" — that was a loose thread term, dropped.) **BUILD order = blog/report first, email last** (the rich pair anchors the feedback loop; you can't judge insight-richness from a terse email). **DELIVERY order** (which output ships when, to whom) is a separate, unsettled business question, NOT the build order. Owned **once** in `_style/output_contracts.md` §1, with `architecture.md`, `use_cases.md`, `status/capabilities.md` pointing there.
- **Relocate** the two `2026-06-12_*` session logs so they aren't read as fundamentals (stay under `learning/logs/`, but `learning/README` frames logs as session records, not the learning track).
- **Date-sync** the front door to 2026-06-13 and link the active plans.
- **Reconcile** `status/commands.md` to the filesystem (`/recap` marked built but absent; `/test-resource`+`/extract` exist).

## 5 · The Friday meeting minutes are a reference, not canon

The 2026-06-12 minutes were given as an **initial reference to return to later**, not as approved content. An earlier pass wrongly embedded their specifics across the docs; that was **stripped back out** on owner direction (2026-06-13). The minutes remain an external input the owner will direct us to when ready — nothing from them is written into canon here. (The broader principle — external inputs are *pulled when directed*, not hand-embedded per resource, so the approach scales past a handful of resources — is a separate design conversation, not actioned in this plan.)

## 6 · Verification (before close)

Parallel checkers: zero dead links, zero orphaned `docs/NN_` or `` `NN` `` number-refs outside `archive/`, every single-owner topic restated in exactly one place, every `See also` footer resolves.

---

**See also**: `README.md` (plan-folder rules), `../principles.md` P1 (the seam this reorg embodies), `2026-06-11_layered_reference_v1.md` (the active resource-layer plan, paused at Phase 5 during this reorg).
