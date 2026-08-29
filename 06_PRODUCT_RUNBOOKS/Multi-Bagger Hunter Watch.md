# MARK CAOS — Multi-Bagger Hunter Watch

**Command:** `MARK CAOS Multi-Bagger Hunter Watch` (background watch, no manual trigger phrase in the source doc)
**Status:** NOT YET BUILT
**Default schedule (inactive):** daily condition watch, at most hourly

## What this product will do
Watches credible long-duration external sources (Motley Fool Stock Advisor/Rule Breakers/high-conviction lists, Seeking Alpha Alpha Picks/high-confidence Quant ideas, IBD 50 changes/Stock of the Day, notable TipRanks elite-analyst signals, and other sources Mark later admits) for materially new or changed signals. Deduplicates on SOURCE + TICKER + RECOMMENDATION_OR_CHANGE_DATE. Every qualified signal must independently verify the underlying company evidence and resolve to High-Priority Challenger, Challenger, trigger-gated Watch, or Reject — external sources are scouts only, never authority.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#13. External Multi-Bagger Hunter Watch]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
