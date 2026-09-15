# CAOS Anchor Execution Recommendations Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make every Daily Anchor produce a broker-neutral buy, sell, hold-cash, no-change, or blocked execution recommendation, with balanced one-day limit prices and session-aware market-open validation.

**Architecture:** Extend the existing documentation-driven CAOS pipeline instead of adding a separate trading system. Verifier establishes the US session and execution inputs; Underwriter and Portfolio Court establish valuation boundaries and rank actions; Orchestrator produces the mandatory execution card; the existing Post-Open Delta workflow becomes the validation path for the matching US session.

**Tech Stack:** Markdown, Obsidian wikilinks, CAOS agent role contracts, shell-based contract and link checks using `rg`, `find`, and `test`.

**Spec:** `docs/superpowers/specs/2026-09-15-anchor-execution-recommendations-design.md`

## Global Constraints

- Mark is the sole decision-maker and execution authority.
- CAOS recommends orders but never submits, cancels, modifies, or assumes broker orders or fills.
- Every Anchor ends with exactly one of `EXECUTE`, `CONDITIONAL EXECUTE`, `HOLD CASH`, `NO CHANGE`, or `EXECUTION BLOCKED`.
- The balanced limit-price method and same-US-trading-day expiry apply to both buys and sells.
- The last completed US core session is the off-hours baseline; calendar-day shortcuts are prohibited.
- Broker capabilities are verified at run time and never hard-coded for a named broker.
- No market-order fallback, margin, leverage, derivatives, Kelly sizing, or automatic Master Ledger mutation.
- Existing dated files in `03_AGENT_RUNS/` and user-owned changes in the Master Ledger remain untouched.
- If Git-index writes remain restricted, complete and verify file changes but do not claim commits were created.

---

### Task 1: Establish the Constitutional Execution Contract

**Files:**
- Modify: `00_START_HERE/CAOS — OPERATOR MANUAL.md`
- Modify: `00_START_HERE/CAOS — START HERE.md`
- Modify: `00_START_HERE/CAOS — COMMAND CARD.md`

**Interfaces:**
- Consumes: Approved verdict names, session fields, broker-neutral capability rule, and Mark-only execution boundary from the design specification.
- Produces: Canonical rules that every runbook and agent specification must follow.

- [ ] **Step 1: Run the contract check and confirm the new contract is absent**

Run:

```bash
rg -n "CONDITIONAL EXECUTE|SESSION_ID|Market-Open Execution Validation|broker capabilities" \
  "00_START_HERE/CAOS — OPERATOR MANUAL.md" \
  "00_START_HERE/CAOS — START HERE.md" \
  "00_START_HERE/CAOS — COMMAND CARD.md"
```

Expected: no complete definition of all four terms; the check demonstrates that the approved contract is not yet implemented.

- [ ] **Step 2: Amend the Operator Manual laws and execution controls**

In §3, preserve `No Autonomous Trading` and add this rule directly after it:

```markdown
13. **Mandatory Execution Recommendation.** Every Daily Anchor ends with exactly one execution verdict: `EXECUTE`, `CONDITIONAL EXECUTE`, `HOLD CASH`, `NO CHANGE`, or `EXECUTION BLOCKED`. A recommendation may cover buys, sells, or both. Mark remains the only person who may enter or confirm an order.
```

Renumber later constitutional laws consistently. In §4, replace the blanket off-hours exact-sizing prohibition with:

```markdown
At the start of every execution-sensitive run, stamp `SESSION_ID`, `MARKET_STATE`, `BASELINE_SESSION`, price type/source/timestamp, portfolio source/timestamp, and FX source/timestamp. During the regular US session, exact sizing requires verified live execution inputs. Outside the regular session, exact conditional sizing may use the verified last completed regular-session price only when portfolio quantities and real cash are current, a valuation boundary is visible, broker support is verified, the order is a same-session limit order, and cancellation conditions are explicit.
```

Add to §12:

