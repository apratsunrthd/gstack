# This fork

This is a personalized fork of [garrytan/gstack](https://github.com/garrytan/gstack). Everything below this point is my own customization on top of upstream, not part of Garry's original project — see the [README](../README.md) for that.

The goal was simple: make gstack run on a Karpathian standard — code minimalism, deliberate agent autonomy, building to understand rather than trusting the surface, and English-as-spec discipline — and make those standards durable rules in `CLAUDE.md` rather than one-off habits that don't survive a new session.

## What's different from upstream

All of it lives in [`CLAUDE.md`](../CLAUDE.md), plus two small code changes. In the order a reader would hit them in the file:

- **Karpathian engineering principles** — four standing rules: code minimalism and hackability (resist premature abstraction, delete aggressively), agent autonomy discipline (read every AI-authored diff before calling it done, verify consequential decisions explicitly instead of assuming), first-principles/build-to-understand (folded into the pre-existing "Search before building" section rather than duplicated), and English-as-code/spec-first (state intent before touching code).
- **Project intake protocol** — before starting non-trivial work: interview for the real goal behind the request (not just its literal words), define precise task-specific success criteria and match a past example's format when one exists in the repo, and bias toward small, independently shippable specs over one sprawling one.
- **Repo definition of done** — a 9-point checklist for calling a change finished: matches the interviewed intent, passes the automated test gates, holds up under Karpathian minimalism, key decisions were verified not inferred, clean at every redaction/egress sink, commits are bisected, CHANGELOG/VERSION scaled correctly, no hardcoded platform assumptions, and complex builds (MINOR/MAJOR-scale) get a second system's agreement via `/codex review` before shipping.
- **Gap audit protocol** — a reusable methodology for auditing this file's own coherence: check whether what CLAUDE.md mandates is actually enforced anywhere (a skill, a test, a hook) or just prose a session might skip, report gaps as file/problem/fix, and separately flag which risky actions rely on model compliance alone rather than a hook.
- **`/careful`'s destructive-command hook is now always on** — it used to only run when `/careful` or `/guard` was explicitly invoked that session. A new `.claude/settings.json` wires the same `PreToolUse` hook to run on every Bash call in this repo by default.
- **`careful/bin/check-careful.sh` covers two more bypasses** — `git commit`/`push --no-verify`/`--no-gpg-sign` and `GSTACK_REDACT_PREPUSH=skip`, the two ways CLAUDE.md's own redaction-guard section says the guard gets bypassed that the hook didn't check for.
- **README install instructions point at this fork** — all three `git clone` commands (Claude Code, OpenClaw, other agents) now clone `apratsunrthd/gstack` instead of upstream `garrytan/gstack`, with a callout at the top of the Install section explaining the swap and how to get stock upstream instead.
- **Standing commit + PR policy** — material changes in this repo, or any repo with a GitHub remote, always get committed to a non-main branch and shipped via a PR automatically, never committed straight to `main`. Mirrored into the global `~/.claude/CLAUDE.md` (plus a Stop-hook backstop at `~/.claude/hooks/no-commits-on-main.sh`) so it applies outside this repo too — this section is the tracked, in-repo record of that decision.

## PR log

| PR | What it did |
|----|-------------|
| [#1](https://github.com/apratsunrthd/gstack/pull/1) | Added the Karpathian engineering principles section |
| [#2](https://github.com/apratsunrthd/gstack/pull/2) | Folded the project intake rules into the Karpathian section instead of a separate header |
| [#3](https://github.com/apratsunrthd/gstack/pull/3) | Added the definition-of-done checklist |
| [#4](https://github.com/apratsunrthd/gstack/pull/4) | Added the `/codex review` gate for complex (MINOR/MAJOR-scale) builds |
| [#5](https://github.com/apratsunrthd/gstack/pull/5) | Added precise success criteria + past-example matching to project intake |
| [#6](https://github.com/apratsunrthd/gstack/pull/6) | Added the Gap audit protocol |
| [#7](https://github.com/apratsunrthd/gstack/pull/7) | Three fixes found by running that protocol: renamed the definition-of-done section to stop colliding with `/spec`'s own "Definition of Done" field, closed the two redaction-bypass gaps in `check-careful.sh`, and made the destructive-command hook always-on for this repo |
| [#8](https://github.com/apratsunrthd/gstack/pull/8) | Added this catalog (`docs/FORK_CHANGES.md`) and a banner in README.md pointing to it |
| [#9](https://github.com/apratsunrthd/gstack/pull/9) | Repointed README's install instructions at this fork instead of upstream |
| [#10](https://github.com/apratsunrthd/gstack/pull/10) | Added the standing commit + PR policy (branch → commit → PR, never straight to `main`) |

All merged directly to this fork's `main` — none of it went upstream to `garrytan/gstack`.
