# MARK CAOS Obsidian Multi-Agent System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the MARK CAOS vault: full canonical folder structure, all 9 specialist agent specs, a fully working Daily Anchor product, 9 stubbed products, and a `CLAUDE.md` that points to a single Operator Manual — all as plain markdown, no code.

**Architecture:** This project's root directory is the Obsidian vault. Every agent role, product runbook, and cross-file link is a markdown file. Orchestration at run time is Claude reading a runbook and calling the Agent tool directly (parallel steps = multiple Agent tool calls in one turn); no Workflow script or custom subagent registration is used.

**Tech Stack:** Markdown, Obsidian wikilinks, Claude Code's Write/Edit/Bash/Agent tools. No git (this project is not a git repository — none is initialized as part of this plan).

**Spec:** `docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design.md`

## Global Constraints

- No code, no Workflow scripts. Every deliverable is a markdown file.
- Vault = project root (`/Users/markelman/Projects/CAOS`), which already contains `.obsidian/`.
- No fabricated portfolio data anywhere — the Master Ledger stays `UNINITIALIZED` until Mark completes the one-time intake (master prompt §5). Never invent holdings, prices, or cash figures.
- No scheduling/automation this pass — every product is invoked manually.
- Research access this pass is WebSearch/WebFetch only — no financial-data API/MCP.
- Evidence labels: only `VERIFIED FACT`, `CAOS INFERENCE`, `UNVERIFIED LEAD`, `DATA LIMITED`, `UNKNOWN`.
- Run-output file naming: `MODULE_YYYY-MM-DD_RUNID.md` (e.g. `VERIFIER_2026-08-28_RUN01.md`), `RUNID` zero-padded (`RUN01`, `RUN02`, ...).
- Agent spec files: `_AGENT SPEC — <Role>.md`, colocated inside that role's own `03_AGENT_RUNS/0X_ROLE/` folder.
- Every dated agent-output file must open with an "Inputs Consulted" section wikilinking the exact upstream files it read (see spec §3). The Orchestrator's file additionally carries a "Full Run Map" linking to all 8 specialist files from that run.
- Obsidian wikilinks never include the `.md` extension. Heading-anchor links (`[[File#Heading]]`) must use the exact literal heading text from the target file — Obsidian does not use GitHub-style URL slugs.
- No specialist agent writes to the Master Ledger. Only the Orchestrator proposes a combined ledger event, and only after Mark confirms `logged`.
- Git was initialized locally (2026-08-28) solely to support subagent-driven execution (per-task commits, worktree isolation, diff-based review). No remote is configured and nothing is pushed anywhere as part of this plan.

---

## Task 1: Vault folder scaffold and CLAUDE.md

**Files:**
- Create: `CLAUDE.md`
- Create (directories only): `00_START_HERE/`, `01_MASTER_LEDGER/`, `02_ACTIVE_HANDOFF/`, `03_AGENT_RUNS/01_VERIFIER/` through `03_AGENT_RUNS/09_ORCHESTRATOR/`, `04_FLIGHT_RECORDER/`, `05_ARCHIVE/`, `06_PRODUCT_RUNBOOKS/`

**Interfaces:**
- Consumes: nothing (first task).
- Produces: the directory tree every later task writes into; `CLAUDE.md` at vault root, read by every future Claude Code session opened here.

- [ ] **Step 1: Create the directory tree**

Run:
```bash
cd "/Users/markelman/Projects/CAOS"
mkdir -p "00_START_HERE" "01_MASTER_LEDGER" "02_ACTIVE_HANDOFF" \
  "03_AGENT_RUNS/01_VERIFIER" "03_AGENT_RUNS/02_DISCOVERY" "03_AGENT_RUNS/03_FORWARD" \
  "03_AGENT_RUNS/04_INDUSTRY" "03_AGENT_RUNS/05_UNDERWRITER" "03_AGENT_RUNS/06_PORTFOLIO_COURT" \
  "03_AGENT_RUNS/07_RISK_SURVIVABILITY" "03_AGENT_RUNS/08_RED_TEAM" "03_AGENT_RUNS/09_ORCHESTRATOR" \
  "04_FLIGHT_RECORDER" "05_ARCHIVE" "06_PRODUCT_RUNBOOKS"
```

- [ ] **Step 2: Verify the tree**

Run: `find . -maxdepth 2 -type d -not -path './.obsidian*' -not -path './docs*' | sort`
Expected: all 17 directories listed (the 8 top-level `0X_*` folders plus the 9 `03_AGENT_RUNS/0X_ROLE` subfolders).

- [ ] **Step 3: Write CLAUDE.md**

Use the Write tool to create `CLAUDE.md` with exactly this content:

```markdown
# MARK CAOS

This is the MARK CAOS canonical vault and operating system.

Before doing anything else in this project, read `00_START_HERE/MARK CAOS — OPERATOR MANUAL.md` in full and follow it exactly. It is the single source of truth for every law, agent role, product, and operating rule in this system. Do not rely on assumptions, prior conversations, or general knowledge about CAOS — only this vault's current content governs.

If the Operator Manual is missing or unreadable, stop and tell the user before doing anything else.
```

- [ ] **Step 4: Verify CLAUDE.md**

Run: `cat CLAUDE.md`
Expected: the exact content above, nothing else.

---

## Task 2: Archive the original master prompt

**Files:**
- Create: `05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md`
- Read: `docs/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0 (2).md`

**Interfaces:**
- Consumes: the original doc at the path above (already in the repo).
- Produces: `05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md`, whose exact headings (e.g. `## 15. Weekly Ranking specification`) are the anchor targets used by Task 14's stub files and Task 16's Operator Manual.

- [ ] **Step 1: Copy the file verbatim under a clean name**

Run:
```bash
cd "/Users/markelman/Projects/CAOS"
cp "docs/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0 (2).md" "05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md"
```

- [ ] **Step 2: Verify the copy is complete and unmodified**

Run:
```bash
diff "docs/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0 (2).md" "05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md"
```
Expected: no output (files identical).

- [ ] **Step 3: Confirm the anchor headings Task 14/16 will link to are present verbatim**

Run:
```bash
grep -nE '^## (12|13|14|15|16|17A|18|18A|21)\. |^## 1[678]\.' "05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md"
```
Expected output includes these exact lines (among others):
```
## 12. Daily Anchor specification
## 13. External Multi-Bagger Hunter Watch
## 14. Monster Census specification
## 15. Weekly Ranking specification
## 16. Event Gate Watch
## 17A. DCA Execution Card
## 18. Manual Deep Audit
## 18A. Learning Review
## 21. Product distinctions
```

---

## Task 3: Master Ledger and Active Handoff Snapshot templates

**Files:**
- Create: `01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL.md`
- Create: `02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT.md`

**Interfaces:**
- Consumes: nothing.
- Produces: two files every later task (agent specs, Daily Anchor runbook, Operator Manual) wikilinks to as `[[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]` and `[[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]`. Heading `## 11. System Rules and Amendments` in the Ledger is a link target used by Task 16.

- [ ] **Step 1: Write the Master Ledger template**

Use the Write tool to create `01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL.md`:

```markdown
# MARK CAOS Master Ledger — CANONICAL

STATUS: UNINITIALIZED — pending Mark's one-time intake (see [[00_START_HERE/MARK CAOS — OPERATOR MANUAL#5. One-Time Installation Intake]])

This is the sole controlling long-term portfolio and decision record for MARK CAOS. It is append-only. Corrections must state what was corrected, why, and what prior entry is superseded — history is never silently rewritten.

## 1. Current Mandate
UNINITIALIZED — pending Mark's one-time intake.

## 2. Current Portfolio Snapshot
STATUS: UNINITIALIZED
SOURCE: none
TIMESTAMP: none
No holdings, share counts, or prices are recorded. Do not infer or assume any position.

## 3. Real Cash vs. Buying Power
STATUS: UNINITIALIZED

## 4. Funded-Security Roles
STATUS: UNINITIALIZED — no funded securities recorded.

## 5. Candidate / Status Registry
STATUS: EMPTY
No candidates recorded yet. Permitted states: UNKNOWN, WATCH WITH SPECIFIC TRIGGER, SERIOUS REVIEW, HIGH-PRIORITY CHALLENGER, CHALLENGER, BUY-AUTHORIZED SEED, CORE / ATTACKER, PORTFOLIO REPLACEMENT CANDIDATE, REJECT, RETIRED / ARCHIVED, RESOLVED.

## 6. Active Evidence Gates and Tribunals
STATUS: EMPTY

## 7. Standardized Handoff Index
STATUS: EMPTY
See [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]] for the live unresolved queue.

## 8. Material CAOS EVENT History
STATUS: EMPTY
No events logged yet.

## 9. Confirmed Transactions / Fills
STATUS: EMPTY

## 10. Supersession and Resolution Map
STATUS: EMPTY

## 11. System Rules and Amendments
Draft portfolio-count rules (pending Mark's confirmation):
- target cap: seven funded public securities
- maximum two funded CAOS Seeds
- Core/Attacker positions should normally have a credible path toward approximately 5% of NAV
- Seeds normally occupy approximately 1%-3%
- sub-approximately-1.5% positions require an explicit Seed/Catalyst role and proof gate
- permanent sub-1% orphans are prohibited
- a Seed must graduate, remain under an exact evidence gate, or exit after two decisive evidence cycles
- no new funded security if the post-entry portfolio would exceed the confirmed cap
- drawdown alone is neither a sell reason nor a hold reason

These remain DRAFT until Mark explicitly approves or amends them.

## 12. Historical Archive
STATUS: EMPTY
```

