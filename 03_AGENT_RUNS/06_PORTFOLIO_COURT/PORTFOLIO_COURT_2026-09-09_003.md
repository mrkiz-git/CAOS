# PORTFOLIO COURT RUN — 2026-09-09_003

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-09_001]] — scope: CEG, ISRG, CIFR, ONDS only (no AVGO/KTOS/RCAT underwriting in current run)
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — portfolio state: 6 funded holdings, €5,465.84 cash, 7-cap draft rule
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] — ONDS is HIGH-PRIORITY CHALLENGER; WULF/IREN evidence gate active; portfolio-count overage RESOLVED by 2026-09-09 rebalance
- [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_2026-09-09_001]] — KTOS, RCAT, AVGO, PDYN, AVAV, VRT listed as "already tracked, excluded from discovery" per prior handoff

## Scope and Evidence Quality Note
**CRITICAL:** The Underwriter deliberately scoped 2026-09-09_001 to only CEG, ISRG, CIFR, and ONDS. The original task request to rank AVGO, KTOS, RCAT cannot be fulfilled because those candidates were not underwritten in this run — Discovery notes them as "already tracked" from a prior run, but no current Underwriter comparative evidence exists for them. Portfolio Court can rank only candidates the Underwriter provided. This is a **DEGRADED** state relative to the task request.

---

## Part 1: 100%-Cash Holdings Trial

**HOLDINGS UNKNOWN / EXECUTION BLOCKED**

All six current holdings (NVDA, MSFT, GOOGL, TSLA, IREN, WULF) are marked tentatively as CORE/ATTACKER pending formal role assignment in a forthcoming Deep Audit per Operator Manual §3–§4 and Master Ledger §4. Their holding-vs-cash comparative advantage cannot be asserted without:
1. Formal thesis statements for each position (not yet written in this run)
2. Expected CAGR projections from today (not yet provided)
3. Explicit kill conditions and proof gates for each (not documented in this run)
4. Comparative survivability-adjusted attractiveness scores (not provided)

**Finding:** The 100%-cash trial cannot complete until the Deep Audit formally assigns roles and theses to the six inherited holdings. Candidate research may proceed independently.

**Consequence:** Portfolio Court can rank candidates against each other and against the "hold cash" option, but cannot perform the full 100%-cash reconstitution test as specified.

---

## Part 2: Next Uncommitted Euro — Ranking

**Candidate scope in current Underwriter output:**

| Rank | Ticker | Status | Survivability-Adjusted Attractiveness | Time to 3x | Holding? |
|------|--------|--------|------|---|---|
| 1 | ISRG | CHALLENGER | MODERATE-TO-GOOD | 8–12 years | No |
| 2 | ONDS | HIGH-PRIORITY CHALLENGER | MODERATE | 3–6 years | No |
| 3 | CEG | WATCH W/ SPECIFIC TRIGGER | MODERATE | 7–12 years | No |
| 4 | CIFR | WATCH W/ SPECIFIC TRIGGER | MODERATE-LOW | 4–7 years | No |
| 5 | CASH HOLD | N/A | N/A | Immediate liquidity | Yes |

### Ranking Logic

**Tier 1 (Ranking 1): ISRG (CHALLENGER)**
- **VERIFIED FACT:** $126.3bn equity value, 40.6x trailing P/E, Q2 revenue +19%, da Vinci procedure volume +15%, Ion procedures +36%, installed base +12% to 11,710 units.
- **Survivability:** **VERY GOOD.** Cash/investments €8.63bn, balance sheet strong, recurring instruments/service revenue proven.
- **Attractiveness cap:** Valuation demands sustained performance. Business quality is the highest in this set; 3x is **possible over a long period, low near-term credibility** per Underwriter.
- **Why rank first:** Highest business-quality asymmetry offset by highest valuation. Non-GAAP gross margin 68%-69% with repeating revenue model makes this a compounding machine, not a speculation play.
- **Proof gate:** FY2026 da Vinci procedure growth ≥13.5%, gross margin ≥68%. Kill gate at <10% growth for two consecutive quarters.
- **Portfolio role:** CHALLENGER (not buy-authorized; downstream Red Team must confirm survivability + Red Team verdict must clear).

