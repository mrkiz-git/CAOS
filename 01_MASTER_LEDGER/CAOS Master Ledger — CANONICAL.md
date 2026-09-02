# CAOS Master Ledger — CANONICAL

STATUS: INITIALIZED — 2026-08-31 — intake complete, portfolio reconciled

This is the sole controlling long-term portfolio and decision record for CAOS. It is append-only. Corrections must state what was corrected, why, and what prior entry is superseded — history is never silently rewritten.

## 1. Current Mandate
**Investor:** Mark (mark@mlmn-commerce.com)
**Timezone:** Europe/Sofia
**Broker:** Revolut (fractional shares supported)
**Investing Horizon:** Long-term (5+ years, indefinite)
**Monthly Contribution:** €300
**Objective:** Maximize CAGR
**Risk Tolerance:** 40% max drawdown target (hard limit 50%)
**Leverage/Derivatives:** NO
**Restrictions:** None (no sector, geographic, security-type, or liquidity exclusions)

## 2. Current Portfolio Snapshot
STATUS: INITIALIZED — refreshed 2026-09-02
SOURCE: Revolut broker export (user-provided screenshot)
TIMESTAMP: 2026-09-02 (prices from screenshot, exact live fetch time unknown — refresh recommended before trading)
CURRENCY: Mixed (EUR for cash, USD for holdings; living portfolio — all future snapshots will use current live prices at update time)
ACCOUNT TOTAL (per broker, mixed-currency, not independently recomputed): €9,333.67 (+128.91% since account inception, per broker)

**Funded Holdings (8 securities):**
| Ticker | Company | Type | Shares | Avg Cost | Current Price | Role Status |
|--------|---------|------|--------|----------|----------------|-------------|
| PLTR | Palantir | EQUITY | 21.68808861 | $29.44 | $177.56 | CORE/ATTACKER |
| NVDA | NVIDIA | EQUITY | 14.88458404 | $98.59 | $216.89 | CORE/ATTACKER |
| MSFT | Microsoft | EQUITY | 1.96105021 | $356.11 | $497.14 | CORE/ATTACKER |
| KO | Coca-Cola | EQUITY | 11.07061496 | $68.13 | $88.11 | CORE/ATTACKER |
| GOOGL | Alphabet Class A | EQUITY | 1.85516511 | $106.45 | $336.75 | CORE/ATTACKER |
| TSLA | Tesla | EQUITY | 1.67642235 | $213.97 | $356.00 | CORE/ATTACKER |
| IREN | Iris Energy | EQUITY | 8.1098693 | $37.61 | $36.01 | CORE/ATTACKER |
| WULF | Terawulf Inc | EQUITY | 18.91535598 | $16.12 | $14.46 | CORE/ATTACKER |

**Cash:**
| Currency | Amount | Type | Availability |
|----------|--------|------|---------------|
| EUR | €0.95 | Real unlevered cash | Full |
| USD | $0.00 | Real unlevered cash | None |

CORRECTION (2026-09-02): the €1,000.95 cash figure recorded at 2026-08-31 intake was wrong — Mark confirmed real cash has always been €0.95, not €1,000.95. No transaction occurred; this is a data-entry fix, not a withdrawal. See Event 1 in §8.

## 3. Real Cash vs. Buying Power
STATUS: INITIALIZED (2026-08-31), cash figure corrected 2026-09-02

**Real unlevered cash:** €0.95 (in broker, no margin, no leverage)
**Broker buying power:** equal to real cash (no credit line, no margin account)
**Committed to monthly contribution:** €300/month (future contribution, not yet in account)
**Constraint:** Leverage explicitly prohibited; all positions unlevered

## 4. Funded-Security Roles
STATUS: INHERITED (8 securities, pre-CAOS portfolio intake, roles need assignment)

All 8 holdings from Revolut export are marked tentatively as CORE/ATTACKER pending CAOS mandate review. These will be formally re-evaluated in the first post-intake Deep Audit (to be scheduled). No sizing changes or sell decisions may be made until this review completes.

**Holds awaiting formal role assignment:**
- PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF (all inherited, pre-CAOS intake)

## 5. Candidate / Status Registry
STATUS: EMPTY
No candidates recorded yet. Permitted states: UNKNOWN, WATCH WITH SPECIFIC TRIGGER, SERIOUS REVIEW, HIGH-PRIORITY CHALLENGER, CHALLENGER, BUY-AUTHORIZED SEED, CORE / ATTACKER, PORTFOLIO REPLACEMENT CANDIDATE, REJECT, RETIRED / ARCHIVED, RESOLVED.

## 6. Active Evidence Gates and Tribunals
STATUS: EMPTY

## 7. Standardized Handoff Index
STATUS: EMPTY
See [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] for the live unresolved queue.

## 8. Material CAOS EVENT History
STATUS: INITIALIZED

### Event 0: CAOS System Initialization
============================================================
CAOS EVENT
============================================================
EVENT_ID = 2026-08-31-SYSTEM-INIT
EVENT_TYPE = SYSTEM_INITIALIZATION
MODULE = MASTER_LEDGER
TIMESTAMP_LOCAL = 2026-08-31 (intake completion)
DECISION_AUTHORITY = Mark
EXECUTION_AUTHORITY = Mark only
TRANSACTION_RESULT = NO TRADE

