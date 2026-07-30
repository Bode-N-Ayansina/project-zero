# Testing Standard

## Current reality

There is no automated test suite anywhere in this ecosystem yet — not for the Colburn Auctions site, not for the Career Ops n8n workflows, not for anything else. Writing this as though comprehensive automated testing already exists would make this document dishonest. This standard describes the minimum real verification that should happen before calling something "done," until automated testing is actually built.

## Minimum verification before marking something done

1. **For a UI change (site, admin dashboard):** actually load the page and look at it — screenshot or live check — before saying it's fixed. Multiple sessions on Colburn Auctions caught real bugs (broken publish-button UI state, HEIC images not rendering, nav links not working off the homepage) specifically because the change was checked against the live site rather than assumed correct from the code diff alone.
2. **For a database/backend change:** query the actual data after the change to confirm it did what was intended, not just that the query ran without error.
3. **For an automation (n8n workflow, agent task):** run it once manually end-to-end and confirm the real output (a Telegram message arrived, a row appeared in the sheet, a file landed where expected) before considering it live.
4. **For anything touching money, credentials, or a client-facing deliverable:** get explicit confirmation before proceeding, don't assume a prior step succeeded silently.

## Why this matters more than it might seem

Several real bugs this project has already hit (the publish button not updating its UI despite the backend action succeeding; the "Colburn Auction" singular slipping back into the hero heading after being fixed elsewhere; nav links breaking off the homepage) were exactly the kind of thing a "looks right in the code" check would have missed and only a real load-and-look check caught. This standard exists because that pattern already happened, repeatedly, not because it might happen someday.

## What's explicitly out of scope for now

Formal automated test suites (unit, integration, end-to-end) — worth building once a given system (the Colburn platform, an OpenClaw agent) is stable enough that regressions become a real risk, not while it's still actively being built out feature by feature.
