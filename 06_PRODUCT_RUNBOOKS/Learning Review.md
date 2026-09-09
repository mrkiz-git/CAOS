# CAOS — Learning Review

**Command:** `Run CAOS Learning Review`  
**Status:** READY FOR EXECUTION  
**Default schedule:** Manual; recommended monthly (after Deep Audit + Flight Recorder entry review)

---

## What This Product Does

A monthly retrospective that assesses what CAOS got right, wrong, and why. Reads the Master Ledger history, Flight Recorder, and prior Orchestrator outputs to grade decisions, evidence quality, processes, and system health drift.

**Does NOT do:** Re-underwrite holdings, re-rank candidates, or make new portfolio decisions.

**Does do:** 
- Assess prediction accuracy (gates that resolved, theses that held/broke, calls that were right/wrong)
- Distinguish good process / bad outcome from bad process / good outcome
- Grade evidence quality and identify missed information
- Detect system drift (too institutional, too concentrated, too speculative, etc.)
- Propose system improvements (and get Mark's approval before implementing)
- Maintain institutional learning (what we've learned this cycle)

**Key outputs:**
- Right calls (with evidence and process quality)
- Wrong calls (distinguished by cause: bad process vs. good process/bad luck)
- System health assessment (drift indicators)
- Recommended changes (proposals for Mark approval)
- Historical learning entry for future reference

---

## Precondition Checks

**Before starting, verify:**

1. **Deep Audit completed**
   - Read [[06_PRODUCT_RUNBOOKS/Deep Audit]] for current build status
   - At least one monthly Deep Audit must have been completed and marked approved by Mark
   - If no Deep Audit exists yet, state `LEARNING REVIEW BLOCKED — no Deep Audit entry to review` and **STOP**

2. **Flight Recorder entry exists and reviewed**
   - Read [[04_FLIGHT_RECORDER/README — Flight Recorder]]
   - At least one monthly Flight Recorder entry must exist (created after Deep Audit review)
   - If no Flight Recorder entry exists, state `LEARNING REVIEW BLOCKED — no Flight Recorder entry yet` and **STOP**

3. **Master Ledger history readable**
   - Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] §8 (Material CAOS EVENT History)
   - Should show all major decisions from at least the past month

4. **Prior Orchestrator outputs linked**
   - Recent Daily Anchor, Weekly Ranking, Monster Census outputs should be accessible via Active Handoff Snapshot links

---

## The 5 Mandatory Work Items and Who Produces Them

| Item | Producer | Output |
|------|----------|--------|
| **1. Period scope & data gathering** | Orchestrator (primary session) | Define review period (e.g., "2026-08-01 to 2026-09-02"), gather all CAOS EVENT logs, Flight Recorder, Orchestrator outputs |
| **2. Prediction assessment** | Orchestrator (primary session) | Which gates resolved? Which theses held? Which calls were right/wrong with evidence? |
| **3. Process audit** | Orchestrator (primary session) | Good-process/bad-outcome cases distinguished from bad-process cases; evidence quality graded |
| **4. System health drift** | Orchestrator (primary session) | Is CAOS drifting: institutional/conservative/speculative/concentrated without edge/diversified without purpose? |
| **5. Change proposals** | Orchestrator (primary session) | Proposed amendments to mandate, rules, or operating procedures (for Mark's approval only) |

---

## Agent Execution Sequence

**No agents called by default.** This is a synthesis-only product. Read existing documents:

```
Master Ledger (§8 history)
    |
Flight Recorder (recent entries)
    |
Prior Daily Anchor, Weekly Ranking, Monster Census outputs
    |
Active Handoff Snapshot (resolved gates, evidence outcome)
    |
Orchestrator (primary session) synthesizes findings
    |
If specific fact-check needed:
    (optional) Call Agent tool for one targeted verification
```

---

## Execution Procedure

### Step 1: Gather Data (primary session)

Read and document:

1. **Master Ledger §8 (CAOS EVENT History)**
   - All events logged in the review period (e.g., past month)
   - Note decision dates, reasons, and outcomes
   - Check for any unresolved events or missing logs

2. **Flight Recorder (recent entries)**
   - Read [[04_FLIGHT_RECORDER/README — Flight Recorder]] for monthly summaries
   - Note holdings, weights, thesis summary, key decisions for the review period

3. **Prior Orchestrator outputs**
   - Daily Anchor outputs (daily verdicts, thesis re-checks)
   - Weekly Ranking outputs (re-ranked universe, system audits)
   - Monster Census outputs (new discovery, conversion scoreboard)
   - Read dates, verdicts, and any noted drift or contradictions

4. **Active Handoff Snapshot**
   - Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
   - Note event gates that RESOLVED, triggered, or still pending
   - Check for any handoffs that lapsed without being resolved

### Step 2: Assess Predictions & Calls

For each significant decision or prediction in the review period:

**Right Calls (with evidence):**
- Decision: [what was predicted or decided]
- Evidence: [what was the basis]
- Outcome: [what actually happened]
- Process quality: [was the process sound? were assumptions validated?]
- Example: "Predicted NVIDIA data center demand would sustain — earnings confirmed 15% YoY Blackwell revenue growth."

**Wrong Calls (with process diagnosis):**
- Decision: [what was predicted or decided]
- Evidence: [what was the basis]
- Outcome: [what actually happened instead]
- Process quality:
  - **Good process, bad outcome:** Evidence was solid, reasoning was sound, but market/company diverged (luck)
    - Example: "IREN thesis was sound (data center power demand), but Bitcoin price collapse cut revenue forecasts by 40% (external shock, not thesis failure)"
  - **Bad process:** Evidence was weak, reasoning was flawed, or misses were ignored
    - Example: "TSLA chip guidance underestimated Dojo adoption rate — didn't read latest guidance carefully enough"

**False Positives & False Negatives:**
- False positive: Escalated a candidate that turned out weak (wasted underwriting effort)
- False negative: Missed a candidate that later proved compelling (missed opportunity)

### Step 3: Audit Evidence Quality

For the review period, assess:

- **Evidence gaps:** Were there things we should have known but didn't?
  - Missed a guidance update? Overlooked a competitor move? Didn't read a filing?
- **Evidence misinterpretation:** Did we mislabel evidence confidence?
  - Treated a DATA LIMITED item as VERIFIED FACT?
  - Relied on secondary reporting instead of primary sources?
- **Stale gates:** Are there evidence gates still open >90 days without new evidence?
  - Example: "IREN profitability gate dated 2026-06-15; we're now 2026-09-02 with no update"

### Step 4: Detect System Drift

Assess whether CAOS is drifting in any of these dimensions:

| Dimension | Drift Signal | Evidence Required |
|-----------|---|---|
| **Too institutional** | Holdings all large-cap, no asymmetry, indistinguishable from S&P 500 | Compare current holdings to Russell 1000; check median market cap vs. prior year |
| **Too conservative** | Rejecting promising candidates due to survival scores >50% or overstated risk | Count rejected candidates with >60% survival; read rejection reasoning |
| **Too speculative** | Chasing momentum, low-conviction Seed positions, ignoring valuation | Count Seed positions; note their thesis quality; check entry valuations |
| **Concentrated without edge** | Heavy positions (>5% each) in similar themes with no clear thesis differentiation | Tally weights; check thesis overlap; note opportunity cost |
| **Diversified without purpose** | Many small (<1%) positions with no clear rationale for why they coexist | Count positions <1.5%; note justification for each; are they orphans? |

For each dimension, grade: DRIFT DETECTED with evidence, or NONE OBSERVED.

### Step 5: Propose System Changes

If evidence suggests the system should change:

**Proposed amendment format:**

```
AMENDMENT_TITLE = [brief name]
CATEGORY = [CONSTITUTIONAL LAW / OPERATING RULE / MANDATE / PROCEDURE]
CURRENT_STATE = [what's in place now]
PROPOSED_CHANGE = [what should change]
RATIONALE = [evidence from review period]
IMPACT = [what would improve, what might be affected]
IMPLEMENTATION = [how would this change be implemented]
MARK_DECISION_REQUIRED = YES [never self-implement; always ask Mark]
```

**Examples:**
- "Increase minimum survival threshold for Seeds from 60% to 65% (too many failed to deliver)"
- "Add mandatory re-check after every CEO change in funded holdings (missed 3 thesis shifts)"
- "Reduce Monthly Contribution from €300 to €100 (discovery quality suffering from underfunding)"

---

## Primary Session Output

**File:** `03_AGENT_RUNS/09_ORCHESTRATOR/LEARNING_REVIEW_YYYY-MM-DD.md`

**Contents:**

```
# CAOS Learning Review

Review Period: [start date] to [end date]
Reviewed by: [Orchestrator, primary session]

Inputs Consulted:
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] §8 (EVENT history)
- [[04_FLIGHT_RECORDER/README — Flight Recorder]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [list of prior Orchestrator outputs reviewed: Daily Anchor, Weekly Ranking, Monster Census]

---

## RIGHT CALLS (with evidence and process quality)

[List decisions that panned out as predicted]

Example format:
- **NVIDIA data center demand thesis:** Predicted Blackwell revenue growth 10–15% YoY.
  - Evidence: Analyst consensus, NVIDIA guidance, customer commentary.
  - Outcome: +15% actual YoY growth in Blackwell (official 10-Q).
  - Process: SOUND — thesis was validated, assumptions held.
  - Implication: Connected holdings (IREN, WULF) thesis remains intact.

[2–5 right calls with this format]

---

## WRONG CALLS (with diagnosis)

### Good Process, Bad Outcome (external shock, not thesis failure)

[Decisions that were well-reasoned but lost to external events]

Example:
- **IREN profitability gate:** Predicted profitability by Q2 2026 (based on rising Bitcoin prices).
  - Evidence: Historical correlation between Bitcoin and data center power demand.
  - Outcome: Bitcoin crashed 40% in Q3 2026; IREN guided below break-even.
  - Process: SOUND — evidence was current, reasoning was solid.
  - Verdict: Not a process failure; external market shock. Thesis remains valid if Bitcoin recovers.

### Bad Process (evidence missed, misread, or ignored)

[Decisions where the process failed — missed information, weak reasoning, or misread evidence]

Example:
- **TSLA chip autonomy thesis:** Underestimated time-to-revenue; didn't catch updated guidance.
  - Evidence: Read analyst consensus, not official 10-Q.
  - Outcome: Guidance pushed autonomy revenue 2–3 years further out than expected.
  - Process: WEAK — should have read official guidance, not secondhand.
  - Verdict: Process improvement needed (always read official filings for timing updates).

### False Positives & False Negatives

[Candidates escalated that flopped; candidates missed that succeeded]

---

## SYSTEM HEALTH DRIFT ASSESSMENT

### Institutional Drift
- Signal: [holdings all large-cap / median market cap / % Russell 1000]
- Evidence: [current holdings vs. prior year]
- Verdict: [DRIFT / NONE OBSERVED]

### Conservatism Drift
- Signal: [rejection rate / average survival threshold used]
- Evidence: [count rejected candidates with >60% survival; read reasoning]
- Verdict: [DRIFT / NONE OBSERVED]

### Speculation Drift
- Signal: [Seed count / conviction quality / entry valuations]
- Evidence: [% portfolio in Seeds; avg Seed thesis grade; valuation analysis]
- Verdict: [DRIFT / NONE OBSERVED]

### Concentration Drift
- Signal: [portfolio Herfindahl index / top 3 position weights]
- Evidence: [weights; thesis overlap; opportunity cost]
- Verdict: [DRIFT / NONE OBSERVED]

### Diversification Drift
- Signal: [count of <1.5% positions; orphan assessment]
- Evidence: [position list; justification for each micro-position]
- Verdict: [DRIFT / NONE OBSERVED]

---

## STALE GATES & UNCLOSED INVESTIGATIONS

[Any evidence gates still open >90 days without new evidence?]

Example:
- Gate: "IREN profitability Q2 2026"
- Status: Now 2026-09-02; Q2 is past; new gate needed or position should be escalated
- Recommendation: Update gate to "Next profitable quarter" or exit position if thesis failed

---

## EVIDENCE QUALITY AUDIT

### Missed Information
- [Any guidance, filings, or market events we should have caught?]
- Example: "Missed CEO commentary in earnings call on Blackwell ramp timing"

### Misinterpreted Evidence
- [Any VERIFIED FACT labeled that was actually DATA LIMITED?]
- Example: "Treated sell-side consensus as VERIFIED — should have verified against official guidance"

### Source Gaps
- [Any positions where we lack primary source evidence?]
- Example: "Private startup; cannot verify financials or competitive position"

---

## RECOMMENDED SYSTEM AMENDMENTS

[Each as a proposal for Mark's approval — never self-implemented]

### Amendment 1: [title]
- Category: [CONSTITUTIONAL LAW / OPERATING RULE / MANDATE / PROCEDURE]
- Current state: [what's in place]
- Proposed change: [what should change]
- Rationale: [evidence from review period]
- Impact: [benefits and costs]
- Mark Decision: [APPROVED / REJECTED / PENDING]

[0–3 amendments based on evidence]

---

## LEARNING POINTS & INSTITUTIONAL KNOWLEDGE

[What did we learn this cycle that should shape future decisions?]

Example:
- "CEO changes are major thesis inflection points; add mandatory re-check within 1 week of announcement"
- "Guidance timing updates are buried in call transcripts; always read official 10-Q before trusting analyst consensus"
- "Data center power cost drives IREN valuation; track Bitcoin and macro electricity rates as leading indicators"

---

## NEXT MONTH'S FOCUS

[Based on drift, missed information, and approved amendments, what should we focus on?]

Example:
- Reduce Institutional Drift: Allocate next €300 contribution to early-stage discovery
- Tighten Evidence Quality: Always verify guidance from official filings, not analyst consensus
- Monitor IREN: Bitcoin recovery thesis remains valid; set €X price target for re-entry if needed

---

## Master Ledger Event

[If Mark approves any amendment:]

LOG REQUIRED [with paste-ready event block, each amendment as separate event] OR NO LOG REQUIRED
```

---

## Optional: Agent Call for Fact-Check

If a specific claim needs verification (e.g., "Did that earnings call actually say X?"), call the Agent tool **once** with a targeted prompt:

```
Verify this specific claim: [claim description]
Date: [when the event should have occurred]
Source: [where we think it came from]
Look for: [exact quote or data point to verify]
Expected source: [SEC filing, press release, earnings transcript, etc.]
```

Do NOT call the full 9-agent pipeline; this is a single targeted check only.

---

## Execution Rules

From Operator Manual §3:
- **Process Over Outcome.** Judge decisions by process quality, not luck.
- **Radical Honesty.** State what we got wrong and why; don't sugarcoat.
- **Never implement amendments without Mark's approval.** Proposals only until Mark confirms.
- **Distinguish good process / bad outcome from bad process.** The two require different responses.

---

## Success Criteria (Acceptance Checklist)

- ✓ Deep Audit entry exists and reviewed
- ✓ Flight Recorder entry exists for review period
- ✓ Master Ledger §8 history read and summarized
- ✓ Right calls identified with evidence (≥2)
- ✓ Wrong calls identified and diagnosed (good process vs. bad process distinguished)
- ✓ False positives and false negatives assessed
- ✓ Evidence quality audit completed (gaps, misinterpretations noted)
- ✓ System health drift assessed on all dimensions
- ✓ Stale gates identified and addressed
- ✓ Recommended amendments proposed (with rationale) — not yet implemented
- ✓ Learning points identified for future reference
- ✓ File named `LEARNING_REVIEW_YYYY-MM-DD.md` created
- ✓ Master Ledger event proposed ONLY if Mark approves amendment (not before)

---

## Failure States and Recovery

**LEARNING REVIEW BLOCKED — Missing preconditions**
- No Deep Audit entry completed yet → cannot review yet
- No Flight Recorder entry yet → cannot review yet
- Master Ledger or Flight Recorder unreadable → state what's missing
- **Recovery:** Complete required prerequisite, then retry

**LEARNING REVIEW DEGRADED — Limited data**
- `DATA LIMITED — only 1 Deep Audit/Flight Recorder entry; limited history to review`
- **Proceed:** Review with noted limitation (first review will be shorter)

---

## Integration with Master Ledger

Learning Review does NOT directly modify the Master Ledger. Amendments must be approved by Mark first:

1. Orchestrator proposes amendments in the Learning Review output
2. Mark reviews and replies with approval/rejection
3. For each approved amendment, Orchestrator creates a separate Master Ledger CAOS EVENT (§3 System Amendment)
4. Only then is the amendment logged and binding

---

## Design Specification and Details

Full learning-review procedures: [[06_PRODUCT_RUNBOOKS/Learning Review Design.md]] (to be created)

Covers:
- Prediction accuracy grading methodology
- Good process vs. bad process diagnosis framework
- System drift detection thresholds
- Amendment documentation standards
- Historical learning archival

---

## Dry-Run Test Plan

Test procedures and scenarios: `04_FLIGHT_RECORDER/Learning Review Dry-Run Test.md` (to be created)

Covers three scenarios: Happy Path (good learning, no amendments), Process Failure (bad-process wrong call, amendment proposed), System Drift Detected (conservatism drift flagged, allocation adjustment recommended).

---
