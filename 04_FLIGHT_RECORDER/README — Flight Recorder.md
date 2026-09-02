# CAOS — Flight Recorder

STATUS: No real Deep-Audit-generated entries yet.

The Flight Recorder stores consolidated lessons, predictions, errors, false positives, false negatives, ranking changes, unresolved investigations, action queues, and architecture lessons. It does not replace the Master Ledger.

It is created monthly by the Deep Audit product (see [[06_PRODUCT_RUNBOOKS/Deep Audit]], status: NOT YET BUILT) after Mark reviews a completed Deep Audit result. No real Flight Recorder entries exist until that product is built and run.

## What else lives in this folder
- **Dry-run test plans** (`Weekly Ranking Dry-Run Test`, `Monster Census Dry-Run Test`, `Post-Open Delta Check Dry-Run Test`) — written test procedures for validating those products once run for real. As of 2026-09-02 none has actually been executed (their result fields are still `TBD`).
- **`ORCHESTRATOR_... (NON-CANONICAL — never executed).md` files** — narrative walkthroughs of what a Weekly Ranking / Monster Census run might look like, written directly instead of produced by a real Agent-tool pipeline run. Moved here from `03_AGENT_RUNS/09_ORCHESTRATOR/` on 2026-09-02 after audit found their cited upstream specialist files don't exist and at least one contains a fabricated figure (a portfolio NAV off by ~430x from the real Master Ledger). Kept for reference only — do not treat them as evidence either product works.
