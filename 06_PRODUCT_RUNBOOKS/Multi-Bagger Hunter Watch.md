# CAOS — Multi-Bagger Hunter Watch

**Command:** `Run CAOS Multi-Bagger Hunter Watch`  
**Status:** READY FOR EXECUTION  
**Default schedule:** Manual; recommended daily (or as-needed based on source availability)

---

## What This Product Does

Scans external high-conviction stock-picking sources for new or materially changed recommendations. For each new signal found, independently verifies the underlying company evidence against primary sources (SEC filings, IR, earnings calls). Resolves each qualified signal to a candidate state (REJECT / WATCH WITH TRIGGER / CHALLENGER / HIGH-PRIORITY CHALLENGER) and emits handoffs for new escalations.

**Key principle:** External sources are scouts, never authority. A Motley Fool recommendation is a prompt to research, not a buy signal. Independent verification is mandatory before any escalation.

**Key outputs:**
- New signals identified from watched sources
- Independent verification status for each (VERIFIED / UNVERIFIED LEAD / REJECTED)
- Candidate state assignment (REJECT / WATCH / CHALLENGER / HIGH-PRIORITY CHALLENGER)
- Deduplication (no signal is re-escalated if already tracked in Active Handoff Snapshot)
- Handoff emissions for any new escalations

---

## Precondition Checks

**Before starting, verify:**

1. **Active Handoff Snapshot "Active Hunter Signals" section**
   - Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
   - Note existing signals and their dedup keys: `SOURCE + TICKER + SIGNAL_DATE`
   - Used to prevent duplicate escalations

2. **Watched sources accessible**
   - Motley Fool, Seeking Alpha, IBD, TipRanks, and other sources should be reachable
   - If all sources are down/blocked, state `HUNTER WATCH DEGRADED — no sources reachable`

---

## The 3 Mandatory Work Items and Who Produces Them

| Item | Producer | Output |
|------|----------|--------|
| **1. New signal scan** | Hunter Agent | All new recommendations from watched sources (since last check or last signal logged) |
| **2. Independent verification** | Hunter Agent | For each signal: company thesis, financials, growth, market position verified against SEC filings, IR, official reporting |
| **3. State resolution & handoff emission** | Orchestrator (primary session) | Each qualified signal resolved to REJECT / WATCH / CHALLENGER / HIGH-PRIORITY CHALLENGER; handoffs emitted for escalations |

---

## Agent Execution Sequence

```
Read Active Handoff Snapshot "Active Hunter Signals"
    |
Call Hunter Agent:
    - Scan watched sources for new/changed signals
    - Deduplicate against prior signals (DEDUP_KEY = SOURCE+TICKER+SIGNAL_DATE)
    - For each new signal: independently verify company evidence
    - Label: VERIFIED / UNVERIFIED LEAD / REJECTED
    |
Orchestrator role (primary session):
    - Review verified signals
    - Resolve to candidate state
    - Emit handoffs, propose Master Ledger event
```

No parallel dependencies; Hunter Agent → Orchestrator sequential.

---

## Agent Call Sequence

### Step 1: Call Hunter Agent

**Call the Agent tool with this prompt template:**

```
You are Hunter Watch (CAOS). Scan external stock-picking sources for new 
high-conviction signals. Independent verification is mandatory before escalation.

Sources to scan (when accessible):
- Motley Fool Stock Advisor, Rule Breakers, Hidden Gems
- Seeking Alpha Alpha Picks, Quant Screeners (Momentum, Growth, Value)
- IBD 50, IBD Stock of the Day (when materially new or changed)
- TipRanks Elite Analysts (top 5% by accuracy), new initiations or strong reiteration
- Other sources Mark has authorized: [add as needed]

Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]].
Check "Active Hunter Signals" section to see what's already tracked.

Deduplication rule: use dedup key `SOURCE | TICKER | SIGNAL_DATE` to avoid re-escalating 
the same signal. If an existing signal reappears with no material change, state 
"NO NEW MATERIAL — already tracked" and move on.

For EACH new or materially changed signal:
1. Identify: Ticker | Company | Source | Signal Date | Recommendation
2. Independentverification (DO NOT accept scout source claim at face value):
   - Read company's latest 10-K/10-Q filing (SEC EDGAR)
   - Check latest quarterly earnings (official press release, not analyst notes)
   - Verify market cap, business model, revenue, growth rate, profitability (if any)
   - Check competitive position: who are 3 main competitors? What's company's differentiation?
   - Assess valuation: EV/Revenue, EV/EBITDA, P/E vs. peers and historical ranges
   - Identify key risks: execution, competition, macro, financing, dilution
3. Label evidence: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN
4. Verdict: Is the underlying thesis sound? Do you have confidence in the signal?

Output file: 03_AGENT_RUNS/02_DISCOVERY/HUNTER_YYYY-MM-DD_HHmm.md

Format:
- Inputs Consulted: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]], [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Sources Scanned: [list source, scan date, whether new signals found]
- New Signals Table:
  | Ticker | Company | Source | Signal Date | Recommendation | Verification | Thesis Summary | Evidence Quality | Verdict |
- Prior Signal Re-check (optional): any tracked signals with new material? Note here.
- Summary: [N new signals found / NO NEW SIGNALS / DEGRADED — see failures section]

Rules:
- NEVER accept a scout recommendation as authority; verify independently
- NEVER use pre-release analyst estimates for verification; use actual released data only
- NEVER hallucinate company financials or competitive position
- State UNKNOWN if data is unavailable; do not invent
- If thesis lacks independent verification, signal = UNVERIFIED LEAD (don't escalate past WATCH)
```

