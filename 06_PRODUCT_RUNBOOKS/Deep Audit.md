# CAOS — Deep Audit

**Command:** `Run CAOS Deep Audit`  
**Status:** READY FOR EXECUTION  
**Default schedule:** Manual only; recommended monthly (first trading day or after significant market event)

---

## What This Product Does

A complete portfolio re-underwrite that treats every holding as if you were liquidating to 100% cash today and deciding what to buy back. This breaks incumbency bias and tests every position (funded holding, Seed, Challenger) against the full universe of alternatives.

**Key outputs:**
- **Next-Euro Capital Map:** Every funded position, Seed, Challenger, and top fresh candidates ranked by next-capital allocation priority
- **INCLUDE/RESIZE/REPLACE/EXIT verdicts:** For each position, should you buy it fresh at current price, reduce size, swap it for an alternative, or exit entirely?
- **Ledger Self-Audit:** Master Ledger tested for missing logs, contradictions, stale timestamps, broken supersession chains, unresolved handoffs
- **Incumbency Bias Check:** Red Team findings on whether holdings are anchored on sunk cost rather than current evidence
- **Capital map:** Proposed allocation for next €300/month and any tactical rebalancing
- **System recommendations:** Proposed changes to mandate, rules, or operating procedures (if any)

---

## Precondition Checks

**Before calling any agent, verify:**

1. **Master Ledger MUST be initialized**
   - Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
   - If status is `UNINITIALIZED`, state `DEEP AUDIT BLOCKED — Portfolio state unknown, cannot re-audit` and **STOP**
   - Deep Audit has no degraded mode; it either audits real holdings or it doesn't

2. **Broker State Current** — Verifier will verify fresh prices/cash position
   - Prepare most recent broker screenshot/export to share during run
   - If broker state is >7 days stale, Verifier will flag; audit continues in DEGRADED mode

3. **Master Ledger History Complete**
   - Check that §8 (Material CAOS EVENT History) has all major decisions logged
   - If significant gaps, note them before run begins (may surface as findings in audit)

---

## The 6 Mandatory Work Items and Who Produces Them

| Item | Producer | Output |
|------|----------|--------|
| **1. Fresh price data & broker state** | Verifier | Prices for all holdings and top candidates; cash position; buying power distinction; timestamp |
| **2. Universe re-discovery from scratch** | Discovery | ≥40 companies across ≥3 lanes, including top candidates and every funded holding; fresh evidence on each |
| **3. Forward guidance re-check** | Forward Expectations | All holdings + top candidates: guidance, earnings surprises, analyst changes, thesis catalysts since last audit |
| **4. Sector and market regime assessment** | Industry Read-through | Structural shifts, competitive changes, macro conditions affecting all holdings and top candidates |
| **5. 100%-cash frame re-underwriting** | Underwriter | Fresh Monster File for every funded holding (testing inclusion, size, conviction); consolidated universe ranking |
| **6. Portfolio rebuild from scratch** | Portfolio Court & Risk | If cash today, what would you buy? Capital map from zero, then compare to current. Sizing implications, exit candidates |
| **7. Incumbency bias audit** | Red Team | Holdings kept purely due to sunk cost? Evidence of anchoring bias? Recommended rebalancing |
| **8. Ledger self-audit** | Orchestrator | Master Ledger tested against broker state and audit findings; repairs proposed; system drift assessed |

---

## Agent Execution Sequence

```
Broker State Check
    |
Verifier (fresh prices, cash state)
    |
Discovery -- Forward Expectations -- Industry Read-through       (parallel)
    \                |                    /
                Underwriter (100%-cash frame Monster Files)
                /         \
      Portfolio Court    Risk & Survivability                 (parallel)
      (rebuild from      (100%-cash survival
       zero)             scores for all)
                \         /
                Red Team (incumbency bias, anchoring)
                    |
          Orchestrator + Ledger Self-Audit (main session)
```

Timeline: Steps 1–3 (parallel), Step 4 (serial), Steps 5–6 (parallel), Step 7 (serial), Step 8 (primary session).

