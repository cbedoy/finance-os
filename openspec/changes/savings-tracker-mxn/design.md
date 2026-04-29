## Context

No existing codebase to migrate—this is a greenfield single-file web app. The target runtime is any modern browser (Chrome, Firefox, Safari). All data lives in `localStorage`. The app serves a single user (personal finance tool), so multi-tenancy and auth are out of scope.

## Goals / Non-Goals

**Goals:**
- Deliver a fully functional app in a single `index.html` file (HTML + inline CSS + inline JS)
- Implement compound-interest projection engine accurate to the daily compounding formula
- Persist accounts and salary config in `localStorage` with zero setup
- Provide a readable dark terminal UI using DM Mono from Google Fonts CDN
- Support CRUD on savings accounts with immediate recalculation

**Non-Goals:**
- Backend, database, or user authentication
- Multi-currency or non-MXN accounts
- Import/export of data files
- Mobile-native packaging (PWA is acceptable but not required)
- Charts or graphical plots (table-based UI only)

## Decisions

### Single-file delivery (index.html)
**Decision**: All HTML, CSS, and JS inline in one file.  
**Rationale**: Zero build tooling, zero dependencies to install, trivially shareable. The user explicitly requested no backend.  
**Alternative considered**: Separate `.css` / `.js` files—rejected because it adds a local server requirement for `file://` loading.

### Vanilla JS (no framework)
**Decision**: Plain ES2022 JavaScript, no React/Vue/Svelte.  
**Rationale**: The app is inherently state-light (a handful of account objects); a framework would add more complexity than it removes. DM Mono + CSS variables handle all styling needs.  
**Alternative considered**: Alpine.js—lightweight but still an external dependency that violates the "no backend" spirit for offline use.

### Compound interest with daily equivalent rate
**Decision**: Use `dailyRate = (1 + annualRate/100)^(1/365) - 1` for every account.  
**Rationale**: This is the mathematically correct daily equivalent of an annual nominal rate compounded daily, matching how CETES Directo and GBM+ compute yields.  
**Alternative considered**: Simple `annualRate / 365`—rejected because it underestimates yield and diverges noticeably at high rates (e.g., 15%+).

### localStorage schema
```
savings_accounts: Account[]   // array of {id, name, balance, rate}
salary_config: SalaryConfig   // {amount, startDate, frequency: "biweekly"}
```
IDs are generated with `crypto.randomUUID()`.

### Tab navigation via CSS + JS (no router)
**Decision**: Four-tab layout controlled by toggling a CSS class (`active`) on tab panels.  
**Rationale**: Minimal, no URL routing needed for a single-user local tool.

### Projection calculation at render time
**Decision**: The 365-day table is computed fresh on every render from the current account state and salary config.  
**Rationale**: Avoids stale cache; the dataset is small (365 rows × ~5 columns) and computes in <5ms.

## Risks / Trade-offs

- **localStorage size limit (~5MB)**: With compact account objects this is not a concern; hundreds of accounts still fit.  → No mitigation needed.
- **Date drift in biweekly payroll**: Projecting biweekly deposits from a start date across 365 days is calendar-based; months of different lengths mean deposit days shift slightly.  → Mitigation: use JS `Date` arithmetic from the configured start date, adding 14 days per period.
- **Single-file maintainability**: Inline CSS + JS in one file is harder to maintain long-term.  → Accepted trade-off given explicit "no backend" requirement; well-structured comments mitigate.
- **No data backup**: `localStorage` can be cleared by the browser or user.  → Acceptable for a personal tool; a future export feature could address this.
