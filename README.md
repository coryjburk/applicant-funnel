An interactive, single-file browser tool that shows Full-Time MBA students the real math behind applying to jobs: how little recruiter attention any one application actually receives, why "we review every application" can be true and still mean six seconds, and why getting *out* of the anonymous pile (through referrals and connections) is the whole game.

Built for the Full-Time MBA Program, David Eccles School of Business, University of Utah.

---

## **▶ Live tool** **[Application Funnel-Insights](https://coryjburk.github.io/applicant-funnel/)**

---

## What it does

Students adjust five inputs and watch every downstream number recompute live:

- **The WIIFM readout.** The share of a recruiter's time that lands on *their* resume (Stage 1) and *their* screening call (Stage 2), with a note distinguishing this from odds of advancing.
- **The funnel.** Total applicants, then the small group that reaches a conversation, plus what that costs the recruiter in hours and business days.
- **The depth-of-attention proof.** How long it would take one recruiter to give every resume a genuine read at four levels of average attention, measured against a sourced hiring-window benchmark.
- **The "So what?" payoff.** The networking lesson the math sets up. A referral or connection gets you out of the pile instead of trying to win a six-second lottery thousands of times.

## Live demo

Deployed via GitHub Pages at:

```
https://coryjburk.github.io/applicant-funnel/
```

## How to use it

1. Open the page in any modern browser.
2. Pick a starting point with a preset button, or set the five inputs by hand.
3. Read the results. Every panel updates instantly as you move a slider or type a value.

**Inputs**

| Input | Range | Default | What it means |
|---|---|---|---|
| Open requisitions | 1 to 40 | 15 | Reqs one recruiter is carrying at once |
| Applicants per req | 10 to 2,000 | 500 | Applications per opening |
| Resume review time | 1 to 30 sec | 6 | Average time per applicant across the whole first pass, automated screening and any human glance combined. Not a literal human read of every resume. |
| Filter-out rate | 50 to 99.9% | 98 | Share screened out before any conversation, through ATS keyword filters, AI screening, and the recruiter's own rapid pass |
| Screening call time | 5 to 60 min | 15 | Length of a first recruiter phone screen |

**Presets**

| Preset | Reqs | Apps/req | Review | Filter-out | Screen |
|---|---|---|---|---|---|
| Typical corporate | 15 | 500 | 6 sec | 98% | 15 min |
| High-volume role | 18 | 1,000 | 5 sec | 99% | 20 min |
| Boutique / niche | 8 | 150 | 10 sec | 90% | 30 min |

Preset values are illustrative starting points, not sourced figures. Your last-used inputs are saved in the browser (see Privacy below), so the tool reopens where you left off.

## The math

Every figure derives from the five inputs. The workday length (8 hours) and the hiring-window reference (see Sourced figures, below) are the only fixed constants.

```
Total applicants (Stage 1)   = reqs x applicants_per_req
Resume review hours          = total_applicants x review_seconds / 3600
Resume review business days  = review_hours / 8

Pass-through rate            = (100 - filter_out_percent) / 100
Total applicants (Stage 2)   = total_applicants x pass_through
Applicants per req (Stage 2) = stage2_applicants / reqs

Screening hours              = stage2_applicants x screen_minutes / 60
Screening business days      = screening_hours / 8
Combined recruiter time      = review_days + screening_days

Share of Stage 1 time on you = 1 / total_applicants
Share of Stage 2 time on you = 1 / stage2_applicants

Depth tier hours             = total_applicants x tier_seconds / 3600
Depth tier business days     = tier_hours / 8
```

**Display floor:** if the Stage 2 population rounds below 1 (a very small pool filtered very aggressively), the tool displays "1" rather than "0," with a note that this usually means one of three things: no applicant met the bar, the filter is miscalibrated, or the role is not being actively pursued (a "ghost" posting).

**Note on the WIIFM percentages:** these reduce algebraically to 1 divided by the applicant count, so they measure attention share, not selection probability. They will not move if you change the review-time or screening-time slider alone, because everyone's slice scales with yours. The tool flags this in-panel so it is not mistaken for your odds of advancing.

## Sourced figures versus assumptions

Two figures in this tool are cited to external data. Everything else is either a direct calculation from the five inputs or a clearly labeled illustrative default.

**Sourced: hiring-window reference (28 business days).**
Used as the reference line in the depth-of-attention panel, to show which review depths are realistic within a typical hiring cycle. Based on SHRM's 2026 Recruiting Executives Benchmarking report, which puts the median time-to-fill for nonexecutive roles at 39 calendar days (down from 44 in 2025). Converted to business days at a 5/7 ratio, giving approximately 28 business days. This is a broad median across nonexecutive roles generally, not a figure specific to MBA-level or Full-Time MBA target roles, so treat it as directional rather than exact for any one employer or role type.
Source: SHRM, "2026 Recruiting Executives Benchmarking: Attracting Critical Talent," shrm.org/in/topics-tools/research/recruiting-benchmarking/full-data-brief

