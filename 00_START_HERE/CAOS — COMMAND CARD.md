# CAOS — Command Card

| Command | Status | Runbook |
|---|---|---|
| `Run CAOS Daily Anchor` | ACTIVE (proven — real run 2026-08-29) | [[06_PRODUCT_RUNBOOKS/Daily Anchor]] |
| `Run CAOS Post-Open Delta Check` | BUILT, UNPROVEN — no real run on record despite the label; needs a real execution before trusting it | [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check]] |
| `Run CAOS Emergency Thesis Rerun: <ticker/event>` | BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real | [[06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun]] |
| `Prepare CAOS DCA Execution Card` | BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real | [[06_PRODUCT_RUNBOOKS/DCA Execution Card]] |
| `Run CAOS Monster Census` | BUILT, UNPROVEN — agent specs complete; the only "run" on record was a fabricated narrative walkthrough, now quarantined in [[04_FLIGHT_RECORDER/README — Flight Recorder]] | [[06_PRODUCT_RUNBOOKS/Monster Census]] |
| `Run CAOS Weekly Ranking` | BUILT, UNPROVEN — same situation as Monster Census | [[06_PRODUCT_RUNBOOKS/Weekly Ranking]] |
| `Run CAOS Deep Audit` | BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Run CAOS Learning Review` | BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real; also blocked until a real Deep Audit + Flight Recorder entry exist | [[06_PRODUCT_RUNBOOKS/Learning Review]] |
| `Audit CAOS Master Ledger` | Covered by Deep Audit | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Reconcile CAOS portfolio from this screenshot` | ACTIVE (ad hoc) — this is how the 2026-08-31 intake and the 2026-09-02 cash correction were both done; no dedicated runbook, just read the newest screenshot against [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] and reconcile | — |
| `Show active CAOS handoffs` | ACTIVE | Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] directly — no agent pipeline needed |
| `Show CAOS task health` | N/A | No scheduled tasks configured in this build |

**Run CAOS Daily Anchor** is the only product with a real, verified end-to-end run behind its label. Every other product row above marked `BUILT, UNPROVEN` has a written runbook that has never actually been executed through the Agent tool — do not treat the existence of a runbook, or any file sitting in `03_AGENT_RUNS/`, as proof a real run happened. Verify a run's "Inputs Consulted" links actually resolve to files that exist before trusting it.

## Background Watches

These two products run as background watches in the source design, not manual commands, so they have no Command Card row above — link to them directly instead:
- [[06_PRODUCT_RUNBOOKS/Event Gate Watch]] — BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real
- [[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]] — BUILT, UNPROVEN — runbook written 2026-09-02, never executed for real
