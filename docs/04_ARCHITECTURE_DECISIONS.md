# Architecture Decision Records

## Index

| # | Title | Status |
|---|---|---|
| 001 | GitHub as the single engineering repository | Accepted |
| 002 | Public professional identity | Accepted |
| 003 | Medium-sized BVOS agent org (15 agents), department-based | Accepted, in progress |
| 004 | No automated job-application submission | Accepted, permanent |

---

## ADR-001: GitHub as the single engineering repository

**Decision**: Project Zero (this repo) is the source of truth for documentation, architecture, decisions, and roadmap - not ChatGPT, not Claude, not Google Drive.

**Reason**: Version control, backup, accessible from anywhere, readable by AI agents, automatable, professional practice.

**Status**: Accepted

---

## ADR-002: Public professional identity

**Decision**: Use "Bode N. Ayansina" as the public/professional brand across platforms (GitHub, LinkedIn, website, content). Legal name "Nurudeen Bode Ayansina" stays on legal documents, resumes, and anything tied to formal hiring.

**Reason**: Memorable, globally pronounceable, consistent across platforms, flexible enough to support evolution from IT/cybersecurity professional to founder without requiring a future rebrand. No conflict with hiring since name-matching only matters at the legal/background-check stage, not at resume-review stage.

**Status**: Accepted

---

## ADR-003: Medium-sized BVOS agent org (15 agents), department-based not venture-based

**Decision**: Agents belong to shared departments (Executive, Research, Product, Engineering, Security, Growth, Finance, Knowledge) that serve any venture, rather than each venture getting its own dedicated agents. New ventures register into a Venture Registry rather than triggering new agent builds.

**Reason**: Avoids agent-count explosion as the venture list grows, keeps context/token usage sane, matches how real venture studios and consulting firms operate (shared departments serving multiple business lines).

**Status**: Accepted, in progress

---

## ADR-004: No automated job-application submission

**Decision**: Career Ops automation (job discovery, scoring, resume/cover letter tailoring) stops at preparing the application. The final submit action on any job platform is always a manual, human action.

**Reason**: Every major job platform (Indeed, LinkedIn, Workday, Greenhouse, etc.) treats automated form submission as bot activity and risks banning the account. This is a hard constraint, not a preference - the automation's value is in discovery and tailoring speed, not in removing the human click.

**Status**: Accepted, permanent
