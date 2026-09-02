# Weekly Ranking — Design Specification

**Product:** CAOS Weekly Ranking  
**Status:** DESIGN APPROVED  
**Date:** 2026-09-01  

---

## 1. Mission

Weekly Ranking consolidates all discoverable candidates and funded holdings into a unified ranking universe, re-underwriting each with fresh evidence and current prices. It ranks by both raw asymmetry and evidence/survivability-adjusted conviction, runs head-to-head comparisons against portfolio anchors and cash, audits system health (stale gates, orphans, contradictions, handoffs), and confirms execution readiness for the next capital-deployment decision. It runs weekly on a fixed schedule and on-demand.

---

## 2. Core Requirements

**When it runs:**
- Scheduled: Sunday 10:00 in Mark's confirmed timezone
- On-demand: any time via `Run CAOS Weekly Ranking` command
- Dependencies: Most recent Daily Anchor (price baseline), Monster Census output (candidate universe), Active Handoff Snapshot, Master Ledger

**What it outputs:**
- Two ranking tables (raw-asymmetry and evidence/survivability-adjusted)
- Head-to-head fight verdicts (brief, in main output)
- System audit section (stale gates, orphans, contradictions, unresolved handoffs)
- Execution readiness gate (EXECUTION READY or EXECUTION BLOCKED)
- Supporting detailed-analysis document with full fight comparisons
- Handoff emissions for any conviction state changes
- Master Ledger event (LOG REQUIRED or NO LOG REQUIRED)

