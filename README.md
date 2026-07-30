# fed-monitor-data

Data backend for the [Fed Rates & Inflation Dashboard](https://github.com/my7sjkmw5w-lang/fed-monitor-data). Refreshed automatically every morning by a scheduled task; the published dashboard reads these files directly via GitHub's raw content URLs, so the site updates without a redeploy.

## Files

- `data/latest.json` — current snapshot: Fed funds rate/target range, Treasury yields (13W, 5Y, 10Y, 30Y), inflation (CPI/core CPI/PCE/core PCE, YoY and MoM), unemployment, oil prices (WTI/Brent), upcoming FOMC meeting calendar and market-implied hike/hold/cut odds, and recent Fed-related news headlines. Every field carries a `source`/`source_url` (or per-item `url`) pointing at the primary source.
- `data/polls.json` — curated snapshots of Reuters economist polls and CME FedWatch market-implied odds over time. Updated whenever a new poll or notable odds shift is published (not purely mechanical — some editorial curation).
- `data/history/YYYY-MM-DD.json` — daily archived copy of `latest.json`, used by the dashboard to draw simple trend sparklines.
- `data/inflation_10y.json` — 10-year monthly history (2016–present) of headline CPI YoY and Core CPI YoY, sourced from the U.S. Bureau of Labor Statistics via Perplexity Finance. Powers the dashboard's long-run inflation trend chart. Appended monthly as new BLS releases land.

## Update cadence

A daily scheduled task re-pulls Fed funds rate, Treasury yields, inflation (CPI/PCE), oil prices, FOMC odds, and Fed news each morning (US Central time) and commits any changes here.
