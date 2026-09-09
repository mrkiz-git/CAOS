# CAOS — Event Gate Watch

**Command:** `Run CAOS Event Gate Watch`  
**Status:** READY FOR EXECUTION  
**Default schedule:** Manual; recommended daily (or immediately after significant event)

---

## What This Product Does

A lightweight daily check for material new information on earnings, filings, guidance, or events that gate CAOS decisions. Monitors two channels:

1. **Active Event Gates:** Any gate in the Active Handoff Snapshot that is waiting for specific evidence (e.g., "Earnings call 2026-10-15" or "10-Q filing by deadline")
2. **Permanent NVIDIA Gate:** Continuous monitoring of NVIDIA earnings, CFO commentary, 10-Q filings, and guidance updates (read-through to economically connected CAOS holdings like IREN, WULF, TSLA)

**Key outputs:**
- Gate resolution status (TRIGGERED / STILL PENDING / TRANSCRIPT PENDING)
- New NVIDIA evidence and read-through to connected holdings
- Handoff emissions if any gate triggers
- Action items (new evidence may call for unscheduled Daily Anchor)

---

## Precondition Checks

**Before starting, verify:**

1. **Active Handoff Snapshot readable**
   - Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] and check "Event Gates" section
   - If missing or unreadable, state `EVENT GATE WATCH BLOCKED — Active Handoff Snapshot unavailable` and **STOP**

