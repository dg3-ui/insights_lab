# Test Run 001 — Flood Inundation × Gulf Coast / Texas Water-Sited Thermal

| field | value |
|---|---|
| run_date | 2026-06-29 |
| tester | daniel |
| mcp_version | InfraSure MCP (live, as_of 2026-06-29) |
| status | **PASS** |
| anchor | Sabine (EIA 3459) |

---

## Step-by-Step Execution

### R1 — Scope to state
```
search_plants(fuel="gas", state="TX", minMw=50)
```
**Result**: TX NG fleet resolved including Sabine 3459. ⚠ Sabine resolves to **MISO / SERC-Delta** (Entergy Texas), **not ERCOT** — confirmed East-TX Entergy territory; state-scoping correct.

### R2 — Anchor asset
```
get_plant(3459)
```
**Result**: Sabine · Orange County, TX · lat 30.0242, lon -93.878 · 1,811.8 MW · 4× NG steam (1962–1979) · Operating · `cooling_water_source = "Sabine Lake" / "Sabine River"`, once-through, brackish (BR) · on-site 230 kV substation, substation_operator Entergy. Mechanism C substrate confirmed in-field.

### R3 — Nearby plants
```
nearby_plants(3459)
```
**Result**: Orange County Advanced Power Station (66621) · 0.7 km · 1,306 MW NG; Sabine River Operations (10789) · 12.1 km · 594.9 MW NG. Same-reach floodplain fan-out confirmed.

### R4 — CF read (Harvey window probe)
```
get_plant(3459).generation  → monthly CF series
```
**Result**: Harvey window: 2017-08 = 0.308, 2017-09 = 0.306 — **essentially normal**. Two anomalous low months observed: 2023-12 = 0.003, 2024-12 = 0.022 (unrelated, not flood). **CF CANNOT ISOLATE the flood** — confirmed and caveated; proof logged.

### R5 — Event corroboration
```
search_news(query="flood", state="TX")
```
**Result**: returned `[]` (as_of 2026-06-29). **⚠ No `category=` param in live tool** — attempted `category=hazards` earlier; that param does not exist. Gap logged. Event leg rests on public FEMA DR-4332-TX / NOAA Harvey record.

### R6 — VERIFY catch
`news_extracted.company` for Sabine returned **"Cheniere Energy" (conf 0.60, n=1)**. VERIFY discipline: Cheniere is LNG (Sabine Pass terminal, also Orange County area) — **wrong owner; Sabine EIA 3459 is Entergy Texas**. Tag rejected, not used.

### R7 — Retirement flag
`get_plant(3459).units`: gen 1/3/4 carry `planned_retirement = 2026-07` — 3 of 4 units retiring next month. Flagged in the applied insight forward caveat.

### R8 — Blocked-claims gate
| blocked claim type | attempted? | disposition |
|---|---|---|
| $ / EAL / payout | no | clean |
| forward inundation probability / return-period | no | clean |
| per-plant damage from CF | refused explicitly | clean (CF normal through Harvey) |
| which pads flooded / per-pad depth | no | clean |
| site-elevation read | no (not in substrate) | clean |
| national-from-regional scaling | no | clean |
| outreach to third party | no | clean |

Gate: **PASS**

---

## Accepted Claims

1. Sabine (EIA 3459), Orange County TX, is **water-sited** (cooling_water_source = Sabine Lake / Sabine River) in the Gulf Coast riverine-coastal floodplain — confirmed in-field.
2. Exposure mechanisms: **(C)** cooling-intake compromise + **(A)** switchyard inundation — directional, Medium confidence.
3. Harvey (Aug 2017) is a realized regional flood event in this geography (FEMA DR-4332-TX / NOAA public record).
4. Nearby plants 66621 (0.7 km) + 10789 (12.1 km) share the same tidewater reach — portfolio accumulation context.
5. Monthly CF **cannot isolate the flood outage** — proven by Harvey-window CF being normal.

## Rejected Claims

- "Cheniere Energy" as owner → **rejected** (VERIFY: wrong entity; owner is Entergy Texas)
- Any $ / damage attribution from CF → **blocked (model-gpr + CF doesn't show it)**
- Forward inundation probability / depth → **blocked (no site-elevation + no hazard model)**
- In-substrate flood-event news corroboration → **not found** (search_news returned [])

---

## Gaps Logged

| gap | type | impact |
|---|---|---|
| `search_news` has no `category=` param | live-tool signature gap | use `query=` + `event_type` instead; data_requirements.md retrieval step updated |
| `search_news(query="flood", state="TX")` returned `[]` | no in-substrate event article | event leg rests on public Harvey record; log to mcp_gaps.md |
| No site-elevation field | standing substrate gap | blocks inundation depth / return-period |
| Sabine 3 of 4 units retiring 2026-07 | asset lifecycle | forward-looking claims must caveat retirement |

---

## Verdict

**PASS** — directional exposure + mechanism (C/A) at **Medium confidence** issued against anchor EIA 3459. VERIFY catch (Cheniere mis-tag) exercised and rejected correctly. All blocked-claim gates clean. Gaps noted and logged.