**Tier 1 (Ranking 2): ONDS (HIGH-PRIORITY CHALLENGER)**
- **VERIFIED FACT:** $3.81bn equity value, Q2 revenue $83.8m (+67% QoQ), common shares 529.8m (up 39% in H1 2026 from dilution/raise).
- **Survivability:** **MIXED.** Liquidity good post-raise (~$666m cash/restricted, ~$727m short-term investments), but first-half burn $137.4m, acquisitions consuming capital, per-share dilution rapid.
- **Attractiveness:** Smallest denominator and **clearest raw 3x path** (credible but not proven per Underwriter), but integration risk and cash-conversion discipline unproven. Acquisition-heavy model and 39% six-month share growth are decisive risks to per-share value.
- **Why rank second:** Highest raw-convexity asymmetry in the challenger set, but dilution and burn are material headwinds. Underwriter notes this is "arguably cleaner evidence than WULF" (an already-funded holding), making it the closest direct call in this run.
- **Proof gate:** FY2026 guidance ($525M–$550M) reaffirmed/raised AND Army IDIQ awarded-task orders total >$400M (vs. ~$240M today). Also: share count rise discipline (<15% before positive operating cash flow).
- **Kill gates:** FY26 guidance cut, organic growth <30%, IDIQ firm awards stall, burn >$100m per half-year, share dilution >15% before positive cash flow, adjusted liquidity <12 months of obligations.

**Tier 2 (Ranking 3): CEG (WATCH WITH SPECIFIC TRIGGER)**
- **VERIFIED FACT:** $104.5bn equity value, 25.9x trailing P/E, Q2 adjusted operating EPS $2.55, guidance raised to $11.50–$12.50 for 2026, debt $19.6bn (+$12.2bn for Calpine), cash $0.7bn.
- **Survivability:** **GOOD.** Earnings, operating cash flow (H1 $1.55bn), investment-grade ratings, credit access all real. Calpine dilution and leverage are the material caveats.
- **Attractiveness:** **Scarce firm-power exposure with lower tech risk than AI hosters.** But large denominator ($104.5bn), acquisition leverage, and limited pure AI attribution (DATA LIMITED) cap upside. 3x would require EPS near $35–$44 at reasonable valuation multiples — not credible on current evidence.
- **Why rank third:** Highest strategic scarcity (firm power to AI workloads) but lowest asymmetry due to denominator and leverage post-Calpine. Business is solid, opportunity is structural, but expected CAGR from today is moderate vs. denominator.
- **Proof gate:** Maintain 2026 EPS guide, prove Calpine per-share accretion, add clean-power contracts without credit deterioration.
- **Kill gates:** 2026 EPS falls below $11.50, Calpine fails to lift per-share earnings while debt persists, investment-grade ratings lost, Crane restart suffers major regulatory/cost/schedule failure, clean-power contract additions stall while AI demand thesis remains.

