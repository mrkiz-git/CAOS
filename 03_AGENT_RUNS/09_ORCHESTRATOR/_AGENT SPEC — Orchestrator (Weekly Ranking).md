# CAOS — Orchestrator (Weekly Ranking)

**Mission:** Consolidate all 8 agent outputs into unified ranking universe. Produce two ranking tables (raw-asymmetry and evidence/survivability-adjusted), run head-to-head fights (brief format in main output, detailed in supporting document), audit system health, acknowledge active handoffs, confirm execution readiness gates, and propose Master Ledger events. This runs in the primary Claude Code session, not as a subagent.

---

## Required Inputs

1. `03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_HHmm_WEEKLY.md` — current prices, denominator
2. `03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_YYYY-MM-DD_HHmm_WEEKLY.md` — new candidates
3. `03_AGENT_RUNS/03_FORWARD/FORWARD_YYYY-MM-DD_HHmm_WEEKLY.md` — earnings, guidance, analyst changes
4. `03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_YYYY-MM-DD_HHmm_WEEKLY.md` — sector conditions
5. `03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_YYYY-MM-DD_HHmm_WEEKLY.md` — all-candidate thesis status
6. `03_AGENT_RUNS/06_PORTFOLIO_COURT/PORTFOLIO_COURT_YYYY-MM-DD_HHmm_WEEKLY.md` — funded holdings re-validation
7. `03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_YYYY-MM-DD_HHmm_WEEKLY.md` — survival scores (all candidates)
8. `03_AGENT_RUNS/08_RED_TEAM/RED_TEAM_YYYY-MM-DD_HHmm_WEEKLY.md` [optional] — stress test
9. `01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL.md` — holdings list, conviction history
10. `02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT.md` — current candidate states, active handoffs

---

## Output Contract

**Main file:** `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md`

**Supporting detail file:** `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md`

Both files named with format `YYYY-MM-DD` date and `HHmm` time of Orchestrator run start.

---

## Main Output Structure

### Section 1: Inputs Consulted

Wikilink to all 8 agent files, Master Ledger, Active Handoff Snapshot, and Design Spec.

```markdown
## Inputs Consulted
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/03_FORWARD/FORWARD_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/06_PORTFOLIO_COURT/PORTFOLIO_COURT_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_YYYY-MM-DD_HHmm_WEEKLY]]
- [[03_AGENT_RUNS/08_RED_TEAM/RED_TEAM_YYYY-MM-DD_HHmm_WEEKLY]] [optional]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[06_PRODUCT_RUNBOOKS/Weekly Ranking Design]]
```

### Section 2: Consolidated Universe Summary

One-line summary of how many candidates consolidated:
- Holdings: [N] (from Master Ledger)
- Buy-authorized Seeds: [N]
- Funded Seeds: [N]
- Challengers: [N]
- Serious Candidates: [N]
- New candidates (from Discovery): [N]
- Total universe: [N] candidates + cash

### Section 3: Table 1 — Raw-Asymmetry Ranking

**Sort by:** upside/downside ratio (asymmetry ratio) descending

**Columns:**
| Rank | Ticker | Company | Upside | Downside | Asymmetry % | Current Conviction | Status |
|------|--------|---------|--------|----------|-------------|-------------------|--------|

**Rules:**
- All candidates in universe (holdings, Seeds, Challengers, serious candidates, new discoveries, cash)
- Upside and Downside pulled from Underwriter output (expected CAGR upside/downside if thesis holds)
- Asymmetry % = Upside / |Downside| (pure ratio, no evidence or survival adjustment)
- Current Conviction from Master Ledger or Underwriter output (SEED, CHALLENGER, WATCH, CORE, etc.)
- Status: HOLD | REVIEW | WATCH | NEW | CASH

Cash row: one line stating risk-free rate as denominator, no asymmetry.

### Section 4: Table 2 — Evidence/Survivability-Adjusted Ranking

**Sort by:** risk-adjusted conviction (asymmetry × evidence-quality-grade × survival-score) descending

**Columns:**
| Rank | Ticker | Company | Asymmetry % | Evidence Grade | Survival % | Adj. Score | Updated Conviction | Action |
|------|--------|---------|-------------|-----------------|-----------|-----------|-------------------|--------|

