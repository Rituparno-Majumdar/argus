# Changelog

All notable changes to the Argus architecture guide are documented here.
Format loosely follows [Keep a Changelog](https://keepachangelog.com/), with
versions `MAJOR.MINOR.PATCH`: PATCH for wording/accuracy fixes, MINOR for a
new or materially changed pattern, MAJOR for a structural rework of the guide
itself.

## [1.1.0] - 2026-10-18

### Added
- `docs/architecture.md` §12 — a new subsection, "Keeping this guide itself
  current," describing the versioned, draft-only sync hook that watches the
  weekly self-improvement cycle (and manual architectural work outside it)
  and drafts scoped doc updates plus a changelog version bump on a local
  branch, gated behind a single operator approval card before anything is
  published.

## [1.0.0] - 2026-10-18

Initial public release.

### Added
- `README.md` — pitch, cover image, architecture diagram, naming rationale
  ("Why Argus?"), table of contents, honesty section on what this is not.
- `docs/architecture.md` — the comprehensive, integrated architecture guide:
  gateway/dispatch split, on-demand ephemeral execution fleet, consolidated
  monitoring daemon, approval-card system, dual-tier memory, knowledge-vault
  integration, scheduled digests, multi-repo git hygiene, the gateway's own
  model-aggregator pattern, the weekly self-improvement cycle, the
  goal-carrying/life-admin pattern, and the generalized financial-automation
  pattern.
- `docs/interview.md` — the 8-phase interview document meant to be handed to
  any agentic coding CLI, so a reader can be interviewed about their own
  setup before scaffolding an equivalent system.
- `docs/budget.md` — sourced minimum-budget breakdown, with the gateway's own
  conversational-model cost broken out as its own line.
- `docs/comparison.md` — an honest capability comparison against Muse, Grok
  Bot, Dots, and Cursor Ultra, including where those products win outright.
- `docs/assets/argus-cover.png` — original cover art ("Panoptic Field").
- `LICENSE` (MIT), `CONTRIBUTING.md`, `REDACTION_CHECKLIST.md`.
