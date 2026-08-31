# CAOS — START HERE

## Instance Identity
- INSTANCE_NAME: CAOS
- OWNER: Mark
- DECISION_AUTHORITY: Mark
- EXECUTION_AUTHORITY: Mark only

## Absolute Isolation Rule
This is an independent CAOS instance. It must never connect to, copy, or modify Bill's personal CAOS, Bill's Master Ledger, Koziris Portfolio, or any other person's portfolio. This rule has no exceptions.

## Canonical Links
- Operator Manual: [[CAOS — OPERATOR MANUAL]]
- Command Card: [[00_START_HERE/CAOS — COMMAND CARD]]
- Master Ledger: [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- Active Handoff Snapshot: [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
- Archived original master prompt: [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0]]

## Installed Capabilities and Provider Status
- Obsidian vault (this vault): ACTIVE — canonical file store.
- Claude Code Agent tool (subagents): ACTIVE — used for the 8 specialist roles.
- Web search / web fetch: ACTIVE — sole research source for this build.
- Financial-data provider: NOT CONNECTED — this build uses web search/fetch only.
- Scheduled tasks / automation: NOT CONFIGURED — manual command invocation only.

## Active Task Names and Schedules
None scheduled. All products are invoked manually via the Command Card commands.

## Manual Commands
See [[00_START_HERE/CAOS — COMMAND CARD]] for the full list and build status.

## Notification Certification State
N/A — no automation configured in this build.

## Latest Architecture Version
v1.0 — flagship build (Daily Anchor fully working; 9 other products documented as NOT YET BUILT). Design source: [[docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design]] (outside this vault's numbered folders, in the project's `docs/` folder).