**What it skips:**
- No autonomous execution or sizing (that's DCA Execution Card's role)
- No legal/tax/trust recommendations (monthly Family-Wealth check only flags whether professional review is warranted)
- No amendment of Constitutional Laws or system rules (flags for Mark's consideration only)

---

## 3. Architecture

### Agent Sequence

Weekly Ranking runs all 9 agents from the Daily Anchor roster, on the full candidate universe (holdings + funded Seeds + buy-authorized Seeds + Challengers + serious candidates + cash):

```
Verifier (current prices across all candidates)
   |
Discovery -- Forward Expectations -- Industry Read-through   (parallel)
   \                |                    /
                Underwriter (re-validates all candidates + holdings)
                /         \
      Portfolio Court   Risk & Survivability                 (parallel)
                \         /
                 Red Team (optional depth check)
                    |
               Orchestrator (produces unified ranking + audits + gates)
```

**Key characteristics:**
- Serial chain: each agent waits on its named predecessor's output
- Portfolio Court and Risk & Survivability run in parallel (both read Underwriter output, not each other's)
- All 9 agents re-run every Weekly cycle
- Orchestrator consolidates into unified ranking, not separate discovery verdicts

### Data Flow

1. Orchestrator reads Daily Anchor baseline (latest prices, candidate universe, prior convictions)
2. Orchestrator reads Monster Census output (discovered candidates, holdings list)
3. Orchestrator reads Active Handoff Snapshot (current state of all candidates)
4. Orchestrator reads Master Ledger (historical decisions, gates, convictions)
5. Verifier fetches current prices; establishes new weekly denominator
6. Discovery searches for new high-asymmetry candidates (same 9 lanes as Daily Anchor)
7. Forward Expectations detects earnings surprises, guidance changes, analyst revisions
8. Industry Read-through re-assesses structural changes in represented sectors
9. Underwriter re-validates thesis for every funded holding + all candidates in universe
10. Portfolio Court re-validates thesis for funded holdings only (CORE/ATTACKER)
11. Risk & Survivability recalculates survival scores for all candidates
12. Red Team (optional) stress-tests ranking assumptions
13. Orchestrator consolidates findings into unified ranking universe

### Integration Points

**Prerequisites:**
- Daily Anchor must have run within 7 days (used as price check baseline)
- Monster Census must have run within 30 days (used as candidate universe)
- Master Ledger and Active Handoff Snapshot must be readable (per Operator Manual §4, research-only mode if stale)

**Outputs consumed by:**
- DCA Execution Card (ranking tables, execution readiness gate)
- Active Handoff Snapshot (new handoffs for conviction shifts)
- Master Ledger (logging of material changes)
- Event Gate Watch (if handoffs trigger external event checks)

**File linking:**
- Weekly Ranking file opens with "Inputs Consulted" section, wikilinking Daily Anchor, Monster Census, Master Ledger, Active Handoff Snapshot
- Obsidian "Linked mentions" shows downstream consumers (DCA Execution Card, etc.)

---

## 4. Ranking Logic — Two Separate Tables

Weekly Ranking produces two side-by-side ranking tables for the same candidate universe. Each candidate appears in both tables, ranked differently:

### Table 1: Raw-Asymmetry Ranking

**Sort by:** upside/downside ratio (expected CAGR assuming thesis holds)  
**Metric:** pure return asymmetry, no adjustment for evidence quality or survivability  
**Purpose:** "If I believed every thesis equally, which has best asymmetry?"

Example: a high-conviction holding with 3x upside might rank #2; a speculative, high-asymmetry company might rank #1.

**Columns:**
| Rank | Ticker | Company | Upside | Downside | Asymmetry Ratio | Baseline Conviction |
|------|--------|---------|--------|----------|-----------------|-------------------|

### Table 2: Evidence/Survivability-Adjusted Ranking

**Sort by:** risk-adjusted conviction (asymmetry × evidence-quality-grade × survivability-score)  
**Metric:** "Which candidates have the strongest evidence AND realistic survival path?"  
**Purpose:** "Which should actually get next euro, accounting for thesis maturity and business durability?"

Example: the #1 raw-asymmetry play drops to #5 if evidence is weak or survivability is <50%.

**Columns:**
| Rank | Ticker | Company | Asymmetry Ratio | Evidence Grade | Survival % | Adj. Score | Updated Conviction |
|------|--------|---------|-----------------|-----------------|-----------|-----------|-------------------|

**Key principle:** Both tables show all candidates (holdings, Seeds, Challengers, serious candidates, cash). No candidate is hidden; both tables are fully transparent and comparable.

---

## 5. Head-to-Head Fight Format

### Brief Format (Main Output)

Weekly Ranking includes five mandatory head-to-head comparisons in the main output. Each is one or two lines, scannable:

```
HEAD-TO-HEAD FIGHTS

vs. Portfolio Champion [ticker of highest-conviction funded holding]:
  [Top challenger by adjusted ranking] shows [asymmetry comparison],
  BUT current [CORE/ATTACKER] position holds because [reason: lower volatility | proven execution | lower dilution risk].

vs. Quality Anchor [highest-ranked funded Seed]:
  [Top Seed in ranking] is [even/stronger/weaker] — asymmetry [X]% vs [Y]%, evidence [grade comparison].

vs. Strongest Seed:
  [Top Seed by raw asymmetry] has [asymmetry]% upside but [survival]% survival vs [current strongest Seed].

vs. Strongest Challenger:
  [Top Challenger by adjusted rank] edges [Top Challenger by raw asymmetry] on evidence quality [detail].

vs. Cash:
  Minimum edge: [risk-free rate + X]%. Candidates clearing it: [count and tickers]. Below threshold: [count].
```

### Detailed Format (Supporting Document)

File: `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_RANKINGS_DETAIL.md`

For each head-to-head fight, include full analysis:
- Thesis strength comparison (company thesis vs. security thesis vs. portfolio fit for each combatant)
- Evidence quality breakdown (what makes case strong/weak)
- Survivability path for each (financing, dilution, execution risk)
- Sizing implications (if deployed, what weight for each?)
- Key unknowns and next gates

---

## 6. System Audit Section

Weekly Ranking includes a mandatory audit section that flags system health issues:

### 6.1 Stale Gates Audit

For every WATCH WITH SPECIFIC TRIGGER and SERIOUS REVIEW candidate:
- Check if trigger event has occurred
- Check if gate deadline has passed
- State: "Gate still open, next trigger date: X" or "GATE EXPIRED — requires decision"
- Flag any gate older than 90 days without evidence of re-evaluation

**Output format:** One line per candidate:
```
[TICKER] | [STATE] | Gate status: [trigger event / deadline date] | [INFO | WARNING]
```

### 6.2 Orphan Positions Audit

Identify any position with <1.5% of NAV that lacks an explicit Seed/Catalyst role:
- Flag for decision: "This position exists but has no assigned thesis role — is it intentional?"

**Output format:**
```
[TICKER] | [%NAV] | NO ASSIGNED ROLE | [WARNING]
```

### 6.3 Contradictions Audit

Check for internal inconsistencies:
- A CORE holding with survival score <40% (violates Operator Manual §6)
- A holding listed as both REJECT and CHALLENGER
- A candidate with conflicting handoff states (two active handoffs saying opposite things)

**Output format:**
```
[TICKER] | [CONTRADICTION TYPE] | Details: [what conflicts] | [CRITICAL]
```

### 6.4 Unresolved Handoffs Audit

Read Active Handoff Snapshot for every active handoff touching candidates in Weekly Ranking universe:
- State whether each was "ACKNOWLEDGED AND APPLIED" or "LINKAGE DEGRADED / UNAVAILABLE"
- Flag any handoff active >30 days without resolution or explicit extension

**Output format:**
```
HANDOFF ACK CHECK: [HANDOFF_ID] | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO
```

---

## 7. Monthly Special Tasks (First Weekly Run of Each Calendar Month)

On the first Weekly Ranking run of each calendar month, add three additional checks:

### 7.1 Architecture Maintenance

- **Portfolio baseline:** confirm holdings count, NAV source, cash state vs. Master Ledger
- **Candidate registry:** are all SEED/CHALLENGER/WATCH candidates tracked? Any forgotten?
- **Stale gates audit:** explicit monthly refresh of §6.1
- **Task health:** verify all scheduled products ran on time (Daily Anchor, Monster Census, Event Gate Watch, Weekly Ranking itself)
- **Notification health:** confirm Weekly Ranking delivered on time last week
- **Prompt contradictions:** check if any Operator Manual §3 Constitutional Laws or system rules have drifted or contradicted each other
- **Handoff linkage:** verify Active Handoff Snapshot is being read/written correctly by all products
- **Duplicate/supersession logic:** confirm no duplicate active handoffs for same ticker/signal
- **Ledger-worthy changes:** flag if any system rule amendments or major process changes need Master Ledger events
- **Unresolved lessons:** check Flight Recorder (once Learning Review is built) for open learning items that still need action

**Output:** One section titled "Architecture Maintenance" with subsections for each check. Each finding is one line.

### 7.2 Manual Deep Audit Reminder

Output one passive line:
```
Deep Audit reminder: Type `Run CAOS Deep Audit` to perform monthly full re-underwriting and ledger audit.
```

This is a reminder only — Weekly Ranking does not run Deep Audit autonomously.

### 7.3 Family-Wealth Architecture Check

Determine only whether portfolio/family scale, legal/tax changes (e.g., marriage, inheritance, tax residency shift), or expected benefits (e.g., startup exit, bonus timing) justify dedicated professional review.

**Output one of:**
```
FAMILY WEALTH ARCHITECTURE: NO ACTION NEEDED — next check [date/event]
```
OR
```
FAMILY WEALTH ARCHITECTURE: RECOMMEND PROFESSIONAL REVIEW
Reason: [reason — portfolio scale | tax residency change | inheritance | other]
Next trigger: [date/event]
```

**Constraints:**
- Never autonomously recommend trusts, companies, tax structures, or legal action
- Never execute legal/tax decisions
- This is a flag only; Mark decides whether to act

---

## 8. Handoff Protocol Integration

### When to emit handoff:
- Candidate state change (SEED → CHALLENGER, CHALLENGER → WATCH, WATCH → REJECT, etc.)
- Significant survivability shift (>10 percentage points)
- Major evidence quality shift (LOW → HIGH, or HIGH → DATA LIMITED)
- Thesis re-evaluation (company thesis strengthens but security thesis weakens)

### Handoff format (Operator Manual §9):
```
HANDOFF_ID = YYYYMMDD-WEEKLY-TICKER-STATE_CHANGE
ORIGIN_MODULE = WEEKLY
ORIGIN_DATE = YYYY-MM-DD
HANDOFF_TYPE = CANDIDATE_STATE
PREVIOUS_STATE = [prior conviction]
NEW_STATE = [updated conviction]
EVIDENCE_QUALITY = HIGH | MEDIUM | LOW | DATA LIMITED
NEXT_GATE = [specific metric, catalyst, or date]
REQUIRED_CONSUMERS = HUNTER | CENSUS | EVENT_GATE (as relevant)
ACTIVE_UNTIL = [expiration date if gated]
MANDATORY_DEEP_UNDERWRITING = YES | NO
```

### Handoff ACK Check (Operator Manual §9):
Weekly Ranking reads Active Handoff Snapshot and, for every active handoff touching a candidate in its universe, output:
```
HANDOFF ACK CHECK: HANDOFF_ID | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO | RESOLVES_HANDOFF_ID
```

If expected handoff is unavailable, state: `LINKAGE DEGRADED / HANDOFF UNAVAILABLE` — never hallucinate receipt.

---

## 9. Master Ledger Integration

### Logging control (Operator Manual §10):
- Default: human-confirmed (Mark pastes block after review, replies `logged`)
- If material conviction shifts: output `LOG REQUIRED` with paste-ready event block
- If all theses hold and no state changes: output `NO LOG REQUIRED`

### Event template (when LOG REQUIRED):
```
============================================================
CAOS EVENT
============================================================
EVENT_ID = YYYY-MM-DD-WEEKLY-SUBJECT-CHANGE
EVENT_TYPE = CANDIDATE_CONVICTION_WEEKLY_RANKING
MODULE = WEEKLY
TIMESTAMP_LOCAL = [run time]

SOURCE_AND_PORTFOLIO_STATE
- [Weekly Ranking date/time]
- Price denominator: [source, time]
- Holdings reconciled against: [broker source, time]

PREVIOUS_STATE
- [Prior convictions from Daily Anchor or Monster Census]

NEW_STATE
- [Updated convictions after Weekly re-underwriting]

VERIFIED EVIDENCE
- [Verifier price data with sources]
- [Forward Expectations: earnings, guidance, analyst updates]
- [Underwriter re-check: thesis-core assumption changes]
- [Portfolio Court: funded-holding thesis validation]
- [Risk: survivability recalculation]

CAOS INTERPRETATION
- Which theses remain intact, which shifted
- Why (price move, evidence quality, survivability, etc.)
- Conviction direction and magnitude of shifts

SURVIVABILITY / FINANCING / DILUTION
- Survival assumption changes
- Financing or dilution impact from new evidence

ACTIONABILITY
- Which positions can hold as-is
- Which need escalation (Emergency Rerun, Deep Audit, etc.)
- Any immediate portfolio action implications

NEXT PROOF GATE
- [Next Weekly Ranking, or specific catalyst]

============================================================
END CAOS EVENT
============================================================
```

---

## 10. Execution Readiness and DCA Gate

Weekly Ranking does NOT create an execution card. Instead, it confirms four gate conditions before DCA Execution Card can proceed:

### Gate Preconditions:

1. **Portfolio Gate:** Master Ledger is current, holdings are reconciled, cash is verified (per Operator Manual §4)
2. **Price Gate:** All candidates have current verified prices (not older than 2 hours for liquid, 1 business day for illiquid)
3. **Ranking Gate:** Top 3 candidates in adjusted-ranking table are ranked and conviction is stated
4. **Handoff Gate:** All active handoffs touching potential execution targets have been acknowledged (RECEIVED=YES)

### Gate Output:

If all gates pass:
```
EXECUTION READY — proceed to DCA Execution Card
```

If any gate fails:
```
EXECUTION BLOCKED — reason: [specific gate] — retry after [condition met]
```

### Relationship to DCA Execution Card:

- Weekly Ranking produces ranking universe and confirms gates pass
- DCA Execution Card (separate product) reads Weekly Ranking output and ranking tables
- DCA Card selects one target (or two max) from top-ranked candidates
- DCA Card handles sizing, cash reconciliation, execution details
- If Weekly Ranking produces `EXECUTION BLOCKED`, DCA Card states that reason and does not proceed

---

## 11. Constraints and Execution Rules

**CAOS Constitutional Laws (Operator Manual §3) apply:**
1. Reality First — verified prices/evidence only
2. Radical Honesty — state DATA LIMITED or UNKNOWN if data missing
3. Fresh-Evidence Supremacy — current prices override prior convictions if moved
4. Objective Supremacy — no incumbent holding protection
5. Survivability Before Optionality — reject moved positions with degraded survival
6. No autonomous trading (ever)

**Execution discipline:**
- Never claim a price or earnings fact without citing source
- Never assume a fill or trade
- Never claim "thesis intact" without visible evidence
- Never hide degraded linkage or stale data
- Never duplicate prior Anchor findings without stating "no change since [date]"

---

## 12. Acceptance Criteria

13 criteria in total:

- ✓ Product can read Daily Anchor, Monster Census, Master Ledger, and Active Handoff Snapshot
- ✓ All 9 agents (Verifier → Discovery → Forward → Industry → Underwriter → Portfolio Court/Risk → Red Team → Orchestrator) run in the serial chain defined in §3, each waiting on its named predecessor
- ✓ Orchestrator consolidates findings into unified ranking universe (both holdings and new candidates)
- ✓ Two ranking tables produced: raw-asymmetry and evidence/survivability-adjusted, showing all candidates in both
- ✓ Head-to-head fights: brief format in main output (1-2 lines per fight), detailed format in supporting document
- ✓ System audit section: stale gates, orphans, contradictions, unresolved handoffs (§6)
- ✓ Monthly tasks run on first Weekly run of calendar month: Architecture Maintenance, Deep Audit reminder, Family-Wealth check
- ✓ Handoff emissions for conviction state changes with dedup key and ACK check (§8)
- ✓ Master Ledger event paste-ready or NO LOG REQUIRED stated (§9)
- ✓ File links to Daily Anchor, Monster Census, Master Ledger, Active Handoff via "Inputs Consulted" (Obsidian traversable)
- ✓ Execution readiness gate: EXECUTION READY or EXECUTION BLOCKED (§10)
- ✓ Failure states explicitly named (no silent failures)
- ✓ All evidence labeled and sourced (no hallucinated prices/earnings)

---

## 13. Success Metrics

- **Accuracy:** Ranking matches re-underwritten convictions (no stale data)
- **Completeness:** All candidates ranked, no missing positions, handoffs acknowledged
- **Timeliness:** Completes within 20–30 minutes (all 9 agents + consolidation + audit)
- **Actionability:** Ranking is immediately clear (top 3 candidates obvious, next-euro decision enabled)
- **Integrity:** No hallucinated prices, earnings, or evidence; all sources cited
- **Integration:** Handoffs flow into Active Handoff Snapshot; DCA Execution Card can proceed if gates pass

---

## 14. Relationship to Other Products

| Product | Relationship |
|---------|---|
| Daily Anchor | **Prerequisite input.** Weekly Ranking reads most recent Anchor (price baseline, candidate universe, convictions). |
| Monster Census | **Prerequisite input.** Weekly Ranking reads Census output (discovered candidates, holdings list). |
| Post-Open Delta Check | **Peer product.** Both consume Daily Anchor handoffs; both feed into Weekly Ranking's universe. |
| DCA Execution Card | **Downstream consumer.** Reads Weekly Ranking output, ranking tables, execution readiness gate. Selects execution target. |
| Emergency Thesis Rerun | **Escalation destination.** If Weekly Ranking flags major thesis shift, can trigger Emergency Rerun. |
| Deep Audit | **Monthly trigger.** Weekly Ranking reminds Mark to run Deep Audit on first run of each month. |
| Learning Review | **Post-Audit consumer.** Learning Review reads Flight Recorder and prior Weekly Rankings. |
| Master Ledger | **Logging destination.** Weekly Ranking events logged if material conviction changes. |
| Active Handoff Snapshot | **State pipeline.** Weekly Ranking emits handoffs; downstream products consume them. |
| Event Gate Watch | **Handoff consumer.** Receives handoffs from Weekly Ranking if event triggers. |
| Multi-Bagger Hunter Watch | **Peer product.** Both rank candidates; Hunter focuses on discovery, Weekly focuses on ranking. |

---

## 15. File Structure and Naming

**Main output:**  
`03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm.md`

**Supporting detailed-comparison document:**  
`03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_HHmm_RANKINGS_DETAIL.md`

**Main output contents:**
- Inputs Consulted
- Two ranking tables (raw-asymmetry, evidence/survivability-adjusted)
- Head-to-head fights (brief format)
- System audit section (stale gates, orphans, contradictions, unresolved handoffs)
- Handoff ACK checks
- Execution readiness gate
- Master Ledger event (LOG REQUIRED or NO LOG REQUIRED)

**Supporting document contents:**
- Detailed head-to-head fight comparisons (thesis strength, evidence quality, survivability, sizing implications, key unknowns)
- Evidence quality breakdowns per candidate
- Survivability recalculation details

---

## 16. Constraints and Out of Scope

**NOT included:**
- Execution sizing (that's DCA Execution Card's job)
- Autonomous trades or assumed fills (ever)
- Legal/tax advice (only flags whether professional review warranted)
- System rule amendments (only flags for Mark's consideration)
- Margin or leverage (never)
- Kelly sizing claims (unless Mark explicitly authorizes an audited module)

---

