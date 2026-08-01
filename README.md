# Boffo

A weekly box office tracker dashboard built for Sequence Creative, embedded on sequencela.com.

## What it is

Boffo is an editorial dashboard that gives readers a quick, visual snapshot of the domestic box office each week. It shows:

- **Hero numbers** — the current #1 movie's weekend gross vs. the previous weekend's, plus a year-over-year pace comparison
- **Weekend market pulse** — overall domestic gross compared to the prior weekend, the same weekend last year, and a 10-year average
- **This Weekend / Next Weekend / Last Weekend tabs** — the current Top 10, projections for the upcoming weekend, and a link out to Box Office Mojo for the prior weekend
- **Release Calendar** — upcoming movie releases with distributor and trailer info
- **Live chatter ticker** — a scrolling feed combining the Top 10 headline with real-time industry commentary pulled from Bluesky

## How it works

Boffo is made up of three pieces that deploy together:

1. **`index.html`** — the public-facing dashboard people actually see. It's a single webpage that loads its data from a JSON file at runtime, with a built-in emergency fallback in case that file can't be reached.
2. **`boffo-data.json`** — the canonical data file. This is the single source of truth for everything on the page: the Top 10, projections, releases, hero numbers, ticker settings, and so on.
3. **`boffo-data-studio.html`** — an internal editing tool (not shown to the public) with a tab for each section of the dashboard — Weekend Top 10, Projections, Release Calendar, Ticker, Settings, and a Validation tab that checks for missing fields, bad ranges, and duplicate entries. It supports pasting or importing data (from Box Office Mojo tables, CSVs, or JSON), previewing changes against the live dashboard layout before publishing, and exporting the updated `boffo-data.json`.

Updating Boffo weekly means editing data in the Data Studio, validating it, previewing it, then exporting and redeploying the updated JSON file alongside the two HTML files.

The dashboard is hosted for free on GitHub Pages, and the Sequence Creative website embeds it in an iframe so it looks native to the site.

## The weekly rhythm

- **Sunday**: Weekend estimates go in, ticker flags them as fresh/breaking
- **Monday–Wednesday**: Estimates get swapped for confirmed actuals; still flagged as fresh
- **Thursday**: Data is considered settled — the ticker calms down and drops the "breaking" treatment until the next Sunday's estimates
- **Midweek**: The three tabs rotate forward — this weekend's Top 10 becomes "Last Weekend," projections become "This Weekend," and a new set of projections is drafted for "Next Weekend"

## Maintenance

There's no build process and no traditional backend — just three static files (two HTML, one JSON) that get redeployed together each week via the Data Studio's export tools.
