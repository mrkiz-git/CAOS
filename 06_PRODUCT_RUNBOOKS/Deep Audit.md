# MARK CAOS — Deep Audit

**Command:** `Run MARK CAOS Deep Audit`
**Status:** NOT YET BUILT
**Default schedule (inactive):** manual only

## What this product will do
Rebuilds the portfolio from 100% cash without anchoring on existing holdings, re-underwrites the mandate, market regime, holdings, Seeds, Challengers, and cash, runs the full multi-agent pipeline, tests every funded position for inclusion/sizing role/proof gate/replacement, and produces a complete next-euro capital map. It also audits the Master Ledger itself — reconciling it against the freshest broker state, checking every required section, and finding missing logs, duplicates, or contradictions. Creates the monthly [[04_FLIGHT_RECORDER/README — Flight Recorder]] entry after Mark reviews the result.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#18. Manual Deep Audit]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
