# RISK AND SURVIVABILITY RUN — 2026-09-11_001

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-11_001]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-11_001]]

## Portfolio concentration and cash survival

- **VERIFIED FACT:** The freshest broker screenshot shows six funded securities, account total **€9,327.53**, and cash/available-to-invest **€5,487.36**. Cash is **58.8%** of displayed NAV and equals about **18.3 months** of the stated €300 monthly contribution. This is a scale comparison, not a living-expense claim.
- **CAOS INFERENCE:** The equal cash and available figures plus the no-leverage mandate support real-unlevered-cash treatment, although direct account-settings proof is unavailable.
- **CAOS INFERENCE:** The funded sleeve is **41.2%** of NAV. A simultaneous 50% loss across that sleeve with cash unchanged would reduce NAV about **20.6%**; total loss of the sleeve would reduce NAV about **41.2%**, near the 40% target and below the 50% hard limit. These are mechanical stresses, not forecasts or trade triggers.
- **VERIFIED FACT:** Exact funded quantities remain NVDA 7.44229202, MSFT 1.96105021, GOOGL 1.85516511, TSLA 1.67642235, IREN 8.1098693, and WULF 18.91535598.
- **CAOS INFERENCE:** The funded sleeve is already concentrated in AI compute, hyperscaler capex, data-center construction, and power. CRDO adds interconnect exposure and MOD adds cooling, but both still depend on the same infrastructure buildout. AXON provides the most distinct demand lane. ONDS also adds defense/autonomy exposure, but with much weaker per-share discipline.
- **DATA LIMITED:** Exact total-NAV security weights require point-in-time EUR/USD. The Ledger's cash sections conflict, NVDA average cost changed without quantity change, and transaction history remains incomplete. No exact execution sizing is permitted from this state.

### Portfolio gates

- **Proof gate:** Before funding a candidate, reconcile Ledger cash/fills and the NVDA cost-basis anomaly; refresh regular-session broker price and EUR/USD; calculate post-entry total-NAV weight; and show combined exposure to AI infrastructure, data-center buildout, public safety/defense, and cash-burning/dilutive names. **CAOS INFERENCE.**
- **Warning gate:** Cash would fall below **50% of NAV**; any one security would exceed **15% of NAV**; or NVDA+MSFT+GOOGL+IREN+WULF plus CRDO/MOD would exceed **45% of NAV**. These are risk-review thresholds, not automatic trade rules. **CAOS INFERENCE.**
- **Break gate:** Execution remains blocked if controlling holdings/cash become unavailable, real cash cannot be separated from credit, leverage is introduced, or total-loss stress on high-risk funded names would exceed the 50% hard-loss limit. **CAOS INFERENCE.** Drawdown alone is neither a sell nor a hold reason.

## Candidate risk map — Credo Technology (CRDO)

### Applicable categories

- **Concentration / customer concentration:** Customer and product-level concentration are **DATA LIMITED**. A small number of hyperscale deployments or one architecture transition could drive a large share of growth. At portfolio level CRDO deepens AI-capex dependence.
- **Liquidity / financing / maturity:** **VERIFIED FACT:** cash and short-term investments were **$764.3m** and CRDO is profitable. Near-term external-financing and refinancing risk is low; debt maturities were not quantified in the scoped input.
- **Dilution:** Fully diluted shares are **DATA LIMITED**. Per-share risk rises if share growth exceeds earnings growth.
- **Capital intensity / execution:** Receivables, inventory, product qualification, packaging, and supply commitments can absorb cash during a fast ramp. **CAOS INFERENCE.**
- **Regulatory / geographic:** Export controls, China exposure, foundry/assembly geography, and supplier concentration are **DATA LIMITED**.
- **Factor / substitution:** Copper, pluggable optics, co-packaged optics, proprietary fabrics, and custom silicon can shift value between suppliers. **CAOS INFERENCE.** CRDO's roughly 14.7x run-rate-sales price leaves little room for a content-share loss.

### Realistic permanent-loss paths

A major customer or design is lost; interconnect architecture reduces CRDO content per rack; inventory/receivables absorb profits; export controls disrupt supply/demand; dilution outruns per-share growth; or growth remains positive but valuation compresses sharply.

### Gates

- **Proof gate:** Fiscal Q2 2027 reports revenue at or above **$525m**, GAAP gross margin at or above **62.9%**, positive operating cash flow, no major-customer loss, and fully diluted share growth below **5% year over year**. **CAOS INFERENCE.**
- **Warning gate:** Q2 revenue within the guide but below **$530m**; GAAP gross margin below **62.9%**; operating cash flow below **75% of GAAP net income**; one customer exceeds **40% of revenue** if disclosed; or diluted shares rise **5%-10%** year over year. **CAOS INFERENCE.**
- **Break gate:** Q2 revenue below **$525m** without temporary timing cause; GAAP gross margin below **60% for two consecutive quarters**; sequential revenue contraction for two quarters after customer/product loss; diluted shares rise above **10% in twelve months** without matching per-share earnings; operating cash flow materially trails GAAP profit for two quarters; or an architecture change permanently reduces CRDO content without replacement economics. **CAOS INFERENCE.**

