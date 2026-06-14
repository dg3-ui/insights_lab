# Studio Brief — One Cell, One Channel: Storm Surge on the Energy Coast

> **Output type**: report · **As of**: 2026-06-14 · **Audience**: internal (InfraSure team; client-ready on review) · **Grounding**: HYBRID — research-grounded coastal/port exposure (`outlier_playbook.md`) + MCP-grounded in-substrate energy overlay (the Houston Ship Channel gas cluster)
>
> **A cloud-attachable brief**: attach this + `../resources/_style/brand.md` + `../resources/_principles/voice.md` (+ `_craft` if charts) → render for the target format. **Post-gate only** — this brief dresses a *validated* insight (the three guards, `README.md`).
>
> **Entity honesty (read first)**: the brief was commissioned on **"Anten," a recent PORTS acquisition** to be tied to storm-surge / hurricane-season weather. **"Anten" does not resolve.** No company by that name surfaces in public M&A reporting (the nearest real names — AD Ports, I Squared / Philippines Coastal, *Antin* Infrastructure's Aquavista marinas — are different entities and assuming any of them *is* Anten would be invention), and the InfraSure substrate returns nothing for it (`plants_by_owner="Anten"` → one unrelated solar substring hit; `find_by_extracted_fact buyer/company="anten"` → empty; `search_news="Anten"` → an "antenna" false match). So the *specific* entity is **unresolvable** and is flagged as a gap, not faked. What is **fully resolvable** is the phenomenon the meeting actually cares about: storm-surge and hurricane-season risk on a coastal **energy-and-logistics port** as a single-cell chokepoint. That is built here, grounded, with a real in-substrate energy cluster standing in for "the assets a coastal acquisition would actually own or sit beside."

## 1 · The validated insight (the gated content — grounds everything)

**Claim** (two parts, at different confidence):

1. **The chokepoint, research-grounded — directional.** A coastal energy-and-logistics port on the upper Texas coast is a **single-cell exposure**: the same Galveston Bay storm-surge corridor that floods the dock floods the fuel tanks, the substations, and the generation sitting on the same low ground. Much of the developed west side of Galveston Bay lies **below 30 ft elevation**, and a major hurricane can drive a **20-plus-ft surge** up the bay into the Houston Ship Channel; the City of Houston's own briefing puts **~2,000 storage tanks** in the flood envelope of a 22-to-24-ft surge. This is the Red Dog geometry transposed to the warm coast: *one* climate-sensitive corridor gates fuel-in, power, and cargo-out at once.

2. **The in-substrate energy overlay, MCP-grounded — factual co-location.** That corridor is not empty of energy assets. Anchored on **Baytown Energy Center (EIA 55327, 932.9 MW gas combined-cycle, Constellation Energy, Chambers County, lat 29.773 / lon −94.902, ERCOT HB_HOUSTON)**, the substrate places **three more large gas plants within ~3.4 km** — Cedar Bayou (3460, 1,530 MW), Cedar Bayou 5 (68606, 721 MW), Cedar Bayou 4 (56806, 535.5 MW). That is **~3,719 MW of ERCOT gas generation inside a ~3.4 km radius**, all on the same Ship Channel / Galveston Bay surge plain. Add the two ExxonMobil Baytown plants on the channel (10692, 381.8 MW; 10436, 209.3 MW) and the named cluster is **~4,310 MW**. Baytown's own combined-cycle draws cooling water from the **Coastal Water Authority** intake — the asset is physically coupled to the same coastal water system the surge rides in on.

**Scope**: upper Texas coast / Houston Ship Channel · Galveston Bay surge corridor · gas generation co-located on the channel. Anchor: Baytown Energy Center (55327). Same-corridor fan-out: 3460, 68606, 56806 (`nearby_plants`, ≤ 3.4 km), plus 10692 / 10436 on the channel.

**Mechanism** (one breath): a major-hurricane surge pushes Gulf water up the funnel of Galveston Bay into the Ship Channel → low-elevation tank farms, substations, switchyards and CC cooling intakes flood → simultaneous loss of fuel handling, grid interconnection, and thermal generation in one event, with recovery gated by dewatering and equipment replacement, not by the storm passing. The exposure is **geographic and structural** (what sits where), not a dated landfall forecast.

**Source references**:

```text
1. substrate · InfraSure get_plant(55327) · Baytown Energy Center · 932.9 MW gas CC, Constellation Energy (chain Calpine→Constellation), Chambers Co TX, lat 29.773/−94.902, ERCOT HB_HOUSTON, 345 kV, cooling = Coastal Water Authority · as_of 2026-06-14 · primary (the anchor)
2. substrate · InfraSure nearby_plants(55327, ≤25 km) · Cedar Bayou 3460 (1,530 MW, 3.4 km) · Cedar Bayou 5 68606 (721 MW, 3.1 km) · Cedar Bayou 4 56806 (535.5 MW, 3.1 km) · as_of 2026-06-14 · primary (the co-located cluster → ~3,719 MW ≤3.4 km)
3. substrate · InfraSure search_plants(query="Baytown", state=TX) · ExxonMobil Baytown Turbine 10692 (381.8 MW) · ExxonMobil Baytown Refinery 10436 (209.3 MW), Harris Co, on-channel · as_of 2026-06-14 · support (extends named cluster to ~4,310 MW)
4. external · City of Houston PSHS briefing "Risks of Storm Surge from Galveston Bay / Ship Channel" (houstontx.gov) · west Galveston Bay largely <30 ft elevation; 20+ ft surge possible; ~2,000 tanks in a 22–24 ft surge envelope · accessed 2026-06-14 · frames the hazard geography
5. external · Rice University SSPEED Center / Galveston Bay Park Plan (news.rice.edu, 2025; ABC13) · funded in part by Port Houston; a modeled Cat-4 surge cut 5–8 ft in the Ship Channel zone · accessed 2026-06-14 · frames mitigation (a lever exists; not yet built)
6. external · E&E News "Houston is one hurricane away from an oil and gas disaster" (eenews.net) · the channel as a realized single-event energy-logistics risk · accessed 2026-06-14 · frames the precedent class
7. external · NOAA 2026 Atlantic Hurricane Outlook (noaa.gov, May 2026) · BELOW-normal: 8–14 named storms, 3–6 hurricanes, 1–3 major; 55% below / 10% above; El Niño shear; "it only takes one" · accessed 2026-06-14 · frames the season, NOT a site probability
```

**Confidence** (per-part, capped at the weakest input):

- *The surge corridor co-locates fuel, grid and generation on one low-elevation plain* — **medium-high** (elevation, surge range and the tank count are from the City of Houston briefing; the ~3,719 MW co-location is a hard substrate count).
- *A major-hurricane surge would hit this cluster simultaneously* — **medium** (mechanism is sound and the geography is real; magnitude depends on storm track/intensity, which is not modeled here).
- *Forward, this-season risk to the named assets* — **low / directional** (no surge model, no return-period, no per-asset loss — geographic exposure only).

**Caveats**:

- The corridor read is **research-grounded**, not a proprietary surge model — public elevation, surge-range and tank-count figures disciplined by our claim/confidence rules. It is exposure geography, not a forecast.
- The ~3,719 MW (≤3.4 km) and ~4,310 MW (named-cluster) figures are **co-location capacity counts**, not modeled loss and not a simultaneous-outage estimate. They say "this much generation sits in the corridor," nothing about how much would fail in a given storm.
- **NOAA's 2026 season is below-normal** (55% below / 10% above). That lowers basin-wide storm *count*, not a single port's surge exposure: a below-normal season has still produced Category-5 landfalls, and "it only takes one" (NOAA). The chokepoint framing deliberately survives a quiet forecast — that is the point, not a hedge.
- Baytown's spring-2025 capacity-factor dip (monthly CF ~0.25–0.30, Apr–Jun 2025, vs ~0.5–0.6 typical) is **dispatch/economic cycling on a combined-cycle plant, not a storm signal** — no major Gulf landfall in that window; it is named here only to pre-empt mis-reading it as hazard.
- **No dollar figure**: the City briefing's "$40–50 billion" regional-damage range is a third-party scenario frame, not our modeled EAL for these assets; site-level loss is out of scope.

**Actor relevance**:

- **Acquirer / owner of a coastal port or the co-located generation** — surge hardening (tank berms, substation elevation, switchyard flood walls), the Coastal Water Authority intake dependency, and a dewatering/black-start recovery plan are the levers; the Galveston Bay Park Plan is the public mitigation to track.
- **Investor** — capacity concentration in one surge cell (~3.7 GW within 3.4 km) is a correlated, single-event downside axis that portfolio diversification across the basin does not remove.
- **Lender** — a surge-driven multi-asset, multi-month outage on the channel is a correlated-default / DSCR stressor across several financed plants at once, not an idiosyncratic single-asset risk (directional).
- **Operator** — hurricane-season fuel and crew staging, and the order of restoration (grid interconnection vs generation vs fuel handling) when all three flood together.

**Gate (review trace)**: no $ EAL / PML asserted (✓ — the $40–50B figure kept as a third-party scenario frame); no forward hurricane probability or return-period (✓ — NOAA outlook used as season context only); no plant-level production forecast (✓); no single-cause attribution (✓ — surge mechanism stated as directional; the 2025 CF dip explicitly labeled non-storm); not unscoped national (✓ — one corridor, gas on the channel). Every material number carries a `source_ref` with `as_of`. Confidence split per-part and capped. The unresolvable entity is disclosed, not papered over. **Gate: PASS** (research-grounded + MCP-overlay hybrid).

## 2 · The comparison (the moat + the hook)

The home-run line is a **grounded co-location**, produced by `nearby_plants(55327)` against the public surge geography — not an invented stat:

```text
ONE Galveston Bay surge corridor sits over, within a ~3.4 km radius:
   Baytown Energy Center   55327   932.9 MW   gas CC   Constellation Energy   (anchor)
   Cedar Bayou             3460  1,530.0 MW   gas      3.4 km
   Cedar Bayou 5           68606   721.0 MW   gas      3.1 km
   Cedar Bayou 4           56806   535.5 MW   gas      3.1 km
   ───────────────────────────────────────────────────────────────
   ~3,719 MW of ERCOT gas inside one surge cell        (+ ~591 MW ExxonMobil Baytown on-channel → ~4,310 MW named)
```

A vanilla model can describe "Houston hurricane risk." It cannot, in one call, place **~3.7 GW of named, owner-resolved ERCOT gas generation inside a 3.4 km surge radius and tie each MW to an EIA id and an owner**. That co-location *is* the moat: the corridor is not an abstraction, it is four plants you can name. The honest framing of the comparison is **named-cluster vs the surge corridor** (concentration), not "you vs peers over 12 months" — because the bottom-up coastal case has no peer fleet to rank; the concentration itself is the hook.

## 3 · Creative & Activation (the cherry — bounded by the guards)

```text
HERO VISUAL    A single map: the Galveston Bay / Houston Ship Channel surge corridor (public elevation shading,
               <30 ft) with the four gas plants pinned and labeled by id + MW, the ~3.4 km radius drawn around
               the anchor. One caption: "~3,719 MW of ERCOT gas inside one surge cell · source: InfraSure
               nearby_plants(55327) + City of Houston PSHS surge briefing · as_of 2026-06-14." The visual SAYS
               only what §1 gated: co-location, not loss. (_craft: every pin a source_ref; no modeled-damage layer.)
PUNCHLINE/HOOK "One cell, one channel." The punch lands on the FRAMING — a single surge corridor over a named
               4-plant, ~3.7 GW cluster — never on a bigger number. Subhead carries the calibrated season note:
               "NOAA calls 2026 quiet. The corridor doesn't care — it only takes one." (Honest: amplifies the
               below-normal forecast into the chokepoint point, does not inflate risk.)
COMPARISON     Framed as concentration, not ranking: "Diversifying across the basin doesn't help when 3.7 GW
               shares one surge cell." Grounded in the nearby_plants result; no manufactured peer comparison.
CHANNEL NOTES  report subject-line: "Storm surge on the energy coast — the Houston Ship Channel chokepoint (internal draft)."
               blog title (if generalized later, entity-anonymized): "One Cell, One Channel."
               email one-liner: "~3.7 GW of ERCOT gas sits inside a single Galveston Bay surge corridor — here's the geography."
               Send stays human-in-the-loop, post-gate; no automated outreach.
```

## 4 · Render notes

```text
COMPOSE     brand.md Part A (Inter/JetBrains-Mono, green+amber accents, the document bones) → rendered for the
            target via Part B (HTML artifact default; DOCX on request) · voice.md (no em-dashes, claim-first,
            owned caveats) · _craft (the one grounded map; caption + source + as_of below it) · output_contracts.md
            §3 report envelope (a blog scoped to one corridor: lead with the named entities, narrow the caveat to them).
GATE        renders ONLY this validated insight; every number traces to §1's source_refs (P2). The unresolvable
            "Anten" entity is surfaced honestly in the dek/caveat, never silently substituted.
GUARDS      gate-upstream (insight built first, then dressed) · creative≠overclaim (punch on "one cell, one channel",
            numbers held at co-location counts) · grounded-hook (the ~3,719 MW is a real nearby_plants(55327) result).
```

## 5 · Gaps / next

```text
· ENTITY UNRESOLVED — "Anten" does not resolve to a public ports-acquisition company; the specific port(s),
  owner, and assets are unknown. Resolve the real entity (confirm spelling / get the deal name from the meeting),
  then re-anchor the in-substrate overlay on the actual port's coordinates via nearby_plants on its lat/lon.
· MCP GAP — no coordinate/geometry-seeded nearby query: I had to anchor on a known plant (55327) to fan out;
  a "plants within R km of an arbitrary lat/lon" call would let us drop a pin on ANY port (on- or off-substrate)
  and read the surrounding energy cluster directly. Pairs with the county/geometry-aware aggregate gap. (Log to mcp_gaps.)
· MCP GAP — no elevation / surge / flood-zone field on a plant: the corridor exposure had to come from external
  public sources (City of Houston, SSPEED). A served coastal-elevation or FEMA-zone attribute would let the
  surge overlay be substrate-grounded, not just research-grounded. (Log to mcp_gaps — the directional-now-quantify-later wall.)
· METHOD — this is the SECOND outlier-class read (after Red Dog: Arctic-industrial). It opens a new class:
  the COASTAL energy-and-logistics chokepoint (surge · funnel bay · co-located tank+grid+generation). Two outliers
  now share the "single climate-sensitive corridor" concept → per outlier_playbook §6.5, consider formalizing the
  ad-hoc framework. Realized precedent for the class: Houston Ship Channel near-misses (Ike 2008, Harvey 2017).
· FORM — if this lands, promote toward _reference/internal/report/ as the first COASTAL bottom-up report exemplar
  (Red Dog is the cold-region one).
```
