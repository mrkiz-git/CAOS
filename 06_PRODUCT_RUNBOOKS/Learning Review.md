# CAOS — Learning Review

**Command:** `Run CAOS Learning Review`
**Status:** VALIDATED (precondition path only) — executed for real 2026-09-03, correctly returned LEARNING REVIEW BLOCKED (no Mark-reviewed Deep Audit/Flight Recorder entry exists yet); the review logic itself has not been exercised (see [[03_AGENT_RUNS/09_ORCHESTRATOR/LEARNING_REVIEW_2026-09-03]])
**Default schedule (inactive):** monthly, after a completed Deep Audit and Flight Recorder entry — third day of the month at 10:00, Mark's confirmed timezone, if task capacity permits

## What this does
Uses the Master Ledger, Flight Recorder, prior rankings, and available outcomes to assess what the system got right or wrong — not to re-underwrite anything. May recommend system changes; must never implement a constitutional or architectural amendment without Mark's explicit approval.

## Precondition check
Requires at least one completed Deep Audit with a Flight Recorder entry Mark has reviewed (see [[06_PRODUCT_RUNBOOKS/Deep Audit]] and [[04_FLIGHT_RECORDER/README — Flight Recorder]]). If neither exists yet, state `LEARNING REVIEW BLOCKED — no Deep Audit / Flight Recorder entry to review yet` and stop.

## Agent call sequence
This is a synthesis product, not a discovery/underwriting pipeline — it reads what already exists rather than generating new research. No specialist Agent-tool calls are required by default.

1. Perform the review directly (primary session): read the Master Ledger's full event history (§8), the Flight Recorder, and every prior dated Orchestrator output referenced from Active Handoff history.
2. If a specific claim needs outside verification (e.g. confirming whether a predicted catalyst actually occurred), call the Agent tool as needed for that one fact-check — do not spin up the full roster for this.
3. Assess, with evidence for each: predictions that were right or wrong; good processes with bad outcomes and bad processes with good outcomes; false positives and false negatives; missed candidates and omitted handoffs; evidence-quality failures; stale gates and unclosed investigations; ranking drift and incumbency bias; execution errors (cash/FX/fee mistakes, assumed fills); notification/scheduling/linkage failures; whether CAOS is drifting too institutional, too conservative, too speculative, too concentrated without edge, or too diversified without purpose; and any architecture changes the evidence actually supports.

## Required output
```
LEARNING REVIEW: [period covered]
RIGHT CALLS: [list with evidence]
WRONG CALLS: [list with evidence — including good-process/bad-outcome and bad-process/good-outcome cases, kept distinct]
SYSTEM HEALTH: [drift assessment — institutional/conservative/speculative/concentrated/diversified, each with evidence or NONE OBSERVED]
RECOMMENDED CHANGES: [each stated as a proposal for Mark to approve — never self-implemented]
LOG REQUIRED [only if Mark approves an amendment — logged as a Master Ledger system event] / NO LOG REQUIRED
```

## Constraints
- Never implement a constitutional (Operator Manual §3) or architectural amendment without Mark's explicit approval first.
- Every approved amendment gets its own Master Ledger system event — never bundled silently into an unrelated log.
- Distinguish "good process, bad outcome" from "bad process" explicitly — Process Over Outcome (Operator Manual §3) applies here directly.

## Failure handling
If the Master Ledger or Flight Recorder is unreadable, state `LEARNING REVIEW DEGRADED — [what's missing]` rather than reviewing from memory or assumption.