---

## Agent Call Sequence

### Step 1: Call Verifier (Deep Audit)

Use the invocation prompt template from [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]]:

```
You are the CAOS Verifier (Deep Audit). Read your full role spec at
03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md and follow it exactly.

THIS IS A DEEP AUDIT. Verify current broker state (portfolio, holdings, cash, 
buying power), all security prices (holdings + top 10 candidates), market status, 
and evidence hierarchy. This audit will use fresh broker state to test 
compliance with the Master Ledger.

Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].
Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]].

Write output to: 03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_DEEPAUDIT.md

Required output:
- Current broker portfolio (holdings, shares, prices)
- Cash (real cash vs. buying power)
- Price table for all holdings + top 10 candidates (timestamp, source)
- Comparison: broker state vs. Master Ledger last recorded state
- Any discrepancies (holdings in Ledger but not in broker, or vice versa)
- Verdict: DATA QUALITY = PASS / DEGRADED / BLOCKED
```

**Output to verify:**
- Broker holdings table with current prices and quantities
- Reconciliation against Master Ledger (Item 2 of Ledger §2)
- Discrepancy report (if any)
- Evidence quality verdict

### Step 2: Call Discovery, Forward Expectations, Industry (parallel)

Call the Agent tool **three times in the same turn:**

**Discovery (Deep Audit):**
```
You are Discovery (Deep Audit). Read your full role spec at
03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md and follow it exactly.

THIS IS A DEEP AUDIT. Treat this as a fresh discovery run: do NOT pre-assume 
any current holding is justified. Search ≥40 public companies across ≥3 lanes.
Include: all funded holdings (treat them as candidates), all active Seeds/Challengers,
and ≥10 fresh names not in the current Master Ledger Candidate Registry.

For each funded holding: what's the current thesis? Has it changed since purchase?
Is it still conviction-worthy at current price?

Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].
Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]].

Write output to: 03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_YYYY-MM-DD_DEEPAUDIT.md
```

**Forward Expectations (Deep Audit):**
```
You are Forward Expectations (Deep Audit). Read your full role spec at
03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md and follow it exactly.

THIS IS A DEEP AUDIT. Re-check forward guidance for: all funded holdings, 
all active Seeds/Challengers, top 10 fresh candidates. Look for:
- Guidance updates, misses, or guidance withdrawals since last audit
- Earnings surprises
- Analyst rating changes
- Macro catalyst shifts

For each holding: has forward guidance or market consensus changed since you bought?

Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/03_FORWARD/FORWARD_YYYY-MM-DD_DEEPAUDIT.md
```

**Industry Read-through (Deep Audit):**
```
You are Industry Read-through (Deep Audit). Read your full role spec at
03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md and follow it exactly.

THIS IS A DEEP AUDIT. Assess structural shifts in sectors where you have funded holdings.
Look for:
- Competitive changes (new entrants, consolidation, market share shifts)
- Regulatory or macro regime changes
- Technology disruptions affecting the thesis
- Financing environment changes

For each sector with a holding: has the structural case changed since you bought?

Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_YYYY-MM-DD_DEEPAUDIT.md
```

**Outputs to verify:**
- Discovery: ≥40 companies scanned, all holdings re-assessed, ≥10 fresh names
- Forward: Forward guidance re-check on all holdings and candidates
- Industry: Structural assessment on sectors with funded positions

### Step 3: Call Underwriter (Deep Audit)

```
You are the Underwriter (Deep Audit). Read your full role spec at
03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md and follow it exactly.

THIS IS A DEEP AUDIT. Produce fresh Monster Files for EVERY FUNDED HOLDING 
(not just new candidates). For each holding, test:
- Inclusion: would you buy this company fresh at current price?
- Sizing: if you bought it fresh, what % of portfolio?
- Conviction: given current evidence, is conviction higher, same, or lower than at purchase?
- Replacement risk: is there a better alternative in the current universe?

Also produce Monster Files for top 5 fresh candidates (highest asymmetry, >50% survival).

Read Discovery, Forward Expectations, and Industry outputs.
Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_YYYY-MM-DD_DEEPAUDIT.md

Required output:
- Monster File for each funded holding (thesis verdict: INCLUDE / RESIZE / REPLACE / EXIT)
- Monster File for each top-5 fresh candidate
- Consolidated ranking of all candidates and holdings, 100%-cash frame
- Survival score for each security
- Proof gates for all non-core positions
```

