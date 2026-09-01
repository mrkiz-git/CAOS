# Post-Open Delta Check Dry-Run Testing

## Scenario 1: Happy Path (All agents complete, material deltas detected)

### Setup
- Daily Anchor has completed for today (same-day)
- Master Ledger is current and initialized
- Current market data is available (prices, news feeds)
- Verifier, Forward Expectations, Underwriter, Portfolio Court, and Risk & Survivability agent specs are ready
- At least 3 candidates with ±5% price movement or material fundamental changes (earnings, guidance, news)

### Execution

#### 1. Invoke Verifier Agent
- Expected: Agent fetches current prices and establishes new denominator
- Expected output: Price snapshot with timestamp (e.g., "14:30 CET intraday")
- Should identify minimum 3 candidates with ±5%+ price moves
- Expected runtime: 2-5 minutes

#### 2. Invoke Forward Expectations Agent
- Expected: Agent screens changed candidates for earnings surprises, guidance changes, analyst revisions
- Expected output: Forward Expectations findings file with material news/earnings events
- Should flag candidates with earnings surprises, guidance changes, or significant news
- Expected runtime: 3-7 minutes

#### 3. Invoke Underwriter Agent
- Expected: Agent re-checks thesis validity on changed candidates
- Expected output: Underwriter brief re-checks on 3+ changed candidates
- Should verify thesis remains intact or identify degradation
- Expected runtime: 5-10 minutes

#### 4. Invoke Portfolio Court Agent
- Expected: Agent re-validates funded-holding thesis under new prices
- Expected output: Portfolio Court findings on affected CORE/ATTACKER/SEED holdings
- Should confirm survival or identify new risks
- Expected runtime: 3-5 minutes

#### 5. Invoke Risk & Survivability Agent
- Expected: Agent recalculates survival scores for moved positions
- Expected output: Updated survivability assessments for changed candidates
- Should provide survival % estimates and risk changes
- Expected runtime: 3-5 minutes

#### 6. Invoke Orchestrator (main session)
- Expected: Orchestrator reads Daily Anchor output from same session
- Expected output: `POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md`
- Should include:
  - Inputs Consulted section (wikilinks to all agent outputs)
  - Delta Summary (number of candidates with changes)
  - Changed Candidates table with: Ticker, Price Δ %, Change Type, Baseline Conviction, Updated Conviction, Thesis Verdict, Action
  - Orchestrator Verdict (1-2 sentence summary)
  - Handoff Emissions (if conviction shifts)
  - Master Ledger Event block or `NO LOG REQUIRED` statement
  - All evidence labeled (VERIFIED FACT, DATA LIMITED, UNKNOWN)

### Validation
- [ ] All five specialist agent files created and linked in Orchestrator output
- [ ] Orchestrator output has "Inputs Consulted" section with wikilinks to Daily Anchor and all specialist files
- [ ] Orchestrator output has "Full Run Map" linking all agent files
- [ ] Changed Candidates table includes: Ticker, Price Δ %, Change Type, Baseline Conviction, Updated Conviction, Thesis Verdict, Action
- [ ] Minimum 2-3 candidates detected with thesis changes
- [ ] No unchanged candidates listed (changed candidates only)
- [ ] Price denominator explicitly stated (e.g., "Bloomberg 14:30 CET")
- [ ] Unchanged candidates (not moved ±5%) correctly excluded from output
- [ ] All evidence labels present (VERIFIED FACT, DATA LIMITED, etc.)
- [ ] Handoff emissions emitted for conviction shifts with DEDUP_KEY (SOURCE|TICKER|DELTA_CHECK|DATE)
- [ ] Master Ledger event is paste-ready or `NO LOG REQUIRED` explicitly stated
- [ ] Orchestrator Verdict clearly states which positions hold, which need review, portfolio impact

---

## Scenario 2: Degraded State (One agent fails mid-run)

### Setup
Same as Scenario 1, but artificially limit one agent's resources or use a source that's temporarily unavailable to simulate failure.

### Execution

#### 1. Invoke Verifier Agent — succeeds
- Expected: Normal execution, price snapshot created