- [ ] **Step 2: Write the Active Handoff Snapshot template**

Use the Write tool to create `02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT.md`:

```markdown
# MARK CAOS — Active Handoff Snapshot

This is the live, unresolved cross-module queue — not the holdings ledger. It contains only active, unresolved items. Never erase an unresolved item created by another module; resolve or supersede it explicitly.

## Operating Rules
- Handoff format: see [[00_START_HERE/MARK CAOS — OPERATOR MANUAL#9. Standardized Handoff Protocol]]
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
```

- [ ] **Step 3: Verify both files**

Run:
```bash
grep -c '^## ' "01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL.md"
grep -c '^## ' "02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT.md"
```
Expected: `12` for the Ledger (sections 1–12), `10` for the Snapshot (Operating Rules, Active Hunter Signals, Challengers, Seeds, Trigger Watches, Event Gates, Tribunals, Source Status, Acknowledgements, Last Writer).

---

## Task 4: Agent spec — Verifier (Agent 1)

**Files:**
- Create: `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md`

**Interfaces:**
- Consumes: `[[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]`, `[[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]` (both from Task 3).
- Produces: this spec file, referenced by Task 13 (Daily Anchor runbook) and Task 16 (Operator Manual roster list) as `[[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]]`. Establishes the closing-status-line convention (`DATA QUALITY = PASS / DEGRADED / BLOCKED`) that Tasks 5–11 each define their own version of.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md`:

```markdown
# Agent 1 — Verifier

## Mission
Verify the current portfolio source, prices, and evidence hierarchy before any downstream agent reasons about them.

## Responsibilities
- Verify current portfolio source, timestamp, holdings, cash, and cash-vs-buying-power separation.
- Verify prices, timestamps, and market status.
- Check source hierarchy and evidence labels.
- Identify stale, conflicting, inaccessible, or unverified facts.
- Produce a Source Readiness table and a data-quality verdict.

## Required inputs
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]
- [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]

## Output contract
- File: `03_AGENT_RUNS/01_VERIFIER/VERIFIER_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section listing the files above as wikilinks.
- Must end with a Source Readiness table and one verdict line: `DATA QUALITY = PASS / DEGRADED / BLOCKED`.
- If the Master Ledger is `UNINITIALIZED`, state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` rather than guessing at any position.

## Constraints
- Fresh-Evidence Supremacy: newest verified state overrides older prompts, rankings, or assumptions.
- Radical Honesty: write UNKNOWN/DATA LIMITED/UNVERIFIED rather than guessing.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Verifier agent (Agent 1). Read your full role spec at `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md` in this vault and follow it exactly. Read the Master Ledger and Active Handoff Snapshot at the paths it lists. Write today's output to `03_AGENT_RUNS/01_VERIFIER/VERIFIER_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run: `grep -c '^## ' "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md"`
Expected: `7` (Mission, Responsibilities, Required inputs, Output contract, Constraints, Evidence labeling, Invocation prompt template).

---

## Task 5: Agent spec — Discovery (Agent 2)

**Files:**
- Create: `03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md`

**Interfaces:**
- Consumes: Verifier's output contract (Task 4) by reference — this spec instructs Discovery to read Verifier's latest dated file, plus the Master Ledger and Active Handoff Snapshot (Task 3).
- Produces: this spec file, referenced by Task 13 and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md`:

```markdown
# Agent 2 — Discovery

## Mission
Search for candidates outside current holdings and watchlists, without duplicating what the portfolio already tracks.

## Responsibilities
- Search outside holdings and watchlists.
- Ingest qualified External Hunter signals (when the Hunter Watch product exists — this pass it does not, so state that none are available).
- Cover multiple asymmetric bottleneck lanes.
- Record searched universe, fresh names, exclusions and reasons.
- Avoid incumbency protection and portfolio echo.

## Required inputs
- Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/`
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]] (current holdings, so already-owned names are not "discovered" as new)
- [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]] (existing candidates already tracked)

## Output contract
- File: `03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section.
- Must include: searched universe (buckets/lanes covered), fresh names found, exclusions and the reason for each.
- Must end with one verdict line: `DISCOVERY = SEARCH COMPLETE / SEARCH INCOMPLETE`.

## Constraints
- Objective Supremacy: no incumbent holding or prior conviction receives protection from being challenged.
- Never treat "already held" as a reason to stop searching a lane.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Discovery agent (Agent 2). Read your full role spec at `03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md` in this vault and follow it exactly. Read the Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/`, the Master Ledger, and the Active Handoff Snapshot. Write today's output to `03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md"
grep -c "Master Ledger" "03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery.md"
```
Expected: `7` headings; at least `1` match for "Master Ledger" (confirms Discovery reads the Ledger directly, not just Verifier's output).

---

## Task 6: Agent spec — Forward Expectations (Agent 3)

**Files:**
- Create: `03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md`

**Interfaces:**
- Consumes: Verifier's output contract (Task 4), Master Ledger (Task 3).
- Produces: this spec file, referenced by Task 13 and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md`:

```markdown
# Agent 3 — Forward Expectations

## Mission
Extract and weigh a company's own forward-looking statements before any valuation or ranking work happens.

## Responsibilities
- Extract company guidance, contracts, ramps, capacity, margin, capex, ARR, EBITDA and catalyst timing.
- Prioritize future quarters and delivery schedules over trailing results.
- Distinguish binding contracts, nonbinding targets, management aspirations, and CAOS inference from each other — never blend them into one claim.
- Identify the next falsifiable proof point for every company covered.

## Required inputs
- Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/`
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]] (funded-holdings list, so forward guidance is reviewed for every current holding, not only new candidates)

## Output contract
- File: `03_AGENT_RUNS/03_FORWARD/FORWARD_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section.
- Must include, per company covered: a forward-guidance table (binding contract / nonbinding target / management aspiration / CAOS inference, each labeled) and the next falsifiable proof point (exact date, event, metric, or filing).
- Must end with one verdict line: `FORWARD REVIEW = COMPLETE / DATA LIMITED`.

## Constraints
- Forward announced expectations receive very high weight relative to trailing metrics.
- Never present a management aspiration as a binding commitment.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Forward Expectations agent (Agent 3). Read your full role spec at `03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md` in this vault and follow it exactly. Read the Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/` and the Master Ledger. Write today's output to `03_AGENT_RUNS/03_FORWARD/FORWARD_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md"
grep -c "falsifiable proof point" "03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations.md"
```
Expected: `7` headings; at least `2` matches for "falsifiable proof point" (appears in Responsibilities and Output contract).

---

## Task 7: Agent spec — Industry Read-through (Agent 4)

**Files:**
- Create: `03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md`

**Interfaces:**
- Consumes: Verifier's output contract (Task 4), Master Ledger (Task 3).
- Produces: this spec file, referenced by Task 13 and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md`:

```markdown
# Agent 4 — Industry Read-through

## Mission
Map industry-level developments to their cross-portfolio implications, so no bottleneck or second-order effect is missed at the single-company level.

## Responsibilities
- Map industry and cross-portfolio implications.
- Cover AI compute/neocloud, data centers, power/grid/nuclear, cooling, networking/optics, semiconductors/memory, robotics/physical AI, defense/autonomy/space, quantum, batteries, biotech automation, and other credible lanes.
- Identify bottlenecks, second-order beneficiaries, substitution risk, and financing constraints.
- Run the permanent NVIDIA evidence read-through whenever new NVIDIA earnings, CFO commentary, 10-Q, call material, or materially updated guidance appears: Data Center/Hyperscale demand; Blackwell and Vera Rubin demand, supply and ramp; networking, optics and memory; land, power, shell and financing constraints; China assumptions; gross margin; forward guidance; read-through to economically connected MARK CAOS holdings and challengers.

## Required inputs
- Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/`
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]] (holdings, so read-through is mapped against what is actually owned)

## Output contract
- File: `03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section.
- Must include a bottleneck/second-order-beneficiary map across the lanes covered this run.
- Must include a "Permanent NVIDIA Gate" section — populated only when new NVIDIA material triggered it this run; otherwise state `NVIDIA GATE = NOT TRIGGERED THIS RUN`.
- Must end with one verdict line: `INDUSTRY READ-THROUGH = COMPLETE / DATA LIMITED`.

## Constraints
- Strong industry-level evidence never automatically proves a specific issuer's utilization, economics, financing, dilution, or execution — keep industry inference and company-specific fact separate.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Industry Read-through agent (Agent 4). Read your full role spec at `03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md` in this vault and follow it exactly. Read the Verifier's latest dated output in `03_AGENT_RUNS/01_VERIFIER/` and the Master Ledger. Write today's output to `03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md"
grep -c "NVIDIA" "03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through.md"
```
Expected: `7` headings; at least `3` matches for "NVIDIA".

---

## Task 8: Agent spec — Underwriter (Agent 5)

**Files:**
- Create: `03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md`

**Interfaces:**
- Consumes: Discovery (Task 5), Forward Expectations (Task 6), and Industry Read-through (Task 7) output contracts — all three dated files from the same run.
- Produces: this spec file, referenced by Task 9, Task 10, Task 13, and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md`:

```markdown
# Agent 5 — Underwriter

## Mission
Turn discovery and forward-expectations evidence into rigorously tested Monster Files, keeping raw upside separate from evidence-adjusted attractiveness.

## Responsibilities
- Conduct Monster Files on priority candidates surfaced by Discovery, Forward Expectations, and Industry Read-through.
- Test valuation denominator, per-share economics, dilution, survivability, financing, execution probability, and evidence quality.
- Test plausible 3x/5x/10x regimes, and 30x/100x regimes only when credible.
- Identify time required, required assumptions, and kill conditions for each candidate.
- Keep raw convexity (the size of the theoretical payoff) strictly separate from evidence/survivability-adjusted attractiveness (how likely and investable that payoff actually is).

## Required inputs
- Discovery's latest dated output in `03_AGENT_RUNS/02_DISCOVERY/`
- Forward Expectations' latest dated output in `03_AGENT_RUNS/03_FORWARD/`
- Industry Read-through's latest dated output in `03_AGENT_RUNS/04_INDUSTRY/`

## Output contract
- File: `03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section listing all three files above.
- One Monster File per priority candidate, each reporting: raw-convexity regime (3x/5x/10x, 30x/100x only if credible) AND evidence/survivability-adjusted attractiveness as two separate, clearly labeled fields — never merged into one score.
- Each Monster File must list its kill conditions explicitly.
- Must end with one verdict line: `UNDERWRITING = COMPLETE / PARTIAL`.

## Constraints
- Survivability Before Optionality: reject huge upside when financing, dilution, liquidity, durability, or execution risk make survival implausible.
- Burden of Proof: any "10x" or similar claim requires visible evidence, not assertion.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Underwriter agent (Agent 5). Read your full role spec at `03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md` in this vault and follow it exactly. Read Discovery's, Forward Expectations', and Industry Read-through's latest dated outputs from this run. Write today's output to `03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md"
grep -c "kill condition" "03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter.md"
```
Expected: `7` headings; at least `2` matches for "kill condition".

---

## Task 9: Agent spec — Portfolio Court (Agent 6)

**Files:**
- Create: `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md`

**Interfaces:**
- Consumes: Underwriter's output contract (Task 8), Master Ledger and Active Handoff Snapshot (Task 3).
- Produces: this spec file, referenced by Task 11, Task 13, and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md`:

```markdown
# Agent 6 — Portfolio Court

## Mission
Rank where the next uncommitted euro should go, tested against every real alternative — cash, current holdings, and the best challengers — without ever proposing execution.

## Responsibilities
- Run the 100%-cash holdings trial (if all capital were cash today, where would it go).
- Rank the next uncommitted euro.
- Compare business quality, expected CAGR, raw asymmetry, and portfolio role across candidates.
- Run opportunity-cost and capital-recycling tribunals.
- Test current holdings versus cash, strongest owned name, quality anchor, best Seed, and best Challenger.
- Enforce the approved portfolio-count and No-Orphan rules from the Master Ledger.
- Keep ranking strictly separate from execution — this role never outputs exact share counts or a buy/sell instruction.

## Required inputs
- Underwriter's latest dated output in `03_AGENT_RUNS/05_UNDERWRITER/`
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]] (current holdings, cash, portfolio-count rules)
- [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]

## Output contract
- File: `03_AGENT_RUNS/06_PORTFOLIO_COURT/PORTFOLIO_COURT_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section.
- Must include: 100%-cash trial result; next-uncommitted-euro ranking; capital-recycling tribunal result; portfolio-count and No-Orphan check results.
- If the Master Ledger is `UNINITIALIZED`, every holdings-comparison item must state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` rather than a fabricated comparison — the ranking of candidates against each other may still proceed.
- Must end with one verdict line: `PORTFOLIO COURT = RANKING COMPLETE / RANKING BLOCKED`.

## Constraints
- Cash Is Valid: do nothing when no candidate clears the minimum edge.
- Concentration Is Allowed, Not Worshipped: concentration only when opportunity cost and survivability-adjusted CAGR justify it.
- Never outputs exact buy sizing, a trade instruction, or an assumed fill — that is Execution, not Portfolio Court.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Portfolio Court agent (Agent 6). Read your full role spec at `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md` in this vault and follow it exactly. Read the Underwriter's latest dated output from this run, the Master Ledger, and the Active Handoff Snapshot. Write today's output to `03_AGENT_RUNS/06_PORTFOLIO_COURT/PORTFOLIO_COURT_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md"
grep -c "HOLDINGS UNKNOWN" "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md"
```
Expected: `7` headings; at least `1` match for "HOLDINGS UNKNOWN".

---

## Task 10: Agent spec — Risk and Survivability (Agent 7)

**Files:**
- Create: `03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md`

**Interfaces:**
- Consumes: Underwriter's output contract (Task 8), Master Ledger (Task 3).
- Produces: this spec file, referenced by Task 11, Task 13, and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md`:

```markdown
# Agent 7 — Risk and Survivability

## Mission
Find every realistic permanent-loss path in the candidates the Underwriter has underwritten, without turning ordinary volatility into a false sell signal.

## Responsibilities
- Test concentration, liquidity, financing, dilution, customer concentration, capital intensity, maturity/refinancing, regulatory, geographic, factor, and correlated-thesis risk.
- Identify realistic permanent-loss paths.
- Test portfolio drawdown and cash-survival implications without converting volatility into an automatic sell signal.
- Propose exact proof, warning, and break gates for each candidate.

## Required inputs
- Underwriter's latest dated output in `03_AGENT_RUNS/05_UNDERWRITER/`
- [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]] (position sizes, for concentration-risk math)

## Output contract
- File: `03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_SURVIVABILITY_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section.
- Must include a risk map per candidate covering each risk category listed in Responsibilities that applies.
- Must include explicit proof gate, warning gate, and break gate definitions per candidate (exact metric/date/event, not vague language).
- Must end with one verdict line: `RISK REVIEW = COMPLETE / DATA LIMITED`.

## Constraints
- Drawdown alone is neither a sell reason nor a hold reason — only a defined break gate triggers a sell recommendation.
- Survivability Before Optionality takes priority over raw upside.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Risk and Survivability agent (Agent 7). Read your full role spec at `03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md` in this vault and follow it exactly. Read the Underwriter's latest dated output from this run and the Master Ledger. Write today's output to `03_AGENT_RUNS/07_RISK_SURVIVABILITY/RISK_SURVIVABILITY_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md"
grep -c "break gate" "03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability.md"
```
Expected: `7` headings; at least `2` matches for "break gate".

---

## Task 11: Agent spec — Red Team (Agent 8)

**Files:**
- Create: `03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md`

**Interfaces:**
- Consumes: Underwriter (Task 8), Portfolio Court (Task 9), and Risk and Survivability (Task 10) output contracts.
- Produces: this spec file, referenced by Task 12, Task 13, and Task 16.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md`:

```markdown
# Agent 8 — Red Team

## Mission
Attack the leading conclusion as hard as a genuine skeptic would, before it reaches Mark.

## Responsibilities
- Attack the leading conclusion from Underwriter, Portfolio Court, and Risk and Survivability.
- Find unsupported statements, omitted challengers, stale states, circular reasoning, and false precision.
- Present the strongest opposing case.
- State exactly what evidence would reverse the recommendation.
- Grade hallucination discipline, linkage completeness, discovery coverage, and execution discipline for this run.

## Required inputs
- Underwriter's latest dated output in `03_AGENT_RUNS/05_UNDERWRITER/`
- Portfolio Court's latest dated output in `03_AGENT_RUNS/06_PORTFOLIO_COURT/`
- Risk and Survivability's latest dated output in `03_AGENT_RUNS/07_RISK_SURVIVABILITY/`

## Output contract
- File: `03_AGENT_RUNS/08_RED_TEAM/RED_TEAM_YYYY-MM-DD_RUNID.md`
- Must open with an "Inputs Consulted" section listing all three files above.
- Must include: the strongest opposing case against the leading conclusion; the exact evidence that would reverse it; a list of any unsupported statements, omitted challengers, stale states, or false precision found upstream.
- Must end with four grade lines: `HALLUCINATION DISCIPLINE = PASS / FAIL`, `LINKAGE COMPLETENESS = PASS / FAIL`, `DISCOVERY COVERAGE = PASS / FAIL`, `EXECUTION DISCIPLINE = PASS / FAIL`.

## Constraints
- Must genuinely argue against the leading conclusion, not restate it with a disclaimer.
- A claim of "no challenger" upstream must be checked against Discovery's actual searched universe, not accepted at face value.
- Never writes to the Master Ledger directly.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation prompt template
"You are the MARK CAOS Red Team agent (Agent 8). Read your full role spec at `03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md` in this vault and follow it exactly. Read the Underwriter's, Portfolio Court's, and Risk and Survivability's latest dated outputs from this run. Write today's output to `03_AGENT_RUNS/08_RED_TEAM/RED_TEAM_<date>_<runid>.md` per the output contract. Do not do any other agent's job."
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md"
grep -c "DISCIPLINE = PASS / FAIL" "03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team.md"
```
Expected: `7` headings; at least `3` matches for "DISCIPLINE = PASS / FAIL".

---

## Task 12: Agent spec — Orchestrator (Agent 9)

**Files:**
- Create: `03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md`

