# Changelog

All notable changes to Project Zero itself (the engineering foundation, not the products built on it) are recorded here.

## [v0.9-foundation-complete] — 2026-07-30

### Added
- `01_GOVERNANCE.md` — decision authority, AI platform roles, conflict resolution, honest documentation of the write-access reality (all platforms currently authenticate as the Founder), standing cross-platform instruction
- `02_VERSIONING.md` — milestone-based versioning scheme for Project Zero itself
- `03_CHANGELOG.md` — this file
- `05_SECURITY_STANDARDS.md` — secrets handling standard
- `06_TESTING_STANDARD.md` — minimal verification standard for current no-automated-tests reality

### Changed
- `00_PROJECT_STATE.md` — updated to reflect Colburn Auctions no longer blocked (site live, admin dashboard live, domain crisis resolved), LinkedIn work started, and the transition into Implementation Mode
- `04_ARCHITECTURE_DECISIONS.md` — added an index table at the top for scannability as ADR count grows

### Decided
- Architecture discussions pause here unless a real problem surfaces during building — decision made by the Founder after a Claude engineering assessment identified two maturity estimates worth adjusting (Phase 2 architecture down to ~70-75%, Phase 7 AI Agency up to ~35-40%) and one sprint-order change (split foundation docs into "build now" vs. "defer until agents exist to build contracts against")
- Agent Builder removed from the near-term OpenClaw build plan — build individual agents first, generalize into a builder once real patterns exist across them
- Success now measured by working software, working automations, completed repositories, landed clients, and landed jobs — not by architecture elegance

## [Unreleased]
- Session 2: Career Engine completion (GitHub, cybersecurity repos, LinkedIn, resume, portfolio)
- Session 3: Documentation System (not a Documentation Agent — generates docs, updates PROJECT_STATE/CHANGELOG/ADRs, organizes repos)
- Session 4: OpenClaw Core (Agent Contract, Prompt Contract, Memory Contract — defined against real agents, not speculatively)
