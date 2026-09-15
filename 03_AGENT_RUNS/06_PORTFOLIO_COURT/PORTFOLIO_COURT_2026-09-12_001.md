# PORTFOLIO COURT RUN — 2026-09-12_001

## Inputs Consulted

- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-12_001]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-12_001]] — execution-state confirmation

## Court Boundary

- **VERIFIED FACT:** The controlling portfolio contains NVDA, MSFT, GOOGL, TSLA, IREN, and WULF, plus last-verified cash of €5,487.36.
- **DATA LIMITED:** Holdings and prices are stale on Saturday 2026-09-12. Current cash, prices, FX, spreads, and any activity after the 2026-09-11 screenshot are unavailable.
- **VERIFIED FACT:** The same-day Underwriter rated all seven new referrals only `PARTIAL`; no current valuation denominator was available for any of them, and CLS has an unreconciled $3bn equity offering.
- **CAOS INFERENCE:** Research ranking can proceed, but exact allocation and execution cannot. `HOLDINGS STALE / EXECUTION BLOCKED`.

## Active Handoff Acknowledgements

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-PORTFOLIO-REBALANCE-REVIEW | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=Prior rebalancing direction remains the controlling research view; no exact weight or action is permitted with stale broker, FX, and fill data | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-IREN_WULF-UPDATED_GATE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=IREN and WULF remain funded but fail the unrestricted fresh-euro test until delivery, financing, rent, and retained-economics gates close | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260911-DEEPAUDIT-ONDS-STATE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=ONDS remains a 0%-funding Watch and does not enter the next-euro ranking | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

## 100%-Cash Holdings Trial

Hypothesis: every funded position is sold conceptually and the whole account is uncommitted cash. This is a ranking test, not a sale proposal.

### Names that survive the fresh-cash trial

1. **MSFT — strongest owned quality candidate.** **CAOS INFERENCE:** Durable enterprise platform, contracted backlog, and cash generation make it the strongest owned fresh-capital inclusion in the current record. Exact expected CAGR is **DATA LIMITED** without a current valuation.
2. **GOOGL — owned quality inclusion.** **CAOS INFERENCE:** Cloud backlog and a diversified cash engine support inclusion, subject to capex-return and valuation proof.
3. **NVDA — owned attacker inclusion, concentration-limited.** **CAOS INFERENCE:** Operating evidence remains strong, but cyclicality, customer concentration, and the existing portfolio's AI-capex exposure argue against automatic first rank.
4. **CRDO — strongest current Challenger, gate-dependent.** **VERIFIED FACT:** The Ledger records it as a Challenger. **CAOS INFERENCE:** It offers more raw asymmetry than the three large incumbents, but concentration, cash conversion, dilution, architecture, and valuation gaps prevent unrestricted inclusion.
5. **ISRG — quality-anchor Seed candidate.** **VERIFIED FACT:** The Ledger records it as a Seed candidate. **CAOS INFERENCE:** It is the best portfolio diversifier among tracked Seeds, but still requires its procedure, margin, recurring-revenue, and valuation gates.
6. **AXON and CEG — conditional alternatives.** **CAOS INFERENCE:** Both may diversify the portfolio and have stronger evidence than today's new referrals, but open cash-conversion/valuation or debt/accretion gates keep them below the first five.

### Names that do not survive at current conviction

- **TSLA:** **CAOS INFERENCE:** Optionality remains, but binding commercial evidence and expected-return precision are too weak for its current-size fresh-cash inclusion.
- **IREN:** **CAOS INFERENCE:** Contract and financing evidence improved, but delivery and retained economics remain open.
- **WULF:** **CAOS INFERENCE:** Current HPC revenue is real, but project economics, rent commencement, leverage, and tenant support remain open.
- **FIX, POWL, CLS, FN, MRCY, PRCT, INSP:** **DATA LIMITED:** None clears the cash hurdle today because current valuation is missing. FIX and POWL merit comparison work; CLS is also dilution-gated.

### Trial result

**CAOS INFERENCE:** A fresh portfolio would be built first around MSFT, GOOGL, and NVDA, then would admit CRDO, ISRG, AXON, or CEG only after their named gates and valuation checks. It would not recreate the current TSLA/IREN/WULF weights. A material cash reserve remains valid while those comparisons are incomplete.

## Next-Uncommitted-Euro Ranking

This ranks research priority and capital claim. It is not an order.

1. **CASH — current operational winner.** **VERIFIED FACT:** Execution is blocked and no new candidate has a decision-grade valuation. Cash therefore has the highest valid claim on the next euro today.
2. **MSFT — strongest owned name.** **CAOS INFERENCE:** First investable alternative once live price, FX, and valuation are restored.
3. **GOOGL.** **CAOS INFERENCE:** Similar quality with capex-return and regulatory risks.
4. **NVDA.** **CAOS INFERENCE:** Highest owned AI asymmetry, but lower diversification value and greater cycle/concentration exposure.
5. **CRDO — best Challenger.** **CAOS INFERENCE:** Stronger raw convexity, weaker evidence breadth and per-share proof.
6. **ISRG — quality anchor / best Seed.** **CAOS INFERENCE:** Strong diversification and survivability, but likely lower raw asymmetry and still valuation-gated.
7. **AXON.** **CAOS INFERENCE:** Strong recurring platform evidence; stock compensation, cash conversion, and valuation remain open.
8. **CEG.** **CAOS INFERENCE:** Power scarcity exposure and survivability are attractive; Calpine debt and per-share accretion gates remain.
9. **FIX.** **CAOS INFERENCE:** Best same-day new referral by evidence breadth, but organic growth, cash normalization, backlog, and valuation are missing.
10. **POWL.** **CAOS INFERENCE:** Stronger new-name raw convexity than FIX, but order conversion and denominator evidence are weaker.
11. **INSP / MRCY / FN / PRCT.** **DATA LIMITED:** Watch tier only; each lacks enough valuation and issuer-economics evidence for a capital claim.
12. **CLS.** **DATA LIMITED:** Strong operating growth is outweighed by the unreconciled $3bn offering and unknown post-offering per-share denominator.
13. **TSLA / IREN / WULF / ONDS.** **CAOS INFERENCE:** No next-euro claim while their existing proof gates remain open.

