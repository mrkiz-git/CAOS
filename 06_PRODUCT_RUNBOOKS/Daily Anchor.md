# CAOS — Daily Anchor

**Command:** `Run CAOS Daily Anchor`
**Status:** ACTIVE
**Default schedule (inactive):** Monday–Friday 18:15, Mark's confirmed timezone — not configured; run this by typing the command above.

## Precondition check
Before calling any agent, read [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]]. If its status is `UNINITIALIZED` or stale, this run operates in **RESEARCH-ONLY / DEGRADED mode**: state `HOLDINGS UNKNOWN / EXECUTION BLOCKED` up front, and every checklist item below that depends on real holdings/cash reports that status instead of a fabricated result. Discovery and underwriting work still proceeds in full.

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