**Output to verify:**
- Monster File for each funded holding with explicit INCLUDE/RESIZE/REPLACE/EXIT verdict
- Survival scores all ≥40% (WATCH minimum threshold)
- Consolidated ranking table

### Step 4: Call Portfolio Court & Risk and Survivability (parallel)

**Portfolio Court (Deep Audit):**
```
You are Portfolio Court (Deep Audit). Read your full role spec at
03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md and follow it exactly.

THIS IS A DEEP AUDIT. Build a capital map from 100% cash: where would you invest €9,334 
and future €300/month contributions today, given current evidence?

Then compare to current portfolio:
- Which current holdings would you buy back? At what weight?
- Which would you reduce or exit?
- How does optimal allocation differ from current?
- What is the capital recycling verdict (sell X, buy Y)?

Read Underwriter output (consolidatedranking).
Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/06_PORTFOLIO_COURT/PORTFOLIO_COURT_YYYY-MM-DD_DEEPAUDIT.md

Required output:
- Optimal capital map (100% cash frame)
- Current portfolio capital map
- Difference table (exit candidates, resize candidates, buy fresh candidates)
- Next-euro allocation: where does €300/month go?
- Rebalancing recommendation: any immediate trades?
```

**Risk and Survivability (Deep Audit):**
```
You are Risk and Survivability (Deep Audit). Read your full role spec at
03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md and follow it exactly.

THIS IS A DEEP AUDIT. Recalculate survival score for every security under current 
prices and forward guidance. Test hard thresholds:
- All CORE/ATTACKER holdings: ≥40% (no hard floor, but note below 50%)
- All SEED positions: ≥60%
- All CHALLENGER positions: ≥50%
- All WATCH positions: ≥40%

Flag any breach. For any holding with survival <50%, is it a REPLACE candidate?

Read Underwriter output.
Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_YYYY-MM-DD_DEEPAUDIT.md

Required output:
- Survival score table: all securities with current survival % and threshold
- Breach report: any positions below assigned threshold
- Financing risk, dilution risk, execution risk for all core holdings
- Verdict on each position: PASS / PASS WITH MONITORING / BREACH
```

**Outputs to verify:**
- Portfolio Court: Next-euro capital map with exit/resize/buy verdicts
- Risk: Survival scores and threshold compliance; breach report

### Step 5: Call Red Team (Deep Audit)

```
You are Red Team (Deep Audit). Read your full role spec at
03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md and follow it exactly.

THIS IS A DEEP AUDIT. Stress-test the rebuilt portfolio specifically for 
INCUMBENCY BIAS: are holdings kept because the current evidence is compelling, 
or only because we already own them?

For each funded holding:
- Remove sunk cost: pretend you never bought it. Would you buy it today?
- Test conviction drift: has conviction changed since purchase? Why?
- Find hidden anchors: is any thesis held despite new contradictory evidence?

Scenario stress-tests:
- What if asymmetry -50%? Portfolio still optimal?
- What if survival -20pp? Any holdings flip to BREACH?
- What if market regime shifts (rising rates, recession, sector rotation)? Thesis holds?

Read Portfolio Court and Risk outputs.
Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]].

Write output to: 03_AGENT_RUNS/08_RED_TEAM/RED_TEAM_YYYY-MM-DD_DEEPAUDIT.md

Required output:
- Incumbency bias assessment: PASS / FINDINGS (which holdings are sunk-cost anchored?)
- Conviction drift analysis: for each holding, conviction vs. purchase time
- Stress-test results: portfolio robustness under 3–5 scenarios
- Verdict: HOLDS SURVIVE / AUDIT RECOMMENDS REBALANCING
```

