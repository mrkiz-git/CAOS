# CAOS — Post-Open Delta Check

**Command:** `Run CAOS Post-Open Delta Check`  
**Status:** IMPLEMENTATION IN PROGRESS  
**Schedule:** Ad hoc, intraday after market open (never scheduled independently)

---

## Precondition Check

Before calling any agent, perform these two checks:

1. **Daily Anchor Output Check:** Read `03_AGENT_RUNS/09_ORCHESTRATOR/` to verify a same-day Orchestrator file (`ORCHESTRATOR_YYYY-MM-DD_*.md`) exists. If no completed Daily Anchor output is found, stop and return: `DELTA CHECK BLOCKED — NO SAME-DAY ANCHOR. Post-Open Delta Check requires a completed Daily Anchor from today to establish baseline prices and candidate list.`

2. **Master Ledger Status Check:** Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] to verify its status. If status is `UNINITIALIZED` or stale, this run operates in **RESEARCH-ONLY / DEGRADED mode**: state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` as a precondition warning, and every checklist item below that depends on real funded holdings reports that status instead. All other Delta Check work (price verification, thesis re-check, risk recalculation) proceeds in full.

If either precondition blocks the run, do not call any agent. State the blocking condition and stop.

---

## The 7 Mandatory Work Items and Who Produces Them

1. **Price denominator with timestamp and source** — produced by Verifier. Must state current time (HH:mm CET), source (Bloomberg, Yahoo Finance, broker feed, exchange API), and comparison basis ("Daily Anchor close 18:15 CET vs current intraday 14:30 CET").

2. **Changed candidates identification** — produced by Verifier. Flag all candidates with ±5%+ price move from Daily Anchor denominator or fundamental changes (earnings surprise, guidance revision, news, contract award, regulatory event, analyst revision).

3. **Forward expectations re-check** — produced by Forward Expectations. Identify earnings surprises, guidance changes, analyst revisions, and contract/regulatory updates on changed candidates only.

4. **Thesis re-validation** — produced by Underwriter. For each changed candidate, re-check thesis-core assumptions (valuation denominator, per-share economics, survival, financing, execution probability) against current prices and new forward data. Report conviction change explicitly: thesis intact, degraded, confirmed, or falsified.

5. **Funded holding re-validation** — produced by Portfolio Court. For each CORE/ATTACKER position flagged by Verifier, re-validate thesis against current prices and new forward expectations. State whether funded holding thesis is intact, degraded, confirmed, or escalation-required.

6. **Survival recalculation** — produced by Risk and Survivability. For each flagged candidate, recalculate survival percentage using current prices and new forward guidance. Compare to Daily Anchor baseline and flag breaches of hard thresholds (Seed ≥60%, Challenger ≥50%, Watch ≥40%).

7. **Consolidated delta verdict with handoff emissions** — produced by Orchestrator. Compare each changed candidate's Daily Anchor conviction to Delta conviction. Emit handoffs for material conviction shifts. State whether escalation needed before next scheduled Anchor or immediate action required.

---

## Agent Call Sequence

No Workflow script and no custom subagent registration are used — this is Claude reading this runbook and calling the Agent tool directly, using each role's invocation prompt template from its own spec file.

### Step 1: Call Verifier (Delta Check)

Call the Agent tool once for the Verifier, using the invocation prompt template from [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier (Delta Check)]]. Wait for it to return and confirm `03_AGENT_RUNS/01_VERIFIER/VERIFIER_DELTA_<date>_<time>.md` was written.

**Output to verify:** Price denominator table with columns Ticker | Price Δ % | Price Denominator | Source | Timestamp. Must include exact HH:mm timestamp and state `DATA LIMITED` for any tickers where prices unavailable.

### Step 2: Call Forward Expectations, Underwriter, Portfolio Court, Risk & Survivability (parallel)

Call the Agent tool four times **in the same turn** — one call each for:
- Forward Expectations: [[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]
- Underwriter (Delta Check): [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter (Delta Check)]]
- Portfolio Court (Delta Check): [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court (Delta Check)]]
- Risk and Survivability (Delta Check): [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability (Delta Check)]]

These are independent of each other (all depend only on Verifier output), so issuing all four tool calls in one response runs them concurrently. Wait for all four to return.

**Outputs to verify:**
- Forward Expectations: forward-guidance table (binding contract / nonbinding target / management aspiration / CAOS inference) and next falsifiable proof point per company.
- Underwriter Delta: thesis re-check per flagged candidate with conviction change verdict (THESIS INTACT | THESIS DEGRADED | THESIS CONFIRMED | THESIS FALSIFIED).
- Portfolio Court Delta: Holdings Re-Validation Table with columns Ticker | Daily Anchor Conviction | Current Price Δ % | Thesis Verdict | Survival Score | Action. End verdict line states FUNDED HOLDINGS VALIDATED / HOLDINGS DEGRADED / ESCALATION REQUIRED.
- Risk Delta: Survival Recalculation Table with columns Ticker | Baseline Survival | New Survival | Survival Shift | Threshold | Threshold Status | Evidence Quality. End verdict line states RISK DELTA REVIEW = COMPLETE / DATA LIMITED / ESCALATION REQUIRED.

### Step 3: Perform the Orchestrator Role (primary session, not a subagent)

Do not spawn a subagent for this step. Read all 4 agent files from this run, read the Daily Anchor output file from `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_*.md`, and write `03_AGENT_RUNS/09_ORCHESTRATOR/POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md` with the structure specified in "Required Output Format" below. Present the final verdict in chat.

---

## Linking Rule Application

Every file written in steps 1–3 above must open with an "Inputs Consulted" section per each agent's output contract. The Delta Check Orchestrator file (POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md) additionally opens with a "Full Delta Map" section linking:
- Daily Anchor output file (baseline)
- Verifier Delta output (price denominator and flagged candidates)
- Forward Expectations output (forward guidance on changed tickers)
- Underwriter Delta output (thesis re-checks)
- Portfolio Court Delta output (funded holding re-validation)
- Risk Delta output (survival recalculation)

This makes the dependency graph traversable in Obsidian: open any file's "Linked mentions" panel to see every file that later relied on it.

---

## Execution Rules

**From Operator Manual §3 (Constitutional Laws):**
- **Reality First.** Verified prices and news only; state `DATA LIMITED` or `UNKNOWN` if evidence missing.
- **Fresh-Evidence Supremacy.** Current verified prices override Anchor prices if moved ±5%+.
- **Objective Supremacy.** No incumbent holding protection; re-validate all theses on current evidence.
- **Survivability Before Optionality.** Flag holdings with degraded survival; escalate if below hard threshold.
- **No Autonomous Trading.** Never assume a fill or propose a trade. Report conviction change and handoff emission only.
- **No Margin or Leverage.** Use cash-basis prices and assumptions only.
- **No Kelly Sizing.** No sizing claims without explicit Mark authorization of an audited module.

**Discipline specifics:**
- Never claim a price or fundamental change without citing source.
- Never state "thesis intact" without visible evidence from current price/news/guidance.
- Never hide degraded linkage or stale data — state `DATA LIMITED` or `UNKNOWN` explicitly.
- Price direction alone (a stock rising or falling) never implies a buy or sell conviction.

---

## Required Output Format

The Orchestrator file (`POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md`) must include, in order:

### 1. Header
```
# CAOS — Post-Open Delta Check
Date: YYYY-MM-DD HH:mm CET
Baseline: Daily Anchor completed YYYY-MM-DD 18:15 CET
Current: Intraday prices as of HH:mm CET
Price denominator: [specific source, e.g., "Bloomberg 14:30 CET European close"]
```

### 2. Full Delta Map
Wikilink section listing all input files:
- Daily Anchor output (`[[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_*]]`)
- Verifier Delta output
- Forward Expectations output
- Underwriter Delta output
- Portfolio Court Delta output
- Risk Delta output

### 3. Delta Summary
**One-line verdict:** "[No material changes detected]" or "[N] candidates with thesis changes"

### 4. Changed Candidates Table
Only candidates with ±5%+ price move or fundamental changes. Columns: Ticker | Price Δ % | Change Type | Baseline Conviction | Updated Conviction | Thesis Verdict | Action

Example:
```
| Ticker | Price Δ % | Change Type | Baseline Conviction | Updated Conviction | Thesis Verdict | Action |
|--------|-----------|---|---|---|---|---|
| AVGO | +3.2% | Price only | SEED | SEED | Thesis intact, survival 70% confirmed | Hold |
| CEG | -6.5% | Price + earnings news | WATCH | WATCH | Survival dropped to 65%, trigger timeline extended | Review full Anchor before re-entry |
```

### 5. Orchestrator Verdict
1–2 sentence summary: which positions remain valid, which need deep re-analysis, portfolio thesis impact.

Example: "Three candidates moved intraday; all theses remain intact. CEG's survival assumption shifted but trigger remains valid. No escalation needed before next scheduled Anchor."

### 6. Handoff Emissions
If material conviction shifts detected, emit handoff blocks per Operator Manual §9 format.

Example:
```
HANDOFF_ID = 20260831-DAILY-CEG-CONVICTION_SHIFT
ORIGIN_MODULE = DAILY
ORIGIN_DATE = 2026-08-31
SECURITY/TICKER = CEG
HANDOFF_TYPE = CANDIDATE_STATE
SOURCE = Post-Open Delta Check
SOURCE_SIGNAL_DATE = 2026-08-31 14:30 CET
DEDUP_KEY = DAILY|CEG|DELTA_CHECK|20260831
PREVIOUS_STATE = WATCH (survival 75%, trigger Q3 2026)
NEW_STATE = WATCH (survival 65%, trigger timeline extended)
EVIDENCE_QUALITY = MEDIUM
THESIS_OR_ASYMMETRY_CHANGE = Earnings guidance revised; thesis framework intact but timeline shifted
SURVIVABILITY_OR_FINANCING_CHANGE = Survival recalculated from 75% to 65%; remains above 40% Watch threshold
NEXT_GATE = Earnings call transcript review, next Anchor re-check
SUPERSEDES = NONE
RESOLVES_HANDOFF_ID = NONE
ACTIVE_UNTIL = 2026-09-30
REQUIRED_CONSUMERS = WEEKLY,CENSUS
MANDATORY_DEEP_UNDERWRITING = NO
```

### 7. Master Ledger Event (if required)
State either `LOG REQUIRED` (followed by paste-ready event block) or `NO LOG REQUIRED`.

If logging required, paste-ready block includes:
```
============================================================
CAOS EVENT
============================================================
EVENT_ID = YYYY-MM-DD-DELTA-SUBJECT-CHANGE
EVENT_TYPE = CANDIDATE_CONVICTION_DELTA
MODULE = DAILY (subproduct of Daily Anchor)
TIMESTAMP_LOCAL = [intraday time of check]
DECISION_AUTHORITY = Mark
EXECUTION_AUTHORITY = Mark only
TRANSACTION_RESULT = NO TRADE