**Tier 2 (Ranking 4): CIFR (WATCH WITH SPECIFIC TRIGGER RETAINED)**
- **VERIFIED FACT:** $7.36bn equity value, Q2 revenue $24.8m (100% mining, zero HPC revenue), contracted future rent $5.5bn (AWS Black Pearl 15-year lease + Fluidstack), shares outstanding 414.3m (up 2.3% in H1, well-controlled), cash $831.8m but $3.73bn restricted, debt principal $6.02bn.
- **Survivability:** **MIXED.** Restricted cash and project debt cannot count as free corporate liquidity. Operating cash flow is negative ($152m first-half burn). Revenue remains 100% mining. Trigger gate not yet met.
- **Attractiveness:** **PRE-REVENUE IN HPC.** Raw upside is meaningful (3x credible but not proven), and AWS/Google-supported contracts improve evidence quality vs. speculative HPC plays. But CIFR directly overlaps funded IREN/WULF concentration without yet proving superior operating HPC unit economics. No HPC revenue by Q4 2026 = automatic REJECT per Discovery gate.
- **Why rank fourth:** Similar lane to IREN/WULF (already funded), higher execution risk (pre-revenue in new thesis), unproven unit economics. Would add lane concentration without new revenue proof.
- **Proof gate:** Reported non-mining HPC revenue >10% by Q4 2026 (MANDATORY, else auto-REJECT). On-time Black Pearl/Fluidstack rent commencement.
- **Kill gates:** No HPC revenue by Q4 2026 (auto-REJECT), rent commencement slips, project cost overruns force major common-equity issuance, contracted tenants weaken/renegotiate, Bitcoin economics fail before HPC rent covers burn, share count rises >15% before positive recurring HPC revenue.

**Tier 3 (Ranking 5): CASH HOLD**
- **Principle:** Cash Is Valid (Operator Manual §9). Do nothing when no candidate clears the minimum edge.
- **Current state:** €5,465.84 real unlevered cash (58.1% of NAV), no margin, no leverage, full availability.
- **Expected return:** Zero real return in EUR, subject to EUR carry; opportunity cost depends on candidate ranking above.
- **When cash ranks first:** None of the four candidates above clears the minimum edge for immediate funding AND the next monthly contribution (€300) is sufficient to observe the next proof gates (Q3/Q4 2026 earnings for ONDS, CIFR; Q4 guidance for CEG; Q2+ procedure data for ISRG).

---

## Part 3: Capital-Recycling Tribunal

**Current holdings unable to be tested.**

The six funded holdings (NVDA, MSFT, GOOGL, TSLA, IREN, WULF) do not yet have formal theses, expected-CAGR projections, or proof gates assigned. A capital-recycling tribunal requires comparing the survivability-adjusted opportunity cost of holding Position X (at its current size and thesis credibility) versus deploying the same capital to Candidate Y. Without formal thesis statements for current holdings, this comparison cannot be completed.

**Findings:**

1. **Lane concentration check:** Current holdings already include IREN and WULF (Bitcoin mining / AI infrastructure power). CIFR (pre-revenue HPC with AWS contracts) occupies the same lane. Funding CIFR would increase lane concentration without first proving superior operating unit economics vs. IREN/WULF.

2. **No immediate sell signals from candidates:** None of the four candidates (ISRG, ONDS, CEG, CIFR) has a survivability/thesis profile that would require liquidating a current holding to fund. Specifically:
   - ISRG (surgical robotics, high business quality) does not compete with any current holding.
   - ONDS (defense autonomy, IDIQ awards) does not overlap with current lane.
   - CEG (nuclear power generation) does not compete with holdings.
   - CIFR (pre-revenue HPC) overlaps IREN/WULF lane concentration; would require a lane-consolidation decision, not forced by candidate superiority.

3. **Cash sufficiency:** €5,465.84 cash (58.1% of NAV) is sufficient to fund at least one new position (SEED/CHALLENGER role, typically 1%-3% allocation) without selling any current holding. Specifically:
   - Adding 1 holding to 6 current = 7 total (at cap, not over, per draft 7-cap rule).
   - Monthly €300 contribution supports a phased deployment without forced sales.

**Conclusion:**

**NO CAPITAL RECYCLING REQUIRED.** The portfolio has sufficient free cash to fund the next uncommitted euro in the top-ranked candidate (ISRG) without selling any current holding. A capital-recycling tribunal would be warranted only if:
- All cash + next quarterly contribution were insufficient to fund the candidate, OR
- A candidate's edge was so compelling that lane concentration or sizing changes justified a swap.

Neither condition is met in this run.

---

## Part 4: Portfolio-Count Check

**Status: COMPLIANT**

