# CAOS — Workflows Execution Manual

Complete guide to running all 8 workflows manually. Each workflow is fully runnable by following its runbook, copying agent invocation prompts, and orchestrating results in the primary Claude Code session.

---

## QUICK REFERENCE: Workflow Calendar

### ACTIVE (Ready Now)

| Workflow | Schedule | Duration | Complexity | Command |
|----------|----------|----------|-----------|---------|
| **Daily Anchor** | Mon–Fri 18:15 | 20–30 min | High | `Run CAOS Daily Anchor` |
| **Post-Open Delta Check** | Same day, ad hoc | 10–15 min | Medium | `Run CAOS Post-Open Delta Check` |

### READY FOR EXECUTION (Specs Complete, Manually Runnable)

| Workflow | Frequency | Duration | Complexity | Command |
|----------|-----------|----------|-----------|---------|
| **Weekly Ranking** | Sun 10:00 | 30–40 min | High | `Run CAOS Weekly Ranking` |
| **Monster Census** | Sat 09:00 | 45–60 min | Very High | `Run CAOS Monster Census` |
| **Event Gate Watch** | Daily (ad hoc) | 5–15 min | Low | `Run CAOS Event Gate Watch` |
| **Multi-Bagger Hunter Watch** | Daily (ad hoc) | 10–20 min | Low | `Run CAOS Multi-Bagger Hunter Watch` |
| **Deep Audit** | Monthly | 45–60 min | Very High | `Run CAOS Deep Audit` |
| **Learning Review** | Monthly | 20–30 min | Medium | `Run CAOS Learning Review` |

---

## Workflow Dependency Map

```
┌─────────────────────────────────────────────────────────────┐
│                      Daily Anchor (M–F)                      │
│              (Full 9-agent analysis pipeline)                │
│  ✓ ACTIVE — run manually, generates handoff signals          │
└──────────────────┬──────────────────────────────────────────┘
                   │
                   ├─→ Post-Open Delta Check (same day, ad hoc)
                   │   (5-agent subset for intraday changes)
                   │   ✓ ACTIVE
                   │
                   ├─→ Event Gate Watch (daily heartbeat)
                   │   (checks for earnings/filing releases)
                   │   ✓ READY FOR EXECUTION
                   │
                   └─→ Multi-Bagger Hunter Watch (daily heartbeat)
                       (external scout signal verification)
                       ✓ READY FOR EXECUTION
                       │
                       └─→ Weekly Ranking (Sunday)
                           (re-ranks all candidates vs. holdings)
                           ✓ READY FOR EXECUTION
                           │
                           ├─→ Monster Census (Saturday, separate)
                           │   (deep discovery sweep, 40+ companies)
                           │   ✓ READY FOR EXECUTION
                           │
                           └─→ Deep Audit (monthly)
                               (rebuild from 100% cash, test holdings)
                               ✓ READY FOR EXECUTION
                               │
                               └─→ Learning Review (monthly)
                                   (assess what worked/failed this cycle)
                                   ✓ READY FOR EXECUTION
```

---

## EXECUTION SEQUENCE BY DAY

### MONDAY–FRIDAY WORKFLOWS

**18:15 (after market close):**
1. `Run CAOS Daily Anchor`
   - Full 9-agent pipeline
   - ~20–30 minutes
   - Output: execution card, thesis review, next-euro ranking
   - Confirm any trades before executing

**Same day (if urgent news):**
2. `Run CAOS Post-Open Delta Check` (optional)
   - If market event invalidates Daily Anchor thesis
   - ~10–15 minutes
   - Requires same-day Daily Anchor

**As needed (daily heartbeat or event-triggered):**
3. `Run CAOS Event Gate Watch`
   - Check for earnings releases, filing availability
   - ~5–15 minutes depending on gates open
   - Output: gate status (RESOLVED/TRIGGERED/PENDING)

4. `Run CAOS Multi-Bagger Hunter Watch`
   - Scan external sources for new high-conviction signals
   - ~10–20 minutes depending on sources
   - Output: new candidate signals, deduped vs. prior

---

### WEEKEND WORKFLOWS

**Saturday 09:00:**
1. `Run CAOS Monster Census`
   - Deep discovery sweep: 40+ companies, 5+ lanes
   - ~45–60 minutes (3 Discovery agents parallel, then Orchestrator)
   - Output: Top-5 ranking, Monster Files, Conversion Scoreboard
   - Wait for this to complete before Weekly Ranking