#### 2. Invoke Forward Expectations Agent — times out or returns incomplete results
- Expected: Agent fails, times out, or produces partial results (simulating data source outage)
- Expected state: No output file or incomplete file created

#### 3. Invoke Underwriter Agent — succeeds
- Expected: Normal execution, thesis checks completed for available data

#### 4. Invoke Portfolio Court Agent — succeeds
- Expected: Normal execution, funded holdings re-validated

#### 5. Invoke Risk & Survivability Agent — succeeds
- Expected: Normal execution, survival recalculated

#### 6. Invoke Orchestrator with four of five agent files available
- Expected: Orchestrator detects missing or incomplete Forward Expectations input
- Expected behavior: Orchestrator adjusts output to reflect degraded state and continues

### Validation
- [ ] Orchestrator labels run: `DELTA CHECK LIMITED — Forward Expectations incomplete` (or similar)
- [ ] Orchestrator states which agent(s) failed and data gaps
- [ ] Orchestrator explicitly marks evidence quality: `DATA LIMITED` for missing forward-guidance data
- [ ] Changed Candidates table still populated with available data
- [ ] Orchestrator does NOT emit full handoffs — states `HANDOFF BLOCKED — insufficient data`
- [ ] Orchestrator states: `MASTER LEDGER LOGGING BLOCKED — insufficient evidence for conviction shift`
- [ ] Output includes troubleshooting guidance (e.g., "Forward Expectations retry recommended")
- [ ] No claim of "thesis intact" without visible evidence from available agents
- [ ] Degraded state is clearly labeled (not silent failure)

---

## Scenario 3: No Material Deltas (All prices within ±5%, no fundamental changes)

### Setup
- Daily Anchor has completed
- Current prices are all within ±5% of Daily Anchor baseline
- No material earnings surprises, guidance changes, or significant news on any candidates
- Master Ledger is current

### Execution
Run all five agents and Orchestrator as normal.

### Validation
- [ ] Orchestrator consolidates findings
- [ ] No candidates identified with ±5%+ price movement
- [ ] No candidates identified with material fundamental changes
- [ ] Forward Expectations returns no material news/earnings events
- [ ] Underwriter confirms all theses intact
- [ ] Portfolio Court confirms funded holdings stable
- [ ] Risk recalculation shows no material survivability changes
- [ ] Orchestrator output states: `NO MATERIAL DELTAS DETECTED`
- [ ] Orchestrator verdict: "All theses intact. Daily Anchor convictions confirmed. NO LOG REQUIRED."
- [ ] No Changed Candidates table (or empty table)
- [ ] No Handoff Emissions section
- [ ] Master Ledger output: **NO LOG REQUIRED**
- [ ] File created but marked as "no action" in handoff queue

---

## Data Quality Checks

After Orchestrator completes, verify the following across all output files:

### Evidence Labeling Integrity
- Scan all changed candidates and verdict statements for evidence labels
- Check: Every evidence claim is labeled one of: `VERIFIED FACT` | `CAOS INFERENCE` | `UNVERIFIED LEAD` | `DATA LIMITED` | `UNKNOWN`
- Check: `VERIFIED FACT` claims cite specific public sources (Bloomberg, IR, earnings releases, news)
- Check: `CAOS INFERENCE` explains the derivation logic
- Check: `DATA LIMITED` is used when partial data available (e.g., Forward Expectations timeout)
- Check: `UNKNOWN` used only when data truly unavailable
- Expected: 100% compliant labeling across all candidates

### Deduplication
- Check: No duplicate ticker entries across the five specialist agent outputs
- Check: Candidate state is consistent across all mentions (no conflicting verdicts)
- If duplicates found: Verify Orchestrator merged them correctly and kept strongest evidence
- Expected: Each ticker appears once per scenario in consolidated output

### Master Ledger Cross-Check
- Check: No current CORE/ATTACKER/SEED holdings listed as "no change" when prices moved ±5%+
- Check: Conviction shifts match Daily Anchor baseline (no phantom state changes)
- Check: WATCH WITH SPECIFIC TRIGGER positions correctly identified and checked only if trigger occurred
- Check: No incumbent protection (legacy conviction overrides fresh evidence)
- Expected: Cross-check validates every conviction shift against Ledger baseline

