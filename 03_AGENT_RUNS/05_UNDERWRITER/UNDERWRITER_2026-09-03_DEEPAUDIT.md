# UNDERWRITER_2026-09-03_DEEPAUDIT

## Inputs Consulted
- [[03_AGENT_RUNS/05_UNDERWRITER/_AGENT SPEC — Underwriter]] (role spec, read in full)
- [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_2026-09-03_DEEPAUDIT]]
- [[03_AGENT_RUNS/03_FORWARD/FORWARD_2026-09-03_DEEPAUDIT]]
- [[03_AGENT_RUNS/04_INDUSTRY/INDUSTRY_2026-09-03_DEEPAUDIT]]
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] (share counts, avg cost, current price, §11 draft sizing rules)
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] (open Tribunal, Event Gate, and Challenger handoffs — read for context; not adjudicated here, per spec — that is Portfolio Court/Orchestrator's job)

## Scope and Method Note
Per the Deep Audit task brief, this run produces one fresh Monster File for each of the 8 current holdings (PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF), none pre-approved. Each Monster File tests, in order: **inclusion** (would CAOS buy this today starting from 100% cash), **sizing** (is the current weight justified), **proof gate** (next falsifiable checkpoint, taken from Forward), and **replacement risk** (is there better use of this capital among today's Discovery candidates). Raw convexity and evidence/survivability-adjusted attractiveness are reported as two separate, never-merged fields, per spec. No figure is fabricated — where Discovery/Forward/Industry did not surface a number, this file says DATA LIMITED or UNKNOWN.

**Position-weight caveat:** weights below are computed by this agent directly from the Master Ledger's own recorded shares × current price (Verifier's price snapshot, DATA QUALITY = DEGRADED per Verifier/Industry). Total holdings value used as denominator: **$10,817.67** (sum of the 8 positions' shares × price; cash of €0.95 is immaterial and excluded). This is arithmetic on Ledger-recorded numbers, not a new price pull — labeled CAOS INFERENCE for the resulting percentages, VERIFIED FACT for the underlying share counts (Ledger-recorded) and DATA LIMITED for the prices themselves (carried from Verifier's DEGRADED finding).

This agent does not size positions, execute trades, or write to the Master Ledger. Sizing/count-overage adjudication remains Portfolio Court/Orchestrator's job per the open `20260902-DAILY-PORTFOLIO-COUNT_OVERAGE` Tribunal; this file only tests whether current weights are *justified by the evidence*, which is this agent's mandate.

---

## MONSTER FILE 1 — PLTR (Palantir Technologies)

**Position facts:** 21.68808861 sh @ avg cost $29.44, current price $177.56 (VERIFIED FACT, per Ledger/Verifier). Unrealized gain ≈ +503%. Position value ≈ $3,851.35 → **weight ≈ 35.6% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test (100%-cash-first frame):** Would CAOS buy PLTR today, fresh, from cash? On the evidence — Q2 2026 revenue +93% YoY, U.S. commercial +149% YoY, U.S. government +90% YoY (VERIFIED FACT per Forward), FY2026 guidance raised twice this cycle to $8.15B–$8.16B revenue and $4.50B–$4.70B adjusted FCF (CAOS INFERENCE, company guidance) — the growth and profitability case for *some* position is strong. **PASS on inclusion**, but the question that matters more here is sizing, not inclusion.

**Raw convexity regime:** At $177.56, PLTR already trades on a very large forward-growth multiple (no explicit P/S or P/E figure was surfaced by Forward/Industry this run — DATA LIMITED on current multiple). A 3x from here to ~$533/share, sustained, would require FY2026-guided ~82% revenue growth to *continue compounding at a similar rate for several more years* without material multiple compression — theoretically possible given the U.S. commercial trajectory but **not a base case**. A 10x (~$1,776/share) is UNKNOWN / not credible from this evidence base at this starting multiple — no evidence surfaced this run supports it. 30x/100x regimes: **not credible, excluded** (no evidence submitted this cycle supports a company already generating billions in revenue at this valuation re-rating 30–100x from here).

**Evidence/survivability-adjusted attractiveness:** Survivability is not in question (profitable, FCF-positive, guidance raised, no financing/dilution risk surfaced). The adjusted-attractiveness question is entirely about **denominator risk**: the position is already priced for continued hyper-growth, and at 35.6% of holdings, this is no longer a "monster file candidate," it is the single dominant bet in the portfolio. Evidence quality on the growth trajectory itself is HIGH (VERIFIED FACT trailing results, CAOS-INFERENCE-labeled but company-issued forward guidance, raised twice). **Adjusted attractiveness: MODERATE-TO-LOW at current weight** — not because the business case weakened, but because the position size means a normal multiple-compression event (not a business failure) could inflict portfolio-level damage disproportionate to any single stock's normal role.

**Sizing role test:** Master Ledger §11 draft rule: Core/Attacker positions should normally have "a credible path toward approximately 5% of NAV." PLTR sits at ~35.6% — **more than 7x the draft norm**. This is not a marginal overage; it is the largest single-position concentration risk in the portfolio and, per the existing `20260902-DAILY-PORTFOLIO-COUNT_OVERAGE` Tribunal, was already flagged by Red Team as the *larger-in-dollar-terms* breach relative to the count overage. This Deep Audit reconfirms that finding independently: **sizing is not justified by the evidence and requires Portfolio Court adjudication** — this agent does not execute the trim, only flags that the evidence does not support the current weight.

**Proof gate (from Forward):** Q3 2026 earnings (expected early November 2026, exact date unconfirmed) — test is whether reported revenue lands within/above the $2.160B–$2.164B guided range and whether U.S. commercial growth continues tracking toward the >134% FY guide.

**Replacement risk:** No Discovery candidate this run offers a comparable growth+profitability combination at PLTR's scale; replacement risk is **not about swapping PLTR out entirely**, it is about whether capital trapped in the *excess* 30+ points of overweight would be better redeployed toward the count-overage fix (funding a trim into the 7-security cap) or toward AMKR/MP (Challengers, direct AI-supply-chain beneficiaries with less concentration risk). This agent flags the redeployment question; it does not decide it.

**Kill conditions:**
- Two consecutive quarters of revenue growth deceleration below ~50% YoY without a guided reacceleration path
- Any guidance *cut* (not just a smaller raise) on FY revenue or commercial growth
- Loss of U.S. government contract base (a stated concentration risk not tested by this run — DATA LIMITED, no government-contract-concentration figure surfaced)
- Persistent multiple compression (evidence: DATA LIMITED, no current P/S multiple surfaced this run to set a compression trigger against)

---

## MONSTER FILE 2 — NVDA (NVIDIA Corporation)

**Position facts:** 14.88458404 sh @ avg cost $98.59, current price $216.89 (VERIFIED FACT). Unrealized gain ≈ +120%. Position value ≈ $3,228.65 → **weight ≈ 29.8% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** Q2 FY2027 revenue $96.2B (+106% YoY), Data Center segment $89.02B (+117% YoY) — VERIFIED FACT per Forward, primary-source-cited. Q3 FY2027 guide $108.0B ±2% (CAOS INFERENCE, company target). Industry confirms this is unchanged/reaffirmed, no new negative signal, and the HBM/DRAM shortage (Industry §2, DATA LIMITED/UNVERIFIED LEAD on magnitude, but directionally consistent across many aggregator sources) is a **structural tailwind for NVDA's supply position**, not a threat to it — NVDA is the demand-side beneficiary of the same bottleneck that pressures IREN/WULF's build costs. **PASS on inclusion**, comfortably.

**Raw convexity regime:** NVDA is already the largest company in the world by most public accounts (not independently re-verified this run — DATA LIMITED on exact market cap). A 3x from $216.89 (~$651/share) would require sustained hyperscaler capex growth continuing at a scale even larger than the already-enormous current base — MSFT and GOOGL both raised FY2026 capex guidance this cycle and flagged further 2027 growth without a number yet (Forward, CAOS INFERENCE), which is a supportive but not sufficient signal. 10x/30x/100x: **not credible at this scale** — no evidence this run supports outsized re-rating multiples for a company already priced for continued dominance; excluded from the credible regime.

**Evidence/survivability-adjusted attractiveness:** Survivability is essentially not in question — high margins, no financing/dilution risk, unmatched revenue scale. Evidence quality is HIGH across Forward (VERIFIED FACT trailing results, tight guidance discipline) and Industry (no negative signal, permanent gate not triggered this run). **Adjusted attractiveness: MODERATE-HIGH** — the business case remains excellent, but the *raw convexity ceiling is structurally capped by scale* (a company already this large cannot deliver 10x+ without a genuinely new category of demand, which is not what's currently being underwritten — this is continuation of an existing trend, not optionality).

**Sizing role test:** ~29.8% of holdings vs. the ~5% draft Core/Attacker norm — **the second-largest sizing overage in the portfolio**, roughly 6x the draft norm. Same finding as PLTR: not justified by draft §11 rules as currently written, and part of the same Tribunal. This agent flags the mismatch; adjudication is Portfolio Court's job.

**Proof gate (from Forward):** NVDA's Q3 FY2027 earnings release (~late November 2026, exact date unconfirmed) — test is whether revenue lands within $108.0B ±2% and Data Center segment growth continues near the current pace.

**Replacement risk:** No Discovery candidate this run rivals NVDA's combination of scale, margin, and demand visibility. As with PLTR, the replacement question is about the *excess* weight above a justified norm, not about exiting the name. GLW (Corning, fiber optics — NVDA is itself a $3.2B investor in Corning's capacity buildout per Discovery, UNVERIFIED LEAD) and APH/TEL (connector supply chain) are adjacent, smaller-scale beneficiaries of the same capex wave — plausible partial-diversification candidates for excess capital, not replacements for the core position.

**Kill conditions:**
- Any Q3 FY2027 print materially below the $108.0B ±2% guide, or a downward revision to the FY28 ~70% growth guide (Industry §1)
- Evidence that non-hyperscaler demand (~half of NVDA's data-center book per Industry, CAOS INFERENCE, not independently re-verified this run) is masking hyperscaler-side deceleration
- A verified China-market-access reversal materially changing the "no China data-center sales assumed" baseline (Industry §1) — DATA LIMITED, not tested this run beyond noting the baseline assumption
- HBM/DRAM cost inflation (Industry §2) compressing NVDA's own margin guide below the 74.0% ±50bps Q3 guide

---

## MONSTER FILE 3 — MSFT (Microsoft Corporation)

**Position facts:** 1.96105021 sh @ avg cost $356.11, current price $497.14 (VERIFIED FACT). Unrealized gain ≈ +39.6%. Position value ≈ $975.06 → **weight ≈ 9.0% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** Q1 FY2027 guide: revenue $89.85B–$90.95B (~+16% YoY), Azure growth guided toward ~45%, capex to exceed $50B for the quarter (all CAOS INFERENCE, company-issued nonbinding targets per Forward). CY2026 capex reported at ~$175B "comparable" after a useful-life accounting reclassification from an April guide of ~$190B — Forward explicitly flags this is **not a straightforward cut**, the like-for-like figure is the operative signal, not the raw headline. **PASS on inclusion** — durable, profitable, AI-demand-linked growth engine with no survivability concern.

**Raw convexity regime:** MSFT is a >$3T-scale company (not independently re-verified this run — DATA LIMITED on exact market cap). A 3x is arithmetically possible only over a multi-year horizon with sustained ~16%+ revenue growth *and* multiple expansion — plausible but not a near-term base case. 10x/30x/100x: **not credible at this scale**, excluded.

**Evidence/survivability-adjusted attractiveness:** Survivability is not a live question. Evidence quality HIGH (VERIFIED FACT trailing results, CAOS-INFERENCE-labeled forward guidance from a company with a strong guidance-discipline track record). Power/grid constraint noted by Industry (~$80B power-constrained Azure backlog, CAOS INFERENCE, carried forward not re-verified) is a real execution risk on capacity delivery timing, not a demand risk. **Adjusted attractiveness: MODERATE-HIGH**, comparable in quality to NVDA but with lower raw convexity given even larger scale and a more diversified revenue base (less pure-play AI exposure than NVDA).

**Sizing role test:** ~9.0% of holdings vs. the ~5% draft norm — **overweight, but only ~1.8x**, a materially smaller overage than PLTR (7x) or NVDA (6x). This is a marginal, not severe, sizing question.

**Proof gate (from Forward):** MSFT's Q1 FY2027 earnings release (~late October 2026) — test is whether revenue lands within $89.85B–$90.95B, quarterly capex exceeds $50B, and Azure growth reaches ~45%.

**Replacement risk:** No Discovery candidate this run offers a comparable combination of scale, diversification, and AI-demand exposure. Low replacement risk; the modest overweight does not obviously warrant trimming ahead of the more severe PLTR/NVDA overages.

**Kill conditions:**
- Azure growth printing materially below the ~45% guide with no credible reacceleration path
- A genuine (not accounting-reclassification-driven) capex cut signaling demand-side weakness
- 2027 capex guidance, when finally disclosed, coming in flat or down against 2026's ~$175B comparable base (Forward flags this as an open falsifiable gap across MSFT/GOOGL/NVDA)

---

## MONSTER FILE 4 — KO (The Coca-Cola Company)

**Position facts:** 11.07061496 sh @ avg cost $68.13, current price $88.11 (VERIFIED FACT). Unrealized gain ≈ +29.3%. Position value ≈ $975.42 → **weight ≈ 9.0% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** Q2 2026 organic revenue +6% YoY, unit case volume +5%, growth in every reporting segment (VERIFIED FACT per Forward). FY2026 guidance raised: organic revenue ~5% (top of prior range), comparable EPS growth raised to 9%–10% (CAOS INFERENCE, company guidance). This is a well-run, durable consumer-staples compounder. **Inclusion is defensible on stability grounds**, but KO is structurally the weakest fit for a "maximize CAGR" mandate with a 40% drawdown tolerance among the 8 holdings — it is a low-volatility, low-convexity name in a mandate explicitly optimized for compounding growth, not capital preservation. This is the one holding where the inclusion test genuinely strains against the mandate rather than the sizing test.

**Raw convexity regime:** KO is a mega-cap consumer staple with mid-single-digit organic growth. A 3x from $88.11 (~$264/share) is **not credible on any evidence surfaced this run** — no plausible near-to-medium-term catalyst was found in Forward or Industry that would drive a staples name at this growth rate to triple. Even framing this in "raw convexity" terms overstates the honest picture: KO's realistic upside case, per the evidence available, is closer to a high-single-digit-to-low-teens total-return compounder (dividend + ~5% organic growth + modest multiple stability), not a multi-bagger. 10x/30x/100x: **excluded, not remotely credible**.

**Evidence/survivability-adjusted attractiveness:** Survivability is essentially never in question for KO (durable brand, consistent FCF, dividend aristocrat status — not independently re-verified this run but consistent with widely known priors; not fabricated as a new figure). Evidence quality HIGH. But "adjusted attractiveness" in the CAOS framework is explicitly about *how likely and investable the payoff actually is* — and the honest answer is that KO's payoff, however likely, is **small relative to the CAGR-maximization mandate**. **Adjusted attractiveness: LOW-TO-MODERATE for a CAGR-maximizing mandate specifically** (it would score higher under a capital-preservation or income mandate, which this portfolio does not have).

**Sizing role test:** ~9.0% of holdings — **near-double the ~5% draft Core/Attacker norm**, for the lowest-convexity name in the portfolio. This is the sizing question most worth Portfolio Court's attention after PLTR/NVDA: not because KO is risky, but because its weight is not obviously earning its keep in a CAGR-maximization mandate relative to what that capital could do elsewhere.

**Proof gate (from Forward):** KO's Q3 2026 earnings release (~late October 2026) — test is whether organic revenue growth continues tracking toward ~5% FY guide and comparable EPS growth stays within the raised 9%–10% band.

**Replacement risk:** This is the holding where replacement risk is most live. Every Discovery candidate this run (AMKR, MP, SNDK, GLW, CSCO, APH, TEL, CRWD, PANW, FTNT, LHX, RKLB, TMO) offers materially higher raw convexity than KO, though all carry correspondingly higher evidence/survivability uncertainty (mostly UNVERIFIED LEAD per Discovery, not yet Underwriter-tested). This agent does not recommend a swap outright — that requires primary-source underwriting of the specific replacement candidate, not done this run — but flags KO as the **highest-priority inclusion-and-sizing question for the next Deep Audit cycle** given the mandate's explicit CAGR-maximization objective.

**Kill conditions:**
- Organic revenue growth falling back below the pre-raise 4% floor
- Comparable EPS growth missing the raised 9%–10% band
- No genuine near-term case exists for a "kill on convexity failure" the way there would be for a growth name — KO's kill conditions are about *mandate fit*, not business failure

---

## MONSTER FILE 5 — GOOGL (Alphabet Inc., Class A)

**Position facts:** 1.85516511 sh @ avg cost $106.45, current price $336.75 (VERIFIED FACT). Unrealized gain ≈ +216%. Position value ≈ $624.83 → **weight ≈ 5.8% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** Q2 2026 revenue $119.8B (+24% YoY), Cloud revenue $24.8B (+82% YoY), Cloud backlog $514B (VERIFIED FACT per Forward). FY2026 capex guidance raised to $195B–$205B from $180B–$190B (CAOS INFERENCE), attributed to accelerating capacity delivery to meet demand — a genuinely bullish signal, not a defensive one. Market reportedly reacted negatively to the raise (Forward notes this as a live catalyst/risk). **PASS on inclusion.**

**Raw convexity regime:** Alphabet is a >$2T-scale company (not independently re-verified this run — DATA LIMITED). A 3x from $336.75 (~$1,010/share) would require sustained Cloud hyper-growth (82% YoY currently) continuing for years at a similar clip plus multiple re-rating — plausible directionally given the backlog figure, but not a near-term base case. 10x+: **not credible at this scale**, excluded.

**Evidence/survivability-adjusted attractiveness:** Survivability not in question. Evidence quality HIGH (VERIFIED FACT trailing results, large disclosed backlog). The unresolved 2027 capex figure (Forward: "continues to expect" further increase, no number given) is a genuine open item but not a red flag — it mirrors MSFT's identical situation. **Adjusted attractiveness: MODERATE-HIGH**, similar quality tier to MSFT/NVDA.

**Sizing role test:** ~5.8% of holdings — **the closest of any holding to the ~5% draft Core/Attacker norm**, only marginally over. No material sizing concern.

**Proof gate (from Forward):** Alphabet's Q3 2026 earnings release (~late October 2026) — test is whether Cloud revenue growth holds near 82% YoY, the $195B–$205B FY2026 capex range is reaffirmed or breached, and whether a specific 2027 capex figure is finally disclosed.

**Replacement risk:** Low. GOOGL's size and weight are both reasonably matched to the evidence; no Discovery candidate offers a comparable combination of disclosed backlog scale and diversified revenue base.

**Kill conditions:**
- Cloud revenue growth decelerating materially below the 82% YoY pace with no credible explanation
- A 2027 capex figure, when disclosed, implying a genuine slowdown (not merely a pause in the raise cadence)
- Continued negative market reaction to capex raises compounding into a genuine funding/ROI-credibility question (not surfaced as a live risk this run beyond sentiment — DATA LIMITED on whether this is more than a stock-reaction story)

---

## MONSTER FILE 6 — TSLA (Tesla, Inc.)

**Position facts:** 1.67642235 sh @ avg cost $213.97, current price $356.00 (VERIFIED FACT). Unrealized gain ≈ +66.4%. Position value ≈ $596.81 → **weight ≈ 5.5% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** Q2 2026 deliveries 480,126 (+25% YoY, first YoY growth after two years of decline) — VERIFIED FACT per Forward. This alone supports inclusion as a turnaround/recovery story. But the more consequential forward claim — Optimus humanoid-robot production beginning late July/August 2026 at Fremont — is explicitly flagged by Forward as **the single most speculative forward item across all 8 holdings**, with **no independent confirmation found this run that it happened on schedule**. Industry's robotics lane (§5) found no TSLA-specific development this run either (DATA LIMITED, a coverage gap not a negative finding). **Inclusion is defensible on the EV-delivery-recovery thesis alone**, but any part of the thesis resting on Optimus is currently **unverified, not evidenced**.

**Raw convexity regime:** If Optimus scales as a genuinely new robotics product category (not merely an EV maker), the *theoretical* raw convexity is large — a new addressable market, not incremental EV share. This is the one holding in the portfolio where a 10x-or-larger regime is not automatically incredible on structural grounds (new-category optionality, per spec's own carve-out for 30x/100x "only when credible"). **However — critically — no verified evidence this run supports even the near-term Optimus production milestone, let alone a scaled market case.** Per Burden of Proof, an unverified claim cannot support a "credible" 10x/30x/100x label. **This run rates TSLA's raw convexity regime as UNKNOWN pending Optimus verification, not as a credible 10x/30x/100x case** — the theoretical ceiling is high, but "theoretical" is not "credible" without evidence. On the EV-delivery business alone (ex-Optimus), a 3x is a stretch but not absurd given the Q2 delivery inflection; 10x on autos alone is not supported by any evidence surfaced this run.

**Evidence/survivability-adjusted attractiveness:** Survivability is not a near-term concern (large, profitable-ish core auto business — profitability status not independently re-verified this run, DATA LIMITED). But adjusted attractiveness must discount heavily for the fact that the thesis's most convexity-bearing element (Optimus) is **entirely unverified this cycle**. **Adjusted attractiveness: LOW-TO-MODERATE** — the verified part of the thesis (delivery recovery) is real but modest; the part that would justify large convexity (Optimus) is not evidenced and per Burden of Proof cannot be assumed.

**Sizing role test:** ~5.5% of holdings — close to the ~5% draft norm, essentially in line. No material sizing concern on a pure weight basis, though the *quality* of what's being sized (an unverified robotics thesis layered on a verified but modest delivery recovery) is worth flagging to Portfolio Court separately from the arithmetic.

**Proof gate (from Forward):** Two, per Forward: (a) Tesla's Q3 2026 delivery report (~early October 2026) — test whether YoY delivery growth continues; (b) **direct confirmation of whether Optimus production actually began at Fremont in the guided late-July/August 2026 window — this is the more consequential and currently unverified proof point, and this Deep Audit could not close it.**

**Replacement risk:** Moderate. If Optimus verification fails or slips further, TSLA's thesis reduces to an EV-delivery-recovery story, which is a materially lower-convexity proposition than the current position implies — at that point, Discovery's robotics/humanoid-supply-chain names (APH, TEL, CGNX, ALGM, AMBA — all UNVERIFIED LEAD, not yet Underwriter-tested) would be a more diversified way to express the same "humanoid robotics matters" thesis without single-company execution risk on an unverified production claim.

**Kill conditions:**
- Confirmation that Optimus production did **not** begin in the guided window, with no credible near-term rescheduled date
- Delivery growth reversing back to YoY decline after the Q2 rebound
- FY2026 capex guide (>$25B, "further increases in H2 2026") not materializing, suggesting funding strain on the Optimus buildout specifically

---

## MONSTER FILE 7 — IREN (IREN Limited)

**Position facts:** 8.1098693 sh @ avg cost $37.61, current price $36.01 (VERIFIED FACT). Unrealized loss ≈ -4.3%. Position value ≈ $292.04 → **weight ≈ 2.7% of holdings** (CAOS INFERENCE, arithmetic).

**Inclusion test:** IREN's bitcoin-mining-to-AI/HPC pivot is real and underway (Industry, carried forward from prior run). Q4 FY2026 revenue $137.2M beat consensus; >$4B ARR contracted for FY2026 AI Cloud capacity, $1B already operating with Microsoft having accepted "Horizon 1" (CAOS INFERENCE — company-stated via secondary earnings-call reporting, not independently verified against a primary filing, per Forward). **But only ~18% of trailing FY26 revenue is AI Cloud; ~82% is still mining** (per the open Active Handoff evidence-gate finding, VERIFIED FACT on the revenue-mix figure per that gate's own labeling). This run's Industry pass **confirmed** IREN's $3.0B convertible-notes offering as VERIFIED FACT (1.00% senior notes due 2033, Rule 144A, net proceeds ~$2.96B) but found **no source tying Microsoft specifically to this notes offering** — the "investment-grade-rated Microsoft-backed facility" framing in the existing evidence gate appears to actually refer to a *separate* transaction (the ~$9.7B Microsoft/GB300 deal at Childress, TX), whose own credit terms remain **unconfirmed** (UNVERIFIED LEAD, unresolved, same as prior runs). **Inclusion is marginal-to-defensible** given the real, growing AI Cloud contract book, but the financing picture underpinning FY2027 capacity delivery is genuinely incomplete.

**Raw convexity regime:** If the pivot completes and IREN's contracted AI Cloud ARR base scales toward or beyond FY2027's targeted additional 0.5GW, a 3x–5x from $36.01 is a credible regime given the sector's demonstrated re-rating pattern (WULF and other pivot names have shown comparable moves). 10x is more speculative but not incredible given the small current base and the scale of the AI-infrastructure capacity shortage (Industry §1–2). 30x/100x: **not credible from this evidence base** — excluded.

**Evidence/survivability-adjusted attractiveness:** This is where IREN's case weakens materially. FY2027 capex guidance is $25B–$30B; disclosed funding sources total ~$14B (cash + committed GPU financing) — **a funding gap on the order of $11B–$16B not yet closed by named sources** (Forward, CAOS INFERENCE, directly computed from disclosed figures). This is consistent with, and does not resolve, the ~$8B unfinanced-FY27-capex figure already flagged in the open evidence gate. Per **Survivability Before Optionality**, a large unclosed financing gap on a capital-intensive buildout is exactly the kind of risk that should discount raw convexity heavily regardless of how attractive the AI Cloud contract book looks. **Adjusted attractiveness: LOW-TO-MODERATE** — real business momentum, but survivability/financing risk is the dominant, not secondary, consideration here.

**Sizing role test:** ~2.7% of holdings. Per Master Ledger §11 draft rules, this sits **below the ~5% Core/Attacker norm but above the ~1.5% floor that would require an explicit Seed/Catalyst role** — so it is not a sizing violation under the draft rules as written, though its "Core/Attacker" role label (inherited, not yet formally assigned per Ledger §4) may be a mismatch given the financing-risk profile just described; a Seed/Catalyst role with an explicit evidence gate might fit the actual risk profile better than an unconditional Core/Attacker label. This agent flags the *role-label* question; it does not reassign roles (Portfolio Court's job).

**Proof gate (from Forward):** IREN's Q1 FY2027 earnings release (~November 2026) — test is whether the FY2027 "late-stage discussions" convert into a named, dollar-denominated contracted-capacity announcement, and whether the $25B–$30B FY2027 capex guide gets a named financing source closing the ~$11B–$16B gap.

**Replacement risk:** Moderate. AMKR and MP (Challengers, both HIGH/MEDIUM evidence quality per Active Handoff) offer AI-supply-chain exposure with materially cleaner financing pictures (AMKR: "profitable incumbent, no dilution signal" per its handoff). If IREN's financing gap is not closed by the Q1 FY2027 checkpoint, the case for reallocating this capital toward a cleaner-financed AI-infrastructure name strengthens.

**Kill conditions:**
- No named financing source closing the FY2027 capex gap by the Q1 FY2027 report
- AI Cloud revenue mix failing to grow materially beyond the current ~18% of trailing revenue
- Any credit-quality deterioration or downgrade signal on the $3.0B convertible notes or the separate Microsoft GB300 facility
- Confirmation that the Microsoft-backed-facility framing cannot be substantiated at all (currently UNVERIFIED LEAD, unresolved)

---

## MONSTER FILE 8 — WULF (TeraWulf Inc.)

**Position facts:** 18.91535598 sh @ avg cost $16.12, current price $14.46 (VERIFIED FACT). Unrealized loss ≈ -10.3%. Position value ≈ $273.51 → **weight ≈ 2.5% of holdings** (CAOS INFERENCE, arithmetic) — the smallest position in the portfolio.

**Inclusion test:** WULF's pivot is further along than IREN's on a trailing basis — 71% of trailing revenue is already HPC-derived (VERIFIED FACT per the existing evidence gate). The headline asset is the Anthropic lease: 20-year, 401MW, ~$19B contracted revenue over the initial term (up to ~$33B with both extension options exercised) — Forward and Industry both confirm the **lease itself exists and is company-characterized as contracted revenue** (VERIFIED FACT on existence), but **whether the ~$19B is realizable rests on Anthropic's credit standing, which this Deep Audit's dedicated Industry pass could not resolve** (see below). Revenue does not begin until late 2027 (VERIFIED FACT, dated). **Inclusion is the most evidence-thin of any holding this run** — not because the pivot isn't real, but because the single largest number driving the thesis (~$19B) hangs on an unresolved counterparty-credit question.

**Raw convexity regime:** If the Anthropic lease performs as contracted and WULF's broader HPC-hosting pipeline (CB-4 H2 2026, CB-5 early 2027, reaffirmed 250–500MW/year contracting target) continues, a 5x–10x from $14.46 is a credible *theoretical* regime given WULF's small current base relative to the disclosed contract value (~$19B against a sub-$300M position value in this portfolio, and a company-level market cap not independently re-verified this run — DATA LIMITED). This is the highest raw-convexity ceiling of the growth-name holdings on a pure ratio-of-contract-value-to-current-size basis. 30x/100x: not ruled out on pure arithmetic given the small base, but **this run does not label it credible** absent stronger evidence on the counterparty and financing questions below — kept as UNKNOWN rather than asserted.

**Evidence/survivability-adjusted attractiveness:** This is the most consequential finding of this Deep Audit for WULF specifically. This run's Industry pass made the **priority-designated, good-faith attempt** to resolve the Anthropic-credit evidence gate and could not:
- Anthropic is confirmed **private with no independently found S&P/Moody's rating** (VERIFIED FACT — absence of finding).
- A separate, unrelated Anthropic financing structure (the ~$35–36B TPU SPV) achieves investment-grade quality via **Broadcom's third-party residual-value guarantee**, not Anthropic's own unsecured credit (UNVERIFIED LEAD, but a coherent, multiply-corroborated mechanism).
- Secondary coverage of the **TeraWulf lease specifically** claims it is "underpinned by Anthropic's strong investment-grade credit rating" — Industry flags this as **specifically suspect**: no source identifies who rated Anthropic, on what basis, or when, given Anthropic is confirmed to have no public rating.
- The two documents that would resolve this (TeraWulf's own press release and its SEC 8-K exhibit) were **blocked by network egress restrictions this session** — a tooling failure, not a resolved absence of evidence, per Industry's own explicit disclosure.
- Separately, WULF carries **~$5.8B total debt (~63% of a naive debt+equity cap)** and refinancing/conversion risk on $2.5B convertible notes **ahead of** the H2 2027 revenue start (per the existing evidence gate, EVIDENCE_QUALITY = MEDIUM).

Per **Survivability Before Optionality**, this combination — a single counterparty representing the company's largest contract, whose own credit standing cannot be verified, layered on already-high leverage, with revenue not starting for another ~14+ months — is exactly the profile the law is designed to catch. Per **Burden of Proof**, the "investment-grade" characterization of the lease is an assertion this run could not substantiate. **Adjusted attractiveness: LOW.** This is a clear separation case: raw convexity (high, on a small-base/large-contract ratio) versus evidence-adjusted attractiveness (low, on an unresolved counterparty-credit and leverage combination) — precisely the distinction this agent's spec requires never be merged.

**Sizing role test:** ~2.5% of holdings — the smallest position in the portfolio, below the ~5% Core/Attacker norm but above the ~1.5% Seed floor under Ledger §11 draft rules. Given the adjusted-attractiveness finding above, **the current small size is arguably appropriate risk management already in place**, even though the inherited role label is "Core/Attacker" rather than an explicit Seed/Catalyst-with-evidence-gate role. This agent flags that WULF's actual risk profile (unresolved counterparty credit, high leverage, pre-revenue on its largest contract) is a closer structural match to a **Seed/Catalyst role with an exact evidence gate** than to an unconditional Core/Attacker label — consistent with the already-open evidence gate's own framing. Role reassignment is Portfolio Court's job, not this agent's.

**Proof gate (from Forward):** CB-4's phased delivery and rent commencement, guided H2 2026 — the nearest-dated, most falsifiable checkpoint of any item across all 8 holdings — followed by CB-5's "early 2027" target and, further out, the late-2027 Anthropic-lease revenue start. TeraWulf's Q3 2026 earnings release (~November 2026) is the next scheduled checkpoint for CB-4 progress specifically. **Separately and more urgently for the credit question**: the next agent/session with SEC.gov and terawulf.com egress access should retry the two blocked primary documents — Industry's own explicit recommendation, reconfirmed here.

**Replacement risk:** This is the clearest replacement-risk case among the 8 holdings. If the Anthropic-credit question resolves unfavorably (or stays unresolved through the next several cycles while leverage and counterparty concentration remain unchanged), capital here would very plausibly be better deployed toward AMKR (profitable, no dilution signal, direct AI-supply-chain beneficiary) or toward closing the IREN financing gap rather than remaining in an unresolved-credit, high-leverage, pre-revenue single-counterparty bet. This agent does not recommend an immediate sell — the evidence gate remains open, not closed negative — but flags WULF as the **highest replacement-risk holding in the portfolio** pending gate resolution.

**Kill conditions:**
- Confirmation (once the blocked documents are readable) that the Anthropic lease's "investment-grade" characterization has **no** valid guarantor or structural credit enhancement behind it — i.e., it rests on Anthropic's own unrated credit alone
- Any signal of stress in Anthropic's own compute-spending pace relative to disclosed revenue (Industry flags ~$130B+ in aggregate commitments against a revenue base not yet demonstrated to sustainably cover that pace) — not a proven risk yet, but a monitorable one
- CB-4 delivery/rent commencement slipping past H2 2026 without a credible revised date
- Any covenant or refinancing stress signal on the $2.5B convertible notes ahead of the 2027 revenue start
- A public S-1/IPO process for Anthropic that reveals financials materially weaker than the reported ~$65B ARR trajectory (itself UNVERIFIED LEAD)

---

## Cross-Holding Summary (Underwriter-level, not Portfolio Court's ranking)

| Ticker | Weight | Raw Convexity (credible regime) | Adjusted Attractiveness | Sizing vs. ~5% draft norm | Replacement Risk |
|---|---|---|---|---|---|
| PLTR | ~35.6% | 3x plausible; 10x not credible | MODERATE-TO-LOW at current weight | ~7x overweight | Low (name); High (excess weight) |
| NVDA | ~29.8% | 3x plausible; 10x+ not credible (scale-capped) | MODERATE-HIGH | ~6x overweight | Low (name); High (excess weight) |
| MSFT | ~9.0% | 3x possible multi-year; 10x+ not credible | MODERATE-HIGH | ~1.8x overweight | Low |
| KO | ~9.0% | 3x not credible; low-convexity compounder | LOW-TO-MODERATE (mandate-fit specific) | ~1.8x overweight | High (mandate-fit question) |
| GOOGL | ~5.8% | 3x plausible multi-year; 10x+ not credible | MODERATE-HIGH | ~in line | Low |
| TSLA | ~5.5% | UNKNOWN pending Optimus verification (theoretical ceiling high, not evidenced) | LOW-TO-MODERATE | ~in line | Moderate |
| IREN | ~2.7% | 3x–5x credible; 10x speculative | LOW-TO-MODERATE (financing gap dominant) | Below norm, above Seed floor | Moderate |
| WULF | ~2.5% | 5x–10x theoretical (small base/large contract) | LOW (unresolved counterparty credit + leverage) | Below norm, above Seed floor | High |

**Note on this summary table:** it restates, side by side, fields already fully labeled and sourced in each Monster File above — it is a navigation aid, not a new analysis, and carries no evidence labels of its own beyond what each row's Monster File already establishes.

---

## What This Run Explicitly Does Not Do
- Does not adjudicate the open `20260902-DAILY-PORTFOLIO-COUNT_OVERAGE` Tribunal (8-vs-7 count, PLTR/NVDA sizing) — flagged and reconfirmed here with independent arithmetic, decision remains Portfolio Court/Orchestrator's.
- Does not close the `20260902-DAILY-WULF_IREN-EVIDENCE_GATE` — Industry's dedicated attempt this run made real progress but was blocked by tooling (egress restrictions), not resolved; this Underwriter pass treats the gate as still open and adjusts WULF's adjusted-attractiveness rating accordingly (LOW), consistent with Burden of Proof.
- Does not reassign role labels (Core/Attacker vs. Seed/Catalyst) — flagged as a mismatch for IREN and WULF specifically, decision remains Portfolio Court's.
- Does not underwrite any Discovery-fresh candidate to full Monster File depth this cycle (time was allocated entirely to the mandatory 8 holdings per task brief); AMKR, MP, ONDS, SNDK carry their own Active Handoff evidence quality already and remain Portfolio Court's queue.
- Does not write to the Master Ledger or Active Handoff Snapshot.

---

## Verdict

`UNDERWRITING = COMPLETE`

All 8 mandatory current holdings received a fresh Monster File testing inclusion, sizing, proof gate, and replacement risk, with raw convexity and evidence/survivability-adjusted attractiveness reported as two separate, clearly labeled fields per spec, and explicit kill conditions listed for each. No figures were fabricated; every number not directly sourced from Forward/Industry/Discovery or computed directly from the Master Ledger's own recorded shares/prices is labeled DATA LIMITED or UNKNOWN. Two structural findings are reconfirmed for Portfolio Court: (1) PLTR and NVDA's combined ~65.4% weight is not justified by the evidence against the ~5% draft Core/Attacker norm — this is a sizing question, not an inclusion question, for both; (2) WULF's adjusted attractiveness is rated LOW this cycle specifically because the Anthropic-credit evidence gate remains open despite a good-faith, tooling-blocked resolution attempt — this should weigh against any sizing increase until the gate closes. No lighter-touch Discovery-candidate Monster Files were produced this cycle; all available effort went to the mandatory 8-holding core per the Deep Audit task brief.