```markdown
- Every Anchor provides an execution verdict; doing nothing is expressed as `HOLD CASH` or `NO CHANGE`.
- Off-hours executable recommendations are labeled `CONDITIONAL EXECUTE` and use balanced limit prices with expiry at the end of the named US trading session.
- CAOS verifies broker support for the proposed order type, quantity type, expiry, currency, and instrument. It never hard-codes the capabilities of a named broker.
- CAOS never converts an unfilled limit order to a market order.
```

Update §14 acceptance tests with the five verdict names, session-aware pre-open behavior, market-open validation, broker-capability verification, and preserved no-autonomous-trading boundary.

- [ ] **Step 3: Expose the command and current scheduling state**

Add this Command Card row:

```markdown
| `Run CAOS Market-Open Execution Validation` | BUILT BY THIS CHANGE, UNPROVEN until its first linked real run | [[06_PRODUCT_RUNBOOKS/Post-Open Delta Check]] |
```

Keep `Run CAOS Post-Open Delta Check` as a backward-compatible alias and mark its relationship to the new command. In START HERE, keep automation `NOT CONFIGURED` unless a real automation is separately created and verified. Add the new manual command without claiming it is scheduled.

- [ ] **Step 4: Run the constitutional contract check**

Run:

```bash
rg -n "Mandatory Execution Recommendation|CONDITIONAL EXECUTE|SESSION_ID|Market-Open Execution Validation|never hard-codes" \
  "00_START_HERE/CAOS — OPERATOR MANUAL.md" \
  "00_START_HERE/CAOS — START HERE.md" \
  "00_START_HERE/CAOS — COMMAND CARD.md"
```

Expected: each new concept appears in its canonical location; START HERE still says scheduled automation is not configured.

- [ ] **Step 5: Commit only Task 1 files**

```bash
git add "00_START_HERE/CAOS — OPERATOR MANUAL.md" "00_START_HERE/CAOS — START HERE.md" "00_START_HERE/CAOS — COMMAND CARD.md"
git commit -m "feat: define anchor execution recommendation contract"
```

If Git-index writes are restricted, record that fact and continue without claiming a commit.

---

### Task 2: Make Specialist Outputs Execution-Aware

**Files:**
- Modify: `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md`
- Modify: `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md`
- Modify: `03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md`

**Interfaces:**
- Consumes: Canonical session and execution contract from Task 1.
- Produces: `EXECUTION READINESS` from Verifier, valuation boundaries and proposed actions from Portfolio Court, and the mandatory final execution card from Orchestrator.

- [ ] **Step 1: Run the specialist-contract check and confirm required fields are absent**

Run:

```bash
rg -n "BASELINE_SESSION|BROKER_CAPABILITY_STATE|MAXIMUM BUY PRICE|MINIMUM SELL PRICE|QUEUE LIMIT NOW" \
  "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md" \
  "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md" \
  "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
```

Expected: the complete cross-agent contract is absent.

- [ ] **Step 2: Extend the Verifier output contract**

Require a `Session and Execution Readiness` block before the Source Readiness table:

```text
SESSION_ID = ISO date of the current or next valid US core session
MARKET_STATE = PRE_OPEN | CORE_OPEN | AFTER_HOURS | CLOSED_HOLIDAY | CLOSED_WEEKEND | UNKNOWN
BASELINE_SESSION = ISO date of the most recent completed US core session
BASELINE_PRICE_TYPE = OFFICIAL_CLOSE | BROKER_CLOSE | INDICATIVE_PREMARKET | LIVE_BID_ASK | UNKNOWN
BASELINE_PRICE_SOURCE = source and direct reference
BASELINE_PRICE_TIMESTAMP = timestamp with timezone
PORTFOLIO_SOURCE = source and timestamp
FX_SOURCE = source and timestamp or DATA LIMITED
BROKER_CAPABILITY_STATE = VERIFIED | DATA LIMITED | UNKNOWN
EXECUTION READINESS = LIVE READY | CONDITIONAL READY | BLOCKED
```

Add responsibilities to verify exchange holidays, early closes, bid/ask freshness when open, and broker support for the proposed order type, quantity type, expiry, currency, and instrument. A pre-market indication must remain separate from the completed-session close.

