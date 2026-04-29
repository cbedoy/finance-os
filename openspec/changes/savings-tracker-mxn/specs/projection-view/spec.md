## ADDED Requirements

### Requirement: 365-day compound projection engine
The system SHALL project account growth for each of the 365 days following today, compounding each account's daily rate on its balance and adding payroll deposits on their scheduled dates.

#### Scenario: Projection starts from current balances
- **WHEN** the projection tab is opened
- **THEN** day 1 SHALL start from the current sum of all account balances

#### Scenario: Daily compounding applied
- **WHEN** computing day N
- **THEN** the balance for day N SHALL equal the balance for day N-1 multiplied by `(1 + weightedDailyRate)`, plus any payroll deposit scheduled on day N

### Requirement: Key-milestone view
The projection tab SHALL include a view showing only the following milestone days: 1, 7, 15, 30, 45, 60, 90, 120, 150, 180, 270, 365. Each row SHALL show: day number, accumulated total balance, pure yield (balance minus total deposited), cumulative payroll deposits, and that day's yield.

#### Scenario: Milestone rows rendered
- **WHEN** the milestones view is selected
- **THEN** exactly those 12 milestone rows SHALL be displayed in ascending order

### Requirement: Day-by-day full table view
The projection tab SHALL include a toggle to show all 365 rows, one per day, with the same columns as the milestone view.

#### Scenario: Full table toggle
- **WHEN** the user switches to the day-by-day view
- **THEN** all 365 rows SHALL be rendered with correct values for each day

### Requirement: Projection columns
Each projection row (milestone or daily) SHALL contain:
- **Día**: day number
- **Saldo acumulado**: total balance on that day (green)
- **Rendimiento puro**: balance minus total principal deposited (purple)
- **Nómina acumulada**: cumulative payroll deposits through that day (yellow)
- **Rendimiento del día**: the yield earned specifically on that day (purple)

#### Scenario: Column values accuracy
- **WHEN** no payroll is configured
- **THEN** the nómina acumulada column SHALL show MXN 0.00 for all rows and pure yield SHALL equal total balance minus the initial balance

#### Scenario: Payroll deposit day
- **WHEN** a payroll deposit is scheduled on day N
- **THEN** day N's saldo acumulado SHALL include the deposit amount and nómina acumulada SHALL increase by the deposit amount
