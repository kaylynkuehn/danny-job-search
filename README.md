# Danny's Remote Job Search

Automated weekly dashboard of fully remote VP/Director roles for **Danny Murray**, curated to his profile. Live site: https://kaylynkuehn.github.io/danny-job-search/

Data lives in `jobs.json`; the page (`index.html`) renders from it. Full profile is in `danny-profile.md`.

---

## Candidate profile (summary)

Danny Murray - VP Investment Operations Onboarding, Blue Owl Capital. Prior: Mizuho (AVP Client Onboarding), MUFG (KYC Onboarding Team Lead). Certs: CAMS, Series 99, SIE.

Targets: fully remote (US), VP / Director / Senior Director / Head, in KYC/AML/BSA, client & investor onboarding, investment operations, and fund administration, within asset management, private credit, PE, hedge funds, alternative investments, banking, fintech, or wealth management.

---

## Sources to search (every run)

Search all of these, not just LinkedIn:

1. **LinkedIn** (logged in) - filters `f_WT=2` (remote) + `f_E=4,5,6` (mid-senior/director/executive), sorted by date.
2. **Indeed** (logged in) - remote filter on, sorted by date.
3. **Independent web search, ATS-targeted** - restrict to direct applicant-tracking systems: `boards.greenhouse.io`, `job-boards.greenhouse.io`, `jobs.lever.co`, `*.myworkdayjobs.com`, `jobs.ashbyhq.com`. This is where real individual postings live.
4. **RemoteHunter** - https://www.remotehunter.com/jobs?search=<term> (no login needed). Job links are `/apply-with-ai/<id>`.

Search terms: "Fund Administration", "KYC" / "AML" / "BSA", "Investment Operations", "Client Onboarding" / "Investor Onboarding", plus senior compliance titles ("BSA Officer", "MLRO", "Head of Compliance", "Financial Crimes").

## Curation rules

- **Fully remote (US) is non-negotiable.** Drop anything hybrid or on-site, even if otherwise perfect (e.g. an in-office private-credit role is out).
- **Level: VP / Director / Senior Director / Head only.** Exclude analyst, associate, and plain manager roles unless they are genuine senior leadership (a designated officer, or a function lead managing a team).
- **On-focus:** KYC/AML/BSA, client/investor onboarding, investment operations, fund administration.
- **On-industry:** asset mgmt, private credit, PE, hedge funds, alt investments, banking, fintech, wealth mgmt. Nonprofit/philanthropic-fund roles are adjacent - allow only when the function is a strong fund-admin/compliance fit, and label the industry honestly.
- Show a salary badge only when the posting lists pay. Never invent salary or dates.

## Exclusions (what "generic / off-target" means)

- **Generic aggregator pages** - jobs.com, ZipRecruiter, Glassdoor, Zippia, JobToday, and Indeed/Google SEO landing pages ("finance jobs", "remote AML jobs"). These are category pages, not real postings. Skip them; use the direct company/ATS link instead.
- **Off-target roles that only match keywords loosely** - marketing/brand, product management, strategic finance/FP&A, customer success, "co-founder (equity only)" and stealth-startup CEO gigs, recruiter pitches. LinkedIn free-text surfaces many of these; read the actual role before including.

## Liveness rule (important)

**Remove any posting no longer accepting applications - on every source, not just LinkedIn.** Re-verify each carried-over role each run.

- LinkedIn: a closed posting shows a red "No longer accepting applications" banner on the job page (visible when logged in). LinkedIn blocks automated fetching via robots.txt, so check this in the logged-in browser.
- ATS/other: a closed role usually 404s or shows an inactive/closed notice.

## Learnings (2026-08-03 run)

- LinkedIn free-text search with the remote+senior filters is **noisy** - top results were co-founder/equity gigs, marketing, product, and AI-startup roles. Curation must read each posting, not trust the title.
- Open web search returns mostly **aggregator SEO pages**; ATS-restricted search is what surfaces genuine direct postings.
- Liveness matters a lot: **6 of 9** carried-over LinkedIn roles were already closed (Aventum, OSL MLRO, Axonic, Alpaca, Strata, Nymbus). Always re-verify before publishing.
- Senior remote **KYC/AML** roles are scarce on any given day; fund-administration leadership is the most reliable category for Danny.

## Dashboard architecture

- `index.html` fetches `jobs.json` and renders cards. Weekly refresh only edits `jobs.json`.
- Thumbs up/down persist in `localStorage` keyed by **job URL** (`danny_ratings_v2`), so ratings survive refreshes. Do not revert to index-based keys.
- A "Last updated" stamp reads from `jobs.json` `updated`.
- Each job object: `title, src, url, focus, level, industry, salaryMin, salaryLabel, datePosted, desc`. `src` drives the source badge (LinkedIn / Indeed / RemoteHunter / Direct / Web).
- Do not touch the `localStorage` wrapper or the overall visual design when editing.

## Weekly automation (Wednesdays)

1. Re-read these rules. 2. Search all sources. 3. Curate to the rules; drop generic/off-target and any closed postings. 4. Update `jobs.json` and commit (refreshes the GitHub Pages dashboard). 5. Text Danny the top 3 via Messages.

Semi-attended: needs the Mac awake with Chrome + the Claude extension + Messages open, and may prompt to reconnect the browser. The repo is public (required for free GitHub Pages) - keep phone numbers and any tokens in a local `.env`, never committed.


## Weekly text to Danny (template)

Send from Kaylyn's Messages to the emoji-heart (Danny) contact, then the live dashboard link. Format:

```
Here's your weekly remote search round up
Top three picks
- Title, Company (salary range if avail)
- Title, Company (salary range if avail)
- Title, Company (salary range if avail)
```
