# RISK AND SURVIVABILITY RUN — 2026-09-12_001

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-12_001]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-12_001]]

## Portfolio state, concentration, and cash survival

- **VERIFIED FACT:** The controlling six-holding state remains NVDA 7.44229202, MSFT 1.96105021, GOOGL 1.85516511, TSLA 1.67642235, IREN 8.1098693, and WULF 18.91535598.
- **VERIFIED FACT:** Last broker-displayed cash was €5,487.36 and last NAV was €9,327.53. Cash was 58.8% of that stale reference NAV and equal to about 18.3 months of the stated €300 contribution.
- **DATA LIMITED:** Today is Saturday, no fresh usable quotes were obtained, and the direct broker evidence is more than 24 hours old. Current weights, EUR/USD, spreads, and candidate valuation denominators are unavailable. `HOLDINGS STALE / EXECUTION BLOCKED` applies.
- **CAOS INFERENCE:** At the last reference NAV, the funded sleeve was 41.2%. A mechanical 50% sleeve loss with cash unchanged would reduce NAV about 20.6%; total sleeve loss would reduce NAV about 41.2%. These are stale-state stresses, not forecasts or sell triggers.
- **CAOS INFERENCE:** FIX and POWL add electrical/mechanical infrastructure exposure correlated with the portfolio's AI/data-center buildout. CLS and FN add AI hardware/optics supply-chain exposure. MRCY, PRCT, and INSP offer more distinct defense or medical demand drivers, but issuer financial gaps prevent claiming diversification-adjusted superiority.

### Portfolio gates

- **Proof gate:** Before any candidate funding, obtain a fresh broker sync, regular-session price and EUR/USD, current cash/buying power, candidate equity value and diluted shares, then calculate post-entry total-NAV and shared AI-infrastructure exposure. **CAOS INFERENCE.**
- **Warning gate:** Any proposed funding reduces cash below **50% of current NAV**, makes one security exceed **15% of NAV**, or pushes the combined AI compute/data-center/power/equipment cluster above **45% of NAV**. These are review thresholds, not automatic trades. **CAOS INFERENCE.**
- **Break gate:** No execution while `HOLDINGS STALE / EXECUTION BLOCKED` applies, real cash cannot be separated from credit, or a total-loss stress on high-risk funded names would breach the 50% mandate. **CAOS INFERENCE.**

## Candidate risk map — Comfort Systems USA (FIX)

### Applicable risk categories

- **Concentration/customer:** Backlog quality, data-center share, top customers, and fixed-price project concentration are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Q2 operating cash flow was $1.14bn, but working-capital normalization, net debt, covenants, and maturities are **DATA LIMITED**.
- **Dilution:** Diluted shares and acquisition funding are **DATA LIMITED**.
- **Capital intensity/execution:** Skilled labor, materials, project scheduling, acquisitions, and fixed-price contracts can turn revenue growth into margin/cash loss. **CAOS INFERENCE.**
- **Regulatory/geographic:** Labor, safety, permitting, tariffs, and regional construction exposure are **DATA LIMITED**.
- **Factor/correlation:** FIX deepens data-center construction exposure already present through NVDA/MSFT/GOOGL/IREN/WULF. **CAOS INFERENCE.**

**Permanent-loss paths:** acquisition-led growth hides weak organic growth; backlog cancels; fixed-price/labor inflation compresses margins; working capital reverses; leverage rises; or valuation is excessive once verified.

