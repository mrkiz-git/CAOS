# Weekly Ranking — Dry-Run Test Plan

**Objective:** Verify all 9 agents run in sequence, consolidation logic works, ranking tables are accurate, audits detect issues, gates function, and monthly tasks trigger correctly.

**Test plan date:** 2026-09-01  
**Execution date:** [TBD — record actual test date here]

---

## Scenario 1: Happy Path (All Agents Succeed)

**Objective:** Verify complete end-to-end execution with no missing inputs, all agents succeeding, new evidence detected, and proper ranking consolidation.

### Setup

- Daily Anchor has completed within last 7 days (baseline available)
- Monster Census has completed within last 30 days (candidate universe established)
- Master Ledger current and holdings reconciled
- Active Handoff Snapshot up-to-date
- Prices available for all candidates in universe
- Forward evidence exists (earnings releases, guidance updates, analyst changes from past 7 days)
- New candidates discovered from 9 discovery lanes
- At least one sector shows structural change
- No contradictions or stale gates in system (system audit clean)
- All 9 agent specs ready and callable

### Execution Steps

#### Step 1: Invoke Verifier Agent
- Expected: Fetches current prices and establishes weekly denominator (e.g., "14:30 CET European close")
- Expected output: `VERIFIER_YYYY-MM-DD_HHmm_WEEKLY.md`
- Should include: all candidates in universe + prices + source + timestamp
- Expected runtime: 2-5 minutes

#### Step 2: Invoke Discovery, Forward, Industry (parallel)
- Expected: Discovery finds 1-3 new candidates from 9 lanes; Forward detects earnings/guidance changes; Industry reassesses active sectors
- Expected outputs:
  - `DISCOVERY_YYYY-MM-DD_HHmm_WEEKLY.md` (new candidates with asymmetry/thesis)
  - `FORWARD_YYYY-MM-DD_HHmm_WEEKLY.md` (earnings/guidance/analyst changes)
  - `INDUSTRY_YYYY-MM-DD_HHmm_WEEKLY.md` (sector assessments)
- Expected runtime: 8-15 minutes (parallel)

#### Step 3: Invoke Underwriter Agent
- Expected: Re-validates thesis for all candidates (holdings + Seeds + Challengers + serious candidates + new discoveries)
- Expected output: `UNDERWRITER_YYYY-MM-DD_HHmm_WEEKLY.md`
- Should include: all candidates with thesis status, survival score, updated conviction
- Expected runtime: 10-15 minutes

#### Step 4: Invoke Portfolio Court and Risk & Survivability (parallel)
- Expected: Portfolio Court re-validates funded holdings; Risk recalculates survival scores for all candidates
- Expected outputs:
  - `PORTFOLIO_COURT_YYYY-MM-DD_HHmm_WEEKLY.md` (funded holdings table)
  - `RISK_YYYY-MM-DD_HHmm_WEEKLY.md` (all-candidate survival table)
- Expected runtime: 8-12 minutes (parallel)

#### Step 5: Invoke Red Team (optional)
- Expected: Stress-tests top 5 candidates by adjusted ranking
- Expected output: `RED_TEAM_YYYY-MM-DD_HHmm_WEEKLY.md` (4 stress scenarios)
- Expected runtime: 5-10 minutes (optional; can skip if time-constrained)

#### Step 6: Invoke Orchestrator (main session)
- Expected: Reads all agent outputs, consolidates universe, produces two ranking tables, runs audits, confirms gates
- Expected outputs:
  - `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` (main output)
  - `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md` (supporting detail)
- Should include:
  - Consolidated universe summary (holdings count, Seeds, Challengers, serious candidates, new discoveries, cash)
  - Table 1: Raw-Asymmetry Ranking (all candidates sorted by upside/downside ratio)
  - Table 2: Evidence/Survivability-Adjusted Ranking (all candidates sorted by asymmetry × evidence × survival)
  - Head-to-Head Fights (brief format: vs. Portfolio Champion, Quality Anchor, Strongest Seed, Strongest Challenger, Cash)
  - System Audit (stale gates, orphans, contradictions, unresolved handoffs)
  - Handoff ACK Checks (for all active handoffs)
  - Execution Readiness Gate (EXECUTION READY verdict)
  - Handoff Emissions (if conviction shifts detected)
  - Master Ledger Event block (LOG REQUIRED or NO LOG REQUIRED)
