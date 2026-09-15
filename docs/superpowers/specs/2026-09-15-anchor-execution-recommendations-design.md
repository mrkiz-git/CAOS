# CAOS Anchor Execution Recommendations — Design Specification

**Date:** 2026-09-15
**Owner and decision authority:** Mark
**Status:** APPROVED IN CHAT
**Scope:** Daily Anchor execution output, off-hours limit-price recommendations, and market-open validation

## 1. Purpose

Every CAOS Daily Anchor must end with a clear execution recommendation. This applies whether the US market is open or closed and covers both buying and selling.

CAOS remains advisory. It prepares the exact order recommendation, but Mark reviews and manually enters any order with his chosen broker. CAOS never connects to a broker, submits an order, assumes execution, or records a fill without Mark's confirmation.

## 2. Approved Operator Decisions

- Every Anchor must provide an execution recommendation.
- Recommendations cover both buys and sells.
- Limit-price style is `BALANCED`.
- Recommended limit orders expire at the end of one US trading day.
- Off-hours recommendations may include exact broker-supported sizing and a limit price when the required evidence is available.
- Mark manually enters every order with his chosen broker.
- Doing nothing remains a valid execution recommendation.

## 3. Mandatory Anchor Verdict

Every Daily Anchor must end with exactly one top-level execution verdict:

- `EXECUTE` — the regular US session is open and all execution gates pass.
- `CONDITIONAL EXECUTE` — a complete off-hours limit order is available and may be queued subject to its stated conditions.
- `HOLD CASH` — available cash should remain uncommitted.
- `NO CHANGE` — retain current holdings and place no order.
- `EXECUTION BLOCKED` — CAOS has a directional view but one or more required execution inputs are missing or unreliable.

The execution section may never be omitted. If no trade has a positive expected edge over cash and the current portfolio, the result must be `HOLD CASH` or `NO CHANGE` rather than a forced order.

## 4. Session and Price Model

CAOS must reason in US exchange sessions rather than local calendar days.

Every execution-sensitive output must include:

```text
SESSION_ID = next or current US core-session date, YYYY-MM-DD
MARKET_STATE = PRE_OPEN | CORE_OPEN | AFTER_HOURS | CLOSED_HOLIDAY | CLOSED_WEEKEND | UNKNOWN
BASELINE_SESSION = most recent completed US core-session date
BASELINE_PRICE_TYPE = OFFICIAL_CLOSE | BROKER_CLOSE | INDICATIVE_PREMARKET | LIVE_BID_ASK | UNKNOWN
BASELINE_PRICE_SOURCE = source name and direct reference
BASELINE_PRICE_TIMESTAMP = timestamp with timezone
PORTFOLIO_SOURCE = source and timestamp
FX_SOURCE = source and timestamp, or DATA LIMITED
```

The morning Anchor uses the last completed US core session, not simply the previous calendar day. Monday, exchange-holiday, and early-close cases must resolve through an official exchange calendar.

Official closing prices and pre-market indications must be displayed separately. An indicative pre-market price may inform risk, but it may not be described as an official close or an executable quote.

## 5. Mandatory Order Fields

For every proposed buy or sell, the execution card must include:

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

If the Anchor proposes more than one order, it must state the sequence and whether later orders depend on earlier fills. Cash from an unconfirmed sale may not fund a proposed purchase as if the sale had filled.

## 6. Balanced Limit-Price Policy

### 6.1 Valuation boundary

Before CAOS recommends a limit price, Underwriter and Portfolio Court must provide a defensible valuation boundary:

- A buy requires a maximum price at which the candidate still clears the minimum expected-return edge over cash and alternatives.
- A sell requires a minimum acceptable sale price consistent with the reason for selling and the opportunity cost of waiting.
- If no defensible boundary exists, the order is `EXECUTION BLOCKED` or `WAIT FOR OPEN`. CAOS must not invent a limit price.

### 6.2 Pre-open balanced limit

- `BUY LIMIT = lower of the last completed regular-session close and the maximum justified buy price`.
- `SELL LIMIT = higher of the last completed regular-session close and the minimum acceptable sell price`.
- Prices must be rounded to the instrument's supported price increment.
- A verified pre-market observation is shown separately and may cause `WAIT FOR OPEN`, but it does not silently replace the completed-session baseline.

