# CAOS — Command Card

| Command | Status | Runbook |
|---|---|---|
| `Run CAOS Daily Anchor` | ACTIVE | [[06_PRODUCT_RUNBOOKS/Daily Anchor]] |
| `Run CAOS Post-Open Delta Check` | ACTIVE (ad hoc, intraday after Daily Anchor completes) | [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check]] |
| `Run CAOS Emergency Thesis Rerun: <ticker/event>` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun]] |
| `Prepare CAOS DCA Execution Card` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/DCA Execution Card]] |
| `Run CAOS Monster Census` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Monster Census]] |
| `Run CAOS Weekly Ranking` | IMPLEMENTATION IN PROGRESS | [[06_PRODUCT_RUNBOOKS/Weekly Ranking]] |
| `Run CAOS Deep Audit` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Run CAOS Learning Review` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Learning Review]] |
| `Audit CAOS Master Ledger` | NOT YET BUILT | Covered by Deep Audit once built |
| `Reconcile CAOS portfolio from this screenshot` | NOT YET BUILT | Portfolio intake workflow — not built this pass |
| `Show active CAOS handoffs` | ACTIVE | Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] directly — no agent pipeline needed |
| `Show CAOS task health` | N/A | No scheduled tasks configured in this build |

**Run CAOS Daily Anchor** executes the full 9-agent pipeline, and **Run CAOS Post-Open Delta Check** executes a 5-agent subset intraday, gated on a same-day Daily Anchor having already completed — see its runbook's Precondition Check. "Show active CAOS handoffs" works today too, since it is just reading a file. Every other command either returns its stub's "not yet built" content or has no product to run yet.

## Background Watches

These two products run as background watches in the source design, not manual commands, so they have no Command Card row above — link to them directly instead:
- [[06_PRODUCT_RUNBOOKS/Event Gate Watch]] — NOT YET BUILT
- [[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]] — NOT YET BUILT
