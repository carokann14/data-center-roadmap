# Data Center Roadmap

An interactive roadmap of the world's largest AI data center projects: when they come online, how much power they are planned for, and where each project stands today.

It covers Oracle and the OpenAI Stargate program, the hyperscalers (Amazon, Microsoft, Google, Meta), AI labs (xAI/SpaceXAI, Anthropic), neoclouds (CoreWeave, Nebius, IREN, Crusoe, Nscale) and major Chinese players (Alibaba, ByteDance, Tencent). 41 projects in total.

**Live page:** `https://<your-username>.github.io/<repo-name>/` *(replace with your GitHub Pages link)*

**Data as of:** 18 September 2026

> The page itself is in German. The data, sources and structure are described below in English.

---

## Features

### Home (`#start`)
- Key figures: active projects, total announced capacity, cancelled or paused projects, and projects with open permitting or legal risks
- Timeline per company group, showing each project's capacity, construction start, first capacity and completion
- Click a project name to jump to its full profile, including milestones, risks and linked sources
- Filters by program (Oracle, Stargate, hyperscalers, AI labs, neoclouds, China), operator and status, plus a search box

### Yearly overview (`#jahre`, or a specific year such as `#jahr-2027`)
- Stacked bar chart of cumulative capacity in GW per year (2024–2030)
- The annual increase is highlighted inside each bar, and capacity already in operation is shown separately from planned capacity
- Select a year to list every project with a start of operations, a completion or a capacity step in that year

### World map (`#karte`, or a specific project such as `#karte-lighthouse`)
- Rotatable, zoomable 3D globe with all project locations
- **Marker color:** current project status
- **Marker size:** capacity available by the selected year
  - Solid disc: capacity in operation
  - Dashed ring: planned capacity (forecast)
  - "?": capacity unknown
- Nearby sites are grouped when zoomed out and split up again when you zoom in
- Filters by company (every company involved in a project), country, year of first operation and status, plus search
- Time slider with play button to watch capacity build up year by year
- Detail panel for each site:
  - operator, partners and customers
  - capacity in operation, planned expansion steps and maximum final capacity
  - commissioning dates, milestones, sources and date of last review

---

## Data principles

1. **Nothing is invented.** Every value links to a source: company press releases, news reports or analyses.
2. **Confirmed vs. estimated.** Company and news figures are kept apart from third-party estimates, mostly from [Epoch AI](https://epoch.ai/data/ai-data-centers). Estimates are labeled "Prognose Dritter" or shown as "≈ … GW*".
3. **Unknown stays unknown.** Where no public figure exists, the page says so instead of guessing.
4. **No double counting.** Each project appears once, even when several companies are involved. For example, the Abilene campus involves Oracle, OpenAI and Crusoe but is one entry.
5. **Mixed capacity metrics.** Companies report IT load, grid power demand, campus capacity or power purchase agreements. The type is shown next to every value, and totals are only a rough indication.

### How yearly capacity is calculated
Each project has a list of dated, sourced capacity steps: year, GW, in operation or planned, and whether the figure comes from a third party.
- If there is no sourced breakdown, the full capacity is counted in the year of completion.
- Capacity without a published date is not counted and is listed separately.
- The yearly chart and the world map use the same steps, so their totals always match.

### Map positions
Markers sit at the town center or county seat, not at the exact site.

---

## Using and updating

- Everything is in a single, self-contained file: `index.html`. Open it in any browser; it also works offline.
- All data lives in the `const DATA = {...}` block inside the script.
- Each project entry holds:
  - identity: `id`, `group`, `provider`, `status`
  - map data: `geo`, `country`, `companies`
  - capacity: `capacity` (with `est` for third-party estimates) and dated `steps`
  - timeline: `chart` dates and `milestones`
  - `sources` with type and date
- Date formats: `2025-09-30`, `2026-06`, `2026-Q4`, `2027-H1`, `2028`.
- To add a project, add an entry to `sites` and, for a new company group, extend `groups` and `categories`. Every `src` reference must point to an `id` in that project's `sources`.

---

## Credits and licenses

- Charts, timeline and globe: custom SVG built with [d3](https://d3js.org) v7 (ISC license)
- Country shapes: [world-atlas](https://github.com/topojson/world-atlas) countries-110m, based on [Natural Earth](https://www.naturalearthdata.com) (public domain), loaded with topojson-client v3 (ISC license)
- Project data is compiled from the public sources linked for each project

## Disclaimer

This is an independent research overview based on public information as of the date above. Figures and timelines change often and may be incomplete or outdated. It is not investment advice.
