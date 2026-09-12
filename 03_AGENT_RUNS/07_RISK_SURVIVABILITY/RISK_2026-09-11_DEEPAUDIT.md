# RISK AND SURVIVABILITY — FULL DEEP AUDIT — 2026-09-11

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-11_DEEPAUDIT]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-11_DEEPAUDIT]]

## Method, thresholds, and limits

- **VERIFIED FACT:** Funded broker holdings are NVDA, MSFT, GOOGL, TSLA, IREN, and WULF. Cash is €5,487.36, or 58.8% of displayed NAV.
- **CAOS INFERENCE:** Survival scores are structured estimates, not measured probabilities. They combine business durability, liquidity, leverage, financing access, dilution, concentration, and execution evidence. They do not predict price volatility.
- **VERIFIED FACT:** Deep Audit thresholds are: CORE/ATTACKER has no hard floor but must be noted below 50%; SEED **≥60%**; CHALLENGER **≥50%**; WATCH **≥40%**.
- **DATA LIMITED:** Off-hours prices, the NVDA cost-basis anomaly, conflicting Ledger cash sections, and incomplete transaction records block exact execution sizing but not survival review.
- **CAOS INFERENCE:** The funded sleeve is 41.2% of NAV. A simultaneous 50% sleeve loss with cash unchanged is about a 20.6% NAV loss; total sleeve loss is about 41.2%. Cash gives strong near-term portfolio survival, but does not repair security-level breaks.

## Survival score and threshold compliance

| Rank security | Current Deep Audit role | Survival score | Threshold | Result | Replacement implication |
|---|---|---:|---:|---|---|
| MSFT | CORE/ATTACKER | 97% | Note if <50% | PASS | Not REPLACE |
| GOOGL | CORE/ATTACKER | 97% | Note if <50% | PASS | Not REPLACE |
| ISRG | SEED candidate | 96% | 60% | PASS | Not REPLACE |
| NVDA | CORE/ATTACKER | 95% | Note if <50% | PASS | Not REPLACE |
| CEG | SEED candidate | 92% | 60% | PASS | Not REPLACE |
| CRDO | CHALLENGER | 88% | 50% | PASS | Not REPLACE |
| AXON | CHALLENGER | 88% | 50% | PASS | Not REPLACE |
| NVT | WATCH | 82% low confidence | 40% | PASS WITH MONITORING | Evidence too limited to fund |
| KTOS | WATCH | 82% low confidence | 40% | PASS WITH MONITORING | Evidence too limited to fund |
| TSLA | SEED/CATALYST | 78% | 60% | PASS WITH MONITORING | RESIZE; high replacement risk |
| MOD | GATED SEED | 76% | 60% | PASS WITH MONITORING | Margin/cash gate open |
| TEM | WATCH | 70% | 40% | PASS WITH MONITORING | Do not fund before cash proof |
| IREN | SEED | 68% | 60% | PASS WITH MONITORING | RESIZE; medium-high replacement risk |
| WULF | WATCH (Ledger) | 58% | 40% | PASS WITH MONITORING | RESIZE; high replacement risk |
| ONDS | WATCH WITH SPECIFIC TRIGGER | 55% | 40% | PASS WITH MONITORING | Do not fund; dilution gate open |

- **Breach report:** **No current security breaches its assigned threshold.** **CAOS INFERENCE.**
- **Conditional breach:** WULF at 58% would breach the Seed threshold by 2 percentage points if treated as a Seed rather than the Ledger's current WATCH. It cannot be promoted without survival improvement above 60%. **CAOS INFERENCE.**
- **Below-50 funded-holding test:** No funded holding is below 50%; therefore none is a REPLACE candidate solely because of the runbook survival test. TSLA and WULF still have high replacement risk because of weak evidence/optionality and construction/financing risk. **CAOS INFERENCE.**
- **Confidence warning:** NVT and KTOS scores are low-confidence because core financial and issuer-specific evidence is incomplete. Passing a WATCH threshold does not authorize funding.

## Funded-holding financing, dilution, and execution map