**Output to verify:**
- File: `03_AGENT_RUNS/02_DISCOVERY/HUNTER_YYYY-MM-DD_HHmm.md`
- Inputs Consulted section present
- New signals table with verification status for each
- Evidence quality labeled
- Sources scanned disclosed
- Summary: N new signals OR NO NEW SIGNALS stated clearly

### Step 2: Orchestrator Role (primary session)

Do not spawn a subagent. Read Hunter Agent output and Active Handoff Snapshot. For each new verified signal, resolve to a candidate state:

**Candidate state assignment logic:**

| Signal Strength | Verification | → State |
|---|---|---|
| Scout says "must buy" | VERIFIED (thesis strong) | HIGH-PRIORITY CHALLENGER |
| Scout says "strong buy" | VERIFIED (thesis solid) | CHALLENGER |
| Scout says "buy" | VERIFIED (thesis solid) | CHALLENGER |
| Scout says "accumulate" | VERIFIED (thesis weak) | WATCH WITH SPECIFIC TRIGGER |
| Any recommendation | UNVERIFIED LEAD | WATCH WITH SPECIFIC TRIGGER |
| Any recommendation | REJECTED (thesis doesn't hold) | REJECT |

**File:** `03_AGENT_RUNS/02_DISCOVERY/HUNTER_ORCHESTRATOR_YYYY-MM-DD_HHmm.md`

**Contents:**

```
Inputs Consulted:
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [Hunter Agent output file]

Hunter Watch Summary:
- Signals scanned: [N new, M re-checks, L already tracked]
- Deduplication: [X signals already in handoff tracker, not re-escalated]

Signal Resolution Table:
| Ticker | Company | Source | Recommendation | Verification | State | Rationale |
| [per new signal, with assigned state] |

Handoff Emissions:
[For each signal escalated to CHALLENGER or above:]
HANDOFF_ID = YYYY-MM-DD-HUNTER-[TICKER]-SIGNAL
ORIGIN_MODULE = HUNTER
SOURCE = [scout source name]
SOURCE_SIGNAL_DATE = [signal date or update date]
SECURITY/TICKER = [TICKER]
HANDOFF_TYPE = HUNTER_SIGNAL
DEDUP_KEY = [SOURCE|TICKER|SIGNAL_DATE]
PREVIOUS_STATE = UNKNOWN
NEW_STATE = [WATCH / CHALLENGER / HIGH-PRIORITY CHALLENGER]
EVIDENCE_QUALITY = [VERIFIED FACT / DATA LIMITED]
THESIS_OR_ASYMMETRY_CHANGE = [scout's thesis + CAOS independent verification]
NEXT_GATE = [next verification point: earnings date, next quarterly update, price trigger]
ACTIVE_UNTIL = [suggest: +90 days from today, or until state changes]
REQUIRED_CONSUMERS = DAILY, WEEKLY_RANKING, MONSTER_CENSUS [as relevant]
MANDATORY_DEEP_UNDERWRITING = NO [unless very high asymmetry]

Active Handoff Snapshot Updates:
[List new handoff blocks to paste into Active Handoff Snapshot]

Master Ledger Event:
[If any signal escalated:]
LOG REQUIRED [with paste-ready event block, or]
NO LOG REQUIRED

Heartbeat (if no new signals):
HUNTER WATCH: NO NEW SIGNALS
Last scan: [date/time]
Next scan: [recommended timing]
```

---

## Linking Rule Application

**All output files** must open with "Inputs Consulted" section:

- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]

---

## Execution Rules

