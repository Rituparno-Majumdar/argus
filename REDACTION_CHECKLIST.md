# Redaction Checklist

This repository describes an architecture *pattern*, generalized from a real running system. Nothing in this checklist is sensitive by itself — publishing this list reveals no secret. What it protects is the boundary between "a pattern anyone can learn from" and "an operational fingerprint of one specific, real deployment."

Before merging any change to this repository — and before this repository's own history was first made public — every item below must be checked:

- [ ] **Real personal names, handles, or emails.** No contributor's or any operator's real name, GitHub handle, or email address appears anywhere, including in commit messages, code comments, or example output. Use "the operator," "you," or a clearly fictional placeholder instead.
- [ ] **Real infrastructure identifiers.** No real VPS hostname, IP address (IPv4 or IPv6), SSH port number, or hosting-provider-plus-plan pairing framed as "this is what we run." Citing a provider's *public market pricing* as a general reference is fine; pairing that provider with "our setup" is not.
- [ ] **Real platform/account IDs.** No real messaging-platform chat/channel IDs, no real knowledge-management-tool database or page IDs, no real API keys, tokens, or webhook URLs — not even expired or rotated ones. Treat every ID as permanently sensitive, not just currently-valid ones.
- [ ] **Real phone numbers.**
- [ ] **Real file paths and repository names from the originating system.** Replace with generic placeholders (`repo-<project-name>`, `/path/to/your/workspace`, etc.) — a literal real path is itself an identifying detail even without a credential attached.
- [ ] **Screenshots, logs, or pasted output.** Any of the above can hide inside a screenshot, a terminal capture, or a pasted error message just as easily as in prose. If an image or log excerpt is ever added to this repo, it gets the same scrutiny as text.
- [ ] **Real financial or account-specific figures.** No real budget amounts, real holding/ticker symbols, or real transaction figures from the originating system's financial-automation use — describe the *pattern* (a cap, a cycle, a protected-item list) without the real numbers behind it.
- [ ] **Git history itself, not just the current file tree.** A value removed from the current version of a file but still present in an earlier commit is still exposed. Sweep the full history (`git log -p`) before any push to a public remote — the current tree being clean is necessary but not sufficient.

## How to actually check this

A literal `grep` for known-sensitive strings across the working tree and `git log -p` catches exact-string leaks. It does **not** catch a paraphrased giveaway — a description specific enough to identify the real system even without repeating a literal value verbatim. Always follow a clean grep with a full, attentive read-through of every changed file before considering a change safe to publish.
