# Monster Census Integration Checklist

## Daily Anchor Handoff Integration

- [ ] Active Handoff Snapshot has been updated with today's Daily Anchor handoffs
- [ ] Orchestrator consumes these handoffs in "Inputs Consulted" section
- [ ] Each handoff receives ACK check: `HANDOFF ACK CHECK: [ID] | RECEIVED=YES | APPLIED=YES/NO | ...`
- [ ] If any handoff is unreadable: Orchestrator states `LINKAGE DEGRADED / HANDOFF UNAVAILABLE` with handoff ID
- [ ] No handoff is claimed as APPLIED without being explicitly processed

## Master Ledger Logging

- [ ] Orchestrator output includes "Master Ledger Event" section with paste-ready event block OR `NO LOG REQUIRED` statement
- [ ] Event block includes all required fields: EVENT_ID, EVENT_TYPE, MODULE, TIMESTAMP_LOCAL, SOURCE_AND_PORTFOLIO_STATE, PREVIOUS_STATE, NEW_STATE, VERIFIED EVIDENCE, CAOS INTERPRETATION, SURVIVABILITY / FINANCING / DILUTION, ACTIONABILITY, NEXT PROOF GATE, SUPERSEDES / RESOLVES
- [ ] Event ID follows pattern: YYYY-MM-DD-CENSUS-SUBJECT-CHANGE
- [ ] If logging required: Mark can copy-paste the event block into Master Ledger and reply `logged`
- [ ] If no material changes: `NO LOG REQUIRED` is stated and no event block is emitted

## Active Handoff Snapshot Updates

- [ ] Orchestrator emits new handoff blocks for material state changes (new High-Priority Challenger, new Seed, evidence gate change, etc.)
- [ ] Each handoff follows standardized format: HANDOFF_ID, ORIGIN_MODULE, ORIGIN_DATE, SECURITY/TICKER, HANDOFF_TYPE, SOURCE, etc.
- [ ] Dedup key is used to prevent duplicates: SOURCE|TICKER|SIGNAL_TYPE|DATE
- [ ] Only the Orchestrator updates Active Handoff Snapshot (no direct agent writes)
- [ ] All handoff emissions are documented in Orchestrator output

## Weekly Ranking Integration

- [ ] Monster Census completes on Saturday 09:00
- [ ] Weekly Ranking runs on Sunday 10:00 (next day)
- [ ] New High-Priority Challengers from Monster Census are available to Weekly Ranking via Active Handoff Snapshot
- [ ] New Seeds from Monster Census are available to Weekly Ranking via updated Master Ledger candidate registry
- [ ] Weekly Ranking's Inputs Consulted section includes link to this run's Orchestrator file
- [ ] Handoff from Monster Census → Weekly Ranking is ACK'd by Weekly Ranking

## Post-Open Delta Check Independence

- [ ] Post-Open Delta Check is independent of Monster Census
- [ ] Post-Open Delta Check does not depend on Monster Census handoffs
- [ ] Post-Open Delta Check runs daily, Monster Census runs weekly
- [ ] No blocking or sequencing dependency between them

## File Naming and Structure Consistency

- [ ] All Discovery agent files follow naming: `DISCOVERY_INFRA_POWER_YYYY-MM-DD_CENSUS.md`, `DISCOVERY_CHIPS_MEMORY_YYYY-MM-DD_CENSUS.md`, `DISCOVERY_DEFENSE_AUTONOMY_YYYY-MM-DD_CENSUS.md`
- [ ] Orchestrator file follows naming: `ORCHESTRATOR_YYYY-MM-DD_CENSUS.md`
- [ ] All files are markdown format (.md)
- [ ] All files placed in correct folders: Discovery files in `03_AGENT_RUNS/02_DISCOVERY/`, Orchestrator in `03_AGENT_RUNS/09_ORCHESTRATOR/`
- [ ] All wikilinks use correct paths and headings

## Evidence and Sourcing Consistency

- [ ] All candidates labeled with evidence: VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN
- [ ] VERIFIED FACT labels are backed by cited public sources (SEC filings, earnings transcripts, company IR, etc.)
- [ ] No VERIFIED FACT is claimed without a source
- [ ] CAOS INFERENCE is clearly distinguished from verified facts
- [ ] Master Ledger Event evidence section cites all sources used in Monster Files

## Error Handling Compliance

- [ ] If one agent times out: Orchestrator labels run `CENSUS DEGRADED — Agent [A/B/C] incomplete`
- [ ] If fewer than 40 companies scanned or fewer than 8 fresh names: Orchestrator labels `SEARCH INCOMPLETE — [specific gaps]`
- [ ] If handoff is unreadable: Orchestrator states `LINKAGE DEGRADED / HANDOFF UNAVAILABLE — [handoff ID]`
- [ ] If candidate data conflicts with prior state: Orchestrator documents the conflict and supersession

## Acceptance Criteria Met

- [ ] Search completeness: At least 40 companies scanned, 5+ lanes covered, 8+ fresh names, OR `SEARCH INCOMPLETE` with disclosure
- [ ] Monster Files: Top 1–2 fresh candidates + all High-Priority Challengers + at least one Anti-Echo candidate underwritten
- [ ] Terminal resolution: Every candidate reviewed reaches exactly one state (Seed/Challenger/Watch/Reject)
- [ ] Conversion Scoreboard: Funnel tracked from Scanned to Purchased/Winner
- [ ] Handoff ACK: Every active Daily Anchor handoff acknowledged
- [ ] No autonomous trading: Sizing is never assumed; Mark decides on execution
- [ ] Logging: Master Ledger event emitted when material changes occur, or `NO LOG REQUIRED` stated

## Dry-Run Complete

- [ ] Dry-run test passed: All three agents completed, Orchestrator produced output, search completeness met
- [ ] Dry-run validation: Evidence labeling, deduplication, Monster File completeness, terminal resolution all verified
- [ ] Dry-run data quality: No hallucinations, all evidence sourced, handoff ACK checks complete
- [ ] Test results logged in [[04_FLIGHT_RECORDER/Monster Census Dry-Run Test]]
