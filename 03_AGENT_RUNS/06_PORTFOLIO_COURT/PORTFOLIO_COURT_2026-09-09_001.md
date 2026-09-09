# PORTFOLIO COURT RUN — 2026-09-09_001

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-09_001]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-09_001]] — fresh portfolio state supplied for this run
- [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court]]

## Scope and Controlling State

- **VERIFIED FACT:** The fresh broker screenshot displays six funded holdings: NVDA 7.44229202, MSFT 1.96105021, TSLA 1.67642235, GOOGL 1.85516511, IREN 8.1098693, and WULF 18.91535598. It displays €5,465.84 cash and the same amount available to invest.
- **CAOS INFERENCE:** Under the initialized no-leverage mandate, €5,465.84 is treated as real unlevered cash.
- **DATA LIMITED:** The screenshot establishes displayed holdings and cash, but not execution dates, fill prices, fees, FX, or transaction sequence. The Ledger event describes confirmed fills, while Ledger §9 remains empty and the fresh Verifier says fill history is unconfirmed. Fresh-evidence supremacy applies: the Court uses the new portfolio state but makes no fill claim.
- **VERIFIED FACT:** The corrected Underwriter covers only CEG, ISRG, CIFR, and ONDS as candidates. It uses IREN and WULF only as opportunity-cost comparators. NVDA, MSFT, GOOGL, and TSLA have no fresh comparable underwriting in this run.

## Handoff Acknowledgement Checks