**Ranking confidence:** low-to-moderate. Exact expected CAGR cannot be compared because live valuation denominators are missing or stale.

## Mandatory Comparator Trials

### New referrals versus cash

- **FIX vs cash:** Cash wins today. FIX needs normalized cash flow, organic growth, backlog quality, leverage, dilution, and valuation.
- **POWL vs cash:** Cash wins today. A 158% order surge is not enough without backlog conversion, cancellation, capacity, and valuation evidence.
- **CLS vs cash:** Cash wins decisively until the $3bn offering and post-offering share count are reconciled.
- **FN, MRCY, PRCT, INSP vs cash:** Cash wins because these remain trigger-gated Watches.

### New referrals versus strongest owned name (MSFT)

**CAOS INFERENCE:** MSFT wins on demonstrated scale, business quality, and evidence breadth. FIX and POWL may offer more raw convexity, but that cannot be converted into a higher expected-CAGR rank without current valuations and full per-share economics.

### New referrals versus quality anchor (ISRG)

**CAOS INFERENCE:** ISRG wins on recurring economics, diversification, and survivability evidence already in the Ledger. FIX could challenge after cash normalization and valuation; POWL could challenge on raw convexity after order conversion; none does so today.

### New referrals versus best Challenger (CRDO)

**CAOS INFERENCE:** CRDO keeps the lead because it is further through the current evidence chain. FIX may become the more survivable alternative, and POWL may offer a different physical-bottleneck path, but neither has a closed denominator. CLS cannot challenge before dilution reconciliation.

## Capital-Recycling Tribunal

### TSLA

- **Opportunity cost:** High. It ranks below cash, all three owned quality names, and the leading tracked alternatives.
- **Tribunal result:** **RECYCLING CASE REMAINS OPEN.** **CAOS INFERENCE:** Current ownership does not earn protection. A fresh portfolio would not recreate the present exposure, but no sale instruction is issued.

### IREN

- **Opportunity cost:** High while delivery and retained economics remain unverified.
- **Tribunal result:** **RECYCLING CASE REMAINS OPEN PENDING GATE.** Contract optionality is not ignored, but it does not beat cash or the leading alternatives today.

### WULF

- **Opportunity cost:** Highest among funded names because its Watch role competes with stronger owned and tracked alternatives.
- **Tribunal result:** **RECYCLING CASE REMAINS OPEN PENDING 2026-09-15 GATE.** No action is authorized.

### NVDA, MSFT, GOOGL

- **Tribunal result:** **RETAIN IN FRESH-CASH MAP.** This protects no current weight. NVDA still requires concentration discipline, while all three require live valuation before new capital.

### New-candidate displacement result

**CAOS INFERENCE:** FIX and POWL strengthen the evidence that TSLA/IREN/WULF face real opportunity cost, but incomplete underwriting means neither newly discovered name independently justifies recycling capital today.

## Portfolio-Count Check

- **VERIFIED FACT:** Current funded-security count is six.
- **VERIFIED FACT:** Ledger §11 states a seven-security target cap, but Event 3 also states these rules remain **DRAFT** until Mark confirms or amends them.
- **Result:** Six does not exceed the draft cap. One theoretical slot exists, but an empty slot is not a reason to fund a weak or incomplete candidate. Today's new referrals do not clear the cash hurdle.

## No-Orphan Check

- **VERIFIED FACT:** The Ledger's draft rule prohibits permanent sub-1% positions and requires an explicit Seed/Catalyst role plus proof gate for permanent sub-1.5% positions.
- **DATA LIMITED:** Current EUR weights cannot be verified because prices and EUR/USD are stale/unavailable.
- **Result:** Exact compliance cannot be recalculated today. WULF's Watch role and all small-position roles require live weights and dated resolution. No new orphan is proposed.

## Court Decision

- The 100%-cash trial retains MSFT, GOOGL, and NVDA as the owned quality base; CRDO, ISRG, AXON, and CEG remain conditional replacements/additions.
- Cash ranks first for the next uncommitted euro because execution is blocked and no same-day candidate has a complete valuation denominator.
- FIX and POWL advance to direct-comparison work; CLS remains serious-review but dilution-gated. None is funding-ready.
- The capital-recycling case against the current TSLA/IREN/WULF exposure remains open, not executed.
- Portfolio count is within the draft cap; No-Orphan compliance is **DATA LIMITED** until live weights are available.

PORTFOLIO COURT = RANKING COMPLETE
