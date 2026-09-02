# CAOS — Capital Allocation Operating System

An auditable, evidence-driven capital allocation system for maximizing long-run CAGR through survivable asymmetry.

## Mission

CAOS answers: **If all investable capital were cash today, where should the next uncommitted euro be allocated?**

The system continuously discovers, underwrites, compares, monitors, falsifies, ranks, and learns from investment decisions through a nine-agent specialist pipeline. Mark is the sole decision authority and execution authority.

## Core Principles

1. **Reality First** — Evidence outranks narrative.
2. **Radical Honesty** — Explicitly mark uncertainty (UNKNOWN, DATA LIMITED, UNVERIFIED).
3. **Fresh-Evidence Supremacy** — Current verified evidence overrides older assumptions.
4. **No Autonomous Trading** — Every decision requires explicit human approval.
5. **Survivability Before Optionality** — Reject high-upside bets if survival is implausible.
6. **Process Over Outcome** — Judge decisions by evidence quality, not luck.

See `00_START_HERE/CAOS — OPERATOR MANUAL.md` for the complete constitutional laws and governing rules.

## System Architecture

### Agent Roster

Nine specialist agents run in sequence, each with defined inputs, outputs, and constraints:

1. **Verifier** — Audits portfolio state and fresh data sources
2. **Discovery** — Identifies new candidates and monitors existing holdings
3. **Forward Expectations** — Analyzes forward guidance and catalysts
4. **Industry Read-through** — Maps competitive dynamics and trends
5. **Underwriter** — Grades evidence quality and thesis durability
6. **Portfolio Court** — Compares candidates against holdings
7. **Risk and Survivability** — Stress-tests financing and downside scenarios
8. **Red Team** — Falsifies thesis and searches for blindspots
9. **Orchestrator** — Synthesizes findings and proposes ledger events

See `03_AGENT_RUNS/` for each agent's full specification.

### Execution Flow

```
Verifier
   |
Discovery -- Forward Expectations -- Industry Read-through   (parallel)
   \                |                    /
                Underwriter
                /         \
      Portfolio Court   Risk & Survivability                 (parallel)
                \         /
                 Red Team
                    |
               Orchestrator
```

## Products Built

- **Daily Anchor** — Full multi-agent analysis run (see `06_PRODUCT_RUNBOOKS/Daily Anchor`)
- **Post-Open Delta Check** — Intraday subset for same-day market changes (see `06_PRODUCT_RUNBOOKS/Post-Open Delta Check`)

## Key Files and Directories

- `00_START_HERE/` — Operator manual, command card, onboarding
- `01_MASTER_LEDGER/` — Canonical portfolio state and transaction log
- `02_ACTIVE_HANDOFF/` — Cross-module state changes and signals
- `03_AGENT_RUNS/` — Agent specifications and run outputs
- `04_FLIGHT_RECORDER/` — Timestamped execution logs
- `05_ARCHIVE/` — Historical analysis and research library
- `06_PRODUCT_RUNBOOKS/` — Product definitions and execution procedures
- `CLAUDE.md` — Project governance and setup directives

## Getting Started

1. Read `00_START_HERE/CAOS — OPERATOR MANUAL.md` for complete system law and requirements
2. Review `00_START_HERE/CAOS — COMMAND CARD` for available commands
3. Check `06_PRODUCT_RUNBOOKS/` for product-specific execution procedures

### One-Time Setup

Before running portfolio-aware analysis, Mark must complete an intake session providing:
- Personal timezone and tax residence
- Broker details and fractional-share support
- Investing horizon and monthly contribution amount
- Max tolerable drawdown and risk preferences
- Sector/geographic/security exclusions
- Current broker portfolio and cash balances
- Any recent unshown transactions

See `CAOS — OPERATOR MANUAL.md` §5 for full details.

## Evidence and Sources

- Research access: web search and web fetch (no connected financial APIs)
- Primary sources only: company filings, exchange data, regulatory documents
- Evidence labels: VERIFIED FACT, CAOS INFERENCE, UNVERIFIED LEAD, DATA LIMITED, UNKNOWN

## Logging and Audit

All material state changes are logged using the standard CAOS EVENT template. The Master Ledger is the system of record for portfolio state — only the Orchestrator proposes ledger mutations, and only after explicit human confirmation.

The linking rule ensures every dated run file traces its upstream dependencies in Obsidian, making the analysis DAG fully traversable.

## Execution Controls

- No margin or leverage by default
- No fractional-share assumption without broker confirmation
- No exact buy sizing without live verified prices and confirmed real cash
- Price direction alone never implies a trade
- All trades require explicit Mark approval before execution

## Failure Modes and Human Duties

If portfolio state is unavailable or stale, the system returns `HOLDINGS UNKNOWN / EXECUTION BLOCKED` rather than guessing. If a scheduled dependency fails mid-run, the system returns a LIMITED or FAILED result naming what completed, what failed, and what needs manual rerun.

Mark's duties:
- Complete the one-time intake before expecting real portfolio-aware output
- Reply "logged" after manually archiving a LOG REQUIRED block
- Confirm or amend draft portfolio-count rules
- Review Deep Audit and Learning Review outputs as they are built

## License and Governance

Single operator: Mark. All decisions require Mark's explicit confirmation. This system is not open to external trading or autonomous execution.

For questions or updates, see `CLAUDE.md` for project governance or `00_START_HERE/` for system law.
