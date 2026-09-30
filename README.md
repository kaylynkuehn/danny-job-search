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

5. **ZipRecruiter connector** (MCP tool in Kaylyn's Claude account) - filter `location_types: REMOTE` + `seniority_classes: SENIOR`. Returns 5 results per call, so page with `offset`. **Its salary figures are ZipRecruiter estimates, not posted pay - never put them on a card.** Use it to surface leads, then find the employer's own ATS link before publishing.

### Job board connectors (tested 2026-09-11)

- **ZipRecruiter** - works. Real remote + senior filters, real employer links. Skews community bank over fintech, and salaries are estimates. Worth a sweep every run.
- **Indeed** - do not rely on it. Its relevance matching collapses on senior finance-compliance titles: "Director BSA AML Financial Crimes, remote" returned a Chief Compliance Officer at a school-website company; "Director Fund Administration" returned Harvard, Yale, and a part-time development specialist.
- **Snagajob** - hourly and shift work. Not relevant to this search.

Search terms: "Fund Administration", "KYC" / "AML" / "BSA", "Investment Operations", "Client Onboarding" / "Investor Onboarding", plus senior compliance titles ("BSA Officer", "MLRO", "Head of Compliance", "Financial Crimes").

## Curation rules

- **Fully remote (US) is non-negotiable.** Drop anything hybrid or on-site, even if otherwise perfect (e.g. an in-office private-credit role is out).
- **Level: VP / Director / Senior Director / Head only.** Exclude analyst, associate, and plain manager roles unless they are genuine senior leadership (a designated officer, or a function lead managing a team).
- **Pay: $160K is the absolute floor, not the target.** He is not desperate. The posted range should start at roughly $150K+ and have a midpoint of $175K+; the ideal is well above $160K. Drop wide ranges that start low (e.g. $125K-$208K). **Missing salary is common for remote roles.** Keep a no-pay role only when the title, scope and years asked plausibly pay $175K+ (Director/VP/Head or a named-officer seat at a funded fintech, bank, or asset manager). Drop no-pay roles whose title or experience ask reads mid-level.
- **Calibrate to his real level, not the title.** Danny has ~8 years, all in KYC / client onboarding operations (team lead, AVP, VP). He has not been a named BSA officer, CCO, or fund-admin head. Target his *next step*: Director/VP of KYC or onboarding ops, AML/BSA Officer seats at small-to-mid fintechs, Director AML roles asking ~5-10 years. **Exclude** CCO / Deputy CCO seats, SVP/EVP roles, and anything asking 12+ years, even if the title and pay match. Head-of-compliance roles that want a prior named officer can be listed only as a labeled "Reach", never in the top 3.
- Tag each card's desc as **Realistic**, **Stretch**, or **Reach** so Danny can see fit at a glance.
- **On-focus, two equal tracks:** (1) compliance: KYC/AML/BSA, financial crimes, AML officer seats; (2) finance operations: investment operations, fund operations/administration, client and investor onboarding ops, banking/payments/treasury operations. He is in operations today, so ops roles are as important as compliance roles.
- **On-industry:** asset mgmt, private credit, PE, hedge funds, alt investments, banking, fintech, wealth mgmt. Nonprofit/philanthropic-fund roles are adjacent - allow only when the function is a strong fund-admin/compliance fit, and label the industry honestly.
- Show a salary badge only when the posting lists pay. Never invent salary or dates.

## Exclusions (what "generic / off-target" means)

- **Generic aggregator pages** - jobs.com, ZipRecruiter, Glassdoor, Zippia, JobToday, and Indeed/Google SEO landing pages ("finance jobs", "remote AML jobs"). These are category pages, not real postings. Skip them; use the direct company/ATS link instead.
- **Off-target roles that only match keywords loosely** - marketing/brand, product management, strategic finance/FP&A, customer success, "co-founder (equity only)" and stealth-startup CEO gigs, recruiter pitches. LinkedIn free-text surfaces many of these; read the actual role before including.

## Liveness rule (important)

**Remove any posting no longer accepting applications - on every source, not just LinkedIn.** Re-verify each carried-over role each run.

- LinkedIn: a closed posting shows a red "No longer accepting applications" banner on the job page (visible when logged in). LinkedIn blocks automated fetching via robots.txt, so check this in the logged-in browser.
- ATS/other: a closed role usually 404s or shows an inactive/closed notice.

## Known access limits (what breaks a run)

Hit repeatedly through 2026-09-11. Read before assuming a source is dead.

- **Workday postings are JS-rendered.** `*.myworkdayjobs.com` returns only meta tags to the fetch tool, so WEX, UMB, Texas Capital, HedgeServ, CIBC and AML RightSource leads cannot be verified that way. **Open them in the logged-in browser instead.**
- **LinkedIn and RemoteHunter block the fetch tool via robots.txt.** Browser only. On LinkedIn, the logged-in job page reliably gives title, company, location and the closed-posting banner, but the description body sometimes will not render at all - when that happens, leave the role off the dashboard rather than publishing on a title alone.
- **Claude's cloud container has no general internet.** Every request outside the package registries is refused at the proxy, so there is no curl, no clone and no `git push` from there. `jobs.json` must be committed through the GitHub web editor in the logged-in browser.
- **Claude's built-in browser is a separate profile and is not signed in to LinkedIn.** It is a fallback for open sites only.
- **GitHub's web editor uses CodeMirror 6**, reachable at `document.querySelector('.cm-content').cmTile.view`. Dispatch a full-document change against it, then click "Commit changes...".
- **A cloud-scheduled run cannot do any of this.** No logged-in Chrome, no Messages, no commit path. The weekly task has to run on the computer.

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


## Preferences (soft signals, not filters)

On top of the hard rules above, favor these when choosing among qualified roles and when ordering the weekly top 3 for Danny:

- Interesting, well-known, or up-and-coming **fintech** and financial brands (hot/popular names, notable startups) over generic or unknown employers.
- Companies with strong **startup culture** (fast-moving, modern, product-driven).
- Lead the top 3 with the most on-brand fintech/startup fits when they clear every hard rule.

These are tie-breakers and ranking signals only. Never relax the non-negotiables (fully remote US, senior level, on-focus function) just because a brand is exciting.

## History log (update every run)

`history.json` is the permanent backlog behind `history.html` (live: /history.html). Never delete roles from it. On every weekly refresh, after `jobs.json` is final:

1. Append a run: `{"date":"YYYY-MM-DD","count":<roles published>,"note":"<one line>"}` to `runs`. If a run is blocked and nothing could be verified, append it with `"count":null` and say why in `note`.
2. For every role in the new `jobs.json`: if it is already in `roles` (match on company + title), set `lastSeen` to today, add today to `seen`, keep `status:"open"`, refresh `url`/salary if they changed. Otherwise add it with `firstSeen` = `lastSeen` = today, `status:"open"`, `reason:"Still listed on the last verified run"`.
3. For every role with `status:"open"` that is NOT in the new `jobs.json`: set `status` (`closed` = posting gone or no longer accepting applications, `applied` = Danny already applied, `dropped` = no longer fits criteria, `retitled` = same req re-posted under a new title), `removedOn` = today, and a short `reason`.
4. Set `generated` to today.

Role fields: `company, title, url, focus, level, industry, salaryMin, salaryLabel, datePosted, firstSeen, lastSeen, seen[], status, removedOn, reason`.