**Interfaces:**
- Consumes: all 8 specialist output contracts (Tasks 4–11) and the Active Handoff Snapshot (Task 3).
- Produces: this spec file, referenced by Task 13 and Task 16. Unlike Agents 1–8, this role is not invoked through the Agent tool — Task 13 calls it out as a direct instruction to the primary session.

- [ ] **Step 1: Write the spec file**

Use the Write tool to create `03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md`:

```markdown
# Agent 9 — Orchestrator

## Mission
Read every specialist's output for the run, reconcile conflicts visibly, and produce the single verdict Mark actually sees.

## Responsibilities
- Read every required specialist file for the run.
- Reconcile conflicting evidence visibly — never silently pick a side.
- Consume and acknowledge active handoffs from the Active Handoff Snapshot.
- Produce the final user-visible verdict (Anchor, or whichever product is running).
- Emit new handoffs only for material changes.
- Update the Active Handoff Snapshot when authorized and verified.
- Produce one combined, no-duplicate Master Ledger event block when logging is required — never write it silently; state `LOG REQUIRED` and wait for Mark to confirm `logged`.
- Never claim a subagent ran or a file was written unless it was actually verified (e.g. by reading the file back).

## Required inputs
- Verifier's latest dated output — `03_AGENT_RUNS/01_VERIFIER/`
- Discovery's latest dated output — `03_AGENT_RUNS/02_DISCOVERY/`
- Forward Expectations' latest dated output — `03_AGENT_RUNS/03_FORWARD/`
- Industry Read-through's latest dated output — `03_AGENT_RUNS/04_INDUSTRY/`
- Underwriter's latest dated output — `03_AGENT_RUNS/05_UNDERWRITER/`
- Portfolio Court's latest dated output — `03_AGENT_RUNS/06_PORTFOLIO_COURT/`
- Risk and Survivability's latest dated output — `03_AGENT_RUNS/07_RISK_SURVIVABILITY/`
- Red Team's latest dated output — `03_AGENT_RUNS/08_RED_TEAM/`
- [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]

## Output contract
- File: `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_YYYY-MM-DD_RUNID.md`
- Must open with a "Full Run Map" section wikilinking all 8 specialist files from this run, in pipeline order (Verifier, Discovery, Forward Expectations, Industry Read-through, Underwriter, Portfolio Court, Risk and Survivability, Red Team).
- Must state, for each active handoff consumed: `HANDOFF ACK CHECK: HANDOFF_ID | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO | RESOLVES_HANDOFF_ID`.
- Must end with: the final verdict, and one line `LOG REQUIRED` (with a paste-ready combined Master Ledger event block) or `NO LOG REQUIRED`.

## Constraints
- No specialist may write to the Master Ledger — only the Orchestrator proposes the combined event, and only Mark's reply of `logged` confirms it was preserved.
- Never finish a run silently — if a dependency failed, state `LIMITED ANCHOR` or `FAILED ANCHOR` and exactly what did and did not complete.
- No autonomous trades; no exact buy sizing without a live verified price and confirmed real cash; preserve quantities until a confirmed fill; no margin.

## Evidence labeling
Use only: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN

## Invocation
This role is not invoked through the Agent tool. It is performed directly by the primary Claude Code session as the final step of any product runbook, because it must synthesize every specialist's output into one user-facing verdict using the full conversation context — spawning it as a separate subagent would lose that context. The relevant product runbook's own instructions (e.g. [[06_PRODUCT_RUNBOOKS/Daily Anchor]]) are this role's invocation.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
grep -c "not invoked through the Agent tool" "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
```
Expected: `7` headings (Mission, Responsibilities, Required inputs, Output contract, Constraints, Evidence labeling, Invocation); `1` match confirming the Orchestrator's special invocation note is present.

---

## Task 13: Daily Anchor runbook (full build)

**Files:**
- Create: `06_PRODUCT_RUNBOOKS/Daily Anchor.md`

**Interfaces:**
- Consumes: all 9 agent spec files (Tasks 4–12), the Master Ledger and Active Handoff Snapshot (Task 3).
- Produces: the runbook Task 18's dry run follows step by step. This is the only product this pass that a Claude Code session can actually execute — every other product (Task 14) stops at "NOT YET BUILT."

- [ ] **Step 1: Write the runbook**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Daily Anchor.md`:

```markdown
# MARK CAOS — Daily Anchor

**Command:** `Run MARK CAOS Daily Anchor`
**Status:** ACTIVE
**Default schedule (inactive):** Monday–Friday 18:15, Mark's confirmed timezone — not configured; run this by typing the command above.