**Rules:**
- All candidates in same universe (same as Table 1)
- Asymmetry % from Table 1
- Evidence Grade: HIGH (all facts verified, <2h old) | MEDIUM (some sources secondary, <7d old) | LOW (speculative, >7d old) | DATA LIMITED (gaps)
- Survival % from Risk output
- Adj. Score = Asymmetry % × Evidence Weight × Survival% (where Evidence Weight: HIGH=1.0, MEDIUM=0.75, LOW=0.5, DATA LIMITED=0.33)
- Updated Conviction from Risk output (may downgrade if survival <threshold)
- Action: BUY | HOLD | REVIEW | ESCALATE | REJECT

Cash row: single line stating risk-free rate + liquidity advantage.

### Section 5: Head-to-Head Fights (Brief Format)

Five mandatory one-to-two-line comparisons:

```markdown
## Head-to-Head Fights

**vs. Portfolio Champion [highest-conviction funded holding]:**
[Top challenger by adjusted ranking] shows [asymmetry comparison vs. champion],
BUT [champion name] holds due to [reason: lower volatility | proven execution | lower dilution risk | better survival].

**vs. Quality Anchor [highest-ranked funded Seed]:**
[Top Seed in adjusted ranking] is [even/stronger/weaker] than [Quality Anchor name] —
asymmetry [X]% vs [Y]%, evidence [HIGH/MEDIUM/LOW], survival [Z]% vs [W]%.

**vs. Strongest Seed [top Seed by adjusted ranking]:**
[Candidate name] shows [asymmetry]% upside but [survival]% survival, vs. [strongest Seed] at [X]% upside / [Y]% survival.

**vs. Strongest Challenger [top Challenger by adjusted ranking]:**
[Top Challenger adjusted] edges [Top Challenger raw-asymmetry] on evidence and survival:
[asymmetry]% vs [X]%, evidence [grade comparison], survival [Y]% vs [Z]%.

**vs. Cash [risk-free rate + liquidity premium]:**
Minimum edge to deploy: [rate + X]%. Candidates clearing threshold: [count, example tickers].
Below threshold: [count, state HOLD or CASH].
```

### Section 6: System Audit

#### 6.1 Stale Gates Audit

For every WATCH WITH SPECIFIC TRIGGER and SERIOUS REVIEW candidate in Active Handoff Snapshot:

| Ticker | Current State | Gate Type | Trigger Event / Deadline | Status | Action |
|--------|---------------|-----------|-------------------------|--------|--------|

**Status:** OPEN (trigger/deadline pending) | EXPIRED (>90 days, no recent re-eval) | TRIGGERED (event occurred, awaiting decision)

**Action:** WAIT | ESCALATE | RESOLVE

#### 6.2 Orphan Positions Audit

Identify any position with <1.5% of NAV (from Master Ledger) that lacks an explicit Seed/Catalyst role:

| Ticker | % NAV | Current State | Assigned Role | Flag |
|--------|-------|---------------|----------------|------|

**Flag:** NONE | WARNING (position exists but role unclear)

#### 6.3 Contradictions Audit

Check for internal inconsistencies:
- CORE holding with survival score <40%
- Holdings listed as both REJECT and CHALLENGER
- Conflicting handoff states (two active handoffs for same ticker saying opposite things)

| Ticker | Contradiction Type | Details | Severity |
|--------|-------------------|---------|----------|

**Severity:** INFO | WARNING | CRITICAL

#### 6.4 Unresolved Handoffs Audit

Read Active Handoff Snapshot for every active handoff. Output one ACK check per handoff:

```
HANDOFF ACK CHECK: [HANDOFF_ID] | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO | RESOLVES_HANDOFF_ID
```

If expected handoff is missing: state `LINKAGE DEGRADED / HANDOFF UNAVAILABLE` — never hallucinate receipt.

Flag any handoff active >30 days without resolution or explicit extension:

| Handoff ID | Days Active | Status | Action |
|-----------|-------------|--------|--------|

### Section 7: Execution Readiness Gate

Confirm four preconditions. Output one of two verdicts:

**EXECUTION READY:** All four gates pass.  
**EXECUTION BLOCKED [reason]:** State which gate(s) failed and why.

**Gate 1: Portfolio Gate**
- Master Ledger current (not UNINITIALIZED, not >7 days stale)
- Holdings reconciled against broker export or recent screenshot
- Output: PASS or FAIL (reason: Ledger stale | Holdings unknown | Holdings unreconciled)

**Gate 2: Price Gate**
- All candidates in universe have current prices (from Verifier)
- Liquid holdings priced within 2 hours
- Others priced within 1 day
- Output: PASS or FAIL (reason: [N] tickers unpriced | prices >2h old for liquids | other)

