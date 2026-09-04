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
- AMKR (Amkor Technology) — see [[#HANDOFF_ID = 20260903-CENSUS-AMKR-NEW_CHALLENGER]]
- MP (MP Materials) — see [[#HANDOFF_ID = 20260903-CENSUS-MP-NEW_CHALLENGER]]

## Seeds
None.

## Trigger Watches
- SNDK (SanDisk) — see [[#HANDOFF_ID = 20260903-CENSUS-SNDK-WATCH_GATE]]

## Event Gates
- WULF/IREN Anthropic-credit evidence gate (updated, still open) — see [[#HANDOFF_ID = 20260902-DAILY-WULF_IREN-EVIDENCE_GATE]]
- TSLA Optimus production-verification gate (new, paired Burden-of-Proof watch with WULF) — see [[#HANDOFF_ID = 20260903-DEEPAUDIT-TSLA-EVIDENCE_GATE]]

## Tribunals
- Portfolio-count / concentration overage (updated — sizing overage confirmed, exit-priority ranking explicitly withdrawn pending next cycle) — see [[#HANDOFF_ID = 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE]]

## Source Status
Per [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-03_DEEPAUDIT]]: Master Ledger READY (self-consistent, no drift from broker state), Active Handoff Snapshot READY, market-status WebSearch READY (day-level), equity-quote WebSearch DEGRADED (no dedicated financial-data API; IREN/WULF prices internally conflicting ~9-10% within the same search, unresolved for a second cycle), dedicated financial-data API UNAVAILABLE. `DATA QUALITY = DEGRADED` as of 2026-09-03 (reconfirmed, not improved, from 2026-09-02).

## Acknowledgements
None yet — these are new/updated handoffs from today's Deep Audit run, not yet consumed by a downstream product.

## Last Writer
Orchestrator, DCA Execution Card run 2026-09-03 — see [[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_2026-09-03_DCA]] (first real DCA card; resolved HOLD CASH — no confirmed contribution, count-overage sequencing unresolved; closed MP's $400M/$550M+ DoD evidence gate; corrected AMKR's Arizona-timeline framing from "H2 2026" to 2027-2028; NO LOG REQUIRED)

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
SOURCE = Daily Anchor Portfolio Court + Risk and Survivability, 2026-09-02 run; UPDATED by Deep Audit 2026-09-03
SOURCE_SIGNAL_DATE = 2026-09-03 (updated)
DEDUP_KEY = DAILY|PORTFOLIO|COUNT_OVERAGE|2026-09-02
PREVIOUS_STATE = Flagged 2026-09-02, routed to this Deep Audit as NEXT_GATE
NEW_STATE = ADJUDICATED IN PART by Deep Audit 2026-09-03. Count breach (8 vs draft 7) and sizing breach (PLTR ~35.6%, NVDA ~29.8% vs ~5% draft norm) CONFIRMED by 3 independent agents (Underwriter, Portfolio Court, Risk), undisputed by Red Team — RESIZE is the standing recommendation for both, exact target deferred to Mark. Portfolio Court's original WULF-first exit-priority ranking (to fix the count breach specifically) is WITHDRAWN — Red Team returned INCUMBENCY BIAS CHECK = FAIL, finding the ranking apparatus favored already-small/already-familiar incumbents (WULF ranked partly on "cheapest to unwind," a circular argument; GOOGL/MSFT cleared for new capital using a lighter test than KO/WULF faced; TSLA's structurally identical Burden-of-Proof failure got no equivalent scrutiny). No exit-priority order is currently in force. KO flagged REPLACE-WATCH (mandate-fit strain, confirmed independently by 3 agents) pending a genuine swap-comparison against AMKR/MP next cycle — not run this cycle.
EVIDENCE_QUALITY = HIGH for the count/sizing arithmetic; MEDIUM for underlying prices (DEGRADED, reconfirmed 2026-09-03)
THESIS_OR_ASYMMETRY_CHANGE = Not a single-security thesis change — a structural/rule-conformance finding
SURVIVABILITY_OR_FINANCING_CHANGE = Not applicable
NEXT_GATE = Next Deep Audit cycle: a genuine joint-reconstruction test (GOOGL/MSFT explicitly tested as displacement candidates against KO/WULF, not just against idle cash), AMKR/MP underwritten to Monster File depth before being ranked against incumbents. Also requires Mark to confirm, amend, or reject the §11 draft rules themselves.
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Deep Audit cycle
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
SOURCE = Daily Anchor Underwriter + Risk and Survivability + Red Team, 2026-09-02 run; UPDATED by Deep Audit Industry Read-through 2026-09-03; NARROWED by Event Gate Watch 2026-09-03 (first-ever direct primary-source read)
SOURCE_SIGNAL_DATE = 2026-09-03 (narrowed)
DEDUP_KEY = DAILY|WULF_IREN|EVIDENCE_GATE|2026-09-02
PREVIOUS_STATE = Flagged 2026-09-02; Deep Audit made progress but both primary documents remained EGRESS_BLOCKED as of this morning
NEW_STATE = NARROWED, not fully closed. Event Gate Watch retrieved both blocked primary documents directly (via curl workaround, WebFetch itself still EGRESS_BLOCKED) — first time either has actually been read. TeraWulf's own SEC 8-K (filed 2026-07-06, Item 8.01) states verbatim: "Anthropic's payment obligations under the Justified Data Campus Lease are expected to be supported by an investment-grade credit." This answers the original "whose credit" question directly — Anthropic's OWN credit is cited, not a third-party guarantor like the separate Broadcom-guaranteed TPU-SPV structure. But neither document names a rating agency, an actual rating, or a guarantee instrument — "investment-grade credit" is TeraWulf's own unsourced characterization within its own filing, not independent verification. IREN's findings from this morning (convertible notes confirmed, Microsoft-GB300 terms still unconfirmed) are unchanged.
EVIDENCE_QUALITY = MEDIUM-HIGH on "whose credit is cited" (now VERIFIED FACT, direct primary-source quote); still MEDIUM on whether that credit is independently rated/verified (no rating agency named anywhere in either document)
THESIS_OR_ASYMMETRY_CHANGE = Unchanged in substance — this narrows the open question, does not resolve WULF's underwriting rating (still LOW adjusted attractiveness per this morning's Deep Audit)
SURVIVABILITY_OR_FINANCING_CHANGE = WULF: ~$5.8B total debt (~63% naive debt+equity cap), refinancing/conversion risk on $2.5B convertible notes ahead of H2 2027 revenue start. IREN: $11B-$16B FY2027 financing gap, still a management aspiration, not secured.
NEXT_GATE = Confirm whether any rating agency (S&P, Moody's) has actually rated Anthropic or this specific lease obligation — TeraWulf's own filing does not cite one. Also close IREN's Q1 FY2027 financing-gap checkpoint.
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next cycle that finds an actual rating-agency citation or confirms none exists
REQUIRED_CONSUMERS = DAILY, WEEKLY, CENSUS
MANDATORY_DEEP_UNDERWRITING = YES
```

## HANDOFF_ID = 20260903-DEEPAUDIT-TSLA-EVIDENCE_GATE
```
HANDOFF_ID = 20260903-DEEPAUDIT-TSLA-EVIDENCE_GATE
ORIGIN_MODULE = DEEPAUDIT
ORIGIN_DATE = 2026-09-03
SECURITY/TICKER = TSLA
HANDOFF_TYPE = EVIDENCE_GATE
SOURCE = Deep Audit Underwriter + Risk and Survivability + Red Team, 2026-09-03 run; UPDATED by Event Gate Watch 2026-09-03
SOURCE_SIGNAL_DATE = 2026-09-03 (updated)
DEDUP_KEY = DEEPAUDIT|TSLA|EVIDENCE_GATE|2026-09-03
PREVIOUS_STATE = Flagged this morning — Optimus production-start claim unverified, raw convexity rated UNKNOWN
NEW_STATE = OPTIMUS LEG RESOLVED (partial, downgraded from original claim): Tesla's own Q2 2026 shareholder letter (2026-07-22) walked back the specific late-July/August window; multiply-corroborated secondary reporting confirms production did begin at Fremont by late August 2026 — ~3-4 weeks late. Initial builds go to an internal "Optimus Academy" training program, not customer/paid deployment — pilot-stage, not volume production; Musk has publicly said output will be "quite slow," rate "impossible to predict." Satisfies "did it happen" (yes, late); does NOT yet support convexity-at-scale. CYBERCAB LEG STILL PENDING: today's Austin launch event occurred under NDA/embargo, no official outcome released as of this check; real operational signal exists (Cybercabs live on Austin streets, app update shipped, 45/420 TX-registered driverless Tesla vehicles authorized as Cybercabs) but predates rather than confirms a successful public outcome.
EVIDENCE_QUALITY = MEDIUM-HIGH on Optimus production having started (multiply-corroborated secondary reporting plus Tesla's own shareholder letter); DATA LIMITED on Cybercab's actual outcome (embargoed)
THESIS_OR_ASYMMETRY_CHANGE = Optimus question converts from "did production begin" (now answered: yes, late, low-volume) to "at what rate/scale does this become revenue-relevant" — new, more precise open question. Verified EV-delivery-recovery thesis continues to support current in-line (~5.5%) weight on its own.
SURVIVABILITY_OR_FINANCING_CHANGE = Unchanged from this morning
NEXT_GATE = Tesla's Q3 2026 earnings (~early October 2026) for the first disclosed Optimus production-rate/unit-count figure; Cybercab embargo expected to lift within 24-48 hours — re-check next cycle
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next cycle that finds a disclosed Optimus production-rate figure and/or the Cybercab event's actual outcome
REQUIRED_CONSUMERS = DAILY, WEEKLY, CENSUS
MANDATORY_DEEP_UNDERWRITING = NO
```

## HANDOFF_ID = 20260903-CENSUS-AMKR-NEW_CHALLENGER
```
HANDOFF_ID = 20260903-CENSUS-AMKR-NEW_CHALLENGER
ORIGIN_MODULE = CENSUS
ORIGIN_DATE = 2026-09-03
SECURITY/TICKER = AMKR
HANDOFF_TYPE = CANDIDATE_STATE
SOURCE = Monster Census Deep Underwriting (Orchestrator, 2026-09-03); TIMELINE CORRECTED by DCA Execution Card Underwriter, 2026-09-03
SOURCE_SIGNAL_DATE = 2026-09-03 (correction)
DEDUP_KEY = CENSUS|AMKR|NEW_CHALLENGER|2026-09-03
PREVIOUS_STATE = Not tracked
NEW_STATE = CHALLENGER, now with a full-depth Monster File (DCA Underwriter, 2026-09-03) — target role Core/Attacker, adjusted attractiveness MODERATE. Best-fit replacement target identified as WULF specifically.
EVIDENCE_QUALITY = HIGH (Q2 2026 press release + 10-Q figures, multiply corroborated: net income $174M, near-zero net debt, +26% YoY revenue)
THESIS_OR_ASYMMETRY_CHANGE = Direct CoWoS/advanced-packaging bottleneck beneficiary, largest US-headquartered OSAT. **CORRECTION**: prior framing of "Arizona onshoring hedge ramping H2 2026" is not supported by primary sourcing — Amkor's own site materials show construction began Sept 2025, facility completion mid-2027, production start early 2028. The bottleneck thesis is intact; the near-term-ramp framing was wrong and is corrected here.
SURVIVABILITY_OR_FINANCING_CHANGE = None — profitable incumbent, no dilution signal, near-zero net debt. H1 2026 FCF was negative ($(269.9)M) but fully explained by active Arizona capex, not operating weakness.
NEXT_GATE = Q3 2026 report, October 26, 2026 after market close — confirming AI advanced-packaging revenue trajectory and whether the corrected 2027-2028 Arizona timeline stays on track
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Underwriter cycle sizing decision
REQUIRED_CONSUMERS = WEEKLY, DAILY
MANDATORY_DEEP_UNDERWRITING = NO
```

## HANDOFF_ID = 20260903-CENSUS-MP-NEW_CHALLENGER
```
HANDOFF_ID = 20260903-CENSUS-MP-NEW_CHALLENGER
ORIGIN_MODULE = CENSUS
ORIGIN_DATE = 2026-09-03
SECURITY/TICKER = MP
HANDOFF_TYPE = CANDIDATE_STATE
SOURCE = Monster Census Deep Underwriting (Orchestrator, 2026-09-03); GATE CLOSED by DCA Execution Card Underwriter, 2026-09-03
SOURCE_SIGNAL_DATE = 2026-09-03 (gate closure)
DEDUP_KEY = CENSUS|MP|NEW_CHALLENGER|2026-09-03
PREVIOUS_STATE = Not tracked
NEW_STATE = CHALLENGER, now with a full-depth Monster File (DCA Underwriter, 2026-09-03) — target role Seed/Catalyst with an explicit evidence gate (not Core/Attacker), adjusted attractiveness MODERATE (below AMKR on profitability, above WULF on counterparty clarity)
EVIDENCE_QUALITY = HIGH on the DoD deal mechanics (multiply corroborated primary-adjacent sources); MEDIUM on current financials; DATA LIMITED on the 10X Facility production date (not disclosed anywhere found)
THESIS_OR_ASYMMETRY_CHANGE = Rare-earth producer converted to a DoD-backed national-champion play via government equity stake and a $110/kg NdPr price floor with a 10-year 100%-offtake commitment — a genuinely differentiated survivability mechanism nothing else in the portfolio has
SURVIVABILITY_OR_FINANCING_CHANGE = **$400M vs $550M+ DoD-figure discrepancy CLOSED**: both figures were correct and additive, not contradictory — $400M convertible-preferred equity + $150M separate 12-year DoD loan = $550M total direct DoD support. A separate $1.0B JPMorgan/Goldman commitment is private bank debt, not DoD money, and should not be summed into the DoD figure. Company is currently unprofitable (Q2 2026 net loss $(20.3)M), ~8.71% YoY share dilution, mid-ramp on two simultaneous facility builds.
NEXT_GATE = Q3 2026 earnings (~October 29, 2026, date UNVERIFIED LEAD) — test whether a 10X Facility production date is finally disclosed and whether the Independence Facility's "sold out" claim converts to dollar-denominated contracted revenue
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Underwriter cycle
REQUIRED_CONSUMERS = WEEKLY, DAILY
MANDATORY_DEEP_UNDERWRITING = NO
```

## HANDOFF_ID = 20260903-CENSUS-SNDK-WATCH_GATE
```
HANDOFF_ID = 20260903-CENSUS-SNDK-WATCH_GATE
ORIGIN_MODULE = CENSUS
ORIGIN_DATE = 2026-09-03
SECURITY/TICKER = SNDK
HANDOFF_TYPE = EVIDENCE_GATE
SOURCE = Monster Census Deep Underwriting (Orchestrator, 2026-09-03)
SOURCE_SIGNAL_DATE = 2026-09-03
DEDUP_KEY = CENSUS|SNDK|WATCH_GATE|2026-09-03
PREVIOUS_STATE = Not tracked
NEW_STATE = WATCH WITH SPECIFIC TRIGGER
EVIDENCE_QUALITY = MEDIUM (datacenter revenue growth VERIFIED FACT/IR-sourced; price-performance claims UNVERIFIED and extreme — ~1,350% trailing 12mo, unconfirmed)
THESIS_OR_ASYMMETRY_CHANGE = First NAND-specific pure-play surfaced in any CAOS run; real growth story but entry-price asymmetry unassessable given unreliable equity-quote data this cycle
SURVIVABILITY_OR_FINANCING_CHANGE = None identified
NEXT_GATE = Independent (non-WebSearch-aggregator) price/valuation confirmation
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = Next Verifier cycle with a reliable price source, or Mark's own broker-side check
REQUIRED_CONSUMERS = WEEKLY, DAILY
MANDATORY_DEEP_UNDERWRITING = NO
```