From Operator Manual §3 & §6:
- **External sources are scouts, never authority:** A Motley Fool pick is a research prompt, not a buy signal
- **Independent verification mandatory:** Must verify thesis against primary sources (SEC, IR, earnings) before any escalation
- **Reality First:** Use only released financial data, never pre-release analyst forecasts
- **Radical Honesty:** Label evidence (VERIFIED FACT vs. UNVERIFIED LEAD vs. REJECTED)
- **No Hallucination:** Never invent company data; state UNKNOWN if unavailable
- **Deduplication discipline:** Never re-escalate the same signal twice (use DEDUP_KEY)

---

## Success Criteria (Acceptance Checklist)

- ✓ Active Handoff Snapshot "Active Hunter Signals" read for deduplication
- ✓ Watched sources scanned for new or materially changed signals
- ✓ DEDUP_KEY checked for each signal (SOURCE + TICKER + SIGNAL_DATE)
- ✓ For each new signal: independent verification against SEC filings, IR, earnings
- ✓ Evidence quality labeled (VERIFIED FACT / DATA LIMITED / UNKNOWN)
- ✓ Scout source claims NOT accepted at face value; all verified independently
- ✓ Signal resolution: each new signal assigned to REJECT / WATCH / CHALLENGER / HIGH-PRIORITY CHALLENGER
- ✓ Handoff blocks emitted for any new CHALLENGER or above escalation
- ✓ Handoff blocks ready to paste into Active Handoff Snapshot (per Standardized Handoff Protocol §9)
- ✓ Master Ledger event proposed (LOG REQUIRED) or NO LOG REQUIRED stated
- ✓ File named `HUNTER_ORCHESTRATOR_YYYY-MM-DD_HHmm.md` created
- ✓ No duplicate signals: existing signals in Active Handoff not re-escalated
- ✓ Heartbeat condition: if no new signals, state `NO NEW SIGNALS` (no fabricated findings)

---

## Failure States and Recovery

**HUNTER WATCH DEGRADED — Sources unreachable**
- All watched sources unavailable (network down, access blocked)
- **Output:** `HUNTER WATCH DEGRADED — [N] sources unreachable` (no fabricated signals)
- **Recovery:** Retry when sources are accessible

**HUNTER WATCH EMPTY — No new signals**
- Watched sources scanned, no materially new recommendations since last check
- **Output:** Heartbeat line `HUNTER WATCH: NO NEW SIGNALS`

**HUNTER WATCH INCOMPLETE — Partial scan**
- Some sources scanned, some unreachable
- **Output:** `HUNTER WATCH: [N] new signals found, [M] sources unreachable` (disclose limitation)

---

## Run Frequency and Triggers

**Recommended cadence:**
- **Daily check:** Once per day (e.g., 16:00 CET after market close), scanning all sources
- **Ad hoc trigger:** Whenever a major market event, tech stock rotation, or sector shift occurs
  - Example: tech sector drops >5% intraday → run Hunter Watch to check for new AI/infra opportunities
  - Example: major analyst initiates high-conviction AI chip pick → run Hunter Watch to verify

**Sources and cadence:**
- **Motley Fool:** Updated daily (new recs, buy list changes)
- **Seeking Alpha:** Updated continuously (Alpha Picks can change daily)
- **IBD:** Updated daily (IBD 50, Stock of the Day)
- **TipRanks:** Updated continuously (elite analyst actions)

**Note:** Hunter Watch is a lightweight scout, not a comprehensive universe search. For deep discovery, use Monster Census (weekly).

---

## Integration with Active Handoff Snapshot

When a signal is resolved to CHALLENGER or above:

1. Create a new HANDOFF block using Standardized Handoff Protocol (Operator Manual §9)
2. Assign HANDOFF_ID = `YYYY-MM-DD-HUNTER-[TICKER]-SIGNAL`
3. Dedup key = `SOURCE | TICKER | SIGNAL_DATE` (prevents duplicates across runs)
4. Set NEXT_GATE (e.g., next earnings date, price trigger, or +90 day review)
5. Only the Orchestrator writes to Active Handoff Snapshot (no agent direct writes)
6. Paste the handoff block into Active Handoff Snapshot § "Active Hunter Signals" section

---

## Dry-Run Test Plan

Test procedures and scenarios: `04_FLIGHT_RECORDER/Multi-Bagger Hunter Watch Dry-Run Test.md` (to be created)

Covers three scenarios: New Signal (Motley Fool pick, verified and escalated to CHALLENGER), Duplicate Signal (same pick tracked in prior run, not re-escalated), Unverified Lead (high-conviction scout recommendation but weak independent thesis).

---
