# RISK & SURVIVABILITY RUN — 2026-09-09_001

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/UNDERWRITER_2026-09-02_001]] — 5 Monster Files (IREN, WULF, ONDS, OKLO, ABSI) with convexity and evidence/survivability-adjusted attractiveness
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — portfolio state 2026-09-09: 6 funded holdings, €5,465.84 cash, €9,405.50 total, 40% max drawdown target
- [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_2026-09-09_001]] — portfolio count resolved (8→6); CEG/ISRG flagged SERIOUS REVIEW
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-09_001]] — portfolio snapshot confirmed; data quality DEGRADED

**Note:** UNDERWRITER_2026-09-09_001.md does not exist; using UNDERWRITER_2026-09-02_001.md (latest Underwriter output). IREN/WULF are funded holdings; ONDS/OKLO/ABSI are Monster File candidates not yet funded.

---

## PERMANENT-LOSS PATHS & RISK MAP

### MONSTER FILE 1 — IREN LIMITED (IREN) — Current Funded Holding
**Current position:** 8.11 shares @ $36.01 = ~€292 (~3.1% of €9,405.50)

**Concentration Risk (if added):** €1,000 deployment = €1,292 total IREN (~13.7%). €1,500 deployment = €1,792 (~19.0%). Creates single-name concentration risk.

**Liquidity/Financing/Dilution Risk:** NASDAQ trading, $13.2B+ market cap, no acute liquidity friction. Critical gap: ~$8B FY27 capex unfinanced. **DATA LIMITED** on private-placement terms. Dilution path if capex gap closes via >20% equity raise. **Moderate-to-high dilution risk.**

**Execution/Customer/Regulatory/Correlation Risk:** Bitcoin mining declines while AI Cloud ramps from $>4B ARR baseline. Microsoft is sole major counterparty (single-customer concentration). Moderate regulatory risk. IREN + WULF highly correlated (0.8) on mining-decline vector.

**PROOF GATE (Q2 FY27, due 2026-09-30):** AI Cloud quarterly revenue ≥$200M + Bitcoin mining ≥$50M/quarter + Microsoft Horizon 2 acceptance confirmed.

**WARNING GATE (Q2 FY27):** AI Cloud $100M–$199M OR Bitcoin mining <$50M/quarter OR Horizon 2 delayed OR capex financing gap requires equity dilution.

**BREAK GATE (Q2 FY27 or any downgrade):** AI Cloud ≤$99M + Bitcoin mining ≤$30M/quarter OR $3.65B facility downgraded below investment-grade OR >20% equity dilution OR Microsoft terminates Horizon tranches.

**Risk disposition:** WATCH WITH SPECIFIC TRIGGER (Proof gate 2026-09-30). Current holding; no new deployment until proof gate confirmed.

---

### MONSTER FILE 2 — TeraWulf (WULF) — Current Funded Holding
**Current position:** 18.92 shares @ $14.46 = ~€274 (~2.9%)

**Concentration/Liquidity/Financing/Dilution Risk:** €1,000–€1,500 deployable. $5.8B total debt (63% of cap) materially higher leverage than IREN. $2.5B convertible notes standing dilution overhang. **Anthropic lease ($19B headline) rests on unrated, privately-financed, pre-IPO counterparty with NO disclosed credit backstop.** **Single most consequential open gap in Underwriter run.**

**Execution/Customer/Regulatory/Correlation Risk:** Deliver 378MW Fluidstack (H2 2026), 401MW Anthropic Justified Data Campus (H2 2027 start). Fluidstack has Google $3.2B backstop (de-risks). Anthropic credit standing UNVERIFIED. Moderate regulatory risk. Correlated ~0.85 to ANTHROPIC performance + NVDA/MSFT on AI capex.

**PROOF GATE (Q3 2026, due 2026-09-30–2026-12-31):** HPC-lease revenue ≥$30M/quarter + Anthropic lease H2 2027 confirmed + Google 14% stake/backstop reaffirmed. **Anthropic IPO files final prospectus or announces Q4 2026/Q1 2027 listing date.**

**WARNING GATE (Q3 2026):** HPC-lease revenue $20M–$29M/quarter OR Anthropic IPO stalls past Q1 2027 OR Fluidstack 378MW delivery missed OR Google reduces backstop.

