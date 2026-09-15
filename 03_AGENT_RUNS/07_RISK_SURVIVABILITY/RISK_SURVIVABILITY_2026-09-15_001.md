# RISK AND SURVIVABILITY RUN — 2026-09-15_001

## Inputs Consulted

- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-15_001]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-15_001]]

## Portfolio Risk Map and Cash Survival

- **VERIFIED FACT:** Broker display supplied at 10:27 EEST shows €9,379.60 NAV, €5,519.84 cash and available-to-invest, and six unchanged positions: NVDA, MSFT, GOOGL, TSLA, IREN, and WULF.
- **CAOS INFERENCE:** Cash is 58.8% of displayed NAV; funded sleeve is 41.2%. Equal cash and available-to-invest support, but do not prove, unlevered cash.
- **DATA LIMITED:** Screenshot was before US regular trading. No executable bid/ask, authenticated EUR/USD, EUR holding values, transaction history, account-settings proof, or NVDA cost-basis explanation exists. Exact security weights and order sizing are unavailable.
- **CAOS INFERENCE:** NVDA, MSFT, GOOGL, IREN, WULF, and TSSI/AAOI/VICR/BELFB candidates share varying exposure to AI-data-center capex, power, networking, or supplier demand. New positions in those lanes would increase correlated-thesis risk. PLPC has grid/communications overlap. AMBA is less directly correlated but remains semiconductor-cycle exposed.
- **CAOS INFERENCE:** With the displayed funded sleeve, a 50% loss across funded assets with cash unchanged would reduce displayed NAV by about 20.6%; a total loss of funded assets would reduce it by about 41.2%. These are stress illustrations, not forecasts or trade triggers.

### Portfolio gates

- **Proof gate:** Before funding any candidate, obtain a regular-session broker refresh, same-time EUR/USD, exact EUR values and weights, transaction reconciliation, and candidate valuation, diluted-share, debt, cash, free-cash-flow, and concentration data. **CAOS INFERENCE.**
- **Warning gate:** Proposed action would reduce cash below 50% of current NAV, put one security above 15% of NAV, or move combined AI-data-center/power/networking exposure above 45% of NAV. These are draft review thresholds, not automatic trades. **CAOS INFERENCE.**
- **Break gate:** No portfolio execution while `EXECUTION BLOCKED — RESEARCH STATE REFRESHED` applies; while real cash cannot be separated from credit; or while a proposed high-risk position lacks an issuer-specific break gate. **CAOS INFERENCE.**

## Candidate Risk Map — Preformed Line Products (PLPC)

### Risk categories and permanent-loss paths

- **Concentration/customer:** Backlog, customer, geographic, end-market, and cancellation concentration are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** Net debt, covenants, maturities, working-capital normalization, and cash conversion are **DATA LIMITED**.
- **Dilution:** Diluted-share count and acquisition funding are **DATA LIMITED**.
- **Capital intensity/execution:** Capacity investment, fixed-price project risk, skilled-labor availability, materials, and acquisition integration can weaken cash conversion. **CAOS INFERENCE.**
- **Regulatory/geographic:** Utility permitting, safety, tariffs, labor rules, and regional construction exposure are **DATA LIMITED**.
- **Factor/correlation:** Grid hardening and communications demand offer some diversification from direct GPU ownership, but data-center buildout can still drive demand. **CAOS INFERENCE.**
- **Permanent-loss paths:** Backlog cancellations, weak organic demand masked by acquisitions, margin loss from labor/material costs, receivable stress, or debt/dilution without per-share cash growth. **CAOS INFERENCE.**