`HANDOFF ACK CHECK: 20260902-DAILY-ONDS-NEW_CHALLENGER | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=HIGH-PRIORITY CHALLENGER retained; dilution is now verified and the cash-conversion gate remains open | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=Fresh screenshot displays 6 funded securities, below the draft cap of 7; transaction history remains DATA LIMITED and only the Orchestrator may resolve the handoff | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260902-DAILY-WULF_IREN-EVIDENCE_GATE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=Both remain funded and gated; CIFR does not clear either incumbent because it has no reported HPC revenue and adds the same risk lane | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

## 1. 100%-Cash Trial

**Evidence-default decision:** if the whole portfolio were cash today and this run were the only allowed evidence set, the Court would keep the first euro in **CASH**. This is a hold-cash instruction under incomplete comparative evidence. It is not a proven claim that cash has the highest expected CAGR.

**Why:** none of the four candidates is buy-authorized, and four of the six current holdings lack fresh comparable underwriting. IREN and WULF retain open financing or counterparty gates. The Court cannot convert incomplete evidence into a positive ownership claim.

### Candidate ranking within the evidence actually underwritten

1. **ISRG — CHALLENGER.** Highest business quality and corporate survivability in the candidate set. Recurring procedure-linked revenue, strong cash generation, and a large net-liquidity position support the best survivability-adjusted profile. Its valuation makes a near-term 3x unlikely.
2. **ONDS — HIGH-PRIORITY CHALLENGER.** Best raw convexity and smallest denominator. It ranks below ISRG on evidence-adjusted attractiveness because operating cash burn, acquisition integration, and approximately 39% six-month share-count growth weaken per-share compounding.
3. **CEG — WATCH WITH SPECIFIC TRIGGER.** Profitable, cash-generative, and investment grade, but the large denominator, Calpine debt, acquisition dilution, and limited AI-specific economics cap expected upside from today.
4. **CIFR — WATCH WITH SPECIFIC TRIGGER.** Strong contracted HPC evidence and meaningful raw upside, but reported revenue remains entirely bitcoin mining. Restricted cash, project debt, construction risk, and overlap with IREN/WULF make it the weakest survivability-adjusted candidate today.

### Current holdings in the 100%-cash trial

- **NVDA / MSFT / GOOGL / TSLA:** **UNKNOWN** expected CAGR in this run. They are real alternatives but cannot be ranked from reputation, cost basis, or prior conclusions.
- **IREN / WULF:** **DATA LIMITED** for a full expected-CAGR rank. Both remain under active evidence gates; the Underwriter only establishes that CIFR has not proven superior operating HPC economics.

**100%-cash result:** CASH is the evidence-default holding state. Among the fully underwritten candidates, ISRG ranks first on survivability-adjusted attractiveness and ONDS ranks first on raw convexity. No security wins a proven whole-portfolio expected-CAGR trial.

## 2. Next-Uncommitted-Euro Decision and Ranking

### A. Evidence-default instruction

**Keep the next uncommitted euro in CASH pending the missing comparative proof.** This is not trade execution, sizing, or a claim that cash maximizes long-run returns. It is the correct default when no candidate clears the ownership burden and major current alternatives remain unranked.

### B. What is and is not proven about expected CAGR

**No complete expected-CAGR ranking is proven.** The Underwriter gives denominators, operating evidence, raw convexity regimes, time ranges, and survivability-adjusted attractiveness. It does not supply probability-weighted expected returns for all candidates and holdings. Therefore, the Court will not label the cash-first default as an expected-CAGR victory.

The strongest defensible ranking is:

1. **ISRG** — best survivability-adjusted candidate; CHALLENGER, not buy-authorized.
2. **ONDS** — best raw-convexity candidate; HIGH-PRIORITY CHALLENGER, not buy-authorized.
3. **CEG** — high survivability but lower convexity and material acquisition leverage; trigger-gated Watch.
4. **CIFR** — meaningful tail upside but pre-revenue in HPC and financing-heavy; trigger-gated Watch.

**IREN, WULF, NVDA, MSFT, GOOGL, and TSLA remain outside this candidate ordinal.** The current evidence does not support a comparable expected-CAGR number for them. CIFR fails to displace IREN or WULF, but that narrow result does not rank those two against ISRG, ONDS, or the four other holdings.

## 3. Business Quality, Raw Asymmetry, and Portfolio Role

- **ISRG:** business quality HIGHEST in the candidate set; corporate survivability VERY GOOD; raw 3x possible only over a long period; survivability-adjusted attractiveness MODERATE-TO-GOOD; state CHALLENGER.
- **ONDS:** business quality MODERATE; raw convexity HIGHEST; 3x credible but not proven over an estimated 3–6 years; survivability-adjusted attractiveness MODERATE; state HIGH-PRIORITY CHALLENGER.
- **CEG:** business quality and survivability GOOD; raw 3x LOW CREDIBILITY and likely requires 7–12 years; survivability-adjusted attractiveness MODERATE; state WATCH WITH SPECIFIC TRIGGER.
- **CIFR:** current HPC operating quality UNKNOWN because no HPC revenue is reported; raw 3x is a credible tail, not proven; survivability-adjusted attractiveness MODERATE-LOW; state WATCH WITH SPECIFIC TRIGGER.
- **NVDA / MSFT / GOOGL / TSLA:** fresh business quality, valuation, and expected CAGR are UNKNOWN in this run.
- **IREN / WULF:** comparison evidence is DATA LIMITED. Both remain funded under an active financing/counterparty gate.

Raw-convexity order from the Underwriter is **ONDS > CIFR > CEG > ISRG**. Corporate-survivability order is **ISRG > CEG > ONDS > CIFR**. These different orders show why raw upside alone cannot decide where the next euro goes.

## 4. Opportunity-Cost Tribunal

- **ISRG versus cash:** ISRG has the strongest candidate quality, but its valuation and long 3x path prevent a proven minimum edge over cash today. Cash wins only as the evidence default.
- **ONDS versus cash:** ONDS has stronger raw upside, but dilution, burn, and uncertain organic growth prevent a proven per-share edge. Cash remains the default.
- **CEG versus cash:** CEG can compound, but the denominator, Calpine leverage, and acquisition dilution prevent a proven asymmetric edge.
- **CIFR versus cash:** cash wins decisively until non-mining HPC revenue begins and project economics are visible.
- **CIFR versus IREN/WULF:** CIFR does not prove superior operating HPC economics and would add concentration in the same infrastructure/financing lane.
- **Best Challenger versus strongest owned name and quality anchor:** **UNKNOWN.** ISRG is the best quality Challenger and ONDS the best asymmetric Challenger, but no current holding has enough fresh comparable underwriting to name or defeat a strongest owned anchor.
- **Best Seed:** none. The Ledger registry and Active Handoff Snapshot show no funded Seed.

**Opportunity-cost ruling:** no candidate proves a better claim on the next euro than every real alternative. The missing current-holdings comparison is decisive, not a minor disclosure.

## 5. Capital-Recycling Tribunal

**NO CAPITAL-RECYCLING CASE IS PROVEN.**

- CIFR cannot replace IREN or WULF: it lacks reported HPC revenue and adds the same construction, financing, and concentration lane.
- ISRG offers the strongest quality diversification and ONDS the strongest raw convexity, but neither proves a survivability-adjusted expected-CAGR advantage over a specific funded holding.
- CEG offers firm-power exposure but diversification alone is not a reason to fund it.
- Four holdings have no fresh comparable underwriting, so naming a source position for recycling would invent an opportunity-cost conclusion.

This tribunal issues no sell, swap, buy, sizing, or allocation instruction.

## 6. Portfolio-Count and No-Orphan Checks

- **Portfolio count — VERIFIED FACT:** the freshest screenshot displays 6 funded public securities. This is below the Ledger §11 draft target cap of 7. The earlier 8-security displayed condition is no longer present.
- **Rule status — VERIFIED FACT:** all §11 count and sizing rules remain DRAFT until Mark confirms or amends them.
- **Seed count — VERIFIED FACT:** 0 funded CAOS Seeds versus the draft maximum of 2.
- **No-Orphan check — CAOS INFERENCE:** screenshot quantities and USD prices place every displayed holding at roughly $340 or more. No sub-1% residual is evident against the broker total. Exact weights are DATA LIMITED because total account value is in EUR, holdings are priced in USD, and no same-time broker FX conversion is supplied.
- **Count capacity — CAOS INFERENCE:** one new funded security would take the displayed count to 7, not above it. Count capacity is not evidence of merit and creates no authorization.

## Court Disposition

- **Evidence-default next-euro state:** CASH.
- **Proven expected-CAGR winner:** NONE; the comparable ranking is incomplete.
- **ISRG:** CHALLENGER for downstream comparison.
- **ONDS:** HIGH-PRIORITY CHALLENGER retained; dilution gap closed, cash-conversion gate open.
- **CEG:** WATCH WITH SPECIFIC TRIGGER.
- **CIFR:** WATCH WITH SPECIFIC TRIGGER retained; require reported non-mining HPC revenue and visible delivery economics.
- **IREN / WULF:** active evidence gates remain; CIFR does not displace them.
- **NVDA / MSFT / GOOGL / TSLA:** funded state verified, but fresh ranking evidence is UNKNOWN.

`PORTFOLIO COURT = RANKING COMPLETE`