### Handoff ACK Compliance
- Check: If Daily Anchor emitted handoffs on same-day candidates, Orchestrator output includes ACK for each
- Check: ACK format: `HANDOFF ACK CHECK: [ID] | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO`
- Check: DEDUP_KEY format: `SOURCE|TICKER|DELTA_CHECK|DATE` (prevents duplicate Delta Check handoffs on same ticker/date)
- Check: No missing handoffs (every active handoff acknowledged)
- Expected: 100% ACK coverage where applicable

### Thesis Re-Check Completeness
- For each changed candidate, check:
  - Thesis verdict explicitly stated (intact, degraded, confirmed, new conviction, etc.) ✓
  - Updated survival score provided (if applicable) ✓
  - Price impact on assumptions explained ✓
  - Forward-guidance changes documented (if applicable) ✓
  - Action implication clear (hold, review, escalate) ✓
- Expected: All fields present and justified for each changed candidate

### Terminal Resolution Logic
- Check: Every changed candidate has exactly one terminal state in Orchestrator output
- Check: States are only: `SEED` | `CHALLENGER` | `WATCH WITH SPECIFIC TRIGGER` | `CORE/ATTACKER` (unchanged) | `REJECT` (if shifted)
- Check: No vague limbo states like "Further Review" or "TBD"
- Check: State changes justified by evidence in Thesis Verdict column
- Expected: All changed candidates have definitive, evidence-backed resolution

### File Integrity
- Check: All five specialist files exist in `03_AGENT_RUNS/` subdirectories (Verifier, Forward, Underwriter, Portfolio Court, Risk)
- Check: Orchestrator file exists in `03_AGENT_RUNS/09_ORCHESTRATOR/`
- Check: File naming: `POST_OPEN_DELTA_YYYY-MM-DD_HHmm.md` (or `_DRY_RUN` variant for test)
- Check: All files use markdown format with proper wikilinks
- Check: Price denominator explicitly named in Orchestrator file (never claims full Anchor rerun)
- Check: No hallucinated prices, earnings, or news (all data traceable to sources)
- Expected: All files present, named correctly, linked properly

---

## Test Execution Checklist

Track all dry-run test executions in this table. Fill in details after each test run.

| Scenario | Test Run # | Date | Verifier Status | Forward Exp Status | Underwriter Status | Portfolio Court Status | Risk Status | Orchestrator Status | Delta Grade | Master Ledger Event | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Happy Path | 1 | TBD | | | | | | | | | |
| Happy Path | 2 | TBD | | | | | | | | | |
| Degraded (Forward Exp timeout) | 1 | TBD | | | | | | | | | |
| No Material Deltas | 1 | TBD | | | | | | | | | |

**No dry-run has been executed yet.** All rows above are placeholders pending an actual test run — do not fill in results without a verified, real execution. Per Operator Manual §13, inventing a test-execution record is prohibited.

**Instructions for completing the checklist:**
- Fill in Test Run # sequentially for each execution
- Record the actual date of test execution
- Agent Status: PASS, FAIL, TIMEOUT, INCOMPLETE
- Orchestrator Status: PASS, FAIL, PARTIAL, LIMITED
- Delta Grade: COMPLETE (all candidates checked), LIMITED (incomplete data), or BLOCKED (cannot run)
- Master Ledger Event: YES (if emitted), NO (if no changes), or LIMITED (if insufficient data)
- Notes: Candidate tickers detected, price moves, any anomalies or issues

---

## Troubleshooting

### If Verifier times out or cannot fetch prices:
- **Check:** Is web search available and responsive?
- **Check:** Are price sources (Bloomberg, Yahoo Finance, etc.) accessible?
- **Action:** Retry with reduced candidate list (3 instead of 5+)
- **Action:** If still timeout, mark as `VERIFIER TIMEOUT` and label output `DELTA CHECK BLOCKED — NO PRICE DATA`
- **Result tracking:** Document in Test Execution Checklist under "Notes"

