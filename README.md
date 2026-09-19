# Data Center Roadmap

An interactive roadmap of the world's largest AI data center projects: when they come online, how much power they are planned for, and where each project stands today.

It covers Oracle and the OpenAI Stargate program, the hyperscalers (Amazon, Microsoft, Google, Meta), AI labs (xAI/SpaceXAI, Anthropic), neoclouds (CoreWeave, Nebius, IREN, Crusoe, Nscale) and major Chinese players (Alibaba, ByteDance, Tencent). 74 projects in total, plus 123 further data center sites from the companies' official location lists (Google, Meta, Microsoft, Nebius) and 202 cloud regions (Oracle, AWS, Google Cloud, Microsoft Azure) as separate map layers.

**Live page:** https://carokann14.github.io/data-center-roadmap/

**Data as of:** 19 September 2026

> The page is available in German and English. Switch with the **DE / EN** buttons in the sidebar, or open it with `?lang=en` (e.g. `…/DCR.html?lang=en#karte`). German is the default.

---

## Features

### Language (sidebar)
- DE / EN switch at the bottom of the sidebar (top bar on phones); the choice is remembered in the browser
- `?lang=en` or `?lang=de` in the link sets the language, so an English link can be shared directly
- Everything is translated: menus, charts, tooltips, map panels and all project data (names, locations, capacity notes, milestones, facts, source titles, cloud regions). Numbers and dates use English formats (1.2 GW, 30 Sep 2025)
- The search boxes find projects by their German and English names

### Search (sidebar)
- A search box in the sidebar, available on every page (press `/` to jump to it)
- Results appear while you type, grouped into **companies** and **projects**; case, accents and umlauts are ignored
- Selecting a company opens the home page filtered to that company – the same view as picking it from the company filter (link: `#firma-<company>`, e.g. `#firma-Oracle`)
- Selecting a project opens its full profile in the project table (link: `#p-<id>`, e.g. `#p-abilene`)

### Home (`#start`)
- Key figures: active projects, total announced capacity, cancelled or paused projects, and projects with open permitting or legal risks
- Timeline per company group, showing each project's capacity, construction start, first capacity and completion
- Click a project name to jump to its full profile, including milestones, risks and linked sources
- Filters by company (17 companies; a project matches when the company is involved), operator and status, plus a search box. A company filter can be linked directly, e.g. `#firma-Oracle`

### Yearly overview (`#jahre`, or a specific year such as `#jahr-2027`)
- Stacked bar chart of cumulative capacity in GW per year (2024–2030)
- The annual increase is highlighted inside each bar, and capacity already in operation is shown separately from planned capacity
- Select a year to list every project with a start of operations, a completion or a capacity step in that year

### World map (`#karte`, or a specific project or region such as `#karte-lighthouse` or `#karte-oci-eu-frankfurt-1`)
- Rotatable, zoomable 3D globe with all project locations
- **Marker color:** current project status
- **Marker size:** capacity available by the selected year
  - Solid disc: capacity in operation
  - Dashed ring: planned capacity (forecast)
  - "?": capacity unknown
- Nearby sites are grouped when zoomed out and split up again when you zoom in
- Filters by layer (all layers, AI projects, further sites or cloud regions), company (every company involved), country, year of first operation and status, plus search
- **Cloud regions** (Oracle OCI: 57, AWS: 44 incl. sovereign local zones, Google Cloud: 43, Microsoft Azure: 58) as their own layer: diamond = Oracle, square = AWS, triangle = Google, hexagon = Azure, hollow = announced, red = impaired. Regions have no published MW and are never added to the GW totals. A filterable list of all regions sits below the map.
- **Further sites** (Google: 65, Meta: 30, Microsoft: 21, Nebius: 7) from the companies' official location lists as their own layer: pin green = in operation, orange = in development, hollow = listed (status not verified). They have no MW or dates and are never added to the GW totals; sites already tracked as AI projects appear only as projects. A filterable list sits below the map.
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
- The yearly chart and the world map use the same steps. The map only counts projects with a map position (currently the HUMAIN AI Zone, 0.05 GW from 2028, has none).

### Map positions
Markers sit at the town center or county seat, not at the exact site. Cloud regions sit at the city in the region name; where the provider only names an area or country, an approximate stand-in point is used and labeled as such (e.g. the capital). Where Azure only names a US state or a country, the stand-in point is a known Microsoft data center in that state or the capital. AWS GovCloud and Azure Israel Central have no map position.

---

## Using and updating

- Everything is in a single, self-contained file: `DCR.html`. Open it in any browser; it also works offline.
- All data lives in the `const DATA = {...}` block inside the script.
- Each project entry holds:
  - identity: `id`, `group`, `provider`, `status`
  - map data: `geo`, `country`, `companies`
  - capacity: `capacity` (with `est` for third-party estimates) and dated `steps`
  - timeline: `chart` dates and `milestones`
  - `sources` with type and date
- Date formats: `2025-09-30`, `2026-06`, `2026-Q4`, `2027-H1`, `2028`.
- Cloud regions live in `regions` (`provider`, `code`, `name`, `kind`, `city`, `country`, `status`, `geo`, `src`).
- Further sites live in `locations` (`provider`, `companies`, `name`, `city`, `region`, `country`, `status`: in operation / in development / listed, `statusText`, `geo`, `src`).
- Existing sites without a published start date carry `bestand:true` so the map shows them in every year.
- To add a project, add an entry to `sites` and, for a new company group, extend `groups` (and `filterCompanies` for a new main company). Every `src` reference must point to an `id` in that project's `sources`.
- English texts: the German texts in `DATA` are the reference. The English version comes from the dictionary `DATA_EN` (German text → English text), placed right after `DATA`. Every new or changed text in `DATA` needs an entry there. Run `dcrMissingEN()` in the browser console to list texts without one; a missing entry falls back to German. Interface texts live in the script (`tt("German","English")`) and in `UI_EN` for the static HTML.

---

## Credits and licenses

- Charts, timeline and globe: custom SVG built with [d3](https://d3js.org) v7 (ISC license)
- Country shapes: [world-atlas](https://github.com/topojson/world-atlas) countries-110m, based on [Natural Earth](https://www.naturalearthdata.com) (public domain), loaded with topojson-client v3 (ISC license)
- Project data is compiled from the public sources linked for each project

## Disclaimer

This is an independent research overview based on public information as of the date above. Figures and timelines change often and may be incomplete or outdated. It is not investment advice.
