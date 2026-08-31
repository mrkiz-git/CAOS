# CAOS — Obsidian Multi-Agent System Design

Status: draft, pending user review
Source doc: `docs/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0 (2).md`
Scope: flagship-first build (Daily Anchor fully working; 9 other products stubbed)

## 1. Purpose

The source document is a master prompt written for ChatGPT's "Work" mode,
where subagents, scheduled tasks, and Obsidian access are built-in platform
features. This spec translates that design into Claude Code, where the
equivalent primitives are the Agent tool (subagents), a project's
`CLAUDE.md`, and a plain Obsidian vault on disk — with no custom code or
Workflow scripts, per explicit instruction. Everything that describes an
agent, a product, or a task lives in the vault as markdown; Claude Code's
only job is to read that markdown and act on it.

## 2. Vault location and structure

The vault is this project's root directory (it already contains
`.obsidian/`). Final structure:

```
CAOS — Canonical System/
├── CLAUDE.md
├── 00_START_HERE/
│   ├── CAOS — START HERE.md
│   ├── CAOS — OPERATOR MANUAL.md
│   └── CAOS — COMMAND CARD.md
├── 01_MASTER_LEDGER/
│   └── CAOS Master Ledger — CANONICAL.md
├── 02_ACTIVE_HANDOFF/
│   └── CAOS — ACTIVE HANDOFF SNAPSHOT.md
├── 03_AGENT_RUNS/
│   ├── 01_VERIFIER/
│   │   └── _AGENT SPEC — Verifier.md
│   ├── 02_DISCOVERY/
│   │   └── _AGENT SPEC — Discovery.md
│   ├── 03_FORWARD/
│   │   └── _AGENT SPEC — Forward Expectations.md
│   ├── 04_INDUSTRY/
│   │   └── _AGENT SPEC — Industry Read-through.md
│   ├── 05_UNDERWRITER/
│   │   └── _AGENT SPEC — Underwriter.md
│   ├── 06_PORTFOLIO_COURT/
│   │   └── _AGENT SPEC — Portfolio Court.md
│   ├── 07_RISK_SURVIVABILITY/
│   │   └── _AGENT SPEC — Risk and Survivability.md
│   ├── 08_RED_TEAM/
│   │   └── _AGENT SPEC — Red Team.md
│   └── 09_ORCHESTRATOR/
│       └── _AGENT SPEC — Orchestrator.md
├── 04_FLIGHT_RECORDER/
├── 05_ARCHIVE/
│   └── CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md   (copied verbatim)
└── 06_PRODUCT_RUNBOOKS/
    ├── Daily Anchor.md                      (full build)
    ├── Post-Open Delta Check.md              (stub)
    ├── Emergency Thesis Rerun.md             (stub)
    ├── DCA Execution Card.md                 (stub)
    ├── Monster Census.md                     (stub)
    ├── Weekly Ranking.md                     (stub)
    ├── Deep Audit.md                         (stub)
    ├── Learning Review.md                    (stub)
    ├── Event Gate Watch.md                   (stub)
    └── Multi-Bagger Hunter Watch.md          (stub)
```

Dated run-output files accumulate inside each `03_AGENT_RUNS/0X_ROLE/`
folder alongside that role's spec file, so a folder shows both "what this
agent does" and its full run history in one place.

## 3. Naming and linking conventions

**Run-output file naming:** `MODULE_YYYY-MM-DD_RUNID.md`, e.g.
`VERIFIER_2026-08-28_RUN01.md`. `RUNID` is a zero-padded sequence
(`RUN01`, `RUN02`, ...) disambiguating multiple runs of the same module on
the same date (e.g., a Daily Anchor and a same-day Emergency Thesis Rerun
both touching the Verifier).

**Inputs Consulted rule:** every dated output file opens with a section
naming exactly which upstream files it read, as wikilinks:

```markdown
## Inputs Consulted
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-08-28_RUN01]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]
```

Obsidian computes backlinks automatically from these, so opening any
upstream file's "Linked mentions" panel shows every file that consumed it —
no manual reverse-linking needed.

**Full Run Map:** the Orchestrator's dated output additionally opens with
a section linking to all 8 specialist files produced in that run, in
pipeline order — a single-page hub for that day's full run.