**Risk disposition:** **CHALLENGER, NOT BUY-AUTHORIZED.** Strong liquidity and growth; customer concentration, substitution, and valuation are the permanent-loss risks.

## Candidate risk map — Modine Manufacturing (MOD)

### Applicable categories

- **Concentration / customer concentration:** Data Centers produced $348.6m of Q1 sales and grew 90%, increasing segment and AI-buildout dependence. Customer concentration and the $4bn agreement's cancellation/pricing terms are **DATA LIMITED**.
- **Liquidity / financing / maturity:** **VERIFIED FACT:** cash was **$95.3m**, debt **$528.2m**, net debt **$432.9m**, Q1 operating cash flow $41.4m, and free cash flow negative $5.0m. Expansion with negative free cash flow reduces flexibility. Maturity/covenant detail is **DATA LIMITED**.
- **Dilution:** Current equity issuance exposure is **DATA LIMITED**. Separation terms may shift liabilities and per-share economics.
- **Capital intensity / execution:** **VERIFIED FACT:** Data Centers gross margin fell from 29.8% to **20.2%** due to expansion costs, supply constraints, materials, and inefficiency. Capacity growth can destroy value if pricing and execution do not recover margin.
- **Regulatory / geographic:** Environmental rules, refrigerants, water, energy efficiency, tariffs, and global supply exposure are relevant but **DATA LIMITED**.
- **Factor / correlation:** MOD adds physical cooling rather than compute, but remains correlated with NVDA/MSFT/IREN/WULF through data-center construction and financing. Performance Technologies separation adds event risk.

### Realistic permanent-loss paths

Cooling growth stays high but margins remain near 20%; free cash flow stays negative while debt rises; the large agreement is delayed/cancelled or poorly priced; separation leaves stranded cost/debt; supply constraints prevent delivery; or data-center construction slows.

### Gates

- **Proof gate:** By the next **two quarterly reports**, Data Centers revenue growth remains at or above **25%**, segment gross margin recovers above **22% in each quarter** and reaches **25% in at least one**, company free cash flow is positive cumulatively, net debt does not exceed **$432.9m**, and the Performance Technologies transaction remains on schedule for calendar Q4 2026. **CAOS INFERENCE.**
- **Warning gate:** Data Centers growth between **25%-35%** with gross margin still **20%-22%**; a second consecutive negative-FCF quarter; net debt above **$475m**; or separation timing moves into Q1 2027. **CAOS INFERENCE.**
- **Break gate:** Data Centers growth below **25% for two quarters** before margin recovery; gross margin below **22% for two consecutive quarters** after supply constraints ease; FY2027 adjusted EBITDA guidance below **$650m** for structural reasons; negative FCF for **three consecutive quarters** while net debt rises; separation delayed beyond **Q1 2027** or leaves unexpected debt/liabilities/stranded cost; or the large cooling agreement is cancelled, materially delayed, or uneconomic. **CAOS INFERENCE.**

**Risk disposition:** **SERIOUS REVIEW retained, NOT BUY-AUTHORIZED.** The denominator and growth are attractive, but margin recovery, cash conversion, leverage, and separation proof are required.

## Candidate risk map — Axon Enterprise (AXON)

### Applicable categories

- **Concentration / customer concentration:** Public-safety procurement and long-duration government contracts create budget and customer concentration. Future contracted bookings can include termination clauses and are not guaranteed near-term revenue. **DATA LIMITED.**
- **Liquidity / financing / maturity:** **VERIFIED FACT:** cash and short-term investments were about **$673m**, senior-note principal **$1.8bn**, and net debt about **$1.1bn**. Six-month operating cash outflow was $11.4m. Refinancing detail is **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** Q2 stock compensation was about **$144m**, almost five times $29m net income; six-month stock compensation was $278.7m. Common-share economics can lag operating metrics.
- **Capital intensity / execution:** Hardware, software integration, cloud delivery, international expansion, and acquisitions must scale while converting ARR/bookings into cash. **CAOS INFERENCE.**
- **Regulatory / geographic:** Evidence rules, privacy, surveillance policy, procurement, product safety, data sovereignty, and use-of-force litigation can affect adoption. International mix and customer concentration are **DATA LIMITED**.
- **Factor / correlation:** AXON is less correlated with AI-infrastructure capex and provides the best portfolio diversification. It remains a high-duration growth security at roughly 11x annualized sales. Dedrone adds defense/autonomy and acquisition-integration risk.

### Realistic permanent-loss paths

ARR growth/retention slows; stock compensation continuously transfers value; operating cash remains negative despite adjusted earnings; bookings are cancelled or delayed; Dedrone underperforms/impairs; regulatory or reputational events slow adoption; or valuation compresses.

### Gates

