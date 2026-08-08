# Project State

Last updated: August 7, 2026

## Status: Active - Project Zero v0.9 (Foundation Complete), Implementation Mode

Architecture discussions are paused as of this milestone unless a real problem surfaces during building. Success is now measured by working software, working automations, completed repositories, landed clients, and landed jobs — not architecture elegance. See CHANGELOG.md for the full record of this milestone.

## What's actually built and working

**Personal context (new, affects available hours for everything else)**
- Took a temporary full-time painting job at Bombardier aircraft maintenance in Windsor, CT (standard daytime shift, ~7am-3:30pm) while continuing the cybersecurity job search - real income now, changes the daily schedule
- Built a personal routine: workout after work (home equipment), cybersecurity/portfolio study in the evening, weekends for longer lab work
- Finance & habit tracking system built (Google Sheets-style xlsx: income/expenses/investments/weekly review/monthly review/daily habit tracker) - not yet connected to Finance OS (the planned BVOS venture) but conceptually linked; Finance OS automation itself not yet built
- Content pipeline started: a Content Tracker (Google Sheet) exists with real entries (first content piece - a Colburn Auctions case study - drafted in 3 formats: LinkedIn, blog, short caption). Full automated pipeline (Agent 09 auto-logging finished work as content) not yet built, deliberately deferred
- Content creation strategy itself (platforms, cadence, brand direction) explicitly flagged for a dedicated deep-dive session later, not yet planned in detail

**BVOS foundation**
- Company Constitution, 8 departments, 15 agent profiles, 16-venture registry drafted (BVOS Master Blueprint v1)
- OpenClaw running on second PC, 3 agents live (Executive Brain, Client Relations, Automation Engineer), connected via Telegram bot
- MILESTONE: Agent 09 given real, live n8n API access (not just JSON-generation-for-manual-import as originally designed). Verified via a real read-then-write test: listed all 14 workflows on the instance, activated the correct Career Ops workflow (it had never actually been turned on despite being fixed/tested), archived 7 confirmed-duplicate workflows without deleting anything, verified every action with a re-fetch rather than just claiming success. Also confirmed via Agent 09 that the Colburn photo export (see above) was already built and successfully run twice in a separate session. GitHub token and v0.dev API key not yet configured for it.
- Org size: Medium (15 agents) - decided, not fully built out yet

**Career Ops (personal infrastructure, not a venture)**
- Job Discovery Agent: live in n8n, searches 19 categories via Adzuna (IT, cybersecurity, management, AI/automation, general labor, construction), scores by fit and distance, writes to a Google Sheet tracker with dashboard stats
- Dedup working (Append or Update matched on Adzuna ID)
- Security fix applied: the Adzuna app_id/app_key were hardcoded in plaintext in the HTTP node's query parameters (flagged by a note left in the workflow itself) - moved to a proper n8n Custom Auth credential, verified working end-to-end with real live job data
- Google Sheets OAuth credential had expired/been revoked - reconnected, and the append node's column schema (silently dropped during the credential fix) restored - full pipeline (search -> dedupe/filter/score -> write to sheet -> Telegram digest) tested successfully end to end
- Workflow itself was sitting inactive despite being "designed" for daily runs - never actually activated until this session; activation (Publish) still pending a manual approval click in the n8n UI
- In progress: redesigned trigger from a single fixed 7am run to two runs/day (6am, 2pm) gated by a completion check - the afternoon run only fires if every lot/job from the morning batch has been moved off "Ready to Apply" status, with a Telegram skip-notice if not. Adzuna's free tier (~1,000 calls/month, ~33/day; this search uses 19 calls/run) is the hard constraint behind capping it at 2 runs/day rather than something more frequent. New workflow version validated but not yet pushed/tested/activated.
- Master resume built - combined from 11 prior tailored versions into one canonical source
- NOT yet built: Resume/cover letter tailoring agent (blocked on Anthropic API key - key exists from Finance OS project, reusable, just needs wiring in), interview prep agent