- **Proof gate:** Next filing shows organic revenue growth **≥10%**, backlog stable/growing with disclosed conversion/cancellation, positive trailing FCF after working-capital normalization, stable operating margin, net leverage disclosed, and diluted shares growth **<5% YoY**. **CAOS INFERENCE.**
- **Warning gate:** Organic growth **5%-10%**; backlog declines once; operating margin falls **100 bps YoY**; trailing FCF below **75% of net income**; or net leverage rises above **2x EBITDA**. **CAOS INFERENCE.**
- **Break gate:** Organic growth below **10% for two quarters** while acquisition spending remains high; backlog declines for two quarters from cancellations/deferrals; margin compresses for two quarters from unpassed costs; trailing FCF materially trails earnings; or net leverage rises materially/diluted shares exceed **10% growth** without per-share cash growth. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`; not buy-authorized.

## Candidate risk map — Powell Industries (POWL)

### Applicable risk categories

- **Concentration/customer:** Data-center/utility/industrial shares, largest customers, backlog cancellation, and project exposure are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Cash conversion, balance sheet, capex funding, debt, and maturities are **DATA LIMITED**.
- **Dilution:** Share count and equity funding are **DATA LIMITED**.
- **Capital intensity/execution:** $934m orders versus $312m revenue imply a large conversion burden; manufacturing capacity, labor, and component delivery must scale. **CAOS INFERENCE.**
- **Regulatory/geographic:** Grid, utility, safety, local-content, and tariff exposure are **DATA LIMITED**.
- **Factor/correlation:** POWL adds electrical-equipment exposure to the same data-center/power cycle as current holdings. **CAOS INFERENCE.**

**Permanent-loss paths:** orders fail to convert; backlog carries poor margins; one project/customer creates a loss; expansion capex consumes cash; supply constraints delay delivery; or order surge proves cyclical.

- **Proof gate:** Next two filings show book-to-bill **>1.0**, backlog conversion producing **≥10% revenue growth**, gross margin **≥28%**, positive trailing FCF, no customer above **25% of revenue**, and net cash/debt plus dilution disclosed. **CAOS INFERENCE.**
- **Warning gate:** Book-to-bill **0.9-1.0**; margin **25%-28%**; backlog conversion slips one quarter; negative quarterly FCF; or a customer exceeds 25%. **CAOS INFERENCE.**
- **Break gate:** Orders fall below revenue before conversion accelerates; margin below **25% for two quarters**; cancellation/delay removes over **15% of backlog**; expansion creates negative trailing FCF with rising debt; or a concentrated project causes material loss/receivable impairment. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`; not buy-authorized.

## Candidate risk map — Celestica (CLS)

### Applicable risk categories

- **Concentration/customer:** Major-customer and AI-system-program concentration, segment mix, and contract protections are **DATA LIMITED**.
- **Liquidity/financing/maturity:** The announced $3bn equity offering may improve liquidity, but use of proceeds, debt retirement, capacity commitments, and maturity effects are **DATA LIMITED**.
- **Dilution:** **VERIFIED FACT:** a $3bn equity offering was announced. Price, issued shares, fees, and pro-forma dilution remain unavailable.
- **Capital intensity/execution:** Low adjusted operating margin of 8.2%, working capital, capacity, and customer bargaining power give little error tolerance. **CAOS INFERENCE.**
- **Regulatory/geographic:** Trade controls, tariffs, global manufacturing, and supply-chain concentration are **DATA LIMITED**.
- **Factor/correlation:** CLS increases portfolio exposure to AI hardware manufacturing and hyperscaler/OEM programs. **CAOS INFERENCE.**

**Permanent-loss paths:** dilution overwhelms per-share growth; proceeds fund low-return capacity/acquisitions; major customer loss; margin falls; or cash stays negative despite adjusted profit.

- **Proof gate:** Final offering terms show diluted-share increase **≤15%**, proceeds tied to returns above cost of equity, Q3/Q4 adjusted operating margin **≥8%**, positive trailing FCF, and no customer/program loss. **CAOS INFERENCE.**
- **Warning gate:** Dilution **15%-20%**; margin **6%-8%**; negative quarterly FCF; proceeds lack quantified return milestones; or top-customer exposure exceeds **30%** if disclosed. **CAOS INFERENCE.**
- **Break gate:** Diluted shares rise **>20%** without matched per-share FCF within four quarters; margin below **6% for two quarters**; major-customer loss causes two sequential revenue declines; proceeds fund low-return capacity/acquisitions/burn; or trailing FCF remains negative despite adjusted profit. **CAOS INFERENCE.**

