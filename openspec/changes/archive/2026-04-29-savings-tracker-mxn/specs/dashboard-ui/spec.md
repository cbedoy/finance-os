## ADDED Requirements

### Requirement: Dark terminal theme
The system SHALL render all UI with a dark background color `#070b14`, monospace font DM Mono loaded from Google Fonts, and the following semantic color palette:
- Green `#7fd4a0` for balance values
- Blue `#38bdf8` for rate values
- Purple `#a78bfa` for yield values
- Yellow `#fbbf24` for payroll/salary values

#### Scenario: Theme applied on load
- **WHEN** the page loads
- **THEN** the background SHALL be `#070b14` and all text SHALL use DM Mono

### Requirement: Four-tab navigation
The system SHALL present four tabs: **Dashboard**, **Agregar/Editar Cuenta**, **Salario Quincenal**, and **Proyección 365 días**. Only one tab's content SHALL be visible at a time.

#### Scenario: Tab switching
- **WHEN** the user clicks a tab
- **THEN** that tab's panel SHALL become visible and all others SHALL be hidden

### Requirement: Dashboard summary metrics
The dashboard tab SHALL display three top-level metrics: consolidated total balance (green), weighted average annual rate (blue), and estimated daily yield (purple), formatted using `Intl.NumberFormat` with locale `es-MX` and currency `MXN`.

#### Scenario: Metrics display with accounts
- **WHEN** at least one account exists
- **THEN** all three metrics SHALL show correct calculated values in MXN format

#### Scenario: Metrics display with no accounts
- **WHEN** no accounts exist
- **THEN** all metrics SHALL display MXN 0.00

### Requirement: Account list with proportional distribution bars
The dashboard SHALL list each account with its name, balance, rate, and daily yield. When more than one account exists, a horizontal bar SHALL show each account's proportion of the total balance, using the account's position-based or fixed color.

#### Scenario: Single account
- **WHEN** only one account exists
- **THEN** no distribution bar needs to be shown

#### Scenario: Multiple accounts
- **WHEN** two or more accounts exist
- **THEN** a bar row SHALL appear where each segment's width is proportional to that account's share of the total balance

### Requirement: Currency formatting
All monetary values throughout the app SHALL be formatted using `Intl.NumberFormat('es-MX', { style: 'currency', currency: 'MXN' })`.

#### Scenario: Formatted output
- **WHEN** a value of 1234.5 MXN is displayed
- **THEN** it SHALL render as `$1,234.50` in es-MX locale style
