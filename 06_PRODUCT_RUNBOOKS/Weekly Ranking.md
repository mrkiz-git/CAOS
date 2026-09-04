# CAOS — Weekly Ranking

**Command:** `Run CAOS Weekly Ranking`  
**Status:** VALIDATED — executed for real 2026-09-03 (see [[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_2026-09-03_0740_WEEKLY]]); numeric ranking mechanism found structurally blocked, qualitative ordering substituted  
**Default schedule:** Sunday 10:00, Mark's confirmed timezone (manual or scheduled trigger)

---

## What this product does

Ranks every holding, funded Seed, buy-authorized Seed, Challenger, serious candidate, and cash against each other, showing raw-asymmetry and evidence/survivability-adjusted rankings separately. Runs the full 9-agent pipeline on the consolidated candidate universe. Produces head-to-head fights against the portfolio champion, quality anchor, strongest Seed, strongest Challenger, and cash. Runs system audits for stale gates, orphan positions, contradictions, and unresolved handoffs. On the first Weekly run of each calendar month, also runs Architecture Maintenance, the manual Deep Audit reminder, and the Family-Wealth Architecture Check. Confirms execution readiness gates before DCA Execution Card can proceed.

---

## Precondition Check

Before calling any agent, perform these checks:

1. **Daily Anchor Availability Check:** Verify a same-day or recent Daily Anchor output exists (dated within 7 days). Read `03_AGENT_RUNS/09_ORCHESTRATOR/` for `ORCHESTRATOR_YYYY-MM-DD_*.md`. If not found or stale, state: `DATA LIMITED — Daily Anchor stale (>7 days), using last available prices and candidate universe.` Proceed with available data or halt if critical to operation.

2. **Monster Census Availability Check:** Verify Monster Census output exists and is dated within 30 days. If not found or stale, state: `DATA LIMITED — Monster Census stale (>30 days), candidate discovery may be incomplete.` Proceed; note incomplete new-discovery coverage.

3. **Master Ledger Status Check:** Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]. If status is `UNINITIALIZED` or stale (>7 days), this run operates in **RESEARCH-ONLY / DEGRADED mode**: state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` as a precondition warning. Portfolio-specific action items (funded-holding re-validation, DCA Card gating) report that status. All other Weekly work (price verification, thesis re-check, survival recalculation, ranking production) proceeds in full.

4. **Active Handoff Snapshot Availability Check:** Verify [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] is readable and up-to-date. If missing or >3 days stale, state: `DATA LIMITED — Handoff Snapshot stale, handoff ACK checks incomplete.`

If any precondition blocks the run entirely (Daily Anchor >7 days AND marked FAILED, or Monster Census >30 days), halt and return the blocking condition.

---

## The 7 Mandatory Work Items and Who Produces Them

1. **Weekly price denominator with timestamp and source** — produced by Verifier. Must state current time (e.g., "14:30 CET European close"), source (Bloomberg, broker, exchange), and apply to all candidates in universe.

2. **New candidate identification** — produced by Discovery. Search the 9 high-asymmetry lanes for candidates not yet in Monster Census or Active Handoff Snapshot. Output new candidates only.

3. **Forward guidance re-check** — produced by Forward Expectations. On all candidates in universe, detect earnings surprises, guidance revisions, analyst rating changes, and sector consensus shifts from past 7 days. No speculation; verified facts only.

4. **Sector assessment** — produced by Industry Read-through. Assess structural conditions and competitive shifts in sectors where Weekly Ranking has active candidates. Flag structural changes that might affect thesis validity.

5. **All-candidate thesis re-validation** — produced by Underwriter. For every candidate in consolidated universe, re-validate thesis-core assumptions (business model, market position, valuation, leverage, dilution, liquidity, execution). Reuse Monster Census thesis; update only if Forward evidence or price move prompted change.

6. **Funded-holding re-validation** — produced by Portfolio Court. For every CORE/ATTACKER position, re-validate thesis under current prices and new forward expectations. State whether holding still merits current weight and conviction.

7. **Survival score recalculation** — produced by Risk and Survivability. For every candidate in universe, recalculate survival percentage using current prices and new forward guidance. Apply hard thresholds: Seed ≥60%, Challenger ≥50%, Watch ≥40%. Flag breaches.

(The Orchestrator role — consolidation, ranking, audits, gates, handoff emissions, Master Ledger event — is performed in the primary Claude Code session, not as a subagent.)

---

## Agent Execution Sequence

```
Verifier (establish weekly price denominator)
   |
Discovery -- Forward Expectations -- Industry Read-through   (parallel)
   \                 |                    /
                Underwriter
                /          \
      Portfolio Court   Risk & Survivability                 (parallel)
                \          /
                Red Team (optional)
                   |
              Orchestrator (main session)