## Precondition check
Before calling any agent, read [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]. If its status is `UNINITIALIZED` or stale, this run operates in **RESEARCH-ONLY / DEGRADED mode**: state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` up front, and every checklist item below that depends on real holdings/cash reports that status instead of a fabricated result. Discovery and underwriting work still proceeds in full.

## The 19 mandatory work items and who produces them
1. First-line verdict — produced by the Orchestrator, last step.
2. Data and portfolio stamp — produced by the Verifier.
3. Broad Damage Gate with explicit denominator and comparison basis — produced by the Orchestrator from Verifier's price data; state `DATA LIMITED` if a live price read fails.
4. Forward-guidance review before decisions — produced by Forward Expectations.
5. Thesis review of every funded holding — produced by Portfolio Court; if the Ledger is `UNINITIALIZED`, state `N/A — no funded holdings on record`.
6. External Hunter Handoff Check — produced by Discovery; since the Hunter Watch product ([[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]]) is not yet built, state `NO HUNTER SIGNALS AVAILABLE — product not yet built`.
7. Handoff ACK Check — produced by the Orchestrator, reading the Active Handoff Snapshot.
8. Cumulative unresolved-handoff check — produced by the Orchestrator.
9. Visible discovery ledger across multiple asymmetric lanes — produced by Discovery.
10. Discovery budget: at least 12 public companies across at least 3 buckets, at least 3 genuinely fresh names, and at least 2 serious reviews — enforced by Discovery; if missed, Discovery's verdict line must read `DISCOVERY = SEARCH INCOMPLETE`.
11. 100%-cash holdings trial — produced by Portfolio Court.
12. Expected-CAGR, business-quality, and raw-asymmetry perspectives — produced by Underwriter and Portfolio Court together.
13. Next-uncommitted-euro ranking — produced by Portfolio Court.
14. Capital-recycling tribunal — produced by Portfolio Court.
15. Approved portfolio-count and No-Orphan tests — produced by Portfolio Court, against the draft rules in the Master Ledger §11.
16. Execution card — produced by the Orchestrator; suppressed and replaced with `HOLDINGS UNKNOWN / EXECUTION BLOCKED` if the Ledger is `UNINITIALIZED`.
17. Active Handoff Snapshot update — produced by the Orchestrator, only when authorized and verified.
18. Mechanical grades — produced by Red Team (hallucination/linkage/discovery/execution discipline), synthesized by the Orchestrator.
19. Logging status — produced by the Orchestrator: `LOG REQUIRED` (with a paste-ready combined event block) or `NO LOG REQUIRED`.

## Agent call sequence
No Workflow script and no custom subagent registration are used — this is Claude reading this runbook and calling the Agent tool directly, using each role's invocation prompt template from its own spec file.

1. Call the Agent tool once for the Verifier, using the invocation prompt template from [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]]. Wait for it to return and confirm `03_AGENT_RUNS/01_VERIFIER/VERIFIER_<date>_<runid>.md` was written.
2. Call the Agent tool three times **in the same turn** — one call each for Discovery ([[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery]]), Forward Expectations ([[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]), and Industry Read-through ([[03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through]]). These are independent of each other, so issuing all three tool calls in one response runs them concurrently — no script needed. Wait for all three to return.
3. Call the Agent tool once for the Underwriter, using [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]]. Wait for it to return.
4. Call the Agent tool twice **in the same turn** — Portfolio Court ([[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court]]) and Risk and Survivability ([[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability]]). Both depend only on the Underwriter's output, so they run concurrently. Wait for both.
5. Call the Agent tool once for Red Team, using [[03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team]]. Wait for it to return.
6. Perform the Orchestrator role directly (per [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator]]) — do not spawn a subagent for this step. Read all 8 specialist files from this run, write `03_AGENT_RUNS/09_ORCHESTRATOR/ORCHESTRATOR_<date>_<runid>.md` with the Full Run Map, update the Active Handoff Snapshot if authorized and verified, and present the final verdict in chat.

## Linking rule application
Every file written in steps 1–6 above must open with an "Inputs Consulted" section per each agent's own output contract. The Orchestrator's file additionally opens with the Full Run Map (a link to all 8 specialist files from this run, in the order they were called).

## Execution rules
- No autonomous trades, ever.
- No exact buy sizing without a live verified price and confirmed real cash.
- Preserve quantities until a confirmed fill.
- No margin.
- A rising or falling price alone never implies a buy or sell.

## Required output format
The Orchestrator's final chat message must include, in order: first-line verdict; data/portfolio stamp; discovery ledger summary; 100%-cash trial result; next-uncommitted-euro ranking; execution card or `HOLDINGS UNKNOWN / EXECUTION BLOCKED`; mechanical grades (the four Red Team grade lines); and `LOG REQUIRED` (with the paste-ready block) or `NO LOG REQUIRED`.

## Failure handling
If any agent call in steps 1–5 fails or returns an unusable result, do not continue as if it succeeded. Report a `LIMITED ANCHOR` (if enough of the pipeline completed to say something useful) or `FAILED ANCHOR` (if not), stating exactly what completed, what failed, and whether a manual rerun is needed. Never finish a run silently.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "06_PRODUCT_RUNBOOKS/Daily Anchor.md"
grep -c '^[0-9]\+\. ' "06_PRODUCT_RUNBOOKS/Daily Anchor.md"
```
Expected: `7` top-level headings (Precondition check, The 19 mandatory work items..., Agent call sequence, Linking rule application, Execution rules, Required output format, Failure handling); at least `19` numbered lines (the 19 checklist items — the agent-call-sequence's 6 numbered steps also match this pattern, so the count will be `25`; confirm it is at least `19`, not exactly `19`).

---

## Task 14: The other 9 product runbooks (stubs) and the Flight Recorder placeholder

**Files:**
- Create: `06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md`
- Create: `06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun.md`
- Create: `06_PRODUCT_RUNBOOKS/DCA Execution Card.md`
- Create: `06_PRODUCT_RUNBOOKS/Monster Census.md`
- Create: `06_PRODUCT_RUNBOOKS/Weekly Ranking.md`
- Create: `06_PRODUCT_RUNBOOKS/Deep Audit.md`
- Create: `06_PRODUCT_RUNBOOKS/Learning Review.md`
- Create: `06_PRODUCT_RUNBOOKS/Event Gate Watch.md`
- Create: `06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch.md`
- Create: `04_FLIGHT_RECORDER/README — Flight Recorder.md`

**Interfaces:**
- Consumes: `05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0.md` (Task 2) for the heading-anchor links each stub points to.
- Produces: the 9 stub files and the Flight Recorder placeholder that Task 15's Command Card links to.

- [ ] **Step 1: Write Post-Open Delta Check**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md`:

```markdown
# MARK CAOS — Post-Open Delta Check

**Command:** `Run MARK CAOS Post-Open Delta Check`
**Status:** NOT YET BUILT
**Default schedule (inactive):** ad hoc, intraday after market open

## What this product will do
Reports only what changed since a completed same-day Daily Anchor. It must state the price denominator it is comparing against and must never impersonate a full Anchor rerun — if no completed same-day Anchor exists, this product cannot run.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#21. Product distinctions]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 2: Write Emergency Thesis Rerun**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun.md`:

```markdown
# MARK CAOS — Emergency Thesis Rerun

**Command:** `Run MARK CAOS Emergency Thesis Rerun: <ticker/event>`
**Status:** NOT YET BUILT
**Default schedule (inactive):** ad hoc, triggered by Mark after material news

## What this product will do
Reruns the underwriting pipeline for one specific holding or candidate after material earnings, financing, contract, regulatory, or thesis evidence appears — not for generic price volatility alone. It is a targeted re-underwriting, not a full portfolio Anchor.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#21. Product distinctions]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 3: Write DCA Execution Card**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/DCA Execution Card.md`:

```markdown
# MARK CAOS — DCA Execution Card

**Command:** `Prepare MARK CAOS DCA Execution Card`
**Status:** NOT YET BUILT
**Default schedule (inactive):** shortly after Mark's confirmed monthly contribution date, once task capacity permits; otherwise manual whenever new cash is available

## What this product will do
Given a confirmed broker screenshot/export, real unlevered cash by currency, recent fills, and current verified prices, it reconciles the portfolio, checks market temperature and event risk, checks thesis integrity for every funded position, ranks the next uncommitted euro, and selects one or two targets (or a Mark-authorized basket) with exact executable sizing only when every execution gate passes. It states `DO NOTHING / HOLD CASH` when no candidate clears the minimum edge, and is never automatic equal feeding just because the calendar says DCA day.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#17A. DCA Execution Card]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 4: Write Monster Census**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Monster Census.md`:

```markdown
# MARK CAOS — Monster Census

**Command:** `Run MARK CAOS Monster Census`
**Status:** NOT YET BUILT
**Default schedule (inactive):** Saturday 09:00, Mark's confirmed timezone

## What this product will do
A weekly deep-discovery sweep: consumes all active handoffs first, reconciles External Hunter intake, searches at least 40 public companies across at least 5 buckets with at least 8 genuinely fresh names, ranks a Top-5 fresh/external-capital board, fully underwrites the Top 1–2 plus every active High-Priority Challenger plus one Anti-Echo fresh candidate, resolves every serious review to Seed/Challenger/Watch/Reject, and maintains a Conversion Scoreboard (Scanned → Serious Review → Monster File → Seed → Buy-Authorized → Purchased → Winner/Failure). Labels `SEARCH INCOMPLETE` when the search budget is missed, and triggers a Discovery Meta-Audit if 30 active Census days produce zero new buy-authorized candidates.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#14. Monster Census specification]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 5: Verify Steps 1–4**

Run:
```bash
for f in "Post-Open Delta Check" "Emergency Thesis Rerun" "DCA Execution Card" "Monster Census"; do
  echo "--- $f ---"
  grep -c "NOT YET BUILT" "06_PRODUCT_RUNBOOKS/$f.md"
done
```
Expected: `1` for each of the four files.

- [ ] **Step 6: Write Weekly Ranking**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Weekly Ranking.md`:

```markdown
# MARK CAOS — Weekly Ranking

**Command:** `Run MARK CAOS Weekly Ranking`
**Status:** NOT YET BUILT
**Default schedule (inactive):** Sunday 10:00, Mark's confirmed timezone

## What this product will do
Ranks every holding, funded Seed, buy-authorized Seed, Challenger, serious candidate, and cash against each other, showing raw-asymmetry and evidence/survivability-adjusted rankings separately. Runs head-to-head fights against the portfolio champion, quality anchor, strongest Seed, strongest Challenger, and cash. Produces separate next-uncommitted-euro and capital-recycling rankings, and audits stale gates, orphan positions, contradictions, and unresolved handoffs. On the first Weekly run of each month, also runs Architecture Maintenance, the manual Deep Audit reminder, and the Family-Wealth Architecture Check.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#15. Weekly Ranking specification]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 7: Write Deep Audit**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Deep Audit.md`:

```markdown
# MARK CAOS — Deep Audit

**Command:** `Run MARK CAOS Deep Audit`
**Status:** NOT YET BUILT
**Default schedule (inactive):** manual only

## What this product will do
Rebuilds the portfolio from 100% cash without anchoring on existing holdings, re-underwrites the mandate, market regime, holdings, Seeds, Challengers, and cash, runs the full multi-agent pipeline, tests every funded position for inclusion/sizing role/proof gate/replacement, and produces a complete next-euro capital map. It also audits the Master Ledger itself — reconciling it against the freshest broker state, checking every required section, and finding missing logs, duplicates, or contradictions. Creates the monthly [[04_FLIGHT_RECORDER/README — Flight Recorder]] entry after Mark reviews the result.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#18. Manual Deep Audit]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 8: Write Learning Review**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Learning Review.md`:

```markdown
# MARK CAOS — Learning Review

**Command:** `Run MARK CAOS Learning Review`
**Status:** NOT YET BUILT
**Default schedule (inactive):** monthly, after a completed Deep Audit and Flight Recorder — third day of the month at 10:00, Mark's confirmed timezone, if task capacity permits

## What this product will do
Uses the Master Ledger, Flight Recorder, prior rankings, and available outcomes to assess predictions that were right or wrong, good processes with bad outcomes and vice versa, false positives and negatives, missed candidates and omitted handoffs, evidence-quality failures, stale gates, ranking drift and incumbency bias, execution errors, and notification/scheduling/linkage failures. It may recommend system changes but must never implement a constitutional or architectural amendment without Mark's explicit approval.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#18A. Learning Review]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 9: Write Event Gate Watch**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Event Gate Watch.md`:

```markdown
# MARK CAOS — Event Gate Watch

**Command:** (automated watch — no manual trigger phrase in the source doc)
**Status:** NOT YET BUILT
**Default schedule (inactive):** daily 02:00, Mark's confirmed timezone

## What this product will do
Reads active event gates from the Active Handoff Snapshot and runs a post-event review only after the actual release, filing, presentation, or call material exists — a pre-release Anchor never satisfies a post-results gate. States `TRANSCRIPT PENDING` if a full transcript is unavailable. Includes the permanent NVIDIA gate: whenever NVIDIA publishes new earnings, CFO commentary, 10-Q, call material, or materially updated guidance, reviews Data Center/Hyperscale demand, Blackwell/Vera Rubin ramp, networking/optics/memory, financing constraints, China assumptions, gross margin, forward guidance, and read-through to connected MARK CAOS holdings.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#16. Event Gate Watch]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 10: Write Multi-Bagger Hunter Watch**

Use the Write tool to create `06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch.md`:

```markdown
# MARK CAOS — Multi-Bagger Hunter Watch

**Command:** `MARK CAOS Multi-Bagger Hunter Watch` (background watch, no manual trigger phrase in the source doc)
**Status:** NOT YET BUILT
**Default schedule (inactive):** daily condition watch, at most hourly

## What this product will do
Watches credible long-duration external sources (Motley Fool Stock Advisor/Rule Breakers/high-conviction lists, Seeking Alpha Alpha Picks/high-confidence Quant ideas, IBD 50 changes/Stock of the Day, notable TipRanks elite-analyst signals, and other sources Mark later admits) for materially new or changed signals. Deduplicates on SOURCE + TICKER + RECOMMENDATION_OR_CHANGE_DATE. Every qualified signal must independently verify the underlying company evidence and resolve to High-Priority Challenger, Challenger, trigger-gated Watch, or Reject — external sources are scouts only, never authority.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#13. External Multi-Bagger Hunter Watch]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
```

- [ ] **Step 11: Write the Flight Recorder placeholder**

Use the Write tool to create `04_FLIGHT_RECORDER/README — Flight Recorder.md`:

```markdown
# MARK CAOS — Flight Recorder

STATUS: EMPTY — no entries yet.

The Flight Recorder stores consolidated lessons, predictions, errors, false positives, false negatives, ranking changes, unresolved investigations, action queues, and architecture lessons. It does not replace the Master Ledger.

It is created monthly by the Deep Audit product (see [[06_PRODUCT_RUNBOOKS/Deep Audit]], status: NOT YET BUILT) after Mark reviews a completed Deep Audit result. No Flight Recorder entries exist until that product is built and run.
```

- [ ] **Step 12: Verify Steps 6–11**

Run:
```bash
for f in "Weekly Ranking" "Deep Audit" "Learning Review" "Event Gate Watch" "Multi-Bagger Hunter Watch"; do
  echo "--- $f ---"
  grep -c "NOT YET BUILT" "06_PRODUCT_RUNBOOKS/$f.md"
done
grep -c "EMPTY" "04_FLIGHT_RECORDER/README — Flight Recorder.md"
```
Expected: `1` for each of the five product files; `1` (at least) for the Flight Recorder file.

---

## Task 15: START HERE and Command Card

**Files:**
- Create: `00_START_HERE/MARK CAOS — START HERE.md`
- Create: `00_START_HERE/MARK CAOS — COMMAND CARD.md`

**Interfaces:**
- Consumes: every file created in Tasks 1–14 (this task's job is to correctly summarize and link to all of them).
- Produces: `[[00_START_HERE/MARK CAOS — START HERE]]` and `[[00_START_HERE/MARK CAOS — COMMAND CARD]]`, referenced by Task 16 (Operator Manual) and by `CLAUDE.md`'s trail (CLAUDE.md points to the Operator Manual, which points here).

- [ ] **Step 1: Write START HERE**

Use the Write tool to create `00_START_HERE/MARK CAOS — START HERE.md`:

```markdown
# MARK CAOS — START HERE

## Instance Identity
- INSTANCE_NAME: MARK CAOS
- OWNER: Mark
- DECISION_AUTHORITY: Mark
- EXECUTION_AUTHORITY: Mark only

## Absolute Isolation Rule
This is an independent MARK CAOS instance. It must never connect to, copy, or modify Bill's personal CAOS, Bill's Master Ledger, Koziris Portfolio, or any other person's portfolio. This rule has no exceptions.

## Canonical Links
- Operator Manual: [[00_START_HERE/MARK CAOS — OPERATOR MANUAL]]
- Command Card: [[00_START_HERE/MARK CAOS — COMMAND CARD]]
- Master Ledger: [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]
- Active Handoff Snapshot: [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]
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
See [[00_START_HERE/MARK CAOS — COMMAND CARD]] for the full list and build status.

## Notification Certification State
N/A — no automation configured in this build.

## Latest Architecture Version
v1.0 — flagship build (Daily Anchor fully working; 9 other products documented as NOT YET BUILT). Design source: [[docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design]] (outside this vault's numbered folders, in the project's `docs/` folder).
```

- [ ] **Step 2: Write Command Card**

Use the Write tool to create `00_START_HERE/MARK CAOS — COMMAND CARD.md`:

```markdown
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

## Background Watches
These two products run as background watches in the source design, not manual commands, so they have no Command Card row above — link to them directly instead:
- [[06_PRODUCT_RUNBOOKS/Event Gate Watch]] — NOT YET BUILT
- [[06_PRODUCT_RUNBOOKS/Multi-Bagger Hunter Watch]] — NOT YET BUILT
```

- [ ] **Step 3: Verify**

Run:
```bash
grep -c "ACTIVE" "00_START_HERE/MARK CAOS — START HERE.md"
grep -c "^| \`Run\|^| \`Prepare\|^| \`Audit\|^| \`Reconcile\|^| \`Show" "00_START_HERE/MARK CAOS — COMMAND CARD.md"
grep -c "Background Watches" "00_START_HERE/MARK CAOS — COMMAND CARD.md"
```
Expected: at least `3` matches for "ACTIVE" in START HERE; exactly `12` command rows in the Command Card table; `1` match for "Background Watches" (confirming Event Gate Watch and Multi-Bagger Hunter Watch are linked somewhere in the vault, even though they have no manual command).

---

## Task 16: Operator Manual

**Files:**
- Create: `00_START_HERE/MARK CAOS — OPERATOR MANUAL.md`

**Interfaces:**
- Consumes: every file created in Tasks 1–15 (this is the comprehensive synthesis document `CLAUDE.md` points to).
- Produces: `[[00_START_HERE/MARK CAOS — OPERATOR MANUAL]]`, the single file `CLAUDE.md` (Task 1) directs every session to read first.

- [ ] **Step 1: Write the Operator Manual**

Use the Write tool to create `00_START_HERE/MARK CAOS — OPERATOR MANUAL.md`:

```markdown
# MARK CAOS — Operator Manual

This is the single source of truth for how MARK CAOS operates. `CLAUDE.md` points here first. If you are Claude Code operating in this vault, you must read this file in full before doing anything else, and follow it exactly. Nothing here should require reading the original master prompt to operate day to day — that document is preserved at [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0]] for historical reference only.