**Sunday 10:00:**
2. `Run CAOS Weekly Ranking`
   - Re-ranks all holdings, Seeds, Challengers, fresh candidates
   - ~30–40 minutes (9-agent pipeline, same as Daily Anchor)
   - Requires: Daily Anchor <7 days old, Monster Census <30 days old
   - Output: ranked universe, funded-holding re-validation, next-euro map

---

### MONTHLY WORKFLOWS

**First trading day of month:**
1. `Run CAOS Deep Audit`
   - Rebuild portfolio from 100% cash, no anchoring
   - ~45–60 minutes (9-agent pipeline + Ledger self-audit)
   - Output: capital map, INCLUDE/RESIZE/REPLACE/EXIT verdicts, Ledger repairs
   - Creates Flight Recorder entry (after Mark's review)

**3rd of month (after Deep Audit + Flight Recorder):**
2. `Run CAOS Learning Review`
   - Assess what worked/failed, evidence quality, system drift
   - ~20–30 minutes (synthesis only, no agents by default)
   - Output: right/wrong calls, drift assessment, amendment proposals
   - Amendments require Mark approval before logging

---

## FULL WORKFLOW RUNBOOKS

Each workflow has a complete runbook with:
- **Precondition checks** (what must be true before starting)
- **Mandatory work items** (what agents produce)
- **Agent call sequence** (exact invocation prompts to copy/paste)
- **Output contracts** (what each file should contain)
- **Linking rules** (how files reference upstream inputs)
- **Execution rules** (CAOS constitutional laws applied)
- **Success criteria** (acceptance checklist)
- **Failure handling** (recovery procedures)

### ACTIVE WORKFLOWS

**[[06_PRODUCT_RUNBOOKS/Daily Anchor]]**
- Full 9-agent analysis of all holdings + top 12+ candidates
- Manual run: read runbook, call agents in sequence, orchestrate
- Output files: 8 agent outputs + 1 Orchestrator output with execution card

**[[06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design]]**
- 5-agent subset (Verifier, Discovery, Forward, Portfolio Court, Orchestrator)
- Precondition: same-day Daily Anchor must be ACTIVE
- Manual run: follow runbook, call 5 agents, deliver thesis rerun

### READY FOR EXECUTION

**[[06_PRODUCT_RUNBOOKS/Weekly Ranking]]**
- 9-agent pipeline (same agents, Weekly Ranking variants)
- Consolidates all candidates, re-ranks, audits system health
- Produces: funded-holding re-validation, Top-5 fresh candidates, execution readiness gate
- Monthly special: first run of calendar month includes Architecture Maintenance check

**[[06_PRODUCT_RUNBOOKS/Monster Census]]**
- 3 Discovery agents (parallel lanes: AI/Infrastructure, Semiconductors, Defense/Other)
- 1 Orchestrator (consolidation, Monster Files, Conversion Scoreboard)
- Produces: 40+ company scan, 8+ fresh names, Top-5 ranking, deep underwriting files

**[[06_PRODUCT_RUNBOOKS/Event Gate Watch]]**
- Check for material new evidence on active event gates (earnings, filings, guidance)
- Permanent NVIDIA gate (continuous monitoring)
- Manual run: 1–N gate checks, optional NVIDIA read-through, Orchestrator consolidation
- Output: gate status, read-through to connected holdings, handoff emissions

**[[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]]**
- Scan external scout sources (Motley Fool, Seeking Alpha, IBD, TipRanks)
- Independent verification of each signal (no accepting scout claims at face value)
- Manual run: Hunter Agent verification, Orchestrator state resolution, handoff emission
- Output: new signals table, verification status, candidate state (REJECT/WATCH/CHALLENGER/HIGH-PRIORITY)

**[[06_PRODUCT_RUNBOOKS/Deep Audit]]**
- Rebuild portfolio from 100% cash, no anchoring
- Test every funded position for inclusion, sizing, replacement
- Includes: Ledger self-audit, incumbency bias check, capital map
- Manual run: 9-agent pipeline (Deep Audit variants) + Orchestrator, Ledger repair if needed
- Output: next-euro capital map, INCLUDE/RESIZE/REPLACE/EXIT verdicts, Ledger audit

**[[06_PRODUCT_RUNBOOKS/Learning Review]]**
- Synthesis only (no agents by default)
- Assess right calls, wrong calls (good process vs. bad), evidence quality, system drift
- Propose amendments (Mark approval required before logging)
- Manual run: read Master Ledger + Flight Recorder + prior outputs, Orchestrator synthesizes
- Output: right/wrong calls, drift assessment, amendment proposals, learning points

---

## HOW TO RUN A WORKFLOW

### Step-by-Step Pattern

1. **Read the runbook** — Located in `06_PRODUCT_RUNBOOKS/[Workflow Name].md`
   - Verify preconditions are met
   - Note mandatory work items
   - Review agent call sequence

2. **Precondition checks** — Ensure all required files exist and are current
   - Master Ledger status (INITIALIZED? stale?)
   - Active Handoff Snapshot readable?
   - Required prior outputs (Daily Anchor, Monster Census, etc.) available?

3. **Gather inputs** — Prepare any data needed for agents
   - Fresh broker screenshot/export (if agents verify portfolio state)
   - Known gates or signals (from Active Handoff Snapshot)

4. **Call agents in sequence** — Use invocation prompt templates from runbook
   - Copy the exact invocation prompt from runbook
   - Call Agent tool with the prompt
   - **Wait for agent to complete** (do not continue until output file is confirmed)

5. **Orchestrator synthesis** — Primary session (not a subagent)
   - Read all agent output files from this run
   - Synthesize into Orchestrator output file (ORCHESTRATOR_YYYY-MM-DD_[RUN_TYPE].md)
   - Include Full Run Map (wikilinks to all upstream files)
   - Present final verdict in chat

6. **Linking rule application** — Every file opens with "Inputs Consulted"
   - Agent outputs: wikilink Master Ledger, Active Handoff, any prior agent outputs they read
   - Orchestrator: wikilink all agent files + Master Ledger + Active Handoff

7. **Handle logging** — If changes to Master Ledger needed
   - If `LOG REQUIRED`: present paste-ready event block
   - Mark pastes into Master Ledger and replies `logged` to confirm
   - Do NOT mark as logged until Mark confirms

---

## COPYING AGENT INVOCATION PROMPTS

Each workflow runbook includes **invocation prompt templates** for each agent. These are ready to copy directly into the Agent tool:

**Example:**
```
**Verifier invocation template from Daily Anchor runbook:**

"You are the CAOS Verifier agent (Agent 1). Read your full role spec at 
`03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md` in this vault 
and follow it exactly. Read the Master Ledger and Active Handoff Snapshot 
at the paths it lists. Write today's output to 
`03_AGENT_RUNS/01_VERIFIER/VERIFIER_<date>_<runid>.md` per the output 
contract. Do not do any other agent's job."
```

**How to use:**
1. Read the runbook
2. Find the agent invocation template section
3. Copy the exact prompt
4. Replace `<date>` with YYYY-MM-DD and `<runid>` with a run identifier (e.g., WEEKLY, CENSUS, DEEPAUDIT)
5. Paste into Agent tool call
6. Call Agent tool

---

## NAMING CONVENTIONS FOR OUTPUT FILES

All output files follow the CAOS naming standard:

**Agent outputs:**
- Verifier: `VERIFIER_YYYY-MM-DD_[SUFFIX].md`
- Discovery: `DISCOVERY_[LANE]_YYYY-MM-DD_[SUFFIX].md`
- Forward Expectations: `FORWARD_YYYY-MM-DD_[SUFFIX].md`
- Industry Read-through: `INDUSTRY_YYYY-MM-DD_[SUFFIX].md`
- Underwriter: `UNDERWRITER_YYYY-MM-DD_[SUFFIX].md`
- Portfolio Court: `PORTFOLIO_COURT_YYYY-MM-DD_[SUFFIX].md`
- Risk and Survivability: `RISK_YYYY-MM-DD_[SUFFIX].md`
- Red Team: `RED_TEAM_YYYY-MM-DD_[SUFFIX].md`

**Orchestrator outputs:**
- Daily Anchor: `ORCHESTRATOR_YYYY-MM-DD_DAILY.md`
- Weekly Ranking: `ORCHESTRATOR_YYYY-MM-DD_WEEKLY.md` (+ optional `_WEEKLY_RANKINGS_DETAIL.md`)
- Monster Census: `ORCHESTRATOR_YYYY-MM-DD_CENSUS.md`
- Deep Audit: `ORCHESTRATOR_YYYY-MM-DD_DEEPAUDIT.md`
- Event Gate Watch: `EVENT_GATE_WATCH_YYYY-MM-DD_HHmm.md`
- Hunter Watch: `HUNTER_ORCHESTRATOR_YYYY-MM-DD_HHmm.md`
- Learning Review: `LEARNING_REVIEW_YYYY-MM-DD.md`

**Suffix conventions:**
- Leave blank for standard runs (Daily Anchor, Daily work)
- `_WEEKLY` for Weekly Ranking
- `_CENSUS` for Monster Census
- `_DEEPAUDIT` for Deep Audit
- `_DELTA` for Post-Open Delta Check

---

## HANDLING FAILURES & BLOCKED RUNS

Each workflow runbook includes a "Failure States and Recovery" section. Common patterns:

**Precondition BLOCKED — Cannot proceed**
- Master Ledger UNINITIALIZED
- Required prior workflow output missing or >threshold days stale
- **Action:** Fix the blocking condition, then retry

**Degraded data — Can proceed with limitations**
- `DATA LIMITED — portfolio state stale, proceeding in research-only mode`
- `DATA LIMITED — price source unavailable for [TICKER]`
- **Action:** Proceed, note limitation in output, re-run when fresh data available

**Agent failure mid-run**
- An agent crashes, produces unreadable output, or fails its task
- **Action:** Stop the run, fix the failing agent, rerun (do not continue with degraded output)

**Silent failures prohibited**
- Never skip a failed agent and continue as if it succeeded
- Always state explicitly: `BLOCKED`, `DEGRADED`, or reason why
- If run cannot complete, report `[WORKFLOW NAME] INCOMPLETE` with details

---

## INTEGRATING WITH MASTER LEDGER & ACTIVE HANDOFF

### Master Ledger ([[ 01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]])

Every workflow may produce material changes to be logged:
- New Seed/Challenger escalations
- Holdings exited or resized
- System amendments or mandate changes
- Event gates resolved or superseded

**Logging procedure:**
1. Workflow Orchestrator produces output with candidate state changes
2. If changes require logging, output includes `LOG REQUIRED [paste-ready event block]`
3. You copy the event block
4. You paste into Master Ledger §8 (Material CAOS EVENT History)
5. You reply `logged` to confirm

**Never:** Self-modify Master Ledger; only the logged event block becomes official.

### Active Handoff Snapshot ([[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]])

Workflows emit handoff blocks for material state changes:
- New candidate escalations (UNKNOWN → SERIOUS REVIEW → CHALLENGER)
- Evidence gates (expected earnings date, filing deadline)
- Handoff ACKs (confirming consumption of prior handoffs)

**Emission procedure:**
1. Workflow Orchestrator produces handoff blocks per Standardized Handoff Protocol (Operator Manual §9)
2. You copy the handoff blocks
3. You paste into Active Handoff Snapshot relevant section (Event Gates, Hunter Signals, Candidate Escalations)
4. No confirmation needed (unlike Master Ledger); handoff is active on paste

**Only the Orchestrator writes to Active Handoff Snapshot.** Agents never write directly; only propose via Orchestrator.

---

## TIME ESTIMATES FOR PLANNING

| Workflow | Agents | Parallel Calls | Sequential Steps | Est. Total |
|----------|--------|---|---|---|
| Daily Anchor | 9 | 3 parallel groups | 6 sequential | 20–30 min |
| Post-Open Delta | 5 | 1 parallel group | 3 sequential | 10–15 min |
| Weekly Ranking | 9 | 3 parallel groups | 6 sequential | 30–40 min |
| Monster Census | 4 (3 Discovery + Orchestrator) | 3 parallel | 2 sequential | 45–60 min |
| Event Gate Watch | 1–2 (gates + optional NVIDIA) | varies | 2 sequential | 5–15 min |
| Hunter Watch | 1 | N/A | 2 sequential | 10–20 min |
| Deep Audit | 9 | 3 parallel groups | 8 sequential (incl. Ledger audit) | 45–60 min |
| Learning Review | 0 agents (synthesis only) | N/A | 1 (synthesis) | 20–30 min |

**Tips for efficiency:**
- Start your Day Anchor at exactly 18:15; agents will have output by ~18:50–19:00
- If you're running 3+ workflows the same day, start with the shortest (Event Gate Watch, Hunter Watch)
- Monster Census (Sat 09:00) and Weekly Ranking (Sun 10:00) can start immediately after each other (dependencies are satisfied)
- Deep Audit and Learning Review have no time pressure (manual, not scheduled)

---

## QUALITY GATES & SIGN-OFF

Before marking a workflow complete:

1. **All mandatory work items produced** — Check success criteria in runbook
2. **Files written and linked** — Every output file exists, "Inputs Consulted" wikilinks correct
3. **No silent failures** — Run states explicitly PASS / DEGRADED / BLOCKED; never hides failures
4. **Evidence quality labeled** — All claims marked VERIFIED FACT / DATA LIMITED / UNKNOWN
5. **Handoff emissions complete** — Any state changes emit handoff blocks (for Active Handoff paste)
6. **Logging status clear** — Either LOG REQUIRED (with event block) or NO LOG REQUIRED stated
7. **Execution card ready** — If applicable, trades/rebalancing decisions stated and awaiting Mark confirmation

---

## TROUBLESHOOTING QUICK REFERENCE

| Problem | Diagnosis | Fix |
|---------|-----------|-----|
| Precondition check BLOCKS run | Master Ledger UNINITIALIZED, required output missing, data stale | Initialize/update precondition, retry |
| Agent fails mid-run | Agent crash, bad output format, cannot read required inputs | Check agent spec, fix input path, rerun agent (not the whole workflow) |
| Incomplete agent output | Agent ran but didn't produce required sections | Compare to spec output contract; ask agent to re-run with full requirements |
| Conflicting handoffs | New discovery contradicts prior escalation | State contradiction, verify both pieces of evidence, emit new handoff with SUPERSEDES reference |
| Ledger self-audit finds repairs needed | Discrepancies between broker state and Master Ledger | Orchestrator proposes repairs; wait for Mark `logged` confirmation before treating as applied |
| Portfolio state unknown | Broker screenshot stale or unavailable | Provide fresh broker state, re-run Verifier |

---

## NEXT STEPS: AUTOMATION & SCHEDULING

The manual workflows are production-ready now. Future enhancements could include:

1. **Command automation** — Script wrappers for workflow triggers (bash, Python)
2. **Scheduled execution** — Cron jobs or background agents for repeating workflows
3. **Slack/email summaries** — Notify on completed workflow with verdict/action items
4. **Workflow dashboard** — Track execution status, output file locations, pending logs
5. **Ledger watchdog** — Alerts if Master Ledger falls out of sync with broker state

But these are convenience features. **Manual execution is fully functional now** — each workflow is complete, runnable, and integrated into the CAOS system.

---

## Related Documentation

- **Operator Manual:** [[00_START_HERE/CAOS — OPERATOR MANUAL.md]] — Constitutional laws, governance, agent roster
- **Command Card:** [[00_START_HERE/CAOS — COMMAND CARD.md]] — Quick status reference (ACTIVE, NOT YET BUILT, IMPLEMENTATION IN PROGRESS)
- **Individual Runbooks:** `06_PRODUCT_RUNBOOKS/[Workflow Name].md`
- **Master Ledger:** [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — Portfolio state, event history
- **Active Handoff Snapshot:** [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] — Current signals, gates, escalations
- **Flight Recorder:** [[04_FLIGHT_RECORDER/README — Flight Recorder]] — Monthly portfolio snapshots and decision logs
- **Agent Specifications:** `03_AGENT_RUNS/[Agent]/` — Full spec files for each specialist

---

## Version History

- **2026-09-09:** Complete manual workflows execution guide created
  - All 8 workflows now fully runnable (Daily Anchor + 7 others)
  - Standardized runbook format with precondition checks, work items, agent sequences, output contracts
  - Integration with Master Ledger and Active Handoff Snapshot documented
  - Failure handling and recovery procedures outlined
  - Time estimates and efficiency tips provided
  - This execution manual created as central reference

---

**You are now ready to execute any CAOS workflow manually.** Start with Daily Anchor (Mon–Fri 18:15), and expand to weekly/monthly workflows as needed. Each runbook is self-contained and designed to be followed step-by-step.

For questions on specific workflows, reference the individual runbook. For system-level questions, refer to the Operator Manual. For governance and portfolio state, refer to the Master Ledger.

Good luck!