- **Proof gate:** Next two quarterly filings show gross margin **≥30%** in each; disclose backlog, conversion period, cancellation terms, top customers and geographies; show positive trailing free cash flow after working-capital and capacity spending; and disclose net debt, diluted shares, and valuation. **CAOS INFERENCE.**
- **Warning gate:** Organic growth is **0%-10%** for one quarter; gross margin is **28%-30%**; backlog falls once; trailing free cash flow is below **75% of net income**; or net leverage exceeds **2x EBITDA**. **CAOS INFERENCE.**
- **Break gate:** Organic revenue declines for two quarters while capacity spending rises; gross margin is below **28% for two quarters** without disclosed temporary cause; cancellations or receivable impairment show weak demand; trailing free cash flow structurally trails earnings; or debt/dilution rises without per-share cash-flow growth. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`; no funding.

## Candidate Risk Map — TSS (TSSI)

### Risk categories and permanent-loss paths

- **Concentration/customer:** Largest customer, contract length, pricing power, cancellation rights, receivables, and backlog are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** Cash generation, liquidity, debt, maturities, share count, and funding source for planned investment are **DATA LIMITED**.
- **Dilution:** Issued shares and future equity need are **DATA LIMITED**.
- **Capital intensity/execution:** Management expects about **$17m** investment for next-generation AI-data-center integration. Returns may fail if procurement-heavy revenue has low margins or conversion is delayed. **VERIFIED FACT** for planned investment; **CAOS INFERENCE** for risk.
- **Regulatory/geographic:** Export controls, supplier access, data-center permitting, and manufacturing location are **DATA LIMITED**.
- **Factor/correlation:** This is direct AI-rack integration exposure and would deepen existing AI-capex correlation. **CAOS INFERENCE.**
- **Permanent-loss paths:** One customer controls volume and working capital; high reported growth is low-margin procurement; planned investment does not earn returns; dilution/debt finances routine losses; or AI deployment slows. **CAOS INFERENCE.**

- **Proof gate:** Next two quarterly filings disclose largest-customer share, contract protections, systems-integration gross margin, operating cash flow, free cash flow, liquidity, debt, diluted shares, and valuation; systems-integration growth stays **≥15% YoY**; and $17m investment shows profitable volume conversion within two reporting cycles. **CAOS INFERENCE.**
- **Warning gate:** One customer exceeds **25%** of revenue; systems-integration growth is **15%-25%** with declining margin; one quarter has negative operating cash flow; or planned investment rises above $17m without disclosed return milestones. **CAOS INFERENCE.**
- **Break gate:** A dominant customer lacks firm contractual protection; operating cash flow remains negative after planned investment; gross margin compresses for two quarters from mix or price pressure; debt/dilution funds routine losses or working capital; or revenue growth is below **15% for two quarters** while capex rises. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`, concentration-gated; no funding.

## Candidate Risk Map — Bel Fuse (BELFB)

### Risk categories and permanent-loss paths

- **Dilution:** **VERIFIED FACT:** Company raised **$441.6m** net equity proceeds and repaid **$197.5m** debt. Offering price, shares issued, pro-forma diluted count, fees, and remaining-proceeds use are **DATA LIMITED**.
- **Concentration/customer:** Customer, distributor, end-market, inventory, and acquisition concentration are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** Debt reduction is verified, but remaining cash, debt maturity profile, free cash flow, and returns on new equity are **DATA LIMITED**.
- **Capital intensity/execution:** Power/protection/connectivity demand can be cyclical. Remaining equity proceeds can destroy value through low-return capacity or acquisitions. **CAOS INFERENCE.**
- **Regulatory/geographic:** Defense/export controls, tariffs, global sourcing, and end-market exposure are **DATA LIMITED**.
- **Factor/correlation:** Power and connectivity exposure overlaps with AI-data-center investment; defense exposure may diversify it. **CAOS INFERENCE.**
- **Permanent-loss paths:** Equity dilution exceeds operating gain; reported growth is acquired or channel-driven; inventory write-downs or pricing reduce margins; remaining proceeds earn poor returns; or concentration breaks demand. **CAOS INFERENCE.**

