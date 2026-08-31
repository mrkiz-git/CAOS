# CAOS — Event Gate Watch

**Command:** (automated watch — no manual trigger phrase in the source doc)
**Status:** NOT YET BUILT
**Default schedule (inactive):** daily 02:00, Mark's confirmed timezone

## What this product will do
Reads active event gates from the Active Handoff Snapshot and runs a post-event review only after the actual release, filing, presentation, or call material exists — a pre-release Anchor never satisfies a post-results gate. States `TRANSCRIPT PENDING` if a full transcript is unavailable. Includes the permanent NVIDIA gate: whenever NVIDIA publishes new earnings, CFO commentary, 10-Q, call material, or materially updated guidance, reviews Data Center/Hyperscale demand, Blackwell/Vera Rubin ramp, networking/optics/memory, financing constraints, China assumptions, gross margin, forward guidance, and read-through to connected CAOS holdings.

Full requirements: see [[05_ARCHIVE/CAOS_Mark_Independent_Clone_Master_Prompt_v1.0#16. Event Gate Watch]]

## Why this isn't built yet
This build covers only the Daily Anchor pipeline end-to-end. This product reuses the same 9-agent roster, but its own run sequence, checklist, and output format haven't been written yet.
