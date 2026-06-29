# Historical Context — Offtaker / PPA Counterparty Concentration

> **Status**: draft 2026-06-25.
>
> **Role**: `frames` + `external` evidence. This file informs commercial-risk mechanism, actor relevance, and blocked claims for `offtaker_concentration`. It **never** grounds the offtaker book of a current asset set; re-ground every buyer, PPA, and contract field live before use.

## How To Use This File

```text
USE       as historical context for PPA enforceability, counterparty bankruptcy, contract rejection, renegotiation,
          and financing uncertainty
DO NOT    use as proof that a current offtaker is risky, defaulting, or likely to reject a contract
```

## Event Ledger

### PG&E Bankruptcy and Renewable PPAs — 2019-2020

| Field | Notes |
|---|---|
| Geography / market | California utility offtaker / renewable PPA book. |
| What happened | PG&E filed for Chapter 11 in January 2019, creating uncertainty around outstanding wholesale PPAs; a legal review says the bankruptcy raised whether PG&E could renegotiate or reject PPAs, while FERC and the bankruptcy court disputed jurisdiction ([Capital University Law Review article](https://www.capitallawreview.org/article/21664-resolving-the-jurisdictional-tussle-over-power-purchase-agreements-in-electricity-utility-bankruptcy-lessons-from-pg-e-s-recent-chapter-11-reorganiza.pdf), accessed 2026-06-25). |
| Mechanism illustrated | PPA counterparty risk is not only non-payment; bankruptcy can create enforceability, financing, renegotiation, and jurisdictional uncertainty. |
| Magnitude / impact | A USC Schwarzenegger Institute report says PG&E held **387 PPAs** with renewable providers and that many older contracts exceeded **$100/MWh**, while new industrial-scale solar projects could be below **$50/MWh**; the report says the PPAs were ultimately maintained in the court-approved reorganization plan ([USC report](https://schwarzenegger.usc.edu/wp-content/uploads/images/files/Environmental_Implications_of_PGE_Bankruptcy_and_Renewable_Energy_Contracts_FINAL2.pdf), accessed 2026-06-25). |
| Asset / actor relevance | Investors/lenders should watch buyer concentration, buyer credit, contract vintage, and above-market PPA exposure. |
| What it licenses | A commercial mechanism claim: concentrated exposure to a distressed buyer can matter even if contracts are ultimately honored. |
| What it does NOT license | A claim that a current buyer will reject or renegotiate PPAs, or that a null `offtakers` array means no PPA. |

### SunEdison Bankruptcy and Project/PPA Execution Risk — 2016

| Field | Notes |
|---|---|
| Geography / market | Renewable developer / project pipeline, including Hawaii projects. |
| What happened | Reuters reported SunEdison filed for Chapter 11 on April 21, 2016 after debt-fueled expansion became unsustainable ([Reuters](https://www.reuters.com/article/business/solar-developer-sunedison-in-bankruptcy-as-aggressive-growth-plan-unravels-idUSKCN0XI1TC/), accessed 2026-06-25). |
| Mechanism illustrated | Developer bankruptcy can affect PPA execution and project completion, not just operating offtaker payment. |
| Magnitude / impact | Hawaiian Electric terminated contracts for **148 MW** of solar from three SunEdison projects, citing SunEdison's precarious financial condition and missed milestones ([Renewable Energy World](https://www.renewableenergyworld.com/solar/hawaiian-electric-cancels-contracts-for-power-from-three-sunedison-projects/), accessed 2026-06-25). |
| Asset / actor relevance | Developers and lenders should distinguish operating counterparty concentration from development-stage execution risk. |
| What it licenses | A development/execution caveat for queue-stage or not-yet-operating projects. |
| What it does NOT license | A claim that SunEdison-style risk applies to all renewable developers or all PPAs. |

### FirstEnergy Solutions PPA Rejection Litigation — 2018-2019

| Field | Notes |
|---|---|
| Geography / market | PJM / wholesale power contract and REC exposure. |
| What happened | A bankruptcy court opinion says FirstEnergy Solutions was party to nine bundled long-term PPAs involving about **500 MW** of capacity and **1.3 TWh** of 2017 purchases, and sought to reject those PPAs in bankruptcy ([U.S. Bankruptcy Court opinion](https://www.ohnb.uscourts.gov/sites/default/files/opinions/op-424554-791762-20180518-re-firstenergy-solutions-corp-et-al-v-federal-energy-regulatory-commission.pdf), accessed 2026-06-25). |
| Mechanism illustrated | Bankruptcy courts, FERC jurisdiction, and public-interest balancing can shape whether a buyer can reject wholesale PPAs. |
| Magnitude / impact | Public bankruptcy pleadings cited by court records and coverage described the PPAs / related agreements as a large long-term burden; ExchangeMonitor described **$765 million** in contracts as the dispute frame ([ExchangeMonitor](https://www.exchangemonitor.com/bankruptcy-firstenergy-tries-skirt-765m-contracts/), accessed 2026-06-25). |
| Asset / actor relevance | Lenders/investors should treat PPA enforceability and buyer bankruptcy law as part of commercial risk, not just price. |
| What it licenses | A legal-enforceability caveat: PPA value depends on counterparty credit and the legal forum in distress. |
| What it does NOT license | A current legal opinion on any specific PPA. |

## Cross-Event Patterns

```text
PATTERN 1  PPA risk is multi-dimensional: buyer credit, contract vintage, above/below-market price, jurisdiction,
           development milestone risk, and financing all matter.
PATTERN 2  Bankruptcy can create uncertainty even when contracts are ultimately honored.
PATTERN 3  The current resource still must ground buyer identity from live substrate/resolved facts; history is only context.
```

## Sources

| Source | Use | Accessed |
|---|---|---|
| [Capital University Law Review on PG&E PPAs](https://www.capitallawreview.org/article/21664-resolving-the-jurisdictional-tussle-over-power-purchase-agreements-in-electricity-utility-bankruptcy-lessons-from-pg-e-s-recent-chapter-11-reorganiza.pdf) | PG&E PPA bankruptcy/jurisdiction context | 2026-06-25 |
| [USC Schwarzenegger Institute PG&E PPA report](https://schwarzenegger.usc.edu/wp-content/uploads/images/files/Environmental_Implications_of_PGE_Bankruptcy_and_Renewable_Energy_Contracts_FINAL2.pdf) | PG&E renewable PPA count/vintage/cost context | 2026-06-25 |
| [Reuters SunEdison bankruptcy](https://www.reuters.com/article/business/solar-developer-sunedison-in-bankruptcy-as-aggressive-growth-plan-unravels-idUSKCN0XI1TC/) | SunEdison filing context | 2026-06-25 |
| [Renewable Energy World: Hawaiian Electric cancels SunEdison contracts](https://www.renewableenergyworld.com/solar/hawaiian-electric-cancels-contracts-for-power-from-three-sunedison-projects/) | 148 MW Hawaii project/PPA cancellation context | 2026-06-25 |
| [U.S. Bankruptcy Court FirstEnergy/FERC opinion](https://www.ohnb.uscourts.gov/sites/default/files/opinions/op-424554-791762-20180518-re-firstenergy-solutions-corp-et-al-v-federal-energy-regulatory-commission.pdf) | FirstEnergy PPA rejection litigation | 2026-06-25 |
| [ExchangeMonitor FirstEnergy contracts coverage](https://www.exchangemonitor.com/bankruptcy-firstenergy-tries-skirt-765m-contracts/) | FirstEnergy contract-burden frame | 2026-06-25 |

---

**See also**: `knowledge.md` · `resource.yml` · `data_requirements.md` · `../../../docs/method/resource_standard.md`.
