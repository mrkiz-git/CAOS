# CAOS — DCA Execution Card

**Command:** `Prepare CAOS DCA Execution Card`
**Status:** NOT YET BUILT
**Default schedule (inactive):** shortly after Mark's confirmed monthly contribution date, once task capacity permits; otherwise manual whenever new cash is available

## What this product will do
Given a confirmed broker screenshot/export, real unlevered cash by currency, recent fills, and current verified prices, it reconciles the portfolio, checks market temperature and event risk, checks thesis integrity for every funded position, ranks the next uncommitted euro, and selects one or two targets (or a Mark-authorized basket) with exact executable sizing only when every execution gate passes. It states `DO NOTHING / HOLD CASH` when no candidate clears the minimum edge, and is never automatic equal feeding just because the calendar says DCA day.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#17A. DCA Execution Card]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
