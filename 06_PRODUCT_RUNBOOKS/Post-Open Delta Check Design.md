# Post-Open Delta Check — Design Specification

**Product:** CAOS Post-Open Delta Check  
**Status:** DESIGN APPROVED  
**Date:** 2026-08-31  

---

## 1. Mission

Post-Open Delta Check validates Daily Anchor convictions intraday. It runs only after a same-day Daily Anchor completes, compares current market state to Anchor's established baseline, and reports only material changes (price ±5% or fundamental news/earnings). It is never a full rerun and cannot run independently.

---

## 2. Core Requirements

**When it runs:**
- Only after same-day Daily Anchor completes and writes its output file
- Ad hoc intraday, never scheduled independently
- Command: `Run CAOS Post-Open Delta Check`

**What it checks:**
- Candidates with price movement ±5% or more from Daily Anchor denominator
- Candidates with fundamental changes (earnings surprise, guidance revision, news, contract award, regulatory event, analyst call)
- All funded holdings (CORE/ATTACKER positions) automatically included
- All SEED and CHALLENGER candidates automatically included
- WATCH WITH SPECIFIC TRIGGER positions if trigger event occurred

**What it outputs:**
- Changed candidates only (no noise on unchanged positions)
- One-line thesis verdict per changed ticker (thesis intact, degraded, confirmed, new conviction, etc.)
- Brief action implication (hold, review, escalate)
- Master Ledger event if material conviction shifts
- Explicit price denominator and source (never impersonate full Anchor)

**What it skips:**
- No independent discovery of new candidates intraday
- No full re-underwriting unless conviction changed materially
- No autonomous trades or sizing
- No leverage, margin, or Kelly claims

---

## 3. Architecture

### Agent Sequence

```
Verifier (fetch current prices, establish new denominator)
   |
Forward Expectations
Underwriter
Portfolio Court
Risk & Survivability
   (all parallel — depend only on Verifier output)
   |
Orchestrator (main session — consolidate delta, compare to Anchor, emit verdict)
```

**Why this subset:**
- **Verifier:** Establishes current price denominator (e.g., "14:30 CET intraday" vs "18:15 CET Anchor close")
- **Forward Expectations:** Detects earnings surprises, guidance changes, analyst revisions on affected tickers
- **Underwriter:** Re-checks thesis validity with new prices and forward data for changed candidates
- **Portfolio Court:** Re-validates funded-holding thesis under new prices
- **Risk & Survivability:** Recalculates survival scores for moved positions
- **Orchestrator:** Consolidates findings, compares each candidate's Anchor verdict to updated verdict, proposes handoffs and Master Ledger event

**Why NOT:**
- Discovery: no new companies discovered intraday
- Industry Read-through: structure unchanged intraday
- Red Team: (optional; include only if delta logic integrity check needed)

### Data Flow

1. Claude reads Daily Anchor output from same session (`ORCHESTRATOR_YYYY-MM-DD_*.md`)
2. Verifier fetches current prices; identifies candidates with ±5% price move or fundamental news
3. Forward Expectations screens changed candidates for earnings/guidance/analyst changes
4. Underwriter re-checks thesis on changed candidates (short version, not full Monster File)
5. Portfolio Court re-validates thesis for changed funded holdings
6. Risk recalculates survival for moved candidates
7. Orchestrator consolidates: for each changed candidate, compares Daily Anchor conviction to Delta conviction, flags shifts

### Integration Points

**Prerequisites:**
- Daily Anchor must have completed same-day (blocks if missing)
- Master Ledger must be INITIALIZED and current (blocks if stale per Operator Manual §4)

**Outputs consumed by:**
- Active Handoff Snapshot (new handoffs if conviction shifts)
- Master Ledger (logging of material changes)
- Weekly Ranking (handoff feed for next cycle)
- Emergency Thesis Rerun (if escalation needed)

**File linking:**
- Delta Check file opens with "Inputs Consulted" section, wikilinks Daily Anchor baseline
- Obsidian "Linked mentions" shows downstream consumers (Weekly Ranking, etc.)

---

## 4. Price-Move Threshold

**Trigger threshold:** ±5% price movement from Daily Anchor denominator price

This captures intraday moves meaningful enough to re-examine thesis assumptions (momentum alone insufficient; structural change signal required).

---

## 5. Delta Detection Logic

### Candidates Included (checked for delta)

**Always:**
- All CORE/ATTACKER funded holdings (survivability may shift)
- All SEED and CHALLENGER candidates (thesis at risk)
- WATCH WITH SPECIFIC TRIGGER positions if trigger event occurred

**If conditions met:**
- Any candidate with ±5%+ price move
- Any candidate with fundamental change detected (news, earnings, guidance, contract, regulatory, analyst)

