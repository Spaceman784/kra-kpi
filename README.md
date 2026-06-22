# Nap Chief — KPI Dashboard (v5, table view)

A single self-contained file: **`napchief-kpi-dashboard.html`**. No build step, no
dependencies, zero investment. Open it directly, or run it with npm (below).

## How it's organised

**Landing = team tiles.** The dashboard opens on a grid of department tiles —
**All Teams, Ops, Social Media, Marketplace, Shopify, CRM**. Each tile shows the
team's headcount and a live **on-track / off-track** total (plus watch / not-updated
when present). Click a tile to open that team's board; "All Teams" shows everyone.

**Team board.** Inside a board you get a "← All teams" button, the team's on/off
summary, a KPI-tier filter (All / North Star / Secondary / Tertiary), an as-of week
selector and a time-range filter — then each person's KRA/KPIs as per-period tables.

**Per-period tables.** North Stars read as a real table: one column per week
(`Apr 27 · May 4 · May 11 · May 18`) with **actual / target** per cell, color-coded by
status. Secondary metrics show month-on-month, Tertiary show quarter-on-quarter. A
Month / Quarter / Year rollup aggregates each KPI sensibly (counts summed, rates
averaged, stock metrics take the latest).

**"vs last week" comparison.** The last column is a simple, bold comparison: a colored
arrow + change vs the previous period (▲ up, ▼ down). The **color** tells you if the
move is good or bad for that KPI (so a falling Rework Rate shows ▼ in green).

**Light / dark theme.** Toggle top-right (🌙 / ☀). Your choice is remembered.

## Data — who's on the dashboard

Sample data ships inside the file. Right now there is **one real person: Arjun P. (Ops)**,
using his actual KRA/KPI structure from `Arjun Paleja | KRA_KPIs.xlsx`:

- North Star (weekly): Automation Projects Completed · Time/Cost/Quality Impact
- Secondary (monthly): Rework Rate (≤15%) · Automation Brief Delivery Rate
- Tertiary (quarterly): AI Tool Adoption · Deliverable Documentation Rate · Culture Rating

### Adding a teammate

Find `const MOCK_PEOPLE = [` near the top of the `<script>` and add an object like
Arjun's. Set `dept` to one of the team names in `const DEPARTMENTS = [...]` (Ops,
Social Media, Marketplace, Shopify, CRM) and they'll appear under that tile. To add a
new team, just add its name to `DEPARTMENTS`.

## Going live off Google Sheets

1. Publish the central database's Database tab to web → CSV → Publish, copy the URL.
2. In the file, find `const DATA_SOURCE = { mode: "mock", sheetCsvUrl: "" };`
3. Set `mode: "sheets"` and paste the URL into `sheetCsvUrl`. Save, reopen.
4. The "Source" pill should read **Source: Google Sheets (live)**.

CSV columns: `person, role, dept, tier, kpi_name, goal_dir, period_start, target,
actual, status, notes` (`tier` = `northStar` | `secondary` | `tertiary`;
`goal_dir` = `up` | `down`; `status` = `ontrack` | `watch` | `off`).

## Run it

```bash
cd "Kra kpi "
npm run dev          # opens at http://localhost:5173/napchief-kpi-dashboard.html
```

Or with no server at all:

```bash
open "napchief-kpi-dashboard.html"
```
