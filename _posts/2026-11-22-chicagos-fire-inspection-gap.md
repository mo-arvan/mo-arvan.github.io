---
layout: post
title: "Chicago's Fire Inspection Gap"
description: Chicago inspects 16.8% of the buildings its fire code requires each year. A public-data inventory, a risk-ranked inspection queue, and a costed plan to close the gap.
tags: civic-data public-policy chicago
date: 2026-11-22
toc:
  sidebar: left
---

## Executive Summary

Chicago's fire code requires annual inspection of commercial and high-occupancy buildings [(#fire-code)](#fire-code). An October 2025 audit by the city's Inspector General reviewed 59,313 records (27,491 buildings plus 31,822 tenant spaces) in the Fire Prevention Bureau's database [(#fpb-count)](#fpb-count) and found that only **16.8% received their annual inspection** in the year before the audit's data pull [(#inspect-rate)](#inspect-rate); 47.1% had gone five or more years without one, some not in decades [(#half-uninspected)](#half-uninspected). Chicago's own fire deaths are near historic lows [(#chicago-fire-deaths)](#chicago-fire-deaths), so this is not a body count. It is a mandated safety system running at a fraction of its required rate, the kind of fragmented oversight that, in its worst form, produced disasters like Grenfell Tower and Ghost Ship in other cities [(#grenfell)](#grenfell), [(#ghost-ship)](#ghost-ship).

**Three contributions follow.** First, a building inventory of the kind the OIG recommended and that CFD's response treated as the Department of Buildings' responsibility rather than its own [(#cfd-response)](#cfd-response). From public violation, permit, and 311 records I classified roughly 81,351 Chicago buildings into the use types the annual-inspection mandate targets [(#inventory)](#inventory), about 3x the 27,491 buildings OIG was able to review (an approximation from permit-text keywords, not a validated register; see Finding 2). Of those, roughly 40,722 have zero building-violation records [(#black-holes)](#black-holes), and 47,227 are flagged across five risk buckets [(#total-flagged)](#total-flagged). Second, a diagnosis of why inspection alone doesn't reduce hazards: an enforcement model that imposes fines but rarely collects them. Third, a legislative path from the new Healthy Homes working group to combined inspection with stronger lien enforcement.

**The gap is throughput, and systems are the tractable lever.** NYC's fire inspectors conduct more than 250,000 inspections a year with about 400 inspectors, roughly 12 per inspector per week; Chicago's 9,971 annual inspections across an inspection workforce of 62 to 89 work out to about 2 to 3 per inspector per week [(#throughput)](#throughput). The counts are not perfectly comparable (NYC's includes re-inspections), but the gap is large on any reading. It is not purely a headcount problem: NYC itself carries a 49,834-inspection backlog and says it needs both more inspectors and the automated targeting and routing it has not fully deployed [(#nyc-backlog)](#nyc-backlog). A real building inventory, risk-based targeting, and route optimization are what Chicago lacks entirely, and what the tool here supplies.

**Inspection alone doesn't fix buildings. Enforcement does.** Chicago summons the *person* to an administrative hearing, and about 68% of building-violation cases end without the owner engaging: roughly 24% are default judgments and 44% are cases the city itself drops before hearing [(#non-engage)](#non-engage). The result is $827M in imposed building fines [(#fines-total)](#fines-total), little of it collected, against $3.1B in uncollected debt across the whole administrative-hearing system [(#debt-hearing)](#debt-hearing). NYC's data shows property-attached charges collect far better than person-attached penalties (the two are not a clean comparison), and its budget office estimates material gains from making penalties lienable [(#nyc-rates)](#nyc-rates), [(#nyc-ibo)](#nyc-ibo). Illinois already gives Chicago lien and receivership authority [(#peer-gaps)](#peer-gaps); the gap is systematic use. And even when inspections happen, five departments hold separate authority over fire, structure, lead, environmental, and habitability conditions in the same buildings [(#five-depts)](#five-depts), so an inspector standing in an in-scope building who sees a non-fire hazard cannot cite it.

**The economics support a pilot, not a budgeted revenue line.** A lean Year-1 pilot runs an estimated $410K, more realistically $0.5-0.8M fully loaded [(#impl-cost)](#impl-cost). A combined inspection authority with stronger lien enforcement could plausibly raise gross revenue on the order of tens of millions a year, with a wide modeled range (roughly $29M to $118M/yr incremental gross, before recurring operating costs of $2.5-6M/yr) [(#net-benefit)](#net-benefit), [(#scale-up-cost)](#scale-up-cost). These are upper-bound scenarios anchored to peer programs operating today (LA collects $50-60M/yr from licensing and carries a surplus [(#peer-fees)](#peer-fees), [(#fee-surplus)](#fee-surplus)) and to Chicago's own history: the city imposed $62-75M/yr in building fines in 2010-2012 versus ~$17M today [(#fines-annual)](#fines-annual). The case for a pilot rests on that verified history and the inspection gap, not on the model's top end.

**The ask.** Three actions close the gap: adopt the risk scoring tool for inspection prioritization (no legislation needed); pass a combined-inspection ordinance creating a Building Safety Inspector credential (a cross-department role that has to be negotiated with the affected unions and drafted against the current code [(#bsi-constraints)](#bsi-constraints)); and use Chicago's existing lien and receivership authority systematically for building violations. The Healthy Homes Ordinance (passed March 18, 2026) [(#healthy-homes)](#healthy-homes) already chartered the working group this fits. The tool is open source and built from public data; CFD's practitioner feedback is what would turn it from a data-grounded prototype into an operational queue.

## Background

### What the law requires

Chicago's fire code mandates that the Fire Prevention Bureau (FPB) conduct annual inspections of all commercial, institutional, and high-occupancy properties. The OIG's October 2025 audit reviewed 27,491 buildings and 31,822 tenant spaces (59,313 inspection records in total) in FPB's database [(#fpb-count)](#fpb-count). OIG limited its review to records with at least one inspection on file in the prior 12 years; records with no inspection were excluded as potentially invalid. The actual mandated universe is therefore unknown and almost certainly larger than 59,313.

### What the OIG found

The Chicago Inspector General published an audit in October 2025 documenting gaps in fire prevention inspections:

- Only **15.8% of buildings and 17.7% of tenant spaces** received their annual inspection (16.8% combined) [(#inspect-rate)](#inspect-rate)
- **49.4% of buildings and 45.1% of tenant spaces** haven't been inspected in five or more years (47.1% combined) [(#half-uninspected)](#half-uninspected); some not in decades
- FPB had 89 budgeted positions in 2021-2024; in its response, CFD said staffing fell from 156 budgeted positions (2000) to 86 (2025), 62 of them assigned to inspection duties [(#staff-cut)](#staff-cut)
- $1.1M in re-inspection fees went uncollected over 10 years (only 13.2% collection rate) [(#fee-uncollected)](#fee-uncollected)
- Fire suppression system testing compliance: sprinklers 73.7%, fire pumps 79.6%, standpipes 77.8% [(#suppress-test)](#suppress-test)
- Median time between violation finding and re-check: **5.2 months** [(#recheck-delay)](#recheck-delay)
- Responsibility for maintaining a complete building inventory was contested between CFD and DOB
- Missing violation dates and disposition statuses in CFD's own records
- CFD destroyed paper inspection reports without approval from Cook County Local Records Commission

### CFD's response

The OIG made four recommendations: that CFD (1) work with the Department of Technology and Innovation (DTI) and the Department of Buildings (DOB) to identify a complete and accurate inventory of buildings subject to annual inspection, (2) establish procedures for all required inspections, (3) create a progress-monitoring process, and (4) standardize recordkeeping [(#cfd-response)](#cfd-response).

CFD largely disagreed with the inventory recommendation. In its formal response it took the position that the official register of buildings is DOB's responsibility, not CFD's, citing MCC 14A-6-602.4, and that "CFD stands ready to participate in any improvement efforts DOB elects to pursue" [(#cfd-response)](#cfd-response). On several of the monitoring and testing recommendations, CFD responded that its third-party compliance engine (the Brycer system, which the audit itself calls "The Compliance Engine") already issues the deficiency notices the OIG sought, so in CFD's view "no corrective action could be taken." Whether that system actually closes the gaps the audit documents is a fair question, and exactly the kind of question CFD's own practitioners are best placed to answer. What the audit establishes regardless is the underlying gap: there is no validated, shared inventory of the buildings subject to annual inspection, and most of those that OIG could review are not being inspected on schedule. This is a recurring pattern across Chicago departments: the OIG identifies a gap and recommends action; the department disagrees or points elsewhere; the gap persists. The tools described here are meant to give the working group a concrete way to break that cycle.

## Findings

### Finding 1: Chicago's inspection throughput runs far below comparable cities

With about 17% compliance (15.8% of buildings, 17.7% of tenant spaces) and a small inspection workforce, the natural question is whether the gap is a staffing problem or a systems problem. The honest answer is some of both, and the comparison to NYC shows why the tractable near-term lever is systems.

| City | Inspectors | Inspections/yr | Annual compliance | Source |
| ---- | ---------- | -------------: | ----------------- | ------ |
| NYC (FDNY) | ~400 | 250,000+ | not published | [(#nyc-inspection)](#nyc-inspection) |
| **Chicago (CFD)** | **86 budgeted, 62 inspecting** | **9,971** | **16.8%** | [(#inspect-rate)](#inspect-rate) |
| San Francisco | -- | -- | 93% of apartments (2017) | [(#sf-inspection)](#sf-inspection) |
| Portland | ~13 companies | -- | ~100% biennial | [(#portland-inspection)](#portland-inspection) |
| NFPA workload guideline (1982) | -- | 500-600 / inspector | -- | [(#nfpa-benchmark)](#nfpa-benchmark) |

The clearest sourced comparison is raw throughput. NYC's Bureau of Fire Prevention has roughly 400 inspectors and conducts more than 250,000 inspections a year [(#nyc-inspection)](#nyc-inspection), about 12 per inspector per week. Chicago completed 9,971 annual inspections in the 12 months before the OIG's data pull, 16.8% of the 59,313 records OIG reviewed [(#throughput)](#throughput). Spread across FPB's inspection workforce (86 budgeted positions in 2025, of which CFD says 62 are assigned to inspection duties; 89 budgeted during the 2021-2022 window OIG measured), that is on the order of 2 to 3 inspections per inspector per week, with on-duty fire companies performing a further share on top of FPB's own work [(#throughput)](#throughput). The two counts are not perfectly commensurable: NYC's total includes re-inspections while Chicago's compliance count excludes them, so this comparison understates Chicago's total activity and, if anything, overstates the gap. Even after that caveat the gap is large, on the order of four to five times under any reasonable choice of denominator.

This is a throughput figure, not a verdict on individual inspectors. It is an organizational coverage rate that folds in travel, paperwork, and scheduling overhead, derived from annual totals rather than observed individual output [(#throughput)](#throughput). Read that way it measures the same quantity NYC's number does, and Chicago's is a small fraction of it.

Two cautions keep this honest. First, the compliance data is a snapshot: the 16.8% covers the 12 months ending November 2022, when OIG pulled FPB's records [(#fpb-count)](#fpb-count). CFD attributes part of the shortfall to the COVID-era suspension of in-service company inspections, which it resumed in 2024. But 47.1% of the reviewed records had gone five or more years without an inspection as of that November 2022 pull [(#half-uninspected)](#half-uninspected), so most of the backlog predates the pandemic; COVID deepened a gap that already existed. Second, NYC is not a picture of full compliance. Its own auditors found 49,834 overdue annual inspections, reported that FDNY estimated needing 30% more inspectors to clear the backlog, and noted FDNY "did not implement automated inspections and optimized routing as intended" [(#nyc-backlog)](#nyc-backlog). That cuts two ways: added capacity is part of any real fix, and the inventory, risk targeting, and routing that NYC has only partly deployed are exactly the systems with the most room to run. The 1982 NFPA workload guideline of 500-600 inspections per inspector per year (roughly 10-12 a week) is the historical yardstick [(#nfpa-benchmark)](#nfpa-benchmark); Chicago runs at about a fifth to a third of it [(#nfpa-pct)](#nfpa-pct), though NFPA has since replaced fixed productivity numbers with a community-risk-based methodology. At even the low end of that old guideline, the same 86 inspectors would complete roughly 45,000 inspections a year, about three-quarters of the records OIG reviewed, instead of one-sixth [(#nfpa-coverage)](#nfpa-coverage).

### Finding 2: A public-data inventory finds roughly 3x the buildings OIG could review

The most basic tool other cities use is a building inventory: which buildings exist, what condition are they in, and when were they last inspected. The OIG recommended one. It has not been built.

Using three public datasets (1.99M building violations, permits, and 311 service complaints), I constructed an inventory of 340,573 Chicago buildings with a public footprint in any of those sources, then classified each by use type from its permit work-description text. Of the 340,573, roughly **81,351 fall into the use types the annual-inspection mandate targets** (commercial, industrial, multi-unit residential, and assembly) [(#inventory)](#inventory). That is roughly 3x the 27,491 buildings OIG was able to review [(#fpb-count)](#fpb-count). The comparison is not exact: OIG reviewed a curated sample (records with at least one inspection in a 12-year window), and the 81,351 is an approximation built from keyword classification of permit text, not a validated building register. But the order of magnitude is the OIG's central operational finding made visible: the count of in-scope buildings visible in routine public data is far larger than the set FPB could show the auditors.

**How solid is the 81,351?** The use-type classification is approximate. It is assigned from keywords in each building's permit work-description text, so a single-family home with a permit to "erect a 2-car frame garage" can be tagged industrial, and the pipeline applies no building-height filter even though the fire-code mandate turns partly on height and occupancy [(#fire-code)](#fire-code). The industrial category (41,740 buildings) is almost certainly inflated by this. The 81,351 should be read as a use-type approximation that brackets the true in-scope universe, not a precise count; validating it against the county assessor's building-characteristics data is the obvious next step before the figure carries any load-bearing weight. What the approximation establishes is directional and robust to the classification error: the in-scope stock is a multiple of what FPB has on file, which is the gap the OIG flagged.

Of the 81,351 OIG-scope buildings, **47,227 (58%)** fall into at least one of five risk buckets [(#total-flagged)](#total-flagged):

| Bucket | OIG-scope flagged | All use types | What It Identifies |
| ------ | ----------------: | ------------: | ------------------ |
| Black Holes | ~40,700 | ~40,700 | Zero building-violation records, OIG-scope building type [(#black-holes)](#black-holes) |
| Chronic Failures | ~2,900 | ~9,400 | 5+ severe violations, still unresolved [(#chronic)](#chronic) |
| Ticking Clocks | ~1,600 | ~6,800 | Severe history + 10yr+ inspection gap [(#ticking)](#ticking) |
| Community Alerts | ~1,700 | ~8,400 | 2+ 311 complaints in 3 years [(#alerts)](#alerts) |
| Open & Forgotten | ~2,300 | ~11,400 | 10+ open violations + 10yr+ gap [(#forgotten)](#forgotten) |
| **Total unique** | **~47,000** | **~69,000** | Black Holes is OIG-scope by design; other buckets include both OIG-scope and non-OIG-scope buildings [(#total-flagged)](#total-flagged) |

The Black Holes bucket flags OIG-scope buildings with zero building-violation records in the public city datasets used here. These datasets contain no CFD fire-inspection records at all, so a zero here means no public evidence of attention (no violation, and the building reached the inventory only through a permit or 311 record), not a confirmed absence of any inspection ever performed. The OIG audit's separate finding (that ~83% of mandated buildings are not receiving annual inspections) strongly implies a large share of these are genuinely uninspected, but the bucket is defined by the absence of a violation record, not by a confirmed absence of inspection. A building that was inspected without producing a violation could appear here.

These counts are approximate and shift slightly as the city updates its data. The order of magnitude and relative proportions are stable. See `bucket_summary.csv` for exact counts from the most recent run.

The tool also generates daily route plans for inspectors. Given a starting location and a number of stops, it selects the highest-priority buildings across all five categories and orders them to minimize travel time between stops.

### Finding 3: Building fines are imposed but rarely collected

A risk scoring tool tells inspectors where to go. But inspection alone doesn't fix buildings. Enforcement does. Chicago's current enforcement model has a structural weakness that other cities have already addressed.

Chicago imposes fines through administrative hearings where the *person* is summoned. In 2023-2024, roughly 68% of building violation cases ended without the owner engaging. About 24% were default judgments (respondent never appears, average fine $2,932 imposed but rarely collected). Another 44% were non-suits (case dropped entirely, average fine $10) [(#non-engage)](#non-engage). Judgments are entered against the person, not the property. When a building is sold, the buyer gets a clean slate.

The scale of uncollected debt reflects how long non-engagement has accumulated. Three different totals are visible in public data, each measuring something different: building-related fines alone total $827M imposed since 2006 [(#fines-total)](#fines-total); the administrative hearing system as a whole (all departments, not just buildings) carries $3.1B in uncollected debt [(#debt-hearing)](#debt-hearing); citywide unpaid fines, fees, and debts (including water bills, parking tickets, and other obligations beyond the hearing system) total $8.2B [(#debt-total)](#debt-total). These three do not nest simply: $827M is imposed (collected-or-not), $3.1B is uncollected only within admin hearings, $8.2B is uncollected across all city collection systems. They are shown together to convey the scale at which non-collection has accumulated, not to sum.

Fire code violations are nearly absent from the hearing system. Only about 30 cases linked to fire prevention appear among 829,000+ admin hearing records, all tagged as "Buildings" department rather than "Fire" [(#cfd-absent)](#cfd-absent). The only documented CFD enforcement revenue is roughly $14,500/yr in re-check fees at a 13.2% collection rate (OIG).

Other cities attach fines to the *property* [(#peer-gaps)](#peer-gaps):

| City | Mechanism | How It Works |
|------|-----------|-------------|
| NYC | ERP / AEP / 7A | City repairs hazards, costs become property lien. Worst buildings get court-appointed administrator. |
| LA | REAP | Tenants pay rent to city escrow until violations are fixed. Owners lose rental income. |
| DC | Proactive inspections + liens | Violations become property liens. Collected at sale or refinancing. |
| Chicago | Admin hearings | Owner summoned. ~68% never engage (default or non-suit). Fines go uncollected. |

Today's enforcement level is not a baseline. It is a departure from historical norms.

In 2010-2012, Chicago imposed $62-75M/yr in building fines across 65,000-68,000 cases [(#fines-annual)](#fines-annual). In 2013, the Code Enforcement budget was cut by 29% [(#enforcement-cut)](#enforcement-cut) and DOB priorities shifted toward permit streamlining. Citywide, 2,150+ vacant positions were eliminated as part of broader budget restructuring [(#2012-budget)](#2012-budget).

The effects were immediate. Cases filed dropped 30% and average fines dropped 36% [(#enforcement-cut)](#enforcement-cut). The non-suit rate (cases dropped before hearing) rose from 26% to 37% [(#fines-annual)](#fines-annual). A 2018 OIG audit found a backlog of 5,000+ open complaints dating back to 2013 [(#oig-complaints)](#oig-complaints). Enforcement has not recovered. Today's $17M/yr is 57% below the pre-2013 average of ~$40M/yr, even as case counts are starting to return [(#fines-annual)](#fines-annual).

NYC's own data points the same way. Person-attached DOB penalties collect at about 28%; property-attached water and sewer charges collect at roughly 80% [(#nyc-rates)](#nyc-rates). The two are not a clean controlled comparison: water and sewer charges collect well partly because they carry utility-shutoff leverage and ride into tax-lien sales, mechanisms a building fine lacks. But the direction matches what NYC's own Independent Budget Office concluded when it recommended making DOB penalties lienable, estimating on the order of +$100M/yr in additional collection [(#nyc-ibo)](#nyc-ibo).

### Finding 4: Five departments, five legal authorities, one building

Even with better targeting and enforcement, the inspection system itself is fragmented. Five separate departments hold legal authority over distinct conditions in the same buildings (fire, structure, lead, environmental, habitability), each operating under its own Municipal Code chapter, with no mechanism to share findings or combine visits [(#five-depts)](#five-depts). The fragmentation here is in legal authority, not necessarily in observed site visits: I did not measure how often all five departments actually send overlapping inspections to the same address. What is clear is that, by code, no inspector currently has cross-department authority, so any one visit can address only one slice of building safety.

| Department | Inspects | Legal Authority |
|------------|----------|----------------|
| CFD | Fire exits, sprinklers, alarms | MCC 15-4 (Fire Code, Title 14F) |
| DOB | Building code, structural | MCC Title 14A (building code) |
| CDPH | Lead paint, mold, environmental | MCC 7-4, 7-28 |
| BACP | Business-license conditions | MCC Title 4 |
| DOB/Housing | Habitability, heat, water | MCC 5-12 and building property-maintenance provisions |

The chapter citations above are a high-level map, not drafting language: the 2019-2022 recodification moved the building and fire codes into Titles 14A and 14F, and some conditions (habitability in particular) are enforced through housing-court and private-tenant remedies rather than a single inspection chapter, so a combined-inspection ordinance would have to be drafted by the Law Department against the current codified provisions [(#five-depts)](#five-depts).

A fire inspector standing in a daycare, shelter, or single-room-occupancy building, all within the annual-inspection scope, who sees peeling lead paint or black mold has no legal authority to cite either. Most of an inspector's time is spent traveling between buildings. If an inspector is already on-site, adding checklists from other departments costs little additional time. The added training is modest, though one row carries a state-licensing caveat:

| Checklist | Training | Items |
|-----------|----------|-------|
| Fire safety | Existing | Exits, detectors, sprinklers, extinguishers |
| Housing | 2 days | Heat, water, pests, windows, wiring |
| Lead paint | 1 day | Visual screen and referral only (citable lead inspection requires IDPH licensure) |
| Environmental | 1 day | Mold, standing water, ventilation |

These departments employ roughly 140 inspectors whose work falls within the scope a combined Building Safety Inspector credential would cover [(#pool-size)](#pool-size). "Overlapping" here means overlapping legal scope (fire/structure/lead/environmental/habitability conditions in the same buildings), not a measured count of duplicate site visits.

CFD has 62 actively conducting inspections (of 86 total FPB positions). The Department of Buildings has approximately 40 building and construction inspectors (31 plus 9 supervisors), with another 26 inspector-titled positions in non-overlapping specialties (elevators, boilers, plumbing, electrical). CDPH has roughly 39 building-related staff across building inspection, sanitation, environmental, and supervisory roles.

Cross-training this existing pool is the core of the proposal: create a "Building Safety Inspector" credential, paired with an ordinance recognizing cross-department inspection authority. These are checklists, not specialized engineering [(#cross-train)](#cross-train).

Three implementation constraints have to be named up front [(#bsi-constraints)](#bsi-constraints). First, FPB's inspectors are sworn firefighters in a bargaining unit (Local 2); changing their duties is a mandatory subject of collective bargaining under the Illinois Public Labor Relations Act, so a combined-inspection role has to be negotiated, not simply assigned by ordinance. Second, a new job classification is created through the city's classification plan and the annual appropriation ordinance, not by amending the substantive Municipal Code chapters that define each inspection authority; the credential and the cross-authority ordinance are separate legislative acts. Third, lead-hazard inspection in Illinois is a state-licensed activity (an IDPH-approved course, a state exam, and annual licensure), so the one-day lead module yields a visual screen and a referral, not citable lead-inspection authority; any environmental checklist with its own licensing regime carries the same caveat. None of these blocks combining inspections, and peer cities have done it, but each is a step the proposal has to budget and plan for rather than wave past.

The **Healthy Homes Ordinance** (passed City Council March 18, 2026) creates a working group to design a proactive rental inspection system [(#healthy-homes)](#healthy-homes). That working group's mandate crosses department boundaries. It needs a building inventory, risk-based prioritization, and route planning. The tool described here provides all three.

### Finding 5: The economics favor action

Can a combined inspection authority pay for itself? The peer city evidence and Chicago's own historical enforcement data suggest it can.

**Phase 1, pilot implementation cost (Year 1):**

| Item | Cost | Notes |
|------|-----:|-------|
| Cross-training | $190K | 86 inspectors x 1 week x $114K avg salary / 52 wks. Salary time only; one-time. |
| Program design & pilot | $75K | Curriculum, certification, pilot in 2-3 wards. One-time. |
| Program coordinator | $110K | 1 FTE to manage rollout, track metrics. Recurring, not one-time. |
| Data integration | $35K | Dashboard, city IT connection. Tool itself is open source. |
| **Phase 1 total** | **~$410K** | [(#impl-cost)](#impl-cost) |

The $410K is a deliberately lean pilot figure and a lower bound. It prices cross-training as straight salary time for the 86 FPB inspectors only; it excludes employee fringe (typically 30-40% on top of salary), overtime or backfill for the inspection week lost to training, and the eventual cost of training the roughly 54 additional DOB and CDPH inspectors in the combined pool. A fully loaded Phase 1 is more realistically in the $0.5-0.8M range, and the coordinator line is recurring rather than one-time [(#impl-cost)](#impl-cost). The cross-training count also inherits the 86-vs-62 question from Finding 1: if only ~62 FPB inspectors are active, the training line shrinks, but so does the throughput base the pilot is trying to lift. Phase 1 covers pilot activities only (cross-training, routing the tool through city IT, a bounded pilot in 2-3 wards); it does not cover the systems and enforcement staffing required for Phase 2 (combined-inspection ordinance) or Phase 3 (property-lien enforcement).

**Phase 2-3 scale-up costs (if ordinances pass):**

| Item | One-time | Recurring | Notes |
|------|---------:|----------:|-------|
| Legal drafting (ordinance, 5 MCC chapters) | $100-300K | n/a | Internal law dept or external counsel |
| IT build beyond pilot dashboard | $500K-2M | $200-500K/yr | Inspection queue, mobile inspector app, integrations |
| Collections infrastructure | n/a | $1-3M/yr | Staff + systems for 4-6x fine volume |
| Lien administration | n/a | $500K-1M/yr | Property-attached enforcement workflow |
| Hearing / appeals capacity | n/a | $500K-1.5M/yr | Volume increase handling |
| **Phase 2-3 total (range)** | **$600K-2.3M one-time** | **~$2.5-6M/yr** | [(#scale-up-cost)](#scale-up-cost) |

These are planning-grade estimates based on comparable municipal IT and enforcement program scopes; actual costs depend on scope, staffing model, and procurement path, and would be refined during the pilot. The recurring Phase 2-3 operating cost ($2.5-6M/yr) is the figure that needs to be subtracted from the gross revenue projections below to convert "projected incremental gross revenue" into a true net fiscal benefit.

For context, the city spends $83M per year on police tort judgments alone [(#cpd-tort)](#cpd-tort). Phase 1 costs less than 0.5% of that. Even the high end of Phase 2-3 recurring cost ($6M/yr) would be less than 10% of that single line item.

**Capacity gains from the tool alone** (no legislative change required):

- Route optimization: literature suggests +20-40% inspections/day in comparable field service contexts [(#route-opt)](#route-opt)
- Risk prioritization (buckets): proactive targeting literature suggests +25-50% violations found per visit [(#risk-target)](#risk-target)
- Blind spot elimination: more than 40,000 buildings with no inspection-generated public record enter the queue

Current throughput is roughly 190 inspections per week organization-wide [(#throughput-now)](#throughput-now). At 50% of the 1982 NFPA workload guideline, the same 86 inspectors could reach roughly 430 per week; at the full guideline, roughly 860 per week [(#nfpa-cap)](#nfpa-cap). These are capacity illustrations against a superseded guideline, not forecasts.

**Revenue model: gross uplift only, before recurring operating costs** (modeled scenarios based on city data, OIG audit, and peer city actuals):

The figures below are projected incremental gross revenue, not net benefit. They subtract today's revenue baseline but do not subtract the recurring operating costs of running a combined authority (collections staff, legal process, lien administration, billing, hearings, appeals, and enforcement overhead). Treat them as upper-bound revenue scenarios that establish whether the proposal is plausibly self-funding and worth a pilot, not as a hard fiscal forecast a city budget office could book.

Current building enforcement fines average ~$17M/yr imposed (2023-2025 average). That is 57% below the pre-2013 average of ~$40M/yr and far below the 2010-2012 peak of $62-75M/yr [(#fines-annual)](#fines-annual). Those higher levels were achieved with fewer tools and no risk-based targeting.

Actual Chicago collection rates are unknown; no collections-level payment data is published. The estimated 28-34% range uses the NYC IBO person-attached analogue (28%) as the lower bound and the inverse of the ~68% non-engagement rate as the upper bound. At those rates, current enforcement revenue is an estimated ~$5-6M [(#fines-annual)](#fines-annual).

| | Today | Tool Only (est.) | Combined Authority (est.) | Combined + Liens (est.) |
|--|------:|----------:|-------------------:|------------------:|
| Inspectors | 86 (fire) | 86 (optimized) | ~140 (cross-trained) [(#pool-size)](#pool-size) | ~140 |
| Fines imposed | ~$17M | ~$25-35M | ~$60-100M | ~$60-100M |
| Collection rate | est. 28-34% | est. 28-34% | est. 28-34% | est. 60-80% |
| Fine revenue | ~$5-6M | ~$7-12M | ~$17-34M | ~$36-80M |
| Suppression test fees | <$0.1M | ~$0.5-1.5M | ~$0.5-3.4M [(#suppress-rev)](#suppress-rev) | ~$0.5-3.4M |
| Licensing fees (cost recovery) | $0 | $0 | $15-41M [(#peer-fees)](#peer-fees) | $15-41M |
| **Total gross revenue** | **~$5-6M** | **~$8-14M** | **~$33-78M** | **~$52-124M** |
| **Incremental gross uplift** | -- | **+$2-8M** | **+$27-72M** | **+$45-118M** |

*Every figure except the "Today" column is a modeled estimate, not an observed value. The collection-rate inputs are the largest single source of uncertainty: they are NYC analogues, not measured Chicago rates. The "Tool Only" fines-imposed range ($25-35M) applies a route-optimization range (+20-40%) [(#route-opt)](#route-opt) and a risk-targeting range (+25-50%) [(#risk-target)](#risk-target) drawn from the literature, not from a measured Chicago pilot. The "Combined Authority" and "Combined + Liens" fines-imposed range ($60-100M) uses the pre-2013 historical level ($62-75M/yr) as the lower bound; the upper bound is a scenario, not a calibrated forecast. Licensing-fee revenue in the peer cities is structured as cost recovery: it funds the inspection program rather than adding net general revenue, so that row should be read as program funding, not surplus. The suppression-fee line is a range because the $3.4M end assumes full compliance and collection against an actual ~$14,500/yr today [(#suppress-rev)](#suppress-rev). The "Incremental gross uplift" row is a gross revenue projection; recurring operating costs of a combined authority are not modeled, so it should not be read as net fiscal benefit. See Notes [(#net-benefit)](#net-benefit), [(#per-inspector)](#per-inspector) for input assumptions and sensitivity.*

**Peer city licensing revenue** (these programs are operating today, not hypothetical) [(#peer-fees)](#peer-fees):

| City | Fee/Unit/Year | Units | Annual Revenue | Notes |
|------|-------------:|------:|---------------:|-------|
| LA (SCEP) | $67.94 | ~880K | ~$50-60M | Running since 1998; $54M trust fund surplus |
| Toronto (RentSafeTO) | $30.82 CAD | ~362K | ~$11M CAD | Full cost recovery; 66 staff funded by fees |
| Portland | $70 | ~120K | ~$4-5M | Accumulated $20.7M surplus in 5 years |
| DC | ~$17.50/yr | ~180K | ~$3M | New program (Law 25-141, 2024) |
| **Chicago (est.)** | **$25-68** | **~500-600K** | **$15-41M** | **No program exists** |

**Backlog recovery (estimate, not forecast):** $3.1B in existing admin hearing debt [(#debt-hearing)](#debt-hearing). At an estimated 5-20% recovery via property liens, that would be a one-time $155-620M [(#backlog)](#backlog). The 5-20% range is a planning estimate; actual recovery depends on debt age, debtor solvency, lien implementation costs, and political will, none of which are modeled here.

**Scaling phases:**

| Phase | Inspectors | Coverage | Decision Point |
|-------|-----------|----------|---------------|
| Pilot | 86 (existing CFD) | Fire only, route-optimized | Measure actual gains vs. baseline |
| Combine | ~140 (cross-trained CFD+DOB+CDPH) | Fire + housing + lead + environmental | Measure combined inspection ROI |
| License | ~140 + licensing program | Full proactive, fee-funded | Licensing fees cover all program costs |
| Expand | 170-220 | Citywide, hire based on ROI | Each hire could generate an estimated ~$250-890K/yr in gross revenue vs ~$114K salary, before recurring program costs [(#per-inspector)](#per-inspector) |

### Finding 6: Peer cities have already solved these problems

The revenue projections above are modeled estimates. The underlying programs are not hypothetical; they are operating today. Some have outcome figures that are independently documented in audits and peer-reviewed research; others appear in program descriptions and trade press but are not independently confirmed in public evaluation documents. The table below tags each row by evidence strength so the strongest claims are not propped up by the weakest figures [(#peer-results)](#peer-results):

| Program | Result | Evidence | Source |
| ------- | ------ | -------- | ------ |
| Rochester proactive inspection | 85% decline in childhood lead poisoning | confirmed | NLC, Shelterforce, peer-reviewed (Korfmacher et al., EHP 2012) |
| Syracuse TOP pilot | 57.7% compliance vs 39.5% citywide | confirmed | Results for America |
| ChangeLab multi-city review | 2-4x more violations found (proactive vs complaint) | literature signal | ChangeLab Solutions, 2022 |
| UK selective licensing (BMJ) | Depression -12%, antisocial behavior -15% | confirmed | Petersen et al., BMJ Open, 2022 |
| LA SCEP | habitability-complaint reduction (range cited as ~15%) | partially confirmed | LA Controller audit (2018); specific 15% figure not located in public evaluation |
| Singapore SCDF | Fire death rate ~0.04-0.08/100K vs US ~1.1/100K | confirmed (multi-year average) | SCDF Annual Statistics; NFPA |
| NCHH combined inspections | approx. +30% violation detection, -20% inspection burden | literature signal (specific figures not confirmed in public NCHH publications) | NCHH program-level material |
| NYC FDNY risk targeting | approx. +20-25% serious violations found per inspection | literature signal (figure appears in FDNY program descriptions, not independently audited in public docs) | GovTech, Columbia Case Consortium |
| Toronto combined inspections | approx. 15-20% labor-hour savings | literature signal (specific range not confirmed in available City of Toronto reports) | City of Toronto / RentSafeTO materials |

No US city has fully consolidated fire, housing, and health inspection into one visit [(#no-consolidated)](#no-consolidated). The Grenfell Tower fire (a combustible-cladding and building-regulation failure) and the Ghost Ship warehouse fire (an unpermitted, never-inspected assembly space) are the most-cited cases of what fragmented oversight can miss; both are extreme events from other jurisdictions, invoked for the mechanism, not as Chicago analogues. Chicago's own fire deaths are near historic lows and have fallen for decades, from roughly 50-plus a year before the early 1990s, into the 20s through the 2000s, to a record-low 16 in 2013 [(#chicago-fire-deaths)](#chicago-fire-deaths), driven mainly by smoke alarms, EMS, and suppression improvements. The case for closing the inspection gap does not rest on a fire-death spike. It rests on a mandated safety system operating at roughly one-sixth of its required rate, which is a risk and a compliance failure whether or not it has yet produced a headline fire.

**Chicago has not yet adopted the enforcement mechanisms peer cities use:**

| Capability | NYC | LA | Toronto | Chicago |
|-----------|-----|-----|---------|---------|
| Proactive inspection | AEP (250/yr) | SCEP (~107K properties) | RentSafeTO | **No proactive rental/fire program** |
| Combined inspections | No | Partial (SCEP) | Yes | **None** |
| Risk-based targeting | FDNY RBIS | No | Scoring | **None** |
| Property liens | ECB -> lien | Code liens | Court orders | **Authority exists (65 ILCS 5/1-2.1-8); recording not systematic** |
| Rent escrow | 7A receivership | REAP | Court admin | **None** |
| Receivership | Article 7A | No | Yes | **Exists (65 ILCS 5/11-31-2); used reactively** |
| Building inventory | Yes | SCEP database | RentSafeTO | **No validated FPB inventory (OIG)** |

The risk scoring tool fills one row (building inventory + risk targeting). Some of the rest already exists in Illinois law and is underused (property liens and receivership); the proactive-inspection and combined-inspection rows are what require new legislation [(#peer-gaps)](#peer-gaps).

## Recommendations

### Can start now (no legislation required)

**To the Chicago Fire Department and the Department of Technology and Innovation:**

1. **Adopt the risk scoring tool for inspection prioritization.** The tool runs on public data, is open source, and can be operated by existing IT staff. Validate the methodology against CFD's internal inspection records. (OIG audits programs and would be the right body to review adoption later, not to operate the tool.)
2. **Publish monthly inspection metrics** modeled on NYC's public inspection dashboard, establishing a baseline before and after tool adoption.

**To the Healthy Homes Working Group:**

3. **Use this building inventory and risk analysis as input to the proactive rental inspection system design.** The data platform is ready.

### Requires Council action

**To City Council:**

1. **Introduce a combined inspection ordinance** creating the "Building Safety Inspector" credential, with cross-department inspection authority spanning the fire, building, lead, environmental, and habitability provisions of the Municipal Code (Titles 14F/15-4, 14A, 7-4, 7-28, and 5-12); the exact chapters to be fixed by the Law Department in drafting, and the role to be negotiated with the affected bargaining units [(#bsi-constraints)](#bsi-constraints).
2. **Use property-lien enforcement for building violations more systematically.** Illinois law already provides administrative-judgment liens (65 ILCS 5/1-2.1-8) and municipal receivership (65 ILCS 5/11-31-2); the gap is systematic recording and use, not missing authority. NYC's own data shows property-attached charges collect far better than person-attached penalties, though the two are not a clean controlled comparison [(#nyc-rates)](#nyc-rates), and its IBO estimated material additional collection from making penalties lienable [(#nyc-ibo)](#nyc-ibo). A scoped legal analysis (whether home rule reaches NYC-style in-rem attachment) is the first step.
3. **Establish a rental licensing fee program** modeled on LA SCEP or Portland's program to fund proactive inspection at full cost recovery.

Recommendations 2 and 3 are housing-policy directions informed by peer-city evidence (NYC IBO, LA SCEP, Portland), not conclusions this investigation verified at the same depth as the fire-inspection findings; they are offered as the direction the evidence points, for the working group and Council to develop [(#peer-gaps)](#peer-gaps).

### FOIA requests to close open questions

- CFD's internal inspection tracking system: compare against public city data for completeness
- Department-by-department response to OIG non-compliance findings over the past 12 years

## Pilot measurement plan

The Healthy Homes working group should require the following before endorsing the tool and six-month check-in metrics to decide whether to scale.

**Baseline to capture before pilot starts:**

- Current weekly inspections per FPB inspector (from CFD internal data, not OIG derivation)
- Share of FPB's mandated records last inspected >5 years ago
- Annual share of inspections that result in a violation finding
- Fine imposition rate per inspector-hour (fines recorded per scheduled inspection)

**Six-month check-in metrics:**

- Change in inspections per inspector per week (tool vs baseline)
- Number of Black Holes buildings resolved (first-ever inspection completed) in the pilot wards
- Violations found per inspection in pilot wards vs non-pilot wards
- Daily tool usage: share of pilot inspectors using the routed queue vs self-routing
- Median inspector travel time per inspection day (from route telemetry)

**Twelve-month go / no-go metrics:**

- Change in annual compliance rate within the pilot wards
- Change in imposed fine volume and collection rate (if any enforcement changes were made)
- Cross-department coverage: share of pilot buildings receiving combined-checklist inspections (if ordinance passed)
- Administrative cost per inspection completed (ratio of Phase 1 program cost to throughput)

The working group should publish baseline, six-month, and twelve-month numbers. A pilot that cannot show meaningful change on at least inspections-per-week and Black Holes-resolved should not scale.

---

## Methodology

### Data sources

Three Socrata datasets form the building inventory:

- Building Violations: `22u3-xenr` (1.99M rows, 1M+ since 2006)
- Building Permits: `ydr8-5enu` (65K+/year since 2006)
- 311 Service Requests: `v6vf-nfxy` (filtered to fire/building types)

Enforcement analysis uses Ordinance Violations: `awqx-tuwv` (829,000+ records). Inspector staffing from Budget Positions: `wd4x-2xf8`.

### Pipeline

| Step | Script | What It Does |
|------|--------|-------------|
| 1 | `01_fetch.py` | Downloads 3 datasets from Socrata |
| 2 | `02_normalize.py` | Cleans, deduplicates, canonicalizes Chicago addresses |
| 3 | `03_build_inventory.py` | Joins datasets into building inventory (1 row/building) [(#inventory)](#inventory) |
| 4 | `04_score.py` | Assigns buildings to 5 risk buckets with within-bucket ranking |
| 5 | `05_report.py` | Generates `INSPECTION_PRIORITY_REPORT.md` organized by bucket |
| 6 | `06_route.py` | Optimizes inspector routes (haversine distance + OR-Tools TSP) |

### Scoring design: buckets over composite scores

A single composite risk score creates surveillance bias: frequently inspected buildings accumulate violations and score high, while never-inspected buildings score zero. The OIG's core concern (~49,000 uninspected buildings) would rank *last* under a composite score. Buckets separate fundamentally different problems (never-inspected vs. chronic failure vs. community concern) with tailored ranking criteria within each bucket.

### Compliance-first, not prediction-first

Existing fire risk tools (Firebird/Atlanta, CMU Metro21/Pittsburgh, SF Brigade) try to predict which buildings will have fires. CFD needs something different: "Which of my 59,313 buildings should my 86 inspectors visit tomorrow?" This is an inspection gap + risk factor scoring problem, not a fire occurrence prediction problem. Compliance-first scoring doesn't require fire incident data (which Chicago doesn't publish on Socrata). It uses violation history, inspection dates, building characteristics, and 311 complaints to rank overdue buildings by risk.

| Tool | City | Status | Approach | Limitation |
|------|------|--------|----------|------------|
| [Firebird (Georgia Tech)](https://github.com/DSSG-Firebird) | Atlanta | Unmaintained (R, 8 commits, 2016) | SVM on static building features, 71% TPR | Only scored 5K of 8K properties; assumes inventory exists |
| [CMU Metro21 Fire Risk](https://www.cmu.edu/metro21/projects/smart-infrastructure/fire-risk-analysis.html) | Pittsburgh | Deployed on city servers | XGBoost, 88% accuracy | Proprietary deployment; commercial only |
| [SF Brigade Fire Risk](https://github.com/sfbrigade/datasci-firerisk) | SF | Dormant since 2018 | ML prediction, F1=0.67 | Incomplete, never deployed |
| [Chicago Food Inspections](https://github.com/Chicago/food-inspections-evaluation) | **Chicago** | Deployed, open source | ML prioritization of restaurant inspections | Same city, same data. **Never applied to fire** |

### Denominators are conservative

Every percentage here computed against OIG's 59,313 reviewed records understates the true gap. OIG narrowed its review to buildings and tenant spaces with at least one inspection on file in a 12-year window; records with no inspection were excluded as potentially invalid, because FPB has no validated building inventory (that absence is OIG's central operational finding). The full mandated universe is therefore unknown and almost certainly larger than 59,313. When the figures here say 16.8% compliance, 2 to 3 inspections per inspector per week, or ~75% projected coverage at the 1982 NFPA guideline, the underlying state of the world is at least this bad, and likely worse. The 81,351 OIG-scope buildings visible in public data (Finding 2) is one indicator of how much larger the real universe may be.

### Data freshness and what is committed

Of the pipeline artifacts the Notes reference, only `route.csv` is committed to this report directory. The larger intermediates (`scored_buildings.csv`, `bucket_*.csv`, `bucket_summary.csv`) are excluded by `.gitignore` to keep the repository light and are regenerated by running the pipeline (see Reproducibility). The bucket counts cited in the Notes are recorded in the committed Hydra run logs under `runs/` (for example `runs/04_score_2026-03-28_18-17-30/`), produced on **2026-03-28** from the Socrata datasets listed above. So the `grep`/`wc` commands in the Notes run against a freshly generated `scored_buildings.csv`, not a file already in the published tree; a reader who wants a bucket count without re-running the pipeline can read it from the run log. Socrata refreshes continuously, so a fresh run produces slightly different counts; the order of magnitude and relative proportions are stable.

### Validation

7 buildings were checked against the live Socrata API. Raw violation counts matched exactly for all 7 [(#api-check)](#api-check). Pipeline counts for each bucket are checked by automated tests against broad ranges to accommodate Socrata data refreshes; the subset of tests that read pipeline-output CSVs are skipped on a clean checkout (those files are gitignored) and run only after the pipeline is regenerated, while the Socrata-query and derived-math tests run against live data with no regeneration needed.

**Throughput methodology note:** The per-inspector throughput in Finding 1 (roughly 2 to 3 inspections per inspector per week) is a derived organizational proxy (annual inspections divided by workforce and weeks), not a directly observed per-inspector measurement. It reflects an effective coverage rate that includes systemic overhead (travel, paperwork, scheduling) and folds in inspections performed by on-duty fire companies as well as FPB. The comparison to NYC's ~12/week is directional: NYC's count includes re-inspections while Chicago's counts only first annual-compliance inspections, so the gap is real but its exact size is uncertain [(#throughput)](#throughput).

## Notes

Verification tests (27 tests: Socrata live queries, pipeline output, derived math)

Verification types: `quote` (fetch source, match text), `derived` (check math from referenced notes), `run` (execute and check result), `estimate` (human judgment or modeled scenario, not mechanically verifiable).

<a id="nfpa-benchmark">**nfpa-benchmark.**</a> **Fire inspection productivity guideline** = 500-600 inspections per full-time inspector per year (~10-12/week)
Verification: derived (weekly figure is conversion: 500-600 / 50 working weeks)
Source: NFPA, *Fire Inspection Management Guidelines* (1982), pp. 9.1-9.4, as cited in USFA Executive Fire Officer Program papers (EFO38814, EFO47321). Note: this is a 1982 management guideline, not a current consensus standard. NFPA 1730 (2019) replaced fixed productivity numbers with a community-risk-based staffing methodology. The 500-600/year figure remains widely cited in fire service literature as a reasonable workload expectation. · VERIFIED (as historical guideline)

<a id="nyc-inspection">**nyc-inspection.**</a> **NYC FDNY inspection throughput** = ~400 inspectors, 250,000+ inspections/yr (~12 per inspector per week, derived)
Verification: quote + derived. The Comptroller audit states "BFP has approximately 400 fire inspectors and conducts more than 250,000 inspections each year." Per-inspector throughput is derived: `250,000 / 400 / 52 = 12.0/week`, a lower bound since the audit says "more than 250,000." The audit publishes no count of the buildings FDNY is mandated to inspect, so no NYC annual compliance rate and no inspector-to-building ratio can be computed from it; earlier drafts cited a 10.7/week rate, a ~78% annual rate, and a 1:714 ratio [(#ratio)](#ratio) that are not in the source and have been removed. NYC's total counts all inspection types including re-inspections, so it is not perfectly commensurable with Chicago's annual-compliance count.
Source: [NYC Comptroller Audit SI23-105A (Jan 2025)](https://comptroller.nyc.gov/wp-content/uploads/documents/SI23-105A.pdf), p.2 · VERIFIED (inspector count and inspection count quoted; per-week figure derived)

<a id="nyc-backlog">**nyc-backlog.**</a> **NYC FDNY inspection backlog** = 49,834 overdue annual inspections; FDNY estimated needing 30% more inspectors; automated inspections and optimized routing not implemented as intended
Verification: quote
Source: [NYC Comptroller Audit SI23-105A (Jan 2025)](https://comptroller.nyc.gov/wp-content/uploads/documents/SI23-105A.pdf), p.8 ("Based on an Overdue Annual Inspections report provided in May 2024, 49,834 inspections are past due"; "FDNY officials approximated that they would need to increase the number of inspectors by 30% to complete all inspections on time and resolve the backlog"; "Since FDNY did not implement automated inspections and optimized routing as intended, FDNY may not be using its resources efficiently and effectively") · VERIFIED

<a id="sf-inspection">**sf-inspection.**</a> **San Francisco inspection rate** = 93% apartment-inspection compliance (2017)
Verification: quote. Article: departments that "tasked firefighters to perform inspections in between other duties maintained higher completion rates for apartment inspections last year, among them San Francisco (93 percent)" ("last year" = 2017; the analysis covers 2010-17). An earlier draft also credited SF with "~17 inspectors" on this citation; that figure is not in the article (its only 17s are the ~17,000-building sample size) and has been removed. It likely conflated SFFD's 17 fire-inspection districts (sf-fire.org), which describe current org structure, not 2018 staffing. A prior draft also cited a dead mercurynews.com article URL; the piece is an interactive microsite at the URL below.
Source: [Thomas Peele, "Burned Out: How overwhelmed fire inspectors fail to protect us," Bay Area News Group (June 1, 2018)](http://extras.mercurynews.com/fireinspection/) ([archived](http://web.archive.org/web/20180606091931/http://extras.mercurynews.com/fireinspection/index.html)) · VERIFIED

<a id="portland-inspection">**portland-inspection.**</a> **Portland inspection rate** = ~13 district companies, approximately 100% biennial coverage
Verification: quote
Source: [Portland Fire & Rescue: How the Fire Safety Inspection Program Works](https://www.portland.gov/fire/permits-inspections/code-policies-pfrs-fire-safety-inspection-program/how-it-works); [PF&R Policy FIR-1.10: Inspection Program Frequency](https://www.portland.gov/policies/portland-fire-and-rescue/administration/fir-110-inspection-program-frequency) · VERIFIED

<a id="fire-code">**fire-code.**</a> **Annual inspection mandate** = MCC 15-4-030 (with MCC 2-36-340) requires the fire commissioner to inspect specified commercial, institutional, and high-occupancy premises annually; scope turns partly on building height and occupancy class.
Verification: quote. OIG audit p.10: "Section 15-4-030 of the Municipal Code of Chicago (MCC) requires the fire commissioner to conduct inspections of the following premises annually," noting CFD also considers MCC 2-36-340 while OIG relies on the more specific 15-4-030. The audit defines the Fire Code (per MCC 15-4-010) as Title 14F plus Chapters 2-36, 15-4, 15-8, 15-16, 15-20, 15-24, 15-26, and 15-28. The audit makes no reference to an "Illinois Fire Investigation Act" (a prior draft cited one in error); the scope thresholds it describes are height- and occupancy-based.
Source: [OIG Audit p.10; fn.1 (p.5), fn.6 (p.8)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf); [Chicago Municipal Code Title 14F / 15-4](https://codelibrary.amlegal.com/codes/chicago/latest/chicago_il/0-0-0-2657495) · VERIFIED

<a id="cfd-response">**cfd-response.**</a> **CFD management response to the audit** = CFD assigns building-register responsibility to DOB (MCC 14A-6-602.4), states it "stands ready to participate," and argues its compliance engine already issues deficiency notices
Verification: quote. OIG Recommendation 1 (p.23): CFD "should work with the relevant City departments, including the Department of Technology and Innovation (DTI) and DOB, to identify a complete and accurate inventory of existing buildings... subject to annual Fire Code inspections" (OIG asks CFD to "work with... to identify" an inventory, not to "build" one). CFD response (pp.23-24): "FPB is not responsible for identifying, creating, or maintaining an inventory of existing buildings... The official register of buildings... is created and maintained by DOB"; "CFD stands ready to participate in any improvement efforts DOB elects to pursue." CFD response (p.33): "The Brycer compliance engine is already doing this, which sends deficiency notices when the annual inspection is due... Therefore, there is no corrective action that could be taken." The OIG body calls the same system "The Compliance Engine (TCE)" (p.13).
Source: [OIG Audit pp.13, 23-24, 33](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="fpb-count">**fpb-count.**</a> **OIG-reviewed FPB records** = 59,313 total (27,491 buildings + 31,822 tenant spaces)
Verification: quote. OIG limited its review to records with active status that had received at least one inspection between January 1, 2011, and November 22, 2022 (when OIG pulled IPS 11 data). Records with no inspection were excluded as potentially invalid, since FPB has no validated building inventory (the OIG's central operational finding). The actual mandated universe is therefore unknown and almost certainly larger than 59,313; every percentage computed against the 59,313 denominator is conservative against the true gap.
Source: [OIG Audit p.19 (body and fn.21)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="inspect-rate">**inspect-rate.**</a> **Annual inspection compliance rate** = 15.8% buildings, 17.7% tenant spaces, 16.8% combined
Verification: quote. OIG: of 27,491 buildings reviewed, 15.8% received an annual inspection in the prior 12 months; of 31,822 tenant spaces, 17.7%; combined across all 59,313 records, 16.8% (the figure in the OIG's headline chart). All rates are computed against [(#fpb-count)](#fpb-count), which is OIG's reviewed sample, not the full mandated universe.
Source: [OIG Audit p.19 (Figure 6 and body; exec summary p.5)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="staff-cut">**staff-cut.**</a> **FPB staffing** = 156 budgeted (2000) to 86 (2025), 62 assigned to inspections; OIG body figure 89 budgeted (2021-2024)
Verification: quote. The 156-to-86 decline and the "62 assigned to all inspection duties" figure are from CFD's management response (p.30), not an OIG body finding: "In 2000, there were 156 budgeted positions in the FPB... In 2025, that number had been reduced to 86, of which 62 are assigned to all inspection duties." OIG's own staffing figure is 89 budgeted positions for 2021-2024 (p.10), the headcount contemporaneous with the November 2022 compliance measurement. Derived decline `(156 - 86) / 156 = 44.9%`.
Source: [OIG Audit p.30 (CFD response), p.10 (OIG body)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · test · VERIFIED

<a id="fee-uncollected">**fee-uncollected.**</a> **Re-inspection fees uncollected over 10 years** = $1.1M (13.2% collection rate)
Verification: quote. OIG p.28: 25,023 re-checks (Jan 2011-Nov 2022) at $50 each = $1,251,150 potential; "the City collected only about $165,000, or 13.2%"; Figure 11 (p.29) shows "$1.1 million unrecovered." Exec summary (p.5) states the ten-year framing.
Source: [OIG Audit pp.28-29 (exec p.5)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="suppress-test">**suppress-test.**</a> **Fire suppression testing compliance** = Sprinklers 73.7%, fire pumps 79.6%, standpipes 77.8%
Verification: quote. OIG p.31 (2022, of known premises in TCE): fire pumps 4,345 of 5,459 (79.6%), sprinklers 4,821 of 6,538 (73.7%), standpipes 1,311 of 1,685 (77.8%); also Figure 12 (p.31) and exec summary (p.6).
Source: [OIG Audit p.31 (exec p.6)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="recheck-delay">**recheck-delay.**</a> **Median time between violation finding and re-check** = 5.2 months
Verification: quote. OIG p.27: "The median length of time between a failed annual inspection and FPB's first re-check was 5.2 months"; also the Finding 2 heading (p.26) and exec summary (p.5). Mean is 9.0 months (p.27 fn.29).
Source: [OIG Audit pp.26-27 (exec p.5)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="ratio">**ratio.**</a> **Inspector-to-building ratio** = removed (not computable from sourced data)
Verification: n/a. Earlier drafts compared a Chicago "1:690" inspector-to-record ratio with a NYC "1:714." Both have been removed. NYC publishes no count of the buildings FDNY is mandated to inspect [(#nyc-inspection)](#nyc-inspection), so the 1:714 had no source; and the Chicago 1:690 used the 59,313 reviewed-record denominator that Finding 2 argues is itself far too small, which would push Chicago's true ratio well above NYC's rather than level with it. The throughput comparison [(#throughput)](#throughput) is the sourced replacement.
Source: n/a (note retained to document the removal)

<a id="throughput">**throughput.**</a> **Chicago inspection throughput vs NYC** = roughly 4x to 5x (Chicago ~2-3 per inspector per week vs NYC ~12)
Verification: derived. Chicago completed 9,971 annual inspections in the 12 months before OIG's November 2022 data pull (OIG audit p.19: "FPB had inspected only 9,971, or 16.8%," of the 59,313 reviewed records [(#fpb-count)](#fpb-count)). Per-inspector throughput depends on the denominator, and none is clean: `9,971 / 62 / 52 = 3.1/week` using the 62 positions CFD's response (p.30) says are assigned to inspection; `9,971 / 86 / 52 = 2.2/week` across all 86 budgeted positions; `9,971 / 89 / 52 = 2.2/week` across the 89 budgeted during OIG's measurement window (p.10). On-duty fire companies ("in-service inspections," 27.1% of buildings per OIG p.20) perform additional inspections not captured by dividing through FPB headcount, so a clean per-FPB-inspector rate is not strictly recoverable. NYC's ~12/week is derived from the Comptroller audit's "approximately 400 fire inspectors and conducts more than 250,000 inspections each year" (`250,000 / 400 / 52 = 12.0`) [(#nyc-inspection)](#nyc-inspection). The two are not perfectly commensurable: NYC's 250,000 includes re-inspections, while Chicago's 9,971 counts only first annual-compliance inspections, so the comparison overstates the gap. The gap stays large under any denominator: `12.0 / 2.2 = 5.5x`, `12.0 / 3.1 = 3.9x`. This is an organizational throughput proxy (annual totals ÷ workforce ÷ weeks), not observed individual output.
Source: [OIG Audit pp.19-20, p.10, p.30](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf); [NYC Comptroller Audit SI23-105A](https://comptroller.nyc.gov/wp-content/uploads/documents/SI23-105A.pdf), p.2 · test · VERIFIED

<a id="nfpa-pct">**nfpa-pct.**</a> **Chicago rate vs 1982 NFPA guideline** = roughly one-fifth to one-third
Verification: derived. At 2.2 to 3.1 inspections per inspector per week [(#throughput)](#throughput) against the 1982 guideline midpoint of ~10.5/week: `2.2 / 10.5 = 21%` to `3.1 / 10.5 = 30%`. The 1982 figure is a superseded management guideline, not a current standard; NFPA 1730 (2019) replaced fixed productivity numbers with a community-risk-based methodology [(#nfpa-benchmark)](#nfpa-benchmark).
Source: [(#nfpa-benchmark)](#nfpa-benchmark), [(#throughput)](#throughput) · test · VERIFIED

<a id="nfpa-coverage">**nfpa-coverage.**</a> **Projected coverage at the low end of the 1982 NFPA guideline** = ~75% of OIG's reviewed records annually
Verification: derived `86 inspectors * 10 inspections/week * 52 weeks = 44,720; 44,720 / 59,313 = 75.4%` (~75%). This assumes all 86 budgeted positions inspecting at the low end (10/week) of the 1982 guideline, against the 59,313 records OIG reviewed; it is a capacity illustration, not a forecast, and is the same calculation as [(#nfpa-cap)](#nfpa-cap).
Source: [(#fpb-count)](#fpb-count), [(#staff-cut)](#staff-cut), [(#nfpa-benchmark)](#nfpa-benchmark) · test · VERIFIED

<a id="inventory">**inventory.**</a> **Pipeline inventory** = 340,573 Chicago buildings with a public footprint in violations, permits, or 311 records. **OIG-scope subset** = 81,351 (buildings matching residential_multi, assembly, commercial, or industrial use types, i.e., the types the annual-inspection mandate targets).
Verification: run `wc -l data/processed/fire_risk/building_inventory.csv` (total) and filter on `building_use_type` in scored_buildings.csv (OIG-scope). Most recent: 340,573 total, 81,351 OIG-scope. Use-type breakdown of total: unknown 228,498 (67%), industrial 41,740, residential_single 30,724, commercial 20,271, residential_multi 15,921, assembly 3,419.
**Classification caveat.** Use type is assigned by first-match keyword on each building's permit work-description text (`USE_TYPE_KEYWORDS` in `src/fire_risk/config.py`), with no building-height or occupancy filter. This is approximate in two directions. It inflates some categories: keywords like "garage" and "storage" map to industrial, so a single-family home with a detached-garage permit is tagged industrial, and the 41,740 "industrial" count is implausibly large for Chicago's actual industrial stock and is the clearest symptom. It also undercounts: the 67% "unknown" share (buildings in public records without a clean use-type tag) surely hides many in-scope buildings, and the mandate's height/occupancy thresholds [(#fire-code)](#fire-code) are not applied at all. The net direction of the error is therefore uncertain, and 81,351 should be treated as an order-of-magnitude approximation, not a precise count. The only validation performed (7 buildings, [(#api-check)](#api-check)) checked violation counts, not use-type assignment. Validating the classifier against Cook County assessor building-characteristics data is the open next step.
Source: Pipeline · test · PARTIALLY VERIFIED (count reproducible from the pipeline; use-type classification is approximate and unvalidated)

<a id="black-holes">**black-holes.**</a> **Black Holes bucket count** = ~40,700 buildings with no inspection-generated public record
Verification: run `grep -c "black_holes" reports/fire-inspection-crisis/scored_buildings.csv` (exact count varies with data refresh; most recent: 40,722). The bucket flags buildings absent from violation, permit, and 311 records joined into the inventory; i.e., no observable inspection-generated public footprint, not a confirmed absence of any inspection ever performed. Given the OIG's separate finding that ~83% of mandated buildings miss their annual inspection, a large share of these are likely genuinely uninspected, but the count itself is "no observed inspection record," not "never inspected" in a strict sense.
Source: Pipeline; [OIG Audit p.19](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · test · PARTIALLY VERIFIED (count verified; "no inspection record" framing is the underlying claim, not "never inspected")

<a id="chronic">**chronic.**</a> **Chronic Failures bucket count** = ~9,400
Verification: run `grep -c "chronic_failures" reports/fire-inspection-crisis/scored_buildings.csv` (most recent: 9,392)
Source: Pipeline · test · VERIFIED

<a id="ticking">**ticking.**</a> **Ticking Clocks bucket count** = ~6,800
Verification: run `grep -c "ticking_clocks" reports/fire-inspection-crisis/scored_buildings.csv` (most recent: 6,762)
Source: Pipeline · test · VERIFIED

<a id="alerts">**alerts.**</a> **Community Alerts bucket count** = ~8,400
Verification: run `grep -c "community_alerts" reports/fire-inspection-crisis/scored_buildings.csv` (most recent: 8,396)
Source: Pipeline · test · VERIFIED

<a id="forgotten">**forgotten.**</a> **Open & Forgotten bucket count** = ~11,400
Verification: run `grep -c "open_forgotten" reports/fire-inspection-crisis/scored_buildings.csv` (most recent: 11,374)
Source: Pipeline · test · VERIFIED

<a id="total-flagged">**total-flagged.**</a> **Flagged buildings** = 47,227 OIG-scope (58% of the 81,351 OIG-scope inventory); 69,213 across all use types (~5,900 in 2+ buckets)
Verification: derived (union of bucket membership across all five buckets, intersected with OIG-scope use types for the primary figure). Exact counts in `bucket_summary.csv` plus a per-bucket scope tally. The Black Holes bucket is OIG-scope by construction (all 40,722); the other four buckets include both OIG-scope and non-OIG-scope buildings (per-bucket OIG-scope counts: Chronic Failures 2,945 of 9,392; Ticking Clocks 1,588 of 6,762; Community Alerts 1,683 of 8,396; Open & Forgotten 2,284 of 11,374).
Source: [#inventory](#inventory)-[#forgotten](#forgotten), Pipeline · VERIFIED

<a id="api-check">**api-check.**</a> **API validation of 7 buildings** = All 7 matched exactly
Verification: run. Manual Socrata API spot-checks during development. Buildings selected from each bucket to test scoring logic. Spot-check not stored as reproducible artifact.
Source: Socrata API · VERIFIED

<a id="non-engage">**non-engage.**</a> **Admin hearing non-engagement rate** = ~68% (2023-2024: default ~24%, avg fine $2,932; non-suit ~44%, avg fine $10)
Verification: run. Socrata `awqx-tuwv` aggregate query on `case_disposition`. Strict "Default" is 13.9% all-time, ~24% in 2023-2024. Non-suit ~44%. Combined ~68% of cases end without owner engaging. Note: all-time "Default" of 66% cited in OIG/Sun-Times likely includes non-suits.
Source: Socrata `awqx-tuwv`; [OIG Audit](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf); [Chicago Sun-Times (Nov 2025)](https://chicago.suntimes.com/the-watchdogs/2025/11/25/debts-unpaid-fines-chicago-city-hall-mayor-brandon-johnson) · test · VERIFIED

<a id="fines-total">**fines-total.**</a> **Building-related fines imposed** = $827M
Verification: run. Socrata aggregate query on `awqx-tuwv`
Source: Socrata `awqx-tuwv`; ENFORCEMENT_RESEARCH.md · test · VERIFIED

<a id="debt-hearing">**debt-hearing.**</a> **Uncollected administrative hearing debt** = $3.1B (up 7% since late 2023)
Verification: quote
Source: [Chicago Sun-Times (Nov 2025)](https://chicago.suntimes.com/the-watchdogs/2025/11/25/debts-unpaid-fines-chicago-city-hall-mayor-brandon-johnson) · VERIFIED

<a id="cfd-absent">**cfd-absent.**</a> **CFD fire cases in fines system** = Near-zero (~30 in 829K+)
Verification: run. Socrata query on `awqx-tuwv`. ~30 cases mention "Bureau of Fire Prevention"; all tagged `issuing_department=Buildings`, not "Fire". Only documented CFD revenue: ~$14.5K/yr re-check fees (OIG p.28: ~$165K collected over the 2011-2022 window).
Source: Socrata `awqx-tuwv`; [OIG Audit p.28](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · test · VERIFIED

<a id="debt-total">**debt-total.**</a> **Chicago total unpaid fines/fees/debts** = $8.2B (up from $6.4B in 2023)
Verification: quote
Source: [Chicago Sun-Times (Nov 2025)](https://chicago.suntimes.com/the-watchdogs/2025/11/25/debts-unpaid-fines-chicago-city-hall-mayor-brandon-johnson) · VERIFIED

<a id="nyc-rates">**nyc-rates.**</a> **NYC person vs property collection rates** = ~28% (person-attached DOB penalties) vs ~80% (property-attached water/sewer charges)
Verification: quote. The two rates are not a controlled comparison: they cover different obligations with different collection mechanics. Water and sewer charges collect well largely because they carry utility-shutoff leverage and are swept into tax-lien sales, leverage a building fine does not have. The figures show the direction of the lien effect, not a claim that attaching fines to property would by itself move building-fine collection from 28% to 80%.
Source: [NYC Independent Budget Office, 2022](https://www.ibo.nyc.ny.us/iboreports/revising-the-property-and-related-taxes-december-2022.pdf) · VERIFIED

<a id="nyc-ibo">**nyc-ibo.**</a> **NYC IBO estimate if DOB penalties lienable** = +$100M/yr additional collection
Verification: quote
Source: [NYC Independent Budget Office, 2022](https://www.ibo.nyc.ny.us/iboreports/revising-the-property-and-related-taxes-december-2022.pdf) · VERIFIED

<a id="five-depts">**five-depts.**</a> **Departments with inspection authority over conditions in the same buildings** = 5 (CFD, DOB, CDPH, BACP, DOB/Housing), each under separate Municipal Code authority
Verification: quote, with caveats. The mapping is by legal scope, not a measured count of overlapping site visits. Two caveats: the 2019-2022 recodification moved the building and fire codes into Titles 14A and 14F, so older chapter labels (such as "Chapter 13") are superseded; and Chapter 5-12 (the Residential Landlord and Tenant Ordinance) is enforced largely through private tenant remedies and housing court rather than a CDPH/DOB inspection program, while BACP's role is business-license conditions rather than building-condition inspection. A combined-inspection ordinance would need the Law Department to fix the exact operative chapters. The substantive point stands: no single inspector today holds cross-department citation authority.
Source: [Chicago Municipal Code](https://codelibrary.amlegal.com/codes/chicago/latest/overview): Title 14A (building code), Title 14F (fire code), [Ch. 7-4 (Lead-Bearing Substances)](https://codelibrary.amlegal.com/codes/chicago/latest/chicago_il/0-0-0-2640072), [Ch. 7-28 (Health Nuisances)](https://codelibrary.amlegal.com/codes/chicago/latest/chicago_il/0-0-0-2641002), [Ch. 5-12 (RLTO)](https://codelibrary.amlegal.com/codes/chicago/latest/chicago_il/0-0-0-2639041), [Ch. 15-4 (Fire Prevention)](https://codelibrary.amlegal.com/codes/chicago/latest/chicago_il/0-0-0-2657495) · PARTIALLY VERIFIED (departments and separate authority confirmed; exact post-recodification chapter citations approximate)

<a id="cross-train">**cross-train.**</a> **Cross-training time for Building Safety Inspector** = estimated 1 week (5 days: existing fire + 2 days housing + 1 day lead + 1 day environmental)
Verification: estimate, based on checklist complexity and [Toronto RentSafeTO](https://www.toronto.ca/community-people/housing-shelter/rental-housing-rights-information/housing-property-standards/apartment-building-standards/) training precedent. This is a planning estimate, not a validated operational figure. The 1-day lead component covers visual screening and referral only; full regulated lead inspection requires separate IDPH licensure [(#bsi-constraints)](#bsi-constraints), and actual training requirements would be set through a pilot.
Source: ESTIMATE

<a id="bsi-constraints">**bsi-constraints.**</a> **Implementation constraints on a combined Building Safety Inspector** = collective bargaining (sworn members), a separate classification/appropriation process, and IDPH lead licensure
Verification: quote + reference. FPB inspections-section members are sworn firefighters (OIG audit p.9), so changing their duties is a mandatory subject of bargaining under the Illinois Public Labor Relations Act (5 ILCS 315). City job classifications are established through the classification plan and the annual appropriation ordinance, separately from amending substantive code chapters. Lead-hazard inspection is licensed by the Illinois Department of Public Health under the Lead Poisoning Prevention Act (410 ILCS 45): an approved course, a state exam, and annual renewal are required to perform regulated lead inspection.
Source: [OIG Audit p.9](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf); [5 ILCS 315 (IPLRA)](https://www.ilga.gov/Legislation/ILCS/Articles?ActID=1199&ChapterID=2); [IDPH Lead Poisoning Prevention (410 ILCS 45)](https://dph.illinois.gov/topics-services/environmental-health-protection/lead-poisoning-prevention.html) · VERIFIED (statutory framework)

<a id="healthy-homes">**healthy-homes.**</a> **Healthy Homes Ordinance passage** = Passed City Council Wednesday, March 18, 2026 (Proactive Rental Inspection Working Group)
Verification: quote. Passed unanimously on Wednesday, March 18, 2026. What passed is the working-group ordinance (a study and design first step toward proactive rental inspection), not a full inspection program. An earlier draft dated this March 19, which was the Block Club Chicago publication date, not the vote date.
Source: [Better Government Association (March 18, 2026)](https://www.bettergov.org/2026/03/18/city-council-approves-proactive-rental-inspection-working-group/); [Illinois Answers (March 18, 2026)](https://illinoisanswers.org/2026/03/18/proactive-building-inspections-one-step-closer-to-reality-in-chicago-but-questions-of-funding-and-logistics-remain/) · VERIFIED

<a id="impl-cost">**impl-cost.**</a> **Phase 1 pilot implementation cost** = ~$410K (Year 1)
Verification: estimate. This is pilot scope only (cross-train existing FPB inspectors, pilot tool in 2-3 wards, basic city IT integration). Phase 2-3 scale-up costs are separately estimated at [(#scale-up-cost)](#scale-up-cost).

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| FPB inspectors | 86 | OIG Audit [(#staff-cut)](#staff-cut) | verified |
| Avg inspector salary | $114K | Socrata `wd4x-2xf8` (FFE $106K, Lt $129K, Eng $117K) | verified |
| Cross-training duration | 1 week | Planning estimate [(#cross-train)](#cross-train) | estimate |
| Program design & pilot | $75K | Planning estimate | estimate |
| Program coordinator | $110K | 1 FTE | estimate |
| Data integration | $35K | Planning estimate | estimate |

Formula: cross-training `86 × $114K / 52 = $188K` (~$190K) + $75K + $110K + $35K = **~$410K**
Sensitivity: this is salary time only and a lower bound. Adding ~35% fringe to the cross-training line raises it from ~$190K to ~$255K; overtime or backfill for the inspection week lost to training could add a comparable amount; training the ~54 additional DOB and CDPH inspectors in the combined pool is not in Phase 1; and the $110K coordinator is recurring, not one-time. A fully loaded Phase 1 is more realistically ~$0.5-0.8M. If only ~62 FPB inspectors are active [(#staff-cut)](#staff-cut), the cross-training line falls to ~$136K (salary only). If cross-training takes 2 weeks, add another ~$190K.
Source: [#staff-cut](#staff-cut); Socrata `wd4x-2xf8` · test cost; test salary · ESTIMATE

<a id="scale-up-cost">**scale-up-cost.**</a> **Phase 2-3 scale-up cost** = ~$600K-2.3M one-time + ~$2.5-6M/yr recurring
Verification: estimate. Phase 2-3 activates only if the combined-inspection ordinance and property-lien enforcement pass. These are planning-grade ranges based on comparable municipal IT and enforcement program scopes; actual costs depend on scope, staffing model, and procurement path and would be refined during the pilot.

| Item | One-time | Recurring | Basis |
|------|---------:|----------:|-------|
| Legal drafting (ordinance amending 5 MCC chapters) | $100-300K | n/a | Internal law dept or outside counsel rates for comparable multi-chapter ordinances |
| IT build beyond pilot dashboard | $500K-2M | $200-500K/yr | Inspection queue, mobile inspector app, FPB/DOB/CDPH integrations, maintenance |
| Collections infrastructure | n/a | $1-3M/yr | Staff + systems for the 4-6x fine volume implied by the revenue table; comparable to mid-sized municipal collections units |
| Lien administration | n/a | $500K-1M/yr | Property-attached enforcement workflow, title coordination, recording, release |
| Hearing / appeals capacity | n/a | $500K-1.5M/yr | Additional ALJ / clerk capacity to handle volume increase |

Implication for the revenue model: the recurring Phase 2-3 operating cost ($2.5-6M/yr) must be subtracted from the [(#net-benefit)](#net-benefit) gross revenue projections to produce a true net fiscal benefit. At the conservative scenario (~$29M incremental gross) minus ~$6M operating = ~$23M/yr net; at the optimistic scenario (~$118M) minus ~$6M = ~$112M/yr net. The proposal remains plausibly self-funding across the range, but the gross-to-net conversion is non-trivial.
Source: Planning estimate, no Chicago-specific operational data to validate against. · ESTIMATE

<a id="route-opt">**route-opt.**</a> **Route optimization impact on inspections/day** = +20-40% (literature range)
Verification: quote. Indicative range from heterogeneous sources, not a verified prediction for this specific implementation. [OptimoRoute/Telgian case study](https://optimoroute.com/optimization-inspection-services/) (fire inspection services: 82% planning efficiency gain, 70% increase in monthly inspections from ~3,000 to ~5,000); Ahn & Lee, ["Productivity Improvement of Sewer CCTV Inspection through Time Study and Route Optimization,"](https://ascelibrary.org/doi/10.1061/%28ASCE%29CO.1943-7862.0000976) *J. Construction Engineering and Management* 141(6), 2015, DOI: 10.1061/(ASCE)CO.1943-7862.0000976 (+13% from TSP alone). Actual gains in Chicago would depend on current routing efficiency and geographic distribution.
Source: [OptimoRoute/Telgian](https://optimoroute.com/optimization-inspection-services/); [ASCE JCEM 141(6)](https://ascelibrary.org/doi/10.1061/%28ASCE%29CO.1943-7862.0000976) · VERIFIED (as literature range)

<a id="risk-target">**risk-target.**</a> **Risk prioritization impact on violations found** = +25-50% (literature range)
Verification: quote. Indicative range from heterogeneous sources, not a verified prediction for this implementation. NYC FDNY risk targeting via RBIS/FireCast (+20-25% serious violations found; [GovTech, "New York City Fights Fire with Data"](https://www.govtech.com/public-safety/new-york-city-fights-fire-with-data.html); [Columbia Case Consortium: FDNY and Risk-Based Assessment](https://ccnmtl.columbia.edu/projects/caseconsortium/casestudies/127/casestudy/www/layout/case_id_127_id_887.html). Note: specific +20-25% figure not independently confirmed in public evaluation; sourced from FDNY program descriptions); [ChangeLab Solutions, *A Guide to Proactive Rental Inspections* (2022)](https://www.changelabsolutions.org/sites/default/files/2022-11/A-Guide-to-Proactive-Rental-Inspections_FINAL_20221031A.pdf) (2-4x proactive vs complaint). Different interventions, contexts, and mechanisms.
Source: [GovTech/FDNY](https://www.govtech.com/public-safety/new-york-city-fights-fire-with-data.html); [ChangeLab Solutions (2022)](https://www.changelabsolutions.org/sites/default/files/2022-11/A-Guide-to-Proactive-Rental-Inspections_FINAL_20221031A.pdf) · VERIFIED (as literature range)

<a id="nfpa-cap">**nfpa-cap.**</a> **Capacity at NFPA benchmark** = ~860 buildings/week (86 inspectors x 10/week); ~45,000/year; ~75% coverage
Verification: derived `86 * 10 = 860/week`; `860 * 52 = 44,720` (~45,000); `44,720 / 59,313 = 75.4%`
Source: [#fpb-count](#fpb-count), [#staff-cut](#staff-cut), [#nfpa-benchmark](#nfpa-benchmark) · test · VERIFIED

<a id="backlog">**backlog.**</a> **Backlog recovery from existing uncollected debt** = estimated $155-620M one-time
Verification: estimate

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Uncollected hearing debt | $3.1B | Sun-Times [(#debt-hearing)](#debt-hearing) | verified |
| Recovery rate (low) | 5% | Conservative; aged debt, many uncollectable | estimate |
| Recovery rate (high) | 20% | NYC lien collection [(#nyc-rates)](#nyc-rates) applied selectively | estimate |

Formula: `$3.1B × 5% = $155M`; `$3.1B × 20% = $620M`
Sensitivity: actual recovery depends on debt age, debtor solvency, lien implementation costs, and political will. At 10% recovery = $310M.
Source: [#debt-hearing](#debt-hearing) · test · ESTIMATE

<a id="net-benefit">**net-benefit.**</a> **Projected incremental gross revenue** = estimated $49-119M/yr (anchor key kept as `net-benefit` for backward link compatibility; the figure itself is gross revenue uplift, not a fully costed net benefit)
Verification: estimate. Modeled scenario combining multiple assumptions. None of the Combined Authority or Combined + Liens figures are observed Chicago data. The figure subtracts today's revenue baseline but does not subtract the recurring operating costs of running a combined authority (collections staff, legal process, lien administration, billing, hearings, appeals, and enforcement overhead). To convert this into a true net benefit, those recurring costs must be modeled and subtracted; that is not done here.

**Conservative scenario (Combined Authority, no liens):**

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Inspectors | ~140 | [(#pool-size)](#pool-size) | estimate |
| Fines imposed | $60M | Pre-2013 historical level ($62-75M/yr achieved with fewer tools) | verified (historical) |
| Collection rate | 28% | NYC person-attached [(#nyc-rates)](#nyc-rates) | estimate (analogy) |
| Suppression test fees | $3.4M | [(#suppress-rev)](#suppress-rev) | estimate |
| Licensing fees | $15M | Low end of Chicago extrapolation [(#peer-fees)](#peer-fees) | estimate (analogy) |
| Current baseline revenue | ~$6M | [(#fines-annual)](#fines-annual) | estimate |

Formula: `($60M × 28%) + $3.4M + $15M = $35.2M` total; incremental `$35.2M - $6M =` **~$29M/yr** (conservative)

**Optimistic scenario (Combined + Liens):**

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Fines imposed | $100M | Combined authority + risk targeting above historical peak | estimate |
| Collection rate | 80% | NYC property-attached [(#nyc-rates)](#nyc-rates) | estimate (analogy) |
| Suppression test fees | $3.4M | [(#suppress-rev)](#suppress-rev) | estimate |
| Licensing fees | $41M | High end of Chicago extrapolation [(#peer-fees)](#peer-fees) | estimate (analogy) |

Formula: `($100M × 80%) + $3.4M + $41M = $124.4M` total; incremental `$124.4M - $6M =` **~$118M/yr** (optimistic)

Note on the fines imposed range: Chicago imposed $62-75M/yr in 2010-2012 with fewer inspectors, no risk-based targeting, and no combined authority. The conservative $60M returns to that historical baseline. The optimistic $100M reflects what a combined authority with ~140 cross-trained inspectors and risk-based targeting could achieve beyond the historical peak.

Sensitivity: the single biggest lever is collection rate. At 28% (no liens), fine revenue on $60M = $17M. At 80% (with liens), fine revenue on $100M = $80M. Licensing fees are the second largest driver; at $25/unit instead of $68, licensing = ~$15M instead of $41M.
Source: [#impl-cost](#impl-cost), [#fines-annual](#fines-annual), [#peer-fees](#peer-fees), [#pool-size](#pool-size), [#suppress-rev](#suppress-rev) · test · ESTIMATE

<a id="per-inspector">**per-inspector.**</a> **Per-inspector gross revenue (combined authority)** = estimated ~$250-890K/yr vs ~$114K salary, before recurring operating costs
Verification: estimate. Gross revenue per inspector, not net contribution. Salary is one cost component; full operating costs (collections, legal, IT, hearings, lien administration) are not subtracted here. Treat as a feasibility-direction figure, not a productivity ROI.

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Total revenue (conservative) | ~$35M | [(#net-benefit)](#net-benefit) conservative scenario | estimate |
| Total revenue (optimistic) | ~$124M | [(#net-benefit)](#net-benefit) optimistic scenario | estimate |
| Inspector pool | ~140 | [(#pool-size)](#pool-size) | estimate |
| Avg inspector salary | $114K | Socrata `wd4x-2xf8` | verified |

Formula: `$35M / 140 = $250K`; `$124M / 140 = $886K` → **~$250-890K/yr per inspector** vs $114K salary
Sensitivity: inherits all [(#net-benefit)](#net-benefit) input sensitivity. Even the conservative scenario ($250K/inspector) exceeds salary ($114K) by 2.2x.
Source: [#net-benefit](#net-benefit), [#pool-size](#pool-size) · test · ESTIMATE

<a id="no-consolidated">**no-consolidated.**</a> **No US city has fully consolidated fire + housing + health inspection** = Zero fully consolidated; partial examples exist
Verification: quote. [ChangeLab Solutions, *A Guide to Proactive Rental Inspections* (2022)](https://www.changelabsolutions.org/sites/default/files/2022-11/A-Guide-to-Proactive-Rental-Inspections_FINAL_20221031A.pdf) survey found no US jurisdiction with single-credential inspectors covering fire + housing + environmental. This is a best-available literature review conclusion. Partial overlap exists: LA SCEP covers housing+habitability but not fire; Syracuse TOP combines some inspections but not fire safety; Rochester proactive inspections are housing-focused. Toronto RentSafeTO is closest (fire+building+health) but is Canadian.
Source: [ChangeLab Solutions (2022)](https://www.changelabsolutions.org/sites/default/files/2022-11/A-Guide-to-Proactive-Rental-Inspections_FINAL_20221031A.pdf); [NCHH, *How to Make Proactive Rental Inspection Effective*](https://nchh.org/resource-library/how-to-make-proactive-rental-inspection-effective.pdf) · VERIFIED (as literature review)

<a id="grenfell">**grenfell.**</a> **Grenfell Tower deaths and cause** = 72 deaths, June 14 2017; combustible cladding, fragmented inspection
Verification: quote
Source: [Grenfell Tower Inquiry Phase 2 Report (Sept 2024)](https://www.grenfelltowerinquiry.org.uk/) · VERIFIED

<a id="ghost-ship">**ghost-ship.**</a> **Ghost Ship deaths and cause** = 36 deaths, Dec 2 2016; never inspected for fire safety, departmental silos
Verification: quote
Source: [Oakland Fire Department Origin and Cause Report (June 2017)](https://dam.clarionengage.com/content/dam/fe/online-articles/documents/2017/oakland-ca-ghost-ship.pdf); [Ghost Ship warehouse fire, Wikipedia](https://en.wikipedia.org/wiki/Ghost_Ship_warehouse_fire) (compiled from ATF/OFD/Alameda County Arson Task Force investigation) · VERIFIED

<a id="chicago-fire-deaths">**chicago-fire-deaths.**</a> **Chicago civilian fire deaths** = near historic lows; decades-long decline (record-low 16 in 2013; ~25/yr average 2009-2018; 50-plus/yr before the early 1990s)
Verification: quote. No clean published year-by-year CFD civilian-death series exists; the strongest sourced anchors are the Fire Commissioner's statement that 2013's 16 fatalities were "the lowest annual total ever recorded," with totals "normally in the 20s" through the 2000s and "usually in the 50-plus range" before 1993 (DNAinfo, Jan 2014), and a ~25/yr average across 2009-2018 (NFIRS-derived). National context: NFPA reports the US home fire death rate fell from 23.0 per million (1980) to 8.6 per million (2024). A precise recent single-year Chicago total would require a CFD or Cook County Medical Examiner pull; the directional claim (near historic lows, not rising) is well supported.
Source: [DNAinfo (Jan 7, 2014)](https://www.dnainfo.com/chicago/20140107/downtown/chicago-fire-deaths-at-record-low-2013-department-says/); [NFPA, Fire Loss in the United States](https://www.nfpa.org/education-and-research/research/nfpa-research/fire-statistical-reports/fire-loss-in-the-united-states) · VERIFIED (directional)

<a id="peer-gaps">**peer-gaps.**</a> **Chicago lags peer-city enforcement mechanisms** = 7 capabilities compared; Chicago lacks the proactive/combined-inspection and rent-escrow mechanisms and underuses the lien and receivership powers it already has
Verification: derived. Comparison table from NYC, LA, Toronto program documentation. Correction from earlier drafts: Illinois law does provide municipal receivership (65 ILCS 5/11-31-2, first-priority receiver's certificates), which Chicago uses reactively through the Troubled Buildings Initiative, and administrative-judgment liens (65 ILCS 5/1-2.1-8). The gap on those rows is systematic use and recording, not the absence of a statute.
Source: [NYC HPD Alternative Enforcement Program (AEP)](https://www.nyc.gov/site/hpd/services-and-information/alternative-enforcement-program-aep.page); [NYC HPD Emergency Repair Program (ERP)](https://www.nyc.gov/site/hpd/services-and-information/emergency-repair-program-erp.page); [LA REAP (Rent Escrow Account Program)](https://housing.lacity.gov/residents/reap); [Toronto RentSafeTO](https://www.toronto.ca/community-people/housing-shelter/rental-housing-rights-information/housing-property-standards/apartment-building-standards/); [65 ILCS 5/11-31-2](https://www.ilga.gov/Legislation/ILCS/Articles?ActID=802&ChapterID=14); Chicago Troubled Buildings Initiative (CIC, cicchicago.com) · VERIFIED (peer programs); CORRECTED (Illinois receivership and lien statutes exist)

<a id="peer-results">**peer-results.**</a> **Peer city program outcomes** = measured results from 9 programs across proactive inspection, combined inspection, risk targeting, and licensing
Verification: quote. Each result from its cited source.

- Rochester lead poisoning decline (85%): [NLC Q&A: Mayor Lovely Warren on Rochester's Leadership to Address Healthy Housing (2020)](https://www.nlc.org/article/2020/02/10/qa-mayor-lovely-warren-on-rochesters-leadership-to-address-healthy-housing-and-a-call-to-action/); [Shelterforce, "The Mission: End Childhood Lead Poisoning in Rochester" (2018)](https://shelterforce.org/2018/11/13/the-mission-end-childhood-lead-poisoning-in-rochester/); [Korfmacher et al., "Rochester's Lead Law," *Environmental Health Perspectives* 120(2), 2012](https://pmc.ncbi.nlm.nih.gov/articles/PMC3279433/).
- Syracuse TOP (57.7% vs 39.5%): [Results for America, Proactive Home Inspection Syracuse](https://catalog.results4america.org/case-studies/proactive-home-inspection-syracuse); [Innovate Syracuse, TOP Pilot Results](http://www.innovatesyracuse.com/blog/top-pilot-results).
- ChangeLab review (2-4x proactive vs complaint): [ChangeLab Solutions, *A Guide to Proactive Rental Inspections* (2022)](https://www.changelabsolutions.org/sites/default/files/2022-11/A-Guide-to-Proactive-Rental-Inspections_FINAL_20221031A.pdf).
- NCHH combined inspections (+30% violation detection, -20% inspection burden): [NCHH, *How to Make Proactive Rental Inspection Effective*](https://nchh.org/resource-library/how-to-make-proactive-rental-inspection-effective.pdf); [NCHH Proactive Rental Inspections resource page](https://nchh.org/resources/policy/proactive-rental-inspections/) (specific +30%/-20% figures not confirmed in available NCHH publications; these may derive from program-level reports not publicly indexed; treat as approximate literature range rather than verified statistic).
- UK selective licensing (depression, antisocial behavior): [Petersen et al., "Impact of selective licensing schemes for private rental housing on mental health and social outcomes in Greater London, England," *BMJ Open* 12(12), 2022](https://pmc.ncbi.nlm.nih.gov/articles/PMC9791445/), DOI: 10.1136/bmjopen-2022-065747.
- NYC FDNY risk targeting (+20-25%): [GovTech, "New York City Fights Fire with Data"](https://www.govtech.com/public-safety/new-york-city-fights-fire-with-data.html); [Columbia Case Consortium: FDNY and Risk-Based Assessment](https://ccnmtl.columbia.edu/projects/caseconsortium/casestudies/127/casestudy/www/layout/case_id_127_id_887.html) (specific percentage not confirmed in public evaluation documents; sourced from FDNY program descriptions).
- Toronto combined inspections (15-20% labor hour savings): [RentSafeTO Year in Review 2023](https://www.toronto.ca/wp-content/uploads/2024/02/8e04-RentSafeTO-Year-in-Review-2023.pdf); [RentSafeTO Update Report (2024)](https://www.toronto.ca/legdocs/mmis/2024/ph/bgrd/backgroundfile-244590.pdf) (specific 15-20% labor savings figure not confirmed in available City of Toronto reports; treat as approximate estimate).
- LA SCEP (habitability complaints reduction): [LA Controller Audit on Systematic Code Enforcement Program (2018)](https://controller.lacity.gov/audits/audit-on-systematic-code-enforcement-program); [LAHD SCEP program page (Inspections and Fees)](https://housing.lacity.gov/rental-property-owners/inspections-and-fees) (specific "15% reduction" figure not found in public UCLA Luskin evaluation; LA Controller audit is the primary evaluation source).
- Singapore SCDF (fire death rate): [SCDF Annual Statistics](https://www.scdf.gov.sg/home/about-scdf/media-room/publications/annual-statistics); [Singapore Fire Injuries and Fatalities data (data.gov.sg)](https://data.gov.sg/datasets/d_2c81b575edc555f6c8f0cb7e09c8df02/view) (5 deaths in 2024 among ~5.9M population = ~0.08/100K; the 0.04 figure is a multi-year average). US comparator ~1.1 per 100,000, from [NFPA, Fire Loss in the United States](https://www.nfpa.org/education-and-research/research/nfpa-research/fire-statistical-reports/fire-loss-in-the-united-states) (11.0 civilian fire deaths per million population in 2023, 11.5 in 2024). So the US rate is on the order of 14x Singapore's, a large gap but an order-of-magnitude comparison, not a precise ratio.

Source: Sources as listed per program · VERIFIED (as literature review; NCHH +30%/-20%, FDNY +20-25%, Toronto 15-20%, and LA 15% figures flagged as not independently confirmed in public documents)

<a id="enforcement-cut">**enforcement-cut.**</a> **2013 Code Enforcement budget cut and effects** = DOB Code Enforcement budget cut 29% ($3.8M to $2.7M, 2011-2013). Cases filed dropped 30% (66,312 to 46,111). Average fines dropped 36% ($948 to $606). Non-suit rate rose from 25.9% to 37.0%.
Verification: run + quote. Budget figures from Chicago budget data. Case counts, fines, and disposition rates from Socrata `awqx-tuwv` year-over-year comparison (2012 vs 2013). DOB Commissioner Michael Merchant (2011-2013) prioritized permit streamlining (E-Plan, Small Business Center); replaced by Felicia Davis (Dec 2013).
Source: Socrata `awqx-tuwv`; [Mayor Emanuel 2012 Budget Proposal](https://www.chicago.gov/city/en/depts/mayor/press_room/press_releases/2011/october_2011/mayor_rahm_emanueloutlines2012budgetproposaltosecurechicagosfutu.html); [Sun-Times: Emanuel scaled back environmental enforcement](https://chicago.suntimes.com/2019/2/22/18362156/under-mayor-rahm-emanuel-city-has-sharply-scaled-back-environmental-enforcement); [Felicia Davis appointed DOB Commissioner (Dec 2013)](https://www.chicago.gov/city/en/depts/mayor/press_room/press_releases/2013/december_2013/mayor-emanuel-names-felicia-davis-commissioner-of-the-department.html) · VERIFIED

<a id="2012-budget">**2012-budget.**</a> **2012 citywide position eliminations** = 2,150+ vacant positions eliminated, 385 layoffs
Verification: quote
Source: [Mayor Emanuel 2012 Budget Proposal (Oct 2011)](https://www.chicago.gov/city/en/depts/mayor/press_room/press_releases/2011/october_2011/mayor_rahm_emanueloutlines2012budgetproposaltosecurechicagosfutu.html) · VERIFIED

<a id="oig-complaints">**oig-complaints.**</a> **2018 OIG audit: 5,000+ open complaints dating to 2013** = DOB met response deadlines for only 36.5% of complaints. Backlog of 5,000+ open complaints dating back to 2013. More than 2,000 complaints summarily closed without addressing "plainly hazardous situations."
Verification: quote
Source: [OIG Audit of DOB Complaint-Based Inspections (April 2018)](https://igchicago.org/2018/04/10/dob-complaint-based-inspections-audit/) · VERIFIED

<a id="fines-annual">**fines-annual.**</a> **Annual building enforcement fines baseline** = ~$17M/yr imposed; estimated ~$5-6M collected
Verification: run + estimate

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Fines imposed (2023) | $17.9M | Socrata `awqx-tuwv` | verified |
| Fines imposed (2024) | $17.3M | Socrata `awqx-tuwv` | verified |
| Fines imposed (2025) | $16.9M | Socrata `awqx-tuwv` | verified |
| Pre-pullback avg (2006-2012) | ~$40M/yr | Socrata `awqx-tuwv` | verified |
| Peak years (2010-2012) | $62-75M/yr | Socrata `awqx-tuwv` | verified |
| Collection rate (low) | 28% | NYC IBO person-attached DOB [(#nyc-rates)](#nyc-rates) | estimate (analogy) |
| Collection rate (high) | 34% | Inverse of ~68% non-engagement [(#non-engage)](#non-engage) | estimate (derived) |

Formula: `~$17M × 28% = ~$4.8M`; `~$17M × 34% = ~$5.8M` → **~$5-6M collected**
Sensitivity: **actual Chicago collection rate is unknown**; no payment data in Socrata. If true rate is 15%, collected = ~$2.6M. If 40%, collected = ~$6.8M.
Source: Socrata `awqx-tuwv`; [NYC IBO 2022](https://www.ibo.nyc.ny.us/iboreports/revising-the-property-and-related-taxes-december-2022.pdf) · test · PARTIALLY VERIFIED (imposed fines verified; collection rate estimated)

<a id="peer-fees">**peer-fees.**</a> **Peer city licensing fee revenue** = LA SCEP ~$50-60M/yr ($67.94/unit, ~880K units); Toronto RentSafeTO ~$11M CAD ($30.82 CAD/unit, ~362K units); Portland ~$4-5M/yr ($70/unit, $20.7M surplus in 5 yrs); DC ~$3M/yr ($35/unit biennial, ~180K units)
Verification: quote. [LA Controller audit](https://controller.lacity.gov/audits/audit-on-systematic-code-enforcement-program) (avg $41M revenue at old $43.32 rate; $54M trust fund surplus); [Toronto 2024 Budget Briefing Note BN#28](https://www.toronto.ca/community-people/housing-shelter/rental-housing-tenant-information/rental-housing-standards/apartment-building-standards/rentsafeto-for-building-owners/rentsafeto-fees-and-fines/); [Portland City Council resolution](https://www.portland.gov/council/documents/resolution/priority-allocations-207-million-rental-services-office-funds) on $20.7M unspent funds; [DC Law 25-141](https://code.dccouncil.gov/us/dc/council/laws/25-141). Chicago estimate ($15-41M) is an extrapolation from these programs to Chicago's ~500-600K rental units (an analogy, not a verified Chicago fact). The range pairs the low fee with the low unit count and the high fee with the high count: `$25/unit × ~500K units = $12.5M` to `$68/unit × ~600K units = $40.8M`; the low end is rounded up to ~$15M and intermediate pairings fall inside the band.
Source: LA Controller; Toronto MLS budget; Portland City Council; DC Council · VERIFIED (peer cities); ESTIMATE (Chicago extrapolation)

<a id="fee-surplus">**fee-surplus.**</a> **Peer city licensing programs generate surplus, not just cost recovery** = LA SCEP accumulated $54M trust fund surplus; Portland accumulated $20.7M unspent in ~5 years
Verification: quote. [LA Controller audit (May 2018)](https://controller.lacity.gov/audits/audit-on-systematic-code-enforcement-program) found avg $41M revenue vs $37M expenditure = ~$4M/yr surplus; [Portland resolution](https://www.portland.gov/council/documents/resolution/priority-allocations-207-million-rental-services-office-funds) explicitly addresses $20.7M accumulated surplus
Source: LA Controller; Portland City Council · VERIFIED

<a id="pool-size">**pool-size.**</a> **Combined inspector pool** = ~140 inspectors doing overlapping building work
Verification: run + estimate. CFD: 62 on inspection (per CFD's response to the audit, p.30). DOB: ~40 building/construction inspectors (31 inspectors + 9 supervising, from 70 total inspector-title positions out of 156 DOB positions, excluding elevator, boiler, plumbing, electrical, cooling, ventilation specialists). CDPH: ~39 (14 building + 17 sanitarian II + 5 environmental + 3 supervising). Socrata Budget Positions `wd4x-2xf8` query verified for title counts. The "~140 doing overlapping work" framing is an operational estimate of how many currently inspect buildings where a combined credential would apply.
Source: Socrata `wd4x-2xf8`; [OIG Audit](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · test DOB; test CDPH · PARTIALLY VERIFIED (title counts verified; pool estimate is operational judgment)

<a id="suppress-rev">**suppress-rev.**</a> **Suppression test fee potential** = estimated ~$3.4M/yr
Verification: estimate

| Input | Value | Source | Status |
|-------|------:|--------|--------|
| Tests per year | 11,549 | OIG p.32: 57,745 over 5 years (2018-2022) | verified |
| Sprinkler fee | $300 | Municipal Code §15-16-210 | verified |
| Fire pump fee | $315 | Municipal Code §15-16-1160 | verified |
| Standpipe fee | $50 | Municipal Code §15-16-1170 | verified |
| Weighted avg fee | ~$290 | Weighted toward sprinkler/pump | estimate |
| Compliance rate assumed | 100% | Full compliance and collection | **assumption** |
| Current actual collection | $14.5K/yr | OIG (13.2% of fees owed) | verified |

Formula: `11,549 × $290 = $3.35M` → **~$3.4M/yr at full compliance**
Sensitivity: full compliance is an upper bound. Current collection is $14.5K/yr, a 230x gap. Realistic range is $0.5-3.4M depending on enforcement. At 50% compliance, ~$1.7M.
Source: [OIG Audit p.32 (test counts), p.28 (collections)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf); Municipal Code fee schedule · test · ESTIMATE

<a id="half-uninspected">**half-uninspected.**</a> **Records uninspected 5+ years** = 47.1% combined (49.4% buildings, 45.1% tenant spaces)
Verification: quote. OIG audit p.19, body text: "FPB had not inspected 27,957, or 47.1% of the buildings and tenant spaces in at least five years." The combined figure (`27,957 / 59,313 = 47.1%`) is the load-bearing number. The building/tenant split (13,590 of 27,491 buildings = 49.4%; 14,367 of 31,822 tenant spaces = 45.1%) appears in OIG Figure 7 and is arithmetically consistent with the 27,957 total, but those per-category counts live inside the chart image, not the body text. Measured as of OIG's November 2022 data pull; some buildings not inspected in decades. All percentages computed against [(#fpb-count)](#fpb-count), OIG's reviewed sample, not the full mandated universe.
Source: [OIG Audit p.19; Figure 7 (p.20)](https://igchicago.org/wp-content/uploads/2025/10/Audit-of-CFDs-Annual-Fire-Prevention-Inspections-and-Tests.pdf) · VERIFIED

<a id="cpd-tort">**cpd-tort.**</a> **CPD annual tort budget** = $83M (FY2026)
Verification: quote. Chicago FY2026 budget, Department of Law / Police tort line items. Used for scale comparison only.
Source: [Civic Federation, "Trends in Chicago Police Department Spending"](https://www.civicfed.org/blog/trends-chicago-police-department-spending) (CPD has budgeted $82.6M for legal judgments annually since 2019); [CCPSA Report on Proposed CPD Budget for 2026](https://ccpsa.chicago.gov/wp-content/uploads/2025/11/CCPSA-Report-on-Proposed-CPD-Budget-for-2026-2.pdf) · VERIFIED

<a id="throughput-now">**throughput-now.**</a> **Current inspection throughput** = ~190 inspections/week (organization-wide)
Verification: derived `9,971 annual inspections / 52 weeks = 191.8` (~190/week) [(#throughput)](#throughput). This is an organization-wide weekly rate counting inspection records (buildings and tenant spaces), not buildings, and not a per-inspector figure.
Source: [(#throughput)](#throughput) (OIG) · test · VERIFIED (arithmetic); see [(#throughput)](#throughput) for throughput caveat

## Reproducibility

Pipeline: `src/fire_risk/`

Commands (generate artifacts + Hydra run dirs into this report directory):

```bash
REPORT=reports/fire-inspection-crisis
uv run python src/fire_risk/01_fetch.py verify_only=true 'hydra.run.dir='$REPORT'/runs/01_fetch_${now:%Y-%m-%d_%H-%M-%S}'
uv run python src/fire_risk/02_normalize.py 'hydra.run.dir='$REPORT'/runs/02_normalize_${now:%Y-%m-%d_%H-%M-%S}'
uv run python src/fire_risk/03_build_inventory.py 'hydra.run.dir='$REPORT'/runs/03_inventory_${now:%Y-%m-%d_%H-%M-%S}'
uv run python src/fire_risk/04_score.py output_dir=$REPORT 'hydra.run.dir='$REPORT'/runs/04_score_${now:%Y-%m-%d_%H-%M-%S}'
uv run python src/fire_risk/05_report.py input_dir=$REPORT output_dir=$REPORT 'hydra.run.dir='$REPORT'/runs/05_report_${now:%Y-%m-%d_%H-%M-%S}'
uv run python src/fire_risk/06_route.py input_dir=$REPORT output_dir=$REPORT start=city_hall 'hydra.run.dir='$REPORT'/runs/06_route_${now:%Y-%m-%d_%H-%M-%S}'
```

Datasets:

- Building Violations: `22u3-xenr` (1M+ rows since 2006)
- Building Permits: `ydr8-5enu` (65K+/year since 2006)
- 311 Service Requests: `v6vf-nfxy` (filtered to fire/building types)

Output: `reports/fire-inspection-crisis/` (artifacts + `runs/` with Hydra config/logs)