### If Forward Expectations cannot access news/earnings data:
- **Check:** Are news sources (PR Newswire, IR websites, analyst sites) available?
- **Check:** Is web fetch working?
- **Action:** Retry with manual date-narrowing (e.g., "last 2 hours only")
- **Action:** If data truly unavailable, label evidence `DATA LIMITED — earnings/news source unavailable [TICKER1, TICKER2]`
- **Result tracking:** Document in Scenario 2 (Degraded State) execution notes

### If Orchestrator cannot read a specialist file:
- **Check:** File is saved in correct folder (e.g., `03_AGENT_RUNS/03_FORWARD/`)
- **Check:** File name matches expected pattern (e.g., agent name + date)
- **Check:** File is valid markdown and is readable
- **Action:** Re-run the failing agent, save with correct name and folder
- **Action:** If file truly unreadable, state `LINKAGE DEGRADED` and proceed with available specialist outputs
- **Result tracking:** Document in Scenario 2 (Degraded State) execution notes

### If Master Ledger event fails to paste or format:
- **Check:** Event block is paste-ready (no unescaped markdown syntax errors)
- **Check:** EVENT_ID is unique and not duplicating prior run
- **Check:** All required fields are present (EVENT_TYPE, MODULE, TIMESTAMP_LOCAL, etc.)
- **Action:** Copy event block to text editor, verify format, paste manually
- **Action:** Reply `logged` to confirm logging complete
- **Result tracking:** Document in Test Execution Checklist under "Notes"

### If price denominator is not explicit or Delta Check appears to claim full Anchor rerun:
- **Check:** Orchestrator file states denominator clearly (e.g., "Bloomberg 14:30 CET European close")
- **Check:** Output does not re-run discovery, industry structure, or full underwriting
- **Action:** Verify Orchestrator verdict is brief (1-2 sentences) and compares ONLY to Daily Anchor baseline
- **Result tracking:** Document as failure in Data Quality Checks section

---

## Pre-Test Validation Checklist

Before starting any test scenario, confirm:

- [ ] Daily Anchor output exists for today (same session)
- [ ] Daily Anchor file is readable and has complete output (all 8 agents + Orchestrator)
- [ ] Master Ledger is current and readable (status: UNINITIALIZED or INITIALIZED)
- [ ] Verifier spec is loaded and approved
- [ ] Forward Expectations spec is loaded and approved
- [ ] Underwriter spec is loaded and approved
- [ ] Portfolio Court spec is loaded and approved
- [ ] Risk & Survivability spec is loaded and approved
- [ ] Orchestrator spec is loaded and approved
- [ ] `03_AGENT_RUNS/` directory structure exists with subdirectories for each agent
- [ ] `04_FLIGHT_RECORDER/` directory exists for test tracking
- [ ] Web search and web fetch tools are accessible
- [ ] All required market data sources accessible (Bloomberg, IR, news feeds, etc.)

---

## Post-Test Validation Checklist

After each test run, confirm:

- [ ] All expected output files created (Verifier, Forward Expectations, Underwriter, Portfolio Court, Risk, Orchestrator)
- [ ] Data quality checks completed (all 7 categories reviewed)
- [ ] Evidence labels verified for compliance (VERIFIED FACT, DATA LIMITED, UNKNOWN, etc.)
- [ ] Terminal states verified for validity (SEED, CHALLENGER, WATCH, CORE, REJECT only)
- [ ] Handoff ACKs verified where applicable (100% coverage)
- [ ] Price denominator explicitly stated in Orchestrator file
- [ ] Changed candidates table accurate and complete
- [ ] No unchanged candidates listed
- [ ] Master Ledger event (if applicable) is paste-ready
- [ ] Test Execution Checklist row completed with all details
- [ ] Troubleshooting guide consulted for any issues
- [ ] No unresolved errors or warnings

---

## Success Criteria Summary

A test run is considered **successful** when:

### 1. Happy Path test:
- ✓ All 5 specialists complete and produce output files
- ✓ Orchestrator successfully consumes all 5 files
- ✓ Minimum 2-3 candidates identified with ±5%+ price moves or material news
- ✓ Changed Candidates table includes Ticker, Price Δ %, Change Type, Baseline Conviction, Updated Conviction, Thesis Verdict, Action
- ✓ All theses have explicit verdicts (intact, degraded, confirmed, etc.)
- ✓ Unchanged candidates excluded from output
- ✓ Price denominator explicitly stated (never impersonates full Anchor)
- ✓ All evidence labeled (VERIFIED FACT, DATA LIMITED, etc.)
- ✓ Handoff emissions include DEDUP_KEY (SOURCE|TICKER|DELTA_CHECK|DATE)
- ✓ Master Ledger event emitted if conviction shifts, or `NO LOG REQUIRED` stated
- ✓ All data quality checks pass
- ✓ All 12 acceptance criteria from design spec §11 verified

### 2. Degraded State test:
- ✓ Orchestrator detects and documents missing/incomplete specialist input
- ✓ Output clearly labeled `DELTA CHECK LIMITED` or similar
- ✓ Data quality labeled `DATA LIMITED` for missing elements
- ✓ Handoff emissions blocked (not emitted with incomplete data)
- ✓ Master Ledger event NOT emitted
- ✓ Evidence gaps disclosed (no silent failures)
- ✓ Troubleshooting guidance provided

### 3. No Material Deltas test:
- ✓ Orchestrator completes normally
- ✓ Output states `NO MATERIAL DELTAS DETECTED`
- ✓ Changed Candidates table is empty or absent
- ✓ No Handoff Emissions section
- ✓ Master Ledger output: `NO LOG REQUIRED`
- ✓ Data quality checks confirm no conviction shifts
- ✓ All agents completed; findings just indicate no action needed

---

## Acceptance Criteria Coverage (Design Spec §11)

This test suite verifies all 12 acceptance criteria from the Post-Open Delta Check design specification:

1. **✓ Product can read Daily Anchor output from same session**
   - Scenario 1: Orchestrator successfully reads Daily Anchor file via "Inputs Consulted" wikilink
   - Scenario 3: Confirms Anchor is available (test blocks if missing)

2. **✓ Verifier successfully fetches current prices and establishes new denominator**
   - Scenario 1 validation: Price snapshot created, denominator explicit (e.g., "14:30 CET")
   - Scenario 2: Verifier success in degraded state test

3. **✓ Forward Expectations → Underwriter → Portfolio Court/Risk run the serial chain post-Verifier**
   - All scenarios: Forward Expectations, then Underwriter, then Portfolio Court and Risk (parallel) invoked in that order after Verifier completes; each waits for its named predecessor's dated output file
   - Test execution table tracks completion of all five agents in sequence

4. **✓ Orchestrator consolidates findings and compares to Anchor baseline**
   - Scenario 1 validation: Changed Candidates table compares "Baseline Conviction" to "Updated Conviction"
   - Scenario 3: Confirms theses match baseline (no changes)

5. **✓ Changed candidates only in output (no noise)**
   - Scenario 1 validation: "No unchanged candidates listed" checkpoint
   - Scenario 3: Confirms no Changed Candidates table when no deltas

6. **✓ Price denominator explicitly stated (never impersonates full Anchor)**
   - All scenarios: Data Quality Check #7 (File Integrity) verifies denominator in Orchestrator file
   - Troubleshooting guide addresses this integrity constraint

7. **✓ Handoff emissions emit for conviction shifts with dedup key**
   - Scenario 1 validation: "Handoff emissions emitted for conviction shifts with DEDUP_KEY"
   - Scenario 2 validation: "Handoff emissions blocked" (degraded state)
   - Data Quality Check #4 verifies DEDUP_KEY format (SOURCE|TICKER|DELTA_CHECK|DATE)

8. **✓ Master Ledger event paste-ready or `NO LOG REQUIRED` stated**
   - Scenario 1: "Master Ledger event is paste-ready"
   - Scenario 2: "Master Ledger event NOT emitted" (degraded)
   - Scenario 3: "Master Ledger output: NO LOG REQUIRED"