SOURCE_AND_PORTFOLIO_STATE
- Revolut broker account, Sofia, Bulgaria
- 8 funded securities (PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF)
- €1,000.95 real unlevered cash
- All USD holdings, EUR cash (living mixed-currency portfolio)

PREVIOUS_STATE
- CAOS system UNINITIALIZED
- No portfolio state recorded
- All products running in research-only / degraded mode

NEW_STATE
- CAOS Master Ledger INITIALIZED
- Current portfolio snapshot reconciled against broker
- System ready for production execution
- All products now able to run in portfolio-aware mode

VERIFIED EVIDENCE
- User intake completed: timezone (Europe/Sofia), broker (Revolut with fractional support), cash (€1,000.95), monthly contribution (€300), risk mandate (maximize CAGR with 40% max drawdown target, 50% hard limit), leverage (prohibited), restrictions (none)
- Broker portfolio screenshot verified: 8 holdings + €0.95 residual cash
- Available capital: €1,000.95 unlevered

CAOS INTERPRETATION
- System initialization is a prerequisite for all portfolio-aware products (Monster Census, Weekly Ranking, Emergency Thesis Rerun, etc.)
- Inherited portfolio (8 holdings) now requires formal CAOS mandate review via Deep Audit
- No holdings are pre-approved under CAOS process; all role assignments pending

SURVIVABILITY / FINANCING / DILUTION
- Not applicable (system event, not portfolio event)

ACTIONABILITY
- Next step: Execute Monster Census for first discovery sweep (scheduled Saturday 09:00)
- Subsequent: Schedule first Deep Audit to formally review role assignments for 8 inherited holdings

NEXT PROOF GATE
- Monster Census completion: 2026-08-31 (TODAY) or 2026-09-07 (next Saturday if deferred)
- Deep Audit assignment: TBD

SUPERSEDES / RESOLVES
- None (inaugural event)
============================================================
END CAOS EVENT
============================================================

### Event 1: Cash Figure Correction + Price Refresh
============================================================
CAOS EVENT
============================================================
EVENT_ID = 2026-09-02-LEDGER-CASH-CORRECTION
EVENT_TYPE = LEDGER_CORRECTION
MODULE = MASTER_LEDGER
TIMESTAMP_LOCAL = 2026-09-02 (Europe/Sofia)
DECISION_AUTHORITY = Mark
EXECUTION_AUTHORITY = Mark only
TRANSACTION_RESULT = NO TRADE

SOURCE_AND_PORTFOLIO_STATE
- Revolut broker export (user-provided screenshot), 2026-09-02
- Same 8 funded securities as Event 0, unchanged share counts (confirmed to 8 decimal places against the 8/31 intake)
- Cash: €0.95 (screenshot "Cash balance", both Total and Available to invest)

PREVIOUS_STATE
- Master Ledger §2/§3 recorded real cash as €1,000.95 as of 2026-08-31 intake

NEW_STATE
- Real cash corrected to €0.95
- All 8 holdings' Current Price refreshed to 2026-09-02 broker snapshot
- No change to share counts, avg cost, or role status

VERIFIED EVIDENCE
- Mark directly confirmed (2026-09-02, in response to a direct question about the €1,000 discrepancy): the original €1,000.95 figure was wrong at intake — real cash has always been €0.95
- No entry exists in §9 Confirmed Transactions/Fills between 2026-08-31 and 2026-09-02, and no holding's share count changed — ruling out an unlogged buy as the explanation

CAOS INTERPRETATION
- This is a correction of a bad intake data point, not a portfolio event (no cash left the account; it was never there in the recorded amount)
- Per Radical Honesty and Fresh-Evidence Supremacy, the wrong figure is corrected here rather than silently edited — Event 0 above is left untouched as the historical record of what was recorded at the time

SURVIVABILITY / FINANCING / DILUTION
- Not applicable

ACTIONABILITY
- Real investable cash is €0.95, not €1,000.95 — do not size any near-term action assuming the larger figure
- Monthly €300 contribution (§1) remains the actual source of future deployable cash

NEXT PROOF GATE
- Next broker screenshot/export reconciliation

SUPERSEDES / RESOLVES
- Corrects the cash figure stated in Event 0 (2026-08-31-SYSTEM-INIT); Event 0 itself is not superseded, only its cash figure
============================================================
END CAOS EVENT
============================================================

## 9. Confirmed Transactions / Fills
STATUS: EMPTY

## 10. Supersession and Resolution Map
STATUS: EMPTY

## 11. System Rules and Amendments
Draft portfolio-count rules (pending Mark's confirmation):
- target cap: seven funded public securities
- maximum two funded CAOS Seeds
- Core/Attacker positions should normally have a credible path toward approximately 5% of NAV
- Seeds normally occupy approximately 1%-3%
- sub-approximately-1.5% positions require an explicit Seed/Catalyst role and proof gate
- permanent sub-1% orphans are prohibited
- a Seed must graduate, remain under an exact evidence gate, or exit after two decisive evidence cycles
- no new funded security if the post-entry portfolio would exceed the confirmed cap
- drawdown alone is neither a sell reason nor a hold reason

These remain DRAFT until Mark explicitly approves or amends them.

## 12. Historical Archive
STATUS: EMPTY
