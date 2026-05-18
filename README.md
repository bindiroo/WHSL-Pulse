# All Orders Report

A self-contained HTML dashboard for tracking order performance across all seasons and years. No server, no dependencies to install — just open the HTML file in a browser and drop in your latest CSV.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The dashboard (open this in a browser) |
| `All Orders [date].csv` | Weekly data export — drop in the latest file each week to refresh |

## Weekly Update Workflow

1. Export your updated All Orders data as a CSV
2. Open `index.html` in a browser
3. Drag and drop the new CSV file anywhere onto the page — all charts, trend lines, and KPIs update instantly
4. Or click **Load CSV** in the top-right corner to browse for the file

No need to rename the file. Any `.csv` you drop will be accepted.

## Dashboard Tabs

### Fall
Compares Fall seasons year-over-year (Fall 2024 → Fall 2025 → Fall 2026 → ...).

### Spring / Summer
Combines Spring and Summer seasons on one tab. Spring and Summer for the same year are treated as part of the same warm-weather cycle and appear as separate lines. New Spring or Summer seasons are picked up automatically when added to the CSV.

### Annual
Combines **all seasons for a given year** into a single trend line — so Fall 2026 + Summer 2026 + Spring 2026 become one "2026" line. This is the primary view for comparing total annual order volume: 2024 vs 2025 vs 2026 vs 2027.

Each tab includes:
- **Cumulative Units** — week-normalized trend lines (Week 1 = first order received for that season or year, so years are directly comparable regardless of when ordering opened)
- **Cumulative Revenue** — same view for dollars
- **Monthly Activity** — new units booked per month, all years/seasons overlaid
- **Order Source Mix** — stacked bar showing Pre-Book vs Post Deadline vs At-Once (AO) units per season or year

## KPI Cards

The top of the dashboard shows the most recent season for each category compared to the prior year:
- Active seasons (e.g., Summer 2026) compare to the prior year **at the same week in the season**
- Completed seasons compare to the prior year's **full season total**

The **Annual tab** has its own KPI row showing each year's total units and revenue with year-over-year percentage change.

## CSV Format

The dashboard expects the standard All Orders export with this column layout:

```
Season  [empty x3]  Date  [empty x3]  Qty less Cxl  Amount  Source  [empty]
```

| Column | Value |
|--------|-------|
| 0 | Season name (e.g., `FALL 2026`, `SUMMER 2026`) |
| 4 | Date in `MM/DD/YY` format |
| 8 | Qty less Cxl (integer) |
| 9 | Amount (dollar value — `$` and commas are fine) |
| 10 | Source (`PRE-BOOK`, `Post Deadline`, or `AO`) |

Summary/total rows (blank date) are automatically ignored.

**Season names** must include a recognizable keyword and year — `FALL 2027`, `SUMMER 2027`, `SPRING 2027`, etc. New seasons are picked up automatically; no code changes needed.

## Adding Future Seasons

When 2027 seasons start appearing in your export, they will automatically show up in the correct tab with their own color and trend line. The Annual tab will add a 2027 line once any 2027 season data is present.

Pre-configured colors by year:
- **2024** — Amber
- **2025** — Blue
- **2026** — Green *(current)*
- **2027** — Orange *(next)*

## Sharing with the Team

**Option A — Shared drive:** Put the HTML file in a shared folder. Teammates open it locally and drag in the latest CSV themselves.

**Option B — GitHub Pages:** Enable GitHub Pages on this repo and share the URL. Upload a new CSV to the repo each week to update the hosted version.

**Option C — Local web server:** Run `python3 -m http.server` in this folder, then open `http://localhost:8000/`. The dashboard will attempt to auto-load `All Orders.csv` from the same directory on every page refresh.