9. **✓ File links to Daily Anchor via "Inputs Consulted" (Obsidian traversable)**
   - Scenario 1 validation: "Orchestrator output has "Inputs Consulted" section with wikilinks"
   - Backlinks in Obsidian automatically show consumers

10. **✓ Failure states explicitly named (no silent failures)**
    - Scenario 2 dedicated to degraded/failure states
    - Troubleshooting guide covers timeout, incomplete data, file access issues
    - All failures labeled (DELTA CHECK LIMITED, DATA LIMITED, LINKAGE DEGRADED, etc.)

11. **✓ No trades, no sizing, no autonomous execution**
    - All scenarios: Orchestrator Verdict is read-only (action: hold, review, escalate — never trade)
    - No buy/sell recommendation in output
    - No trade execution or sizing claims

12. **✓ All evidence labeled and sourced**
    - Data Quality Check "Evidence Labeling Integrity": every claim scanned for `VERIFIED FACT` | `CAOS INFERENCE` | `UNVERIFIED LEAD` | `DATA LIMITED` | `UNKNOWN`
    - `VERIFIED FACT` claims checked for cited public sources; expected 100% compliant labeling across all candidates

---

## Sign-Off Section

After all three test scenarios are complete and all data quality checks pass, mark the following:

### Scenario Completion Checkboxes

- [ ] **Happy Path (Scenario 1):** All 5 agents complete, minimum 2-3 deltas detected, Orchestrator consolidates correctly, all evidence labeled, handoffs emitted for shifts, Master Ledger event paste-ready
- [ ] **Degraded State (Scenario 2):** One agent times out or fails, Orchestrator detects gracefully, output labeled LIMITED, handoffs blocked, evidence gaps disclosed
- [ ] **No Material Deltas (Scenario 3):** All agents complete, no deltas ±5%, output states "NO MATERIAL DELTAS DETECTED," NO LOG REQUIRED confirmed

### Readiness Confirmation

- [ ] **Test file completeness:** This document contains 3 scenarios, 7 data quality checks, troubleshooting guide, tracking table, and all required checklists
- [ ] **All 12 acceptance criteria from design spec §11 covered by test scenarios**
- [ ] **All failure states tested (BLOCKED, DEGRADED, FAILED)**
- [ ] **Price-move threshold (±5%) test verified**
- [ ] **Evidence labeling (VERIFIED FACT, DATA LIMITED, UNKNOWN) validated**
- [ ] **Handoff dedup key (SOURCE|TICKER|DELTA_CHECK|DATE) tested**
- [ ] **No hallucinated prices, news, or earnings in test outputs**
- [ ] **All wikilinks functional (Daily Anchor baseline, specialist files)**
- [ ] **Pre-test and post-test checklists completed**

### Approval for Operational Deployment

- [ ] **Product Design Spec (§11 acceptance criteria):** All 12 items verified ✓
- [ ] **Failure Handling (§7):** BLOCKED, DEGRADED, FAILED states tested and labeled ✓
- [ ] **Handoff Protocol (§8):** Emissions, DEDUP_KEY, evidence quality tested ✓
- [ ] **Master Ledger Integration (§9):** LOG REQUIRED / NO LOG REQUIRED output validated ✓
- [ ] **Constitutional Laws (Operator Manual §3):** Reality First, Radical Honesty, Fresh-Evidence Supremacy confirmed ✓
- [ ] **Evidence Integrity (Design Spec §6):** All claims sourced, no hallucinations ✓

**Post-Open Delta Check is approved for operational deployment when all checkboxes above are marked.**

---

## Signed and Approved

| Item | Status | Date | Notes |
|---|---|---|---|
| Test Plan Completion | ⏳ | TBD | All 3 scenarios executed and validated |
| Data Quality Audit | ⏳ | TBD | All 7 categories verified |
| Design Spec Coverage | ⏳ | TBD | All 12 acceptance criteria confirmed |
| Operational Readiness | ⏳ | TBD | Approved for deployment |

---

**Version History:**
- **2026-08-31:** Dry-run test plan created (pre-deployment)
