# Forward Expectations — TSLA Emergency Thesis Rerun

**Run type:** Emergency Thesis Rerun (single-ticker, full re-underwriting depth)
**Ticker:** TSLA
**Trigger:** Tesla Cybercab robotaxi launch event, Austin TX, 2026-09-03
**Scope:** TSLA only. This run does not touch any other holding.

## Inputs Consulted
- [[03_AGENT_RUNS/03_FORWARD/_AGENT SPEC — Forward Expectations]] (role spec, followed exactly)
- [[06_PRODUCT_RUNBOOKS/Emergency Thesis Rerun]] (product runbook governing this rerun's scope and output contract)
- [[01_MASTER_LEDGER/CAOS Master Ledger — CANONICAL]] — TSLA current state: funded holding, 1.67642235 shares, cost basis $213.97, marked price $356.00, role CORE/ATTACKER (tentative, pending formal Deep Audit role review)
- [[03_AGENT_RUNS/03_FORWARD/FORWARD_2026-09-03_DEEPAUDIT]] — this morning's Deep Audit Forward run; reused for TSLA's pre-event forward-guidance baseline (Q2 2026 deliveries, FY2026 capex guide, prior Optimus guidance), not re-derived from scratch
- [[03_AGENT_RUNS/03_FORWARD/FORWARD_2026-09-03_DCA]] — this morning's DCA-scoped Forward run, which flagged the Cybercab event as "in progress" and its outcome as not yet reported at that time
- WebSearch, run 2026-09-04 (session date), multiple queries: Cybercab event outcome/recap, pricing, NHTSA/regulatory status, production volume target, geographic expansion, and separately Optimus production status — sources include Motor1, Teslarati, Electrek, Not a Tesla App, Yahoo Finance, Statesman, Motley Fool (fool.com — search-snippet only, direct fetch blocked by network egress proxy), Benzinga, Drive Tesla Canada, TechXplore, InsideEVs, BasenOr, GearMusk, Sunday Guardian Live
- WebFetch attempted on fool.com Cybercab recap article — blocked by network egress proxy (EGRESS_BLOCKED); relied on WebSearch snippets from that and other outlets instead, all cross-checked against multiple independent sources

---

## 1. Cybercab Launch Event — What Actually Happened (2026-09-03, Austin)

Per the Emergency Thesis Rerun runbook, every forward-looking statement the event produced is extracted below, each labeled per the required evidence taxonomy (VERIFIED FACT | CAOS INFERENCE | UNVERIFIED LEAD | DATA LIMITED | UNKNOWN). No figure is fabricated; where sources conflict, the conflict is stated rather than resolved by picking one number.

| Forward-looking statement | Type | Label |
|---|---|---|
| Tesla officially unveiled the production version of the Cybercab in Austin, Texas on 2026-09-03 — its first vehicle purpose-built for autonomy (two-seat, no steering wheel, no pedals), running on Tesla's FSD/AI4 stack | Event occurrence | VERIFIED FACT — corroborated across Motor1, Teslarati, Electrek, Statesman, GearMusk, Sunday Guardian Live, Motley Fool |
| Cybercab is being folded into Tesla's existing commercial Robotaxi service (currently modified Model Y vehicles operating in limited areas of Austin, Dallas, Houston, Miami, Orlando, Tampa), rather than launching as a standalone new service | Commercial rollout mechanism | VERIFIED FACT, multi-source corroborated |
| Reported that ~45 registered Cybercabs in Austin were poised to enter service following the event, with rollout beginning via employee rides before being added to the public Robotaxi app, reportedly "as early as the week following the event" | Commercial rollout timeline | UNVERIFIED LEAD — sourced from single outlets (GearMusk / Statesman-family reporting) without a primary Tesla press release or SEC filing confirming the exact unit count or activation date; treat as reported-but-not-company-confirmed |
| Pricing: Musk has long targeted "less than $30,000" for Cybercab at scale; one outlet reports a "confirmed starting price of $25,000 for fleet operators and individual buyers," while multiple others state final consumer pricing, destination charges, order fees, financing terms, and private-buyer delivery dates were **not yet published** as of the event | Pricing | CONFLICTING — the sub-$30K aspiration is a long-standing management aspiration (not new to this event); the specific "$25,000 confirmed" figure appears in only one source found and is UNVERIFIED LEAD; the absence of a published consumer configurator/pricing page as of 2026-09-03 is itself the more load-bearing, better-corroborated fact — labeled DATA LIMITED on final consumer pricing |
| Regulatory status (NHTSA): as of the event, Tesla has **not** received a formal NHTSA blanket approval/exemption for the Cybercab's controls-free design. NHTSA has proposed streamlining Part 555 exemption timelines and a rule change that would remove the manual-brake-pedal requirement for FSD-exclusive vehicles, and a NHTSA spokesperson told Reuters the agency "is in contact with Tesla and is evaluating the situation." Tesla separately holds an EPA Certificate of Conformity for the 2026 Cybercab (an emissions classification, not a safety/autonomy approval) | Regulatory status | VERIFIED FACT that full NHTSA approval/exemption has **not** been granted as of the event — this is an open regulatory question, not a closed one. CAOS INFERENCE: the rulemaking trajectory (proposed brake-pedal rule change, streamlined Part 555 process) is directionally favorable to Tesla but is a pending/proposed rule, not an issued approval |
| Production volume target: one source ("2 million units annually") reported as a production-target figure attached to the Cybercab launch | Production volume target | UNVERIFIED LEAD — this figure appeared in only one search result (Tesorb "Cybercab Tracker") without corroboration from Reuters, Electrek, Teslarati, or a Tesla primary source; do not treat as company-confirmed guidance. Separately, "volume production" of Cybercab (and Tesla Semi) "this year" (2026) was reiterated as a target, consistent with prior guidance, not a new commitment |
| Geographic expansion: Cybercab availability is limited to parts of Austin at launch; Tesla has stated availability "will expand in the future" but has **not** given a definitive nationwide rollout date. A public beta for Cybercab-specific ride-hailing in additional cities (Austin plus possibly Las Vegas) is reported as targeted for "late Q3 or early Q4 2026" | Geographic expansion plans | Austin-only-at-launch = VERIFIED FACT; "will expand, no date given" = VERIFIED FACT (an explicit non-commitment); the Las Vegas/multi-city beta timing = UNVERIFIED LEAD, single-source, not attributed to a Tesla primary statement |
| Musk reiterated the long-standing "before 2027" / "2026" production-scale aspiration for Cybercab first stated at the 2024 unveiling | Timeline reiteration | CAOS INFERENCE — this is a restated management aspiration, not a new binding commitment; flagged explicitly per the Forward spec's requirement to distinguish aspiration from commitment |
| Whether the event included any live malfunction, delay announcement, analyst Q&A content, or other event-specific news beyond what pre/post-event press coverage captured | Event content beyond press recap | DATA LIMITED — this agent has no live/streaming access to the event itself and relied entirely on post-event secondary press coverage; a materially different picture could exist in primary transcript/8-K filings not yet indexed by WebSearch at time of this run |

**Net assessment against the Emergency Thesis Rerun's four named questions:**
- **Commercial rollout timeline** — a rollout into the existing Austin Robotaxi service is underway/imminent (employee rides → app addition), but the exact activation date and unit count are UNVERIFIED LEAD, not company-confirmed.
- **Pricing** — no finalized, published consumer price as of the event; the sub-$30K target is a reiterated aspiration, not new information from this event.
- **Regulatory status (NHTSA)** — **not yet approved**; an open, pending regulatory question with a directionally favorable but unfinished rulemaking track. This is the most consequential unresolved forward item from the event.
- **Production volume targets** — no well-corroborated new figure; the one volume figure found (2M/yr) is single-sourced and not treated as verified guidance.
- **Geographic expansion** — Austin-only at launch, explicit "will expand, no date" statement; any multi-city beta timing is unverified.

---

## 2. Optimus Humanoid-Robot Production Status — Separate Open Evidence Gate

| Statement | Type | Label |
|---|---|---|
| As of Tesla's Q2 2026 shareholder update (2026-07-22, predates today's event and predates this morning's earlier runs), Model S/X production at Fremont had ended and the line was being physically converted to first-generation Optimus manufacturing lines | Trailing/context fact | VERIFIED FACT (per company shareholder update, cited via Electrek) |
| The specific "late July/August 2026" Optimus production-start date given on the Q1 2026 earnings call was **superseded** by Tesla's own Q2 update, which restated the timeline as the vaguer "anticipated later this year" (2026) | Management aspiration — schedule slip acknowledged by the company itself | VERIFIED FACT that the original date was **not met on schedule** and was replaced with a looser target; CAOS INFERENCE that this constitutes a confirmed slip, not merely an unconfirmed one as this morning's Deep Audit run had flagged |
| Musk has separately stated that initial Optimus output will be "quite slow" and called production-rate prediction "literally impossible" this year, citing ~10,000 unique parts on an entirely new line | Management aspiration / risk caveat | CAOS INFERENCE — management itself is signaling low confidence in near-term Optimus volume, reinforcing rather than resolving the open evidence gate |
| First external/commercial Optimus customers are targeted for "late 2026"; a dedicated 5.2M sq ft Optimus factory at Giga Texas North Campus ($5–10B investment) is targeted for ~10M units/year capacity with production "expected summer 2027" | Nonbinding target / management aspiration, long-dated | CAOS INFERENCE — a capacity target three-plus quarters out, unverified against any binding contract or filing |
| No new statement was found, as of this search, giving a confirmed Optimus production **start date that has actually occurred** (i.e., no verification that Optimus units are now rolling off the Fremont line) | Absence of confirming evidence | DATA LIMITED — this agent's WebSearch access did not surface a primary-source (10-Q, 8-K, or on-the-record company statement) confirming Optimus production has begun as of 2026-09-03/04; the most recent company-level statement found is the 2026-07-22 Q2 shareholder update's "later this year" language |

**Net assessment:** Since this morning's earlier runs, there is no new Tesla statement found that resolves the Optimus evidence gate. What has changed is that the July/August 2026 date cited in this morning's Deep Audit run as "unverified whether it happened on schedule" is now better characterized as **verified-slipped** — Tesla's own Q2 update replaced that date with the vaguer "later this year" before the date arrived, which is itself evidence the original schedule was not met, independent of whether Optimus production has since started under the new looser target. The evidence gate (`20260903-DEEPAUDIT-TSLA-EVIDENCE_GATE` per the Active Handoff Snapshot) remains open.

---

## Next Falsifiable Proof Points (TSLA)

1. **Cybercab commercial rollout:** confirmation via Tesla's own Robotaxi app, an SEC filing, or an on-the-record Tesla statement that Cybercabs are live for public (non-employee) rides in Austin, with an actual date — tests whether the "week following the event" reporting was accurate.
2. **NHTSA regulatory status:** any NHTSA ruling, exemption grant, or finalized brake-pedal rule change (public comment period referenced as closing around 2026-07-27) — tests whether Cybercab's controls-free design gets a clear federal path or remains an open compliance question.
3. **Consumer pricing:** publication of an actual Tesla configurator page or press release with confirmed price, fees, and delivery timing for individual buyers — tests whether the sub-$30K (or reported $25K) figures become real, orderable prices.
4. **Optimus production start:** a Tesla-issued statement (earnings call, 8-K, or shareholder update) confirming Optimus units have actually begun rolling off the converted Fremont line under the "later this year" target — the next scheduled Tesla disclosure event for this is the Q3 2026 earnings call/shareholder update, expected ~October 2026.

---

## Constraints Observed
- No sizing, ranking, valuation, or Master Ledger writes performed — this is Forward Expectations' scope only, per the Emergency Thesis Rerun runbook (Verifier, Underwriter, Risk, Portfolio Court, and Orchestrator steps are separate agent calls not performed here).
- Every figure above is attributed to a cited outlet; single-sourced figures are explicitly flagged as UNVERIFIED LEAD rather than presented as confirmed.
- No management aspiration (sub-$30K pricing, "later this year" Optimus, "before 2027" Cybercab scale) is presented as a binding commitment.

---

**FORWARD REVIEW = COMPLETE**
