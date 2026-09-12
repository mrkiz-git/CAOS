# FORWARD EXPECTATIONS — FULL DEEP AUDIT — 2026-09-11

## Inputs Consulted
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-11_DEEPAUDIT]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[03_AGENT_RUNS/03_FORWARD/FORWARD_2026-09-11_001]]

Primary evidence was rechecked through current company investor-relations releases and SEC filings linked below. The ten-candidate audit set is CEG, KTOS, ISRG, CRDO, MOD, AXON, ONDS, CIFR, VRT, and AVGO.

## Audit state and evidence limits

- **VERIFIED FACT:** The current funded holdings are NVDA, MSFT, GOOGL, TSLA, IREN, and WULF. The broker screenshot is less than one day old.
- **DATA LIMITED:** All 16 prices are off-hours observations. The Ledger has conflicting cash values, an empty fill section, and a stale NVDA average cost. The Active Handoff Snapshot still exposes 2026-09-02 states and does not contain the Ledger's newer 2026-09-10 handoffs.
- **CAOS INFERENCE:** Forward research can continue, but no price-sensitive sizing or execution conclusion is valid from this file.
- **DATA LIMITED:** No consistent primary-source analyst-rating database exists. Analyst changes are therefore not used as authority. Where secondary reports mention a rating change, it remains an `UNVERIFIED LEAD` and does not alter a company gate.

## Funded holdings

### NVIDIA — NVDA

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | AWS announced deployment of 2m additional NVIDIA GPUs through Q2 FY2029; economics and cancellation terms are not disclosed. | VERIFIED FACT / DATA LIMITED |
| Nonbinding guidance | Q3 FY2027 revenue **$108bn ±2%**, gross margin **74.0% ±0.5 points**, operating expense about **$9.2bn GAAP / $9.0bn non-GAAP**; no China Data Center compute revenue assumed. | VERIFIED FACT |
| Target/aspiration | Management expects about **70% FY2028 revenue growth** and says Rubin is in full production. | VERIFIED FACT that stated; nonbinding |
| CAOS inference | The guide is stronger evidence than long-range AI-factory language. Margin and China exclusion make Q3 directly falsifiable. | CAOS INFERENCE |