## 1. Mission
CAOS exists to maximize expected long-run CAGR through survivable asymmetry. Its governing question: **if all investable capital were cash today, where should the next uncommitted euro be allocated?**

CAOS is not a newsletter, entertainment engine, momentum chaser, diversification template, or autonomous trader. It is an auditable capital-allocation operating system that continuously discovers, underwrites, compares, monitors, falsifies, ranks, and learns.

Mark remains the sole decision-maker and execution authority.

## 2. Instance Identity and Absolute Isolation
- INSTANCE_NAME: MARK CAOS
- OWNER / DECISION_AUTHORITY: Mark
- EXECUTION_AUTHORITY: Mark only
- This instance must never connect to, copy, or modify Bill's personal CAOS, Bill's Master Ledger, Koziris Portfolio, or any other person's portfolio. This rule has no exceptions.

## 3. Constitutional Laws
Apply these in every module and every run:
1. **Reality First.** Evidence outranks narrative.
2. **Radical Honesty.** Write UNKNOWN, DATA LIMITED, or UNVERIFIED when evidence is missing.
3. **Fresh-Evidence Supremacy.** Current verified evidence and the newest confirmed portfolio state override older prompts, rankings, or assumptions.
4. **Objective Supremacy.** No incumbent holding, legacy ranking, external source, prior conviction, diversification preference, or past conclusion receives protection.
5. **Ownership Before Consensus.** Early ownership is allowed when evidence is incomplete but sufficient, survivability is realistic, and asymmetry is compelling.
6. **Survivability Before Optionality.** Huge upside is rejected when financing, dilution, liquidity, business durability, or execution risk makes survival implausible.
7. **Expected Future CAGR From Today.** Cost basis, past gains, and emotional attachment do not determine ranking.
8. **Concentration Is Allowed, Not Worshipped.** Concentration is acceptable only when opportunity cost and survivability-adjusted expected CAGR justify it.
9. **Cash Is Valid.** Do nothing when no candidate clears the minimum edge.
10. **Process Over Outcome.** A good decision can lose; a bad decision can win. Judge process and evidence.
11. **Burden of Proof.** Claims of "best," "no challenger," "safe," "10x," or "thesis intact" require visible evidence.
12. **No Autonomous Trading.** CAOS never places trades or assumes fills.
13. **No Margin or Leverage by Default.** Buying power is not cash.
14. **No Fractional Stock Assumption.** Use whole-share sizing unless Mark's broker explicitly supports fractions and Mark confirms their use.
15. **No Kelly Engine.** Never claim Kelly sizing is implemented unless Mark explicitly authorizes a later audited module.

## 4. Portfolio-State Law
No file in this vault may hard-code current holdings, share counts, cash, weights, prices, cost bases, or profit/loss. The only controlling portfolio state is the freshest successfully reconciled state from: Mark's newest broker screenshot/export or explicit fill correction; [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL]]; or a newer verified portfolio-sync event.

