# CAOS — Build Task Tracker

Tracks the design and build of the Obsidian + Claude Code multi-agent system
described in `CAOS_Mark_Independent_Clone_Master_Prompt_v1.0 (2).md`. This
file is project-status tracking, not part of the CAOS vault itself.

Last updated: 2026-08-28

## Status
Design phase (brainstorming). No vault files have been created yet — this
tracker documents decisions made in conversation so the build can proceed
from a written plan rather than being re-derived.

## Decisions locked in
- **Vault = this project folder.** It already contains `.obsidian/`; no
  separate vault location.
- **No code, no Workflow scripts.** Agent roles, products, and tasks are
  plain markdown files. Orchestration happens by Claude reading a runbook
  and calling the Agent tool directly — parallel steps use multiple Agent
  tool calls in one turn (native Claude Code behavior), not a scripted
  pipeline.
- **CLAUDE.md is a thin pointer** to `00_START_HERE/CAOS — OPERATOR
  MANUAL.md`, which is the single generic file containing everything the
  system needs.
- **Obsidian holds all agent descriptions, product/skill runbooks, and task
  status** — nothing about "what an agent does" or "what a product does"
  lives outside the vault.
- **Linking rule:** every dated agent-run output file has an "Inputs
  Consulted" section with wikilinks to the exact upstream files it read.
  Obsidian's automatic backlinks then give free reverse-navigation. The
  Orchestrator's file additionally gets a "Full Run Map" linking to every
  specialist file for that day's run. The Active Handoff Snapshot gets one
  heading per `HANDOFF_ID` so agent files can link to a specific handoff,
  not just the whole file.
- **Scheduling: manual only for now.** No cron/routine automation. All
  products are invoked by typing their Command Card command.
- **Data sources: web search/fetch only for v1.** No financial-data
  API/MCP wired in yet.
- **Build scope: flagship-first.** Build the vault, all 9 agent spec
  files, and a fully working **Daily Anchor** runbook; stub the other 9
  products. Decided 2026-08-28.

## Not yet built
- [ ] Vault folder structure (`00_START_HERE` … `06_PRODUCT_RUNBOOKS`)
- [ ] `CLAUDE.md`
- [ ] `START HERE`, `OPERATOR MANUAL`, `COMMAND CARD` files
- [ ] `Master Ledger — CANONICAL` template (UNINITIALIZED — no fabricated
      holdings)
- [ ] `Active Handoff Snapshot` template (empty queue)
- [ ] 9 agent spec files (`_AGENT SPEC — <Role>.md`), one per role in
      master prompt §10: Verifier, Discovery, Forward Expectations,
      Industry Read-through, Underwriter, Portfolio Court, Risk &
      Survivability, Red Team, Orchestrator
- [ ] `Daily Anchor.md` runbook (full build)
- [ ] Remaining 9 product runbooks (stubs only, for this pass)
- [ ] Copy of the original master prompt doc into `05_ARCHIVE/`
- [ ] First real end-to-end run of Daily Anchor, to validate the pattern
      before anything else is built on top of it

## Explicitly out of scope for this pass
- Any scheduling/automation (cloud routine or local cron) — manual command
  invocation only
- Real portfolio intake (master prompt §5) — Ledger stays UNINITIALIZED
- Any financial-data API/MCP beyond WebSearch/WebFetch
- Dataview / Templater / Obsidian Git setup — may be suggested as optional
  plugins in the Operator Manual, but nothing is built using them

## Next step
Design spec written: `docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design.md`.
Pending Mark's review before moving to an implementation plan.