**Disposition:** `SERIOUS REVIEW`, dilution-gated; not buy-authorized.

## Candidate risk map — Fabrinet (FN)

### Applicable risk categories

- **Concentration/customer:** Optical/datacom mix, top customers, and contract protections are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Operating cash flow, FCF, net cash/debt, and maturities are **DATA LIMITED**.
- **Dilution:** Diluted shares and capacity funding are **DATA LIMITED**.
- **Capital intensity/execution:** Contract manufacturing needs capacity, yields, component supply, and customer qualification; customers can retain much of the economics. **CAOS INFERENCE.**
- **Regulatory/geographic:** Asian manufacturing, tariffs, export controls, and logistics exposure are **DATA LIMITED**.
- **Factor/correlation:** FN deepens optics/AI-bandwidth exposure linked to NVDA and hyperscaler capex. **CAOS INFERENCE.**

**Permanent-loss paths:** one customer cuts programs; optical architecture shifts; margins compress; capex outruns demand; cash conversion turns negative; or routine expansion requires dilution/debt.

- **Proof gate:** Next two quarters each show revenue growth **≥25%**, stable gross/operating margins, positive OCF and FCF, no top customer above **35%**, and net cash/debt, dilution, and valuation disclosed. **CAOS INFERENCE.**
- **Warning gate:** Revenue growth **15%-25%**; margin declines one quarter; customer above 35%; or negative quarterly FCF. **CAOS INFERENCE.**
- **Break gate:** Revenue growth below **15%** before diversification improves; top-customer reduction causes sequential contraction; margins decline for two quarters; trailing OCF turns negative; or material dilution/debt funds routine capacity without returns. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; not buy-authorized.

## Candidate risk map — Mercury Systems (MRCY)

### Applicable risk categories

- **Concentration/customer:** Funded/unfunded backlog, program and government concentration, contract modifications, and receivables are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Q4 FCF was $29m, but debt, covenants, maturity, and normalized cash conversion are **DATA LIMITED**.
- **Dilution:** Share trend and acquisition equity exposure are **DATA LIMITED**.
- **Capital intensity/execution:** Defense qualification and backlog conversion are slow; bookings growth of 93.1% versus revenue growth of 6.1% creates execution burden. **CAOS INFERENCE.**
- **Regulatory/geographic:** Appropriations, procurement, security rules, export controls, and program cancellation are material. **CAOS INFERENCE.**
- **Factor/correlation:** MRCY offers more distinct defense demand than data-center candidates, but government budgets create concentration. **CAOS INFERENCE.**

**Permanent-loss paths:** backlog is unfunded/cancelled; conversion stays slow; program loss; FCF turns negative; debt/dilution funds weak growth; or margins fail to recover.

- **Proof gate:** Within next two filings, organic revenue growth reaches **≥10%**, book-to-bill stays **>1.0**, backlog is mostly funded, GAAP operating profit improves, and FCF remains positive. **CAOS INFERENCE.**
- **Warning gate:** Growth **5%-10%**; book-to-bill **1.0-1.2**; funded backlog remains undisclosed; or one negative-FCF quarter. **CAOS INFERENCE.**
- **Break gate:** Book-to-bill below **1.0 for two quarters** while backlog declines; backlog fails to create double-digit organic growth within two cycles; FCF negative for two quarters structurally; major program cancellation; or debt/shares rise without per-share cash growth. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; not buy-authorized.

## Candidate risk map — PROCEPT BioRobotics (PRCT)

### Applicable risk categories