- [ ] **Step 3: Extend the Portfolio Court output contract**

Require a visible action comparison across buy, sell, hold cash, and no change. For every proposed trade require:

```text
ACTION = BUY | SELL
MAXIMUM BUY PRICE = amount or NOT APPLICABLE
MINIMUM SELL PRICE = amount or NOT APPLICABLE
VALUATION BOUNDARY EVIDENCE = concise evidence chain
QUANTITY TYPE REQUIRED = WHOLE SHARES | FRACTIONAL SHARES
WHY THIS BEATS CASH AND NO CHANGE = concise comparison
```

Require Portfolio Court to block an exact order when the valuation boundary is missing. Sale proceeds remain unavailable for a later purchase until Mark confirms the sale fill.

- [ ] **Step 4: Extend the Orchestrator output contract**

Require the final output to end with one top-level verdict and, when an order is proposed, this complete block:

```text
TICKER =
ACTION = BUY | SELL
ORDER_STATUS = QUEUE LIMIT NOW | WAIT FOR OPEN
ORDER_TYPE = LIMIT
QUANTITY =
QUANTITY_TYPE = WHOLE SHARES | FRACTIONAL SHARES
BROKER_CAPABILITY_STATE = VERIFIED | DATA LIMITED | UNKNOWN
LIMIT_PRICE_USD =
LIMIT_PRICE_ROLE = MAXIMUM BUY PRICE | MINIMUM SELL PRICE
TIME_IN_FORCE = SAME US TRADING DAY
ESTIMATED_GROSS_VALUE =
ESTIMATED_FEES_AND_FX = amount or DATA LIMITED
EXPECTED_CASH_AFTER = amount or DATA LIMITED
PRICE_BASIS = source, timestamp, and price type
WHY_THIS_BEATS_ALTERNATIVES =
CANCEL_IF = explicit conditions
NEXT_VALIDATION = command and expected time
EXECUTION_AUTHORITY = Mark only
```

Require dependency-aware ordering for multiple trades and prohibit using unconfirmed sale proceeds.

- [ ] **Step 5: Run the specialist-contract check**

Run:

```bash
rg -n "EXECUTION READINESS|BROKER_CAPABILITY_STATE|MAXIMUM BUY PRICE|MINIMUM SELL PRICE|QUEUE LIMIT NOW|unconfirmed sale" \
  "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md" \
  "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md" \
  "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
```

Expected: Verifier owns session readiness, Portfolio Court owns valuation boundaries and action comparison, and Orchestrator owns final order construction.

- [ ] **Step 6: Commit only Task 2 files**

```bash
git add "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md" "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md" "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
git commit -m "feat: add execution contracts to CAOS agents"
```

If Git-index writes are restricted, record that fact and continue without claiming a commit.

---

### Task 3: Make the Daily Anchor Always Produce an Execution Verdict

**Files:**
- Modify: `06_PRODUCT_RUNBOOKS/Daily Anchor.md`

**Interfaces:**
- Consumes: Verifier session readiness, Portfolio Court action comparison and valuation boundaries, Risk and Red Team outputs.
- Produces: A mandatory broker-neutral execution verdict and zero or more balanced one-day limit-order recommendations.

- [ ] **Step 1: Confirm the current runbook allows the execution section to be suppressed**

Run:

```bash
rg -n "Execution card|suppressed|No exact buy sizing|Required output format" "06_PRODUCT_RUNBOOKS/Daily Anchor.md"
```

Expected: the current runbook can suppress the card and has no mandatory five-verdict contract.

- [ ] **Step 2: Replace the execution work item**

Replace work item 16 with:

```markdown
16. Mandatory execution recommendation — produced by the Orchestrator on every Anchor. It must return exactly one of `EXECUTE`, `CONDITIONAL EXECUTE`, `HOLD CASH`, `NO CHANGE`, or `EXECUTION BLOCKED`. When data is insufficient, preserve any supported directional view and state the missing execution inputs.
```