2. **Last Event Gate Watch timestamp**
   - Check the most recent `EVENT_GATE_WATCH_YYYY-MM-DD_HHmm.md` in [[03_AGENT_RUNS/02_DISCOVERY/]]
   - If found, note the timestamp (used for deduplication: don't re-report events logged in last check)

---

## The 2 Mandatory Work Items and Who Produces Them

| Item | Producer | Output |
|------|----------|--------|
| **1. Active event gates status check** | Agent (one call per gate, or combined if few) | For each gate: RESOLVED / TRIGGERED / STILL PENDING / TRANSCRIPT PENDING with evidence summary |
| **2. Permanent NVIDIA gate check** | Industry Read-through agent (if new NVIDIA material) | NVIDIA earnings/guidance summary, data center/AI demand, connected-holding read-through |
| **3. Handoff emissions & ledger event** | Orchestrator (primary session) | New handoff blocks (if gate triggered), Master Ledger event proposal or NO LOG REQUIRED |

---

## Agent Execution Sequence

```
Read Active Handoff Snapshot "Event Gates" section
    |
For each open gate:
    Call Agent tool (one call per gate, or combined if multiple)
    to check for material new evidence
    |
Separately: Check for new NVIDIA material
    If found, call Industry Read-through Agent
    |
Orchestrator role (primary session):
    Consolidate findings, emit handoffs, propose Master Ledger event
```

No dependencies between gate checks (all can run in parallel if multiple gates).

---

## Agent Call Sequence

### Step 1: Check Each Active Event Gate

For each gate listed in Active Handoff Snapshot "Event Gates" section:

**Call the Agent tool with this prompt template:**

```
You are Event Gate Watch (CAOS). Your task: check for material new evidence 
on one or more active event gates.

Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]].
Identify the "Event Gates" section.

For each gate listed:
- Gate description: [gate name/description]
- Expected trigger: [trigger event, e.g., "Earnings call 2026-10-15"]
- Current status: check whether the trigger has occurred and material evidence is released

For EACH gate:
1. Has the trigger event occurred? (e.g., did the earnings call happen on the scheduled date?)
2. If yes, is the full evidence available? (e.g., full call transcript, official press release, 10-Q filing)
3. If evidence is available: summarize it (max 200 words) and state whether it RESOLVES, 
   TRIGGERS, or leaves the gate STILL PENDING.
4. If evidence is partially available: state TRANSCRIPT PENDING and distinguish 
   confirmed facts from incomplete/inferred facts.
5. If the trigger has not yet occurred: state STILL PENDING with expected date.

Output format:
- Gate ID: [gate name]
- Trigger: [what event gates the decision]
- Status: [RESOLVED / TRIGGERED / STILL PENDING / TRANSCRIPT PENDING]
- Summary: [one paragraph if event has occurred; empty if pending]
- Read-through: [how this affects connected CAOS holdings if triggered]

RULES:
- Never use pre-release forecasts or guidance updates to satisfy a post-results gate 
  (only actual released results count)
- Separate VERIFIED FACT (from release material), CAOS INFERENCE (your interpretation), 
  and UNKNOWN clearly
- Never hallucinate transcript details or invent earnings results
- If transcript is embargoed or behind paywall, state TRANSCRIPT PENDING, 
  not "based on discussion"
```

If there are ≥3 open gates, you may bundle them into one Agent tool call. If gates are independent, parallel calls are OK.

**Output to verify:**
- Each gate status clearly marked
- Evidence summary (if gate has triggered)
- Read-through to connected holdings

### Step 2: Check Permanent NVIDIA Gate

**Every Event Gate Watch run,** check whether NEW NVIDIA material has appeared since the last Event Gate Watch run. New material includes:
- Quarterly earnings release (earnings date or press release date)
- Earnings call (new call date after prior check date)
- 10-Q, 10-K, or 8-K filing
- CFO commentary or investor day presentation
- Materially updated guidance (revenue ramp, margin guidance, supply assumptions)

**If new material found,** call the Agent tool with this prompt:

```
You are Industry Read-through (CAOS) — Permanent NVIDIA Gate. Read your full role spec at
03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md and follow it exactly.

THIS IS AN EVENT GATE WATCH RUN. New NVIDIA material has appeared since [LAST CHECK DATE].

Material to check:
- [Describe new earnings, filing, guidance, or commentary]

Assess NVIDIA on these dimensions (from Permanent NVIDIA Gate specification):
1. Data Center/Hyperscale demand: revenue growth, customer concentration, platform shifts
2. Blackwell and Vera Rubin: demand, production capacity ramp, yield/margin impact
3. Networking, optics, memory: revenue contribution, competitive threats
4. Land, power, shell, financing: data center expansion constraints, CapEx guidance
5. China assumptions: revenue exposure, policy risk, competitive pressure
6. Gross margin: trends, execution, manufacturing efficiency
7. Forward guidance: revenue/margin outlook, demand visibility

Read-through to economically connected CAOS holdings:
- IREN (Iris Energy): power demand from NVIDIA AI, data center electricity costs
- WULF (Terawulf): similar power/infrastructure exposure
- TSLA: no direct exposure, but monitor for NVIDIA AI chip usage in autonomy (speculative)

Write output to: 03_AGENT_RUNS/04_INDUSTRY/NVIDIA_GATE_YYYY-MM-DD_HHmm.md

Output format:
- NVIDIA Summary: [key findings from new material, max 300 words]
- Demand Verdict: [data center AI demand strong/softening/uncertain; confidence level]
- Margin Outlook: [gross margin trajectory and risks]
- Connected-Holding Read-through: [implications for IREN, WULF, others]
- NVIDIA Gate Verdict: [POSITIVE / NEUTRAL / CAUTION — for CAOS thesis validation]
- Evidence Quality: [VERIFIED FACT / DATA LIMITED / UNKNOWN for each claim]
```

**Output to verify:**
- NVIDIA material summarized with sources and dates
- Connected-holding read-through (IREN, WULF specifically)
- Evidence quality labeled

### Step 3: Orchestrator Role (primary session, not a subagent)

Do not spawn a subagent. Read all gate check outputs and any NVIDIA gate output. Synthesize into one Event Gate Watch report:

**File:** `03_AGENT_RUNS/02_DISCOVERY/EVENT_GATE_WATCH_YYYY-MM-DD_HHmm.md`

**Contents:**

```
Inputs Consulted:
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [any Agent outputs from gate checks]

Event Gate Status Report:
[For each gate checked:]
- Gate: [gate name]
- Status: [RESOLVED / TRIGGERED / STILL PENDING / TRANSCRIPT PENDING]
- Evidence: [summary, or "awaiting trigger"]
- Read-through: [impact on connected holdings]

NVIDIA Gate: [NEW MATERIAL / NO NEW MATERIAL]
[If new material:]
- Summary: [key findings]
- Impact: [POSITIVE / NEUTRAL / CAUTION for connected holdings]
- Connected holdings affected: [IREN, WULF, others]

Action Items:
[List any gates that TRIGGERED or RESOLVED]
- [Gate name] TRIGGERED → consider unscheduled Daily Anchor or thesis rerun
- [Gate name] RESOLVED → update Active Handoff Snapshot per protocol

Handoff Emissions:
[For any gate that triggered or resolved:]
HANDOFF_ID = YYYY-MM-DD-EVENT_GATE-[GATE_NAME]-TRIGGERED
SOURCE = EVENT_GATE_WATCH
EVIDENCE_QUALITY = [VERIFIED FACT / DATA LIMITED]
DEDUP_KEY = [gate_name + trigger_date]
...

Master Ledger Event:
[If any gate triggered and requires Master Ledger logging:]
LOG REQUIRED [with paste-ready event block]
OR
NO LOG REQUIRED
```

**Heartbeat condition:** If no gates are open and no new NVIDIA material:

```
EVENT GATE WATCH: NO NEW EVENT GATES
Timestamp: [HH:mm CET]
Next scheduled check: [tomorrow same time, or ad hoc on market news]
```

---

## Linking Rule Application

**All output files** must open with "Inputs Consulted" section:

- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Wikilink: any Agent output files from gate checks

---

## Execution Rules

From Operator Manual §3 & §6:
- **Reality First:** Only actual released evidence counts (earnings dates, filed documents, call transcripts). Pre-release forecasts do NOT satisfy a post-results gate.
- **Radical Honesty:** Separate VERIFIED FACT (from release), CAOS INFERENCE (interpretation), and UNKNOWN clearly
- **Fresh Evidence Supremacy:** New NVIDIA material overrides prior assumptions about data center demand or AI ramp
- **No Hallucination:** Never invent earnings results, guidance updates, or transcript quotes
- **External sources as scouts:** NVIDIA analyst reports or sell-side estimates inform but never conclude read-through to connected holdings without independent verification

---

## Success Criteria (Acceptance Checklist)

- ✓ Active Handoff Snapshot "Event Gates" section read
- ✓ Each open gate checked for material new evidence (call transcript, filing, press release)
- ✓ Gate status (RESOLVED / TRIGGERED / STILL PENDING / TRANSCRIPT PENDING) stated clearly
- ✓ For gates that TRIGGERED: read-through to connected holdings completed
- ✓ Permanent NVIDIA gate checked for new material
- ✓ If new NVIDIA material: read-through to IREN, WULF (and others if applicable)
- ✓ All evidence cited with source and date; no hallucinated quotes or results
- ✓ Handoff emissions for any gate that resolved or triggered
- ✓ Master Ledger event proposal (LOG REQUIRED) or NO LOG REQUIRED stated
- ✓ File named `EVENT_GATE_WATCH_YYYY-MM-DD_HHmm.md` created
- ✓ No silent skips: state BLOCKED, DEGRADED, or NO NEW GATES explicitly

---

## Failure States and Recovery

**EVENT GATE WATCH BLOCKED — Cannot proceed**
- Active Handoff Snapshot unreadable → cannot identify open gates
- **Recovery:** Fix Handoff Snapshot, retry

**EVENT GATE WATCH DEGRADED — Limited data**
- `TRANSCRIPT PENDING — earnings call confirmed but full transcript not yet released` (proceed with partial evidence)
- `DATA LIMITED — NVIDIA filing delayed, using last quarter guidance for read-through`
- **Recovery:** Re-check next scheduled time when evidence is available

**EVENT GATE WATCH EMPTY — No gates, no action**
- No open gates in Active Handoff Snapshot, no new NVIDIA material
- **Output:** Heartbeat line `NO NEW EVENT GATES` (no fabricated findings)

---

## Run Frequency and Triggers

**Recommended cadence:**
- **Daily heartbeat:** Once per day (e.g., 02:00 or after market close), checking for new gate material
- **Ad hoc trigger:** Immediately upon material market event, earnings announcement, or guidance update
  - Example: if NVIDIA announces earnings date, run Event Gate Watch that day
  - Example: if a connected holding's 10-Q is filed, run Event Gate Watch to check read-through

**Emergency trigger:**
- CAOS holdings drop >10% intraday on news → run Event Gate Watch to check if a gate has triggered
- Unscheduled earnings/filing announcement → run Event Gate Watch within 4 hours of release

---

## Integration with Active Handoff Snapshot

When a gate RESOLVES or TRIGGERS:

1. Read current Active Handoff Snapshot "Event Gates" section
2. Find the corresponding HANDOFF_ID for the resolved gate
3. Emit a new handoff block (Standardized Handoff Protocol §9) with:
   - RESOLVES_HANDOFF_ID = [prior handoff ID]
   - NEW_STATE = [RESOLVED / TRIGGERED]
   - NEXT_GATE = [if gate only partially resolved, next expected evidence]
4. Only the Orchestrator role writes to Active Handoff Snapshot; no direct agent writes

---

## Dry-Run Test Plan

Test procedures and scenarios: `04_FLIGHT_RECORDER/Event Gate Watch Dry-Run Test.md` (to be created)

Covers three scenarios: Gate Resolved (earnings call released, thesis validated), Gate Triggered (new evidence contradicts prior assumption), No New Events (daily heartbeat).

---