SOURCE_AND_PORTFOLIO_STATE
- [Portfolio state timestamp from Daily Anchor baseline]

PREVIOUS_STATE
- [Daily Anchor conviction for changed candidates]

NEW_STATE
- [Updated conviction after Delta Check]

VERIFIED EVIDENCE
- [Verifier price stamp with source and timestamp]
- [Forward Expectations findings on changed candidates]
- [Underwriter thesis re-check conclusions]
- [Portfolio Court funded-holding re-validation verdict]
- [Risk survival recalculation results]

CAOS INTERPRETATION
- Which theses remain intact, which shifted
- Why (price move, news, earnings surprise, guidance change, etc.)
- Conviction direction and magnitude of shift

SURVIVABILITY / FINANCING / DILUTION
- [Any survival assumption changes]
- [Financing or dilution impact from price move or news]

ACTIONABILITY
- Which positions can hold as-is
- Which need escalation (full Anchor re-run, Emergency Rerun, etc.)
- Any immediate action implications

NEXT PROOF GATE
- [Next daily Anchor, or specific trigger]

SUPERSEDES / RESOLVES
- [Prior handoff or event, if applicable]
============================================================
END CAOS EVENT
============================================================
```

---

## Failure Handling

### Blocked Conditions (cannot run)

**`DELTA CHECK BLOCKED — NO SAME-DAY ANCHOR`**
- Daily Anchor output not found for today
- Cannot establish baseline for comparison
- Action: Do not call any agent. Stop and inform Mark.

**`DELTA CHECK BLOCKED — STALE MASTER LEDGER`**
- Master Ledger status is `UNINITIALIZED` or stale (per Operator Manual §4)
- Portfolio state unknown; cannot re-validate thesis for funded holdings
- Action: State `HOLDINGS UNKNOWN / EXECUTION BLOCKED` and stop. Research-only work cannot proceed without funded holdings baseline.

### Degraded Conditions (can continue with caveats)

**`DATA LIMITED — price source unavailable [TICKER1, TICKER2]`**
- Verifier unable to fetch current prices for specific tickers
- Action: State which tickers. Resume with available data for other candidates. Underwriter, Portfolio Court, and Risk skip unavailable tickers.

**`NO MATERIAL DELTAS`**
- No candidates moved ±5% or had fundamental changes
- Action: Output "All theses intact. Daily Anchor convictions confirmed. NO LOG REQUIRED."

### Hard Constraints (per Operator Manual §12)
- No autonomous trades
- No buy sizing without live price and confirmed real cash
- No margin or leverage
- No Kelly claims
- No hallucinated prices, news, or earnings data (Verifier must cite sources)

### Failure States

If any agent call in step 1–2 fails or returns an unusable result, do not continue as if it succeeded. Report:
- **`DELTA CHECK DEGRADED`** if enough of the pipeline completed to say something useful about some candidates
- **`DELTA CHECK FAILED`** if not

State exactly what completed, what failed, and whether a manual rerun is needed. Never finish a run silently.

---

## Acceptance Criteria Checklist

- ✓ Daily Anchor output from same session exists and is readable
- ✓ Master Ledger status is checked; run reports `HOLDINGS UNKNOWN / EXECUTION BLOCKED` if stale
- ✓ Verifier successfully fetches current prices and establishes new denominator with exact HH:mm timestamp
- ✓ Changed candidates identified by Verifier (±5% price move or fundamental news)
- ✓ Forward Expectations, Underwriter Delta, Portfolio Court Delta, and Risk Delta run in parallel post-Verifier
- ✓ Orchestrator consolidates findings and compares each candidate's Daily Anchor conviction to Delta conviction
- ✓ Changed candidates only in output (no unchanged holdings listed)
- ✓ Price denominator explicitly stated with source (never impersonates full Anchor rerun)
- ✓ Handoff emissions emitted for material conviction shifts using DEDUP_KEY rule
- ✓ Master Ledger event paste-ready or `NO LOG REQUIRED` stated
- ✓ Full Delta Map wikilinks all 4 specialist files from this run (traversable in Obsidian)

---

## Design Spec Integration

This runbook implements the full design specification at [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md]]:

- **§1 Mission:** Validates Daily Anchor convictions intraday, reports only material changes (±5% price or fundamental news)
- **§3 Architecture:** Agent sequence matches spec (Verifier → 4 parallel → Orchestrator)
- **§4 Price-Move Threshold:** ±5% trigger implemented in Verifier and all downstream agents
- **§5 Delta Detection Logic:** Included/excluded candidate logic implemented per design
- **§6 Output Format:** File naming and structure match design spec exactly
- **§7 Failure Handling:** BLOCKED, DEGRADED, FAILED states per design
- **§8 Handoff Protocol Integration:** Handoff format and DEDUP_KEY rule per design
- **§9 Master Ledger Integration:** Logging control and event template per design
- **§10 Constraints:** Constitutional Laws (§3) and execution discipline rules per design
- **§11 Acceptance Criteria:** All 11 criteria implemented in acceptance checklist above

---

## Relationship to Daily Anchor

Post-Open Delta Check is a **lightweight intraday validation** of Daily Anchor, not a full rerun:

- **Prerequisite:** Must have same-day completed Daily Anchor output
- **Scope:** Changed candidates only (±5% move or fundamental news)
- **Agent subset:** Uses 5 of 9 agents (no Discovery, Industry, Red Team)
- **Output:** Changed candidates table + handoff emissions for conviction shifts
- **Execution:** No trades, no sizing, no autonomous decisions
- **Escalation path:** If material conviction shifts detected, triggers Emergency Thesis Rerun or next scheduled Daily Anchor

---

## Reference Links

- Design Specification: [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design]]
- Verifier (Delta Check) Agent: [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier (Delta Check)]]
- Forward Expectations Agent: [[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]
- Underwriter (Delta Check) Agent: [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter (Delta Check)]]
- Portfolio Court (Delta Check) Agent: [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court (Delta Check)]]
- Risk and Survivability (Delta Check) Agent: [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability (Delta Check)]]
- Master Ledger: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Active Handoff Snapshot: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Operator Manual: [[00_START_HERE/CAOS — OPERATOR MANUAL]]
- Daily Anchor Runbook: [[06_PRODUCT_RUNBOOKS/Daily Anchor]]
