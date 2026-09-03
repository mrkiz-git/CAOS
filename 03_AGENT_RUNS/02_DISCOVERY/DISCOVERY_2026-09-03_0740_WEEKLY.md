# DISCOVERY RUN — 2026-09-03_0740_WEEKLY

## Inputs Consulted
- [[03_AGENT_RUNS/01_VERIFIER/VERIFIER_2026-09-03_0740_WEEKLY]] — `WEEKLY PRICES VERIFIED | 0 prices confirmed, 9 DATA LIMITED / MARKET CLOSED / NO DATA`; market not yet open, equity-quote WebSearch layer showing staleness/cache artifacts and internal conflicts. No live price denominator available this run.
- Monster Census output: **UNAVAILABLE** — has never run for real (same gap the Verifier flagged). Per the Weekly spec's fallback and this run's brief, the Active Handoff Snapshot is treated as the only prior-tracking source for deduplication, cross-checked against yesterday's real Daily Anchor Discovery output.
- [[02_ACTIVE_HANDOFF/CAOS — ACTIVE HANDOFF SNAPSHOT]] — Challengers: ONDS only. Seeds/Trigger Watches/Hunter Signals: empty.
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — 8 funded holdings: PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF.
- [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_2026-09-02_001]] — yesterday's real Daily Anchor Discovery run, read in full to avoid re-surfacing its 23 tickers as "new": OKLO, SMR (NuScale), ETN, VRT, GEV, PWR, UBTECH (9880.HK), IONQ, RGTI, QBTS, Infleqtion, ONDS, KTOS, AVAV, RXRX, SDGR, ABSI, RLAY, MU, LRCX, TT, PH, AAON.
- WebSearch (this agent's only research access) — 7 queries run across 6 of the 9 lanes this pass, 2026-09-03.

## Search Strategy
- **Scope:** Weekly deep search for new high-asymmetry candidates, lighter pass than yesterday's full Discovery per the Orchestrator's brief — focused on genuinely new names since 2026-09-02, not a repeat sweep.
- **Reuse:** Yesterday's 23-ticker universe (listed above) treated as already-catalogued; not re-surfaced as "new" here even where it re-appeared in today's search results.
- **Novelty filter applied:** candidate must be absent from (a) yesterday's Discovery output, (b) the Active Handoff Snapshot, (c) Master Ledger holdings.
- **Asymmetry gate:** every surfaced candidate must show a plausible upside > downside case vs. holding cash. Given the Verifier's `DATA LIMITED` finding on all 9 tracked tickers this run (market not yet open, aggregator staleness/cache artifacts, internally conflicting reads), **no live price denominator exists for any security today** — this applies equally to new candidates. Asymmetry below is therefore stated qualitatively (thesis-catalyst-based), with any numeric market-cap/price figures explicitly labeled by evidence quality, consistent with the Verifier's Radical Honesty stance this run. No number below is asserted as a verified live quote.
- **Thesis depth:** SEED-level only — market size/funding, one or two near-term catalysts, team/financing sanity check. No full underwriting.

## Lane-by-Lane Search Results

### Lane 1 — Chips & Memory
**New candidate:**
- **SK Hynix (Nasdaq ADR: SKHY)** — South Korea's largest memory maker (HBM leader, ~57–62% HBM market share per secondary reporting) completed a historic $26.5B Nasdaq ADR listing on 2026-07-10, priced at $149/ADR, opening at $170. This closes the exact gap yesterday's Discovery flagged and excluded ("SK Hynix — no clean US-listed common ticker surfaced this pass"). — **VERIFIED FACT** that the listing occurred and priced as described (multiple corroborating sources: Yahoo Finance, CNBC, IPOScoop, SK Hynix's own newsroom); market cap figure (~$843B, one aggregator, 2026-09 read) — **UNVERIFIED LEAD**, single-source, not cross-checked against a primary filing or second aggregator.
- Search terms: "SK Hynix Nasdaq ADS ticker listing 2026"; "'this week' new stock listing AI chip memory HBM September 2026".
- Exclusions: Micron (MU), Lam Research (LRCX) — already in yesterday's Discovery.

### Lane 2 — Inference & Power
No genuinely new name surfaced this pass distinct from yesterday's Eaton/Vertiv/GE Vernova/Quanta Services set. Search terms used ("optical networking semiconductor stock AI data center... 2026") returned optics/photonics names captured under Lane 7 instead (see below) rather than inference-hardware or power-distribution names. **Lane flagged as under-searched this pass** — see Verdict.

### Lane 3 — Defense, Autonomy & Space
**New candidates:**
- **Karman Holdings (NYSE: KRMN)** — hypersonic/missile-defense and space-launch component manufacturer (structures, propulsion components); IPO'd 2025. Market cap ~$8.2B per one secondary source (2026-08-17 read) — **UNVERIFIED LEAD**.
- **Firefly Aerospace (Nasdaq: FLY)** — small/medium launch vehicle and lunar lander company (Blue Ghost lander flown 2025); recent IPO. No independently confirmed market cap this pass — **DATA LIMITED**.
- **AST SpaceMobile (Nasdaq: ASTS)** — space-based direct-to-cellular broadband network; described in one source as "~3x Karman's market cap" (implying roughly $21–24B), not independently confirmed — **UNVERIFIED LEAD**.
- Context (not itself a new candidate, thesis catalyst only): SpaceX's own IPO is reportedly targeted for mid-2026 at a $1.75–2T valuation, which multiple secondary sources cite as the catalyst repricing the entire public launch-infrastructure comp set upward — **UNVERIFIED LEAD**, single-theme secondary reporting, not a candidate itself (SpaceX not yet listed).
- Search terms: "space launch infrastructure stock public company 2026 new listing"; "Karman Holdings KRMN market cap Firefly Aerospace FLY market cap AST SpaceMobile ASTS market cap".
- Exclusions: Ondas (ONDS), Kratos (KTOS), AeroVironment (AVAV) — already tracked/yesterday's Discovery.

### Lane 4 — Quantum
No genuinely new public name surfaced. IonQ's reported SkyWater Technology and Vector Atomic acquisitions (2026) are **UNVERIFIED LEAD** (single-source secondary reporting) and do not create a new standalone public ticker — SkyWater ceases to be independently investable if the acquisition is real. Infleqtion (INFQ) already surfaced in yesterday's Discovery.
- Search terms: "quantum sensing quantum networking stock company 2026 new".
- Exclusions: IonQ, Rigetti, D-Wave, Infleqtion — already in yesterday's Discovery.

### Lane 5 — Advanced Batteries & Materials
**New lane — not covered by yesterday's Daily Anchor Discovery at all.**
**New candidates:**
- **Solid Power (Nasdaq: SLDP)** — solid-state battery electrolyte/technology licensor; three-way partnership with Samsung SDI and BMW (demonstration vehicle, late 2025) is the nearest verified proof point. Market cap ~$1.05B per one secondary source (dated October 2025, i.e. stale even by that source's own timestamp) — **DATA LIMITED**.
- **Solidion Technology (Nasdaq: STI)** — small-cap battery materials/silicon-anode name surfaced in the same search sweep; not independently deep-dived this pass — **UNVERIFIED LEAD**.
- **Factorial Energy** — solid-state battery startup, targeting a mid-2026 SPAC merger with Cartesian Growth Corporation III (ticker to become FAC on Nasdaq), deal values Factorial ~$1.1B with a $100M raise; production target 2027. **Not yet public** — watch-only, same treatment as yesterday's Agility Robotics pre-close flag.
- Search terms: "advanced battery materials stock IPO 2026 solid-state battery public company".
- Exclusions: none from prior lists (lane untouched until this run).

### Lane 6 — Biotech Automation
**New candidates:**
- **Generate Biomedicines (Nasdaq: GENB)** — AI-driven protein-therapeutics design platform with automated laboratory testing; IPO'd 2026-02-27, raised ~$400M at $16/share. — **UNVERIFIED LEAD** (single secondary source, not cross-checked against the S-1/prospectus).
- **Alamar Biosciences** — commercial-stage proteomics tools company (ultra-sensitive protein biomarker detection instruments, used in automated biotech lab workflows); closed an upsized IPO 2026-04, raising ~$219.9M at $17/share. Exact resulting ticker not confirmed this pass — **DATA LIMITED**.
- Search terms: "lab automation robotics biotech stock 2026 IPO synthetic biology".
- Exclusions: Recursion (RXRX), Schrödinger (SDGR), Absci (ABSI), Relay Therapeutics (RLAY) — already in yesterday's Discovery.

### Lane 7 — Networking, Optics, Semiconductors
**New candidates:**
- **Applied Optoelectronics (Nasdaq: AAOI)** — 800G/1.6T optical transceiver maker; completed first volume shipment of 800G products to a hyperscale customer in Q1 2026 per one secondary source — **UNVERIFIED LEAD**.
- **Lumentum (Nasdaq: LITE)** and **Coherent (NYSE: COHR)** — both received a reported $2B direct investment from NVIDIA each (~$4B total) in March 2026, paired with multi-year purchase agreements, per one secondary source citing the deal — **UNVERIFIED LEAD** (large, specific, single-source claim; would be decision-grade if confirmed via primary filing, not yet done this pass).
- **Tower Semiconductor (Nasdaq: TSEM)** — specialty foundry; demonstrated 400Gbps/lane silicon-modulator production process with Coherent, March 2026, per one secondary source and referenced in a Tower 6-K SEC filing link surfaced directly in search results (filing itself not opened/read this pass) — **DATA LIMITED**, primary-source link exists but was not independently pulled and verified this run.
- Search terms: "optical networking semiconductor stock AI data center 800G silicon photonics 2026".
- Exclusions: none from prior lists (lane untouched until this run).

### Lane 8 — Power, Grid, Nuclear & Cooling
No new search run this pass — already deep-covered yesterday (OKLO, SMR/NuScale, ETN, VRT, GEV, PWR, TT, PH, AAON). **Lane deliberately not re-searched this run** per the "lighter pass, avoid re-covering the same ground" brief; flagged in Verdict as intentionally skipped rather than exhausted.

### Lane 9 — Robotics & Physical AI
**New candidate:**
- **Ouster (Nasdaq: OUST)** — digital lidar sensor maker; closed Stereolabs acquisition (adds cameras/AI compute/perception software), combining a bill-of-materials set relevant to humanoid robots and robotaxi platforms. Reported +149.86% YTD, +13.43% on 2026-06-30 per one secondary source — **UNVERIFIED LEAD**, no independent price/market-cap confirmation this pass.
- Context only, not new candidates: Unitree Robotics' Shanghai IPO registration approved (raising ~$618M, ~$5.9B implied valuation) — **foreign listing, not confirmed US-accessible** — excluded, same treatment as yesterday's UBTech (Hong Kong-listed) exclusion logic. Figure AI, Apptronik, 1X, Sanctuary AI — still private, excluded (no ticker).
- Search terms: "robotics physical AI stock news September 2026 humanoid IPO".
- Exclusions: UBTech (9880.HK), Agility Robotics (SPAC merger not independently re-confirmed closed this pass) — already flagged yesterday.

## Candidate Summary Table

| Ticker | Company | Lane | Market Cap / Funding | Upside (%) | Downside (%) | Asymmetry | Thesis Stage | Next Gate | Evidence Quality |
|--------|---------|------|-----|--------|----------|-----------|-----------|----------|-------------------|
| SKHY | SK Hynix (Nasdaq ADR) | Chips & Memory | ~$843B (unverified single-source) | HBM supercycle continuation; direct NVDA/hyperscaler supply exposure at index-scale liquidity | Mega-cap, limited multi-bagger asymmetry; ADR-structure/FX considerations vs. common | Thesis-level only — index-scale name, asymmetry is "safer beta on the bottleneck" not multi-bagger | SEED | Confirm ADR liquidity/structure and first post-listing 10-K-equivalent disclosure via primary source | DATA LIMITED |
| KRMN | Karman Holdings | Defense/Autonomy/Space | ~$8.2B (unverified) | Hypersonic/missile-defense + space-component demand ramp, diversified supplier (not single-program dependent) | Execution/margin risk typical of newly-public defense-supply-chain name; single unverified cap figure | Plausible positive asymmetry, unconfirmed magnitude | SEED | Next quarterly filing confirming backlog/margin trajectory via primary source | UNVERIFIED LEAD |
| FLY | Firefly Aerospace | Defense/Autonomy/Space | Not confirmed this pass | Flown lunar lander (Blue Ghost) proof point; launch-sector re-rating catalyst (SpaceX IPO comp effect) | Small-launch-vehicle sector has high historical failure/cash-burn rate; no cap/financials confirmed | Cannot be assessed — market cap and financing state DATA LIMITED | SEED | Primary-source (10-Q/8-K) pull on cash runway and launch cadence | DATA LIMITED |
| ASTS | AST SpaceMobile | Defense/Autonomy/Space | ~$21–24B (derived, unverified) | Direct-to-cell satellite network, large TAM, multiple carrier partnerships reported | Capital-intensive satellite deployment, dilution risk typical of the sub-sector | Plausible positive asymmetry, unconfirmed magnitude | SEED | Primary-source confirmation of carrier contract terms and financing runway | UNVERIFIED LEAD |
| SLDP | Solid Power | Advanced Batteries & Materials | ~$1.05B (stale, Oct-2025-dated source) | Samsung SDI/BMW demonstration-vehicle partnership is a real near-term proof point | Small-cap, pre-major-revenue, licensing-model dependent on OEM adoption timing | Plausible positive asymmetry, unconfirmed magnitude | SEED | Samsung SDI/BMW demo-vehicle milestone confirmation via primary source | DATA LIMITED |
| STI | Solidion Technology | Advanced Batteries & Materials | Not confirmed this pass | Silicon-anode/battery-materials small-cap, genuinely unexamined name | No financials or cap confirmed this pass — cannot assert asymmetry | Cannot be assessed | SEED | Basic primary-source financial pull before any further step | UNKNOWN |
| GENB | Generate Biomedicines | Biotech Automation | ~$400M raised at IPO (Feb 2026) | AI-driven protein-therapeutics design + automated lab testing, fresh IPO with cash from raise | Pre-revenue biotech, binary clinical/platform-validation risk typical of the sub-sector | Plausible positive asymmetry, unconfirmed magnitude | SEED | First post-IPO quarterly filing confirming cash runway and pipeline progress | UNVERIFIED LEAD |
| ALMR* | Alamar Biosciences | Biotech Automation | ~$219.9M raised at IPO (Apr 2026) | Commercial-stage (not pre-revenue) proteomics instrument maker — more advanced than typical biotech-automation Seed | Small-cap, commercialization-ramp risk | Plausible positive asymmetry, unconfirmed magnitude | SEED | Confirm exact ticker and first commercial-revenue print via primary source | DATA LIMITED |
| AAOI | Applied Optoelectronics | Networking/Optics/Semiconductors | Not confirmed this pass | First 800G hyperscale volume shipment (Q1 2026); direct optical-interconnect-bottleneck exposure | Historically volatile small/mid-cap optics name, execution risk on 1.6T transition | Plausible positive asymmetry, unconfirmed magnitude | SEED | Primary-source confirmation of hyperscale shipment volumes/customer concentration | UNVERIFIED LEAD |
| LITE / COHR | Lumentum / Coherent | Networking/Optics/Semiconductors | Not confirmed this pass | Reported $2B NVIDIA direct investment each + multi-year purchase agreements (Mar 2026) — if confirmed, a decision-grade catalyst | Single-source claim of this magnitude needs primary confirmation before being treated as real | Cannot be fully assessed until the NVIDIA-investment claim is independently confirmed | SEED | Primary-source (8-K/press release) confirmation of the NVIDIA investment terms | UNVERIFIED LEAD |
| OUST | Ouster | Robotics & Physical AI | Not confirmed this pass (reported +149.86% YTD, single source) | Lidar + Stereolabs perception-stack combination fits humanoid/robotaxi bill-of-materials | Small-cap lidar sector has a history of failed/consolidated players; single-source price-performance claim | Plausible positive asymmetry, unconfirmed magnitude | SEED | Primary-source confirmation of Stereolabs integration revenue contribution | UNVERIFIED LEAD |

*Alamar's exact post-IPO ticker was not independently confirmed this pass — flagged for closure before any further step, not asserted as fact.

## Deduplication & Exclusion Log

**Already in yesterday's Daily Anchor Discovery (2026-09-02) — not re-surfaced as new:**
OKLO, SMR (NuScale), ETN, VRT, GEV, PWR, UBTECH (9880.HK), IONQ, RGTI, QBTS, Infleqtion (INFQ), ONDS, KTOS, AVAV, RXRX, SDGR, ABSI, RLAY, MU, LRCX, TT, PH, AAON — all logged in [[03_AGENT_RUNS/02_DISCOVERY/DISCOVERY_2026-09-02_001]], discovery date 2026-09-02.

**Already in Active Handoff Snapshot — not re-surfaced as new:**
ONDS — state HIGH-PRIORITY CHALLENGER per HANDOFF_ID = 20260902-DAILY-ONDS-NEW_CHALLENGER; no recheck warranted this pass, no new evidence found on ONDS specifically this run (out of scope — Discovery does not re-underwrite an existing Challenger).

**Already in Master Ledger (funded holdings) — excluded from "discovery" by design:**
PLTR, NVDA, MSFT, KO, GOOGL, TSLA, IREN, WULF. Per Objective Supremacy and the spec's "No Incumbent Exclusion" clause, this is procedural only — not a statement these positions are validated or protected.

**Names rejected / not carried to the summary table:**
- **Factorial Energy (pending ticker FAC)** — not yet public (SPAC merger targeted mid-2026, not closed); watch-only, same treatment as yesterday's Agility Robotics pre-close exclusion.
- **Unitree Robotics** — Shanghai-listed only (registration approved, ~$618M raise); no confirmed US-accessible listing — excluded, same logic as yesterday's UBTech/SK Hynix (pre-listing) exclusions.
- **SpaceX** — not yet listed (IPO reportedly targeted mid-2026); cited only as a sector re-rating catalyst, not a candidate.
- **Tower Semiconductor (TSEM)** — a primary-source SEC 6-K filing link was surfaced directly in search results but not opened/read this pass; held out of the summary table pending that primary-source pull rather than asserted on secondary-source strength alone.

## Evidence Labeling
Per [[00_START_HERE/CAOS — OPERATOR MANUAL#6. Sources and Evidence]]: `VERIFIED FACT` | `CAOS INFERENCE` | `UNVERIFIED LEAD` | `DATA LIMITED` | `UNKNOWN`. Applied throughout above. No company name, ticker, or financial figure in this report was invented — all sourced from WebSearch results returned this run; every figure not independently cross-checked against a primary filing this pass is labeled `UNVERIFIED LEAD` or `DATA LIMITED`, never asserted as `VERIFIED FACT` unless multiple independent sources corroborated the same discrete fact (applied only to the SK Hynix listing having occurred, per Chips & Memory above).

## Verdict

**Lanes fully searched this pass:** Chips & Memory, Defense/Autonomy/Space, Quantum, Advanced Batteries & Materials, Biotech Automation, Networking/Optics/Semiconductors, Robotics & Physical AI (7 of 9).

**Lanes not searched this pass (intentional, per lighter-weekly-pass brief):**
- **Inference & Power** — attempted, but the search query returned optics/networking results instead of inference-hardware/power-distribution names; no genuinely new candidate confirmed. Should be re-run with a more targeted query before being treated as exhausted.
- **Power, Grid, Nuclear & Cooling** — deliberately not re-searched, having been deep-covered in yesterday's real Daily Anchor Discovery run with no material time elapsed since to expect new entrants; re-searching would have duplicated effort rather than surfaced genuinely new names, contrary to this run's brief.

**New candidates surfaced this run (11):** SKHY, KRMN, FLY, ASTS, SLDP, STI, GENB, Alamar Biosciences (ticker unconfirmed), AAOI, LITE/COHR (paired), OUST — spanning 6 lanes, none overlapping yesterday's 23-ticker universe or the Active Handoff Snapshot.

`DISCOVERY_WEEKLY = SEARCH INCOMPLETE` — Inference & Power lane yielded no confirmed new candidate and warrants a re-run with a better-targeted query; Power/Grid/Nuclear/Cooling was intentionally not re-searched this pass. All other 7 lanes were searched to this run's SEED-level standard. No candidate above should be treated as decision-grade without Underwriter-stage primary-source verification (SEC EDGAR / official IR), consistent with every figure here being labeled `UNVERIFIED LEAD` or `DATA LIMITED` rather than `VERIFIED FACT`.