| Holding | Financing/liquidity risk | Dilution/per-share risk | Execution/concentration risk | Verdict |
|---|---|---|---|---|
| NVDA | Self-funded, strong cash generation; customer payment terms and inventory rose | Buybacks offset dilution; fully diluted trend must be monitored | Hyperscaler concentration, memory supply/cost, Rubin ramp, export controls, custom silicon | PASS |
| MSFT | Strong cash generation; exceptional capex and leases raise return burden | Low funding dilution risk; asset-life/lease accounting can obscure economics | Azure capacity utilization, AI commoditization, OpenAI/RPO concentration | PASS |
| GOOGL | Strong operating cash; $85.2bn uncommenced leases add commitments | New common/mandatory-convertible capital raises per-share burden | Search disruption, Cloud conversion, antitrust remedies, capex returns | PASS |
| TSLA | Access to capital, but >$25bn planned capex and speculative projects can consume FCF | Equity compensation/future funding can weaken per-share economics | Auto margins, Robotaxi/Cybercab/Optimus proof, regulation/safety, simultaneous ramps | PASS WITH MONITORING |
| IREN | Microsoft prepay/facility covers much project capex; retained cash after debt remains open | Project funding may still create dilution if overruns emerge | Microsoft concentration, Horizon delivery/acceptance, hardware obsolescence, power | PASS WITH MONITORING |
| WULF | High construction/tenant/leverage sensitivity; Google support helps but does not remove debt risk | Convertible/project funding can dilute or transfer value | CB-4/CB-5 timing, cost/MW, tenant and credit support, retained project cash | PASS WITH MONITORING |

## Funded-holding gates

### NVDA — survival 95%, CORE/ATTACKER
- **Proof:** Q3 revenue **$105.84bn-$110.16bn**, gross margin **73.5%-74.5%**, Rubin shipment proof, transparent China treatment, and operating cash conversion consistent with earnings.
- **Warning:** Q3 below midpoint; gross margin below **73.5%**; inventory/receivables grow faster than revenue for two quarters; hyperscaler capex guidance slows.
- **Break:** Two structural guide misses; gross margin below **68% for two quarters**; material CUDA displacement; sustained hyperscaler capex reversal; or export restrictions remove a major market without offsetting demand.

### MSFT — survival 97%, CORE/ATTACKER
- **Proof:** Q1 capex above **$50bn**, Cloud margin near **65%**, continued Azure growth, RPO conversion consistent with 30% twelve-month expectation, and positive FCF.
- **Warning:** Cloud margin below **63%**; Azure growth below **30%**; capex grows faster than cloud gross profit for two quarters; RPO conversion slows.
- **Break:** Azure growth below **20% for two quarters**; Cloud margin below **60%** without temporary cause; RPO contraction; capex materially outruns cloud gross profit for four quarters; or material AI-service commoditization.

### GOOGL — survival 97%, CORE/ATTACKER
- **Proof:** Next filing maintains Cloud growth above **30%**, Cloud backlog grows or converts without deterioration, Cloud margin remains at least **30%**, and search monetization remains positive.
- **Warning:** Cloud growth **25%-30%**; backlog decline without disclosed conversion; Cloud margin below 30%; repeated funding/lease expansion without matching cash generation.
- **Break:** Cloud growth below **25% for two quarters**; backlog decline not caused by conversion; search revenue contraction without offsetting AI economics; repeated equity funding despite strong operating cash; or material antitrust-remedy damage.

### TSLA — survival 78%, SEED/CATALYST
- **Proof:** Q3 delivery evidence plus disclosed paid Robotaxi miles/coverage, Cybercab production or deployed units, capex progress versus >$25bn, and improving automotive margin excluding credits.
- **Warning:** Vehicle volume or automotive margin falls for one quarter; no quantified paid Robotaxi scale by Q4 update; capex rises without deployment metrics.
- **Break:** Two quarters of vehicle-volume decline with falling automotive margin; no measurable paid Robotaxi scale by year-end 2026; Cybercab delay without measurable replacement plan; material safety/regulatory suspension; or persistent negative FCF tied to speculative projects.

### IREN — survival 68%, SEED
- **Proof:** Horizon 2 acceptance, Horizons 3-4 delivered in Q4, progress to 0.3GW, recognized AI revenue consistent with operating ARR, and unchanged financing/covenant capacity.
- **Warning:** Any Horizon delay; recognized revenue more than **20% below** operating ARR indication for one quarter; project-cost increase above **10%**; liquidity below 24 months of obligations.
- **Break:** Missed Q4 delivery without customer relief; Microsoft termination/material reduction; uncovered overrun; recognized revenue materially below operating ARR for two quarters; or liquidity below 12 months of obligations.