- **Current holdings:** 6 funded securities (NVDA, MSFT, GOOGL, TSLA, IREN, WULF)
- **Draft cap:** 7 funded public securities (per Master Ledger §11, DRAFT pending Mark's confirmation)
- **Available slots:** 1
- **Candidates ready for funding consideration:** ISRG (CHALLENGER) and ONDS (HIGH-PRIORITY CHALLENGER) are both ready for downstream Red Team/Orchestrator review
- **Consequence of 1 new position:** 6 + 1 = 7 (at cap, not over)

**Finding:** The portfolio-count constraint is not a blocker to funding the next-ranked candidate. The 2026-09-09 rebalance resolved the prior 8-holding overage by exiting PLTR and KO, creating room for new deployment.

**Caveat:** The draft 7-cap rule itself remains DRAFT per Master Ledger §11 and requires Mark's confirmation before it becomes binding. If Mark amends the cap upward or downward, this check must be re-run.

---

## Part 5: No-Orphan Check

**Status: PASSED**

Every candidate ranked in Part 2 has an explicit thesis, proof gate, and kill conditions per the Underwriter's Monster Files:

| Candidate | Thesis | Proof Gate | Kill Gates | Orphan? |
|-----------|--------|-----------|-----------|---------|
| ISRG | Recurring surgical-instruments revenue + long da Vinci procedure growth runway | FY2026 guidance (13.5%-15.5% procedure growth, 68%-69% gross margin) | Procedure growth <10% for 2 quarters; gross margin <68%; major safety/recall | NO |
| ONDS | Defense autonomy IDIQ awards + organic revenue growth + acquisition integration | FY26 guidance reaffirm + Army IDIQ >$400M awarded (vs. ~$240M today) | Guidance cut; organic growth <30%; IDIQ stalls; burn >$100m/half-year | NO |
| CEG | Scarce firm power to AI workloads + Calpine integration accretion | 2026 EPS guidance maintained + per-share accretion proof + clean-power contracts | EPS <$11.50; Calpine integration fails; ratings downgrade; Crane restart delays | NO |
| CIFR | AWS/Fluidstack contracted HPC rent + AI-hosting revenue emergence | HPC revenue >10% by Q4 2026 (MANDATORY) + on-time rent commencement | No HPC revenue by Q4 2026 (auto-REJECT); rent delays; dilution >15% before HPC revenue | NO |
| CASH | Safe harbor during candidate observation | €300 monthly contribution funds next gate; no forced hold | None (cash has no kill gates, only opportunity cost) | NO |

**Current holdings:** NVDA, MSFT, GOOGL, TSLA, IREN, WULF remain without formal theses per Master Ledger §4, pending Deep Audit assignment. This is a KNOWN LIMITATION of the current run, not a portfolio-orphan problem — they are inherited holdings under provisional CORE/ATTACKER status, not newly proposed positions.

**Conclusion:** No new position can be added without an explicit thesis and proof gate. All four candidates in scope satisfy this requirement. Current holdings will be formally reviewed in the Deep Audit.

---

## Summary: Candidacy Status After Portfolio Court

| Candidate | Status Before | Status After | Rationale |
|-----------|---|---|---|
| ISRG | CHALLENGER (Underwriter) | **RANK 1 — READY FOR DOWNSTREAM COURT** | Highest business-quality asymmetry; ready for Red Team survivability check |
| ONDS | HIGH-PRIORITY CHALLENGER (Handoff) | **RANK 2 — READY FOR DOWNSTREAM COURT** | Clearest raw 3x path; dilution discipline is key open gate; ready for Red Team verification |
| CEG | WATCH W/ SPECIFIC TRIGGER | **RANK 3 — READY FOR DOWNSTREAM COURT** | Structural power scarcity justifies monitoring; too large denominator for immediate top-3 ranking; proof gates well-defined |
| CIFR | WATCH W/ SPECIFIC TRIGGER | **RANK 4 — HOLD IN WATCH** | Pre-revenue in HPC; mandatory Q4 2026 gate is binary (HPC revenue >10% or auto-REJECT); does not rank above CEG until gate is met |
| RCAT, AVGO, KTOS | Not in scope (Underwriter deliberate exclusion) | **CANNOT RANK — DATA UNAVAILABLE** | These candidates were not underwritten in 2026-09-09_001; Discovery lists them as "already tracked, excluded"; no current comparative evidence |

---

## Handoff Acknowledgement Checks

`HANDOFF ACK CHECK: 20260902-DAILY-ONDS-NEW_CHALLENGER | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=ONDS confirmed HIGH-PRIORITY CHALLENGER, ranked #2 in next-uncommitted-euro tribunal | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

`HANDOFF ACK CHECK: 20260902-DAILY-PORTFOLIO-COUNT_OVERAGE | RECEIVED=YES | APPLIED=YES | RESULTING_STATE=Portfolio rebalance 2026-09-09 resolved count overage; 6 holdings + 1 slot available under 7-cap = compliant | STILL_ACTIVE=NO | RESOLVES_HANDOFF_ID=20260902-DAILY-PORTFOLIO-COUNT_OVERAGE (RESOLVED by user action 2026-09-09)`

`HANDOFF ACK CHECK: 20260902-DAILY-WULF_IREN-EVIDENCE_GATE | RECEIVED=YES | APPLIED=NO | RESULTING_STATE=UNCHANGED; Anthropic-credit and IREN-financing gaps remain open; no current Underwriter reassessment in this run | STILL_ACTIVE=YES | RESOLVES_HANDOFF_ID=NONE`

---

## Integrity and Limits

- **No transaction, fill, or sizing instruction:** Portfolio Court output is a ranking and tribunal verdict only. Mark retains all execution authority. No buy/sell order is proposed or assumed.
- **Holding thesis gap:** Current six funded holdings do not yet have formal CAOS theses per Master Ledger §4. The 100%-cash trial cannot complete until Deep Audit assigns formal roles and theses.
- **Underwriter scope limitation:** Candidates AVGO, KTOS, RCAT were intentionally excluded from the Underwriter's 2026-09-09_001 scope. Portfolio Court cannot rank them without Underwriter evidence.
- **Evidence quality:** Underwriter evidence quality is HIGH for financials, MEDIUM-to-HIGH for candidate comparisons, DATA LIMITED for HPC unit economics (CIFR) and AI-specific revenue attribution (CEG, IREN, WULF). Red Team's independent survivability verification is mandatory before funding.
- **Process over outcome:** This ranking reflects current evidence as of 2026-09-09. Outcome depends on execution, market conditions, and ongoing proof-gate results.

---

## Next Proof Gates (Portfolio Court to Downstream Consumers)

1. **Red Team Survivability Check (Agent 8):** Confirm ISRG and ONDS are worthy of portfolio concentration despite not being in the current portfolio yet. Verify financing risk and competitive durability.

2. **Orchestrator Consolidated Verdict (Agent 9):** Integrate Portfolio Court ranking with Red Team verdict and Risk/Survivability findings. Confirm portfolio-count and No-Orphan compliance. Propose final ranking to Mark for execution decision.

3. **Current Holdings Deep Audit (Future):** Formal thesis and role assignment for NVDA, MSFT, GOOGL, TSLA, IREN, WULF is a prerequisite for future capital-recycling tribunals and the full 100%-cash trial.

4. **Candidate Gate Timeline:**
   - **ISRG:** FY2026 Q2+ guidance confirmation (procedure growth ≥13.5%, gross margin ≥68%)
   - **ONDS:** Q3/Q4 2026 earnings + FY26 guidance reaffirm
   - **CEG:** 2026 EPS guidance maintenance + Calpine per-share accretion proof
   - **CIFR:** Q3 2026 earnings (HPC revenue >10% or Q4 gate fails, auto-REJECT)

---

PORTFOLIO COURT = RANKING COMPLETE