**Venture #16 - AI Web & App Agency**
- First live client: Colburn Auctions (colburnauctions.com) - fully live, real content, real client, no longer blocked
- Site: the actual live design is the v0.dev-generated one (auction-house-homepage-design project), rebuilt with Pat's real content (bio, Why Choose Us, Five Steps, Sell With Us with real client stories), no placeholder stats, no personal photo per client request
- Catalog + admin system live: Next.js app connected to a Supabase project (free tier) - `lots` and `lot_photos` tables, RLS policies (public sees published only), storage bucket for photos with automatic HEIC-to-JPEG conversion on upload (client uses an iPad, HEIC is its default format)
- All 272 original catalog lots transcribed and seeded as drafts; client is writing/correcting descriptions and uploading photos himself through the admin dashboard as he goes; "Add New Lot" feature added for items outside the original 272, including photo-only uncatalogued items
- 7+ lots published with real photos so far, catalog page paginated (24/page)
- Live-auction platform confirmed: LiveAuctioneers (per the client's own printed event flyer, now embedded on the site)
- Domain crisis and recovery: colburnauctions.com was suspended by Namecheap for unverified WHOIS contact info (the actual root cause of a site outage that looked like a DNS problem at first) - contact verified, Cloudflare zone rebuilt from scratch (junk NS records from the suspension process removed, A/CNAME records corrected to point at Vercel), Zoho Mail's MX/SPF/DKIM/DMARC records preserved through the rebuild
- Open items: client still confirming ~35 lots with no description sheet on file (lots 1-11, 17-24, 84-88, 94, 132-135, 215-219, 235) and two numbering overlaps (250/251, 264/265); most of the catalog still needs photos uploaded
- UPDATE: client finished writing all 310 lot descriptions (all gaps filled, both numbering overlaps resolved) - loaded into Supabase, titles separated from descriptions, sort order bug fixed (lot_number is text, was sorting alphabetically not numerically)
- Client finished uploading photos for all 310 lots through admin (1,482 individual photos total, confirmed via count)
- LiveAuctioneers catalog spreadsheet (CSV + XLSX, lot number/title/description, all 310 lots correctly ordered) generated and delivered
- DONE (completed in a separate session using a handoff prompt, confirmed via Agent 09 read-only inspection): photo export for LiveAuctioneers. Workflow "Colburn Auctions - LiveAuctioneers Photo Export" (n8n ID 2dvEy2HHfLpTkjBZ) built, tested, and run successfully twice (executions #78 and #80) - all 1,482 photos across 310 lots, batched into 193 zip files, emailed to nurudeenayansina@gmail.com. Structurally complete: manual trigger -> batch descriptor build -> split into batches -> expand to photo URLs -> download -> rename to lot number -> recombine -> zip -> email per batch -> completion summary email.
- PROBLEM FOUND (confirmed via LiveAuctioneers' own docs, fetched directly): the exported photos are named like "1a.jpg" (lot number + letter, no separator) - LiveAuctioneers requires "1-1.jpg" (lot number + hyphen + sequential number) for automatic filename-to-lot matching. Confirmed via the actual batch email body text ("renamed to lot-number format (e.g. 1a.jpg, 12b.jpg)"). Also flagged: LiveAuctioneers caps images at 3840x3840px: iPad photos may exceed this and need resizing, unconfirmed since no tool could open the zips to check actual pixel dimensions directly.
- Two real options identified: (1) rename all 1,482 files to the correct format + resize any oversized images, or (2) skip renaming and add ImageFile.1-20 columns to the catalog spreadsheet listing exact existing filenames per lot (LiveAuctioneers' documented fallback for non-matching filenames)
- IN PROGRESS, INCOMPLETE: gave Agent 09 the rename+resize+re-zip+re-email task (option 1). It started, reported 150/1,482 photos processed with zero failures, then crashed ("something went wrong") and would not recover even via /new retry - looks like the whole OpenClaw session/process may need a manual restart on the PC itself, not just a task-level retry. Confirmed via Gmail search: zero corrected-batch emails were sent before the crash, so nothing was lost/duplicated - safe to restart clean.
- NOT YET DONE: get Agent 09 (or another approach) to actually complete the rename+resize task, or fall back to option 2 (spreadsheet ImageFile columns) if the OpenClaw crash isn't resolved. Also not yet done: the one-batch real-upload test on LiveAuctioneers' actual Confirm screen to verify photo-to-lot matching actually works once corrected files exist.
- LiveAuctioneers seller registration still not submitted (setup details doc already prepared - dates, terms, buyer's premium; bid increments still need Pat's input); call prep doc also prepared

**Career development - LinkedIn**
- LinkedIn optimization content drafted (headline, About, experience rewrites, skills list, Featured section plan) from the latest master resume version
- Not yet applied to the live profile - manual copy-paste, or via Claude in Chrome extension (client was walked through installing it) once set up

## Open decisions

- **Public name/brand**: "Bode N. Ayansina" recommended for GitHub/LinkedIn/public brand, legal name "Nurudeen Bode Ayansina" stays on resumes and official documents. Split adopted, not yet fully applied everywhere.

## Immediate next actions (in priority order)

**Session 2 — Career Engine** (highest priority, directly affects income) — IN PROGRESS
1. Career Ops Agent 1: push/test/activate the gated 2-run/day version (6am + 2pm with completion gate), confirm the Publish approval goes through, verify the gate actually blocks/allows correctly on a real second run
2. Get Anthropic API key wired in -> build Career Ops Agent 2 (resume + cover letter tailoring, pulling from the master resume) - key already exists from Finance OS, reusable
3. Finish priority GitHub cybersecurity portfolio repos
4. Apply the drafted LinkedIn content to the live profile
5. Resume variants and job application workflow

**Session 3 — Documentation System** (not an agent — a system: generates docs, updates PROJECT_STATE/CHANGELOG/ADRs, organizes repos)

**Session 4 — OpenClaw Core** (Agent Contract, Prompt Contract, Memory Contract — defined against real agents now that enough exist to build against, not speculatively)

**Ongoing / not session-bound — TOMORROW'S REAL PRIORITIES**
1. Check Career Ops Agent 1 actually ran at 7am (first time it's ever been genuinely active) - confirm the Telegram digest arrived
   - CONFIRMED: it ran automatically, found 57 real matches. BUG FOUND AND FIXED: the digest message showed "undefined" for every field - the Format Telegram Digest code was reading pre-Google-Sheets field names (title, company, fit_score) but that node runs AFTER the Sheets append step, which renames everything to the actual spreadsheet headers (Job Title, Company, Fit Score). Fixed the code to read the correct field names and extract the raw URL out of the Apply Link HYPERLINK formula. Tested with a real execution - digest now shows real job titles, companies, salaries, working apply links, correctly sorted by fit score. Live for tomorrow's 7am run automatically.
2. Check whether Agent 09 / OpenClaw recovered on its own overnight, or manually restart the OpenClaw process on the second PC if it's still stuck erroring on every message. Once it's responsive, re-send the photo rename+resize task (full task text saved as agent09-photo-fix-task.md in this session's outputs) - this time ask it to work in chunks (~20 zip batches at a time) with progress updates between chunks, since processing all 1,482 photos in one continuous run may be what caused the crash
3. Once corrected photo batches actually arrive by email, do the one-batch real-upload test on LiveAuctioneers' Confirm screen before trusting all 193 batches - that's the only real proof the filename fix worked
4. Finish the LiveAuctioneers seller registration (setup + call-prep docs already exist, only bid increments still open)
5. Check lot 46 on the live site now that the Vercel image-quota bug is fixed - confirm if it's really the wrong photo or was a display artifact
6. Finish giving Agent 09 real access: GitHub fine-grained token (scoped, not broad) and v0.dev API key, same careful pattern as the n8n key
7. Capture real screenshots for the drafted Colburn content pieces (homepage hero, admin dashboard) and post the two "Ready to Post" pieces from the Content Tracker
- Update this file at the end of any session with real progress, per 01_GOVERNANCE.md's standing instruction
