# RISK_SURVIVABILITY_2026-09-03_DEEPAUDIT

## Inputs Consulted
- [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability]] (role spec, read in full)
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-03_DEEPAUDIT]] (today's Underwriter output — fresh Monster Files for all 8 current holdings)
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] (position sizes, §1 mandate, §11 draft sizing rules)

## Scope and Method Note
This is a Deep Audit. Per the task brief, the 100%-cash rebuild frame is applied to all 8 current holdings (PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF) for risk purposes: each holding is risk-mapped as if being evaluated for a fresh position today, not grandfathered in because it is already held. This agent does not re-underwrite the business cases (that is the Underwriter's completed job, consulted above) — it tests permanent-loss paths, concentration/liquidity/financing/dilution/customer-concentration/capital-intensity/maturity/regulatory/geographic/factor/correlated-thesis risk (whichever apply per holding), and sets explicit proof/warning/break gates. No numeric survival score (0–100) is fabricated: no such baseline exists anywhere upstream this cycle (Underwriter output above contains no survivability score field, and no prior Weekly Ranking/Daily Anchor score for 2026-09-03 was surfaced to this agent), so this run uses qualitative survivability ratings (HIGH/MODERATE/LOW survivability confidence) labeled with the standard evidence tags instead of inventing a number. This is consistent with the same gap already handled by Weekly Ranking and Daily Anchor this cycle.

Per spec: drawdown alone is neither a sell reason nor a hold reason — only a defined break gate below triggers a sell recommendation. This agent does not size positions, execute trades, or write to the Master Ledger.

**Position weights used (from Underwriter, CAOS INFERENCE arithmetic on Ledger-recorded shares × Verifier-sourced current price, denominator $10,817.67):** PLTR ≈35.6%, NVDA ≈29.8%, MSFT ≈9.0%, KO ≈9.0%, GOOGL ≈5.8%, TSLA ≈5.5%, IREN ≈2.7%, WULF ≈2.5%. **PLTR + NVDA combined ≈65.4% of holdings** — flagged explicitly below, consistent with the same finding already made on 2026-09-02 (Red Team) and reconfirmed independently by the Underwriter today.

---

## PORTFOLIO-LEVEL RISK MAP (applies across all 8 holdings)

### Concentration risk — VERIFIED FACT (arithmetic) / CAOS INFERENCE (weights)
- **PLTR + NVDA = ~65.4% of holdings in two names.** Master Ledger §11 draft rule targets ~5% per Core/Attacker position; PLTR sits at ~7x that norm, NVDA at ~6x. This is the single largest permanent-loss-path amplifier in the portfolio: it does not require either business to fail — a normal, non-fatal multiple-compression event in *either* name, if correlated (see Factor/Correlated-Thesis risk below), could inflict portfolio-level drawdown disproportionate to any one holding's individual risk profile.
- **Top 4 names (PLTR, NVDA, MSFT, GOOGL) = ~80.2% of holdings, all substantially AI-capex-thesis-linked.** This is a concentration risk that sits on top of, and is worse than, simple single-name concentration — see Correlated-Thesis risk below.
- No holding sits below the Ledger §11 draft ~1.5% Seed floor (IREN ~2.7%, WULF ~2.5% are both above it), so there is no "orphan position" risk under the draft rules as currently written (still DRAFT, unconfirmed by Mark, per Ledger §11).

### Correlated-thesis / factor risk — CAOS INFERENCE
Six of the 8 holdings (PLTR, NVDA, MSFT, GOOGL, IREN, WULF) are direct beneficiaries of, or dependents on, the same underlying macro factor: continued hyperscaler/enterprise AI capital-expenditure growth. This is not 6 independent bets — it is one large factor bet expressed 6 times:
- NVDA sells the GPUs; PLTR sells AI software/analytics; MSFT and GOOGL are the hyperscaler capex spenders *and* cloud-AI revenue beneficiaries; IREN and WULF are the power/datacenter infrastructure suppliers to the same buildout.
- A single shared break condition — a genuine, broad-based AI-capex growth deceleration (not a single company's guidance miss, but a sector-wide reset) — would plausibly hit PLTR, NVDA, MSFT, GOOGL, IREN, and WULF simultaneously, i.e., roughly **~85–90% of holdings value** (CAOS INFERENCE, sum of those six weights: 35.6+29.8+9.0+5.8+2.7+2.5 ≈ 85.4%), not the diversified-sounding "8 different companies" the headline count implies.
- TSLA (Optimus thesis) and KO (staples) are the only two holdings materially outside this factor, at ~5.5% and ~9.0% respectively — together ~14.5% of holdings sit outside the AI-capex factor. This is the portfolio's only real factor diversification today.
- **This is a break-gate-relevant finding, not merely descriptive**: any single-holding break gate below should be read against this backdrop — several gates breaking in the same quarter is not 6 independent low-probability events, it is one high-probability event (a factor shock) appearing in 6 places at once.

### Liquidity risk — DATA LIMITED
All 8 holdings are exchange-listed US equities (NYSE/NASDAQ); no evidence surfaced this run or upstream (Underwriter/Forward/Industry) of trading-halt risk, delisting risk, or abnormal bid-ask/float constraints on any of the 8. Small-cap names (IREN, WULF) carry higher position-liquidation-impact risk than the mega-caps on a pure market-cap/float basis, but no specific float or average-daily-volume figure was surfaced this run to quantify it — DATA LIMITED, not tested further.

### Portfolio drawdown / cash-survival framing — VERIFIED FACT (mandate) / CAOS INFERENCE (implication)
Ledger §1: mandate is maximize CAGR, 40% max drawdown target, 50% hard limit, no leverage, monthly contribution €300 is the only committed forward cash (real current cash is €0.95 — Ledger §3). There is **no cash buffer** to fund a trim, a margin call (leverage is prohibited, so no margin call is structurally possible), or opportunistic buying during a drawdown, beyond the €300/month contribution. Given the ~85% AI-capex factor concentration above, a factor-level drawdown event would very plausibly test the stated 40% target directly, given PLTR and NVDA alone are 65.4% of holdings and both carry meaningfully above-market volatility profiles (not independently re-quantified this run — CAOS INFERENCE from known profile, not fabricated as a new beta figure). Per spec, **drawdown alone is not a sell trigger** — the discipline point is that no defined break gate below is currently close to triggering; this section documents the *capacity* to absorb a drawdown, not a signal to act.

---

## HOLDING 1 — PLTR (Palantir Technologies) — weight ≈35.6%

**Risk categories tested:** Concentration, Factor/Correlated-Thesis, Regulatory (government-customer), Customer concentration.

- **Concentration risk (VERIFIED/CAOS INFERENCE):** Single largest permanent-loss-path amplifier in the portfolio at ~7x the ~5% draft Core/Attacker norm. A non-fatal, ordinary multiple-compression event (e.g., growth deceleration to "only" 40–50% YoY, still an excellent print in absolute terms) could still produce a large portfolio-level drawdown purely because of position size, independent of business health.
- **Customer concentration (DATA LIMITED):** Underwriter flagged U.S. government contract base as a "stated concentration risk not tested by this run" — no government-revenue-mix percentage was surfaced this run or upstream. This is an open data gap, not a resolved risk.
- **Factor risk:** Fully inside the AI-capex/enterprise-AI-adoption factor described above.
- **Regulatory risk (DATA LIMITED):** No specific regulatory threat (antitrust, government-contracting-rule change, export-control exposure to PLTR's software business) was surfaced this run. Not tested further; flagged as an open category given the government-revenue exposure above.

**Survivability confidence: HIGH** (profitable, FCF-positive, no financing/dilution risk surfaced — CAOS INFERENCE from Underwriter's inclusion test). The risk here is **concentration-driven portfolio impact**, not business survivability.

**Proof gate:** Q3 2026 earnings (expected early November 2026, exact date unconfirmed) — revenue lands within/above the guided $2.160B–$2.164B range and U.S. commercial growth continues tracking toward the >134% FY guide.

**Warning gate:** Two consecutive quarters of revenue growth decelerating toward the 50–70% YoY band (still strong, but a clear break from the current ~93% trajectory) without a guided reacceleration path; or a smaller-than-prior guidance raise (deceleration in the rate of positive revisions) at the next two guidance updates.

**Break gate (exact, falsifiable):**
1. Any FY2026 revenue or U.S. commercial guidance **cut** (not merely a smaller raise) issued at or before the Q3 2026 print, OR
2. Two consecutive quarters of revenue growth below 50% YoY with no guided reacceleration path, OR
3. A verified, material loss of U.S. government contract base (a specific contract non-renewal or termination disclosed in an 8-K or earnings call).
Any one of these three triggers a mandatory Portfolio Court sizing review of the position (this agent does not execute a sell; it defines the trigger for one to be considered).

---

## HOLDING 2 — NVDA (NVIDIA Corporation) — weight ≈29.8%

**Risk categories tested:** Concentration, Factor/Correlated-Thesis, Customer concentration, Geographic/regulatory (China), Capital-intensity (input-supply/HBM).

- **Concentration risk:** Second-largest sizing overage, ~6x the ~5% draft norm. Same portfolio-impact logic as PLTR.
- **Customer concentration (CAOS INFERENCE, carried from Industry per Underwriter):** ~half of NVDA's data-center book is non-hyperscaler per Industry (not independently re-verified this run) — a genuine but currently unquantified concentration question on the hyperscaler half.
- **Geographic/regulatory risk (DATA LIMITED):** Underwriter/Industry baseline assumes "no China data-center sales" in current guidance. A verified reversal of China market access (either direction — new access, or a policy tightening elsewhere) would materially change this baseline; not tested further this run beyond noting it.
- **Capital-intensity / input-supply risk (UNVERIFIED LEAD, carried from Industry):** HBM/DRAM shortage is directionally consistent across multiple aggregator sources but magnitude is unverified. For NVDA this is a *demand-side tailwind* (NVDA is the buyer with pricing power in this bottleneck) rather than a threat — but a severe-enough shortage could still compress NVDA's own margin guide if input costs outpace NVDA's ability to pass them through.
- **Factor risk:** Fully inside the AI-capex factor.

**Survivability confidence: HIGH** (high margins, no financing/dilution risk, unmatched revenue scale per Underwriter).

**Proof gate:** Q3 FY2027 earnings (~late November 2026, exact date unconfirmed) — revenue lands within $108.0B ±2% and Data Center segment growth continues near current pace.

**Warning gate:** Q3 FY2027 print lands within guidance but Data Center segment sequential growth rate visibly decelerates versus the prior two quarters' trend, without a guided explanation; or gross margin guide for the following quarter drops below 74.0% ±50bps without a stated one-time cause.

**Break gate (exact, falsifiable):**
1. Q3 FY2027 revenue materially below $108.0B ±2% (i.e., below ~$105.8B), OR
2. A downward revision to the FY28 ~70% growth guide (per Industry §1), OR
3. A verified China-market-access reversal materially changing the "no China data-center sales" baseline, OR
4. Gross margin guide dropping below 74.0% ±50bps for two consecutive quarters, tied to HBM/DRAM cost inflation.
Any one triggers a mandatory Portfolio Court sizing review.

---

## HOLDING 3 — MSFT (Microsoft Corporation) — weight ≈9.0%

**Risk categories tested:** Concentration (mild), Factor/Correlated-Thesis, Capital-intensity (power/grid constraint).

- **Concentration risk:** ~1.8x the ~5% draft norm — a marginal, not severe, overage per Underwriter. Materially lower portfolio-impact risk than PLTR/NVDA.
- **Capital-intensity / execution risk (CAOS INFERENCE, carried from Industry):** ~$80B power-constrained Azure backlog (not re-verified this run) is a capacity-delivery timing risk, not a demand risk — flagged as real but distinct from a permanent-loss path.
- **Factor risk:** Fully inside the AI-capex factor (both as spender and as cloud-AI beneficiary).
- **Accounting-transparency risk (CAOS INFERENCE):** The CY2026 capex figure (~$175B "comparable" vs. an April guide of ~$190B) reflects a useful-life accounting reclassification, per Underwriter explicitly not a straightforward cut. This is not itself a break condition, but it is a data-quality risk worth naming: a future capex disclosure that again uses a reclassification to obscure a genuine spending slowdown would degrade the reliability of capex figures as an early-warning signal for this holding and for GOOGL/NVDA (same open gap flagged by Forward).

**Survivability confidence: HIGH.**

**Proof gate:** Q1 FY2027 earnings (~late October 2026) — revenue lands within $89.85B–$90.95B, quarterly capex exceeds $50B, Azure growth reaches ~45%.

**Warning gate:** Azure growth prints in the 38–44% range (below guide but not collapsing) for one quarter without a credible reacceleration explanation.

**Break gate:**
1. Azure growth materially below the ~45% guide (i.e., below ~38%) for two consecutive quarters with no credible reacceleration path, OR
2. A genuine (non-accounting-driven) capex cut signaling demand-side weakness, OR
3. 2027 capex guidance, when disclosed, coming in flat or down against the 2026 ~$175B comparable base.

---

## HOLDING 4 — KO (The Coca-Cola Company) — weight ≈9.0%

**Risk categories tested:** Concentration (mild), Mandate-fit risk (not a standard risk category but material here), Geographic (multinational FX/consumer exposure — not tested in depth this run).

- **Concentration risk:** ~1.8x the ~5% draft norm, but for the portfolio's lowest-convexity holding — this is a different flavor of risk than PLTR/NVDA's overage: it is capital-efficiency risk (capital tied up not earning its keep against a CAGR-maximization mandate) rather than tail-loss-amplification risk. Per Underwriter, this is the sizing question "most worth Portfolio Court's attention after PLTR/NVDA."
- **Business/permanent-loss risk:** LOW on the evidence available — durable brand, consistent organic growth, dividend-aristocrat-consistent priors (not independently re-verified this run, not fabricated as new). No customer-concentration, financing, dilution, or capital-intensity risk applies materially to KO's business model as evidenced this run.
- **Mandate-fit risk (CAOS INFERENCE):** KO is structurally the weakest fit for a 40%-drawdown-tolerant, CAGR-maximizing mandate among the 8 holdings — not a loss-path risk, but an opportunity-cost risk: capital here is unlikely to be the source of a permanent loss, but is also unlikely to drive CAGR maximization relative to what else could occupy this weight.

**Survivability confidence: HIGH** (of the 8 holdings, the least likely to suffer a permanent-loss event on the evidence available).

**Proof gate:** Q3 2026 earnings (~late October 2026) — organic revenue growth continues tracking toward ~5% FY guide, comparable EPS growth stays within the raised 9%–10% band.

**Warning gate:** Organic revenue growth prints below 4.5% for one quarter without a stated one-time cause.

**Break gate:**
1. Organic revenue growth falling back below the pre-raise 4% floor for two consecutive quarters, OR
2. Comparable EPS growth missing the raised 9%–10% band for two consecutive quarters.
Note per Underwriter: there is no credible "convexity failure" break condition for KO the way there is for a growth name — KO's break gates are business-performance gates, not thesis-collapse gates. The **mandate-fit question is not a break-gate matter**; it is a sizing/replacement question that belongs to Portfolio Court, not a risk-of-loss finding.

---

## HOLDING 5 — GOOGL (Alphabet Inc., Class A) — weight ≈5.8%

**Risk categories tested:** Concentration (minimal), Factor/Correlated-Thesis, Capital-intensity, Market-perception/funding-credibility risk.

- **Concentration risk:** Only marginally over the ~5% draft norm — the best-sized of the AI-capex-factor holdings.
- **Factor risk:** Fully inside the AI-capex factor (cloud-AI beneficiary and capex spender, same structural profile as MSFT).
- **Market-perception risk (DATA LIMITED):** Market reportedly reacted negatively to the FY2026 capex raise (Forward, per Underwriter) — flagged as a live catalyst/risk but not yet evidenced as more than a stock-reaction story (no funding/ROI-credibility data surfaced this run).

**Survivability confidence: HIGH.**

**Proof gate:** Q3 2026 earnings (~late October 2026) — Cloud revenue growth holds near 82% YoY, $195B–$205B FY2026 capex range reaffirmed or breached, 2027 capex figure possibly disclosed.

**Warning gate:** Cloud revenue growth decelerates to the 65–80% YoY range for one quarter without a stated explanation.

**Break gate:**
1. Cloud revenue growth decelerating materially below 65% YoY with no credible explanation, OR
2. A disclosed 2027 capex figure implying a genuine slowdown (not merely a pause in the raise cadence), OR
3. Continued negative market reaction to capex raises compounding into a demonstrated (not merely sentiment-based) funding/ROI-credibility problem — e.g., a credit-rating or borrowing-cost impact tied explicitly to capex spending.

---

## HOLDING 6 — TSLA (Tesla, Inc.) — weight ≈5.5%

**Risk categories tested:** Concentration (minimal), Thesis-verification risk (Optimus), Capital-intensity, Customer/demand-cyclicality.

- **Concentration risk:** Close to the ~5% draft norm — not a material sizing concern on a pure weight basis.
- **Thesis-verification risk (CAOS INFERENCE / UNVERIFIED LEAD, per Underwriter):** This is TSLA's dominant risk this cycle, more than any conventional category. The position's stated convexity case rests substantially on Optimus humanoid-robot production, and **no independent confirmation was found this run that Optimus production began on schedule** (guided late-July/August 2026 at Fremont). Per Burden of Proof, this cannot be assumed to have happened; the raw-convexity regime is correctly rated UNKNOWN, not 10x-credible, until verified.
- **Capital-intensity risk (CAOS INFERENCE):** FY2026 capex guide >$25B with "further increases in H2 2026" tied partly to the Optimus buildout — a funding-strain risk specifically on the unverified part of the thesis.
- **Customer/demand-cyclicality (VERIFIED FACT, positive this run):** Q2 2026 deliveries +25% YoY, first YoY growth after two years of decline — reduces near-term demand risk on the core auto business, though this is only one quarter of data after a two-year decline and should not yet be treated as a fully re-established trend.

**Survivability confidence: MODERATE** — not because the core auto business is at risk (profitability status not independently re-verified this run — DATA LIMITED), but because a meaningful share of the position's expected return depends on an unverified claim, which this agent must discount per Burden of Proof regardless of how the stock might trade in the interim.

**Proof gate (two, per Underwriter):**
1. Tesla's Q3 2026 delivery report (~early October 2026) — YoY delivery growth continues.
2. **Direct confirmation of whether Optimus production actually began at Fremont in the guided late-July/August 2026 window** — the more consequential, currently-unverified proof point.

**Warning gate:** Optimus production status remains unconfirmed (neither positive nor negative evidence surfaces) through the Q3 2026 delivery report date without a company-issued update; or delivery growth decelerates to low-single-digit YoY (still positive, but a clear deceleration from the Q2 +25% print).

**Break gate:**
1. Confirmation that Optimus production did **not** begin in the guided window, with no credible near-term rescheduled date, OR
2. Delivery growth reversing back to YoY decline after the Q2 rebound, OR
3. FY2026 capex guide (>$25B, "further increases in H2 2026") not materializing, suggesting funding strain on the Optimus buildout specifically.
Note: given the thesis-verification gap, this agent flags that **the Optimus-verification proof gate deserves priority resolution before the next Deep Audit cycle** — it is the single most consequential open question across all 8 holdings' risk maps.

---

## HOLDING 7 — IREN (IREN Limited) — weight ≈2.7%

**Risk categories tested:** Financing/refinancing, Customer concentration, Capital intensity, Correlated-thesis (AI-capex factor, infrastructure-supply side), Concentration (position-level, below norm).

- **Financing risk (CAOS INFERENCE, directly computed by Underwriter from disclosed figures — this is the dominant risk for this holding):** FY2027 capex guidance is $25B–$30B; disclosed funding sources total ~$14B (cash + committed GPU financing) — **a funding gap of roughly $11B–$16B not yet closed by named sources**. This is the single largest unresolved risk in the IREN risk map and is consistent with, not a new escalation of, the already-open evidence gate.
- **Customer concentration (CAOS INFERENCE, per Underwriter, secondary-source not independently primary-verified):** >$4B ARR contracted for FY2026 AI Cloud capacity, with Microsoft reported as a major counterparty (via secondary earnings-call reporting) — but only **~18% of trailing FY26 revenue is AI Cloud; ~82% is still legacy bitcoin mining**, meaning the AI-thesis customer-concentration risk is currently smaller in dollar terms than the headline contract figures suggest.
- **Debt/credit risk (VERIFIED FACT per Industry, confirmed this run):** $3.0B convertible-notes offering (1.00% senior notes due 2033, Rule 144A, net proceeds ~$2.96B) is confirmed. **No source ties Microsoft specifically to this notes offering** — the "investment-grade Microsoft-backed facility" framing in the prior evidence gate appears to actually reference a separate ~$9.7B Microsoft/GB300 deal at Childress, TX, whose credit terms remain unconfirmed (UNVERIFIED LEAD, unresolved).
- **Capital intensity:** Extreme — this is a capex-heavy infrastructure buildout business, and the financing-gap finding above is a direct consequence of that intensity.
- **Factor risk:** Inside the AI-capex factor, on the infrastructure-supply side (correlated with, not independent of, NVDA/MSFT/GOOGL capex trends).
- **Concentration risk (position-level):** At ~2.7%, below the ~5% Core/Attacker norm but above the ~1.5% Seed floor — not a sizing violation under current draft rules, though the risk profile (financing gap, thin AI-revenue mix) may fit a Seed/Catalyst role better than an unconditional Core/Attacker label (Underwriter's finding, reconfirmed here from a risk-mapping angle: an explicit evidence gate matched to role would itself be a risk-mitigation improvement, but role reassignment is Portfolio Court's job, not this agent's).

**Survivability confidence: LOW-MODERATE** — real, growing AI Cloud contract book, but a large unclosed financing gap on a capital-intensive buildout is, per Survivability Before Optionality, exactly the kind of risk that should dominate the assessment regardless of how attractive the underlying contract book looks.

**Proof gate:** IREN's Q1 FY2027 earnings release (~November 2026) — whether the FY2027 "late-stage discussions" convert into a named, dollar-denominated contracted-capacity announcement, and whether the $25B–$30B FY2027 capex guide gets a named financing source closing the ~$11B–$16B gap.

**Warning gate:** Q1 FY2027 report discloses partial financing progress (e.g., closes less than half the gap) without a credible path to closing the remainder before capex outlays are due.

**Break gate:**
1. No named financing source closing the FY2027 capex gap by the Q1 FY2027 report, OR
2. AI Cloud revenue mix failing to grow materially beyond the current ~18% of trailing revenue by the same checkpoint, OR
3. Any credit-quality deterioration or downgrade signal on the $3.0B convertible notes or the separate Microsoft GB300 facility, OR
4. Confirmation that the Microsoft-backed-facility framing cannot be substantiated at all.

---

## HOLDING 8 — WULF (TeraWulf Inc.) — weight ≈2.5%

**Risk categories tested:** Customer/counterparty concentration (single-counterparty), Financing/leverage, Maturity/refinancing, Capital intensity, Correlated-thesis (AI-capex factor, infrastructure-supply side), Concentration (position-level, below norm).

- **Customer/counterparty concentration risk (this is WULF's dominant, defining risk):** The Anthropic lease (20-year, 401MW, ~$19B contracted revenue over the initial term, up to ~$33B with extensions) represents the company's largest single contract, and **Anthropic's own credit standing cannot be independently verified** — Anthropic is confirmed private with no S&P/Moody's rating found (VERIFIED FACT — absence of finding). Secondary coverage characterizing the lease as "underpinned by Anthropic's strong investment-grade credit rating" is flagged by Industry as specifically suspect, since no source identifies who rated Anthropic or on what basis. A separate, unrelated Anthropic financing structure (the ~$35–36B TPU SPV) does achieve investment-grade quality, but via **Broadcom's third-party residual-value guarantee**, not Anthropic's own credit — this cannot be assumed to extend to the TeraWulf lease without direct evidence, which this run does not have (blocked by network egress restrictions on the two primary documents that would resolve it: TeraWulf's press release and its SEC 8-K exhibit).
- **Leverage/maturity-refinancing risk (EVIDENCE_QUALITY = MEDIUM, per existing evidence gate):** ~$5.8B total debt (~63% of a naive debt+equity cap), including $2.5B convertible notes with refinancing/conversion risk **ahead of** the H2 2027 revenue start. This stacks directly on top of the unresolved counterparty-credit question: high leverage plus an unverified largest-counterparty credit rating plus a ~14-month gap before the flagship contract's revenue begins is precisely the combination Survivability Before Optionality is designed to catch.
- **Capital intensity:** High, same infrastructure-buildout profile as IREN.
- **Factor risk:** Inside the AI-capex factor, infrastructure-supply side, single-counterparty-concentrated within that factor (Anthropic specifically, versus IREN's more diversified-but-thinner AI customer base).
- **Concentration risk (position-level):** At ~2.5%, the smallest position in the portfolio — below the ~5% Core/Attacker norm, above the ~1.5% Seed floor. Given the risk findings above, the current small size functions as risk mitigation already in place, even though the inherited role label ("Core/Attacker") does not formally reflect that. Role reassignment is Portfolio Court's job.

**Survivability confidence: LOW** — this is the lowest-survivability-confidence holding in the portfolio on the current evidence. Not because a negative finding has been confirmed (the evidence gate remains open, not resolved negative), but because the single largest number driving the thesis (~$19B) rests on an unverified counterparty-credit claim, layered on already-high leverage, with revenue not starting for ~14+ months. Per Burden of Proof, "investment-grade" cannot be assumed absent a source; per Survivability Before Optionality, this combination discounts adjusted attractiveness heavily regardless of the raw contract-value convexity.

**Proof gate:** CB-4's phased delivery and rent commencement (guided H2 2026) — the nearest-dated, most falsifiable checkpoint of any item across all 8 holdings — followed by CB-5 ("early 2027") and the late-2027 Anthropic-lease revenue start. TeraWulf's Q3 2026 earnings release (~November 2026) is the next scheduled checkpoint for CB-4 progress. **Separately and more urgently:** the next agent/session with SEC.gov and terawulf.com egress access should retry the two blocked primary documents (TeraWulf press release + 8-K exhibit) to resolve the Anthropic-credit question directly — this is the single highest-value open task across the entire portfolio's risk map.

**Warning gate:** CB-4 delivery slips within H2 2026 but a credible revised date is given (not yet a break); or the blocked primary documents, once read, confirm the lease exists as characterized but do not resolve the credit-rating mechanism either way (evidence gate stays open, not negative).

**Break gate:**
1. Confirmation (once the blocked documents are readable, or via any other primary source) that the Anthropic lease's "investment-grade" characterization has **no** valid guarantor or structural credit enhancement behind it — i.e., it rests on Anthropic's own unrated credit alone, OR
2. Any signal of stress in Anthropic's own compute-spending pace relative to its disclosed revenue base (Industry flags ~$130B+ in aggregate commitments against a revenue base not yet demonstrated to sustainably cover that pace) — monitorable, not yet a proven risk, OR
3. CB-4 delivery/rent commencement slipping past H2 2026 without a credible revised date, OR
4. Any covenant or refinancing stress signal on the $2.5B convertible notes ahead of the 2027 revenue start, OR
5. A public S-1/IPO process for Anthropic revealing financials materially weaker than the reported ~$65B ARR trajectory (itself UNVERIFIED LEAD).

---

## Cross-Holding Risk Summary

| Ticker | Weight | Dominant Risk Category | Survivability Confidence | Nearest Break-Gate Checkpoint |
|---|---|---|---|---|
| PLTR | ~35.6% | Concentration (portfolio-impact) | HIGH | Q3 2026 earnings (~early Nov 2026) |
| NVDA | ~29.8% | Concentration (portfolio-impact) | HIGH | Q3 FY2027 earnings (~late Nov 2026) |
| MSFT | ~9.0% | Capital-intensity (power/grid) | HIGH | Q1 FY2027 earnings (~late Oct 2026) |
| KO | ~9.0% | Mandate-fit (not a loss-path risk) | HIGH | Q3 2026 earnings (~late Oct 2026) |
| GOOGL | ~5.8% | Market-perception/funding-credibility | HIGH | Q3 2026 earnings (~late Oct 2026) |
| TSLA | ~5.5% | Thesis-verification (Optimus, unresolved) | MODERATE | Q3 2026 deliveries (~early Oct 2026) + Optimus confirmation (open, no date) |
| IREN | ~2.7% | Financing gap (~$11B–$16B unclosed) | LOW-MODERATE | Q1 FY2027 earnings (~Nov 2026) |
| WULF | ~2.5% | Counterparty-credit concentration (Anthropic, unresolved) + leverage | LOW | CB-4 delivery (H2 2026) + document-access retry (no date) |

**Portfolio-level dominant risk (not attributable to any one holding):** the ~65.4% PLTR+NVDA concentration and the ~85% AI-capex factor concentration across 6 of 8 holdings, both described in the Portfolio-Level Risk Map above. No single holding's break gate captures this — it is a structural finding for Portfolio Court, reconfirmed independently by this agent from a pure risk-mapping angle (not new, but re-derived rather than merely cited).

## What This Run Explicitly Does Not Do
- Does not fabricate a 0–100 survivability score — no such baseline exists anywhere upstream this cycle; qualitative HIGH/MODERATE/LOW confidence ratings are used instead, consistent with Weekly Ranking and Daily Anchor's handling of the same gap.
- Does not adjudicate the open `20260902-DAILY-PORTFOLIO-COUNT_OVERAGE` Tribunal or the `20260902-DAILY-WULF_IREN-EVIDENCE_GATE` — both are reconfirmed/re-derived here from a risk perspective, decisions remain Portfolio Court/Orchestrator's.
- Does not reassign role labels (Core/Attacker vs. Seed/Catalyst) for IREN/WULF — flagged as a risk-mitigation-relevant mismatch, decision remains Portfolio Court's.
- Does not recommend any sell, trim, or buy action — only defines proof/warning/break gates per spec. Drawdown alone is not treated as a sell or hold reason anywhere in this file.
- Does not write to the Master Ledger.

---

## Verdict

`RISK REVIEW = COMPLETE`
