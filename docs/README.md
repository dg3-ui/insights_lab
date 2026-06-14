# docs/ — Index & Read Order

> **Status**: the docs map, 2026-06-13. Docs are grouped by **job** (folder = job), and the **stable/volatile seam is a folder boundary** — the project's own P1 principle applied to its own documentation. Reorganized from the flat `00–11` sequence per `plans/done/2026-06-13_docs_reorg.md`.

## The Map

```text
docs/
├── README.md         this index
├── architecture.md   THE FRONT DOOR — start here. End-to-end flow (Mermaid + ASCII), the 4 layers,
│                     terminology, the gate. Absorbs the old project-brief + architecture docs.
├── principles.md     THE DISCIPLINE (P1–P5) — what must not move: stable vs volatile · content
│                     downstream of validated insight · process-data laws · iteration · no-mush.
├── use_cases.md      WHO IT'S FOR — the 2 buckets × audience (Pillar 3) + the V0 scope contract
│                     + the proof-of-value validation method.
│
├── method/           HOW TO REASON & BUILD (the contract)
│   ├── analysis_families.md   the 7 families (V0 = Exposure) + the Q&A grammar
│   ├── resource_standard.md   the methodology_resource + applied_insight contracts (+ maturity/peril fields)
│   ├── data_map.md            the input taxonomy + the source_ref shape (sole owner)
│   ├── discovery_spec.md      find_methodology / get_methodology contract
│   ├── workflow_recipes.md    the recipe layer — composing resources into jobs (docs, not a runtime)
│   └── outlier_playbook.md    reverse-engineering an off-substrate outlier (the ad-hoc / research-grounded lane)
│
├── process/          THE LOOP
│   ├── test_protocol.md       the manual test, session capture, failure taxonomy, feedback intake
│   └── commands.md            the command toolchain design (the thin-conductor rule)
│
├── status/           VOLATILE HUB — what's built / next (kept out of the canon docs on purpose)
│   ├── capabilities.md        platform-capability build status + the open architectural decisions
│   ├── mcp_gaps.md            the MCP tool-gap ledger (gap · workaround · roadmap)
│   └── commands.md            the per-command build registry
│
├── plans/            the active working plans (the real currency of "what's next")
└── learning/         onboarding fundamentals (01–04) + session logs (logs/ — session records, not the track)
```

```text
STABLE CANON                          VOLATILE                         NAVIGATIONAL
architecture · principles · use_cases   status/ (3 ledgers)              README (this)
method/ (6) · process/ (2)              plans/ (working plans)           See-also footers
                                        learning/logs/ (session records)
read once, trust                        check for what's live            wayfinding
```

## Read Order (by audience)

```text
NEW CONTRIBUTOR   architecture.md  →  learning/ (README → 01 → 02 → 03 → 04)
                  →  resources/weather_and_climate/el_nino_enso/  (the worked example)

SENIOR REVIEWER   architecture.md  →  principles.md  →  use_cases.md
                  →  method/  →  status/capabilities.md

AUTHOR (a new     architecture.md  →  method/resource_standard.md  →  method/data_map.md
 resource)        →  process/test_protocol.md  →  /new-resource  →  resources/_reference/ (form)

"WHAT'S NEXT?"    plans/  (active work)  →  status/capabilities.md (build state)
                  →  status/mcp_gaps.md (tool roadmap)
```

## Conventions

- **House doc style**: every doc opens with a `> **Status**` blockquote, reasons in ASCII diagrams + tight tables, and ends with a `See also` footer. Cross-references are by **path/name** (the `00–11` numbers are retired — a name survives a future reorg, a number doesn't).
- **Single-owner**: each topic is owned by one doc; everyone else points. The big owners: the 4-layer diagram → `architecture.md`; the principles → `principles.md`; the `source_ref` shape → `method/data_map.md`; the output matrix → `resources/_style/output_contracts.md`; the underscore-folder rule → `resources/README.md`.

---

**See also**: `architecture.md` (the front door), `../README.md` (repo map + working rules), `../CLAUDE.md` (the full agent instructions), `plans/done/2026-06-13_docs_reorg.md` (why this structure).