**BREAK GATE (Q3 2026 or any announcement):** HPC-lease revenue ≤$19M/quarter OR Anthropic IPO halted past Q2 2027 OR convertible-note covenant breach OR Google exits stake OR Justified Data Campus ramp delayed 12+ months.

**Risk disposition:** WATCH WITH SPECIFIC TRIGGER (Proof gate 2026-09-30–2026-12-31). Anthropic credit is highest-priority open gap. New deployment NOT recommended until Anthropic IPO clarifies.

---

### MONSTER FILE 3 — Ondas Holdings (ONDS)
**Current position:** Not funded; HIGH-PRIORITY CHALLENGER

**Concentration/Liquidity/Financing/Dilution Risk:** €1,000–€1,500 deployable at ~$3.2B market cap. Cash ~$1.4B (~44% of market cap); deployed $325M for acquisitions; **dilution history unconfirmed for terms/pricing.** Moderate dilution risk if cash burns faster than expected.

**Execution/Customer/Regulatory/Correlation Risk:** Mistral/LUS IDIQ $982M ceiling; $240M awarded (24% conversion). Key risk: if task-order conversion plateaus, "backlog" overstates revenue. FY26 guidance ($525M–$550M) must hold. DZYNE/Cyber Hawk integration must execute cleanly. **100% DoD-dependent; zero geographic diversification.** Asymmetric regulatory risk (upside from DoD spending, downside from appropriations squeeze).

**PROOF GATE (Q3 2026, due 2026-10-31):** FY26 guidance reaffirmed or raised + Army IDIQ awarded total >$400M (from $240M) + DZYNE/Cyber Hawk integration shows no write-downs.

**WARNING GATE (Q3 2026):** FY26 guidance reaffirmed but IDIQ awarded remains $240M–$300M OR DZYNE/Cyber Hawk shows margin dilution (1–2 points) OR FY27 growth guided <20%.

**BREAK GATE (Q3 2026 or any announcement):** FY26 guidance walked back OR IDIQ awarded plateaus ≤$250M OR DZYNE/Cyber Hawk produces >2 point margin dilution OR Congress delays DoD appropriations into 2027.

**Risk disposition:** HIGH-PRIORITY CHALLENGER, NOT BUY-AUTHORIZED. Proof gate 2026-10-31 required before Seed authorization.

---

### MONSTER FILE 4 — Oklo (OKLO)
**Current position:** Not funded; pre-revenue Serious Review

**Concentration/Liquidity/Financing/Dilution Risk:** $6.66B market cap (down ~80% from 2025 highs), €1,000–€1,500 deployable. **Dilution is dominant risk:** +15.3% share growth in H1 2026 via $1.85B ATM offerings. **Per-share dilution eroding faster than enterprise value grows.** All capex equity-funded (zero commercial revenue).

**Execution/Customer/Regulatory/Correlation Risk:** Core thesis: Groves isotope + Aurora powerhouse delivery 2029+ (multi-year, binary technology risk). **Zero commercial revenue; no paying customers.** Depends on Centrus HALEU supply agreement + NRC licensing + customer demand. **Highest regulatory risk in portfolio** — NRC approval is existential. **Asymmetric political risk: upside from nuclear/AI power policy, downside from anti-nuclear shifts.**

**PROOF GATE (within 12 months, by 2027-09-09):** Centrus supply LOI converts to binding priced agreement + Groves/Aurora reaches late-stage NRC licensing (FSAR approval) + Oklo secures paying customer contract (binding PO) with 2029–2030 delivery and pricing.

**WARNING GATE (by 2027-09-09):** Centrus LOI unsigned AND Groves/Aurora NRC licensing still early stage OR cash-burn guidance raised OR share dilution >15% annually.

**BREAK GATE (any date):** NRC design rejection OR Centrus supply terminated OR share dilution >20% YoY (40%+ annualized) OR cash runway revised from "H2 2028" to "H1 2028" or earlier.

**Risk disposition:** WATCH WITH SPECIFIC TRIGGER (Proof gate within 12 months). **Recommend €1,000 max deployment, not €1,500** (asymmetric tail risk).

---

### MONSTER FILE 5 — Absci (ABSI)
**Current position:** Not funded; clinical-stage biotech

