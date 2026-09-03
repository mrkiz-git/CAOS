# CAOS — Active Handoff Snapshot

This is the live, unresolved cross-module queue — not the holdings ledger. It contains only active, unresolved items. Never erase an unresolved item created by another module; resolve or supersede it explicitly.

## Operating Rules
- Handoff format: see [[CAOS — OPERATOR MANUAL#9. Standardized Handoff Protocol]]
- Every consumer must output an ACK check when it reads a handoff here.
- Only the Orchestrator updates this file, and only when authorized and verified.

## Active Hunter Signals
None. (Hunter Watch product has no real run yet.)

## Challengers
- ONDS (Ondas Holdings) — see [[#HANDOFF_ID = 20260902-DAILY-ONDS-NEW_CHALLENGER]]

## Seeds
None.

## Trigger Watches
None.

## Event Gates
- WULF/IREN Anthropic-credit evidence gate — see [[#HANDOFF_ID = 20260902-DAILY-WULF_IREN-EVIDENCE_GATE]]

## Tribunals
- Portfolio-count / concentration overage — see [[#HANDOFF_ID = 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE]]

## Source Status
Per [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-02_001]]: Master Ledger READY (self-consistent), Active Handoff Snapshot READY, market-status WebSearch READY, equity-quote WebSearch DEGRADED (no dedicated financial-data API; TSLA/IREN/WULF prices internally conflicting across sources), dedicated financial-data API UNAVAILABLE. `DATA QUALITY = DEGRADED` as of 2026-09-02.

## Acknowledgements
None yet — these are new handoffs from today's run, not yet consumed by a downstream product.

## Last Writer
Orchestrator, Weekly Ranking run 2026-09-03_0740 — see [[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_2026-09-03_0740_WEEKLY]] (no new handoffs emitted this run; all 3 open items re-ACK'd and left open)

---

## HANDOFF_ID = 20260902-DAILY-ONDS-NEW_CHALLENGER
```
HANDOFF_ID = 20260902-DAILY-ONDS-NEW_CHALLENGER
ORIGIN_MODULE = DAILY
ORIGIN_DATE = 2026-09-02
SECURITY/TICKER = ONDS
HANDOFF_TYPE = CANDIDATE_STATE
SOURCE = Daily Anchor Discovery + Underwriter + Portfolio Court, 2026-09-02 run
SOURCE_SIGNAL_DATE = 2026-09-02
DEDUP_KEY = DAILY|ONDS|NEW_CHALLENGER|2026-09-02
PREVIOUS_STATE = Not tracked
NEW_STATE = HIGH-PRIORITY CHALLENGER (watch, not funded)
EVIDENCE_QUALITY = MEDIUM — Q2 2026 revenue +67% QoQ and FY26 guidance raise are VERIFIED FACT; the $982M IDIQ figure is a ceiling (only ~24% actually awarded, corrected from Discovery's initial framing); dilution/cash-raise history is UNVERIFIED LEAD, the single largest closeable gap
THESIS_OR_ASYMMETRY_CHANGE = Defense-tech/autonomous-drone name with real, verified revenue growth; Portfolio Court's own tribunal notes its evidence is "arguably cleaner" than WULF's (an already-funded holding), the closest call in this run
SURVIVABILITY_OR_FINANCING_CHANGE = Cash pile (~$1.4B at 2026-06-30) is ~44% of market cap — raises the question of how much was raised via dilutive equity vs. organic generation; ~$325M already deployed for DZYNE/Cyber Hawk acquisitions in Q3 2026, reducing the cushion
NEXT_GATE = Q3/Q4 2026 report confirming FY26 guidance ($525M–$550M) is reaffirmed/raised AND Army IDIQ awarded-task-order total surpasses $400M (from ~$240M); or, sooner, a primary-source (SEC EDGAR) pull confirming the "$217M stock offering" terms and share-count-vs-revenue growth
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Underwriter/Verifier cycle that closes the dilution-history gap
REQUIRED_CONSUMERS = DAILY, WEEKLY, CENSUS
MANDATORY_DEEP_UNDERWRITING = NO
```

## HANDOFF_ID = 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE
```
HANDOFF_ID = 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE
ORIGIN_MODULE = DAILY
ORIGIN_DATE = 2026-09-02
SECURITY/TICKER = PORTFOLIO (all 8 holdings)
HANDOFF_TYPE = SYSTEM_STATE
SOURCE = Daily Anchor Portfolio Court + Risk and Survivability, 2026-09-02 run
SOURCE_SIGNAL_DATE = 2026-09-02
DEDUP_KEY = DAILY|PORTFOLIO|COUNT_OVERAGE|2026-09-02
PREVIOUS_STATE = Not previously flagged (first Portfolio Court run against an INITIALIZED Ledger)
NEW_STATE = Portfolio holds 8 funded securities against Master Ledger §11's DRAFT cap of 7 — already over before any new candidate is considered. Paired finding: PLTR (~35.6%) and NVDA (~29.8%) are both multiples over the equally-DRAFT ~5% Core/Attacker sizing norm — Red Team flagged that this run was treating the count breach as more decisional than the (larger, in dollar terms) sizing breach, despite both rules carrying identical DRAFT/unconfirmed status
EVIDENCE_QUALITY = HIGH (arithmetic on Ledger's own recorded share counts and prices) for the count and position-size math; MEDIUM for the underlying prices themselves (Verifier's DATA QUALITY = DEGRADED this run)
THESIS_OR_ASYMMETRY_CHANGE = Not a single-security thesis change — a structural/rule-conformance finding
SURVIVABILITY_OR_FINANCING_CHANGE = Not applicable
NEXT_GATE = Deep Audit — resolve the count and sizing overage together, not separately; also requires Mark to confirm, amend, or reject the §11 draft rules themselves before either finding can become a binding block
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = First Deep Audit
REQUIRED_CONSUMERS = DAILY, WEEKLY, CENSUS
MANDATORY_DEEP_UNDERWRITING = YES
```

## HANDOFF_ID = 20260902-DAILY-WULF_IREN-EVIDENCE_GATE
```
HANDOFF_ID = 20260902-DAILY-WULF_IREN-EVIDENCE_GATE
ORIGIN_MODULE = DAILY
ORIGIN_DATE = 2026-09-02
SECURITY/TICKER = WULF, IREN
HANDOFF_TYPE = EVIDENCE_GATE
SOURCE = Daily Anchor Underwriter + Risk and Survivability + Red Team, 2026-09-02 run
SOURCE_SIGNAL_DATE = 2026-09-02
DEDUP_KEY = DAILY|WULF_IREN|EVIDENCE_GATE|2026-09-02
PREVIOUS_STATE = Not previously flagged (first Daily Anchor run since intake with both names funded)
NEW_STATE = Both names' bitcoin-mining-to-AI/HPC pivot is real and underway. IREN's is financed via an investment-grade-rated Microsoft-backed facility but only 18% of trailing FY26 revenue is AI Cloud (82% still mining) and ~$8B of FY27 capex remains unfinanced. WULF's largest contract ($19B, Anthropic) rests on an unrated, privately-financed, pre-IPO counterparty with no revenue until H2 2027, on materially higher leverage — but WULF's trailing revenue mix (71% HPC-derived, VERIFIED FACT) is already further along its pivot than IREN's. Red Team found the WULF-riskier-than-IREN framing was restated three times across the report chain without independent re-verification at each stage — directionally correct, magnitude overstated.
EVIDENCE_QUALITY = MEDIUM — the pivot and revenue-mix figures are VERIFIED FACT; Anthropic's own credit standing and IREN's private-placement pricing terms remain UNVERIFIED LEAD / DATA LIMITED, sourced only via WebSearch snippets, not primary filings
THESIS_OR_ASYMMETRY_CHANGE = Both names' investment case has partially shifted from bitcoin-mining-economics-exposed toward AI-hosting/power-exposed; treat as in-progress for both, not settled for either
SURVIVABILITY_OR_FINANCING_CHANGE = WULF: $5.8B total debt (~63% of a naive debt+equity cap), refinancing/conversion risk on $2.5B convertible notes ahead of H2 2027 revenue start. IREN: ~$8B FY27 financing gap still a management aspiration, not secured.
NEXT_GATE = Next Verifier/Underwriter cycle: independently verify Anthropic's credit standing (IPO timing, debt covenants, revenue durability) via primary sources, not WebSearch snippets — this is the single most consequential open gap in this run. Also close IREN's private-placement pricing terms. Dated break/warning gates for both names are defined in [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_SURVIVABILITY_2026-09-02_001]].
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Verifier/Underwriter cycle that closes the Anthropic-credit gap
REQUIRED_CONSUMERS = DAILY, WEEKLY, CENSUS
MANDATORY_DEEP_UNDERWRITING = YES
```
