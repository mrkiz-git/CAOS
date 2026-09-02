# CAOS — DCA Execution Card

**Command:** `Prepare CAOS DCA Execution Card`
**Status:** IMPLEMENTATION IN PROGRESS — runbook written, never yet executed for real
**Default schedule (inactive):** shortly after Mark's confirmed monthly contribution date, once task capacity permits; otherwise manual whenever Mark says new cash is available

## What this does
Decides where the next uncommitted euro of fresh contribution cash should go — reinforce an existing position, fund a new Seed, recycle capital out of a weaker holding, or hold cash — and only when a candidate clears the minimum edge. This is not automatic equal feeding: it must never deploy simply because the calendar says DCA day.

## Precondition check
Before starting, require: a current broker screenshot or export; confirmed real unlevered cash by currency (per [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL#3. Real Cash vs. Buying Power]]); any recent buys, sells, deposits, withdrawals, or fills not yet reflected in the Ledger; current verified prices and market status; the broker's whole-share/fractional-share support; FX, brokerage-fee, and spread awareness. If the Ledger is `UNINITIALIZED` or stale, state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` and stop — this product cannot run in degraded mode, unlike Daily Anchor.

## Agent call sequence
1. Call the Agent tool once for the Verifier, using [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]], to reconcile current cash and prices.
2. Call the Agent tool twice in the same turn — Forward Expectations ([[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]) and Industry Read-through ([[03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through]]) — for the market-temperature and event-risk check (is anything about to report earnings, face a catalyst, or sit in a blackout window that argues for waiting).
3. Call the Agent tool once for the Underwriter, using [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]], for a thesis-integrity check on every funded position and the strongest live Seed/Challenger candidates.
4. Call the Agent tool once for Portfolio Court, using [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court]], for the next-uncommitted-euro ranking: compare reinforcing an existing position, funding a new Seed, recycling capital out of a weaker holding, and holding cash.
5. Perform the Orchestrator role directly (primary session): apply the minimum-edge filter, select one target (two maximum, unless Mark explicitly authorizes a basket), and produce the Required output below.

## Required output
```
CAOS DCA CARD: BUY | PARTIAL DEPLOY | HOLD CASH | REVIEW
1. TICKER — ACTION — exact shares only when execution-ready
2. Optional second ticker
Ammo to use/keep =
Expected leftover cash =
Verified prices/source/time =
Why this beats alternatives =
Next trigger =
Execution note = Mark decides and executes
LOG REQUIRED / NO LOG REQUIRED
```
State `DO NOTHING / HOLD CASH` explicitly when no candidate clears the minimum edge — this is a valid, expected outcome, not a failure of the run.

## Constraints
- No autonomous trades, ever; no exact buy sizing without a live verified price and confirmed real cash (Operator Manual §12).
- No fractional-share assumption unless the broker explicitly supports it and Mark confirms (per Master Ledger §1: Revolut does support fractional shares for this account).
- No margin or leverage.
- Never treat the calendar date alone as a reason to deploy.
- Never writes to the Master Ledger directly — only the Orchestrator proposes the event, and only Mark's `logged` confirms it.

## Failure handling
If any precondition is missing (stale Ledger, no current cash figure, no live prices), state exactly what's missing and stop — do not produce a card built on stale or assumed inputs.
