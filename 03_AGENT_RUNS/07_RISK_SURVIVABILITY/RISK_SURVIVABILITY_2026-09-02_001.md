# RISK & SURVIVABILITY REVIEW — 2026-09-02_001

## Inputs Consulted
- [[03_AGENT_RUNS/07_RISK_SURVIVABILITY/_AGENT SPEC — Risk and Survivability]] — role spec followed for this run
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-02_001]] — Monster Files on IREN, WULF, ONDS, OKLO, ABSI; NVDA light-touch check; source of counterparty, financing, dilution, and cash-runway figures used below
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — current 8 funded-position sizes/cost basis (§2), cash position (§2–3), mandate/drawdown limits (§1), draft sizing rules (§11)
- No independent research access this run (per spec, this agent works from the Underwriter's output and the Ledger only — it does not re-verify primary filings). All figures below are inherited from the Underwriter's evidence labels unless marked otherwise; this agent adds no new VERIFIED FACTs, only risk analysis, portfolio-math, and gate design built on top of what the Underwriter already labeled.

**Scope discipline:** This report does not resize or rank positions, does not recommend trades, and writes nothing to the Master Ledger. It tests loss paths and proposes gates only.

---

## Part A — Portfolio-Level Risk (all 8 funded holdings)

### A1. Position sizing (from Ledger §2, current-price mark, 2026-09-02 snapshot)

| Ticker | Value (shares × price, USD) | % of 8-holding total |
|---|---|---|
| PLTR | ~$3,851 | ~35.6% |
| NVDA | ~$3,228 | ~29.8% |
| KO | ~$975 | ~9.0% |
| MSFT | ~$975 | ~9.0% |
| GOOGL | ~$625 | ~5.8% |
| TSLA | ~$597 | ~5.5% |
| IREN | ~$292 | ~2.7% |
| WULF | ~$274 | ~2.5% |
| **Total** | **~$10,817** | **100%** |

CAOS INFERENCE: arithmetic on Ledger's own share counts and current prices; not independently re-verified against a fresh broker pull this run. The implied EUR/USD cross needed to reconcile this USD total against the Ledger's stated €9,333.67 account total is not confirmed this run — DATA LIMITED, flag for the next Ledger refresh rather than a risk finding.

**Concentration finding:** PLTR + NVDA alone are ~65% of the funded book. This is a single-factor concentration (AI-capex/AI-software beta) before WULF/IREN are even added — not a diversified eight-name portfolio in risk terms, whatever the ticker count suggests. Per Ledger §11 draft rule (Core/Attacker positions "should normally have a credible path toward approximately 5% of NAV"), PLTR and NVDA are already multiples over that target on a mark-to-market basis, while IREN and WULF sit *under* the ~5% target — the portfolio's realized risk budget is currently concentrated in the two largest names, not the two most-discussed thesis-shift names.

### A2. Correlated-thesis / factor risk — the cross-cutting finding this run adds

The Underwriter's Monster Files, read together with the other 6 funded holdings, expose a structural correlation the position-count alone hides:
- **NVDA, PLTR, MSFT, GOOGL, IREN, and WULF are all, to varying degrees, levered to the same AI-capex supercycle factor.** A hyperscaler capex slowdown, a GPU-supply/memory shock (Industry's NVIDIA Gate already flags a live memory-constraint issue at NVDA), or a broad AI-infrastructure multiple compression would not diversify away inside this portfolio — it would hit 6 of 8 names simultaneously. Only KO (consumer staples) and, to a lesser extent, TSLA (EV/auto, though TSLA also carries its own AI/robotics narrative premium) sit meaningfully outside this factor.
- **MSFT and GOOGL are structurally dual-role in this book**: they are funded holdings *and* the credit anchors underwriting the risk quality of two other funded holdings (MSFT via the IG-rated Microsoft contract that is IREN's central de-risking argument; GOOGL via the $3.2B backstop and 14% equity stake that de-risks WULF's Fluidstack leases). This is not diversification — it is the same hyperscaler-capex bet expressed four different ways (direct MSFT/GOOGL equity, NVDA as the arms dealer, IREN/WULF as the landlords). A shock to hyperscaler AI capex plans is a single point of failure touching the majority of this portfolio's dollar value, not an isolated single-name event.
- **CAOS INFERENCE:** this concentration is not itself a break-gate condition (per spec, drawdown/factor exposure alone is not a sell signal) but it should inform how the next Deep Audit treats "diversification" claims about this book, and it raises the bar for what a WULF or IREN break gate should require — because if either fires, it is unlikely to fire in isolation from the rest of the AI-capex-exposed sleeve.

### A3. Portfolio-level liquidity / cash-survival

- Real unlevered cash: **€0.95** (Ledger §3, VERIFIED per Ledger's own event log). No margin, no credit line, no leverage (mandate prohibits leverage — Ledger §1).
- Only source of fresh deployable capital is the **€300/month** contribution (Ledger §1).
- **Survivability implication:** the portfolio itself has effectively zero dry powder. It cannot average down, backstop a position through a liquidity event, or opportunistically add to a name that gaps down on a break-gate-adjacent scare, except via the next month's €300 contribution. This does not threaten solvency (all positions are unlevered long equity — there is no margin call, no forced-liquidation mechanism, no derivative exposure per Ledger §1), so drawdown, however large, cannot force a sale. But it does mean **the portfolio's only real lever in a stress scenario is patience and the monthly contribution**, not tactical cash deployment. This is a structural fact to hold in mind when setting warning gates below — a warning gate should be actionable without assuming spare cash exists to act on it with.
- No leverage anywhere in the book (Ledger §1: "Leverage/Derivatives: NO") — this removes margin-call and forced-deleveraging as a permanent-loss path for the *portfolio* itself, even though several *underlying companies* (WULF in particular) carry heavy balance-sheet leverage that could theoretically zero the equity while doing the investor no additional portfolio-mechanical harm beyond the position's own loss.

---

## Part B — Risk Map Per Candidate

### B1. IREN (funded holding — extra depth per this run's brief)

| Category | Assessment |
|---|---|
| Concentration | ~2.7% of funded book (Part A). Sub-target on Ledger §11's ~5% norm — position-sizing risk is currently *low*, not high, despite being the more research-intensive name. |
| Liquidity | Company-level: ~$14B starting cash + committed GPU financing (VERIFIED per Underwriter) — no near-term company liquidity crunch identified. |
| Financing | $3.65B facility secured (IG-rated, A/A-low), but **~$8B of FY27 capex ($25B–$30B guided) remains unfinanced and is a management aspiration, not a signed facility** (Underwriter, MANAGEMENT ASPIRATION label). This is the single largest open financing risk on IREN. |
| Dilution | $2.1B of the $3.65B facility was a private placement; pricing/terms not independently confirmed (DATA LIMITED per Underwriter). Company/lender framing says the structure avoids heavy dilution, but this is one financing round, not a durable guarantee against dilution if the ~$8B gap is closed equity-heavy. |
| Customer concentration | Microsoft is effectively IREN's flagship AI-Cloud counterparty (>$4B contracted ARR figure cited). Single-hyperscaler concentration risk exists even though the counterparty itself is IG-rated — a Microsoft-side capex pullback or contract renegotiation would hit IREN disproportionately versus a multi-customer book. |
| Capital intensity | Extremely high — data-center/GPU buildout at hyperscaler capex scale ($25–30B FY27 guide against a ~$13–14.5B market cap). This is the core survivability variable for the name. |
| Maturity/refinancing | $3.65B facility terms (delayed-draw term loan + private placement) — maturity schedule not detailed in Underwriter's pass; flag as DATA LIMITED for the next cycle. |
| Regulatory | Data-center/power-siting and (for the bitcoin-mining legacy book, still 82% of FY26 trailing revenue) energy-policy/crypto-mining regulatory exposure in the jurisdictions IREN operates. Not independently assessed this run — UNKNOWN. |
| Geographic | Not detailed in Underwriter's pass this run — UNKNOWN (IREN's facilities are understood to be multi-jurisdiction from prior CAOS context, but not re-verified this run). |
| Factor | AI-capex / hyperscaler-capex factor, and residually bitcoin-price factor while 82% of trailing revenue is still mining — a live dual-factor exposure, not a clean single-thesis name yet. |
| Correlated-thesis | See Part A2 — correlated with NVDA (GPU supply), MSFT (direct counterparty), and WULF (same sector pivot, same NVIDIA-gate exposure). |

**Realistic permanent-loss paths for IREN:**
1. The ~$8B unfinanced FY27 capex gap closes only via distressed-price equity issuance or high-cost debt, permanently impairing per-share economics even if the underlying AI-Cloud business succeeds operationally.
2. Bitcoin-mining revenue (still 82% of FY26 trailing revenue) collapses on a bitcoin-price shock faster than AI-Cloud scales, creating a revenue/cash-flow air-pocket that forces distress financing before Horizon tranches ramp.
3. Microsoft, despite being IG-rated, materially slows or renegotiates a subsequent Horizon tranche (capex discipline at the hyperscaler level) — this would not be a credit-quality failure but a demand/scheduling failure, and IREN's model is a single-customer-scheduling-dependent story regardless of Microsoft's own solvency.

### B2. WULF (funded holding — extra depth per this run's brief; the most consequential name this run)

| Category | Assessment |
|---|---|
| Concentration | ~2.5% of funded book — smallest dollar position among the 8, but carries the single largest *contract* headline figure ($19B) of any name in the book, and the heaviest balance-sheet leverage. Position-sizing risk is low; company-level financial-structure risk is the highest in the book. |
| Liquidity | Not separately quantified beyond debt figures in Underwriter's pass; cash runway against debt-service obligations through the 2027 ramp gap is a named open item — DATA LIMITED. |
| Financing | $5.8B total debt (VERIFIED, 10-Q): $2.5B corporate convertible notes, $3.2B WULF Compute LLC senior secured notes, $100M Kentucky bridge loans. Debt-to-market-cap (~63% of a naive debt+equity capitalization, per Underwriter's own arithmetic) is materially higher leverage than IREN's. |
| Dilution | $2.5B convertible notes at the corporate level are a **standing dilution overhang** if conversion triggers are hit — conversion terms/strike not independently confirmed (DATA LIMITED). |
| **Customer concentration — the decisive risk category for WULF** | The $19B, 20-year Anthropic lease is WULF's largest single contract by dollar value. Anthropic is **privately held, unrated, itself financing via ~$50B in fresh debt ahead of an unconfirmed IPO (draft S-1 filed, timing spanning Q4 2026–Q1 2027)**, and the lease generates **no revenue until H2 2027** (initial capacity) with full ramp not until early 2028. This is a single-counterparty concentration on an unrated, pre-IPO credit, materially weaker in credit-quality terms than IREN's Microsoft exposure, and the revenue is 12–18 months out from this run's date. By contrast, the Fluidstack/Google-backstopped side ($3.2B Google backstop, 14% Google equity stake) is a meaningfully stronger counterparty structure — the risk is concentrated specifically in the Anthropic lease, not WULF's whole customer book. |
| Capital intensity | Very high, comparable to IREN — data-center buildout at hyperscaler-adjacent scale funded on a materially thinner equity cushion (32% equity / 68% debt project-level capitalization, per Underwriter). |
| Maturity/refinancing | $2.5B convertible notes and $3.2B senior secured notes both carry refinancing/conversion risk against a revenue stream (Anthropic lease) that does not begin until H2 2027 — a maturity/revenue-timing mismatch is the core structural risk. Exact maturity dates not detailed in Underwriter's pass — DATA LIMITED. |
| Regulatory | Not independently assessed this run — UNKNOWN. |
| Geographic | Lake Mariner / Justified Data Campus / Kentucky subsidiaries implied by the debt structure (VERIFIED as entity names per 10-Q) — full geographic concentration profile not assessed this run. |
| Factor | Same AI-capex/GPU-demand factor as IREN, plus incremental **private-AI-lab financing-market factor risk** specific to Anthropic's own capital-markets access — a factor exposure IREN does not share (Microsoft does not need capital-markets access to honor its contract; Anthropic's ability to fund its side of the buildout is itself capital-markets-dependent). |
| Correlated-thesis | See Part A2. Additionally: WULF's Anthropic-side thesis is correlated with the broader "AI-lab-financing-boom continues uninterrupted" macro bet — a bet this portfolio does not otherwise hold directly (no OpenAI/Anthropic-adjacent private exposure elsewhere in the book), making WULF the portfolio's single point of exposure to that specific factor. |

**Realistic permanent-loss paths for WULF (ranked by directness):**
1. **Anthropic-financing failure path:** Anthropic's IPO stalls or its financing conditions deteriorate materially before H2 2027 (e.g., a down round, a credit-market pullback on AI-lab debt, or IPO withdrawal) → Anthropic cannot fund its side of the Justified Data Campus buildout or defaults/renegotiates the lease down → the $19B headline figure is impaired or never materializes → WULF's $5.8B debt load (priced and raised partly against this future revenue story) becomes harder to service or refinance → forced dilutive equity raise or distressed refinancing at materially worse terms → permanent per-share value destruction even if WULF's own operations (Fluidstack side) are fine.
2. **Refinancing-gap path:** the $2.5B convertible notes or $3.2B senior secured notes mature or face refinancing pressure before the Anthropic lease begins generating recognized revenue (H2 2027) → refinanced at high-cost terms or via conversion-triggered dilution → permanent impairment independent of whether Anthropic itself ever defaults.
3. **Air-pocket path (shared with IREN):** legacy bitcoin-mining revenue declines faster than HPC lease revenue scales, on a balance sheet with materially less cushion than IREN's, reproducing IREN's air-pocket risk with less room to absorb it.
4. **Google backstop path (lower probability, still real):** Google reduces or exits its 14%/$3.2B backstop commitment to the Fluidstack side — would not directly touch the Anthropic lease but would remove the one clearly investment-grade-quality credit support in WULF's book, re-concentrating all of WULF's counterparty risk in unrated private counterparties.

### B3. NVDA (funded holding — light-touch, per Underwriter's own light-touch pass)

| Category | Assessment |
|---|---|
| Concentration | ~29.8% of funded book — the single largest factor exposure in the portfolio alongside PLTR. |
| Financing/Liquidity | Mega-cap, not a survivability concern in the sense this spec is built for. |
| Customer concentration | Broad hyperscaler customer base — the opposite of WULF/IREN's single-counterparty risk, but that customer base overlaps materially with this portfolio's own AI-capex names (MSFT, GOOGL, indirectly IREN/WULF as GPU buyers), reinforcing Part A2's factor point. |
| Capital intensity | N/A — supplier, not buildout operator. |
| Regulatory | Export-control/geopolitical risk on advanced-chip sales (China, general knowledge, not re-verified this run) — CAOS INFERENCE, not independently confirmed this pass. |
| Factor | AI-capex factor, concentrated specifically in the memory/CoWoS supply-chain constraint Industry's Gate and this run's Underwriter check both flagged: NVIDIA is **cutting its own product specs** (reduced HBM/SOCAMM configuration on Vera Rubin/Rubin Ultra) to fit memory allocation — a live competitive/execution risk, not yet a break condition. |
| Correlated-thesis | Central node of Part A2's factor concentration — NVDA's GPU-supply health is a direct input to IREN's and WULF's ability to deliver contracted capacity on schedule. |

**Realistic permanent-loss path:** not identified this run at the "permanent loss" bar — NVDA's risks surfaced (memory constraint, competitive spec-cutting) are margin/growth-rate risks, not solvency or existential risks, per both Industry's and Underwriter's framing. No break gate proposed beyond the monitoring items below.

### B4. PLTR, MSFT, KO, GOOGL, TSLA (funded holdings — not covered by this run's Underwriter pass)

These five names were not re-underwritten this run (Underwriter's scope was IREN/WULF thesis-shift plus three fresh candidates). Per Burden of Proof, this agent does not fabricate fresh figures for them. What can be said from the Ledger and cross-cutting structure alone:

| Ticker | Concentration (Part A1) | Factor/correlated-thesis note | Other categories |
|---|---|---|---|
| PLTR | ~35.6% — largest single position in the book | AI-software factor, correlated with NVDA/IREN/WULF's AI-capex thesis; separately carries US-government-contract customer-concentration risk (CAOS INFERENCE from general market knowledge, not verified this run) | Liquidity/financing/dilution/regulatory/geographic: UNKNOWN this run — DATA LIMITED, recommend next Underwriter pass include PLTR given its outsized portfolio weight |
| MSFT | ~9.0% | Dual role — see A2; also IREN's counterparty | As above, UNKNOWN this run |
| KO | ~9.0% | The one clearly non-AI-factor holding in the book — genuine diversification value | As above, UNKNOWN this run |
| GOOGL | ~5.8% | Dual role — see A2; also WULF's Fluidstack backstop provider | As above, UNKNOWN this run |
| TSLA | ~5.5% | Partially outside the AI-capex factor (EV/auto core), but carries its own execution/key-person and China-regulatory exposure (CAOS INFERENCE, not verified this run) | As above, UNKNOWN this run |

**No permanent-loss paths asserted for these five this run** — absence of fresh evidence is not evidence of safety, but this agent will not invent risk findings without input data. Flagged for the next Deep Audit / Underwriter cycle, particularly PLTR given it is over one-third of the funded book.

### B5. ONDS (candidate)

| Category | Assessment |
|---|---|
| Concentration | N/A — not yet a funded position. |
| Liquidity | $1.4B cash as of 2026-06-30 (VERIFIED), reduced by ~$325M already deployed for DZYNE/Cyber Hawk acquisitions in Q3 2026 — real but shrinking cushion. |
| Financing/Dilution | Cash pile is ~44% of market cap, raising the question of how much was raised via dilutive equity vs. organic generation — **not resolved by the Underwriter this run (DATA LIMITED)**; a "$217M stock offering" headline was surfaced but not traced to specific terms. |
| Customer concentration | Army IDIQ ceiling is $982M but only ~$240M (~24%) has actually converted to awarded task orders (VERIFIED, corrects Discovery's framing) — single-customer (US Army) concentration with substantial award-conversion uncertainty. |
| Capital intensity | Not flagged as capital-intensive in Underwriter's pass (drone/defense-tech hardware, but no capex figures surfaced). |
| Maturity/refinancing | Not applicable — no debt load surfaced this run. |
| Regulatory | Defense-contracting/procurement regulatory exposure inherent to Army IDIQ structure — UNKNOWN specifics this run. |
| Geographic | Not detailed this run — UNKNOWN. |
| Factor | Defense-tech/drone factor, distinct from the portfolio's existing AI-capex factor — genuine diversification value *if* added. |
| Correlated-thesis | Low correlation with existing 8 holdings' AI-capex factor — a portfolio-construction positive if this candidate is ever funded. |

**Realistic permanent-loss path:** IDIQ ceiling-to-award conversion stalls well below the pace implied by the last two quarters while FY26 guidance ($525–550M) is walked back, forcing the company to burn down its cash cushion (already reduced by the DZYNE/Cyber Hawk spend) without a clear revenue-visibility offset, ultimately forcing a dilutive raise at a depressed valuation.

### B6. OKLO (candidate)

| Category | Assessment |
|---|---|
| Liquidity | $3.0B cash by Q2 2026 (VERIFIED), funds several years of guided burn ($120–150M opex, $400–500M capex) — genuinely strong near-term survivability. |
| Financing/Dilution | **Heavy, ongoing, already-realized dilution**: weighted-average shares +15.3% in six months (173.3M → 186.0M), funded almost entirely by $1.9B in 2026 ATM raises (VERIFIED, 10-Q). This is the decisive risk category for OKLO. |
| Customer concentration | Zero commercial revenue (VERIFIED) — no customer-concentration risk yet because there are no paying customers; the risk is the *absence* of revenue, not its concentration. |
| Capital intensity | Very high relative to current zero-revenue state ($400–500M capex guide against a pre-revenue balance sheet). |
| Maturity/refinancing | No debt load surfaced — dilution, not debt, is the financing mechanism, which removes refinancing/covenant risk but does not remove per-share value erosion risk. |
| Regulatory | NRC licensing risk specific to Oklo's SMR design — flagged directly in Underwriter's kill conditions. |
| Geographic | Not detailed this run — UNKNOWN. |
| Factor | Nuclear/SMR-policy and AI-datacenter-power-demand factor — partially correlated with the portfolio's AI-capex exposure (SMR demand is downstream of data-center power needs) but on a much longer multi-year timeline (targets from 2029). |
| Correlated-thesis | Loosely correlated with IREN/WULF's power-demand thesis but on a sufficiently different time horizon (pre-2029 vs. near-term) that it does not compound near-term AI-capex-factor risk. |

**Realistic permanent-loss path:** continued ATM-funded dilution at the current pace compounds for multiple more years before any Aurora powerhouse reaches revenue (2029+ target), progressively destroying per-share economics even though the company itself does not run out of cash — a "die of a thousand dilutive cuts" path rather than a bankruptcy path. Separately, any NRC licensing setback specific to Oklo's design would be a more abrupt, binary permanent-loss trigger.

### B7. ABSI (candidate)

| Category | Assessment |
|---|---|
| Liquidity | $201.1M cash (VERIFIED), runway guided into H2 2028 — solid near-term survivability. |
| Financing/Dilution | Shares outstanding +31% in the past year (VERIFIED) — substantial, already-realized dilution funding a business with *declining* partner revenue. |
| Customer concentration | Partner-program revenue is declining ($0.3M Q2 2026 vs. $0.6M Q2 2025) and concentrated around a small number of pharma relationships, headlined by the $40M Eli Lilly investment — a single-partner-dependent credibility signal, not a diversified customer base. |
| Capital intensity | Clinical-stage biotech capital intensity (trial costs), not capex/infrastructure — different capital-intensity profile than the AI-infra names in this book. |
| Maturity/refinancing | No debt load surfaced. |
| Regulatory | FDA/clinical-trial regulatory pathway risk for ABS-201 — inherent to the asset class, not separately quantified this run. |
| Geographic | Not detailed this run — UNKNOWN. |
| Factor | Biotech/clinical-catalyst factor — genuinely uncorrelated with the portfolio's AI-capex factor, a real diversification candidate if funded. |
| Correlated-thesis | Independent of the AI-capex correlated-thesis cluster in Part A2 — lowest correlation of the three candidates with the existing book. |

**Realistic permanent-loss path:** ABS-201 Phase 1 reads out negative or ambiguous while partner revenue continues its declining trend and no new partnership materializes — the "AI drug discovery platform" narrative collapses to a single failed clinical asset with a shrinking, dilution-funded cash pile and no offsetting revenue story, at which point further dilutive raises would fund a thesis the trailing financials no longer support.

---

## Part C — Proof / Warning / Break Gates

Per spec: exact metric/date/event, not vague language. "Break gate" = a defined, falsifiable trigger that (per Ledger §11 and this spec's constraints) is the *only* legitimate basis for a sell recommendation — ordinary drawdown is explicitly excluded.

### IREN
- **Proof gate:** Microsoft accepts and pays for Horizon Tranche 2 (or the next contractual tranche) on its stated schedule, AND the company secures ≥50% of the ~$8B additional FY27 financing gap via debt/facility (not equity issuance) by the FY27 capex ramp date currently guided.
- **Warning gate:** Any single quarter where AI-Cloud revenue growth stalls quarter-over-quarter against the >$4B contracted ARR run-rate, OR the additional FY27 financing is announced but >50% equity-funded.
- **Break gate:** (a) Microsoft fails to accept or pay for a subsequent Horizon tranche on schedule, OR (b) the $3.65B facility's investment-grade rating is downgraded or a covenant is breached, OR (c) bitcoin-mining revenue declines >30% quarter-over-quarter without a corresponding AI-Cloud offset, creating the air-pocket scenario, in any single reported quarter.

### WULF
- **Proof gate:** Anthropic completes its IPO (or a confirmed, priced financing round) on or before Q1 2027 as currently estimated, with no disclosed adverse change to the Justified Data Campus lease terms, AND WULF's H2 2027 initial-capacity date for that campus is reaffirmed in a Q1/Q2 2027 company filing.
- **Warning gate:** Any of: (a) Anthropic's confidential S-1 process is publicly reported as delayed beyond Q1 2027, (b) any news of Anthropic credit-facility covenant stress or a down-round in its private financing, (c) WULF discloses any slippage to the H2 2027 initial-capacity date, or (d) the $2.5B convertible notes trade or are reported at a level implying near-term conversion pressure.
- **Break gate:** (a) Anthropic's IPO is formally withdrawn or its financing conditions deteriorate to the point of a confirmed down-round or credit-facility default, OR (b) WULF misses the H2 2027 initial-capacity date for the Justified Data Campus as subsequently confirmed in a company filing, OR (c) WULF refinances the $2.5B convertible notes or $3.2B senior secured notes at materially worse terms (rate increase or forced conversion) before the Anthropic lease begins recognizing revenue, OR (d) Google discloses a reduction of its 14% stake or $3.2B backstop commitment.

### NVDA (monitoring only, per Underwriter's light-touch scope — no break gate proposed this run)
- **Proof gate:** Vera Rubin ramp lands at or above the ~20% of Q3 FY27 data-center-revenue projection despite the flagged memory constraint.
- **Warning gate:** Gross margin guidance is cut again beyond the already-guided 71–72% Q4 FY27 trough, OR a named competitor is disclosed as having secured materially better HBM/LPDRAM allocation.
- **Break gate:** Not proposed this run — no evidence surfaced rises to a solvency/existential threshold for a mega-cap supplier; escalate to a full re-underwrite only if a competitor is confirmed to have taken disclosed market share as a result of NVIDIA's memory-driven spec cuts.

### ONDS
- **Proof gate:** Q3 or Q4 2026 report confirms FY26 revenue guidance ($525–550M) is reaffirmed or raised, AND Army IDIQ awarded-task-order total surpasses $400M (from ~$240M currently).
- **Warning gate:** IDIQ award-conversion pace for two consecutive quarters falls below the trailing two-quarter pace, OR DZYNE/Cyber Hawk integration produces a disclosed write-down.
- **Break gate:** FY26 guidance is formally walked back at Q3 or Q4 report, OR the company announces a dilutive equity raise driven by cash-position deterioration rather than growth investment.

### OKLO
- **Proof gate:** Centrus HALEU supply LOI converts to a binding, priced supply agreement, AND weighted-average share growth for H2 2026 comes in below the H1 2026 pace (15.3%/6mo) — i.e., dilution rate decelerating.
- **Warning gate:** Any single-quarter dilution pace at or above the H1 2026 rate continuing for two additional consecutive quarters without a corresponding de-risking milestone (binding supply agreement, first customer contract).
- **Break gate:** Groves isotope facility or first Aurora powerhouse delivery is confirmed delayed materially past the 2029 target in a company filing, OR any NRC licensing setback specific to Oklo's design is confirmed.

### ABSI
- **Proof gate:** ABS-201 Phase 1 data reads out positive, or a second pharma partner signs an investment/licensing deal comparable in scale to the Eli Lilly $40M investment.
- **Warning gate:** Partner-program revenue declines for one additional consecutive quarter without a new signed partnership announced.
- **Break gate:** ABS-201 Phase 1 data reads out negative or is confirmed ambiguous by the company AND no new partnership is announced within the same reporting cycle.

---

## Part D — Drawdown vs. Break-Gate Discipline (explicit statement per spec)

Per Ledger §1 (40% max-drawdown target, 50% hard limit) and this spec's constraint ("drawdown alone is neither a sell reason nor a hold reason — only a defined break gate triggers a sell recommendation"): IREN is currently at roughly -4.3% and WULF at roughly -10.3% against their respective average costs (Ledger §2 current price vs. avg cost). **Neither drawdown level, nor any future drawdown up to the Ledger's 50% hard limit, is by itself a basis to sell or hold either name.** Only the break-gate events defined in Part C above (Anthropic financing failure, missed H2 2027 date, Microsoft tranche non-acceptance, IG-rating downgrade, etc.) constitute a legitimate sell trigger under this framework. If a future drawdown approaches the mandate's 50% hard-limit threshold on either name without a break gate having fired, that is a Master-Ledger-level portfolio-risk-tolerance question for Mark to resolve directly, not a signal this agent or any other CAOS agent should treat as an automatic sell instruction.

---

## Verdict

```
RISK REVIEW = COMPLETE / DATA LIMITED
```

Complete in that: every applicable risk category from this agent's mandate was tested against all 8 funded holdings and all 3 candidates, portfolio-level concentration/factor/correlated-thesis math was computed from the Ledger, realistic permanent-loss paths were identified for every name with sufficient input evidence, and exact proof/warning/break gates were defined for IREN, WULF, NVDA, ONDS, OKLO, and ABSI.

Data-limited in that: this agent had no independent research access this run and inherited all factual figures from the Underwriter's labels — several of which the Underwriter itself flagged as DATA LIMITED or UNVERIFIED LEAD (WULF's current September market cap, IREN's private-placement pricing terms, ONDS's precise dilution history, Anthropic's own credit standing, exact debt-maturity dates for WULF's notes). Additionally, five of the eight funded holdings (PLTR, MSFT, KO, GOOGL, TSLA) were outside this run's Underwriter scope and received only structural/concentration analysis from the Ledger, not a fresh risk review — flagged in Part B4 for the next Underwriter cycle, particularly PLTR given it is the single largest position in the book (~35.6% of the funded total).

**Top finding this run:** WULF's break-gate risk is real, specific, and dated (Anthropic's IPO/financing timeline through Q1 2027, WULF's own H2 2027 revenue-start date), and is materially different in kind from IREN's — WULF's largest contract rests on an unrated, privately-financed counterparty rather than an investment-grade one. This does not by itself justify a sell (per Part D, no break gate has fired), but it does mean WULF's warning gates deserve tighter monitoring cadence than IREN's between now and Anthropic's IPO window.