**Concentration/Liquidity/Financing/Dilution Risk:** $1.56B market cap, €1,000–€1,500 deployable. Cash $201.1M (runway H2 2028). **Shares +31% in past year.** Per-share economics eroding. Dependent on Phase 1 success for partnership/licensing/better funding.

**Execution/Customer/Regulatory/Correlation Risk:** Origin-1 AI platform for antibody design **unproven:** trailing partner revenue **declining** ($0.3M Q2 2026 vs $0.6M Q2 2025; -50% YoY). Disqualifying evidence against platform-monetization thesis. ABS-201 Phase 1 is binary clinical readout (success = partnerships; failure = thesis broken within 6 months). Phase 2 is 12–24 months later. **Low direct regulatory risk.** Inverse correlation to AI capex cycle (potential hedge).

**PROOF GATE (within 12 months, by 2027-09-09):** ABS-201 Phase 1 data positive (meets primary endpoints) + major pharma partner (beyond Eli Lilly) announces partnership/licensing (≥$10M upfront) + Eli Lilly or secondary partner commits ≥$50M milestone funding Phase 2/3.

**WARNING GATE (by 2027-09-09):** Phase 1 positive BUT below blockbuster efficacy OR Eli Lilly no follow-on partnership by 12 months OR partner revenue <$0.5M/quarter OR cash runway shortens from "H2 2028" to "H1 2028".

**BREAK GATE (any date):** Phase 1 negative or safety signals OR Eli Lilly terminates partnership OR partner revenue <$0.2M/quarter OR down-round below $9.22 OR >40% annualized share dilution OR bankruptcy/distressed sale.

**Risk disposition:** WATCH WITH SPECIFIC TRIGGER (Proof gate within 12 months). **Recommend €1,000 max deployment, not €1,500** (clinical binary outcome).

---

## PORTFOLIO SURVIVABILITY CHECK

**Current (6 securities + €5,465.84 cash):** NVDA 17.1%, MSFT 10.4%, GOOGL 6.7%, TSLA 6.3%, IREN 3.1%, WULF 2.9%  
**40% max drawdown target:** €3,762.20  
**Cash buffer:** €5,465.84 (58.1%, strong protection)

**Current holdings break-gate status:** No signals yet. IREN/WULF require proof gates by 2026-09-30 / 2026-12-31. **If either misses proof gate by year-end 2026, Portfolio Court must re-assess conviction.**

**New deployment impact (€1,000–€1,500):** All 5 candidates fundable within 40% max-drawdown tolerance. **Recommend IREN (€1,500, proof gate 2026-09-30) or ONDS (€1,500, proof gate 2026-10-31).** Defer OKLO/ABSI (binary outcomes; €1,000 max each).

---

## CORRELATED-RISK MAPPING

**IREN + WULF (0.8 correlation):** Both bitcoin-mining-to-hosting pivots. **Double exposure if both deployed.** Recommend IREN over WULF for new capital.

**NVDA + IREN/WULF (0.8 correlation):** Current NVDA 17.1% + IREN 3.1% + WULF 2.9% = **23.1% correlated to AI infrastructure.** Concentration risk material.

**ONDS (0.1–0.2 correlation with all holdings):** Defense autonomy **diversifier.** Recommended new-deployment candidate.

**OKLO (0.4–0.5 correlation):** Reinforces AI infrastructure thesis; defer until proof gate confirmed.

**OKLO + ABSI (0.6 correlation):** Both binary outcomes; do not deploy to both in same rebalance.

---

## PERMANENT-LOSS PATHS RANKED BY SEVERITY

1. **ABSI** (50–70% failure risk, Phase 1 clinical binary)
2. **OKLO** (NRC rejection or 3+ year delay, multi-year runway buys time)
3. **ONDS** (DoD budget/political risk, 10–20% annual probability)
4. **WULF** (Anthropic credit unrated/unverified, IPO timing uncertain)
5. **IREN** (Microsoft strong, financing IG-rated, $8B capex gap real)

---

```
RISK REVIEW = COMPLETE
```

**Run date:** 2026-09-09  
**Agent:** Risk and Survivability (Agent 7/9)  
**Status:** COMPLETE  
**Next downstream:** Red Team (optional) / Portfolio Court / Orchestrator
