# Versioning

## How Project Zero itself is versioned

Project Zero uses milestone-based versioning, not strict semver — the milestones represent maturity stages, not API compatibility.

- **v0.x** — Foundation stage. Documentation, governance, and standards exist; implementation artifacts (bootstrap system, agent/prompt/memory contracts) do not yet.
- **v1.0** — Full foundation complete: everything in v0.x, plus a working bootstrap mechanism and defined agent/prompt/memory contracts, reached once real agents exist to build those contracts against.
- **v1.x and beyond** — Incremental additions to the foundation as new capabilities (Documentation System, OpenClaw Core, Agency System) reveal what the foundation actually needs.

Each milestone gets a git tag on `main` (e.g. `v0.9-foundation-complete`) and a corresponding entry in `03_CHANGELOG.md`.

## How downstream repos will reference Project Zero (not yet built)

This is aspirational until the bootstrap mechanism exists — recorded here so the intent isn't lost:

A downstream repo (a venture, a client project, an agent) should be able to state which Project Zero version it was set up against, so that when Project Zero's standards change, it's possible to tell which repos are stale. Likely mechanism: a `PROJECT_ZERO_VERSION` marker file or a line in each downstream repo's own state doc, checked manually until automation exists.

## What NOT to version this way

Client-facing products (e.g. the Colburn Auctions site) have their own deployment/release cadence tied to Vercel deployments, not to Project Zero's version. Don't conflate the two — Project Zero versions the *engineering foundation*, not the products built on it.