```

All agents run in strict serial order shown above. Orchestrator consolidates findings in main Claude Code session (not as subagent).

---

## Agent Call Sequence

No Workflow script and no custom subagent registration are used — this is Claude reading this runbook and calling the Agent tool directly, using each role's invocation prompt template from its own spec file.

### Step 1: Call Verifier (Weekly Ranking)

Call the Agent tool once for Verifier, using the invocation prompt template from [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier (Weekly Ranking)]]. Wait for it to return and confirm `03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_HHmm_WEEKLY.md` was written.

**Output to verify:** Price table with columns Ticker | Current Price | Source | Timestamp. Must include exact HH:mm CET timestamp and state `DATA LIMITED` for any tickers where prices unavailable.

### Step 2: Call Discovery, Forward Expectations, Industry (parallel)

Call the Agent tool three times **in the same turn** — one each for:
- Discovery (Weekly): [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Weekly Ranking)]]
- Forward Expectations (Weekly): [[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations (Weekly Ranking)]]
- Industry Read-through (Weekly): [[03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through (Weekly Ranking)]]

All three depend on Verifier's output (prices and candidate list) but not each other, so all may run concurrently once Step 1 returns. Wait for all three to return.

**Outputs to verify:**
- Discovery: New candidates only, with asymmetry, thesis stage, next gate
- Forward Expectations: Evidence table with ticker | company | evidence type | previous guidance | new guidance | conviction impact | source
- Industry: Sector status table with sector | structural conditions | competitive read | implications for candidates

### Step 3: Call Underwriter (Weekly)

Call the Agent tool once for Underwriter, using the invocation prompt template from [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter (Weekly Ranking)]]. Underwriter's Required Inputs name Forward Expectations and Industry outputs as dependencies, so this call must wait for Step 2 to return. Wait for it to return and confirm `03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_YYYY-MM-DD_HHmm_WEEKLY.md` was written.

**Output to verify:** All-candidate thesis re-validation table with columns Ticker | Company | Company Thesis Status | Security Thesis Status | Survival Score | Prior Conviction | Updated Conviction | Thesis Verdict | Evidence Quality. All candidates in consolidated universe must appear (not just changes).

### Step 4: Call Portfolio Court and Risk & Survivability (parallel)

Call the Agent tool twice **in the same turn** — one each for:
- Portfolio Court (Weekly): [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court (Weekly Ranking)]]
- Risk and Survivability (Weekly): [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability (Weekly Ranking)]]

Both agents' Required Inputs name Underwriter's Weekly output as a dependency, and neither reads the other's output, so both calls wait for Step 3 to return but may then run concurrently in the same turn. Wait for both to return.

**Outputs to verify:**
- Portfolio Court: Funded holdings table with columns Ticker | Position | Current Weight | Thesis Verdict | Survival % | Conviction | Action | Escalate?
- Risk: All-candidate survival table with columns Ticker | Company | Conviction | Survival Score | Threshold | Pass/Fail | Financing Risk | Dilution Risk | Verdict

### Step 5: Call Red Team (optional)

Call the Agent tool once for Red Team (optional), using the invocation prompt template from [[03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team (Weekly Ranking)]]. Red Team depends on Risk output (top 5 candidates by adjusted ranking). If time is constrained, skip this step; Orchestrator will continue without it. Wait for it to return if executed.

**Output to verify:** Stress-test scenarios with columns Scenario | Affected Candidates | Ranking Breaks | Robustness. Scenarios: Asymmetry -50% | Survival -20pp | Company Thesis Breaks | Sector Collapse.

### Step 6: Perform the Orchestrator Role (primary session, not a subagent)

Do not spawn a subagent for this step. Read all agent outputs from steps 1–5 above, read Daily Anchor output, read Master Ledger, read Active Handoff Snapshot, and write:
- `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` (main output)
- `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY_RANKINGS_DETAIL.md` (supporting detail)

See [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Weekly Ranking)]] for full output structure and execution steps. Present the final verdict in chat.

---

## Linking Rule Application

Every file written in steps 1–5 above must open with an "Inputs Consulted" section per each agent's output contract, wikilinked to upstream files it read. The Orchestrator file additionally opens with an "Inputs Consulted" section linking all 8 agent files, Daily Anchor, Master Ledger, and Active Handoff Snapshot.

This makes the dependency graph traversable in Obsidian: open any file's "Linked mentions" panel to see every file that later relied on it.

---

## Execution Rules

**From Operator Manual §3 (Constitutional Laws):**
- **Reality First.** Verified prices and evidence only; state `DATA LIMITED` or `UNKNOWN` if evidence missing.
- **Fresh-Evidence Supremacy.** Current verified prices and newest confirmed portfolio state override prior prices, rankings, or assumptions.
- **Objective Supremacy.** No incumbent holding protection; re-validate all theses on current evidence.
- **Survivability Before Optionality.** Reject huge upside when survival is implausible.
- **No Autonomous Trading.** Never assume a fill or place a trade. Report verdict and handoff emission only.
- **No Margin or Leverage.** Use cash-basis assumptions only.
- **No Kelly Sizing.** No sizing claims without explicit Mark authorization.

**Discipline specifics:**
- Never claim a price, earnings fact, or guidance update without citing source.
- Never state "thesis intact" without visible evidence from current price/news/guidance.
- Never hide degraded linkage or stale data — state `DATA LIMITED` or `UNKNOWN` explicitly.
- Price direction alone (a stock rising or falling) never implies a buy or sell conviction.
- No hallucinated companies, financials, or market data.

---

## Success Criteria (Acceptance Checklist)

- ✓ All 9 agents run in order (Verifier → Discovery/Forward/Industry parallel → Underwriter → Portfolio Court/Risk parallel → Red Team optional → Orchestrator)
- ✓ Verifier establishes weekly price denominator for full universe
- ✓ All agent outputs written and linked in Orchestrator "Inputs Consulted"
- ✓ Consolidated universe built (union of holdings + Seeds + Challengers + serious candidates + new discoveries + cash)
- ✓ Two ranking tables produced (raw-asymmetry and evidence/survivability-adjusted) with all candidates visible in both
- ✓ Head-to-head fights output in brief format (1-2 lines per fight) in main Orchestrator output
- ✓ Detailed fight comparisons in supporting RANKINGS_DETAIL document
- ✓ System audit section: stale gates, orphans, contradictions, unresolved handoffs
- ✓ Handoff ACK checks for all active handoffs touching universe candidates
- ✓ Execution readiness gate confirms EXECUTION READY or states EXECUTION BLOCKED [reason]
- ✓ If first run of calendar month: Architecture Maintenance, Deep Audit reminder, Family-Wealth check outputs included
- ✓ Handoff emissions emitted for any conviction state changes (HANDOFF_ID blocks)
- ✓ Master Ledger event proposal or NO LOG REQUIRED stated
- ✓ No hallucinated prices, earnings, or evidence; all sources cited
- ✓ File named `ORCHESTRATOR_YYYY-MM-DD_HHmm_WEEKLY.md` and supporting detail file created
- ✓ No silent failures: state DATA LIMITED, BLOCKED, DEGRADED explicitly when conditions warrant

---

## Failure States and Recovery

**RANKING BLOCKED — Missing precondition**
- Daily Anchor not found and required for baseline
- Monster Census not found and critical for candidate universe
- Master Ledger UNINITIALIZED and holdings state unknown
- **Recovery:** Fix missing precondition and retry

**RANKING DEGRADED — Limited data available**
- `DATA LIMITED — price source unavailable for [TICKER1, TICKER2]` — continue with available data for other candidates
- `DATA LIMITED — portfolio state stale, running in research-only mode` — ranking proceeds; funded-holding-specific items blocked
- `DATA LIMITED — handoff snapshot stale or incomplete` — handoff ACK checks incomplete; flag in output
- **Recovery:** Fetch missing data and rerun, or proceed with limited coverage and note gaps in output

**RANKING FAILED — Agent failure mid-run**
- [Agent name] failed (specify which and why) — **do not continue to next step.** Halt, state the failure, and determine whether agent output is recoverable. If critical agent (Verifier, Underwriter), halt the entire run. If optional agent (Red Team), skip and continue to Orchestrator.
- Orchestrator unable to consolidate (specify missing or corrupt inputs) — state which input file is unreadable or corrupt, and whether run can proceed with degraded data
- **Recovery:** Fix the failing agent, rerun, or proceed with DATA LIMITED status if tolerable

---

## Design Spec and Detailed Requirements

See: [[06_PRODUCT_RUNBOOKS/Weekly Ranking Design]]

Full specification of ranking logic (two tables), head-to-head fight format, system audit checks, monthly special tasks, handoff protocol, execution gates, and constraints.

---

## Dry-Run Test Plan

See: `04_FLIGHT_RECORDER/Weekly Ranking Dry-Run Test.md`

Covers three scenarios: Happy Path (all agents succeed), Degraded Data (stale Master Ledger), No State Changes (all theses hold). Includes pre-run checklist, execution tracking table, post-run checklist, and troubleshooting guide.

---