Add `Session and Execution Readiness` to the Verifier-dependent work items. Require every Anchor to identify the matching `SESSION_ID` and `BASELINE_SESSION` before downstream reasoning begins.

- [ ] **Step 3: Add balanced limit construction and queue eligibility**

Add these rules under Execution Rules:

```markdown
- Pre-open buy limit: lower of the last completed regular-session close and the maximum justified buy price.
- Pre-open sell limit: higher of the last completed regular-session close and the minimum acceptable sell price.
- Core-session limit: start from the verified live bid/ask midpoint, bounded by the maximum justified buy price or minimum acceptable sell price.
- `QUEUE LIMIT NOW` requires current portfolio quantities and cash, verified baseline, visible valuation boundary, no known pre-open thesis-changing event, acceptable liquidity, verified broker capability, and no dependence on unconfirmed sale proceeds.
- Otherwise use `WAIT FOR OPEN`, `HOLD CASH`, `NO CHANGE`, or `EXECUTION BLOCKED`.
- Never replace an unfilled limit order with a market order.
```

Insert the complete order fields from the Orchestrator contract into Required Output Format.

- [ ] **Step 4: Update failure handling**

Require the execution section even for `LIMITED ANCHOR` and `FAILED ANCHOR`. A failed pipeline normally returns `EXECUTION BLOCKED`, but it may return `HOLD CASH` or `NO CHANGE` when that conclusion is supported without the failed dependency. It may never fabricate shares or a price.

- [ ] **Step 5: Verify the Daily Anchor contract**

Run:

```bash
rg -n "Mandatory execution recommendation|CONDITIONAL EXECUTE|Pre-open buy limit|Pre-open sell limit|QUEUE LIMIT NOW|market order|SESSION_ID" "06_PRODUCT_RUNBOOKS/Daily Anchor.md"
```

Expected: all required concepts appear and no rule says the execution section is suppressed.

- [ ] **Step 6: Commit the Daily Anchor update**

```bash
git add "06_PRODUCT_RUNBOOKS/Daily Anchor.md"
git commit -m "feat: require execution verdict in every anchor"
```

If Git-index writes are restricted, record that fact and continue without claiming a commit.

---

### Task 4: Convert Post-Open Delta into Market-Open Execution Validation

**Files:**
- Modify: `06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md`
- Modify: `06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md`

**Interfaces:**
- Consumes: The latest completed Anchor whose `SESSION_ID` matches the current US session.
- Produces: Per-order `CONFIRM`, `ADJUST`, `CANCEL`, `NO ORDER`, or `EXECUTION BLOCKED`, plus a handoff to DCA Execution Card when a full card must be rebuilt.

- [ ] **Step 1: Confirm the calendar-day blocker exists**

Run:

```bash
rg -n "NO SAME-DAY ANCHOR|same-day Anchor|never scheduled independently" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md"
```

Expected: both documents bind validation to the local calendar date and prohibit independent scheduling.

- [ ] **Step 2: Replace the prerequisite with session matching**

Replace the same-day rule with:

```markdown
Read the latest completed Daily Anchor and require its `SESSION_ID` to equal the verified current US core-session date. If it does not match, return `EXECUTION VALIDATION BLOCKED — NO MATCHING SESSION ANCHOR`. The Anchor may have been produced on an earlier local calendar date when a weekend, holiday, or timezone boundary applies.
```

Keep `Run CAOS Post-Open Delta Check` as an alias. Make `Run CAOS Market-Open Execution Validation` the primary command and permit it to be scheduled only after the system independently verifies that the US core session is open.

- [ ] **Step 3: Expand the validation inputs and outputs**

Before thesis-delta work, require Verifier to refresh:

```text
CURRENT_SESSION_ID
CORE_SESSION_STATUS
CURRENT_BID
CURRENT_ASK
SPREAD
QUOTE_SOURCE_AND_TIMESTAMP
FX_SOURCE_AND_TIMESTAMP
CURRENT_REAL_CASH
CURRENT_QUANTITIES
BROKER_CAPABILITY_STATE
```

For every Anchor order, require one result:

```text
ORDER_VALIDATION = CONFIRM | ADJUST | CANCEL | NO ORDER | EXECUTION BLOCKED
VALIDATED_QUANTITY = amount or NOT APPLICABLE
VALIDATED_LIMIT_PRICE = amount or NOT APPLICABLE
CHANGE_FROM_ANCHOR = concise reason
MARK_ACTION = exact manual next step
```

Run fundamental re-checks when material news exists even if the price move is below the existing five-percent Delta threshold. Execution validation cannot use the five-percent threshold as permission to ignore a smaller move that crosses the recommended limit or valuation boundary.

- [ ] **Step 4: Add queued-order handling**

State that a `QUEUE LIMIT NOW` order may have executed at the opening auction before validation. The validator must first ask for or inspect actual broker order status. It must not recommend cancellation or adjustment as if a filled order were still pending. `WAIT FOR OPEN` orders must not be entered until validation returns `CONFIRM` or `ADJUST`.

- [ ] **Step 5: Verify both documents use the new contract**

Run:

```bash
rg -n "Market-Open Execution Validation|NO MATCHING SESSION ANCHOR|CURRENT_BID|CURRENT_ASK|CONFIRM.*ADJUST.*CANCEL|opening auction|five-percent" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md"
```

Expected: both files define matching-session validation, live execution inputs, order-state awareness, and the five possible validation results.

- [ ] **Step 6: Commit the validation workflow update**

```bash
git add "06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md" "06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md"
git commit -m "feat: add market-open execution validation"
```

If Git-index writes are restricted, record that fact and continue without claiming a commit.

---

### Task 5: Align DCA and the Workflow Manual

**Files:**
- Modify: `06_PRODUCT_RUNBOOKS/DCA Execution Card.md`
- Modify: `00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md`

**Interfaces:**
- Consumes: Mandatory Anchor execution card and Market-Open Execution Validation result.
- Produces: One coherent manual operating flow with no false local-time or broker-specific assumptions.

- [ ] **Step 1: Identify conflicting workflow language**

Run:

```bash
rg -n "18:15 \(after market close\)|same day|No exact buy sizing|fractional|Revolut|DCA CARD" \
  "00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md" \
  "06_PRODUCT_RUNBOOKS/DCA Execution Card.md"
```

Expected: the manual contains the incorrect `18:15 (after market close)` description and the DCA card does not consume the new session contract.

- [ ] **Step 2: Make the DCA card broker-neutral and session-aware**

Require DCA to consume `SESSION_ID`, current market state, the Anchor valuation boundary, and the latest validation result. Replace any named-broker capability statement with run-time verification. Use the same mandatory order fields and balanced limit-price policy as Daily Anchor. Preserve `DO NOTHING / HOLD CASH` when no candidate clears the edge.

Add:

```markdown
If invoked from Market-Open Execution Validation, this card may use only the validated price, FX, cash, quantity, and broker-capability state from the matching `SESSION_ID`. It must recalculate if any input timestamp is stale or any proposed earlier order has filled partially or fully.
```

- [ ] **Step 3: Correct the operating calendar**

In the Workflow Execution Manual:

- Remove the claim that 18:15 Europe/Sofia is after the US market close.
- Describe morning Anchor as an allowed pre-open workflow using the last completed US session.
- Describe US market timing in `America/New_York` exchange time and require dynamic timezone conversion.
- Add the Market-Open Execution Validation command after the matching morning Anchor.
- Preserve manual-only scheduling status unless a real automation is separately created and verified.
- Replace all hard-coded `CET` examples with explicit timezone identifiers or source timestamps.

- [ ] **Step 4: Verify the integrated workflow**

Run:

```bash
rg -n "SESSION_ID|Market-Open Execution Validation|America/New_York|last completed US|manual" \
  "00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md" \
  "06_PRODUCT_RUNBOOKS/DCA Execution Card.md"
```

Then run:

```bash
rg -n "18:15 \(after market close\)|Revolut|hard-coded CET" \
  "00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md" \
  "06_PRODUCT_RUNBOOKS/DCA Execution Card.md"
```