**Gate 3: Ranking Gate**
- Top 3 candidates by adjusted ranking have stated convictions
- No "UNKNOWN" or "DATA LIMITED" in top 3
- Output: PASS or FAIL (reason: top [N] missing convictions | data too limited)

**Gate 4: Handoff Gate**
- All active handoffs in Snapshot touching universe candidates have `RECEIVED=YES`
- No `LINKAGE DEGRADED` states
- Output: PASS or FAIL (reason: [N] handoffs missing receipt | [N] linkage gaps)

**Verdict:**
```
EXECUTION READINESS GATE: [EXECUTION READY | EXECUTION BLOCKED]

Portfolio Gate: [PASS | FAIL — reason]
Price Gate: [PASS | FAIL — reason]
Ranking Gate: [PASS | FAIL — reason]
Handoff Gate: [PASS | FAIL — reason]

[If BLOCKED:] DCA Execution Card cannot proceed until [specific gate] is cleared.
```

### Section 8: Monthly Special Tasks (If First Run of Calendar Month)

Only run if calendar date is the first Weekly run of the month.

#### 8.1 Architecture Maintenance

Run these checks:

| Check | Finding | Status |
|-------|---------|--------|
| Portfolio baseline | Holdings count, NAV source, cash state vs. Ledger | [OK | MISMATCH] |
| Candidate registry | Are all SEED/CHALLENGER/WATCH candidates tracked? | [COMPLETE | GAPS] |
| Stale gates audit | Explicit monthly refresh of §6.1 findings | [CLEAN | FINDINGS] |
| Task health | Daily Anchor, Monster Census, Event Gate Watch, Weekly Ranking — all ran on time last month? | [HEALTHY | LATE | MISSED] |
| Notification health | Weekly Ranking delivery confirmation | [OK | FAILED] |
| Prompt contradictions | Any Operator Manual §3 Constitutional Laws drift or contradictions? | [NONE | DRIFT DETECTED] |
| Handoff linkage | Active Handoff Snapshot being read/written correctly by all products? | [OK | GAPS] |
| Duplicate/supersession logic | Any duplicate active handoffs for same ticker/signal? | [CLEAN | DUPLICATES] |
| Ledger-worthy changes | Any system rule amendments or major process changes? | [NONE | PENDING LOGGING] |

**Output:** One subsection per check, one line per finding.

#### 8.2 Deep Audit Reminder

Output one passive line:
```
Deep Audit reminder: Type `Run CAOS Deep Audit` to perform monthly full re-underwriting and ledger audit.
```

#### 8.3 Family-Wealth Architecture Check

Determine whether portfolio/family scale, legal/tax changes (marriage, inheritance, tax residency shift), or expected benefits (startup exit, bonus timing) justify dedicated professional review.

Output one of:
```
FAMILY WEALTH ARCHITECTURE: NO ACTION NEEDED — next check [date/event]
```
OR
```
FAMILY WEALTH ARCHITECTURE: RECOMMEND PROFESSIONAL REVIEW
Reason: [reason — portfolio scale | tax residency change | inheritance | startup exit imminent | other]
Next trigger: [date/event]
```

**Constraints:** Never autonomously recommend trusts, companies, tax structures, or legal action.

### Section 9: Handoff Emissions

For any conviction state changes detected (SEED → CHALLENGER, CHALLENGER → WATCH, WATCH → REJECT, etc.), or survivability shifts >10 percentage points, or major evidence quality shifts, emit handoff blocks:

```
HANDOFF_ID = YYYYMMDD-WEEKLY-TICKER-STATE_CHANGE
ORIGIN_MODULE = WEEKLY
ORIGIN_DATE = YYYY-MM-DD
SECURITY/TICKER = [ticker]
HANDOFF_TYPE = CANDIDATE_STATE
SOURCE = [Weekly Ranking Orchestrator]
SOURCE_SIGNAL_DATE = [date of Weekly run]
DEDUP_KEY = SOURCE|TICKER|SIGNAL_TYPE|DATE
PREVIOUS_STATE = [prior conviction from Ledger/Handoff Snapshot]
NEW_STATE = [updated conviction from Risk output]
EVIDENCE_QUALITY = HIGH | MEDIUM | LOW | DATA LIMITED
THESIS_OR_ASYMMETRY_CHANGE = [brief description]
SURVIVABILITY_OR_FINANCING_CHANGE = [brief description if survival shifted >10pp]
NEXT_GATE = [specific metric, catalyst, or date]
SUPERSEDES = [prior HANDOFF_ID if this overwrites one] or NONE
RESOLVES_HANDOFF_ID = [prior HANDOFF_ID if this closes one] or NONE
ACTIVE_UNTIL = [expiration date if gated] or OPEN
REQUIRED_CONSUMERS = DAILY | CENSUS | HUNTER | [as relevant]
MANDATORY_DEEP_UNDERWRITING = YES | NO
```