This policy avoids chasing an opening gap. It also means an order may not fill, which is an acceptable result.

### 6.3 Core-session balanced limit

When a reliable live bid and ask are available:

- Start with the current bid/ask midpoint.
- A buy limit may not exceed the maximum justified buy price.
- A sell limit may not fall below the minimum acceptable sell price.
- If the spread, liquidity, or timestamp is unreliable, return `WAIT FOR OPEN` or `EXECUTION BLOCKED`.

CAOS does not use a market order as a fallback when a limit order does not fill.

## 7. Queue Eligibility

An off-hours order may receive `QUEUE LIMIT NOW` only when all of these conditions pass:

- Portfolio quantities and real unlevered cash are current and reconciled.
- The baseline price is from the last completed regular US session and has a source and timestamp.
- The valuation boundary is visible and supported by the underwriting.
- No earnings release, filing, regulatory decision, or other known thesis-changing event is expected before the opening auction.
- The security is sufficiently liquid for the proposed order.
- The broker's current support for the proposed quantity type, limit order, and one-day expiry is verified.
- Fees and FX are verified or shown conservatively without creating false precision.
- The limit order does not rely on proceeds from an unconfirmed sale.
- The proposed quantity complies with portfolio-count, role, survivability, concentration, and no-orphan rules.

Use `WAIT FOR OPEN` when any of the following applies:

- Important news or a scheduled catalyst can occur before the open.
- The pre-market indication is materially outside the approved limit or valuation range.
- Volatility, spread, liquidity, price provenance, or FX is unreliable.
- The thesis is broken and a sell limit based on the prior close could prevent a necessary review of a gap-down opening.
- Broker support for the required quantity type or order settings is unknown or unavailable.

## 8. Broker Capability Constraint

CAOS must not hard-code broker capabilities. Broker features can change and may differ by country, account, instrument, or order type. Therefore:

- Every execution-sensitive run verifies support for the proposed order type, quantity type, expiry, currency, and instrument.
- Fractional sizing is permitted only when current broker evidence confirms that fractional limit orders are supported for that instrument and account.
- If fractional limit support is unavailable, CAOS uses whole shares or returns `EXECUTION BLOCKED` when whole-share sizing would break the intended allocation or no-orphan rules.
- CAOS may not silently create a permanent orphan position.
- A full exit that cannot be represented by a supported limit order requires a separate live-session review and explicit Mark decision.
- Missing broker-capability evidence is labeled `DATA LIMITED` or `UNKNOWN`; CAOS must not guess.

## 9. Market-Open Validation

Add the command:

`Run CAOS Market-Open Execution Validation`

The command consumes the Anchor prepared for the matching `SESSION_ID` and performs a short validation:

1. Verify that the US core session is open.
2. Refresh broker quantities, real cash, live bid/ask, FX, spread, fees, and market status.
3. Check material news and guidance published since the Anchor.
4. Recalculate the proposed quantity and limit price.
5. Return `CONFIRM`, `ADJUST`, `CANCEL`, `NO ORDER`, or `EXECUTION BLOCKED` for each proposed order.
6. If a complete DCA or rebalancing card is needed, hand off to the DCA Execution Card workflow.

The current Post-Open Delta Check may be extended or renamed to implement this command. Its prerequisite must change from a same-calendar-day Anchor to an Anchor with the matching US `SESSION_ID`.

A queued `QUEUE LIMIT NOW` order can execute at the opening auction before CAOS performs this validation. This is why queue eligibility is stricter than ordinary research eligibility. A `WAIT FOR OPEN` order must not be entered before validation.

## 10. Fill and State Handling

- Partial or full execution is never assumed.
- Portfolio quantities remain unchanged until Mark provides a broker confirmation or explicit fill correction.
- Mark's confirmation must include ticker, side, quantity, price, fees, FX, timestamp, and whether any part remains open when available.
- A partially filled one-day order expires at the end of that session. The unfilled quantity requires a new Anchor or explicit rerun; it does not roll forward automatically.
- Logging remains human-confirmed. CAOS provides one combined event block and waits for Mark to reply `logged`.

## 11. Files to Update

Implementation must update the smallest consistent set of canonical files:

- `00_START_HERE/CAOS — OPERATOR MANUAL.md`
- `00_START_HERE/CAOS — COMMAND CARD.md`
- `00_START_HERE/CAOS — START HERE.md`
- `00_START_HERE/CAOS — WORKFLOWS EXECUTION MANUAL.md`
- `06_PRODUCT_RUNBOOKS/Daily Anchor.md`
- `06_PRODUCT_RUNBOOKS/Post-Open Delta Check.md`
- `06_PRODUCT_RUNBOOKS/Post-Open Delta Check Design.md`
- `06_PRODUCT_RUNBOOKS/DCA Execution Card.md`
- `03_AGENT_RUNS/01_VERIFIER/_AGENT SPEC — Verifier.md`
- `03_AGENT_RUNS/06_PORTFOLIO_COURT/_AGENT SPEC — Portfolio Court.md`
- `03_AGENT_RUNS/09_ORCHESTRATOR/_AGENT SPEC — Orchestrator.md`

Other role specifications should change only if the new output contract requires it. Existing historical run outputs remain untouched.

## 12. Constitutional Amendment

Preserve the laws that Mark alone decides and executes, that fills are never assumed, and that margin and leverage are prohibited.

Amend the exact-sizing rule to allow conditional off-hours sizing only when:

- The last completed regular-session price is verified.
- Portfolio quantities and real unlevered cash are current.
- The order is a one-day limit order using a broker-supported quantity type.
- A valuation boundary and cancellation conditions are visible.
- The output is marked `CONDITIONAL EXECUTE`.

This is an exception for recommendation quality, not permission for autonomous trading.

## 13. Failure Handling

Every Anchor still produces the execution section when a dependency fails:

- Stale portfolio or cash: `EXECUTION BLOCKED` with the directional recommendation preserved where evidence supports it.
- Missing verified baseline price: `EXECUTION BLOCKED`.
- Missing valuation boundary: `EXECUTION BLOCKED — NO DEFENSIBLE LIMIT PRICE`.
- Missing live bid/ask during an open-session card: `WAIT FOR OPEN` or `EXECUTION BLOCKED`.
- Market holiday or weekend: bind the order to the next valid `SESSION_ID`; do not label the previous calendar day as a trading session.
- Unsupported or unknown broker capability: use a supported order structure or return `EXECUTION BLOCKED`.
- No candidate or holding change clears the edge: `HOLD CASH` or `NO CHANGE`.

## 14. Acceptance Tests

The updated system is accepted only when all tests below produce the stated behavior:

1. **Weekday pre-open:** Anchor uses the prior completed US close and produces a complete `CONDITIONAL EXECUTE`, `HOLD CASH`, `NO CHANGE`, or explicit block.
2. **Monday morning:** Friday is selected as the baseline when Friday was a regular session.
3. **Exchange holiday:** The session calendar skips the holiday and binds the recommendation to the next valid session.
4. **US/EU daylight-saving mismatch:** Market state is derived from US Eastern exchange time, not a hard-coded Sofia hour.
5. **Regular session open:** Live bid/ask and FX replace the conditional denominator after verification.
6. **Opening gap beyond buy limit:** The buy remains unfilled or is cancelled; CAOS does not chase it.
7. **Opening gap below sell limit:** The sell remains unfilled and is escalated for review; CAOS does not silently convert it to a market order.
8. **Material overnight news:** Queue eligibility fails and the card states `WAIT FOR OPEN`.
9. **Stale broker state:** Exact shares and limit price are blocked.
10. **Broker capability:** Supported whole-share or fractional sizing is used only after verification; unsupported or unknown capabilities produce an explicit block.
11. **Partial fill:** Holdings remain unchanged until Mark supplies the actual fill; the remaining order does not roll into the next day automatically.
12. **No positive edge:** The mandatory execution result is `HOLD CASH` or `NO CHANGE`.
13. **Link integrity:** Every changed runbook and role specification points to readable upstream inputs.
14. **Historical integrity:** No dated prior run output is rewritten.

## 15. Out of Scope

- Connecting CAOS to any broker.
- Submitting, cancelling, or modifying broker orders.
- Assuming or recording fills without Mark's confirmation.
- Market orders as an automatic fallback.
- Margin, leverage, derivatives, or Kelly sizing.
- Persistent multi-day orders.
- Automatic Master Ledger mutation.
