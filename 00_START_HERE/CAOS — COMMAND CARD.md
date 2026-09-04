# CAOS — Command Card

| Command | Status | Runbook |
|---|---|---|
| `Run CAOS Daily Anchor` | VALIDATED — real runs 2026-08-29, 2026-09-02 | [[06_PRODUCT_RUNBOOKS/Daily Anchor]] |
| `Run CAOS Post-Open Delta Check` | VALIDATED — real run 2026-09-03; correctly returned BLOCKED (no same-day Anchor) once the precondition wasn't met | [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check]] |
| `Run CAOS Emergency Thesis Rerun: <ticker/event>` | VALIDATED — real run 2026-09-03 on TSLA (Cybercab launch trigger), verdict DEGRADED | [[06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun]] |
| `Prepare CAOS DCA Execution Card` | VALIDATED — real run 2026-09-03, resolved HOLD CASH | [[06_PRODUCT_RUNBOOKS/DCA Execution Card]] |
| `Run CAOS Monster Census` | VALIDATED — real run 2026-09-03, first-ever; the prior fabricated narrative walkthrough remains quarantined in [[04_FLIGHT_RECORDER/README — Flight Recorder]] for reference only | [[06_PRODUCT_RUNBOOKS/Monster Census]] |
| `Run CAOS Weekly Ranking` | VALIDATED — real run 2026-09-03; found the numeric ranking mechanism structurally blocked (no candidate anywhere carries a numeric score) and substituted qualitative ordering | [[06_PRODUCT_RUNBOOKS/Weekly Ranking]] |
| `Run CAOS Deep Audit` | VALIDATED — real run 2026-09-03, first post-intake review; confirmed PLTR/NVDA sizing overage, Ledger event LOG REQUIRED pending Mark's review | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Run CAOS Learning Review` | VALIDATED (precondition path only) — real run 2026-09-03, correctly returned BLOCKED (no Mark-reviewed Deep Audit/Flight Recorder entry exists yet); the review logic itself remains unexercised until that precondition clears | [[06_PRODUCT_RUNBOOKS/Learning Review]] |
| `Audit CAOS Master Ledger` | Covered by Deep Audit | [[06_PRODUCT_RUNBOOKS/Deep Audit]] |
| `Reconcile CAOS portfolio from this screenshot` | ACTIVE (ad hoc) — this is how the 2026-08-31 intake and the 2026-09-02 cash correction were both done; no dedicated runbook, just read the newest screenshot against [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] and reconcile | — |
| `Show active CAOS handoffs` | ACTIVE | Read [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] directly — no agent pipeline needed |
| `Show CAOS task health` | N/A | No scheduled tasks configured in this build |

Every product above now has at least one real, verified end-to-end run behind its label — verify a run's "Inputs Consulted" links actually resolve to files that exist before trusting any of them; do not treat the existence of a runbook, or any file sitting in `03_AGENT_RUNS/`, as proof by itself. One real run each is a floor, not a ceiling: several products (Learning Review's review logic, Event Gate Watch and Hunter Watch's steady-state cadence, every product's behavior across a wider range of market conditions) have only been exercised once and should not be assumed robust beyond what that single run actually tested.

## Background Watches

These two products run as background watches in the source design, not manual commands, so they have no Command Card row above — link to them directly instead:
- [[06_PRODUCT_RUNBOOKS/Event Gate Watch]] — VALIDATED — real run 2026-09-03, 2 gates checked and advanced (WULF/IREN credit gate narrowed via a first-ever direct primary-source read; TSLA Optimus/Cybercab gate partially resolved)
- [[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]] — VALIDATED — real run 2026-09-03, first-ever; correctly returned NO NEW SIGNALS rather than fabricating one
