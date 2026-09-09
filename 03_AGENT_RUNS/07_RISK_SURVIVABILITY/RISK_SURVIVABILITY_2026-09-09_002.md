# RISK AND SURVIVABILITY RUN — 2026-09-09_002

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-09_002]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-09_001]]

## Portfolio state and survival

- **VERIFIED FACT:** The fresh broker screenshot shows six funded securities, total account value **€9,405.50**, and **€5,465.84** available cash. Cash is **58.1%** of displayed account value and equals about **18.2 months** of the stated €300 monthly contribution. This is a scale comparison, not a claim about living expenses.
- **CAOS INFERENCE:** Equal cash and available-to-invest figures plus the no-leverage mandate support treating this as real unlevered cash. Direct account-settings proof remains unavailable.
- **VERIFIED FACT:** Screenshot quantities and prices imply about **$4,594.67** invested before FX: NVDA $1,671.32, MSFT $965.37, TSLA $627.38, GOOGL $610.07, IREN $381.00, and WULF $339.53.
- **CAOS INFERENCE:** NVDA is **36.4%** of invested value; NVDA plus MSFT are **57.4%**; IREN plus WULF are **15.7%**. Exact total-NAV security weights are **DATA LIMITED** because the broker reports cash/total in EUR and securities in USD without verified spot FX.
- **CAOS INFERENCE:** A 50% funded-sleeve loss with cash unchanged would reduce account value about **20.9%**. Total loss of the funded sleeve would reduce it about **41.9%**, near the 40% target but below the 50% hard limit. These are mechanical stresses, not forecasts or sell rules.
- **CAOS INFERENCE:** Cash is the portfolio's strongest survival asset, so there is no need to force a purchase. CIFR would deepen the funded IREN/WULF risk lane; CEG partly shares the power-demand theme; ISRG gives the clearest business-driver diversification; ONDS adds defense/autonomy but also acquisition and dilution risk.
- **DATA LIMITED:** The Ledger event says rebalance fills were confirmed, but its confirmed-transactions section is empty and the Verifier says transaction history was unavailable. Fill prices, fees, dates, and realized results remain unreconciled; current displayed holdings do not.

### Portfolio proof, warning, and break gates

- **Proof gate:** Before funding any candidate, reconcile the Ledger snapshot/fills to the 2026-09-09 broker state, refresh live broker price and EUR/USD, calculate post-entry total-NAV weight, and show combined exposure to its main risk lane. **CAOS INFERENCE.**
- **Warning gate:** Cash would fall below **40% of NAV**, one security would exceed **20% of NAV**, or IREN plus WULF plus a new data-center/power-infrastructure name would exceed **20% of NAV**. These are risk-review thresholds, not constitutional limits. **CAOS INFERENCE.**
- **Break gate:** No execution if real cash cannot be distinguished from credit, controlling portfolio state is stale/unavailable, leverage is introduced, or high-risk positions could breach the 50% hard-loss limit under a total-loss stress. **CAOS INFERENCE.** Drawdown alone is neither a sell nor hold reason.

## Candidate risk map — Constellation Energy (CEG)

### Applicable risk categories

- **Concentration:** Direct AI revenue and customer concentration are **DATA LIMITED**. Calpine creates integration concentration, while the thesis partly depends on scarce-power demand.
- **Liquidity, financing, and maturity:** **VERIFIED FACT:** CEG had $0.7bn cash, $7.0bn available credit, $19.6bn long-term debt, investment-grade ratings, and $1.55bn first-half operating cash flow. **CAOS INFERENCE:** survival is good, but refinancing and collateral stress matter because cash is small relative to debt. The full maturity ladder is **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** Calpine consideration included about 50m new shares and average diluted shares rose to 360m from 314m. Repurchases partly offset, but do not erase, acquisition dilution.
- **Capital intensity and execution:** **CAOS INFERENCE:** Calpine integration and Crane restart require long-cycle operational and capital execution. Cost, outage, or schedule failure can permanently impair value.
- **Regulatory and geographic:** Crane licensing and nuclear oversight are material. Geographic earnings exposure is **DATA LIMITED**.
- **Factor and correlated thesis:** **CAOS INFERENCE:** CEG reduces technology risk but overlaps IREN/WULF through power-demand economics. Commodity, weather, outage, and rate sensitivity add distinct risks.

### Realistic permanent-loss paths

Calpine fails to lift per-share earnings while debt stays high; credit downgrade/refinancing or collateral calls consume liquidity; Crane suffers material regulatory/cost/schedule failure; commodity weakness reduces earnings; or new issuance outruns per-share growth.

### Gates