### WULF — survival 58%, WATCH
- **Proof:** CB-4 rent starts in H2 2026, cost stays within **$8m-$10m per critical IT MW**, Fluidstack/Google protections remain unchanged, CB-5 stays on track for Q1 2027, and project cash after financing is disclosed.
- **Warning:** CB-4 slips into Q1 2027; cost reaches the $10m/MW ceiling; credit support weakens; project cash retention remains undisclosed at next filing.
- **Break:** CB-4 rent delayed beyond Q1 2027 without compensation; cost above $10m/MW without tenant support; loss/weakening of credit support; material covenant stress; or project cash fails to cover debt and corporate needs.

## Candidate risk map and gates

### CRDO — survival 88%, CHALLENGER
- **Risk map:** Good liquidity/profitability; customer concentration and product mix **DATA LIMITED**; architecture substitution, export controls, inventory/receivable funding, and premium valuation drive permanent-loss risk.
- **Proof:** Q2 revenue ≥**$525m**, GAAP margin ≥**62.9%**, positive operating cash flow, diluted shares <5% YoY, and customer concentration disclosed.
- **Warning:** Revenue <$530m; margin <62.9%; OCF <75% of GAAP profit; one customer >40%; shares +5%-10% YoY.
- **Break:** Revenue <$525m without timing cause; margin <60% for two quarters; major customer loss; shares >10% YoY without per-share growth; or cash conversion trails earnings for two quarters.

### MOD — survival 76%, GATED SEED
- **Risk map:** Net debt and negative quarterly FCF reduce flexibility; Data Centers margin collapse, customer/contract concentration, capacity capex, separation liabilities, and data-center-cycle correlation are key.
- **Proof:** Data Centers growth ≥25%; margin >22% in each next two quarters and ≥25% once; cumulative positive FCF; net debt ≤**$432.9m**; clean separation on schedule.
- **Warning:** Margin 20%-22%; second negative-FCF quarter; net debt >**$475m**; separation moves to Q1 2027.
- **Break:** Growth <25% for two quarters before margin recovery; margin <22% for two quarters; EBITDA guide <$650m structurally; three negative-FCF quarters with rising debt; or harmful/delayed separation beyond Q1 2027.

### AXON — survival 88%, CHALLENGER
- **Risk map:** Durable ARR and retention; net debt, weak cash conversion, very high stock compensation, procurement/cancellation, regulation/privacy, and Dedrone integration threaten per-share value.
- **Proof:** Revenue/ARR growth ≥30% for two filings, NRR ≥120%, SBC <15% of revenue, positive trailing OCF, and organic/acquired growth separated.
- **Warning:** Growth 25%-30%; NRR 115%-120%; SBC >15% one quarter; net debt >$1.3bn; bookings growth <25%.
- **Break:** Revenue <25% for two quarters; NRR <115% or ARR growth <25%; SBC >15% for two quarters without faster per-share cash earnings; negative trailing OCF; booking cancellation or acquisition impairment.

### NVT — survival 82% low confidence, WATCH
- **Risk map:** Broad operations may support survival, but data-center mix, backlog, margin, FCF, leverage, valuation, customer concentration, and expansion funding are **DATA LIMITED**.
- **Proof:** Current filing verifies data-center mix/growth, order conversion, cooling margin, positive post-capex FCF, net leverage, diluted shares, and valuation.
- **Warning:** Capacity opens with utilization below **70%**; cooling margin below company average for one quarter; negative FCF; net leverage rises.
- **Break:** New capacity lacks contracted demand for two quarters; cooling margin below company average for two quarters; negative trailing FCF with rising net debt; material impairment; or equity funds ordinary expansion without per-share accretion.

### TEM — survival 70%, WATCH
- **Risk map:** Liquidity and growth are real; operating losses, $460m convertible, Personalis integration, reimbursement/data-rights regulation, dilution, and GAAP gains unrelated to operations threaten durability.
- **Proof:** 2026 revenue **$1.595bn-$1.605bn**, data/model growth ≥30%, positive trailing OCF, clear Personalis milestones, and fully diluted convertible treatment.
- **Warning:** Revenue at guide floor; data/model growth 20%-30%; integration raises burn; dilution >5% before positive OCF.
- **Break:** Guide below $1.595bn structurally; data/model growth <20% for two quarters; rising post-integration burn; material reimbursement/data-rights loss; impairment; or dilution without per-share gains.

