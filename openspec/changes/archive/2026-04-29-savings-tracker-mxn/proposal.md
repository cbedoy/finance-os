## Why

There is no simple, privacy-focused tool to consolidate and project the growth of multiple Mexican savings accounts in a single view. Managing accounts across CETES, GBM, Nu, Flink, and similar platforms requires manual spreadsheet math; this app automates compound-interest projections and payroll deposit scheduling without sending data to any server.

## What Changes

- Introduce a client-side single-page web app (vanilla JS + HTML) with no backend
- Add compound daily-rate yield calculation using `(1 + rate/100)^(1/365) - 1`
- Add 365-day projection engine with key-milestone and day-by-day views
- Add biweekly payroll deposit scheduling integrated into projections
- Persist all data in `localStorage` so no account is lost across sessions

## Capabilities

### New Capabilities

- `account-management`: CRUD for savings accounts—entity name, current balance (MXN), and annual yield rate (%)
- `yield-calculator`: Compound interest engine that computes daily rate, per-account daily yield, weighted average rate, and total consolidated balance
- `salary-tracker`: Configuration of biweekly payroll amount and deposit schedule for integration into 365-day projections
- `dashboard-ui`: Main dashboard tab showing consolidated balance, weighted average rate, daily yield estimate, and proportional distribution bars per account
- `projection-view`: 365-day projection tab with two sub-views: key milestones (days 1, 7, 15, 30, 45, 60, 90, 120, 150, 180, 270, 365) and full day-by-day table showing accumulated balance, pure yield, cumulative payroll deposits, and that day's yield

### Modified Capabilities

## Impact

- New standalone `index.html` file (or equivalent single-file app) delivered as a static asset
- No external API calls; all computation runs in the browser
- `localStorage` keys introduced: `savings_accounts`, `salary_config`
- Runtime dependencies: Google Fonts (DM Mono) loaded via CDN; no JS framework required
