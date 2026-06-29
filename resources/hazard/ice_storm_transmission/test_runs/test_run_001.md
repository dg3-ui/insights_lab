# Test Run 001 — Ice Storm × South-Central Ice Belt / Oklahoma Wind + Delivery Corridor

| field | value |
|---|---|
| run_date | 2026-06-29 |
| tester | daniel |
| mcp_version | InfraSure MCP (live, as_of 2026-06-29) |
| status | **PASS** |
| anchor | Wagon Wheel Wind (EIA 69224) |

---

## Step-by-Step Execution

### R1 — Scope to state
```
search_plants(fuel="wind", state="OK", minMw=50)
```
**Result**: OK wind fleet resolved — Wagon Wheel 69224 (598.4 MW, Logan Co), Traverse 63479 (999 MW, Custer Co), Frontier II 62837, Diamond Spring 63327.

### R2 — Anchor asset
```
get_plant(69224)
```
**Result**: Wagon Wheel Wind · Logan County, OK · lat 36.153, lon -97.575 · 598.4 MW WND · Owner: Southwestern Electric Power (SWEPCO) / AEP · Operating. AEP/SWEPCO also owns regional transmission in this corridor — the delivery-infrastructure hook confirmed by owner identity.

### R3 — Grid detail
`get_plant(69224).grid` drill deferred (not required for exposure + mechanism claim). Substation / interconnection detail logged as next-run drill.

### R4 — CF read
Skipped this run — monthly CF cannot isolate an ice-storm delivery outage from the winter seasonal minimum. **Blocked/Low** per resource confidence rules. Explicitly not read in.

### R5 — Event corroboration
No news query issued this run — climatological ice-belt exposure framing. Gap logged; a future run should attempt `search_news(query="ice storm Oklahoma", event_type=...)`.

### R6 — Cross-resource boundary
Generation-side freeze (gas wellhead / pipeline) confirmed to be `extreme_cold_winter_storm` resource — **not double-counted** here. Delivery-infrastructure boundary stated.

### R7 — Mechanism statement
Three mechanisms stated and distinguished: (A) transmission ice-load failure [PRIMARY], (B) blade icing → shutdown [temporary], (C) delivery stranding — undamaged plant cannot export. Delivery-infrastructure framing: loss is **grid-side**, not plant-side for (C).

### R8 — Blocked-claims gate
| blocked claim type | attempted? | disposition |
|---|---|---|
| $ / restoration cost / payout | no | clean |
| forward ice-load probability / return-period | no | clean |
| per-span or per-plant attribution from CF | refused explicitly | clean |
| single-cause CF read | no | clean |
| which spans collapsed | no (not in substrate) | clean |
| generation-side freeze double-count | explicitly refused | clean |
| national-from-regional scaling | no | clean |
| outreach to third party | no | clean |

Gate: **PASS**

---

## Accepted Claims

1. Wagon Wheel Wind (EIA 69224), Logan County OK, is in the **South-Central ice-storm belt** (NOAA/SPIA freezing-rain climatology) — geographic exposure confirmed.
2. AEP/SWEPCO owns both the wind asset and regional transmission → delivery-infrastructure corridor relevance confirmed by owner identity.
3. Primary exposure: **(A) transmission ice-load mechanical failure** — capital-intensive delivery outage.
4. Secondary exposures: **(C) delivery stranding** (physically undamaged plant cannot export) + **(B) blade icing** (temporary shutdown).
5. Loss framing: **delivery-infrastructure**, not plant-damage for (C); do not claim physical damage when the line, not the turbine, fails.
6. OK wind fleet shares the same ice-belt delivery-dependence (Wagon Wheel 69224, Traverse 63479, Frontier II 62837, Diamond Spring 63327).

## Rejected Claims

- Any $ / restoration cost / payout → **blocked (model-gpr)**
- Forward ice-load probability / return-period → **blocked (no served ice-load model)**
- Per-span conductor ratings → **blocked (not in substrate)**
- CF attribution of an ice-storm outage → **blocked (winter seasonal confound)**
- Generation-side freeze as part of this resource → **blocked (cross-resource boundary; use extreme_cold_winter_storm)**

---

## Gaps Logged

| gap | type | impact |
|---|---|---|
| No conductor/tower ratings or line geometry | standing substrate gap | blocks per-span ice-load failure claim |
| No served ice-load model | R12 missing | directional only |
| `search_news` event not attempted | deferred | ice-storm event corroboration absent this run |
| `get_plant(69224).grid` drill deferred | next-run drill | substation / interconnection detail |

---

## Verdict

**PASS** — directional delivery-infrastructure exposure + three mechanisms at **Medium confidence** issued against anchor EIA 69224. Cross-resource boundary (extreme_cold_winter_storm) observed cleanly. All blocked-claim gates clean. Gaps noted and logged.