- **Proof gate:** Next quarterly filing closes offering price, issued shares, fees, use of proceeds, and pro-forma diluted shares; then shows organic growth and gross-profit growth by end market, positive trailing free cash flow, debt reduction, and return milestones for remaining equity. **CAOS INFERENCE.**
- **Warning gate:** Fully diluted shares rise **5%-10%** without per-share cash-flow growth; gross margin is **32%-35%**; free cash flow is negative for one quarter; or remaining proceeds lack return milestones. **CAOS INFERENCE.**
- **Break gate:** Fully diluted shares rise materially without matching per-share cash-flow growth within four quarters; gross margin is below **32% for two quarters**; equity proceeds fund losses, low-return acquisitions, or routine working capital; organic demand weakens while reported growth depends on acquisitions/inventory; or new debt/dilution returns before capital returns are demonstrated. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`, dilution-gated; no funding.

## Candidate Risk Map — Vicor (VICR)

### Risk categories and permanent-loss paths

- **Concentration/customer:** Customer concentration, design-win conversion, product/royalty mix, and end-market exposure are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** Cash flow, balance sheet, debt, maturities, dilution, and valuation are **DATA LIMITED**.
- **Capital intensity/execution:** Power-conversion capacity, yields, product qualification, and price competition can prevent a profitable sequential step-up from becoming durable. **CAOS INFERENCE.**
- **Regulatory/geographic:** Semiconductor supply-chain, tariffs, export controls, and manufacturing concentration are **DATA LIMITED**.
- **Factor/correlation:** AI/high-density-compute power exposure increases portfolio hardware/capex correlation. **CAOS INFERENCE.**
- **Permanent-loss paths:** One customer drives temporary demand; royalties or product mix reverse; pricing reduces margin; cash flow diverges from earnings; or capacity is added into a downcycle. **CAOS INFERENCE.**

- **Proof gate:** Next two quarterly filings show profitable revenue growth, no material pricing deterioration, disclosed top-customer share and royalty/product mix, positive operating and free cash flow, net cash/debt, diluted shares, valuation, and stable gross margin. **CAOS INFERENCE.**
- **Warning gate:** Revenue growth drops below **10%** for one quarter; a top customer exceeds **35%** of revenue; gross margin falls more than **300 bps** year over year; or operating cash flow trails net income for one quarter. **CAOS INFERENCE.**
- **Break gate:** Revenue contracts for two quarters after the Q2 step-up; a top-customer reduction causes sustained operating-profit decline; cash flow materially diverges from net income without disclosed temporary cause; or pricing/mix causes two-quarter gross-margin deterioration. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; no funding.

## Candidate Risk Map — Applied Optoelectronics (AAOI)

### Risk categories and permanent-loss paths

- **Liquidity, financing, and maturity:** **VERIFIED FACT:** Q2 revenue was $191.9m, GAAP net loss was $22.8m, and Q3 revenue guidance is $255m-$290m. Cash burn, liquidity, debt service, maturities, and funded runway are **DATA LIMITED**.
- **Dilution:** Share count, capital needs, and financing terms are **DATA LIMITED**.
- **Concentration/customer:** Top customers, contract protections, optical mix, and inventory risk are **DATA LIMITED**.
- **Capital intensity/execution:** Optical capacity, yields, component supply, and customer qualification can consume cash before margins improve. **CAOS INFERENCE.**
- **Regulatory/geographic:** Export controls, Asian supply chains, tariffs, and logistics are **DATA LIMITED**.
- **Factor/correlation:** Optical AI-networking demand is strongly correlated with current AI compute/data-center exposure. **CAOS INFERENCE.**
- **Permanent-loss paths:** Q3 guide misses; loss widens despite revenue growth; inventory is written down; a large customer changes architecture; or expensive financing/dilution sustains operations. **CAOS INFERENCE.**

- **Proof gate:** Next Q3 earnings release reports revenue within **$255m-$290m**, positive GAAP earnings or a materially narrowing loss, disclosed gross-margin trend, positive or improving operating cash flow, funded runway, top-customer share, inventory exposure, debt, diluted shares, and valuation. **CAOS INFERENCE.**
- **Warning gate:** Q3 revenue is at/below **$255m**; GAAP loss does not narrow; operating cash flow is negative for one quarter; top customer exceeds **35%**; or share count rises **5%-10% YoY**. **CAOS INFERENCE.**
- **Break gate:** Q3 misses the stated range for structural demand or execution reasons; GAAP loss widens despite revenue growth for two quarters; gross margin deteriorates or operating cash flow stays negative without funded runway; customer loss/inventory write-down breaks growth quality; or material dilution/high-cost financing is needed to sustain operations. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; no funding.

## Candidate Risk Map — Ambarella (AMBA)

### Risk categories and permanent-loss paths

- **Concentration/customer:** Automotive/edge-AI revenue mix, design-win pipeline, production conversion, customer concentration, and product-cycle length are **DATA LIMITED**.
- **Liquidity, financing, and maturity:** Cash burn, net cash/debt, maturities, and profitability runway are **DATA LIMITED**.
- **Dilution:** Diluted shares and stock-based compensation are **DATA LIMITED**.
- **Capital intensity/execution:** Automotive qualification cycles, software investment, and design-win timing can delay operating leverage. **CAOS INFERENCE.**
- **Regulatory/geographic:** Automotive safety, export controls, semiconductor supply chain, and geographic demand are **DATA LIMITED**.
- **Factor/correlation:** Edge AI is less direct than data-center hardware but still linked to semiconductor-cycle risk. **CAOS INFERENCE.**
- **Permanent-loss paths:** Design wins do not convert to production; customer loss or price pressure reduces margin; cash runway weakens; stock compensation/dilution offsets growth; or GAAP loss persists through weak growth. **CAOS INFERENCE.**

- **Proof gate:** Next two quarterly filings show revenue growth above **13.2% YoY**, GAAP gross margin near **57.7%**, narrowing GAAP loss in both quarters, verified cash runway, disclosed automotive/edge-AI design wins and production conversion, customer concentration, net cash/debt, diluted shares, stock compensation, and valuation. **CAOS INFERENCE.**
- **Warning gate:** Revenue growth is **10%-13.2%**; GAAP gross margin is **50%-57.7%**; GAAP loss stops narrowing; or diluted shares rise **5%-10% YoY**. **CAOS INFERENCE.**
- **Break gate:** Revenue growth is below **10% for two quarters** while GAAP loss persists; GAAP gross margin is below **50% for two quarters**; disclosed design wins miss stated production timelines; material customer loss or pricing pressure weakens per-share economics; or equity financing is required before a credible profitability path is shown. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; no funding.

## Active Handoff Acknowledgements

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-PORTFOLIO-REBALANCE-REVIEW | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=fresh broker state improves cash reference only; exact allocation and execution remain blocked | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-IREN_WULF-UPDATED_GATE | RECEIVED=YES | APPLIED=NO | RESULTING_STATE=no delivery, rent, financing, or retained-economics evidence in this risk review | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-ONDS-STATE | RECEIVED=YES | APPLIED=NO | RESULTING_STATE=ONDS is outside this Underwriter referral set | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

## Risk Verdict

- **CAOS INFERENCE:** PLPC has lowest closed operating-risk profile of this six-name set, but its balance sheet, cash conversion, concentration, and valuation remain open.
- **CAOS INFERENCE:** BELFB needs dilution reconciliation. TSSI has highest direct customer/conversion risk. VICR, AAOI, and AMBA remain Watch because issuer survival, per-share, and valuation evidence is incomplete.
- **VERIFIED FACT:** No referred candidate is buy-authorized by Underwriter. No sell, purchase, sizing, or Ledger/Snapshot change follows from this review.
- **DATA LIMITED:** Candidate liquidity, financing, maturity, concentration, valuation, and correlation numbers cannot be calculated from current evidence.

RISK REVIEW = DATA LIMITED
