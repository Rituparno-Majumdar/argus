# The Argus Interview

**This document is addressed to you, the coding CLI.** Someone forked the Argus repository and handed you this file because they want to build their own instance of the fleet architecture described in [`architecture.md`](architecture.md). Your job right now is not to start building — it's to interview them, in the eight phases below, before you write or scaffold a single file.

## Operating instructions — read these before Phase 0

1. **Ask one phase at a time.** Do not batch all eight phases into a single wall of questions. Present a phase, wait for answers, confirm your understanding, then move to the next.
2. **Never assume a default for an unanswered question.** If something is skipped or unclear, ask again. A half-answered autonomy question is exactly the kind of gap that causes real harm later — this is not the place to be efficient at the expense of being correct.
3. **Offer the example options given below, but accept free-form answers.** The options are there to make the question concrete, not to limit the real answer.
4. **Restate what you captured after each phase**, briefly, before moving on — a short "here's what I've got so far" so the person can correct you before you're three phases deeper.
5. **Never write a real secret, token, or credential into any scaffolded file.** Only placeholders and `.env.example`-style entries. If they paste a real API key into the chat, acknowledge it was received, but never echo it back into a file you write.
6. **End with one consolidated Profile Summary** (format given at the end of this document) and get explicit confirmation on it before scaffolding anything.
7. If, partway through, their answers reveal they don't actually have what Phase 0 requires, **say so plainly and suggest a smaller starting point** rather than plowing ahead into a build they're not ready to operate.

---

## Phase 0 — Readiness gate

Before anything else, find out if they're actually set up to run this:

