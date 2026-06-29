# Test Run 001 — Lightning × Florida Solar+Storage Flash-Density Maximum

| field | value |
|---|---|
| run_date | 2026-06-29 |
| tester | daniel |
| mcp_version | InfraSure MCP (live, as_of 2026-06-29) |
| status | **PASS** |
| anchor | Echo River Solar (EIA 62490) |

---

## Step-by-Step Execution

### R1 — Scope to fuel class + state
```
search_plants(fuel="solar", state="FL", minMw=50)
```
**Result**: FL solar fleet resolved including Echo River Solar (62490, 104.5 MW, Suwannee Co, fuel_types [SUN, MWH]) and Sunshine Gateway (61763, Columbia Co, NextEra) — same north-FL flash-density band.

### R2 — Anchor asset
```
get_plant(62490)
```
**Result**: Echo River Solar · Suwannee County, FL · lat 30.296, lon -82.864 · 104.5 MW · `fuel_types = [SUN, MWH]` (solar + storage) · Owner: Florida Power & Light / NextEra Energy · Operating. **`fuel_types` includes MWH** — inverter + BMS electronics confirmed present; mechanism B substrate confirmed in-field.

### R3 — Flash-density geography
NLDN cloud-to-ground flash-density climatology: Florida is the US maximum. Suwannee County (north FL, lat 30.3) is within the high-flash-density band. Confirmed via external (NOAA/Vaisala NLDN) — this is the geographic anchor.

### R4 — Nearby plant (fleet context)
Sunshine Gateway Solar (61763) · Columbia County, FL · NextEra — same north-FL band, same owner. Confirms fleet-level accumulation context for NextEra.

### R5 — LPS / surge-protection status
**Not in the substrate** — confirmed. No per-asset LPS adequacy claim issued.

### R6 — CF read
Not drilled. Monthly CF cannot resolve a component-level lightning strike. **Blocked/Low** per resource confidence rules.

### R7 — Event corroboration
No news query issued this run — cumulative-exposure framing, not an event translation this run. A future run should attempt `search_news(query="lightning solar", state="FL")`.

### R8 — Mechanism distinction
Two mechanisms stated and distinguished:
- **(B) Induced surge** into inverters / transformers / BMS — **PRIMARY for solar + storage** (applies here)
- **(A) Direct strike** — dominant for tall wind turbines (cross-class; not the anchor here)
Echo River is solar + storage → mechanism B is the concrete one; mechanism A is acknowledged as cross-class.

### R9 — Framing guard
Stated explicitly: **high-frequency / lower-severity cumulative component risk + design adequacy** — NOT a catastrophe. Frame: cumulative O&M / availability drag, not a single loss event.

### R10 — Blocked-claims gate
| blocked claim type | attempted? | disposition |
|---|---|---|
| $ / EAL / payout | no | clean |
| forward strike rate / component-failure probability | no | clean |
| per-plant damage from CF | refused | clean |
| LPS adequacy claim | refused (not in substrate) | clean |
| catastrophe framing | refused (wrong frame) | clean |
| national-from-regional scaling | no | clean |
| outreach to third party | no | clean |

Gate: **PASS**

---

## Accepted Claims

1. Echo River Solar (EIA 62490), Suwannee County FL, is in the **US cloud-to-ground flash-density maximum (Florida)** — NLDN-confirmed geography.
2. `fuel_types = [SUN, MWH]` confirms solar + storage electronics (inverters + BMS) — mechanism **(B) induced surge** substrate confirmed in-field.
3. Exposure framing: **high-frequency / lower-severity cumulative component risk + design adequacy** — NOT a catastrophe.
4. FL solar fleet (Echo River 62490 + Sunshine Gateway 61763) shares the same north-FL flash-density band → NextEra accumulation context.
5. Overall exposure + mechanism: **Medium confidence** (flash-density geography + mechanism B substrate; LPS status not in substrate → adequacy blocked).

## Rejected Claims

- Any $ / EAL / payout → **blocked (model-gpr)**
- Forward strike rate or component-failure probability → **blocked (no served strike-rate model)**
- LPS / surge-protection adequacy claim → **blocked (not in substrate)**
- Per-plant damage from CF → **blocked (component-level strike doesn't resolve in monthly CF)**
- Catastrophe framing → **rejected (wrong frame — this is high-frequency/lower-severity)**
- Mechanism A (direct strike to blade/nacelle) as the primary for this solar anchor → **rejected (correct for tall wind; mechanism B applies to solar)**

---

## Gaps Logged

| gap | type | impact |
|---|---|---|
| No LPS / surge-protection-status field | standing substrate gap | blocks per-asset adequacy claim |
| No served strike-rate model | R12 missing | directional only; blocks $ |
| `search_news` event not attempted | deferred | event corroboration absent this run |
| `get_plant(62490)` inverter/BMS detail + CF drill deferred | next-run drill | component-level detail |

---

## Verdict

**PASS** — directional high-frequency/lower-severity exposure + mechanism B at **Medium confidence** issued against anchor EIA 62490. `fuel_types = [SUN, MWH]` confirmed mechanism B substrate in-field. Frame guard (cumulative component risk, not catastrophe) exercised correctly. All blocked-claim gates clean. Gaps noted and logged.