**Output to verify:**
- Incumbency bias findings (which positions appear anchored?)
- Stress-test results
- Rebalancing recommendation

### Step 6: Perform Orchestrator Role + Ledger Self-Audit (primary session)

**Do not spawn a subagent.** Read all agent outputs (Verifier through Red Team), Master Ledger, and Active Handoff Snapshot. Produce:

**File 1: Main Deep Audit Output**
```
03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_DEEPAUDIT.md

Contents:
1. Inputs Consulted (wikilinks to all 6 agents, Master Ledger, Active Handoff)
2. Executive Summary
   - DEEP AUDIT VERDICT: [one paragraph: portfolio is [HEALTHY / NEEDS REBALANCING / CRITICAL ISSUES], reason]
3. Broker Reconciliation
   - Verifier's broker state vs. Master Ledger §2 (Current Portfolio Snapshot)
   - Any discrepancies noted
4. Next-Euro Capital Map
   - Table: Security | Current Position | Current Weight | Verdict | Recommended Weight | Action
   - Every funded holding + top candidates
   - Verdicts: INCLUDE / RESIZE UP / RESIZE DOWN / REPLACE / EXIT
5. Incumbency Bias Check
   - Red Team findings: any holdings appear sunk-cost anchored?
   - Conviction drift: which positions show conviction change vs. purchase?
6. Survival Threshold Compliance
   - Risk table: all positions with survival % and threshold
   - Breach report: any breaches?
7. Recommended Next Steps
   - Immediate rebalancing trades (if any)
   - New candidates for seeding
   - Positions to monitor or re-evaluate
8. System Audit Findings (see step 7 below)
9. Handoff Emissions
   - New handoff blocks for any candidate state changes or evidence gates
10. Master Ledger Event Proposal or NO LOG REQUIRED
```

**Step 7: Ledger Self-Audit** (same step as Orchestrator)

Test [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] against audit findings:

1. **§1 Current Mandate** — Does investor profile match? Leverage prohibition still valid? Update needed?
2. **§2 Current Portfolio Snapshot** — Reconcile against Verifier's broker state. Any holdings missing? Phantom positions?
3. **§3 Real Cash vs. Buying Power** — Correct per Verifier? Contribution status current?
4. **§4 Funded-Security Roles** — Do assigned roles (CORE/ATTACKER) still match Underwriter's verdict? Any REPLACE candidates?
5. **§5 Candidate / Status Registry** — Any candidates with stale state? Evidence gates still valid? Contradictions in prior handoffs?
6. **§6 Active Evidence Gates** — Any gates dated >90 days without resolution?
7. **§7 Standardized Handoff Index** — Link to Active Handoff Snapshot; are there unresolved handoffs >30 days old?
8. **§8 Material CAOS EVENT History** — Any major decisions missing from log? Any contradictions between logged events and current state?
9. **§9–§10 Notes & Amendments** — Any system rule changes needed?

If repairs needed:
- Produce a "LEDGER REPAIR BLOCK" with format:
  ```
  REPAIR_ID = YYYY-MM-DD-SECTION-FINDING
  SECTION = [§1, §2, etc.]
  CURRENT_CONTENT = [what's in the Ledger now]
  PROPOSED_CONTENT = [what should be there instead]
  WHY = [evidence for the repair]
  SUPERSEDES = [prior event ID if this corrects a logged decision]
  ```
- Present the repair block in the Orchestrator output
- **Wait for Mark's reply `logged` before treating repair as applied**

---

## Linking Rule Application

**All agent output files** must open with "Inputs Consulted" section:

**Each agent (Verifier, Discovery, Forward, Industry, Underwriter, Portfolio Court, Risk, Red Team):**
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Wikilink: any prior agent output it reads (e.g., Underwriter reads Discovery, Forward, Industry)

**Orchestrator output:**
- Wikilink all 6 agent files
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]

---

## Execution Rules

