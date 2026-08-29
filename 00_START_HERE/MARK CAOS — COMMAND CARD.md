# MARK CAOS — Command Card

| Command | Status | Runbook |
|---|---|---|
| `Run MARK CAOS Daily Anchor` | ACTIVE | [[06_PRODUCT_RUNBOOKS/Daily Anchor]] |
| `Run MARK CAOS Post-Open Delta Check` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check]] |
| `Run MARK CAOS Emergency Thesis Rerun: <ticker/event>` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun]] |
| `Prepare MARK CAOS DCA Execution Card` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/DCA Execution Card]] |
| `Run MARK CAOS Monster Census` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Monster Census]] |
| `Run MARK CAOS Weekly Ranking` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Weekly Ranking]] |
| `Run MARK CAOS Deep Audit` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Run MARK CAOS Learning Review` | NOT YET BUILT | [[06_PRODUCT_RUNBOOKS/Learning Review]] |
| `Audit MARK CAOS Master Ledger` | NOT YET BUILT | Covered by Deep Audit once built |
| `Reconcile MARK CAOS portfolio from this screenshot` | NOT YET BUILT | Portfolio intake workflow — not built this pass |
| `Show active MARK CAOS handoffs` | ACTIVE | Read [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]] directly — no agent pipeline needed |
| `Show MARK CAOS task health` | N/A | No scheduled tasks configured in this build |

Only **Run MARK CAOS Daily Anchor** executes a full multi-agent pipeline in this build. "Show active MARK CAOS handoffs" works today too, since it is just reading a file. Every other command either returns its stub's "not yet built" content or has no product to run yet.
