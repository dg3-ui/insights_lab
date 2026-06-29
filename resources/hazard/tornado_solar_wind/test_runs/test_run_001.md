# Test Run 001 — Tornado × Southern Plains / Oklahoma Wind

| field | value |
|---|---|
| run_date | 2026-06-29 |
| tester | daniel |
| mcp_version | InfraSure MCP (live, as_of 2026-06-29) |
| status | **PASS** |
| anchor | Traverse Wind Project (EIA 63479) |

---

## Step-by-Step Execution

### R1 — Scope to state
```
search_plants(fuel="wind", state="OK", minMw=50)
```
**Result**: Traverse 63479 (999 MW, Custer Co), Wagon Wheel 69224 (598.4 MW, Logan Co), Frontier II 62837, Diamond Spring 63327 — OK wind fleet resolved.

### R2 — Anchor asset
```
get_plant(63479)
```
**Result**: Traverse Wind Project · Custer County, OK · lat 35.71, lon -98.83 · 999 MW WND · Owner: Southwestern Electric Power (SWEPCO) / AEP · Operating · verified as SPC Tornado-Alley corridor geography.

### R3 — Flash / event corroboration
`search_news` event corroboration not attempted this run — climatological exposure framing only. No news query issued. **Gap logged** (see below).

### R4 — CF read
Skipped this run — a per-plant strike via narrow-footprint tornado would not resolve in the monthly CF series. **Blocked/Low** per resource confidence rules.

### R5 — Sub-plant geometry
Sub-plant turbine layout **not in the substrate** (confirmed). No per-turbine destruction claim issued.

### R6 — Mechanism statement
EF-scale winds + debris → binary total loss in path → **catastrophic-but-localized**. Stated directionally. Annualizing across nameplate explicitly refused.

### R7 — Blocked-claims gate
| blocked claim type | attempted? | disposition |
|---|---|---|
| $ / EAL / payout | no | clean |
| forward strike probability / return-period | no | clean |
| per-plant damage from CF | no | clean |
| per-turbine destruction (sub-plant geometry) | no | clean |
| annualizing total loss across nameplate | refused explicitly | clean |
| national-from-regional scaling | no | clean |
| outreach to third party | no | clean |

Gate: **PASS**

---

## Accepted Claims

1. Traverse Wind (EIA 63479), Custer County OK, is geographically in the SPC Southern-Plains tornado-climatology corridor.
2. Tornado exposure is **catastrophic-but-localized**: total structural loss of turbines in a strike path, narrow footprint.
3. Exposure framing: **directional, Medium confidence** (corridor geography + mechanism stated; per-asset probability blocked).
4. OK wind fleet (63479, 69224, 62837, 63327) shares the same Tornado-Alley corridor geography.

## Rejected Claims

- Any $ / expected-loss / payout number → **blocked (model-gpr)**
- Per-asset annual strike probability → **blocked (no hazard model)**
- Annualizing a total loss across 999 MW nameplate → **explicitly refused (catastrophic-but-localized)**
- Which specific turbines destroyed → **blocked (sub-plant geometry not in substrate)**

---

## Gaps Logged

| gap | type | impact |
|---|---|---|
| No served tornado-hazard model | R12 missing | blocks per-asset strike probability and $ |
| No sub-plant geometry | standing substrate gap | blocks per-turbine destruction extent |
| `search_news` event not attempted | deferred | event corroboration absent this run |

---

## Verdict

**PASS** — directional exposure + mechanism at **Medium confidence** issued against anchor EIA 63479. All blocked-claim gates clean. Gaps noted and logged.
