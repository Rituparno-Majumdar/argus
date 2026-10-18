# Budget

All figures below are **list prices gathered via web research in October 2026.** Pricing for AI products moves quickly and sources frequently disagree with each other — confirm every number against the vendor's own current pricing page before budgeting against it. Nothing here should be treated as a quote or a guarantee.

## This architecture's cost

The gateway's own conversational-layer model is listed as its **own explicit line**, separate from the dispatch-fleet worker costs — these are two genuinely different cost axes, not one "the AI" line item, and conflating them hides a real design decision (see [`architecture.md` §11](architecture.md#11-the-gateways-own-model-aggregator-pattern)).

| Component | Minimum | Recommended | Notes |
|---|---|---|---|
| VPS | ~$5–10/mo | $20–40/mo | Ultra-budget/regional providers can go very low but trade off reliability; a mainstream provider (e.g. a well-known European or US VPS host) in the 4–8GB RAM range is the safer baseline for anything you intend to run unattended. |
| Primary coding-CLI seat (review/audit role) | $20/mo | $20–100/mo | The entry-level paid tier of a leading agentic coding CLI is generally sufficient for a single reviewer-role worker; heavier usage tiers scale from there. |
| Secondary coding-CLI seat (build/implementation role) | $0/mo | $0–20/mo | A free individual tier is often genuinely viable for moderate usage; paid tiers only become necessary at high volume. |
| Knowledge-management integration | $0/mo | $0/mo | Free tiers of mainstream knowledge-management tools are typically sufficient for this pattern's usage (a handful of API calls per task, not per-second traffic). |
| Messaging gateway (bot API) | $0/mo | $0/mo | Bot APIs for mainstream messaging platforms are free regardless of volume at this scale. |
| **Gateway's own model-aggregator LLM** (separate axis) | ~$1–5/mo | ~$5–20/mo | Cost-efficient "flash"-tier models via an aggregator typically run on the order of $0.03–0.19 per million input tokens and $0.13–1.13 per million output tokens, depending on exact model choice. At realistic personal conversational volume, this lands in the low single digits of dollars per month; scales up with usage and with choosing a stronger model tier. |
| **Minimum-viable all-in total** | **~$25–35/mo** | **~$50–150/mo** | The minimum column assumes one paid coding-CLI seat, a free second CLI tier, free KM/messaging, and light aggregator usage. The recommended column assumes a mainstream (not ultra-budget) VPS and headroom on CLI usage. |

## Competitor pricing (for comparison only)

| Product | Entry tier | Mid tier | Top tier | Caveats |
|---|---|---|---|---|
| Meta's Muse | Free tier available | ~$10/mo (reported "Premium," proactive goal assistance) | — | The $10/mo figure is reported by third-party sources and is **not confirmed against Meta's own official pricing materials** — verify before relying on it. |
| xAI's Grok Bot (via SuperGrok) | ~$10/mo (SuperGrok Lite — likely insufficient for the always-on-agent feature specifically) | ~$30/mo (standalone SuperGrok) | ~$300/mo list (SuperGrok Heavy; promotional pricing has reportedly dropped this to ~$99/mo for limited windows) | Grok Bot access itself is gated and in beta; sources disagree on exactly which tier unlocks it and tier-to-feature mapping has reportedly shifted during rollout. |
| OpenAI's Dots | ~$100/mo (ChatGPT Pro, minimum tier with access) | ~$100–125/seat/mo (Business Premium — sources conflict on exact figure) | ~$500/mo ("Pro 500" tier — 25x base usage, "ultrafast" inference) | **Unresolved contradiction in public reporting**: some sources state Dots usage is free on top of an eligible plan; others state Dots work draws against the plan's own token/usage allowance. This repo does not resolve that contradiction — confirm directly with OpenAI before assuming either way. |
| Cursor Ultra (closest coding-agent analog, not a full always-on agent) | — | — | ~$200/mo | Included as a secondary reference point specifically for coding-agent capability, not life-admin/goal-carrying. Teams Premium pricing (~$120/seat, reported by only one source) is unconfirmed. |

## A note on comparing these numbers directly

These tables are not an apples-to-apples comparison, and presenting them as one would overstate the case. The competitor products are managed, supported, zero-setup consumer services; this architecture is a self-hosted pattern requiring real technical setup and ongoing operational responsibility. The honest framing of what's actually comparable — and what isn't — is in [`comparison.md`](comparison.md). Read the cost table alongside that document, not in isolation.
