# CAOS — Multi-Bagger Hunter Watch

**Command:** `Run CAOS Multi-Bagger Hunter Watch` (background watch — no scheduler configured this pass; invoke manually by typing the command)
**Status:** VALIDATED — executed for real 2026-09-03, NO NEW SIGNALS (see [[03_AGENT_RUNS/02_DISCOVERY/HUNTER_2026-09-03_1500]])
**Default schedule (inactive):** daily condition watch, at most hourly, Mark's confirmed timezone

## What this does
Scans external long-duration scout sources for materially new or changed high-conviction signals, independently verifies the underlying company evidence, and resolves each qualified signal to a candidate state. External sources are scouts only — never authority (Operator Manual §6). A signal with no material change produces no artificial escalation and no duplicate event.

## Precondition check
Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] "Active Hunter Signals" section first, so a source's prior recommendation isn't re-escalated as new.

## Sources watched
When accessible via web search/fetch:
- Motley Fool Stock Advisor / Rule Breakers / high-conviction lists
- Seeking Alpha Alpha Picks / high-confidence Quant ideas
- IBD 50 changes / Stock of the Day when material
- Notable TipRanks elite-analyst initiations, reiterations, or high-conviction signals
- Other sources Mark admits later

## Deduplication key
`SOURCE + TICKER + RECOMMENDATION_OR_CHANGE_DATE` — check this against the Active Handoff Snapshot's existing Hunter Signals before treating anything as new.

## Agent call sequence
This is a single-agent watch, not the full 9-agent pipeline — no dedicated agent spec file exists for this role since its scope is narrow and self-contained.

1. Call the Agent tool once with this task: "Search the watched sources above for materially new or changed high-conviction signals since the last recorded Hunter signal (check [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] Active Hunter Signals for what's already tracked, using the dedup key `SOURCE+TICKER+RECOMMENDATION_OR_CHANGE_DATE`). For each new signal, independently verify the underlying company evidence (official IR, SEC filings, primary reporting — never accept the scout source's claim at face value). Label all evidence per Operator Manual §6. Do not escalate a signal that lacks independent verification. Write findings to `03_AGENT_RUNS/02_DISCOVERY/HUNTER_YYYY-MM-DD_HHmm.md` with an Inputs Consulted section, a table of sources checked, and one line per new signal with its verification status. If nothing new was found, state that explicitly — do not fabricate a signal to justify the run."
2. Perform the Orchestrator role directly (primary session, no subagent): read the Hunter agent's output, resolve each qualified signal to exactly one state (`HIGH-PRIORITY CHALLENGER`, `CHALLENGER`, `WATCH WITH SPECIFIC TRIGGER`, or `REJECT`), and if authorized and verified, add it to the Active Handoff Snapshot's "Active Hunter Signals" section using the Standardized Handoff Protocol (Operator Manual §9).

## Required output
```
HUNTER WATCH: NEW SIGNALS FOUND [N] / NO NEW SIGNALS
[per new signal:]
- TICKER — SOURCE — SIGNAL_DATE — independent verification: [summary] — RESOLVED STATE: [state]
LOG REQUIRED / NO LOG REQUIRED
```
If the platform requires a visible result even when nothing changed, this line itself (`NO NEW SIGNALS`) is that heartbeat — never invent a signal just to have something to report.

## Constraints
- Never treat an external scout recommendation as authority — independent verification is mandatory before escalation past `WATCH WITH SPECIFIC TRIGGER`.
- Never duplicate a signal already in the Active Handoff Snapshot under the same dedup key.
- Never writes to the Master Ledger directly — only the Orchestrator step may propose an Active Handoff Snapshot update, and only when verified.

## Failure handling
If the search agent's sources are all unreachable, state `HUNTER WATCH DEGRADED — no sources reachable` rather than a silent empty result.
