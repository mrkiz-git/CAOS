# CAOS — Monster Census

**Command:** `Run CAOS Monster Census`  
**Status:** READY FOR EXECUTION  
**Default schedule:** Saturday 09:00, Mark's confirmed timezone (manual trigger)

---

## What This Product Does

A weekly deep-discovery sweep that comprehensively scans 40+ public companies across 5+ thematic lanes, identifies 8+ genuinely fresh candidates, fully underwrites top opportunities, and maintains a Conversion Scoreboard tracking every candidate's journey (Scanned → Serious Review → Monster File → Seed → Buy-Authorized → Purchased → Winner/Failure).

**Key outputs:**
- **Monster Files:** Deep thesis documents for Top 1–2 candidates, all High-Priority Challengers, and one Anti-Echo (contrarian) candidate
- **Top-5 Ranking:** Raw asymmetry and survivability-adjusted rankings of fresh/highest-conviction opportunities
- **Conversion Scoreboard:** Full pipeline from discovery to execution (shows conversion rates and drop-off points)
- **System audits:** Stale gates, new evidence on existing candidates, contradictions in prior thesis assessments
- **Handoff ACKs:** Confirms consumption of Daily Anchor handoffs (Hunter signals, etc.)
- **Candidate state resolutions:** Every serious review resolved to terminal state (SEED / CHALLENGER / WATCH WITH TRIGGER / REJECT)

---

## Precondition Checks

**Before calling any agent, verify:**

1. **Daily Anchor Availability** — Most recent Daily Anchor output dated within 7 days
   - Read `03_AGENT_RUNS/09_ORCHESTRATOR/` for latest `ORCHESTRATOR_YYYY-MM-DD_*.md` (non-Weekly variant)
   - If missing or >7 days old, state `DATA LIMITED — Daily Anchor missing, using last available handoffs` and proceed
   - If Daily Anchor FAILED, state `CENSUS BLOCKED — Daily Anchor failed, cannot consume handoffs reliably`

2. **Master Ledger Status** — Current and initialized
   - Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
   - If `UNINITIALIZED` or stale (>7 days), state `DATA LIMITED — portfolio state stale, proceeding in discovery-only mode` (candidate universe work proceeds; sizing/seeding blocked)

3. **Active Handoff Snapshot** — Available and current
   - Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
   - If missing or >3 days stale, state `DATA LIMITED — Active Handoff Snapshot incomplete, prior handoffs may be missed`

4. **Candidate Registry Readiness** — Master Ledger §5 (Candidate / Status Registry) is readable
   - Used to check for duplicate reviews and track state transitions

---

## The 8 Mandatory Work Items and Who Produces Them

| Item | Producer | Output |
|------|----------|--------|
| **1. Search scope & completeness metadata** | Discovery Agents A, B, C combined | ≥40 companies scanned, ≥5 thematic lanes, ≥8 fresh names, search timestamp |
| **2. New candidate identification** | Discovery (three lanes parallel) | All new candidates with: ticker, thesis stage, asymmetry grade, next gate, lane assignment |
| **3. Prior-candidate re-check** | Discovery (three lanes parallel) | Updates on any candidates in Master Ledger with new evidence, price moves, or thesis changes |
| **4. Top-5 Fresh Candidates ranking** | Orchestrator | Raw-asymmetry and survivability-adjusted rankings; head-to-head brief vs. cash |
| **5. Monster File underwriting** | Orchestrator (using Discovery + Underwriter pattern) | Full Monster File for each: Top 1–2, all High-Priority Challengers, one Anti-Echo candidate; includes thesis, survival score, proof gates, execution risks |
| **6. Conversion Scoreboard** | Orchestrator | Pipeline table: Scanned → Serious Review → Monster File → Seed → Buy-Authorized → Purchased → Winner/Failure (counts and drop-off rates) |
| **7. System audit findings** | Orchestrator | Stale gates (evidence expected but not received); contradictions (prior conviction vs. current evidence); orphaned candidates; unresolved handoffs lingering >30 days |
| **8. Handoff ACK & emissions** | Orchestrator | ACK every active Daily Anchor handoff; emit new handoff blocks for any candidate state transitions, new evidence gates, or new Seed/Challenger escalations |

