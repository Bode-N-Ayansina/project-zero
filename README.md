# Project Zero

Single source of truth for BVOS (Bode Venture Operating System) - the founder's operating framework, spanning career, agency, and venture systems.

This repo exists so that ChatGPT, Claude, and OpenClaw agents can all work from the same understanding of current state, decisions made, and what's next - instead of context living separately in three different chat histories.

## Structure

- `docs/00_PROJECT_STATE.md` - current status, what's done, what's active, what's next
- `docs/01_PROJECT_CHARTER.md` - mission, vision, founder role, success definition
- `docs/03_BRAND_STRATEGY.md` - identity, naming, positioning across platforms
- `docs/04_ARCHITECTURE_DECISIONS.md` - ADR log, one entry per major decision
- `docs/05_ROADMAP.md` - phased plan
- `docs/06_SESSION_HANDOFF.md` - what to read first when picking this up in a new session

## How to use this repo

At the start of any session with any AI tool, point it to `docs/06_SESSION_HANDOFF.md` first. That file tells it what's current and where to look next.

After any session that produces a decision, a built system, or a plan change - update the relevant doc before the session ends. Nothing important should stay trapped inside a single chat.
