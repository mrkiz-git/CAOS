# CAOS — Event Gate Watch

**Command:** (automated watch — no manual trigger phrase in the source doc; invoke by typing `Run CAOS Event Gate Watch`)
**Status:** VALIDATED — executed for real 2026-09-03, 2 gates checked and advanced (see [[03_AGENT_RUNS/09_ORCHESTRATOR/EVENT_GATE_WATCH_2026-09-03]])
**Default schedule (inactive):** daily at 02:00, Mark's confirmed timezone — not configured; run manually

## What this does
Reads active event gates from the Active Handoff Snapshot and runs a post-event review only after the actual release, filing, presentation, or call material exists — a pre-release Anchor never satisfies a post-results gate. Also runs the permanent NVIDIA gate whenever new NVIDIA earnings, CFO commentary, 10-Q, call material, or materially updated guidance appears, regardless of whether NVIDIA has an open event gate.

## Precondition check
Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] "Event Gates" section. If it's empty and no NVIDIA material has appeared since the last check, this run is a heartbeat only — see Required output.

## Agent call sequence
1. For each open event gate in the Active Handoff Snapshot: call the Agent tool once per gate with this task: "Check whether real release/filing/presentation/call material now exists for `<gate description>` (expected: `<trigger event/deadline from the handoff>`). If a full transcript is unavailable, state `TRANSCRIPT PENDING` and distinguish confirmed release facts from incomplete call evidence — never fill the gap with inference presented as fact. If the material exists, summarize it and state whether it resolves, triggers, or leaves the gate open." Independent gates may run in the same turn (parallel Agent tool calls).
2. Separately, check whether new NVIDIA earnings, CFO commentary, 10-Q, call material, or materially updated guidance has appeared since the last Event Gate Watch run (or since the last Industry Read-through run touched it). If so, call the Agent tool once using the invocation prompt template from [[03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through]], specifically for the Permanent NVIDIA Gate: Data Center/Hyperscale demand; Blackwell and Vera Rubin demand, supply and ramp; networking, optics and memory; land, power, shell and financing constraints; China assumptions; gross margin; forward guidance; read-through to economically connected CAOS holdings and challengers.
3. Perform the Orchestrator role directly (primary session): consolidate every gate check and the NVIDIA gate result (if triggered) into one output. Update the Active Handoff Snapshot's Event Gates section for any gate that resolved or triggered, per the Standardized Handoff Protocol (Operator Manual §9).

## Required output
```
EVENT GATE WATCH: [N] gates checked, [M] resolved/triggered / NO NEW EVENT GATE
[per checked gate:]
- GATE — STATUS (RESOLVED / TRIGGERED / STILL PENDING / TRANSCRIPT PENDING)
NVIDIA GATE = TRIGGERED THIS RUN [summary] / NOT TRIGGERED THIS RUN
LOG REQUIRED / NO LOG REQUIRED
```
If nothing is open and NVIDIA has no new material, output the compact `NO NEW EVENT GATE` heartbeat line above — do not fabricate a finding to have something to report.

## Constraints
- Never run a post-event review on a pre-release Anchor or forecast — only actual released material counts.
- Separate verified fact, inference, and unknown at all times; strong industry-level NVIDIA evidence never automatically proves a specific connected issuer's utilization, economics, financing, dilution, or execution.
- Never duplicate a prior event — if nothing changed since the last check, say so plainly.
- Never writes to the Master Ledger directly.

## Failure handling
If the Active Handoff Snapshot is unreadable, state `EVENT GATE WATCH BLOCKED — Active Handoff Snapshot unavailable` rather than silently skipping the check.
