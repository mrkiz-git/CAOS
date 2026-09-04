# CAOS — Emergency Thesis Rerun

**Command:** `Run CAOS Emergency Thesis Rerun: <ticker/event>`
**Status:** VALIDATED — executed for real 2026-09-03 on TSLA (Cybercab launch trigger), verdict DEGRADED (see [[03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_2026-09-03_TSLA_EMERGENCY]])
**Default schedule (inactive):** ad hoc, triggered by Mark after material news

## What this does
Reruns the underwriting pipeline for one specific holding or candidate after material earnings, financing, contract, regulatory, or thesis evidence appears — not for generic price volatility alone. A targeted re-underwriting of one ticker, not a full portfolio Anchor. Distinct from Post-Open Delta Check (which is price-move-triggered and portfolio-wide) and from Daily Anchor (which is the full scheduled pipeline) — see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#21. Product distinctions]].

## Precondition check
Requires Mark to name both a ticker and the material event/evidence that triggered the request (e.g. `Run CAOS Emergency Thesis Rerun: NVDA — Q3 earnings beat + raised guidance`). If only a ticker is given with no stated trigger, ask what material evidence prompted the rerun before proceeding — price direction alone is never sufficient grounds (Operator Manual §12).

## Agent call sequence
Full-depth re-underwriting of one ticker, using the same specs as Daily Anchor but scoped to a single security throughout.

1. Call the Agent tool once for the Verifier ([[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]]), scoped to just this ticker's current price, timestamp, and market status.
2. Call the Agent tool once for Forward Expectations ([[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]), instructed to focus entirely on the stated triggering event and extract every forward-looking statement it contains.
3. Call the Agent tool once for the Underwriter ([[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]]), instructed to produce a full fresh Monster File for this one ticker — not a lightweight delta check. This is the key difference from Post-Open Delta Check.
4. Call the Agent tool once for Risk and Survivability ([[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability]]), recalculating survival for this ticker against the new evidence.
5. If this ticker is a funded holding, also call the Agent tool for Portfolio Court ([[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court]]) to re-validate its thesis and role. Skip this step for a candidate that isn't yet funded.
6. Perform the Orchestrator role directly (primary session): reconcile all outputs into one verdict for this ticker, explicitly stating the conviction change (if any) versus its prior state in the Master Ledger or Active Handoff Snapshot.

## Required output
```
EMERGENCY THESIS RERUN: TICKER
TRIGGER: [the material event Mark named]
PRIOR STATE: [conviction/role before this rerun]
NEW STATE: [conviction/role after this rerun]
THESIS VERDICT: INTACT | STRENGTHENED | DEGRADED | CHALLENGED | INVALIDATED
KILL CONDITIONS: [status]
RECOMMENDATION: [for Mark's decision — never an executed action]
LOG REQUIRED / NO LOG REQUIRED
```

## Constraints
- Triggered only by material evidence (earnings, financing, contract, regulatory, thesis-changing news) — never by price volatility alone.
- Full re-underwriting depth for the one named ticker — do not silently downgrade this into a lightweight delta check.
- No autonomous trades, sizing, or fills.
- Never writes to the Master Ledger directly — only the Orchestrator proposes the event, and only Mark's `logged` confirms it.

## Failure handling
If the named ticker isn't a real, resolvable security, or if no material trigger is stated, stop and ask rather than guessing at what Mark meant.
