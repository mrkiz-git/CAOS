# CAOS — Monster Census

**Command:** `Run CAOS Monster Census`
**Status:** IMPLEMENTATION IN PROGRESS (Agent specs complete; scheduling and integration pending)
**Default schedule (inactive):** Saturday 09:00, Mark's confirmed timezone

## What this product will do
A weekly deep-discovery sweep: consumes all active handoffs first, reconciles External Hunter intake, searches at least 40 public companies across at least 5 buckets with at least 8 genuinely fresh names, ranks a Top-5 fresh/external-capital board, fully underwrites the Top 1–2 plus every active High-Priority Challenger plus one Anti-Echo fresh candidate, resolves every serious review to Seed/Challenger/Watch/Reject, and maintains a Conversion Scoreboard (Scanned → Serious Review → Monster File → Seed → Buy-Authorized → Purchased → Winner/Failure). Labels `SEARCH INCOMPLETE` when the search budget is missed, and triggers a Discovery Meta-Audit if 30 active Census days produce zero new buy-authorized candidates.

## Implementation Architecture

This product uses a specialized multi-agent approach with three parallel Discovery agents and a consolidating Orchestrator:

### Discovery Agents
1. [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery AI-Power-Cooling]] — AI infrastructure, power, cooling, networking
2. [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery Semiconductors-Memory]] — Semiconductors, memory, equipment, devices
3. [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery Defense-Autonomy]] — Defense, autonomy, quantum, batteries, biotech, other

### Orchestrator
- [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Census)]] — Consolidation, ranking, underwriting, handoff emission

See [[06_PRODUCT_RUNBOOKS/Monster Census Design.md]] for the full architecture specification.

## Execution Procedure

### Before Running Census

1. Verify Daily Anchor has completed for this week (to consume active handoffs)
2. Verify Master Ledger is current with latest portfolio state
3. Confirm all three Discovery agent specs are ready

### Running the Census

**Step 1: Invoke Discovery Agent A** (in Agent tool)
- Use the prompt from [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery AI-Power-Cooling#AGENT PROMPT]]
- Output will be: `DISCOVERY_INFRA_POWER_YYYY-MM-DD_CENSUS.md`

**Step 2: Invoke Discovery Agent B** (in Agent tool)
- Use the prompt from [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery Semiconductors-Memory#AGENT PROMPT]]
- Output will be: `DISCOVERY_CHIPS_MEMORY_YYYY-MM-DD_CENSUS.md`

**Step 3: Invoke Discovery Agent C** (in Agent tool)
- Use the prompt from [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery Defense-Autonomy#AGENT PROMPT]]
- Output will be: `DISCOVERY_DEFENSE_AUTONOMY_YYYY-MM-DD_CENSUS.md`

**Step 4: Invoke Orchestrator** (primary session, after all three agents complete)
- Use the prompt from [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator (Census)#ORCHESTRATOR PROMPT]]
- Output will be: `ORCHESTRATOR_YYYY-MM-DD_CENSUS.md`

**Step 5: Review Orchestrator output**
- Check search completeness grade: SEARCH COMPLETE or SEARCH INCOMPLETE
- Review Monster Files for Top 1–2 + High-Priority Challengers
- Review Conversion Scoreboard (Scanned → Serious Review → Monster File → Seed → Purchased)
- Check for handoff emissions and Master Ledger event

**Step 6: Log if required**
- If event block is present, copy it to Master Ledger and reply `logged` to confirm
- If NO LOG REQUIRED, proceed without additional logging

### Acceptance Checklist

- [ ] All three Discovery agents completed and files saved
- [ ] Orchestrator read all three agent files and acknowledged in "Inputs Consulted"
- [ ] Search completeness: SEARCH COMPLETE or SEARCH INCOMPLETE with disclosure
- [ ] At least 40 companies scanned, 8+ fresh names, 5+ lanes covered
- [ ] Top-5 ranking produced
- [ ] Monster Files completed for Top 1–2, all High-Priority Challengers, and Anti-Echo candidate
- [ ] Every serious review resolved to terminal state (Seed/Challenger/Watch/Reject)
- [ ] Handoff ACK checks for every Daily Anchor handoff
- [ ] Conversion Scoreboard emitted
- [ ] Master Ledger event produced (LOG REQUIRED) or NO LOG REQUIRED stated
- [ ] All files linked in "Inputs Consulted" and "Full Run Map"

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#14. Monster Census specification]]