---

## Agent Execution Sequence

```
Daily Anchor Handoff Consumption
    |
Discovery A (Lane 1: AI/Infrastructure/Power/Cooling/Networking)
Discovery B (Lane 2: Semiconductors/Memory/Equipment/Devices)      (parallel)
Discovery C (Lane 3: Defense/Autonomy/Quantum/Batteries/Biotech/Other)
    |
    └─→ Orchestrator (consolidation, ranking, Monster Files, audits, emissions)
```

**Timeline:** Steps 1–3 can run concurrently (no dependencies). Orchestrator waits for all three to complete.

---

## Agent Call Sequence

### Step 1: Call Discovery Agents A, B, C (parallel)

Call the Agent tool **three times in the same turn** (one per lane). Use invocation prompt templates from [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Census Lanes)]], substituting lane assignment for each:

**Lane A (AI infrastructure, power, cooling, networking):**
```
You are Discovery Agent A (Monster Census). Read your full role spec at
03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Census Lanes).md 
and follow it exactly. Your lane assignment: Lane A (AI, Infrastructure, 
Power, Cooling, Networking). Search for 15+ companies in this lane. 
Read the Master Ledger, Active Handoff Snapshot, and most recent Daily Anchor.
Write output to: 03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_INFRA_POWER_YYYY-MM-DD_CENSUS.md
```

**Lane B (Semiconductors, memory, equipment, devices):**
```
You are Discovery Agent B (Monster Census). Read your full role spec at
03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Census Lanes).md 
and follow it exactly. Your lane assignment: Lane B (Semiconductors, Memory, 
Equipment, Devices). Search for 15+ companies in this lane. 
Read the Master Ledger, Active Handoff Snapshot, and most recent Daily Anchor.
Write output to: 03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_CHIPS_MEMORY_YYYY-MM-DD_CENSUS.md
```

**Lane C (Defense, autonomy, quantum, batteries, biotech, other):**
```
You are Discovery Agent C (Monster Census). Read your full role spec at
03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery (Census Lanes).md 
and follow it exactly. Your lane assignment: Lane C (Defense, Autonomy, 
Quantum, Batteries, Biotech, Other). Search for 15+ companies in this lane. 
Read the Master Ledger, Active Handoff Snapshot, and most recent Daily Anchor.
Write output to: 03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_DEFENSE_AUTONOMY_YYYY-MM-DD_CENSUS.md
```

**Outputs to verify:**
- Lane A: `DISCOVERY_INFRA_POWER_YYYY-MM-DD_CENSUS.md`
- Lane B: `DISCOVERY_CHIPS_MEMORY_YYYY-MM-DD_CENSUS.md`
- Lane C: `DISCOVERY_DEFENSE_AUTONOMY_YYYY-MM-DD_CENSUS.md`
- Each file must open with "Inputs Consulted" section
- Each file must include: search count (≥15 per lane), new candidates table, re-check on prior candidates, search completeness assessment

### Step 2: Call Orchestrator (primary session, not a subagent)

**Do not spawn a subagent.** Read all three Discovery outputs and synthesize into Census Orchestrator output. Use invocation prompt from [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Census)]] as a template:

```
You are the CAOS Orchestrator (Monster Census). Read your full role spec at
03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Census).md 
and follow it exactly. You are consolidating a Monster Census run.

Read the following Discovery outputs:
- DISCOVERY_INFRA_POWER_<date>_CENSUS.md
- DISCOVERY_CHIPS_MEMORY_<date>_CENSUS.md
- DISCOVERY_DEFENSE_AUTONOMY_<date>_CENSUS.md

Read the most recent Daily Anchor (consumes handoffs), Master Ledger, 
and Active Handoff Snapshot.

Consolidate all findings into a single output:
03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_CENSUS.md

This output must include:
- Full Run Map (wikilinks to all 3 Discovery + Orchestrator, Daily Anchor, Master Ledger)
- Consolidated search completeness grade (40+ companies, 5+ lanes, 8+ fresh)
- Top-5 fresh candidates ranking (raw asymmetry + survivability-adjusted)
- Monster Files (Top 1-2, all High-Priority Challengers, Anti-Echo candidate)
- Conversion Scoreboard with pipeline metrics
- System audit section (stale gates, contradictions, orphans)
- Handoff ACK checks and new handoff emissions
- Master Ledger event proposal or NO LOG REQUIRED
```

