# Contributing to Argus

Argus is a documentation-only architecture pattern, not a codebase. Contributions here are changes to the *written description* of the pattern — clarifications, corrected pricing, a better-explained rationale for a design decision, a new generalized pattern worth adding.

## Before you open a pull request

- **Read [`REDACTION_CHECKLIST.md`](REDACTION_CHECKLIST.md) and apply it to your own diff.** This is the one hard rule of this repository: no real operator-identifying data, ever — not a real name, not a real hostname or IP, not a real account ID, not a real credential, not a real screenshot or log excerpt. Every example value in this repo is a placeholder pattern. If your contribution is based on your own real running system, genericize it the same way the rest of this repo already has been before submitting.
- Keep additions in the same register as the existing docs: describe the *pattern*, not a specific deployment. "A monitoring daemon runs many concurrent loops" is in scope; "my-server-01 runs these exact 14 cron jobs" is not.
- If you're proposing a new pattern (a new section for `architecture.md`, a new phase for `interview.md`), explain the problem it solves and why the boundary or design choice exists — not just what it does.
- Pricing in `budget.md` goes stale quickly. If you're correcting a figure, cite where you got the updated number and when.

## Pull request etiquette

- One topic per PR — a pricing correction and a new architecture section are two PRs, not one.
- Describe what changed and why in the PR description, not just in the diff.
- Expect a redaction-focused review pass on every PR before merge, regardless of how small the change looks.