**Handoff-level linking:** the Active Handoff Snapshot uses one markdown
heading per `HANDOFF_ID` (format defined in master prompt §8). Agent files
referencing a specific handoff link to
`[[...ACTIVE HANDOFF SNAPSHOT#HANDOFF_ID]]` rather than the whole file.

## 4. CLAUDE.md

```markdown
# CAOS

This is the CAOS canonical vault and operating system.

Before doing anything else in this project, read `00_START_HERE/CAOS
— OPERATOR MANUAL.md` in full and follow it exactly. It is the single
source of truth for every law, agent role, product, and operating rule in
this system. Do not rely on assumptions, prior conversations, or general
knowledge about CAOS — only this vault's current content governs.

If the Operator Manual is missing or unreadable, stop and tell the user
before doing anything else.
```

## 5. Canonical files

**START HERE** records (per master prompt §7): instance identity, owner
and decision authority, canonical folder link, Master Ledger link, Active
Handoff link, installed capabilities and provider status, active task
names and schedules (state "none scheduled — manual command invocation
only" for this build), manual commands, notification certification state
(N/A — no automation this pass), latest architecture version, and the
absolute-isolation rule (never touch Bill's CAOS/ledger/portfolio).

**OPERATOR MANUAL** is the file CLAUDE.md points to. It must explain the
complete machine in plain language, reorganizing master prompt §1–§21
content: mission, constitutional laws, portfolio-state law, source
hierarchy and evidence labels, the agent roster and multi-agent pipeline,
candidate taxonomy, handoff protocol, logging standard, the Command Card
(which products are built vs. stubbed and why), execution controls,
acceptance tests, failure states, and human duties. This is the single
generic instructions file — nothing essential should require reading the
original master prompt to operate the system day to day (the original
stays archived for historical/reference fidelity).

**COMMAND CARD** lists all 12 commands from master prompt §7, each marked
`ACTIVE` (Daily Anchor only) or `NOT YET BUILT` (the other 9), consistent
with the Radical Honesty law.

**Master Ledger — CANONICAL** template contains all 12 required sections
from master prompt §7 (mandate, portfolio snapshot, cash vs. buying power,
funded-security roles, candidate registry, evidence gates, handoff index,
CAOS EVENT history, confirmed transactions, supersession map, system
rules, archive), each stamped `UNINITIALIZED — pending Mark's one-time
intake (master prompt §5)`. No fabricated holdings, prices, or cash
figures.

**Active Handoff Snapshot** template contains the required sections
(operating rules, active Hunter signals, Challengers, Seeds, trigger
watches, event gates, tribunals, source status, acknowledgements, Last
writer), all empty, with the per-`HANDOFF_ID` heading convention ready to
receive entries.

## 6. Agent roster (9 files)

Every `_AGENT SPEC — <Role>.md` follows this template:

```markdown
# Agent <N> — <Role Name>

## Mission
<1–2 sentences>

## Responsibilities
<from master prompt §10>

## Required inputs
<wikilinks to the files this role must read before writing its output>

## Output contract
- File: `03_AGENT_RUNS/0X_ROLE/MODULE_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section (see §3 of this spec)
- <role-specific required content/format>

## Constraints
<relevant constitutional laws from master prompt §3, e.g. "never write
directly to the Master Ledger," "keep raw convexity separate from
survivability-adjusted attractiveness">

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED
| UNKNOWN

## Invocation prompt template
<the exact text Claude uses as the `prompt` argument to the Agent tool
when calling this role>
```

Worked example — Verifier:

```markdown
# Agent 1 — Verifier

## Mission
Verify the current portfolio source, prices, and evidence hierarchy
before any downstream agent reasons about them.

## Responsibilities
- Verify current portfolio source, timestamp, holdings, cash, and
  cash-vs-buying-power separation.
- Verify prices, timestamps, and market status.
- Check source hierarchy and evidence labels.
- Identify stale, conflicting, inaccessible, or unverified facts.
- Produce a Source Readiness table and a data-quality verdict.

## Required inputs
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]]

## Output contract
- File: `03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_RUNID.md`
- Must open with "Inputs Consulted"
- Must end with a Source Readiness table and one verdict line:
  `DATA QUALITY = PASS / DEGRADED / BLOCKED`

## Constraints
- Fresh-Evidence Supremacy: newest verified state overrides older
  prompts, rankings, or assumptions.
- Radical Honesty: write UNKNOWN/DATA LIMITED/UNVERIFIED rather than
  guessing.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED
| UNKNOWN

## Invocation prompt template
"You are the CAOS Verifier agent (Agent 1). Read your full role spec
at `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md` in this vault and
follow it exactly. Read the Master Ledger and Active Handoff Snapshot at
the paths it lists. Write today's output to
`03_AGENT_RUNS/01_VERIFIER/VERIFIER_<date>_<runid>.md` per the output
contract. Do not do any other agent's job."
```

The remaining 8 roles follow the same template, populated from master
prompt §10:

Portfolio-state awareness is a cross-cutting requirement (master prompt
§3 laws apply "in every module," §4 requires every execution-sensitive
run to stamp portfolio source) — so several roles read the Master Ledger
and/or Active Handoff Snapshot directly, not just Verifier's output:

| # | Role | Required inputs | Key output |
|---|------|-----------------|------------|
| 2 | Discovery | Verifier's output, Master Ledger (current holdings), Active Handoff Snapshot (existing candidates) | Searched universe, fresh names, exclusions + reasons — echo-avoidance depends on knowing what's already tracked |
| 3 | Forward Expectations | Verifier's output, Master Ledger (funded-holdings list) | Guidance/contracts/ramps/capex/ARR/EBITDA + next falsifiable proof point |
| 4 | Industry Read-through | Verifier's output, Master Ledger (holdings for read-through mapping) | Bottlenecks, second-order beneficiaries, substitution risk; permanent NVIDIA gate when triggered |
| 5 | Underwriter | Discovery + Forward + Industry outputs | Monster Files: valuation, dilution, survivability, 3x/5x/10x (and 30x/100x only when credible) regimes, kill conditions |
| 6 | Portfolio Court | Underwriter's output, Master Ledger (current holdings/cash), Active Handoff Snapshot | 100%-cash trial, next-euro ranking, opportunity-cost/capital-recycling tribunal, portfolio-count/No-Orphan checks — these are direct holdings comparisons, not reachable through Underwriter's output alone |
| 7 | Risk and Survivability | Underwriter's output, Master Ledger (position sizes, for concentration risk) | Concentration/liquidity/financing/dilution/regulatory risk map, proof/warning/break gates |
| 8 | Red Team | Underwriter + Portfolio Court + Risk outputs | Strongest opposing case, what evidence would reverse the call, integrity grades |
| 9 | Orchestrator | All 8 specialist outputs + Active Handoff Snapshot | Final Anchor verdict, Full Run Map, handoff updates, LOG REQUIRED/NO LOG REQUIRED |

Per master prompt §10, no specialist may write to the Master Ledger or
make the final portfolio decision; only the Orchestrator proposes the
combined ledger event. The Orchestrator role is performed by the primary
Claude Code session itself (not a spawned subagent), since it must
synthesize every specialist's output into the single user-facing verdict
and needs the full conversation context to do so — it still writes its
own dated file to `09_ORCHESTRATOR/` for audit parity with the other
roles.

## 7. Daily Anchor runbook (full build)

`06_PRODUCT_RUNBOOKS/Daily Anchor.md` contains:

- **Trigger:** `Run CAOS Daily Anchor`
- **Schedule note:** "Manual only — no automation configured. Run this by
  typing the command above."
- **Precondition check:** read the Master Ledger; if portfolio state is
  `UNINITIALIZED` or stale, state `HOLDINGS UNKNOWN / EXECUTION BLOCKED`
  and continue in research-only mode (discovery/underwriting may proceed;
  sizing/execution output is suppressed), per master prompt §4.
- **The 19 mandatory work items** from master prompt §12, restated as a
  checklist the Orchestrator step ties off against before presenting the
  final verdict.
- **Agent call sequence** (no Workflow script — sequential/parallel Agent
  tool calls driven by the runbook text):
  1. Call Verifier (single Agent tool call). Wait for result.
  2. Call Discovery, Forward Expectations, and Industry Read-through as
     three Agent tool calls issued in the same turn (genuinely parallel —
     each is independent of the other two). Wait for all three.
  3. Call Underwriter (single call, reads all three step-2 outputs). Wait.
  4. Call Portfolio Court and Risk & Survivability as two Agent tool
     calls in the same turn (both depend only on Underwriter). Wait for
     both.
  5. Call Red Team (single call, reads Underwriter + Portfolio Court +
     Risk outputs). Wait.
  6. Orchestrator step: the main session reads all 8 files, writes
     `09_ORCHESTRATOR/ORCHESTRATOR_<date>_<runid>.md` with the Full Run
     Map, updates the Active Handoff Snapshot if authorized and verified,
     and presents the user-visible verdict in chat.
- **Linking rule application:** every file written in steps 1–6 includes
  its Inputs Consulted section per §3 of this spec.
- **Execution rules** (master prompt §12): no autonomous trades; no exact
  buy sizing without a live verified price and confirmed real cash;
  preserve quantities until a confirmed fill; no margin; price direction
  alone never implies a buy/sell.
- **Required output format:** first-line verdict, data/portfolio stamp,
  discovery ledger, 100%-cash trial, next-uncommitted-euro ranking,
  execution card (or `DO NOTHING / HOLD CASH`), mechanical grades, and
  `LOG REQUIRED` (with a paste-ready combined Master Ledger event block)
  or `NO LOG REQUIRED`.
- **Failure handling:** if a dependency fails mid-run, return a concise
  `LIMITED ANCHOR` or `FAILED ANCHOR` stating what completed, what
  failed, and whether a manual rerun is needed — never finish silently.

## 8. Product stub template (9 files)

```markdown
# CAOS — <Product Name>

