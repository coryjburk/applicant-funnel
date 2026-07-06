# Full-Time MBA Program · David Eccles School of Business · Recruiters & The Application Funnel

An interactive, single-file browser tool that shows Full-Time MBA students the real math behind applying to jobs: how little recruiter attention any one application actually receives, why "we review every application" can be true and still mean six seconds, and why getting *out* of the anonymous pile (through referrals and connections) is the whole game.

Built for the Full-Time MBA Program, David Eccles School of Business, University of Utah.

---

## What it does

Students adjust five inputs and watch every downstream number recompute live:

- **The WIIFM readout** — the share of a recruiter's time that lands on *their* resume (Stage 1) and *their* screening call (Stage 2).
- **The funnel** — total applicants → the small group that reaches a conversation, plus what that costs the recruiter in hours and business days.
- **The depth-of-attention proof** — how long it would take one recruiter to give every resume a genuine read at four levels of depth, against a typical hiring window.
- **The "So what?" payoff** — the networking lesson the math sets up: a referral or connection gets you out of the pile instead of trying to win a six-second lottery thousands of times.

## Live demo

Deployed via GitHub Pages. Once Pages is enabled for this repo, the tool is available at:

```
https://coryjburk.github.io/<repo-name>/recruiters-application-funnel.html
```

(Replace `<repo-name>` with the actual repository name. If the file is renamed to `index.html`, the trailing filename can be dropped.)

## How to use it

1. Open the page in any modern browser.
2. Pick a starting point with a **preset** button, or set the five inputs by hand:

| Input | Range | Default | What it means |
|---|---|---|---|
| Open requisitions | 1–40 | 15 | Reqs one recruiter is carrying at once |
| Applicants per req | 10–2,000 | 500 | Applications per opening |
| Resume review time | 1–30 sec | 6 | Seconds spent on a first-pass resume scan |
| Filter-out rate | 50–99.9% | 98 | Share screened out before any conversation |
| Screening call time | 5–60 min | 15 | Length of a first recruiter phone screen |

3. Read the results. Every panel updates instantly as you move a slider or type a value.

**Presets**

| Preset | Reqs | Apps/req | Review | Filter-out | Screen |
|---|---|---|---|---|---|
| Typical corporate | 15 | 500 | 6 sec | 98% | 15 min |
| High-volume role | 18 | 1,000 | 5 sec | 99% | 20 min |
| Boutique / niche | 8 | 150 | 10 sec | 90% | 30 min |

Your last-used inputs are saved in the browser (see [Privacy](#privacy)), so the tool reopens where you left off.

## The math

The tool models **one recruiter's total workload across all their open reqs.** Every figure derives from the five inputs:

```
Total applicants (Stage 1)   = reqs × applicants_per_req
Resume review hours          = total_applicants × review_seconds / 3600
Resume review business days  = review_hours / 8

Pass-through rate            = (100 − filter_out_percent) / 100
Total applicants (Stage 2)   = total_applicants × pass_through
Applicants per req (Stage 2) = stage2_applicants / reqs

Screening hours              = stage2_applicants × screen_minutes / 60
Screening business days      = screening_hours / 8
Combined recruiter time      = review_days + screening_days

Share of Stage 1 time on you = 1 / total_applicants        (= review_seconds / total review seconds)
Share of Stage 2 time on you = 1 / stage2_applicants        (= screen_minutes / total screen minutes)
```

The **depth-of-attention** panel reuses the Stage 1 population at four fixed depths (6 sec, 30 sec, 2 min, 5 min) to show how long a real read would take:

```
tier_hours = total_applicants × tier_seconds / 3600
tier_days  = tier_hours / 8
```

Any tier that exceeds the reference hiring window turns red.

## Methodology, assumptions & limits

Read these before putting the tool in front of employers or students who will push on the numbers.

- **8-hour workday** is hardcoded for all "business day" conversions.
- **~30 business-day req window** (used only as the red-line reference in the depth panel) is an *assumption*, not a sourced figure. It's the single number a sharp reader can challenge. Source it or soften it before citing it as fact.
- **"Referred candidates advance at higher rates"** in the closing panel is stated directionally, with no specific multiplier, on purpose — so no unsourced statistic is being defended. Add a number only if you have a source you trust.
- **"Combined recruiter time"** adds resume review + screening. The original source spreadsheet's total cell counted screening only; this tool reports the true combined figure and notes the difference in-panel.
- The model is a **teaching estimate**, not a simulation of any specific employer's ATS or process. Real funnels vary widely by role, season, and company.

## Tech stack

- Single self-contained `.html` file — no build step, no dependencies to install.
- **React 18** (UMD) + **Babel Standalone**, loaded from unpkg CDN, with in-browser JSX compilation.
- Fonts (Archivo, Inter, IBM Plex Mono) from Google Fonts.
- Plain CSS with University of Utah crimson.
- **Requires an internet connection** to load React, Babel, and fonts from their CDNs.

> Note: in-browser Babel transpiles JSX on every page load. That's fine at this size, but adds a small startup cost. If load performance ever matters, pre-compile the JSX and drop the Babel script.

## Editing & customization

Everything lives near the top of the `<script type="text/babel">` block:

- **`PRESETS`** — change or add preset scenarios.
- **`FIELDS`** — adjust input labels, min/max/step ranges, and the guide text under each control.
- **`HOURS_PER_DAY`** — the workday length (default `8`).
- **`reqWindow`** (inside the metrics `useMemo`) — the depth-panel red-line reference (default `30` business days).
- **`STORAGE_KEY`** — the localStorage namespace (`raf_funnel_v1`).

To edit: open the HTML file in any text editor, change the values, save, and refresh the browser. No tooling required.

## Privacy

This tool makes **no network calls of its own** and sends **no data anywhere**. The five inputs are stored only in the visitor's own browser via `localStorage` (key `raf_funnel_v1`) and never leave the device. There is no server, no analytics, and no API. Nothing a student types is transmitted or retained by anyone else.

## Deployment (GitHub Pages)

1. Commit `recruiters-application-funnel.html` to the repository.
2. In **Settings → Pages**, set the source branch (e.g., `main`) and root folder.
3. Wait for the Pages build to finish, then visit the published URL above.

To make it the site's landing page, rename the file to `index.html`.

## License

_Add your license here (e.g., MIT, or an internal University of Utah / Eccles usage note)._

---

*Recruiters & The Application Funnel · Full-Time MBA Program · David Eccles School of Business · University of Utah*