**Sourced: referral hiring advantage (4x, with a documented range up to 10x).**
Used in the closing "So what?" panel to support the case for networking. Industry data consistently shows referred candidates are hired at meaningfully higher rates than applicants from other channels. The specific multiplier reported varies by source and methodology, from about 4x in the more conservative, more traceable citations up to 10x in some vendor-reported figures for specialized roles. This tool cites 4x because it is the number that holds up across independently corroborated sources rather than a single vendor's marketing data. The underlying lineage traces to Jobvite's applicant-tracking data, as reported through SHRM's coverage of ERIN's 2024 referral analysis and corroborated by multiple independent industry sources citing similar applicant-to-hire conversion ratios (roughly 30% for referred candidates versus roughly 7% for other channels). This is industry and HR-technology reporting, not a peer-reviewed controlled study, so it should be presented to students and employers as a well-supported industry estimate rather than an exact statistic.
Representative sources: SHRM's reporting on referral programs (shrm.org/topics-tools/news/talent-acquisition), and industry analyses citing Jobvite and ERIN referral-conversion data.

**Everything else is a direct calculation** from the five adjustable inputs, with no external figure involved. Preset scenario values (Typical corporate, High-volume role, Boutique/niche) are illustrative starting points built for teaching contrast, not sourced benchmarks for those categories specifically.

## Known limitations

- The model represents one recruiter's total workload across all their open reqs, not a single job considered in isolation.
- Resume review time is modeled as an average across the entire first-pass process (automated plus human), not a literal per-resume human read. See the input guidance in the tool itself.
- Real hiring funnels vary by role, industry, season, and company, more than a five-input model can fully capture. The tool is built to make the scale of the funnel intuitive, not to predict any specific employer's process.
- The referral multiplier is a range, not a point estimate. Presenting it as an exact 4x figure to a skeptical audience should come with the caveat that published estimates run from about 4x to about 10x depending on source.

## Privacy and data

The tool makes no network calls of its own and sends no data anywhere. The five inputs are stored only in the visitor's own browser, using local storage under the key `raf_funnel_v1`, and never leave the device. There is no server, no analytics, and no API. Nothing a student types is transmitted or retained by anyone else.

## Deployment (GitHub Pages)

1. Commit `recruiters-application-funnel.html` (or `index.html`, if this is the site's landing page) to the repository.
2. In Settings, then Pages, set the source branch and root folder.
3. Wait for the Pages build to finish, then visit the published URL above.

## Editing and customization

Everything adjustable sits near the top of the `<script type="text/babel">` block in the HTML file. Edit in any text editor, save, and refresh the browser. No build tooling required.

- `PRESETS`: change or add preset scenarios.
- `FIELDS`: input labels, ranges, and the guidance note under each control.
- `HOURS_PER_DAY`: the workday length (default 8).
- `reqWindow` (inside the metrics calculation): the depth-panel reference window, currently 28 business days, sourced from SHRM as described above.
- `STORAGE_KEY`: the browser storage namespace (`raf_funnel_v1`).

## Ops guidelines: keeping sourced figures current

This tool now carries two externally sourced figures (the hiring-window reference and the referral multiplier). Both should be treated as living data points, not permanent constants. Suggested practice for whoever maintains this tool:

**Review cadence.** SHRM typically refreshes its recruiting benchmarking report annually. Check for an updated release each time the Class 5/6 compensation curriculum is refreshed, or at minimum once per academic year, and update `reqWindow` if the median time-to-fill figure has changed materially.

**Where to check.**
- Time-to-fill: search "SHRM recruiting benchmarking report" for the current year, or check shrm.org's research and benchmarking section directly.
- Referral multiplier: search current-year "employee referral statistics SHRM" or "Jobvite referral conversion rate." Cross-check at least two independent sources before updating the cited figure, since this space has a wide range of vendor-reported numbers of varying quality.

**How to update.**
1. Confirm the new figure and its primary source.
2. Update the relevant constant or copy in the HTML file (`reqWindow` for the hiring window; the lever text in the "So what?" panel for the referral multiplier).
3. Update the citation text in this README and in the companion Word manual so both stay in sync with the tool.
4. Note the update date and source in a short changelog entry (a simple dated bullet list is sufficient; this repository does not currently maintain one, so start one if figures are updated for the first time).

**Do not** update a sourced figure based on a single blog post or vendor landing page without a traceable primary source (SHRM, Jobvite, ERIN, or similarly credentialed industry research). Several sources found during initial research cite the same underlying data with different framing, so a range is often more honest than a single new number.

**Standard for adding any new sourced claim to this tool going forward:** cite the primary source in the tool's copy or in this README, distinguish it clearly from assumptions or illustrative defaults, and prefer a defensible conservative figure with a disclosed range over a more dramatic headline number from a single source.

---

*Recruiters & The Application Funnel. Full-Time MBA Program, David Eccles School of Business, University of Utah.*

---

_Developed by Cory Burk, Senior Manager, Program Management · Full-Time MBA Program · David Eccles School of Business.
© 2026 University of Utah, David Eccles School of Business. All rights reserved._