**Output to verify:**
- File: `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_CENSUS.md`
- Opens with "Inputs Consulted" wikilinks to all three Discovery files, Daily Anchor, Master Ledger, Active Handoff
- Contains "Full Run Map" linking all upstream files
- Search completeness: explicit SEARCH COMPLETE or SEARCH INCOMPLETE with reason
- ≥5 Monster Files (Top 1–2 minimum, plus High-Priority Challengers minimum 1–2, plus Anti-Echo 1)
- Conversion Scoreboard table with counts across all pipeline stages

---

## Linking Rule Application

Every file written must open with an "Inputs Consulted" section:

**Discovery outputs (Lanes A, B, C):**
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Wikilink: [[most recent Daily Anchor file]]

**Orchestrator output:**
- Wikilink: [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_INFRA_POWER_YYYY-MM-DD_CENSUS.md]]
- Wikilink: [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_CHIPS_MEMORY_YYYY-MM-DD_CENSUS.md]]
- Wikilink: [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_DEFENSE_AUTONOMY_YYYY-MM-DD_CENSUS.md]]
- Wikilink: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Wikilink: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Wikilink: [[most recent Daily Anchor file]]

This makes the dependency graph traversable in Obsidian and enables Linked Mentions to show all downstream consumers.

---

## Execution Rules

From Operator Manual §3 (Constitutional Laws):
- **Reality First.** Search only for publicly traded companies with verifiable data; state UNKNOWN or DATA LIMITED rather than guessing
- **Radical Honesty.** Label evidence: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN
- **Fresh-Evidence Supremacy.** New evidence overrides prior Monster Census or Daily Anchor rankings
- **Survivability Before Optionality.** Reject candidates with implausible survival even if asymmetry is compelling
- **No Autonomous Action.** Monster Files are recommendations only; no automatic Seed or Challenger state changes without Mark approval
- **No Hallucinated Companies.** Every ticker and every thesis must be verifiable via public filings, IR, or reporting

**Search discipline:**
- Search must span publicly traded companies only (not private equity, unlisted, penny stocks <$1B market cap unless explicit exception)
- Each lane must deliver its ≥15 companies with search methodology disclosed (e.g., "screened by market cap, sector, growth, valuation")
- Mark the timestamp for every news item, guidance, or filing cited (must be within past 90 days for "fresh" evidence)

---

## Success Criteria (Acceptance Checklist)

- ✓ All 3 Discovery agents run and files saved
- ✓ Combined search reaches ≥40 public companies across ≥5 lanes (3 lanes minimum + spillover)
- ✓ ≥8 genuinely fresh names (not reviewed in prior 6 months, not in current Master Ledger Candidate Registry)
- ✓ All new candidates with asymmetry grades, thesis stages, next proof gates
- ✓ Re-checks completed on any prior candidates with new evidence or price moves
- ✓ Top-5 ranking (raw asymmetry + survivability-adjusted) with head-to-head vs. cash briefs
- ✓ ≥5 Monster Files (Top 1–2 + High-Priority Challengers minimum + Anti-Echo)
- ✓ Conversion Scoreboard shows pipeline: Scanned → Serious Review → Monster File → Seed → Buy-Authorized → Purchased → Winner/Failure
- ✓ System audit flags: stale gates (dated and reason), contradictions (prior vs. current conviction), orphan positions (lack recent evidence)
- ✓ Handoff ACK checks: every Daily Anchor handoff received, applied, and current status noted
- ✓ New handoff emissions for any candidate state changes (from UNKNOWN → SERIOUS REVIEW, etc.)
- ✓ Master Ledger event proposed (LOG REQUIRED) or NO LOG REQUIRED stated
- ✓ No hallucinated companies, financials, or evidence; all sources cited with dates
- ✓ File named `ORCHESTRATOR_YYYY-MM-DD_CENSUS.md` created
- ✓ No silent failures: state DATA LIMITED, BLOCKED, DEGRADED explicitly

