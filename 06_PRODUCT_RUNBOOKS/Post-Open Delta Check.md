# CAOS — Post-Open Delta Check

**Command:** `Run CAOS Post-Open Delta Check`
**Status:** NOT YET BUILT
**Default schedule (inactive):** ad hoc, intraday after market open

## What this product will do
Reports only what changed since a completed same-day Daily Anchor. It must state the price denominator it is comparing against and must never impersonate a full Anchor rerun — if no completed same-day Anchor exists, this product cannot run.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#21. Product distinctions]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