### Candidates Excluded (no re-check)

- REJECT holdings (terminal, no thesis to re-validate)
- Unchanged holdings (no price move, no news)
- SERIOUS REVIEW / HIGH-PRIORITY positions that moved but no conviction change expected

---

## 6. Output Format and File Structure

**File naming:**  
`03_AGENT_RUNS/09_ORCHESTRATOR/POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md`

**File structure:**

```
# CAOS — Post-Open Delta Check
Date: YYYY-MM-DD HH:mm CET
Baseline: Daily Anchor completed YYYY-MM-DD 18:15 CET
Current: Intraday prices as of HH:mm CET
Price denominator: [specific source, e.g., "Bloomberg 14:30 CET European close"]

## Inputs Consulted
- [[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_...]]
- [Verifier price stamp]
- [Forward Expectations findings]
- [Underwriter thesis updates]
- [Portfolio Court review]
- [Risk & Survivability recalculation]

## Delta Summary
**[No material changes detected]** or **[N] candidates with thesis changes**

### Changed Candidates
| Ticker | Price Δ % | Change Type | Baseline Conviction | Updated Conviction | Thesis Verdict | Action |
|--------|-----------|---|---|---|---|---|
| AVGO | +3.2% | Price only | SEED | SEED | Thesis intact, survival 70% confirmed | Hold |
| CEG | -6.5% | Price + earnings news | WATCH | WATCH | Survival dropped to 65%, PPA trigger timeline extended | Review full Anchor before re-entry |
| ASML | +1.2% | Price only | CHALLENGER | CHALLENGER | Thesis intact, backlog confirmed solid | Hold |

## Orchestrator Verdict
[1–2 sentence summary: which positions remain valid, which need deep re-analysis, portfolio thesis impact]

Example: "Three candidates moved intraday; all theses remain intact. CEG's survival assumption shifted but trigger remains valid. No escalation needed before next scheduled Anchor."

## Handoff Emissions
[If material conviction shifts, emit handoff blocks per Operator Manual §9]

Example:
```
HANDOFF_ID = 20260831-DAILY-CEG-CONVICTION_SHIFT
ORIGIN_MODULE = DAILY
HANDOFF_TYPE = CANDIDATE_STATE
NEW_STATE = WATCH (survival 65%, trigger timeline extended)
PREVIOUS_STATE = WATCH (survival 75%, trigger Q3 2026)
EVIDENCE_QUALITY = MEDIUM (earnings guidance, intraday move)
NEXT_GATE = earnings call transcript review, next Anchor re-check
```

## Master Ledger Event
[Paste-ready event block if material changes warrant logging; include candidate shifts, thesis impacts, survival changes]

Or: **NO LOG REQUIRED** (if all theses intact and no conviction shifts)
```

**Key output principles:**
- Changed candidates only (no unchanged holdings listed)
- One-line verdicts, scannable format
- Explicit price source and denominator (never impersonate full Anchor rerun)
- Handoff emissions for conviction shifts
- Paste-ready Master Ledger event or explicit `NO LOG REQUIRED`

---

## 7. Failure Handling

**Blocked conditions (cannot run):**

- **`DELTA CHECK BLOCKED — NO SAME-DAY ANCHOR`**  
  Daily Anchor output not found for today. Cannot establish baseline for comparison.

- **`DELTA CHECK BLOCKED — STALE MASTER LEDGER`**  
  Master Ledger status is UNINITIALIZED or stale (per Operator Manual §4). Portfolio state unknown; cannot re-validate thesis for funded holdings.

**Degraded conditions (can continue with caveats):**

- **`DATA LIMITED — price source unavailable [TICKER1, TICKER2]`**  
  Verifier unable to fetch current prices for specific tickers; state which ones. Resume with available data for other candidates.

- **`NO MATERIAL DELTAS`**  
  No candidates moved ±5% or had fundamental changes. Output: "All theses intact. Daily Anchor convictions confirmed. NO LOG REQUIRED."

**Hard constraints (per Operator Manual §12):**
- No autonomous trades
- No buy sizing without live price and confirmed real cash
- No margin or leverage
- No Kelly claims
- No hallucinated prices, news, or earnings data (Verifier must cite sources)

---

## 8. Handoff Protocol Integration

**When to emit handoff:**
- Material conviction shift (SEED→CHALLENGER, CHALLENGER→WATCH, WATCH→REJECT, etc.)
- Significant survivability change (>10 percentage points)
- Thesis-core assumption invalidated (e.g., "PPA timeline moved out 1+ quarters")