**Command:** `<exact Command Card command>`
**Status:** NOT YET BUILT
**Default schedule (inactive):** <schedule from master prompt, noted but
not configured>

## What this product will do
<1 paragraph, drawn from the relevant master prompt section>

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#<anchor>]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product
reuses the same 9-agent roster, but its own run sequence, checklist, and
output format haven't been written yet.
```

Applies to: Post-Open Delta Check, Emergency Thesis Rerun, DCA Execution
Card, Monster Census, Weekly Ranking, Deep Audit, Learning Review, Event
Gate Watch, Multi-Bagger Hunter Watch.

## 9. Execution model (worked example)

When Mark types `Run CAOS Daily Anchor` in a Claude Code session
opened in this vault:

1. `CLAUDE.md` has already directed Claude to read the Operator Manual at
   session start.
2. Claude opens `06_PRODUCT_RUNBOOKS/Daily Anchor.md` and follows it.
3. Claude reads the Master Ledger and Active Handoff Snapshot, stamps
   portfolio source/timestamp, determines research-only vs. full mode.
4. Claude calls the Agent tool once for Verifier, using the invocation
   prompt template from its spec file. The subagent reads its required
   inputs and writes its dated file.
5. Claude calls the Agent tool three times in one turn for Discovery,
   Forward Expectations, and Industry Read-through — these run
   concurrently because they are independent tool calls in a single
   response (standard Claude Code behavior; no scripted pipeline
   required).
6. Claude calls Underwriter once, passing/pointing it at the three step-5
   outputs.
7. Claude calls Portfolio Court and Risk & Survivability in one turn
   (two parallel Agent calls).
8. Claude calls Red Team once.
9. Claude, acting as Orchestrator, reads all 8 files, writes the
   Orchestrator file with the Full Run Map, updates the Active Handoff
   Snapshot, and presents the final verdict to Mark in chat, including
   `LOG REQUIRED` / `NO LOG REQUIRED`.

No JavaScript, no Workflow tool, no custom subagent-type registration —
every step is Claude reading vault markdown and using the Agent tool
directly.

## 10. Out of scope for this pass

- The other 9 products beyond their stub files
- Any scheduling/automation (cloud routine or local cron)
- Real portfolio intake (master prompt §5) — Ledger stays `UNINITIALIZED`
- Any financial-data API/MCP beyond WebSearch/WebFetch
- Dataview / Templater / Obsidian Git — may be mentioned as optional
  plugin suggestions in the Operator Manual; nothing is built using them

## 11. Acceptance test for this build

- Every file in §2's tree exists and is readable.
- `CLAUDE.md` correctly directs a fresh session to the Operator Manual.
- Typing `Run CAOS Daily Anchor` in a vault-rooted session produces,
  at minimum, a `LIMITED ANCHOR` or `FAILED ANCHOR` result stating
  exactly what ran and what didn't (never a silent failure), and — if all
  8 specialist calls succeed — a full Anchor verdict with all 8
  specialist files plus the Orchestrator file cross-linked per §3.
- Typing any of the other 9 Command Card commands returns the stub's
  `NOT YET BUILT` content rather than an improvised run.
