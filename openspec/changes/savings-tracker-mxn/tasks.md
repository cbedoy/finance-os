## 1. Project scaffold

- [ ] 1.1 Create `index.html` with full page structure: `<head>` (DM Mono font link, CSS variables, base reset) and `<body>` with tab nav and four tab panels
- [ ] 1.2 Define CSS custom properties: `--bg: #070b14`, `--green: #7fd4a0`, `--blue: #38bdf8`, `--purple: #a78bfa`, `--yellow: #fbbf24` and base styles for body, monospace font, and tab layout
- [ ] 1.3 Add tab-switching JS logic: clicking a tab adds `.active` to its panel and removes it from others

## 2. localStorage layer

- [ ] 2.1 Implement `loadAccounts()` — reads `savings_accounts` from `localStorage`, returns parsed array or `[]`
- [ ] 2.2 Implement `saveAccounts(accounts)` — serializes array to `localStorage`
- [ ] 2.3 Implement `loadSalaryConfig()` — reads `salary_config` from `localStorage`, returns object or `null`
- [ ] 2.4 Implement `saveSalaryConfig(config)` — serializes salary config to `localStorage`

## 3. Yield calculator engine

- [ ] 3.1 Implement `dailyRate(annualRate)` — returns `(1 + annualRate/100)^(1/365) - 1`
- [ ] 3.2 Implement `accountDailyYield(account)` — returns `account.balance × dailyRate(account.rate)`
- [ ] 3.3 Implement `totalBalance(accounts)` — returns sum of all account balances
- [ ] 3.4 Implement `weightedAverageRate(accounts)` — returns `Σ(balance_i × rate_i) / Σ(balance_i)` or 0 when empty
- [ ] 3.5 Implement `totalDailyYield(accounts)` — returns sum of all per-account daily yields
- [ ] 3.6 Implement `formatMXN(value)` — wraps `Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN' })`

## 4. Dashboard tab

- [ ] 4.1 Render three metric cards: total balance (green), weighted avg rate (blue), daily yield (purple) using values from the calculator engine
- [ ] 4.2 Render account list rows: entity name, balance (green), annual rate (blue), daily yield (purple), and a delete button per row
- [ ] 4.3 Implement proportional distribution bar: when ≥2 accounts exist, render a flex row where each segment width = `(balance / totalBalance) × 100%`
- [ ] 4.4 Wire delete button to remove account from array, call `saveAccounts()`, and re-render dashboard

## 5. Account CRUD tab (Agregar/Editar Cuenta)

- [ ] 5.1 Build the add-account form with fields: entity name (text), balance (number, MXN), annual rate (number, %)
- [ ] 5.2 On form submit: validate all fields non-empty and numeric where required, generate `id` via `crypto.randomUUID()`, push to accounts array, call `saveAccounts()`, re-render dashboard, and clear the form
- [ ] 5.3 Implement inline editing in the account list: clicking an account row's field makes it an `<input>` in place; on blur/Enter commit the new value, call `saveAccounts()`, and re-render; on Escape revert

## 6. Salary tab (Salario Quincenal)

- [ ] 6.1 Build salary config form: biweekly amount (number, MXN) and first deposit date (date input)
- [ ] 6.2 On form submit: save config via `saveSalaryConfig()` and show confirmation
- [ ] 6.3 On tab load: populate form fields from `loadSalaryConfig()` if config exists

## 7. Projection engine

- [ ] 7.1 Implement `buildDepositSchedule(salaryConfig, days)` — returns a `Set` or `Map<dayIndex, amount>` of deposit days within 0–364, stepping 14 calendar days from start date
- [ ] 7.2 Implement `project365(accounts, salaryConfig)` — returns array of 365 objects `{day, balance, pureYield, cumulativePayroll, dailyYieldAmount}` using compound daily rate and deposit schedule
- [ ] 7.3 Ensure day 0 seeds from `totalBalance(accounts)`; each subsequent day compounds with `weightedDailyRate` and adds any deposit

## 8. Projection tab (Proyección 365 días)

- [ ] 8.1 Add a toggle (two buttons or radio) to switch between **Hitos clave** and **Día a día** views
- [ ] 8.2 Render milestone view: filter projection array to days [1, 7, 15, 30, 45, 60, 90, 120, 150, 180, 270, 365] and display as table with columns Día, Saldo acumulado (green), Rendimiento puro (purple), Nómina acumulada (yellow), Rendimiento del día (purple)
- [ ] 8.3 Render day-by-day view: render all 365 rows of the projection array with the same columns
- [ ] 8.4 Apply `formatMXN()` to all monetary columns in both views

## 9. Integration and polish

- [ ] 9.1 Call `renderDashboard()` on page load after reading accounts from `localStorage`
- [ ] 9.2 Call `renderProjection()` whenever the projection tab is activated so it reflects the latest account and salary state
- [ ] 9.3 Verify tab navigation hides/shows correct panels with no layout flicker
- [ ] 9.4 Test with zero accounts: dashboard shows MXN 0.00, projection shows flat line
- [ ] 9.5 Test with multiple accounts: verify distribution bar widths sum to 100%, weighted rate is correct, and projection totals match manual calculation for day 1 and day 30