---

## Failure States and Recovery

**CENSUS BLOCKED — Critical precondition missing**
- Daily Anchor FAILED or dates >14 days old
- Master Ledger UNINITIALIZED
- Active Handoff Snapshot unreadable
- **Recovery:** Ensure Daily Anchor completes successfully, Master Ledger is current, then retry

**CENSUS DEGRADED — Limited data but can proceed**
- `DATA LIMITED — portfolio state stale, proceeding in discovery-only mode` — candidate discovery proceeds; sizing/seeding decisions blocked
- `DATA LIMITED — one lane (Lane B) search incomplete, combined search count 35 of 40` — proceed with note; aim for 40 in next run
- `DATA LIMITED — Active Handoff Snapshot >3 days stale` — handoff ACK checks incomplete; flag in output
- **Recovery:** Proceed with noted limitations; rerun next Saturday with fresher data

**CENSUS FAILED — Agent failure mid-run**
- Discovery Agent A/B/C failed or produced unreadable output — **halt that lane,** state which, determine if other lanes can proceed
- Orchestrator unable to consolidate (corrupt Discovery files) — state which input is unreadable; whether Census can proceed with 2 of 3 lanes
- **Recovery:** Fix the failing agent, rerun that lane, then re-consolidate, OR proceed with available lanes and state DEGRADED

---

## Integration with CAOS System

### Daily Anchor Handoff Consumption
The Census Orchestrator reads the most recent Daily Anchor's Active Handoff emissions. Every active handoff touching the Census discovery universe must be acknowledged:

```
HANDOFF ACK CHECK: [HANDOFF_ID] | RECEIVED=YES | APPLIED=YES/NO | 
RESULTING_STATE | STILL_ACTIVE=YES/NO | RESOLVES_HANDOFF_ID
```

If a Daily Anchor Hunter signal matches a Census discovery, note the match and escalate for serious review.

### Master Ledger Candidate Registry Updates
Before underwriting any discovered candidate, check Master Ledger §5 (Candidate / Status Registry):
- If candidate already registered as SERIOUS REVIEW or higher → skip re-review unless new evidence warrants
- If candidate is new → add to registry with UNKNOWN state, escalate High-Priority candidates to SERIOUS REVIEW
- All state transitions logged in Master Ledger event block

### Active Handoff Snapshot Updates
Census Orchestrator emits new handoffs using the Standardized Handoff Protocol (Operator Manual §9) for:
- New SERIOUS REVIEW candidate escalations
- New evidence gates (e.g., "Earnings call 2026-10-15")
- Any candidate moving to SEED or CHALLENGER status
- Anti-Echo candidates flagged for contrarian review

Only the Orchestrator writes to Active Handoff Snapshot; this maintains single-writer discipline.

---

## Design Specification and Details

Full architecture details: [[06_PRODUCT_RUNBOOKS/Monster Census Design.md]]

Coverage includes:
- Lane assignment and search methodology
- Monster File structure (thesis, valuation, financials, survival, execution risks)
- Conversion Scoreboard pipeline and metrics
- System audit checks (detailed procedures)
- Evidence labeling and source citation standards
- Handoff protocol and state-transition rules

---

## Dry-Run Test Plan

Test procedures and scenarios: `04_FLIGHT_RECORDER/Monster Census Dry-Run Test.md`

Covers three scenarios: Happy Path (all agents complete, 8+ fresh found), Discovery Gaps (one lane completes early, 5 fresh found), and Handoff Conflicts (prior handoff contradicts new discovery).

---

### Weekly Ranking Feed
Monster Census completes Saturday morning. Weekly Ranking runs Sunday morning and consumes all Monster Census handoffs via Active Handoff Snapshot and updated Master Ledger candidate registry.

New Challengers and Seeds from Monster Census are ranked against current holdings and other candidates in Weekly Ranking.

### Independence from Other Products
Monster Census is independent of Post-Open Delta Check, Emergency Thesis Rerun, DCA Execution Card, Deep Audit, and Learning Review. It has no blocking dependencies on those products and does not block their execution.

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#14. Monster Census specification]]