**Handoff format (Operator Manual §9):**
```
HANDOFF_ID = YYYYMMDD-DAILY-TICKER-CHANGE_TYPE
ORIGIN_MODULE = DAILY
ORIGIN_DATE = YYYY-MM-DD
HANDOFF_TYPE = CANDIDATE_STATE
DEDUP_KEY = SOURCE|TICKER|DELTA_CHECK|DATE
PREVIOUS_STATE = [Daily Anchor conviction]
NEW_STATE = [Updated conviction]
EVIDENCE_QUALITY = HIGH | MEDIUM | LOW | DATA LIMITED
NEXT_GATE = [specific metric, filing, or date]
REQUIRED_CONSUMERS = WEEKLY, CENSUS, HUNTER (as relevant)
ACTIVE_UNTIL = [expiration date if gated]
```

**DEDUP rule:**  
SOURCE|TICKER|DELTA_CHECK|DATE — avoids duplicate handoffs from same day's delta check on same ticker.

---

## 9. Master Ledger Integration

**Logging control (Operator Manual §10):**
- Default: human-confirmed (Mark pastes block after review)
- If material conviction shifts: output `LOG REQUIRED` with paste-ready event block
- If all theses intact: output `NO LOG REQUIRED`

**Event template:**
```
EVENT_TYPE = CANDIDATE_CONVICTION_DELTA
MODULE = DAILY (subproduct of Daily Anchor)
TIMESTAMP_LOCAL = [intraday time of check]

VERIFIED EVIDENCE
- [Verifier price stamp, source]
- [Forward Expectations news, earnings, guidance updates]
- [Underwriter thesis re-check findings]
- [Portfolio Court funded-holding re-validation]
- [Risk recalculation]

CAOS INTERPRETATION
- Which theses remain intact, which shifted
- Why (price move, news, earnings surprise, etc.)
- Conviction direction and magnitude of shift

SURVIVABILITY / FINANCING / DILUTION
- Any survival assumption changes
- Financing or dilution impact from price move or news

ACTIONABILITY
- Which positions can hold as-is
- Which need escalation (full Anchor re-run, Emergency Rerun, etc.)
- Any immediate action implications

NEXT PROOF GATE
- [Next daily Anchor, or specific trigger]
```

---

## 10. Constraints and Execution Rules

**CAOS Constitutional Laws (Operator Manual §3) apply:**
1. Reality First — verified news/prices only
2. Radical Honesty — state `DATA LIMITED` or `UNKNOWN` if data missing
3. Fresh-Evidence Supremacy — current prices override Anchor prices if moved
4. Objective Supremacy — no incumbent holding protection
5. Survivability Before Optionality — reject moved positions with degraded survival
6. No autonomous trading (ever)

**Execution discipline:**
- Never claim a price or earnings fact without citing source
- Never assume a fill or trade
- Never claim "thesis intact" without visible evidence
- Never hide degraded linkage or stale data

---

## 11. Acceptance Criteria

- ✓ Product can read Daily Anchor output from same session
- ✓ Verifier successfully fetches current prices and establishes new denominator
- ✓ Forward Expectations, Underwriter, Portfolio Court, Risk run in parallel post-Verifier
- ✓ Orchestrator consolidates findings and compares to Anchor baseline
- ✓ Changed candidates only in output (no noise)
- ✓ Price denominator explicitly stated (never impersonates full Anchor)
- ✓ Handoff emissions emit for conviction shifts with dedup key
- ✓ Master Ledger event paste-ready or `NO LOG REQUIRED` stated
- ✓ File links to Daily Anchor via "Inputs Consulted" (Obsidian traversable)
- ✓ Failure states explicitly named (no silent failures)
- ✓ No trades, no sizing, no autonomous execution
- ✓ All evidence labeled and sourced

---

## 12. Success Metrics

- **Accuracy:** Changed candidates match Anchor baseline (no false positives)
- **Timeliness:** Completes within 5–10 minutes (lightweight)
- **Actionability:** Verdict is immediately clear to Mark (hold, review, escalate)
- **Integrity:** No hallucinated prices, news, or earnings; all sources cited
- **Integration:** Handoffs flow into Active Handoff Snapshot; Master Ledger event logging works

---

## 13. Relationship to Other Products

| Product | Relationship |
|---------|---|
| Daily Anchor | **Prerequisite.** Post-Open Delta Check runs only after Anchor completes same-day. |
| Weekly Ranking | **Downstream consumer.** Reads Delta Check handoffs for candidate state updates. |
| Emergency Thesis Rerun | **Escalation path.** If Delta Check flags major thesis shift, triggers Emergency Rerun. |
| Monster Census | **Peer product.** Both consume Daily Anchor handoffs; both feed Weekly Ranking. |
| Master Ledger | **Logging destination.** Delta events logged if material conviction changes. |
| Active Handoff Snapshot | **State pipeline.** Delta Check emits handoffs; Weekly Ranking consumes them. |