- Expected runtime: 15-25 minutes

### Validation Checklist

- [ ] All 9 agents run in order: Verifier → Discovery/Forward/Industry parallel → Underwriter → Portfolio Court/Risk parallel → Red Team optional → Orchestrator
- [ ] All 8 agent outputs written (VERIFIER, DISCOVERY, FORWARD, INDUSTRY, UNDERWRITER, PORTFOLIO_COURT, RISK, [RED_TEAM])
- [ ] Orchestrator "Inputs Consulted" section wikilinks all 8 agents, Daily Anchor, Master Ledger, Active Handoff Snapshot
- [ ] Consolidated universe contains: holdings + Seeds + Challengers + serious candidates + new discoveries + cash
- [ ] Table 1 (Raw-Asymmetry) includes all candidates sorted by upside/downside ratio
- [ ] Table 2 (Adjusted) includes all candidates sorted by asymmetry × evidence × survival
- [ ] No candidates filtered out; both tables show full universe
- [ ] Head-to-head fights output in brief format (1-2 lines per fight)
- [ ] Detailed fight comparisons present in RANKINGS_DETAIL file
- [ ] System audit: 4 sections (stale gates, orphans, contradictions, unresolved handoffs)
- [ ] Stale gates audit: no gates >90 days without re-eval
- [ ] Orphans audit: no positions <1.5% NAV without assigned role (or flagged as WARNING)
- [ ] Contradictions audit: no CORE holdings with survival <40%, no state conflicts
- [ ] Unresolved handoffs audit: all active handoffs have RECEIVED=YES, none >30 days active
- [ ] Handoff ACK checks output for all active handoffs in Snapshot
- [ ] Execution gate result stated: EXECUTION READY (all 4 gates pass)
- [ ] If test date is first run of month: Architecture Maintenance, Deep Audit reminder, Family-Wealth check outputs present
- [ ] Handoff emissions present (if any conviction state changes detected)
- [ ] Master Ledger event present (LOG REQUIRED block or NO LOG REQUIRED statement)
- [ ] All prices sourced and cited (no hallucinated prices)
- [ ] All evidence labeled (VERIFIED FACT, CAOS INFERENCE, UNVERIFIED LEAD, DATA LIMITED, UNKNOWN)
- [ ] File naming correct: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` + `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md`

---

## Scenario 2: Degraded Data (Stale Master Ledger, Portfolio Gate Fails)

**Objective:** Verify system handles degraded portfolio state gracefully, runs in research-only mode, but blocks execution gate.

### Setup

- Master Ledger UNINITIALIZED or >7 days stale
- Holdings unknown (execution-critical gate fails)
- Price data available for other checks
- All other inputs current (Daily Anchor, Monster Census, Active Handoff Snapshot)
- All 9 agent specs ready

### Execution Steps

#### Steps 1-5: All agents run normally
- Verifier, Discovery, Forward, Industry, Underwriter, Portfolio Court, Risk all complete without data issues
- Only portfolio-state-specific items (funded holdings count, NAV-based orphan detection) will report limitations

#### Step 6: Invoke Orchestrator with degraded portfolio state
- Expected: Orchestrator reads stale Master Ledger
- Expected behavior: Orchestrator runs all ranking logic, produces tables, runs audits, but:
  - States `HOLDINGS UNKNOWN / EXECUTION BLOCKED` in Portfolio Gate
  - Emits `EXECUTION BLOCKED [reason: Portfolio Gate — Master Ledger stale, HOLDINGS UNKNOWN]`
  - DCA Execution Card cannot proceed until Portfolio Gate clears

### Validation Checklist

- [ ] All agents complete despite stale Master Ledger
- [ ] Orchestrator output includes: `DATA LIMITED — portfolio state stale, running in research-only mode`
- [ ] Two ranking tables produced (research mode)
- [ ] Head-to-head fights output (based on available evidence)
- [ ] System audit runs; orphan audit flags `DATA LIMITED — NAV state unknown` for any orphan checks requiring NAV
- [ ] Execution gate explicitly states:
  ```
  Portfolio Gate: FAIL — reason: Master Ledger stale, HOLDINGS UNKNOWN
  Ranking Gate: [status — may PASS if top 3 have convictions]
  Price Gate: [status — likely PASS if prices available]
  Handoff Gate: [status]
  
  EXECUTION READINESS GATE: EXECUTION BLOCKED
  Reason: Portfolio Gate failed. DCA Execution Card cannot proceed.
  ```
- [ ] No portfolio-specific actions proposed (no allocation recommendations)
- [ ] Master Ledger event states: `NO LOG REQUIRED` (ranking only, no changes to log)

---

## Scenario 3: No State Changes (All Theses Intact)

**Objective:** Verify system handles stable week correctly: all agents run, theses hold, no conviction shifts, no logging needed.

### Setup

- All preconditions current (Daily Anchor ≤7d, Monster Census ≤30d, Master Ledger current)
- All agents run normally
- No new candidates discovered (Discovery output empty or "no candidates meet threshold")
- No Forward evidence detected (no earnings, guidance, analyst changes)
- Prices unchanged or <2% move (not sufficient to trigger thesis re-eval)
- Survival scores unchanged
- No contradictions or stale gates
- No conviction shifts from prior week

### Execution Steps

#### Steps 1-6: All agents run, no material changes detected
- Verifier: prices stable
- Discovery: no new candidates above threshold
- Forward: no material forward guidance changes
- Industry: no structural shifts in active sectors
- Underwriter: all theses intact (no updates needed from prior week)
- Portfolio Court: all funded holdings solid, no risks
- Risk: all survival scores stable, all thresholds passed
- Orchestrator: consolidates stable state

### Validation Checklist

- [ ] All agents complete successfully
- [ ] Discovery output: "No candidates meet discovery threshold" or "0 new candidates found"
- [ ] Forward output: "No material forward guidance changes" or empty findings table
- [ ] Ranking tables produced (same as prior week or minor rank order changes from price moves <2%)
- [ ] Head-to-head fights verdict: "Thesis intact" for all comparisons
- [ ] System audit: all clean (no stale gates, no orphans flagged, no contradictions, no unresolved handoffs)
- [ ] Execution gate: EXECUTION READY (all 4 gates pass)
- [ ] Handoff emissions: NONE (no conviction shifts)
- [ ] Master Ledger event: `NO LOG REQUIRED` (no material changes to log)
- [ ] Orchestrator summary: "No material changes from prior week. All theses intact. System healthy."

---

## Pre-Run Checklist

- [ ] Daily Anchor output exists and is dated within 7 days
- [ ] Monster Census output exists and is dated within 30 days
- [ ] Master Ledger is current and reconciled (for Scenario 1 only; Scenario 2 tests degraded state)
- [ ] Active Handoff Snapshot is readable and up-to-date
- [ ] All 9 agent specs are in place and readable:
  - `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier (Weekly Ranking).md`
  - `03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Weekly Ranking).md`
  - `03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations (Weekly Ranking).md`
  - `03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through (Weekly Ranking).md`
  - `03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter (Weekly Ranking).md`
  - `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court (Weekly Ranking).md`
  - `03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability (Weekly Ranking).md`
  - `03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team (Weekly Ranking).md`
  - `03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Weekly Ranking).md`
- [ ] Orchestrator spec is current (consolidated consolidation, ranking, audit, gates logic)
- [ ] Test time is noted (include expected duration buffer: 60-90 minutes for full run)
- [ ] Mark has confirmed timezone for scheduled run

---

## Execution Tracking Table

**Test run date:** ____________  
**Scenario:** ☐ Happy Path | ☐ Degraded Data | ☐ No State Changes  
**Test start time:** ________  

| Step | Agent/Task | Timestamp | Status | Output File | Data Quality | Notes |
|------|------------|-----------|--------|-------------|--------------|-------|
| 1 | Verifier: price denominator | | PASS/FAIL | VERIFIER_...WEEKLY.md | OK/GAP | |
| 2a | Discovery: parallel start | | PASS/FAIL | DISCOVERY_...WEEKLY.md | NEW/NONE | |
| 2b | Forward: parallel start | | PASS/FAIL | FORWARD_...WEEKLY.md | FOUND/NONE | |
| 2c | Industry: parallel start | | PASS/FAIL | INDUSTRY_...WEEKLY.md | OK/LIMITED | |
| 3 | Underwriter: serial after 2 | | PASS/FAIL | UNDERWRITER_...WEEKLY.md | OK/INCOMPLETE | |
| 4a | Portfolio Court: parallel after 3 | | PASS/FAIL | PORTFOLIO_COURT_...WEEKLY.md | OK/INCOMPLETE | |
| 4b | Risk: parallel after 3 | | PASS/FAIL | RISK_...WEEKLY.md | OK/INCOMPLETE | |
| 5 | Red Team: optional after 4 | | SKIP/PASS/FAIL | RED_TEAM_...WEEKLY.md | OK/N/A | |
| 6 | Orchestrator: consolidate | | PASS/FAIL | ORCHESTRATOR_...WEEKLY.md | OK/INCOMPLETE | |
| 6b | Orchestrator: detail doc | | PASS/FAIL | ORCHESTRATOR_...RANKINGS_DETAIL.md | OK/INCOMPLETE | |

**Total test duration:** ________  

---

## Post-Run Checklist

- [ ] Orchestrator main output file created and readable
- [ ] Orchestrator detail file created and readable
- [ ] Two ranking tables present (raw-asymmetry and adjusted)
- [ ] All candidates visible in both tables (no filtering)
- [ ] Head-to-head fights output in brief format (1-2 lines each): vs. Portfolio Champion, Quality Anchor, Strongest Seed, Strongest Challenger, Cash
- [ ] System audit section present with 4 subsections (stale gates, orphans, contradictions, unresolved handoffs)
- [ ] Handoff ACK checks present for active handoffs (RECEIVED=YES/NO stated)
- [ ] Execution gate result stated: EXECUTION READY or EXECUTION BLOCKED [reason]
- [ ] If test date is first run of month: Architecture Maintenance, Deep Audit reminder, Family-Wealth check outputs present
- [ ] If state changes detected: Handoff emissions present (HANDOFF_ID blocks)
- [ ] Master Ledger event present: LOG REQUIRED [paste-ready block] or NO LOG REQUIRED
- [ ] All input files linked in "Inputs Consulted" section
- [ ] No hallucinated data (all prices, earnings, evidence sourced)
- [ ] File naming correct: `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` and detail file

---

## Troubleshooting Guide

**Agent [X] failed or timed out**
- Check agent spec exists and is readable
- Verify agent inputs are present (check prior agent output file)
- Rerun agent; if failure repeats, escalate or skip (if optional, e.g., Red Team)
- If critical agent (Verifier, Underwriter) fails, halt and investigate

**Ranking tables incomplete or missing candidates**
- Verify all 8 agent outputs are present
- Check Orchestrator consolidation logic: is union of all agents' outputs being computed?
- Verify no candidates are being filtered out (should show all, even unchanged ones)

**Execution gate EXECUTION BLOCKED**
- Check which gate failed (Portfolio, Price, Ranking, Handoff)
- Portfolio Gate: Master Ledger stale or holdings unknown → expected in Scenario 2
- Price Gate: which tickers missing prices? → fetch and rerun Verifier
- Ranking Gate: top 3 missing convictions? → rerun Underwriter or Orchestrator
- Handoff Gate: which handoff missing RECEIVED=YES? → check Active Handoff Snapshot

**System audit flags contradictions**
- CORE holding with survival <40% → rerun Risk, confirm survival calculation
- State conflicts → check Active Handoff Snapshot for duplicate/conflicting handoffs
- Handoff conflicts → read specific handoff; if superseded, update to RESOLVED status

**Monthly tasks didn't run (if first run of month)**
- Verify test date is first run of calendar month
- Check Orchestrator code: is calendar date check included?
- If yes but didn't run: debug date check logic

---

## Sign-Off

**Test scenario(s) run:** Scenario 1 ☐ | Scenario 2 ☐ | Scenario 3 ☐

**Result per scenario:**
- Scenario 1 (Happy Path): PASS / FAIL / PARTIAL
- Scenario 2 (Degraded Data): PASS / FAIL / PARTIAL
- Scenario 3 (No State Changes): PASS / FAIL / PARTIAL

**Blocker issues (none / list below):**

- 

**Action items (none / list below):**

- 

**Next step:**
- [ ] All scenarios PASS → approve for production deployment
- [ ] Scenario(s) FAIL → fix blocker(s) and re-test
- [ ] PARTIAL (some scenarios pass) → fix failures and re-test

**Signed by:** ____________  
**Date:** ____________  

---
