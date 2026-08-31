# Monster Census Dry-Run Testing

## Scenario 1: Happy Path (All agents complete, consolidated ranking produced)

### Setup
- Daily Anchor has completed for this week
- Master Ledger is current
- All three Discovery agent specs are ready

### Execution

#### 1. Invoke Discovery Agent A
- Expected: Agent runs for ~10-15 minutes
- Expected output: `DISCOVERY_INFRA_POWER_2026-08-31_DRY_RUN.md`
- Should find minimum 15 companies, 2+ lanes, 4+ fresh names

#### 2. Invoke Discovery Agent B
- Expected output: `DISCOVERY_CHIPS_MEMORY_2026-08-31_DRY_RUN.md`
- Same coverage targets

#### 3. Invoke Discovery Agent C
- Expected output: `DISCOVERY_DEFENSE_AUTONOMY_2026-08-31_DRY_RUN.md`
- Same coverage targets

#### 4. Invoke Orchestrator
- Expected: Orchestrator reads all three files
- Expected output: `ORCHESTRATOR_2026-08-31_DRY_RUN.md`
- Should include:
  - Handoff ACK checks (at least one from Daily Anchor)
  - Consolidated ranking table (all companies merged)
  - Monster Files for 1–2 top candidates
  - Conversion Scoreboard
  - Search completeness grade
  - Master Ledger event block or NO LOG REQUIRED

### Validation
- [ ] All three Discovery files created and linked in Orchestrator output
- [ ] Orchestrator output has "Inputs Consulted" section
- [ ] Orchestrator output has "Full Run Map" linking all agent files
- [ ] Search completeness: At least 40 companies scanned (or SEARCH INCOMPLETE with gaps disclosed)
- [ ] Monster Files present for at least 2 candidates with business model, dilution, survivability assessment
- [ ] Conversion Scoreboard shows funnel (Scanned → Serious Review → etc.)
- [ ] Master Ledger event block is paste-ready or NO LOG REQUIRED is stated

---

## Scenario 2: Degraded State (One agent times out or fails)

### Setup
Same as Scenario 1, but artificially limit one agent's search budget or use a source that's temporarily unavailable.

### Execution

#### 1. Invoke Discovery Agent A — succeeds
- Expected: Normal execution and output file created

#### 2. Invoke Discovery Agent B — times out or returns incomplete results
- Expected: Agent fails, times out, or produces partial results
- Expected state: No output file or incomplete file created

#### 3. Invoke Discovery Agent C — succeeds
- Expected: Normal execution and output file created

#### 4. Invoke Orchestrator with only two of three agent files available
- Expected: Orchestrator detects missing or incomplete input
- Expected behavior: Orchestrator adjusts output to reflect degraded state

### Validation
- [ ] Orchestrator labels run: `CENSUS DEGRADED — Agent B incomplete`
- [ ] Orchestrator states which lanes were not fully searched
- [ ] Search completeness labeled: `SEARCH INCOMPLETE — Agent B failed; semiconductor/memory lanes not fully covered`
- [ ] Orchestrator does NOT emit handoffs or claim full coverage
- [ ] Master Ledger event is NOT emitted

---

## Scenario 3: No Material Changes (Census runs, no new Seed or Challenger promotions)

### Setup
Master Ledger already has comprehensive candidate coverage; discovery finds mostly incumbents.

### Execution
Run all three agents and Orchestrator as normal.

### Validation
- [ ] Orchestrator consolidates findings
- [ ] No new High-Priority Challengers found
- [ ] No new Seed promotions
- [ ] Orchestrator states: `NO LOG REQUIRED` (no material changes)
- [ ] No Master Ledger event emitted

---

## Data Quality Checks

After Orchestrator completes, verify the following across all output files:

### Evidence Labeling Integrity
- Scan all candidates for evidence labels
- Check: Every label is one of `VERIFIED FACT` | `CAOS INFERENCE` | `UNVERIFIED LEAD` | `DATA LIMITED` | `UNKNOWN`
- Check: VERIFIED FACT claims have cited public sources
- Check: CAOS INFERENCE explains the derivation
- Expected: 100% compliant labeling

### Deduplication
- Check: No duplicate tickers across the three Discovery agent outputs
- If duplicates found: Verify Orchestrator merged them and kept only the strongest evidence
- Expected: Each ticker appears once in consolidated ranking

### Master Ledger Cross-Check
- Check: No current holdings are listed as "fresh" without new evidence
- Check: Active Challengers that are still reviewed have updated thesis or new evidence
- Expected: No incumbent protection

### Handoff ACK Compliance
- Check: Orchestrator output includes HANDOFF ACK CHECK for every active handoff
- Check: ACK format: `HANDOFF ACK CHECK: [ID] | RECEIVED=YES | APPLIED=YES/NO | RESULTING_STATE | STILL_ACTIVE=YES/NO`
- Expected: 100% ACK coverage, no missing handoffs

### Monster File Completeness
For each Monster File produced, check:
- Business model described ✓
- Valuation denominator identified ✓
- Dilution path stated ✓
- Survivability assessed ✓
- Kill conditions listed ✓
- Scenarios (base/bull/bear) estimated ✓
- Terminal resolution state selected ✓