Expected: the first command finds the new integrated flow; the second command returns no matches.

- [ ] **Step 5: Commit the workflow integration**

```bash
git add "06_PRODUCT_RUNBOOKS/DCA Execution Card.md" "00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md"
git commit -m "docs: align DCA with session-aware execution"
```

If Git-index writes are restricted, record that fact and continue without claiming a commit.

---

### Task 6: Run Cross-Vault Acceptance and Integrity Checks

**Files:**
- Verify: all files modified in Tasks 1–5
- Do not modify: dated historical outputs under `03_AGENT_RUNS/`
- Do not modify: `01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL.md`

**Interfaces:**
- Consumes: All implementation changes.
- Produces: Evidence that the canonical documents agree and existing historical state was preserved.

- [ ] **Step 1: Verify every mandatory verdict appears in canonical contracts**

Run:

```bash
for term in "EXECUTE" "CONDITIONAL EXECUTE" "HOLD CASH" "NO CHANGE" "EXECUTION BLOCKED"; do
  rg -l "$term" "00_START_HERE/CAOS — OPERATOR MANUAL.md" "06_PRODUCT_RUNBOOKS/Daily Anchor.md" "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
done
```

Expected: each term is found in all three files.

- [ ] **Step 2: Verify the cross-agent ownership boundaries**

Run:

```bash
rg -n "EXECUTION READINESS" "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md"
rg -n "MAXIMUM BUY PRICE|MINIMUM SELL PRICE" "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md"
rg -n "QUEUE LIMIT NOW|TIME_IN_FORCE" "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
```

Expected: Verifier owns readiness, Portfolio Court owns valuation boundaries, and Orchestrator owns the final order card.

- [ ] **Step 3: Verify prohibited contradictions are gone**

Run:

```bash
rg -n "NO SAME-DAY ANCHOR|18:15 \(after market close\)|execution card.*suppressed|hard-code.*Revolut|fractional limit orders.*Revolut" \
  "00_START_HERE" "06_PRODUCT_RUNBOOKS" "03_AGENT_RUNS/01_VERIFIER" "03_AGENT_RUNS/06_PORTFOLIO_COURT" "03_AGENT_RUNS/09_ORCHESTRATOR" \
  --glob '*SPEC*.md' --glob '*.md'
```

Expected: no matches in canonical manuals, runbooks, or current role specifications. Historical dated output files are outside the intended rewrite scope and must not be edited to remove old language.

- [ ] **Step 4: Verify canonical wikilink targets**

Run:

```bash
for path in \
  "00_START_HERE/CAOS — OPERATOR MANUAL.md" \
  "00_START_HERE/CAOS — COMMAND CARD.md" \
  "00_START_HERE/CAOS — START HERE.md" \
  "00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md" \
  "06_PRODUCT_RUNBOOKS/Daily Anchor.md" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md" \
  "06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md" \
  "06_PRODUCT_RUNBOOKS/DCA Execution Card.md" \
  "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md" \
  "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md" \
  "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"; do
  test -r "$path"
done
```

Expected: exit status 0.

- [ ] **Step 5: Confirm user-owned and historical files were not included**

Run:

```bash
git status --short
git diff --name-only
```

Expected: no dated file under `03_AGENT_RUNS/` appears in the implementation diff, and the pre-existing Master Ledger modification remains separate from this work.

- [ ] **Step 6: Review the final diff for wording and whitespace errors**

Run:

```bash
git diff --check
git diff -- "00_START_HERE" "06_PRODUCT_RUNBOOKS" \
  "03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md" \
  "03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md" \
  "03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md"
```

Expected: `git diff --check` produces no output; the diff contains only the approved execution-contract changes.

- [ ] **Step 7: Create the final implementation commit when permitted**

If Tasks 1–5 were not committed because Git-index writes were restricted, do not retry destructively and do not claim a commit. Otherwise confirm the working tree contains no uncommitted implementation files. Do not include the user's pre-existing Master Ledger or dated run files in any commit.