From Operator Manual §3:
- **100%-cash frame, no anchoring:** "We already own it" is never sufficient justification
- **No autonomous trading:** INCLUDE/RESIZE/REPLACE/EXIT verdicts are recommendations only
- **Ledger append-only:** Never silently rewrite history; every correction states what was wrong and what prior event it supersedes
- **Radical Honesty:** State UNKNOWN, DATA LIMITED, or UNVERIFIED rather than guessing
- **Fresh evidence supremacy:** New broker state, new guidance, new market conditions override prior audit conclusions

---

## Success Criteria (Acceptance Checklist)

- ✓ Master Ledger initialized (or audit blocked and stated)
- ✓ All 6 agents run and outputs written
- ✓ Broker state reconciled against Master Ledger §2
- ✓ ≥40 companies in discovery universe, including all funded holdings
- ✓ Forward guidance and sector assessment completed for all holdings
- ✓ Every funded holding has a fresh Monster File with INCLUDE/RESIZE/REPLACE/EXIT verdict
- ✓ Top 5 fresh candidates underwritten with Monster Files
- ✓ Portfolio rebuild from 100% cash complete; next-euro capital map produced
- ✓ Survival scores recalculated; threshold breaches identified
- ✓ Red Team incumbency bias assessment completed
- ✓ Ledger self-audit performed; repairs proposed (if any)
- ✓ All agent outputs linked in Orchestrator "Inputs Consulted"
- ✓ DEEP AUDIT VERDICT statement clear: HEALTHY / NEEDS REBALANCING / CRITICAL
- ✓ NEXT-EURO CAPITAL MAP table with all positions and verdicts
- ✓ LOG REQUIRED (with event + repair blocks) or NO LOG REQUIRED stated
- ✓ File named `ORCHESTRATOR_YYYY-MM-DD_DEEPAUDIT.md` created

---

## Failure States and Recovery

**DEEP AUDIT BLOCKED — Cannot proceed**
- Master Ledger UNINITIALIZED → no portfolio to audit; state reason and stop
- Broker state unavailable → Verifier cannot reconcile; state reason and stop
- **Recovery:** Initialize Master Ledger or provide broker state, then retry

**DEEP AUDIT DEGRADED — Limited data but can audit**
- `DATA LIMITED — broker state >7 days stale, using prices from Verifier read`
- `DATA LIMITED — one agent failed mid-run (e.g., Discovery incomplete)`
- **Recovery:** Proceed with noted limitations; rerun next month with fresh data

**DEEP AUDIT INCOMPLETE — Agent failure mid-run**
- [Agent] failed or produced unreadable output → do not attempt to synthesize results
- **Recovery:** Fix the failing agent, rerun; do not present partial audit as complete

---

## After Deep Audit: Flight Recorder Entry

Once Mark has reviewed Deep Audit findings and approved any rebalancing, the orchestrator creates a Flight Recorder entry (see [[04_FLIGHT_RECORDER/README — Flight Recorder]]):

- Entry date: the day of audit run
- Summary: DEEP AUDIT PASS / NEEDS REBALANCING / CRITICAL FINDINGS
- Key verdicts: capital reallocation decisions approved
- System health: any drift noted (institutional/conservative/speculative/concentrated)

**Do NOT create a Flight Recorder entry before Mark's review and approval.**

---

## Design Specification and Details

Full deep-audit procedures: [[06_PRODUCT_RUNBOOKS/Deep Audit Design.md]] (to be created)

Covers:
- 100%-cash frame mechanics (how to isolate sunk cost)
- Incumbency bias assessment methodology
- Ledger audit checklist (detailed per-section procedures)
- Repair documentation standards
- Capital map rebuilding logic

---

## Dry-Run Test Plan

Test procedures and scenarios: `04_FLIGHT_RECORDER/Deep Audit Dry-Run Test.md` (to be created)

Covers three scenarios: Happy Path (all agents complete, no repairs), Ledger Drift (repairs needed), and Breach Scenario (multiple holdings below survival threshold).