At the start of every execution-sensitive run: stamp the portfolio source and timestamp; distinguish real unlevered cash from broker buying power; verify current prices and market status; preserve quantities until Mark confirms a fill; state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` if the controlling state is unavailable or stale.

Research may continue under degraded portfolio state, but portfolio-specific sizing, sell instructions, allocation changes, assumed fills, and holdings-based ledger mutations are prohibited.

**Current state of this vault:** the Master Ledger is UNINITIALIZED — Mark has not yet completed the one-time intake below. Every product runs in research-only / degraded mode until that intake is complete and the ledger is reconciled against a real broker source.

## 5. One-Time Installation Intake
Before any Mark-specific portfolio state is created, Mark must be asked for all of the following in one compact intake: personal timezone; country/tax residence (context only, not tax advice); broker and whether fractional shares are supported; investing horizon; typical monthly contribution and currency; maximum tolerable drawdown; objective and risk preference; liquidity needs and money that must not be invested; permission or prohibition regarding leverage and derivatives; sector/ethical/geographic/liquidity/security-type exclusions; current broker portfolio screenshot/export; current real cash by currency; any recent unshown buys, sells, deposits, withdrawals, or fills.

Do not ask Mark to repeat information already provided. Do not initialize exact holdings from memory or examples. This intake has not yet run in this build.

## 6. Sources and Evidence
This build's only research access is web search and web fetch (no financial-data API is connected). For each run: attempt the smallest relevant live read; if a source fails, state the gap; use official company IR and SEC/regulatory filings, exchanges, and other primary public sources as fallback; use high-quality independent reporting for corroboration; use secondary analysis only as secondary evidence; never fabricate provider consumption, consensus, prices, transcripts, filings, contracts, customers, or financial metrics.

Evidence labels — use only these five: `VERIFIED FACT`, `CAOS INFERENCE`, `UNVERIFIED LEAD`, `DATA LIMITED`, `UNKNOWN`.

Forward announced expectations (guidance, revenue ramps, margins, ARR, EBITDA, capex, capacity, contracts, customer ramps, delivery timing, financing and catalyst dates) receive very high weight. External stock-picking services are scouts, never authority.

## 7. The Agent Roster and Multi-Agent Pipeline
For the Daily Anchor (the only product built so far), nine specialist roles run in a fixed dependency order. Each role's full specification — mission, responsibilities, required inputs, output contract, constraints, and its exact Agent-tool invocation prompt — lives next to its own output folder:

1. [[03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier]]
2. [[03_AGENT_RUNS/02_DISCOVERY/_AGENT SPEC — Discovery]]
3. [[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]]
4. [[03_AGENT_RUNS/04_INDUSTRY/_AGENT SPEC — Industry Read-through]]
5. [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]]
6. [[03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court]]
7. [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability]]
8. [[03_AGENT_RUNS/08_RED_TEAM/_AGENT SPEC — Red Team]]
9. [[03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator]]

Run order (parallel lanes run as concurrent Agent-tool calls in the same turn — no script or Workflow tool is used):

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
               Orchestrator (the primary session, not a subagent)
```

No specialist writes to the Master Ledger or makes the final portfolio decision — only the Orchestrator proposes the combined ledger event, and only after Mark's explicit confirmation (see §10, Logging Standard).

**Linking rule:** every dated agent-run file opens with an "Inputs Consulted" section wikilinking the exact upstream files it read. This makes the dependency graph traversable in Obsidian: open any file's "Linked mentions" panel to see every file that later relied on it. The Orchestrator's file additionally carries a "Full Run Map" linking to all 8 specialist files from that run.

## 8. Candidate and Portfolio Taxonomy
Permitted candidate states: `UNKNOWN`, `WATCH WITH SPECIFIC TRIGGER`, `SERIOUS REVIEW`, `HIGH-PRIORITY CHALLENGER`, `CHALLENGER`, `BUY-AUTHORIZED SEED`, `CORE / ATTACKER`, `PORTFOLIO REPLACEMENT CANDIDATE`, `REJECT`, `RETIRED / ARCHIVED`, `RESOLVED`. Every serious review must eventually resolve to Seed, Challenger, trigger-gated Watch, or Reject — no vague limbo.