- **Proof gate:** The next report retains adjusted EPS guidance of **$11.50-$12.50 or higher**, keeps investment-grade ratings, holds long-term debt at or below **$19.6bn** unless matched by cash-generating assets, and provides a measurable Calpine per-share accretion or integration milestone. **CAOS INFERENCE.**
- **Warning gate:** Guidance moves to the $11.50 floor; debt rises above **$21.6bn**; cash plus available credit falls below **$5bn**; Crane cost/schedule guidance worsens; or no new clean-power contract is added over **two evidence cycles**. **CAOS INFERENCE.**
- **Break gate:** Structural adjusted EPS guidance below **$11.50**; loss of investment-grade rating; collateral needs exceed cash plus credit; material Crane failure; no Calpine per-share accretion over **two decisive reporting cycles** while debt stays near current levels; or issuance grows faster than per-share earnings over two cycles. **CAOS INFERENCE.**

**Risk disposition:** **WATCH WITH SPECIFIC TRIGGER.** Corporate survival is good; acquisition leverage, dilution, commodity exposure, and the large denominator cap attractiveness.

## Candidate risk map — Intuitive Surgical (ISRG)

### Applicable risk categories

- **Concentration:** **VERIFIED FACT:** $1.735bn of Q2 revenue was recurring instruments/accessories revenue. Customer concentration is **DATA LIMITED**; the model is economically concentrated on installed-base utilization.
- **Liquidity, financing, and maturity:** **VERIFIED FACT:** cash, equivalents, and investments were $8.63bn and increased mainly through operations. Financing risk is low; debt-maturity detail is **DATA LIMITED**.
- **Dilution:** Fully diluted exposure is **DATA LIMITED**; no material financing need appears in reviewed inputs.
- **Capital intensity and execution:** **CAOS INFERENCE:** placements, training, manufacturing quality, service, and procedure utilization must scale together. Weak utilization can make installed-base growth lower quality.
- **Regulatory and geographic:** Safety, recall, liability, cybersecurity, and regulatory events can damage trust and use. Geographic/tariff exposure is **DATA LIMITED**.
- **Factor and correlated thesis:** ISRG offers the strongest diversification from AI infrastructure but remains a high-duration growth equity. Autonomous-surgery or material AI revenue is an **UNVERIFIED LEAD** and receives no risk offset.

### Realistic permanent-loss paths

Procedure growth falls below double digits while valuation remains high; recurring revenue lags procedures; a safety/recall/liability event harms trust; competition causes durable share loss or pricing pressure; or placements grow with weak utilization.

### Gates

- **Proof gate:** The next **two quarters** each show da Vinci procedure growth at or above **13.5%**, instruments/accessories growth no more than **2 percentage points below** procedure growth, non-GAAP gross margin at or above **68%** excluding separately quantified temporary tariffs, and no material safety/recall event. **CAOS INFERENCE.**
- **Warning gate:** Procedure growth below **13.5%**; gross margin below **68%**; recurring growth more than two points below procedures; installed-base growth below **10%**; or disclosed competitive pricing pressure. **CAOS INFERENCE.**
- **Break gate:** Procedure growth below **10% for two consecutive quarters** absent a short-lived disruption; 2026 procedure growth below **13.5%** or gross margin below **68%** without temporary tariff cause; recurring revenue materially lags procedures for two quarters; installed-base growth stalls with weak utilization; or a major safety, recall, liability, regulatory, or sustained share-loss event occurs. **CAOS INFERENCE.**

**Risk disposition:** **CHALLENGER, NOT BUY-AUTHORIZED.** Strongest business survival and portfolio diversification, but valuation demands sustained execution.

## Candidate risk map — Cipher Digital (CIFR)

### Applicable risk categories

- **Concentration:** **VERIFIED FACT:** Q2 revenue was $24.8m, entirely Bitcoin Mining. AWS/Fluidstack contracts create tenant and project concentration; detailed protections are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** **VERIFIED FACT:** $831.8m cash, $3.73bn restricted cash, $6.02bn future principal payments, $152m first-half operating burn, and $2.84bn financing inflow. **CAOS INFERENCE:** restricted cash is not free liquidity; delivery and refinancing are central survival risks. Covenant and maturity detail is **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** shares rose to 414.3m from 405.0m; ATM and employee awards issued shares; a $172.5m convertible can settle in shares.
- **Capital intensity and execution:** **VERIFIED FACT:** the 15-year AWS lease covers about 300 MW and $5.5bn contracted revenue, but rent is not current revenue. Construction, interconnection, equipment, cost, and rent-start delays can create a funding gap. **CAOS INFERENCE.**
- **Regulatory and geographic:** Permitting, grid, curtailment, tax, weather, and contract-remedy detail are **DATA LIMITED**.
- **Factor and correlated thesis:** **CAOS INFERENCE:** CIFR strongly overlaps IREN/WULF. Funding it now creates three-name exposure to construction, power, tenant, financing, and HPC delivery risk.

### Realistic permanent-loss paths

Sites deliver late or over budget; restricted funds cannot cover overruns; tenant, guarantor, or lender terms weaken; mining declines before HPC rent covers burn; dilution outruns per-share contract value; or delivered projects retain weak cash after debt service.