Expected: All fields present and justified

### Terminal Resolution Logic
- Check: Every candidate reviewed has exactly one terminal state
- Check: States are only: `SEED` | `CHALLENGER` | `WATCH WITH SPECIFIC TRIGGER` | `REJECT`
- Check: No vague limbo states like "Further Review" or "TBD"
- Expected: All candidates have definitive resolution

### File Integrity
- Check: All three Discovery files exist in `03_AGENT_RUNS/02_DISCOVERY/`
- Check: Orchestrator file exists in `03_AGENT_RUNS/09_ORCHESTRATOR/`
- Check: File names use correct date and "DRY_RUN" or actual run date
- Check: All files use markdown format with proper wikilinks
- Expected: All files present, named correctly, linked properly

---

## Test Execution Checklist

Track all dry-run test executions in this table. Fill in details after each test run.

| Scenario | Test Run # | Date | Agent A Status | Agent B Status | Agent C Status | Orchestrator Status | Search Grade | Master Ledger Event | Notes |
|---|---|---|---|---|---|---|---|---|---|
| Happy Path | 1 | 2026-08-31 | PASS | PASS | PASS | PASS | COMPLETE | YES | All agents completed, 42 companies, 9 fresh |
| Happy Path | 2 | TBD | | | | | | | |
| Degraded (Agent B timeout) | 1 | TBD | | | | | | | |
| No Material Changes | 1 | TBD | | | | | | | |

**Instructions for completing the checklist:**
- Fill in Test Run # sequentially for each execution
- Record the actual date of test execution
- Agent Status: PASS, FAIL, TIMEOUT, INCOMPLETE
- Orchestrator Status: PASS, FAIL, PARTIAL
- Search Grade: COMPLETE, SEARCH INCOMPLETE (note gaps), or N/A
- Master Ledger Event: YES (if emitted), NO, or N/A (if no material changes)
- Notes: Any issues, anomalies, or additional observations

---

## Troubleshooting

### If Agent A/B/C times out:
- **Check:** Is the search budget too high? (Currently 15+ companies per agent)
- **Check:** Is web search available and responsive?
- **Action:** Reduce search budget to 10 companies, retry
- **Action:** If still timeout, mark as `AGENT TIMEOUT` and skip to Orchestrator with available agents
- **Result tracking:** Document in Test Execution Checklist under "Notes"

### If Orchestrator can't read a Discovery file:
- **Check:** File is saved in correct folder (`03_AGENT_RUNS/02_DISCOVERY/`)
- **Check:** File name matches exact pattern (`DISCOVERY_[LANE]_YYYY-MM-DD_DRY_RUN.md`)
- **Check:** File is valid markdown and is readable
- **Action:** Re-run the failing agent, save with correct name and folder
- **Action:** If file truly unreadable, state `LINKAGE DEGRADED` and proceed with available files
- **Result tracking:** Document in Scenario 2 (Degraded State) execution notes

### If Master Ledger event fails to paste:
- **Check:** Event block is paste-ready (no markdown syntax errors)
- **Check:** Event ID is unique and not duplicating prior run
- **Action:** Copy event block to a text editor, verify format, paste manually
- **Action:** Reply `logged` to confirm logging complete
- **Result tracking:** Document in Test Execution Checklist under "Notes"

---

## Pre-Test Validation Checklist

Before starting any test scenario, confirm:

- [ ] Discovery Agent A spec is loaded and approved
- [ ] Discovery Agent B spec is loaded and approved
- [ ] Discovery Agent C spec is loaded and approved
- [ ] Orchestrator spec is loaded and approved
- [ ] Master Ledger is current and readable
- [ ] `03_AGENT_RUNS/02_DISCOVERY/` directory exists
- [ ] `03_AGENT_RUNS/09_ORCHESTRATOR/` directory exists
- [ ] All required tools and sources are accessible to agents

---

## Post-Test Validation Checklist

After each test run, confirm:

- [ ] All expected output files created
- [ ] Data quality checks completed (all 7 categories reviewed)
- [ ] Evidence labels verified for compliance
- [ ] Terminal states verified for validity
- [ ] Handoff ACKs verified where applicable
- [ ] Master Ledger event (if applicable) is paste-ready
- [ ] Test Execution Checklist row completed
- [ ] No unresolved errors or warnings

---

## Success Criteria Summary

A test run is considered **successful** when:

1. **Happy Path test:**
   - All 3 agents complete and produce output files
   - Orchestrator successfully consumes all 3 files
   - Search covers 40+ companies, 5+ lanes, 8+ fresh names
   - At least 2 Monster Files created with full details
   - Master Ledger event emitted if material changes exist
   - All data quality checks pass

2. **Degraded State test:**
   - Orchestrator detects and documents missing input
   - Output clearly labeled `CENSUS DEGRADED`
   - Search completeness accurately reflects gaps
   - No handoffs emitted
   - No Master Ledger event emitted

3. **No Material Changes test:**
   - Orchestrator completes normally
   - Output states `NO LOG REQUIRED`
   - No Master Ledger event emitted
   - Data quality checks confirm no new promotions