- **Proof gate:** The next **two quarters** each show revenue growth at or above **30%**, ARR growth at or above **30%**, net revenue retention at or above **120%**, stock compensation below **15% of revenue**, and positive trailing-twelve-month operating cash flow. **CAOS INFERENCE.**
- **Warning gate:** Revenue or ARR growth **25%-30%**; retention **115%-120%**; stock compensation above **15% of revenue** for one quarter; net debt above **$1.3bn**; or future contracted bookings growth below **25%**. **CAOS INFERENCE.**
- **Break gate:** Revenue growth below **25% for two consecutive quarters** while valuation remains above 8x sales; retention below **115%** or ARR growth below **25% for two quarters**; stock compensation above **15% of revenue for two quarters** without faster diluted per-share cash earnings; negative trailing-twelve-month operating cash flow despite positive adjusted EBITDA; material booking cancellation/conversion weakness; or Dedrone/acquisition impairment or repeated external-financing need. **CAOS INFERENCE.**

**Risk disposition:** **CHALLENGER, NOT BUY-AUTHORIZED.** Durable recurring evidence and diversification are strong, but valuation, stock compensation, net debt, and cash conversion cap attractiveness.

## Candidate risk map — Ondas (ONDS)

`HANDOFF ACK CHECK: 20260902-DAILY-ONDS-NEW_CHALLENGER | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=HIGH-PRIORITY CHALLENGER retained with dilution and cash-conversion gates | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

### Applicable categories

- **Concentration / customer concentration:** Organic versus acquired growth, customer concentration, and funded task-order conversion are **DATA LIMITED**. IDIQ ceilings are not firm backlog.
- **Liquidity / financing / maturity:** **VERIFIED FACT:** June liquidity included about $666m cash/restricted cash and $727m short-term investments; later acquisitions used about $322.3m cash; first-half operating burn was $137.4m. Debt maturities and remaining acquisition obligations are **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** common shares rose from 380.8m to 529.8m in six months, about **39%**. Prefunded and common warrants create more potential dilution.
- **Capital intensity / execution:** Defense/autonomy requires engineering, inventory, production, integration, and customer acceptance before cash collection. Multiple acquisitions add controls, margin, and impairment risk. **CAOS INFERENCE.**
- **Regulatory / geographic:** Procurement delay/protest, appropriations, aviation approval, export controls, manufacturing geography, and contract termination rights are material but **DATA LIMITED**.
- **Factor / correlation:** ONDS diversifies from hyperscaler capex but adds financing-sensitive, high-duration small-cap exposure. Its $3.65bn denominator improves raw upside but not per-share survival.

### Realistic permanent-loss paths

Acquisition-led growth hides weak organic demand; task-order awards do not convert; burn forces another large raise; warrants/stock deals outrun value; regulation/customer acceptance delays revenue; or an acquisition creates impairment, margin collapse, or unplanned financing.

### Gates

- **Proof gate:** The next filing retains/raises FY2026 guidance, permits calculation of organic revenue growth at or above **30%**, shows sequential growth in firm funded task orders, holds trailing-half operating burn at or below **$100m** after integration, and limits quarter-over-quarter share growth to **5%**. If organic growth cannot be calculated, the gate is unmet. **CAOS INFERENCE.**
- **Warning gate:** Organic growth remains **UNKNOWN**; burn exceeds **$100m per half-year**; shares rise above **5% quarter over quarter** before positive operating cash flow; or adjusted liquidity falls below **24 months** of burn plus committed acquisition obligations. **CAOS INFERENCE.**
- **Break gate:** FY2026 guidance reduction without documented timing cause; organic growth below **30%**; firm task orders fail to grow over **two reporting cycles**; burn remains above **$100m per half-year** after integration; shares rise another **15%+** before positive operating cash flow or equivalent per-share creation; material acquisition impairment/margin collapse/unplanned financing; or adjusted liquidity below **12 months** of operating and acquisition obligations. **CAOS INFERENCE.**

**Risk disposition:** **HIGH-PRIORITY CHALLENGER, NOT BUY-AUTHORIZED.** Best raw multiple path, but worst demonstrated per-share discipline.

## Cross-candidate risk conclusion

- **Corporate survivability:** **CRDO > AXON > MOD > ONDS.** CRDO is profitable/net liquid; AXON has durable recurring economics but net debt and cash-conversion issues; MOD is profitable but has debt and negative quarterly FCF; ONDS has liquidity but burns cash and dilutes. **CAOS INFERENCE.**
- **Raw convexity:** **ONDS > MOD > CRDO > AXON.** Raw upside does not override survival. **CAOS INFERENCE.**
- **Portfolio fit:** AXON provides the strongest diversification; ONDS provides defense/autonomy exposure with the weakest per-share controls; CRDO and MOD add real bottleneck exposure but deepen the portfolio's AI/data-center cycle. **CAOS INFERENCE.**
- **Cash decision:** At **58.8% cash**, no candidate has cleared every proof gate and no deployment is required. Cash remains valid. **CAOS INFERENCE.**
- **Execution discipline:** No purchase, sale, or sizing is authorized. Any later action requires fresh regular-session price, verified FX, reconciled cash/fills/cost basis, and post-trade stress math. **VERIFIED FACT** for CAOS controls.

RISK REVIEW = COMPLETE