- **Concentration/customer:** Procedure, account, recurring/service mix, reimbursement, and hospital concentration are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Operating loss, burn, cash runway, debt, and maturities are **DATA LIMITED**.
- **Dilution:** Fully diluted shares and funding need are **DATA LIMITED**.
- **Capital intensity/execution:** Placements can consume cash before procedure utilization creates recurring economics. Training, manufacturing, service, and clinical adoption must scale. **CAOS INFERENCE.**
- **Regulatory/geographic:** Safety, FDA/other approvals, reimbursement, liability, and geographic expansion are material. **CAOS INFERENCE.**
- **Factor/correlation:** Medical devices diversify AI-infrastructure exposure but add clinical/regulatory risk. **CAOS INFERENCE.**

**Permanent-loss paths:** placements rise without use; reimbursement/safety event slows adoption; cash runway collapses; dilution funds losses; recurring economics fail; or competition reduces procedure share.

- **Proof gate:** Next two quarters show revenue growth **≥18%**, procedure and recurring/service growth at least matching placement growth, narrowing operating loss/burn, and verified cash runway **>24 months** without material dilution. **CAOS INFERENCE.**
- **Warning gate:** Growth **12%-18%**; procedures lag placements; runway **12-24 months**; or diluted shares rise **5%-15% YoY**. **CAOS INFERENCE.**
- **Break gate:** Revenue growth below **12% for two quarters**; placements rise while procedures/account or recurring revenue declines; runway below 12 months without non-dilutive finance; material safety/regulatory/reimbursement restriction; or dilution exceeds **15% in twelve months** without per-share growth. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; not buy-authorized.

## Candidate risk map — Inspire Medical Systems (INSP)

### Applicable risk categories

- **Concentration/customer:** Procedure growth, reimbursement, provider concentration, sales efficiency, and competition are **DATA LIMITED**.
- **Liquidity/financing/maturity:** Q2 OCF was $23.2m, but cash normalization, net cash/debt, and maturities are **DATA LIMITED**.
- **Dilution:** Diluted shares and stock compensation are **DATA LIMITED**.
- **Capital intensity/execution:** Salesforce expansion, provider training, implants, and procedure adoption must produce operating leverage. **CAOS INFERENCE.**
- **Regulatory/geographic:** Reimbursement, safety, device approval, liability, and competing therapies are central. **CAOS INFERENCE.**
- **Factor/correlation:** Medical-device demand diversifies the data-center cluster but is exposed to healthcare budgets and reimbursement. **CAOS INFERENCE.**

**Permanent-loss paths:** raised guidance is missed; sales expense grows faster than adoption; cash turns negative; reimbursement or safety damages demand; competition wins share; or dilution/debt funds weak returns.

- **Proof gate:** Next filing meets the exact raised 2026 guide, achieves positive GAAP operating income, positive normalized OCF/FCF, stable reimbursement, and improved sales efficiency; repeat operating profit in the following quarter. **CAOS INFERENCE.**
- **Warning gate:** Results at guide floor; operating loss persists one quarter; normalized cash conversion falls below **75% of net income**; or procedure growth slows materially. **CAOS INFERENCE.**
- **Break gate:** Structural miss of raised revenue/procedure guide; operating loss widens for two quarters while sales spend rises; trailing OCF turns negative; reimbursement/safety/competitive therapy materially reduces adoption; or dilution/debt rises without per-share cash generation. **CAOS INFERENCE.**

**Disposition:** `WATCH WITH SPECIFIC TRIGGER`; not buy-authorized.

## Cross-candidate conclusion

- **Survivability-adjusted order:** FIX and POWL lead this data-limited set; INSP/MRCY follow as monitored, more diversifying lanes; FN/PRCT require basic financial closure; CLS is blocked by unreconciled dilution. **CAOS INFERENCE.**
- **Raw convexity is unrateable:** every candidate lacks a verified current denominator. No position can be sized or promoted from operating growth alone.
- **Cash decision:** With 58.8% stale-reference cash and no candidate clearing all proof gates, cash remains valid. **CAOS INFERENCE.**
- **Execution:** No purchase, sale, sizing, or Ledger/Snapshot mutation is authorized. Drawdown alone does not trigger a sell.

RISK REVIEW = DATA LIMITED
