# Historical Context — Severe Hail Exposure For Solar Assets

> **Status**: draft 2026-06-25.
>
> **Role**: `frames` + `external` evidence. This file informs the hail mechanism, materiality band, mitigation logic, caveats, and blocked claims. It **never** grounds scoped assets in a new applied insight; re-ground every event, number, and entity live before use.

## How To Use This File

```text
USE       as cited event history for hail damage, hail-stow mitigation, insurance materiality, and false-claim hygiene
DO NOT    use as a plant-level damage model, forward hail probability, EAL/PML, insurance payout, or outreach trigger
```

## Event Ledger

### Fighting Jays Solar — Fort Bend County, Texas, March 15-16, 2024

| Field | Notes |
|---|---|
| Geography / market | Fort Bend County, Texas; ERCOT / Houston-area utility-scale solar cluster. |
| What happened | CIP confirmed the Fighting Jays Solar project was damaged by hail on March 15, 2024; the project spans 3,300 acres and can produce 350 MW, and it continued operating at reduced capacity while the owner assessed generation impact ([Houston Chronicle](https://www.houstonchronicle.com/business/energy/article/large-houston-solar-farm-suffers-extensive-hail-19371591.php), accessed 2026-06-25). PV Tech reported golf-ball-sized hail and described the project as owned by Copenhagen Infrastructure Partners and AP Solar Holdings ([PV Tech](https://www.pv-tech.org/hailstorms-fighting-jays-solar-project-array-hail-tracking-software/), accessed 2026-06-25). |
| Mechanism illustrated | Severe hail can shatter c-Si modules and create both immediate output loss and longer repair/replacement exposure; this is the exact mechanism in `knowledge.md`. |
| Magnitude / impact | The event produced extensive visible module damage and reduced operation, but public reporting did **not** establish exact insured loss, EAL, or plant-level MWh impact; those stay blocked ([PV Tech](https://www.pv-tech.org/hailstorms-fighting-jays-solar-project-array-hail-tracking-software/), accessed 2026-06-25). |
| Asset / actor relevance | Owners: hail-stow readiness, module/glass choice, insurance sublimits. Investors/lenders: one hail footprint can hit hundreds of MW in a clustered solar market. |
| What it licenses | A realized-event frame and mechanism claim, plus a prompt to verify substrate CF / owner / nearby plants live. |
| What it does NOT license | Exact $ loss, EAL/PML, forward probability, or single-cause attribution of a CF dip without live substrate and external verification. |

### Fort Bend Cluster Hail-Stow Comparison — March 2024

| Field | Notes |
|---|---|
| Geography / market | Fort Bend County, Texas; nearby utility-scale solar projects including Cutlass I, Cutlass II, and Old 300. |
| What happened | VDE / PV Tech analysis says three nearby utility-scale solar farms within about 15 km of Fighting Jays were exposed to >500-year hail; two sustained no direct hail-related damage, while a third had only a few dozen damaged modules where a tracker motor issue prevented complete hail stow ([PV Tech reevaluation](https://www.pv-tech.org/reevaluating-hailstorm-damages-fighting-jays-solar-project/), accessed 2026-06-25). |
| Mechanism illustrated | Hail-stow is not generic mitigation prose; it can be the difference between widespread module breakage and limited/no damage when implemented before hail reaches the array. |
| Magnitude / impact | The cited analysis supports comparative mitigation performance, not a precise loss model. |
| Asset / actor relevance | Developers and owners should document hail alerting, stow angle, tracker operability, and stow execution for insurers and lenders. |
| What it licenses | A mitigation / diligence claim: hail-stow protocol and tracker operability are material underwriting variables. |
| What it does NOT license | A universal claim that hail-stow always prevents loss, or that every nearby project had identical exposure. |

### Midway Solar — Pecos County, Texas, May 2019

| Field | Notes |
|---|---|
| Geography / market | Pecos County, West Texas utility-scale solar. |
| What happened | Houston Chronicle reporting on Fighting Jays notes a 2019 Pecos County hailstorm damaged more than 400,000 panels at the 178 MW Midway Solar project and resulted in insurance losses of approximately $70 million ([Houston Chronicle](https://www.houstonchronicle.com/business/energy/article/large-houston-solar-farm-suffers-extensive-hail-19371591.php), accessed 2026-06-25; figure corroborated at ~$70 million, with a $70-80 million range cited across industry coverage). |
| Mechanism illustrated | Utility-scale solar hail loss can become an insurance-scale event, not only an operating nuisance. |
| Magnitude / impact | Use the ~$70 million figure only as cited historical context; do not transfer it to other sites or years. |
| Asset / actor relevance | Lenders and investors should treat hail sublimits and deductible structures as material, especially in Texas. |
| What it licenses | A class-severity framing: hail is a high-materiality solar peril. |
| What it does NOT license | Exact expected loss for another project or a forward return-period. |

## Cross-Event Patterns

```text
PATTERN 1  Hail loss is clustered and operationally sensitive: the same storm complex can hit multiple nearby solar assets.
PATTERN 2  Hail-stow and tracker operability are real controls, not cosmetic mitigations.
PATTERN 3  Insurance materiality is high, but public reporting rarely provides enough to state EAL/PML or exact payouts.
PATTERN 4  Toxicity narratives can be noisy; verify module chemistry and official environmental statements before repeating.
```

## Sources

| Source | Use | Accessed |
|---|---|---|
| [Houston Chronicle: Fighting Jays hail damage](https://www.houstonchronicle.com/business/energy/article/large-houston-solar-farm-suffers-extensive-hail-19371591.php) | Fighting Jays facts; Midway historical loss context | 2026-06-25 |
| [PV Tech: Fighting Jays hailstorm](https://www.pv-tech.org/hailstorms-fighting-jays-solar-project-array-hail-tracking-software/) | Fighting Jays damage and owner statements | 2026-06-25 |
| [PV Tech: reevaluating Fighting Jays](https://www.pv-tech.org/reevaluating-hailstorm-damages-fighting-jays-solar-project/) | Fort Bend hail-stow comparison | 2026-06-25 |
| [pv magazine USA: toxicity / hail risk](https://pv-magazine-usa.com/2024/04/16/hail-damage-and-toxicity-risks-in-solar-power-plants/) | module chemistry correction and insurance-materiality context | 2026-06-25 |

---

**See also**: `knowledge.md` · `resource.yml` · `data_requirements.md` · `../../../docs/method/resource_standard.md`.
