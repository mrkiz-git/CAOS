# CAOS — Active Handoff Snapshot

This is the live, unresolved cross-module queue — not the holdings ledger. It contains only active, unresolved items. Never erase an unresolved item created by another module; resolve or supersede it explicitly.

## Operating Rules
- Handoff format: see [[CAOS — OPERATOR MANUAL#9. Standardized Handoff Protocol]]
- Every consumer must output an ACK check when it reads a handoff here.
- Only the Orchestrator updates this file, and only when authorized and verified.

## Active Hunter Signals
None.

## Challengers
None.

## Seeds
None.

## Trigger Watches
None.

## Event Gates
None.

## Tribunals
None.

## Source Status
No source readiness data yet — will be populated by the Verifier agent's first run.

## Acknowledgements
None.

## Last Writer
None — file not yet updated by any run.

<!-- Individual handoffs get their own heading below, in the form:
## HANDOFF_ID
(full handoff block per the Operator Manual's Standardized Handoff Protocol section)
-->
