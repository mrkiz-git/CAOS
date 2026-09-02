# CAOS — Deep Audit

**Command:** `Run CAOS Deep Audit`
**Status:** IMPLEMENTATION IN PROGRESS — runbook written, never yet executed for real
**Default schedule (inactive):** manual only, recommended monthly

## What this does
The full portfolio re-underwrite: rebuild the portfolio from a 100%-cash starting assumption, without anchoring on existing holdings, and re-underwrite the mandate, market regime, holdings, Seeds, Challengers, and cash using the full multi-agent pipeline. Tests every funded position for inclusion, sizing role, proof gate, and replacement, and produces a complete next-euro capital map. Also audits the Master Ledger itself — not just the portfolio it describes.

## Precondition check
Read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]. Unlike Daily Anchor, Deep Audit does not degrade gracefully if the Ledger is `UNINITIALIZED` — the whole point is auditing real holdings. If uninitialized, state `DEEP AUDIT BLOCKED — Ledger not initialized` and stop.

## Agent call sequence
Identical structure to Daily Anchor's full 9-agent pipeline (see [[06_PRODUCT_RUNBOOKS/Daily Anchor#Agent call sequence]]), with two differences: each specialist is explicitly instructed to test from a 100%-cash-first frame rather than assuming current holdings are correct, and the Orchestrator step additionally performs a Ledger self-audit (step 7 below).

1. Verifier — [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]].
2. Discovery, Forward Expectations, Industry Read-through in parallel — same specs as Daily Anchor, each told explicitly: "This is a Deep Audit. Do not treat any current holding as pre-approved or exempt from full re-discovery and re-underwriting."
3. Underwriter — [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]], instructed to produce a fresh Monster File for every funded holding (not just new candidates), testing inclusion, sizing role, proof gate, and replacement risk for each.
4. Portfolio Court and Risk and Survivability in parallel — same specs as Daily Anchor, each explicitly running the 100%-cash rebuild: "if all capital were cash today, would you buy every current holding back at its current size, weight, or role?"
5. Red Team — [[03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team]], stress-testing the rebuilt portfolio specifically for incumbency bias (holdings kept only because they're already owned).
6. Perform the Orchestrator role directly (primary session): consolidate everything into a next-euro capital map covering every funded position and top candidates.
7. **Ledger self-audit** (Orchestrator, same step): reconcile the Master Ledger against the freshest broker state (from Verifier's output); test §1–§10 of the Ledger for missing material logs, duplicates, contradictions, stale timestamps, and broken supersession chains. Never treat an unconfirmed proposed correction as already logged. If repairs are needed, give Mark one combined repair block and require his reply `logged` before treating any repair as applied.

## Required output
```
DEEP AUDIT VERDICT: [summary]
NEXT-EURO CAPITAL MAP: [ranked table — every funded position + top candidates, each with INCLUDE/RESIZE/REPLACE/EXIT verdict and why]
LEDGER SELF-AUDIT: [PASS / FINDINGS — list each finding with exact section and proposed repair]
INCUMBENCY BIAS CHECK (Red Team): [PASS / FAIL — findings]
LOG REQUIRED [combined event + any ledger repair block] / NO LOG REQUIRED
```

## Constraints
- Every holding must be re-justified from a 100%-cash frame — "we already own it" is never sufficient justification on its own.
- Never silently rewrite Ledger history — every correction states what was corrected, why, and what prior entry is superseded (per the Ledger's own append-only rule).
- No autonomous trades, sizing, or fills — INCLUDE/RESIZE/REPLACE/EXIT verdicts are recommendations for Mark, never executed instructions.
- After Mark reviews the result, the Deep Audit is what triggers the monthly Flight Recorder entry (see [[04_FLIGHT_RECORDER/README — Flight Recorder]]) — do not create a Flight Recorder entry before that review happens.

## Failure handling
If any agent call fails, report `DEEP AUDIT INCOMPLETE` stating exactly what completed and what didn't — never present a partial audit as a full one.