**Surprise/change:** Q2 revenue was $96.2bn and Data Center $89.0bn, with 75.0% gross margin; the new Q3 guide implies further growth but slight margin compression. **Next gate:** Q3 FY2027 filing: revenue **$105.84bn-$110.16bn**, margin **73.5%-74.5%**, and transparent China treatment. [Primary source](https://investor.nvidia.com/news/press-release-details/2026/NVIDIA-Announces-Financial-Results-for-Second-Quarter-Fiscal-2027/default.aspx)

### Microsoft — MSFT

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Commercial RPO **$678bn**; about **30%** expected as revenue within 12 months. Contract modifications remain possible. | VERIFIED FACT |
| Nonbinding guidance | FY2027 double-digit revenue and operating-income growth; margin down less than one point; Q1 capex above **$50bn**; cloud margin roughly stable from 65%. | VERIFIED FACT |
| Target/aspiration | FY2027 capex to grow year over year; calendar-2026 capex about **$175bn** after lease-accounting mix change. | VERIFIED FACT that stated |
| CAOS inference | RPO conversion and cloud margin must validate the return on the spending ramp. | CAOS INFERENCE |

**Surprise/change:** FY2026 Q4 Azure grew 43% and RPO grew 84%; the capex presentation changed because more leases are operating leases, so old capex comparisons need normalization. **Next gate:** FY2027 Q1 filing: capex >$50bn, cloud margin near 65%, continued Azure growth, and RPO conversion consistent with the 30% twelve-month expectation. [Primary source](https://www.microsoft.com/en-us/investor/events/fy-2026/earnings-fy-2026-q4)

### Alphabet — GOOGL

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Revenue backlog **$519.5bn**, of which **$513.9bn** is Cloud; just over half expected to convert within 24 months. Uncommenced data-center leases total **$85.2bn**. | VERIFIED FACT |
| Nonbinding guidance | Technical-infrastructure investment is expected to rise significantly in 2026; precise full-year capex guidance is not present in the reviewed 10-Q text. | VERIFIED FACT / DATA LIMITED |
| Target/aspiration | Just over half of 2026 ML compute was expected to support Cloud. | VERIFIED FACT that stated |
| CAOS inference | Backlog must convert faster than depreciation, lease, debt, preferred-dividend, and dilution costs. | CAOS INFERENCE |

**Surprise/change:** Q2 Cloud revenue accelerated to 82%; the company also raised substantial common and mandatory-convertible capital for AI infrastructure. **Next gate:** Q3 2026 filing: Cloud backlog/conversion, Cloud growth and margin, start/timing of the disclosed $5.8bn Q3 lease, and updated capex funding. [Primary 10-Q](https://www.sec.gov/Archives/edgar/data/1652044/000165204426000071/goog-20260630.htm)

### Tesla — TSLA

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | No material binding Cybercab, Robotaxi, Optimus, or vehicle-delivery commitment was found. | UNKNOWN |
| Nonbinding guidance | 2026 capex expected above **$25bn**. | VERIFIED FACT |
| Target/aspiration | Cybercab production and road testing began; management is preparing for large-scale Optimus production, without binding volume or revenue dates. | VERIFIED FACT that stated / DATA LIMITED |
| CAOS inference | Operational progress does not yet prove commercial fleet scale, regulatory reach, unit economics, or material revenue. | CAOS INFERENCE |

**Surprise/change:** Cybercab moved from preparation to early production/testing, but measurable commercial commitments remain absent. **Next gate:** Q3 2026 deliveries and 10-Q: deliveries, paid Robotaxi miles/metropolitan coverage, Cybercab deployed units or production rate, and capex progress versus >$25bn. [Primary Q2 filing](https://ir.tesla.com/_flysystem/s3/sec/000162828026049270/tsla-20260630-gen.pdf)

### IREN — IREN

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Microsoft contract about **$9.7bn through 2031**, four tranches, 20% prepayment, and delivery acceptance/termination protections. Reported contracted ARR is **$4bn** for 2026 capacity. | VERIFIED FACT |
| Contracted financing | $3.6bn GPU facility plus prepayments funds a stated **96%** of Microsoft GPU capex; $2.8bn other GPU financings support other customers. | VERIFIED FACT |
| Nonbinding target | Horizon 2 commissioning and Horizons 3-4 targeted for Q4 2026; cumulative capacity target **0.3GW in 2026 / 0.8GW in 2027**. | VERIFIED FACT that stated |
| Aspiration/inference | >5GW pipeline is not delivered capacity. ARR is not recognized revenue; acceptance and post-financing cash are decisive. | VERIFIED FACT that stated / CAOS INFERENCE |

**Surprise/change:** Horizon 1 was delivered; $1bn ARR was reported operating. The old “unfinanced Microsoft capex” framing is superseded, though delivery and cash conversion remain open. **Next gate:** next quarterly filing/Q4 2026 update: Horizon 2 acceptance, Horizons 3-4 delivery, progress to 0.3GW, recognized AI revenue consistent with operating ARR, and no weakening of financing. [Primary FY2026 results](https://www.sec.gov/Archives/edgar/data/1878848/000187884826000051/irenreportsfy26results.htm)

### TeraWulf — WULF

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Anthropic 20-year lease covers about **401MW** and **$19bn** initial-term revenue; Google credit support of **$600m** became effective for Fluidstack obligations after CB-3 conditions. | VERIFIED FACT |
| Nonbinding target | CB-4 phased delivery/rent in H2 2026; CB-5 in Q1 2027; 438MW contracted capacity energized by H1 2027. | VERIFIED FACT that stated |
| Target/aspiration | Contract 250-500MW annually; cost guidance **$8m-$10m/critical IT MW**. Later gigawatt sites remain contingent. | VERIFIED FACT that stated / aspiration |
| CAOS inference | The pivot already produces HPC revenue. Delivery schedule, retained project cash, leverage, and tenant remedies are the live tests. | CAOS INFERENCE |

**Surprise/change:** Q2 included $31.9m HPC lease revenue and CB-3 activated credit support, contradicting stale “no HPC revenue” framing. **Next gate:** Q3 filing or earlier CB-4 notice: rent commencement in H2 2026, cost within $8m-$10m/MW, and unchanged Fluidstack/Google protections; CB-5 remains a Q1 2027 gate. [Primary Q2 results](https://investors.terawulf.com/news-events/press-releases/detail/144/terawulf-reports-second-quarter-2026-results)

## Active Seeds, Challengers, and top-ten candidate set

### Constellation Energy — CEG

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | 920MW of new long-term power agreements and the Calpine acquisition are completed/disclosed; exact AI-linked economics remain limited. | VERIFIED FACT / DATA LIMITED |
| Nonbinding guidance | 2026 adjusted operating EPS **$11.50-$12.50**, raised at Q2. | VERIFIED FACT |
| Target/aspiration | Crane nuclear restart and additional clean-power contracting are long-cycle targets, subject to regulation and execution. | VERIFIED FACT that stated |
| CAOS inference | Ledger claims of “two hyperscaler PPAs” and unrelated capex ≤$205bn are not supported CEG gates. Per-share Calpine accretion and leverage are better tests. | CAOS INFERENCE |

**Next gate:** Q3/Q4 2026 filing: retain EPS ≥$11.50, investment-grade ratings, measurable Calpine per-share accretion, debt control, and Crane schedule. [Primary Q2 release](https://www.sec.gov/Archives/edgar/data/1868275/000186827526000097/ceg-20260806991.htm)

### Kratos Defense — KTOS

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Backlog consists of customer awards, but timing varies and government programs remain subject to funding and modification. Exact current backlog from Q2 is DATA LIMITED in the retrieved text. | DATA LIMITED |
| Nonbinding guidance | Q2 release discusses FY2026 revenue, EBITDA, cash flow and capex expectations; exact updated Q2 ranges were not reliably extracted in this bounded read. | DATA LIMITED |
| Target/aspiration | Valkyrie production, higher-margin program starts, and 2026-2027 organic growth are management expectations, not binding awards. | VERIFIED FACT that stated |
| CAOS inference | “Government-backed” does not mean guaranteed revenue. The Ledger's 85% survival and 15% backlog-growth gate are not independently derived here. | CAOS INFERENCE |

**Next gate:** KTOS Q3 2026 filing: exact revenue/EBITDA guidance, funded backlog and book-to-bill, Unmanned Systems organic growth, Valkyrie funded awards/delivery schedule, and operating cash flow. [Primary Q2 release](https://www.kratosdefense.com/newsroom/kratos-reports-second-quarter-2026-financial-results)

### Intuitive Surgical — ISRG

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | No major binding forward customer-volume commitment is disclosed. Recurring instrument revenue depends on procedures. | UNKNOWN |
| Nonbinding guidance | 2026 da Vinci procedure growth **13.5%-15.5%**, non-GAAP gross margin **68%-69%**, operating-expense growth **11%-13%**. | VERIFIED FACT |
| Target/aspiration | Broader robotic-assisted care and future AI assistance remain strategic goals, not contracted AI revenue. | VERIFIED FACT that stated |
| CAOS inference | The Ledger's >80% market-share and 95% survival assertions are not forward guidance. Procedure growth, recurring revenue, and safety are the valid gates. | CAOS INFERENCE |

**Surprise/change:** Q2 da Vinci procedures grew 15%, Ion 36%, and placements rose; guidance remains supported. **Next gate:** Q3 and Q4 2026 filings: procedure growth ≥13.5%, instruments/accessories growth no more than two points below procedures, margin ≥68%, and no material safety event. [Primary Q2 release](https://investor.intuitivesurgical.com/news-releases/news-release-details/intuitive-announces-second-quarter-earnings-6)

### Credo Technology — CRDO

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | No decision-grade long-term customer contract was disclosed in the scoped evidence; concentration terms remain limited. | DATA LIMITED |
| Nonbinding guidance | Fiscal Q2 2027 revenue **$525m-$535m**, GAAP margin **62.9%-64.9%**, non-GAAP margin **67%-69%**. | VERIFIED FACT |
| Target/aspiration | AI connectivity growth and rising content are management/industry expectations, not guaranteed revenue. | VERIFIED FACT that stated / aspiration |
| CAOS inference | The explicit quarterly guide is strong; concentration, architecture substitution, share growth, and cash conversion decide durability. | CAOS INFERENCE |

**Surprise/change:** Q1 revenue $479m was 114.7% above prior year with 64.5% GAAP margin; Q2 midpoint implies further sequential growth. **Next gate:** fiscal Q2 filing: revenue ≥$525m, margin ≥62.9%, positive operating cash flow, concentration disclosure, and diluted shares +<5% year over year. [Primary Q1 filing](https://www.sec.gov/Archives/edgar/data/1807794/000162828026060111/crdo-20260801.htm)

### Modine — MOD

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | A reported $4bn cooling agreement exists, but cancellation, pricing, concentration, and recognition terms remain incomplete. | DATA LIMITED |
| Nonbinding guidance | FY2027 sales growth **20%-35%**, adjusted EBITDA **$650m-$680m**; includes Performance Technologies despite expected Q4 2026 separation. | VERIFIED FACT |
| Target/aspiration | Management expects supply actions to relieve Data Centers bottlenecks and support long-term growth. | VERIFIED FACT that stated |
| CAOS inference | The 90% segment-growth surprise matters only if margin recovers and free cash flow turns positive. | CAOS INFERENCE |

**Surprise/change:** Data Centers sales rose 90%, but gross margin fell to 20.2% and Q1 FCF was negative. **Next gate:** next two filings: segment growth ≥25%, margin >22% each and ≥25% once, cumulative positive FCF, net debt ≤$432.9m, separation on schedule. [Primary Q1 release](https://investors.modine.com/news/news-details/2026/Modine-Reports-First-Quarter-Fiscal-2027-Results/default.aspx)

### Axon Enterprise — AXON

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Future contracted bookings **$15.1bn**, but include termination/optional clauses; 20%-25% expected to fulfill in 12 months. | VERIFIED FACT |
| Nonbinding guidance | 2026 revenue growth **32%-34%**, raised from 30%-32%; adjusted EBITDA margin about **25.5%**. | VERIFIED FACT |
| Target/aspiration | AI Era, Dedrone, international, and enterprise expansion are growth objectives, not guaranteed revenue. | VERIFIED FACT that stated |
| CAOS inference | ARR/retention are strong, but stock compensation and cash conversion must validate per-share economics. | CAOS INFERENCE |

**Surprise/change:** Q2 revenue +35%, ARR +39%, NRR 126%; raised outlook. **Next gate:** next two filings: revenue and ARR growth ≥30%, NRR ≥120%, SBC <15% of revenue, and positive trailing operating cash flow. [Primary Q2 release](https://investor.axon.com/2026-08-05-Axon-reports-Q2-2026-revenue-of-904-million%2C-up-35-year-over-year)

### Ondas — ONDS

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | IDIQ ceiling is not firm backlog; funded task-order value and customer concentration remain incomplete. | DATA LIMITED |
| Nonbinding guidance | FY2026 guidance was retained/raised in prior evidence, but current organic/acquired split remains unavailable. | DATA LIMITED |
| Target/aspiration | Defense/autonomy platform scale through acquisitions and awards is a management objective. | VERIFIED FACT that stated / aspiration |
| CAOS inference | 39% six-month share growth and $137.4m first-half burn make per-share conversion the central gate. | CAOS INFERENCE |

**Next gate:** next filing: retain/raise FY2026 guide, calculable organic growth ≥30%, sequential funded-task-order growth, half-year burn ≤$100m after integration, and quarterly share growth ≤5%. [Primary Q2 10-Q](https://www.sec.gov/Archives/edgar/data/1646188/000119312526349288/onds-20260630.htm)

### Cipher Digital — CIFR

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | AWS and Fluidstack/Google leases cover large HPC capacity; Amazon guarantee and no-convenience-termination protections apply as disclosed, subject to milestones/remedies. | VERIFIED FACT |
| Nonbinding target | Barber Lake initial delivery targeted September 2026; Black Pearl rent phases target October 2026-March 2027; Stingray rent targets April-May 2027. | VERIFIED FACT that stated |
| Target/aspiration | Management presents about $787m average contracted annual NOI; this assumes delivery and rent performance and is not current revenue. | VERIFIED FACT that stated / nonbinding model |
| CAOS inference | The immediate question is delivery and rent commencement, not pipeline size. | CAOS INFERENCE |

**Surprise/change:** Multiple leases and project financings are real, but Q2 revenue remained mining-derived. **Next gate:** September/October 2026 delivery notices and Q3 filing: Barber Lake/Black Pearl rack-ready milestones, rent commencement, costs within tenant-support caps, and initial HPC revenue. [Primary Q2 filing](https://www.sec.gov/Archives/edgar/data/1819989/000181998926000041/cifr-20260630.htm)

### Vertiv — VRT

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Agreement to acquire UIG for $1.45bn cash plus up to $1.15bn earnout, subject to approvals/closing. | VERIFIED FACT |
| Nonbinding guidance | FY2026 sales **$13.8bn-$14.2bn**, organic growth **30%-32%**, adjusted margin **23.3%-24.3%**, adjusted FCF **$2.4bn-$2.6bn**; Q3 sales $3.65bn-$3.85bn. | VERIFIED FACT |
| Target/aspiration | UIG expected to close Q4 2026 and be adjusted-EPS accretive in year one. | VERIFIED FACT that stated; nonbinding |
| CAOS inference | VRT has clearer cash conversion than MOD, but acquisition price, earnout, integration, and AI-buildout concentration must be tested. | CAOS INFERENCE |

**Surprise/change:** Q2 operating profit +44% and FCF $925m; guidance raised, then UIG announced. **Next gate:** Q3 filing: sales within $3.65bn-$3.85bn, margin 24%-25%; Q4 close of UIG with unchanged consideration and first-year accretion bridge. [Q2 source](https://investors.vertiv.com/news/news-details/2026/Vertiv-Reports-Strong-Second-Quarter-2026-with-Diluted-EPS-Growth-of-53-Adjusted-Diluted-EPS-Growth-of-60-Raises-Full-Year-2026-Guidance-Across-All-Key-Metrics/default.aspx) [UIG source](https://investors.vertiv.com/news/news-details/2026/Vertiv-Announces-Agreement-to-Acquire-UtilityInnovation-Group-to-Accelerate-Time-to-Power-for-AI-Data-Centers/default.aspx)

### Broadcom — AVGO

| Class | Forward evidence | Status |
|---|---|---|
| Binding/committed | Customer bookings/contracts are referenced by management, but customer-specific binding revenue terms are not disclosed in the release. | DATA LIMITED |
| Nonbinding guidance | Q4 FY2026 revenue about **$34.8bn** and non-GAAP operating income about **66%** of revenue. | VERIFIED FACT |
| Target/aspiration | Management's longer-range AI revenue expectations are not included as formal guidance in the results release and remain nonbinding unless supported by transcript detail. | DATA LIMITED |
| CAOS inference | Q4 revenue/margin are decision-grade; headline long-range AI targets should not be treated as contracts. | CAOS INFERENCE |

**Surprise/change:** Q3 revenue $29.6bn; AI semiconductor revenue $16.7bn, +221% year over year and +54% sequentially; FCF $13.7bn. **Next gate:** Q4 FY2026 filing: revenue near $34.8bn, non-GAAP operating income near 66%, AI revenue/customer concentration, and updated FY2027 guidance. [Primary Q3 release](https://investors.broadcom.com/news-releases/news-release-details/broadcom-inc-announces-third-quarter-fiscal-year-2026-financial)

## Guidance changes, analyst changes, and macro catalysts

- **VERIFIED FACT:** Raised or strengthened recent outlooks are visible for CEG, AXON, VRT, and the sequential guides for NVDA, CRDO, and AVGO. MOD retained its range despite margin pressure. ISRG retained explicit procedure/margin ranges.
- **VERIFIED FACT:** IREN financing evidence and WULF current HPC revenue supersede parts of the stale 2026-09-02 handoff narrative. The stale handoffs must be formally superseded by the Orchestrator, not silently ignored.
- **DATA LIMITED:** Reliable, comparable analyst-rating changes were not available from primary company/regulatory sources. One secondary report described an AVGO downgrade, but it is an `UNVERIFIED LEAD` and is not used in the verdict.
- **CAOS INFERENCE:** AI/data-center candidates share macro exposure to hyperscaler capex, component inflation, power availability, financing rates, export controls, tariffs, and construction capacity. AXON/KTOS/ONDS also face public-budget and procurement timing; ISRG faces hospital-capital, tariff, and safety/regulatory catalysts; CEG faces commodity, nuclear-regulatory, and credit catalysts.
- **DATA LIMITED:** This Forward role did not independently forecast interest rates, recession, elections, war, or policy. Those regime judgments belong to Industry Read-through; only company-disclosed sensitivities are applied here.

## Cross-audit proof priority

1. **Immediate 2026 delivery:** CIFR September/October rent milestones; WULF CB-4 H2 rent start; IREN Horizon 2 acceptance and Horizons 3-4 Q4 delivery.
2. **Next quarterly numeric guides:** NVDA, CRDO, AVGO, VRT, MSFT, CEG, AXON, MOD, ISRG.
3. **Weakest forward evidence:** TSLA commercial Cybercab/Optimus scale, ONDS organic/task-order conversion, KTOS exact Q2 guidance/backlog extraction.
4. **Ledger corrections needed downstream:** CEG gate uses unrelated capex language; WULF/IREN stale financing/revenue framing; candidate states conflict between Ledger and current handoff/run evidence. This file does not edit the Ledger.

No transaction, fill, sizing, portfolio mutation, or Master Ledger write is made.

FORWARD REVIEW = DATA LIMITED