### CEG — survival 92%, SEED
- **Risk map:** Investment-grade cash generation supports survival; Calpine debt/share issuance, commodity exposure, collateral/refinancing, Crane regulation, and large denominator are the main risks.
- **Proof:** EPS guide remains **$11.50-$12.50+**, investment grade retained, debt controlled, Calpine per-share accretion shown, Crane schedule intact.
- **Warning:** Guide at floor; debt >$21.6bn; cash+credit <$5bn; Crane cost/schedule worsens.
- **Break:** Structural guide <$11.50; rating loss; collateral needs exceed liquidity; acquisition dilution without accretion for two cycles; or material Crane delay.

### ISRG — survival 96%, SEED
- **Risk map:** Strong liquidity/recurring instruments reduce financing risk; valuation, procedure growth, safety/recall/liability, competitive systems, reimbursement, and utilization dominate.
- **Proof:** Procedure growth ≥13.5%, recurring growth within two points, non-GAAP margin ≥68%, and no material safety event for two quarters.
- **Warning:** Procedure growth <13.5%; margin <68%; recurring growth lags >2 points; installed-base growth <10%.
- **Break:** Procedure growth <10% for two quarters; margin <65%; recurring decoupling; or material safety/regulatory restriction.

### KTOS — survival 82% low confidence, WATCH
- **Risk map:** Defense lane supports demand, but current guidance, funded backlog, book-to-bill, FCF, customer/program concentration, and Valkyrie awards are **DATA LIMITED**. Procurement and production are key execution risks.
- **Proof:** Q3 filing verifies guidance, funded backlog/book-to-bill ≥**1.0**, Unmanned Systems organic growth, funded Valkyrie schedule, and positive OCF.
- **Warning:** Book-to-bill 1.0-1.1 with negative OCF; funded delivery slips; backlog growth <10%.
- **Break:** Funded backlog falls; book-to-bill <1 for two quarters; repeated unfunded-program claims; or persistent negative OCF.

### ONDS — survival 55%, WATCH
- **Risk map:** Substantial liquidity but high burn; 39% six-month share growth, acquisitions, task-order conversion, customer/procurement concentration, export/aviation rules, and integration risk weaken per-share survival.
- **Proof:** Guidance retained, organic growth ≥30%, funded task orders grow, half-year burn ≤$100m after integration, and quarterly shares grow ≤5%.
- **Warning:** Organic growth UNKNOWN; burn >$100m/half; shares >5% QoQ; liquidity <24 months of obligations.
- **Break:** Guide cut; organic growth <30%; task orders fail to grow for two cycles; another ≥15% share increase before cash proof; impairment; or liquidity <12 months of obligations.

## Portfolio concentration and permanent-loss map

- **AI infrastructure cluster:** NVDA, MSFT, GOOGL, IREN, WULF, CRDO, MOD, and NVT are not independent bets. A hyperscaler-capex reversal, memory/power constraint, financing shock, or overbuild could affect several. **CAOS INFERENCE.**
- **Highest funded permanent-loss routes:** WULF construction/financing/tenant economics; IREN delivery/customer concentration; TSLA paying for autonomy/robotics before commercial proof. **CAOS INFERENCE.**
- **Best diversifiers:** ISRG and AXON have the most distinct demand mechanics; CEG changes revenue mechanics but retains power-demand exposure. **CAOS INFERENCE.**
- **Cash survival:** 58.8% cash means no weak candidate must be funded. Cash ranks ahead of KTOS/NVT/TEM/ONDS until proof gates close. **CAOS INFERENCE.**

## Handoff acknowledgements

`HANDOFF ACK CHECK: 20260902-DAILY-ONDS-NEW_CHALLENGER | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=WATCH WITH SPECIFIC TRIGGER at 55% survival; passes WATCH threshold but not funded | STILL_ACTIVE=YES pending Orchestrator reconciliation | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=Six funded securities verified; old eight-name condition absent | STILL_ACTIVE=YES pending Orchestrator resolution | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260902-DAILY-WULF_IREN-EVIDENCE_GATE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=IREN 68% Seed PASS WITH MONITORING; WULF 58% WATCH PASS WITH MONITORING and would breach Seed threshold | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

## Final Deep Audit risk verdict

- No assigned-role threshold breach exists today.
- No funded holding is below 50%, so survival scoring alone does not force a REPLACE verdict.
- TSLA and WULF remain highest funded replacement-risk names; IREN is medium-high. Their defined break gates—not price drawdown—control any sell recommendation.
- NVT and KTOS scores are provisional and low confidence. Missing evidence prevents funding despite threshold PASS.
- No trade, sizing, or Ledger mutation is authorized by this report.

RISK REVIEW = COMPLETE