### Gates

- **Proof gate:** By the **Q4 2026 filed report**, positive non-mining HPC revenue exceeds **10% of total revenue**, disclosed rent commencement is on time, project costs have not risen materially, and disclosed economics show cash available after debt service. **CAOS INFERENCE.**
- **Warning gate:** No HPC revenue by the Q3 2026 filing; disclosed delivery slippage; project cost estimate rises more than **10%**; unrestricted cash falls below **$600m** before rent; or shares rise more than **5%** from 414.3m before recurring HPC revenue. **CAOS INFERENCE.**
- **Break gate:** No reported HPC revenue by **Q4 2026**; material rent delay; overruns require major common issuance or expensive parent debt; material tenant/guarantor/lender weakening; mining cannot cover corporate burn before rent; or shares rise more than **15%** above 414.3m before positive recurring HPC revenue. **CAOS INFERENCE.**

**Risk disposition:** **WATCH WITH SPECIFIC TRIGGER.** Contracts are real, but pre-revenue HPC status, restricted funding, debt, dilution, and incumbent overlap prevent promotion.

## Candidate risk map — Ondas (ONDS)

`HANDOFF ACK CHECK: 20260902-DAILY-ONDS-NEW_CHALLENGER | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=HIGH-PRIORITY CHALLENGER retained with verified dilution and exact survival gates | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

### Applicable risk categories

- **Concentration:** Organic versus acquired growth and customer concentration are **DATA LIMITED**. IDIQ ceilings are not firm backlog.
- **Liquidity, financing, and maturity:** **VERIFIED FACT:** about $666m cash/restricted cash plus $727m short-term investments; later acquisitions used $322.3m cash; first-half operating burn was $137.4m. Debt maturities and remaining obligations are **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** shares rose from 380.8m to 529.8m in six months, about 39%; 121.6m warrants at $28 add potential dilution.
- **Capital intensity and execution:** **CAOS INFERENCE:** defense/autonomy requires inventory, engineering, production, integration, and collection before cash generation. Multiple acquisitions add control and impairment risk.
- **Regulatory and geographic:** Procurement delay/protest, aviation approval, export controls, manufacturing geography, and termination rights are material but incompletely quantified. **DATA LIMITED.**
- **Factor and correlated thesis:** **CAOS INFERENCE:** ONDS diversifies away from hyperscaler capex more than CIFR or CEG, but remains exposed to financing conditions and high-duration growth valuations.

### Realistic permanent-loss paths

Acquired growth hides weak organic demand; task orders fail to convert from ceilings; burn forces another raise; warrants/stock deals outrun per-share growth; regulatory acceptance delays revenue; or acquisitions cause impairment or margin collapse.

### Gates

- **Proof gate:** The next filing retains or raises FY2026 guidance, shows calculable organic growth of at least **30%**, reports growth in firm funded task orders, holds trailing-half operating burn at or below **$100m** after integration, and limits quarter-over-quarter share growth to **5%**. If organic growth cannot be calculated, the gate remains unmet. **CAOS INFERENCE.**
- **Warning gate:** Organic growth is **UNKNOWN**; burn exceeds **$100m per half-year**; shares rise more than **5%** quarter over quarter before positive operating cash flow; or adjusted liquidity falls below **24 months** of burn plus acquisition obligations. **CAOS INFERENCE.**
- **Break gate:** Guidance is reduced without documented timing cause; organic growth falls below **30%**; firm task orders fail to grow over **two cycles**; burn remains above **$100m per half-year** after integration; shares rise another **15% or more** before positive operating cash flow or equivalent per-share value creation; material acquisition impairment/margin collapse/unplanned financing occurs; or adjusted liquidity falls below **12 months** of burn plus committed obligations. **CAOS INFERENCE.**

**Risk disposition:** **HIGH-PRIORITY CHALLENGER, NOT BUY-AUTHORIZED.** Highest raw convexity, but per-share survival requires proof of organic growth, funded awards, cash conversion, and dilution control.

## Cross-candidate conclusion

- **Corporate survivability:** **ISRG > CEG > ONDS > CIFR.** **CAOS INFERENCE.**
- **Raw convexity:** **ONDS > CIFR > CEG > ISRG**, but upside does not override leverage, dilution, or delivery risk. **CAOS INFERENCE.**
- **Portfolio fit:** ISRG diversifies risk drivers best; CEG adds established power earnings with some theme overlap; ONDS adds defense/autonomy with financing risk; CIFR fits worst because IREN/WULF already fund its risk lane. **CAOS INFERENCE.**
- **Cash decision:** At **58.1% cash**, with no candidate through all proof gates, survival does not require deployment. Cash remains valid. **CAOS INFERENCE.**
- **Execution discipline:** No trade or sizing is authorized. Later action requires fresh broker price, verified FX, reconciled state, and post-trade concentration stress. **VERIFIED FACT** for CAOS controls.

RISK REVIEW = COMPLETE