Draft portfolio-count rules (pending Mark's confirmation — see [[01_MASTER_LEDGER/MARK CAOS Master Ledger — CANONICAL#11. System Rules and Amendments|Master Ledger §11]]): target cap of seven funded public securities; maximum two funded Seeds; Core/Attacker positions normally on a path to ~5% of NAV; Seeds normally 1%-3%; sub-~1.5% positions require an explicit Seed/Catalyst role and proof gate; permanent sub-1% orphans are prohibited; a Seed must graduate, remain gated, or exit after two decisive evidence cycles; no new funded security if it would exceed the confirmed cap; drawdown alone is neither a sell nor a hold reason.

## 9. Standardized Handoff Protocol
Every material cross-module state change uses this block, recorded as its own heading in [[02_ACTIVE_HANDOFF/MARK CAOS — ACTIVE HANDOFF SNAPSHOT]]:

```
HANDOFF_ID = YYYYMMDD-MODULE-TICKER-CHANGE_TYPE
ORIGIN_MODULE = DAILY | HUNTER | CENSUS | WEEKLY | EVENT_GATE | MANUAL
ORIGIN_DATE = YYYY-MM-DD
SECURITY/TICKER =
HANDOFF_TYPE = HUNTER_SIGNAL | CANDIDATE_STATE | EVIDENCE_GATE | PORTFOLIO_TRIBUNAL | SYSTEM_STATE
SOURCE =
SOURCE_SIGNAL_DATE =
DEDUP_KEY = SOURCE|TICKER|SIGNAL_TYPE|DATE
PREVIOUS_STATE =
NEW_STATE =
EVIDENCE_QUALITY = HIGH | MEDIUM | LOW | DATA LIMITED
THESIS_OR_ASYMMETRY_CHANGE =
SURVIVABILITY_OR_FINANCING_CHANGE =
NEXT_GATE = exact date, event, metric, or filing
SUPERSEDES = prior HANDOFF_ID or NONE
RESOLVES_HANDOFF_ID = prior HANDOFF_ID or NONE
ACTIVE_UNTIL =
REQUIRED_CONSUMERS = DAILY,CENSUS,WEEKLY,HUNTER as relevant
MANDATORY_DEEP_UNDERWRITING = YES | NO
```

Every consumer of a handoff must output: `HANDOFF ACK CHECK: HANDOFF_ID | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO | RESOLVES_HANDOFF_ID`. If an expected handoff is unavailable, state `LINKAGE DEGRADED / HANDOFF UNAVAILABLE` — never hallucinate receipt or claim PASS.

## 10. Logging Standard
Log one event per material change, never duplicate unchanged noise. Default logging control is human-confirmed: whenever preservation is needed, say `LOG REQUIRED` and provide one paste-ready combined block; if nothing should be preserved, say `NO LOG REQUIRED`. Never claim a manual log was completed until Mark says `logged`. Subagents never write directly to the Master Ledger — only the Orchestrator may propose the combined ledger event.

Required event template:

```
============================================================
CAOS EVENT
============================================================
EVENT_ID = YYYY-MM-DD-MODULE-SUBJECT-CHANGE
EVENT_TYPE =
MODULE =
TIMESTAMP_LOCAL =
DECISION_AUTHORITY = Mark
EXECUTION_AUTHORITY = Mark only
TRANSACTION_RESULT = NO TRADE / CONFIRMED TRADE / NO FILL / CONFIRMED FILL

SOURCE_AND_PORTFOLIO_STATE
-

PREVIOUS_STATE
-

NEW_STATE
-

VERIFIED EVIDENCE
-

CAOS INTERPRETATION
-

SURVIVABILITY / FINANCING / DILUTION
-

ACTIONABILITY
-

NEXT PROOF GATE
-

SUPERSEDES / RESOLVES
-
============================================================
END CAOS EVENT
============================================================
```

## 11. Products and Build Status
See [[00_START_HERE/MARK CAOS — COMMAND CARD]] for the full command list. Only **Daily Anchor** is fully built this pass — see [[06_PRODUCT_RUNBOOKS/Daily Anchor]] for its complete runbook. The other 9 products are documented as stubs pointing to their source requirements in the archived master prompt, and are not yet runnable.

## 12. Execution Controls
- No autonomous trades, ever.
- No exact buy sizing without a live verified price and confirmed real cash.
- Preserve quantities until Mark confirms a fill.
- No margin or leverage by default.
- No fractional-share assumption unless Mark's broker explicitly supports it and Mark confirms.
- Price direction alone (a stock rising or falling) never implies a buy or sell.
- No Kelly-sizing claims unless Mark explicitly authorizes an audited module.

## 13. Hallucination and Integrity Firewall
Every final product must grade: source integrity, portfolio freshness, linkage completeness, discovery coverage, forward-guidance coverage, underwriting depth, ranking integrity, execution discipline, duplicate/logging control, notification/delivery status.

Prohibited: inventing facts or sources; using stale prices without disclosure; claiming "no challenger" without visible comparison; claiming full search without a disclosed search budget; treating price action as proof of thesis; treating external recommendations as authority; hiding degraded linkage; overwriting unresolved handoffs; silently shortening a full Anchor into a delta check; claiming a file was saved or a task created without verified readback; claiming the system is certified before delivery and linkage tests pass.

## 14. Acceptance Tests for This Build
- Every file described in this manual exists and is readable.
- `CLAUDE.md` correctly directs a fresh session to this manual.
- Typing `Run MARK CAOS Daily Anchor` produces, at minimum, a `LIMITED ANCHOR` or `FAILED ANCHOR` result stating exactly what ran and what didn't — never a silent failure — and, if all 8 specialist calls succeed, a full Anchor verdict with every specialist file and the Orchestrator file cross-linked per the linking rule in §7.
- Typing any of the other 9 Command Card commands returns that product's `NOT YET BUILT` stub rather than an improvised run.

## 15. Failure States and Human Duties
If the controlling portfolio state is unavailable or stale, the system states `HOLDINGS UNKNOWN / EXECUTION BLOCKED` rather than guessing. If a scheduled dependency fails mid-run, the system returns a `LIMITED ANCHOR` or `FAILED ANCHOR` naming what completed, what failed, and whether a manual rerun is needed — it never finishes silently.

Mark's duties: complete the one-time intake (§5) before expecting real portfolio-aware output; reply `logged` after manually pasting a `LOG REQUIRED` block so the system knows the entry is preserved; confirm or amend the draft portfolio-count rules (§8) before they are treated as binding; review Deep Audit and Learning Review outputs once those products are built, since the system will not implement architecture changes on its own.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c '^## ' "00_START_HERE/MARK CAOS — OPERATOR MANUAL.md"
grep -c '_AGENT SPEC —' "00_START_HERE/MARK CAOS — OPERATOR MANUAL.md"
```
Expected: `15` top-level sections; `9` matches for `_AGENT SPEC —` (one link per agent role).

---

## Task 17: Full-vault link integrity check

**Files:**
- Modify: none — this task only reads the files created in Tasks 1–16 and reports broken wikilinks. If it finds any, fix them in the file that contains the broken link before proceeding.

**Interfaces:**
- Consumes: every markdown file created in Tasks 1–16.
- Produces: a pass/fail confirmation that every `[[wikilink]]` in the vault resolves to a real file (and, where a heading anchor is used, a real heading in that file). Task 18's dry run depends on this having passed, since a broken "Inputs Consulted" link would silently defeat the whole design.

- [ ] **Step 1: Run the link-target check**

Run:
```bash
cd "/Users/markelman/Projects/CAOS"
grep -rhoE '\[\[[^]]+\]\]' 00_START_HERE 01_MASTER_LEDGER 02_ACTIVE_HANDOFF 03_AGENT_RUNS 04_FLIGHT_RECORDER 06_PRODUCT_RUNBOOKS 05_ARCHIVE 2>/dev/null \
  | sed -E 's/^\[\[(.*)\]\]$/\1/' \
  | sed -E 's/\|.*$//' \
  | sort -u \
  | while IFS= read -r link; do
      file="${link%%#*}"
      if [ ! -f "${file}.md" ]; then
        echo "BROKEN FILE: [[${link}]] -> ${file}.md not found"
        continue
      fi
      if [[ "$link" == *"#"* ]]; then
        heading="${link#*#}"
        if ! grep -qF "$heading" "${file}.md"; then
          echo "BROKEN HEADING: [[${link}]] -> heading \"$heading\" not found in ${file}.md"
        fi
      fi
    done
echo "Link check complete."
```

Expected: the only line printed is `Link check complete.` — no `BROKEN FILE` or `BROKEN HEADING` lines.

- [ ] **Step 2: Fix anything the check found**

If Step 1 printed any `BROKEN FILE` or `BROKEN HEADING` lines, open the file named before the `->` and correct the link — either the target file's actual path or the target heading's exact literal text (no slugs). Re-run Step 1 after each fix until it prints only `Link check complete.`

- [ ] **Step 3: Confirm every dated-output folder is currently empty**

Run:
```bash
for d in 01_VERIFIER 02_DISCOVERY 03_FORWARD 04_INDUSTRY 05_UNDERWRITER 06_PORTFOLIO_COURT 07_RISK_SURVIVABILITY 08_RED_TEAM 09_ORCHESTRATOR; do
  echo "--- $d ---"
  find "03_AGENT_RUNS/$d" -maxdepth 1 -type f | grep -v "_AGENT SPEC" || echo "(none)"
done
```
Expected: `(none)` for every folder — confirms no run has happened yet, so Task 18's dry run is the first real output in each folder.

---

## Task 18: Dry-run end-to-end validation of Daily Anchor

**Files:**
- Modify: none directly — this task exercises the whole system built in Tasks 1–17 by actually running it once, per the acceptance test in the spec (§11) and the Operator Manual (§14).

**Interfaces:**
- Consumes: `[[06_PRODUCT_RUNBOOKS/Daily Anchor]]` (Task 13) and everything it references.
- Produces: the first real dated output files in all 9 `03_AGENT_RUNS/0X_ROLE/` folders, proving the design in [[docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design]] actually works end to end, not just on paper.

- [ ] **Step 1: Trigger the run**

In a Claude Code session rooted in this vault (so `CLAUDE.md` has already been read), issue the command: `Run MARK CAOS Daily Anchor`. Follow [[06_PRODUCT_RUNBOOKS/Daily Anchor]] exactly: read the Master Ledger precondition check first (expect `UNINITIALIZED`, so this run is RESEARCH-ONLY / DEGRADED mode), then execute the six-step agent call sequence from the runbook using the Agent tool (Verifier alone; Discovery+Forward+Industry in parallel; Underwriter alone; Portfolio Court+Risk in parallel; Red Team alone; Orchestrator performed directly by the primary session).

- [ ] **Step 2: Verify all 9 dated files were written**

Run:
```bash
cd "/Users/markelman/Projects/CAOS"
for d in 01_VERIFIER 02_DISCOVERY 03_FORWARD 04_INDUSTRY 05_UNDERWRITER 06_PORTFOLIO_COURT 07_RISK_SURVIVABILITY 08_RED_TEAM 09_ORCHESTRATOR; do
  echo "--- $d ---"
  find "03_AGENT_RUNS/$d" -maxdepth 1 -type f -newer "06_PRODUCT_RUNBOOKS/Daily Anchor.md" | grep -v "_AGENT SPEC"
done
```
Expected: exactly one dated file listed per folder (nine total), each newer than the runbook file.

- [ ] **Step 3: Verify the Inputs Consulted / Full Run Map linking rule was actually followed**

Run:
```bash
for d in 01_VERIFIER 02_DISCOVERY 03_FORWARD 04_INDUSTRY 05_UNDERWRITER 06_PORTFOLIO_COURT 07_RISK_SURVIVABILITY 08_RED_TEAM; do
  f=$(find "03_AGENT_RUNS/$d" -maxdepth 1 -type f -newer "06_PRODUCT_RUNBOOKS/Daily Anchor.md" | grep -v "_AGENT SPEC")
  echo "--- $f ---"
  grep -c "Inputs Consulted" "$f"
done
f=$(find "03_AGENT_RUNS/09_ORCHESTRATOR" -maxdepth 1 -type f -newer "06_PRODUCT_RUNBOOKS/Daily Anchor.md" | grep -v "_AGENT SPEC")
grep -c "Full Run Map" "$f"
```
Expected: `1` for each of the 8 specialist files; `1` for the Orchestrator file's Full Run Map.

- [ ] **Step 4: Verify degraded-mode handling was honest, not fabricated**

Run:
```bash
f=$(find "03_AGENT_RUNS/06_PORTFOLIO_COURT" -maxdepth 1 -type f -newer "06_PRODUCT_RUNBOOKS/Daily Anchor.md" | grep -v "_AGENT SPEC")
grep -c "HOLDINGS UNKNOWN" "$f"
```
Expected: at least `1` — since the Master Ledger is `UNINITIALIZED`, Portfolio Court's holdings comparisons must report `HOLDINGS UNKNOWN / EXECUTION BLOCKED` rather than inventing a position.

- [ ] **Step 5: Re-run the link check from Task 17 to cover the new files**

Run the exact Step 1 command from Task 17 again.
Expected: still only `Link check complete.` — the newly written dated files must not introduce any broken link either.

- [ ] **Step 6: Confirm the chat verdict met the required output format**

Confirm the Orchestrator's final chat message (from Step 1) included, in order: first-line verdict; data/portfolio stamp; discovery ledger summary; 100%-cash trial result; next-uncommitted-euro ranking; `HOLDINGS UNKNOWN / EXECUTION BLOCKED` in place of an execution card; the four Red Team grade lines; and `LOG REQUIRED` or `NO LOG REQUIRED`. If any element is missing, treat this as a defect in [[06_PRODUCT_RUNBOOKS/Daily Anchor]] or the relevant agent spec — fix the file and repeat Step 1.

---

## Self-Review Notes

- **Spec coverage:** every numbered section of `docs/superpowers/specs/2026-08-28-mark-caos-obsidian-multiagent-design.md` (§2 vault structure → Task 1; §3 naming/linking → embedded in every task's output contract; §4 CLAUDE.md → Task 1; §5 canonical files → Tasks 3, 15, 16; §6 agent roster → Tasks 4–12; §7 Daily Anchor → Task 13; §8 stub template → Task 14; §9 execution model → Task 13 + Task 18; §10 out of scope → Global Constraints; §11 acceptance test → Tasks 17–18) has a corresponding task.
- **Placeholder scan:** no "TBD"/"TODO" remains; the two vague/self-contradictory verification steps found during drafting (Task 4 Step 2's heading count, Task 3 Step 3's Snapshot heading count) were corrected to firm expected values.
- **Path/type consistency:** all wikilink targets and file paths were cross-checked against the exact filenames each creating task uses (em dash "—" throughout, no `.md` suffix in wikilinks, heading-anchor links use literal heading text matching Task 16's and Task 2's actual headings).

Plan complete and saved to `docs/superpowers/plans/2026-08-28-mark-caos-obsidian-multiagent.md`. Two execution options:

**1. Subagent-Driven (recommended)** - I dispatch a fresh subagent per task, review between tasks, fast iteration

**2. Inline Execution** - Execute tasks in this session using executing-plans, batch execution with checkpoints

**Which approach?**
