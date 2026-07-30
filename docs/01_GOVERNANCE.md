# Governance

## Decision authority

The Founder (Bode) has final say on every decision, always. This document exists to define what happens *before* something reaches the Founder, not to replace that authority.

## AI platform roles

- **Claude** — Engineering Lead. Repository architecture, implementation, documentation, code quality.
- **ChatGPT** — Chief Systems Architect. Long-term architecture, business strategy, AI system design.
- **OpenClaw agents** — Execution. Run defined tasks against defined contracts once those contracts exist (see 04_ARCHITECTURE_DECISIONS.md for status).

## Conflict resolution

When Claude and ChatGPT disagree on a technical or architectural question: surface both positions plainly to the Founder rather than one platform silently overriding the other's prior work. Neither platform's recommendation is binding on its own — the Founder decides, and that decision becomes the record (an ADR, if it's architecturally significant).

A prior AI-driven change is never self-justifying. "Claude already built it this way" is not a reason to keep something the Founder wants changed.

## Write access

**Reality, stated plainly:** every AI platform working on this repo currently authenticates using the Founder's own GitHub credentials. There is no technical separation between "Bode pushed this" and "an AI pushed this while acting as Bode." Branch protection on `main` exists (requires a pull request) but does not enforce against admin-level access, since enforcing it would also block the Founder's own direct pushes — GitHub has no per-platform identity distinction available here without separate machine accounts, which isn't in place.

**What this means in practice:** the real safeguard is process, not tooling. Every AI platform is expected to:
- State clearly when it's about to push directly to `main` vs. when a decision warrants Founder review first
- Never treat a past session's AI-driven changes as authorization for further changes without the Founder's active engagement in the current session
- Keep `00_PROJECT_STATE.md` and `03_CHANGELOG.md` current enough that a quick glance at commit history catches anything wrong

**Future improvement, not yet built:** separate scoped tokens or machine accounts per platform, so pushes are attributable. Not a current blocker, but worth doing if this repo starts taking automated commits from OpenClaw specifically (see 02_VERSIONING.md and the not-yet-built bootstrap system).

## Standing instruction (applies across all platforms)

At the end of any session with real progress on a tracked BVOS venture, career project, or client project: update `00_PROJECT_STATE.md` to reflect what actually happened, not what was planned. Read that file first at the start of any new session before assuming project state.
