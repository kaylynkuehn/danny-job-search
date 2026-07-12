# Danny's Remote Job Search

Automated remote job search dashboard for Danny Murray.

**Live site:** https://kaylynkuehn.github.io/danny-job-search/

## What this is

A single-page dashboard (`index.html`) that lists fully remote VP / Director roles in
investment operations, KYC/AML, fund administration, and client onboarding. It has
filters (focus area, level, industry, salary), thumbs up/down ratings, and preference
tags. Ratings and preferences are stored in the browser via `localStorage`.

## Candidate profile

Danny Murray - VP Investment Operations Onboarding, Blue Owl Capital.
Prior: Mizuho (AVP Client Onboarding), MUFG (AVP KYC Team Lead).
Certs: CAMS, Series 99, SIE.
Targeting: fully remote, VP/Director, asset management / PE / hedge funds / fintech / wealth management.

## Current state

- `index.html` is committed and served via GitHub Pages from the `main` branch (root).
- Job cards are currently hardcoded in the `FEEDS` array inside `index.html`.

## Planned automation (to be built with Claude Code on the Mac Mini)

1. **job-search.js** (Node) - fetch real postings from JSearch (RapidAPI), Remotive, and
   Adzuna using Danny's keywords x (VP, Director, Head of) with remote-only US filters.
   Dedupe, filter to remote VP/Director, then score each 1-10 against Danny's profile via
   the Anthropic API and keep the top matches with a one-line reason. Write `jobs.json`
   (title, company, salary, location/remote, url, datePosted, focus, level, industry,
   score, reason).
2. **Rewire dashboard** - render cards from `jobs.json` instead of the hardcoded `FEEDS`
   array. Keep the exact same design, filters, thumbs, and preference tags. Sort by score.
   Populate salary/date badges from real data (omit salary badge if not listed).
3. **Publish** - after each run, commit and push `jobs.json` + `index.html` to this repo:
   `git remote add origin https://github.com/kaylynkuehn/danny-job-search.git`
4. **iMessage** - after a successful run, text Danny via osascript/AppleScript:
   "Here's your remote job roundup: <live URL>" + top 3 (Title / Company / Salary).
5. **Schedule** - launchd plist running every 3 days at 8am, with logging.
6. **Error handling** - if all APIs fail, do not text Danny; log instead. If salary is
   missing, omit the badge rather than guessing.

## Notes

- Do not touch the `localStorage` wrapper or the overall visual design when editing.
- The repo is public (required for free GitHub Pages), so the dashboard URL is publicly
  accessible - keep API keys and phone numbers in a local `.env` file, never committed.
# danny-job-search
Automated remote job search dashboard for Danny