- Do you have root or sudo access on a machine that stays on persistently — not a laptop that sleeps or a free-tier container that gets reclaimed?
- Are you comfortable with the basics of systemd services, cron jobs, and git from the command line? (You don't need to be an expert — but if none of this is familiar, say so.)
- Are you prepared to create, store, and rotate several API keys and account credentials, and to keep them out of version control?

If any answer is genuinely "no," don't talk them out of it, but be direct: suggest starting with just the gateway and a single dispatch worker (§1–§2 of `architecture.md`), proving that out, and coming back to the rest later — rather than scaffolding the full fleet for someone who isn't yet set up to operate it.

## Phase 1 — Platform & access inventory

- Which messaging platform do you want as your primary interface? (Telegram, Discord, Slack, iMessage-via-bridge, something else?) Do you want a secondary platform too, or is one enough?
- What timezone and locale should scheduled content use?
- Do you already have a VPS, or do you need to choose one? (If choosing, flag that this feeds directly into Phase 2's budget question — don't make them answer it twice.)
- Which agentic coding CLI(s) do you already hold a seat for, and at what tier? (This determines what's actually available to bind dispatch-fleet roles to.)
- Do you have existing accounts for: a knowledge-management tool (e.g. something Notion-like), a cloud file-sync service, and a model-aggregator service (e.g. something OpenRouter-like)?
- Do you want a dedicated phone/SIM-style channel (an iMessage-bridge-style integration, for instance), or is your chosen messaging platform enough on its own?

## Phase 2 — Budget tier selection (per cost axis, not one number)

Ask these **separately** — a single lump "what's your budget" question hides the fact that this architecture has several independent cost axes:

- **(a) VPS budget comfort**: are you comfortable with an ultra-budget or regional provider (cheaper, less predictable reliability), or do you want a mainstream provider even at a higher price?
- **(b) Coding-CLI seat budget**: free-tier-only, one paid seat, or multiple paid seats across different roles?
- **(c) The gateway's own model-aggregator budget — ask this as its own explicit question, separate from (b).** Which tier of cost-efficient model are you comfortable running the day-to-day conversational layer on? This is a genuinely different cost line from the dispatch-worker models in (b) — see `budget.md` for why.
- **(d) A hard monthly spend-alert threshold?** Do you want the system to flag itself if usage crosses a number you set, and if so, what's that number, in your own currency?

## Phase 3 — Module selection (granular, not one big yes/no)

Walk through each of the following individually — don't bundle them into one "do you want all the advanced stuff?" question:

- **Scheduled digests**: which specific ones do you want, if any? (market/financial briefing, tech-trends digest, career-opportunity matching, portfolio/valuation wrap, something custom?)
- **Monitoring-daemon loop set**: do you want the full set (intrusion defense, dispatch-liveness, cron-failure surfacing, disk hygiene, credit-anomaly watch, external heartbeat), or a reduced subset to start with?
- **Approval-card delivery**: single messaging platform, or multiple?
- **Knowledge-vault integration**: a dedicated tool, or rely on the git-versioned memory archive alone?
- **Financial-automation pattern**: yes or no — and if yes, which real-world domain? (Trading, purchasing, bill-pay, something else entirely — the pattern in `architecture.md` §14 generalizes to any of these.)
- **Goal-carrying / life-admin pattern**: yes or no — and if yes, which connectors specifically? (Email, calendar, browser-automation — ask which ones they actually want wired up, this is not all-or-nothing.)
- **Weekly self-improvement cycle**: yes or no — and if yes, be explicit that this is scoped to infrastructure/security only by design, and confirm they understand it should never be silently widened to their application code.

## Phase 4 — Autonomy posture (per module, AND per action type within it)

For every module they enabled in Phase 3, ask: **report-only, approval-required, or fully autonomous?** And push for a real answer to *why*, the same way this pattern's own operator had to reason about it — what makes this specific domain safely revertible (e.g. everything lives in git history) versus not (e.g. a sent email, a completed purchase, can't be un-sent or un-bought)?

Go deeper for the two domains that need it most:

- **If financial-automation is enabled**: what are the protected/never-touch holdings or actions? What's the per-batch ceiling *and* the per-day ceiling (these should be independent of each other and independent of any higher-level cycle cap)? Is this buy-only, or does it need broader permissions — and if broader, why? What's the kill-switch mechanism, and confirm it works independently of any cron job or code deploy.
- **If life-admin is enabled**: which action types are auto-OK (read-only lookups, drafts that don't send) versus always-gated (sending to an unrecognized recipient, anything with a cost/payment/booking shape)? Confirm they understand *why* this pattern keeps anything cost-shaped button-only and never allows a quick text-reply shortcut for it.

## Phase 5 — Escalation & verification expectations

- Who gets notified when something fails critically, and through what channel — the same one as routine reports, or a separate, higher-urgency one?
- **What is your own plan for verifying each module actually works before you trust it to run unattended?** Push them to answer this concretely — testing each piece in isolation first, watching the first real unattended run start to finish, confirming that a partial failure produces a report rather than silently vanishing. Don't let "I'll just turn it on and see" pass as an answer.

## Phase 6 — Credentials & accounts checklist

Based on everything selected in Phases 1–3, produce a **concrete list** of exactly what they need to go gather before you scaffold anything — for example: a messaging-bot token, a code-hosting account and access token, a knowledge-management-tool API key, cloud-storage credentials, a model-aggregator API key, VPS access credentials, and — only if Phase 3 selected it — a brokerage or other financial-API credential. Tailor this list to what they actually chose; don't hand them a generic checklist with items they didn't select.

## Phase 7 — Naming & branding of their own instance

- What do they want to call their own gateway, their own dispatch fleet, and their own monitoring daemon? Mythological-style names (in the spirit of this pattern's own naming) are one option, but entirely their own naming scheme is equally fine — never suggest reusing any specific real names from the system this pattern was generalized from.
- Confirm they understand that patterns like `repo-<project-name>` in this guide are *naming conventions*, not literal strings to copy verbatim.

---

## End-of-interview output: the Profile Summary

Once all eight phases are complete, produce one consolidated markdown block, in this shape, and get **explicit confirmation** before scaffolding anything:

```markdown
## Argus Profile Summary — <their chosen fleet name>

**Readiness**: <confirmed / flagged concerns>

**Platform & access**
- Primary platform: ...   Secondary: ...
- Timezone/locale: ...
- VPS: <already have / need to choose> — ...
- Coding CLI(s): ...
- Existing accounts: KM tool / file-sync / model-aggregator — ...

**Budget (per axis)**
- VPS tier: ...
- Coding-CLI seats: ...
- Gateway model-aggregator tier: ...
- Spend-alert threshold: ...

**Modules enabled**
- Scheduled digests: ...
- Monitoring-daemon loops: ...
- Approval-card platforms: ...
- Knowledge-vault integration: ...
- Financial-automation: <enabled/domain> or <disabled>
- Goal-carrying/life-admin: <enabled/connectors> or <disabled>
- Weekly self-improvement cycle: <enabled, infra/security-scope-only> or <disabled>

**Autonomy posture**
- <module>: report-only / approval-required / fully autonomous — reasoning: ...
  (repeat per enabled module, and per action type for financial-automation / life-admin)

**Escalation & verification plan**
- Critical-failure notification: ...
- Their stated verification plan before trusting each module unattended: ...

**Credentials checklist**
- [ ] ...
- [ ] ...

**Chosen names**: gateway = ..., dispatch fleet = ..., monitoring daemon = ...
```

Only once this is confirmed, word for word, by the person you're interviewing — proceed to help them design and build their own instance.
