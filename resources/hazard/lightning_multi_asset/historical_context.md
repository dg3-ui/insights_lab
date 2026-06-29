# Historical Context — Lightning Exposure For Wind, Solar, and Electrical-Plant Assets

> **Status**: draft 2026-06-29. The realized-event record behind `lightning_multi_asset`. Cited public record, **not** per-plant damage claims. ⚠ **Reconciliation note**: align section headers with the established `historical_context.md` house format if it differs. By design this resource has **no single catastrophe anchor** — the history is cumulative.

## Realized record (cumulative, not a single event)

| Pattern | Where / what (public record) | Mechanism tie-in |
|---|---|---|
| Cumulative flash density | NOAA/Vaisala NLDN places the **US cloud-to-ground flash-density maximum along the Gulf Coast / Florida** (the test-001 geography; anchor Echo River Solar, EIA 62490, Suwannee Co FL). | the geography that drives cumulative exposure |
| Wind-turbine blade strikes | Industry/insurer loss data consistently identify **lightning as a leading cause of wind-turbine blade damage and downtime** — tall structures in open terrain attach direct strikes. | (A) direct strike → blade / nacelle |
| Induced-surge component loss | Across solar/storage/thermal, nearby strikes couple transients into inverters / transformers / control electronics — a recurring, design-managed component-replacement cost rather than a catastrophe. | (B) induced surge → electronics (solar+storage BMS at Echo River) |

## What the substrate carries about these

The substrate grounds **flash-density exposure** (plant lat/lon within the NLDN maximum), the **resolved fleet**, and asset attributes that make the mechanism concrete (Echo River's `fuel_types [SUN, MWH]` — solar + storage — is exactly the inverter/BMS electronics induced surge targets). It does **not** carry lightning-protection-system (LPS) status or a per-asset strike rate, and monthly CF cannot resolve a component-level strike. So the exposure stays geographic and cumulative, never a per-asset adequacy or strike-count claim.

## How history informs the exposure read

Lightning is **high-frequency, lower-per-event-severity, and design-managed** — so the historical signal is *cumulative component attrition + design adequacy*, not a catastrophe to be annualized. A high-flash-density geography establishes elevated exposure; whether it becomes loss depends on LPS / surge-protection adequacy (not in the substrate). Lightning-frequency trends are weakly attributable — no trend claim beyond directional.

## Citations

```text
NOAA / Vaisala NLDN flash-density climatology (Gulf/FL max)   https://www.weather.gov/ · Vaisala Annual Lightning Report
Lightning as a leading cause of wind-turbine blade damage     IEC TR 61400-24 · industry/insurer wind O&M loss literature
Induced-surge / SPD protection of PV + electronics            IEEE C62 series · NREL / Sandia PV surge-protection literature
InfraSure substrate (test 001, 2026-06-29)                    search_plants(solar, FL) → Echo River Solar 62490, fuel_types [SUN, MWH]
```

---

**See also**: `knowledge.md` §5 · `examples/applied_insight_001.md` (the validated Echo River insight) · `data_requirements.md` (gaps).