One block per state change or significant shift.

### Section 10: Master Ledger Event

Consolidate all material changes (new convictions, state shifts, conviction reversals, handoff triggers) into one paste-ready event block.

If no material changes: state `NO LOG REQUIRED`.

If changes warrant logging: output `LOG REQUIRED` with paste-ready block:

```
============================================================
CAOS EVENT
============================================================
EVENT_ID = YYYY-MM-DD-WEEKLY-UNIVERSE-STATE_UPDATE
EVENT_TYPE = RANKING_CONSOLIDATION
MODULE = WEEKLY
TIMESTAMP_LOCAL = YYYY-MM-DD HHmm CET
DECISION_AUTHORITY = Mark
EXECUTION_AUTHORITY = Mark only
TRANSACTION_RESULT = NO TRADE (ranking proposal only)

SOURCE_AND_PORTFOLIO_STATE
- Orchestrator run date: YYYY-MM-DD HHmm
- Price denominator: [e.g., "14:30 CET European close"]
- Holdings verified against Master Ledger [date]
- Cash state confirmed [amount, currency]

PREVIOUS_STATE
- [Prior top 3 ranked candidates]
- [Prior execution readiness gate verdict]

NEW_STATE
- [New top 3 ranked candidates by adjusted ranking]
- [New execution readiness gate verdict]

VERIFIED EVIDENCE
- [Summary of Forward Expectations findings (earnings, guidance, analyst changes)]
- [Summary of Risk recalculation (survival thresholds passed/failed)]
- [Summary of any new contradictions detected (or "none")]

CAOS INTERPRETATION
- Which candidates strengthened/weakened conviction
- Why (evidence quality, survival threshold, asymmetry reassessment)
- Ranking stability (top 3 unchanged or shifted)

SURVIVABILITY / FINANCING / DILUTION
- Any survival score degradation >10 percentage points
- Any financing risks surfaced by Portfolio Court
- Any dilution risks flagged

ACTIONABILITY
- Which positions clear minimum edge vs. cash
- Which need escalation (full Anchor re-run, Emergency Rerun, DCA review)
- Any immediate action implications for Mark's next decision cycle

NEXT PROOF GATE
- [Next Daily Anchor, or specific trigger]

SUPERSEDES / RESOLVES
- [Any prior Weekly event] or NONE
============================================================
END CAOS EVENT
============================================================
```

---

## Execution Steps

1. **Verify all 8 agent outputs exist and are readable**
   - Check files VERIFIER through RED_TEAM (optional)
   - If any required agent output missing: state `DATA LIMITED — [agent] output unavailable` and continue with available data
   - If critical agent (Verifier, Underwriter) missing: state `RANKING BLOCKED — [agent] unavailable`

2. **Build consolidated candidate universe**
   - Union of:
     - Holdings from Master Ledger
     - All candidates from Discovery output (new)
     - All candidates from Underwriter output (existing + re-validated)
     - Cash (always included)
   - Deduplicate (same ticker appears in multiple agent outputs)

3. **Extract theses, prices, survival scores**
   - For each candidate: pull Upside/Downside from Underwriter
   - Pull current price from Verifier
   - Pull Conviction from Underwriter or Master Ledger (whichever newer)
   - Pull Survival Score from Risk output
   - Pull Evidence Quality (HIGH/MEDIUM/LOW/DATA LIMITED) from agent outputs

4. **Compute raw-asymmetry ranking**
   - For each candidate: Asymmetry % = Upside / |Downside|
   - Sort all candidates descending by Asymmetry %
   - Build Table 1 with all universe candidates

5. **Compute evidence/survivability-adjusted ranking**
   - For each candidate: Adj. Score = Asymmetry × Evidence Weight × Survival%
     - Evidence Weight: HIGH=1.0, MEDIUM=0.75, LOW=0.5, DATA LIMITED=0.33
     - Survival%: use Risk output percentage (apply thresholds: Seed ≥60%, Challenger ≥50%, Watch ≥40%)
   - Sort all candidates descending by Adj. Score
   - If survival <threshold: downgrade Conviction (Seed→Watch, Challenger→Watch, Watch→Reject)
   - Build Table 2 with updated Conviction

6. **Write both ranking tables**
   - Both show all candidates (no filtering)
   - Both fully transparent and comparable

7. **Run head-to-head fights (brief format)**
   - vs. Portfolio Champion: top Challenger vs. highest-conviction funded holding
   - vs. Quality Anchor: top Seed in adjusted ranking vs. highest-ranked funded Seed
   - vs. Strongest Seed: top Seed by raw asymmetry vs. current strongest Seed
   - vs. Strongest Challenger: top Challenger by adjusted rank vs. top by raw asymmetry
   - vs. Cash: candidates clearing risk-free rate + X%, count below threshold
   - Write 1-2 lines per fight, scannable format

8. **Run system audit (4 checks)**
   - Stale gates: check WATCH/SERIOUS REVIEW candidates in Active Handoff Snapshot, flag gates >90 days
   - Orphans: identify positions <1.5% NAV with no assigned role
   - Contradictions: CORE with survival <40%, state conflicts, handoff conflicts
   - Unresolved handoffs: read Snapshot, emit ACK checks, flag >30 days active

9. **Confirm execution readiness gate (4 preconditions)**
   - Portfolio: Master Ledger current, holdings reconciled
   - Price: all candidates priced, liquids <2h old
   - Ranking: top 3 have stated convictions
   - Handoff: all active handoffs have RECEIVED=YES
   - Output: EXECUTION READY or EXECUTION BLOCKED [reason]

10. **If first run of calendar month: run Architecture Maintenance, Deep Audit reminder, Family-Wealth check**
    - Check calendar date (YYYY-MM-DD)
    - If first Weekly run of month, run §8 above
    - Otherwise skip

11. **Emit handoffs for conviction state changes**
    - For each candidate with updated conviction ≠ previous: emit HANDOFF_ID
    - For survival shifts >10pp: emit handoff
    - For evidence quality shifts: emit handoff

12. **Propose Master Ledger event**
    - Consolidate all material changes
    - If no changes: output `NO LOG REQUIRED`
    - If changes: output `LOG REQUIRED` + paste-ready event block

13. **Write main output file + supporting detail file**
    - Main: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` (all sections 1-10 above)
    - Detail: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md` (detailed head-to-head comparisons: thesis strength, evidence breakdown, survivability path, sizing implications, next gates)

---

## Constraints

- **Never hallucinate data:** consolidate only from agent outputs. If data missing, state `DATA LIMITED`.
- **Handoff ACK integrity:** never claim RECEIVED=YES or APPLIED=YES unless visible in Snapshot. State `LINKAGE DEGRADED / HANDOFF UNAVAILABLE` if missing.
- **Master Ledger logging:** proposal only; Mark confirms by saying `logged`.
- **No autonomous execution, sizing, or trades:** ever.
- **No autonomous legal/tax/trust recommendations:** flag Family-Wealth issues only; never prescribe actions.
- **Monthly task gate:** run §8 only if first Weekly run of calendar month; check calendar date explicitly.
- **Research-only mode:** if Master Ledger stale, run ranking logic but state research-only for portfolio-specific items; do not block ranking production.

---

## Acceptance Criteria

- ✓ All 8 agent outputs consolidated (or DATA LIMITED stated if unavailable)
- ✓ Consolidated universe built: union of holdings + agents' candidates + cash
- ✓ Two ranking tables produced (both show all candidates, both fully visible)
- ✓ Raw-asymmetry Table 1 sorted by upside/downside ratio
- ✓ Adjusted Table 2 sorted by asymmetry × evidence × survival
- ✓ Head-to-head fights: brief format (1-2 lines) in main output, 5 mandatory comparisons
- ✓ Detailed fight comparisons in supporting RANKINGS_DETAIL file
- ✓ System audit: all 4 sections (stale gates, orphans, contradictions, unresolved handoffs)
- ✓ Handoff ACK checks for all active handoffs touching universe
- ✓ Execution readiness gate: EXECUTION READY or EXECUTION BLOCKED [reason] stated clearly
- ✓ If first run of month: Architecture Maintenance, Deep Audit reminder, Family-Wealth check included
- ✓ Handoff emissions emitted for conviction state changes (HANDOFF_ID blocks)
- ✓ Master Ledger event proposal or NO LOG REQUIRED stated
- ✓ Main output file: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md`
- ✓ Supporting detail file: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md`
- ✓ Inputs Consulted section: wikilinks to all 8 agents + Ledger + Snapshot
- ✓ No hallucinated prices, earnings, or evidence; all sources cited
- ✓ No silent failures: state DATA LIMITED, BLOCKED, DEGRADED explicitly when conditions warrant

---
