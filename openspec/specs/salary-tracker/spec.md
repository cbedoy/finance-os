## ADDED Requirements

### Requirement: Configure biweekly salary
The system SHALL allow the user to enter a biweekly (quincenal) payroll amount in MXN and a first deposit date.

#### Scenario: Salary configuration saved
- **WHEN** the user enters a payroll amount and start date and saves
- **THEN** the configuration SHALL be persisted in `localStorage` under the key `salary_config`

#### Scenario: Salary configuration loaded on startup
- **WHEN** the page loads and a salary config exists in `localStorage`
- **THEN** the salary tab SHALL display the previously saved amount and start date

### Requirement: Biweekly deposit schedule derivation
The system SHALL derive future deposit dates by adding 14 calendar days to each prior deposit date, starting from the configured first deposit date.

#### Scenario: Deposit dates within 365 days
- **WHEN** the start date is set and the projection runs
- **THEN** all deposit dates falling within the 365-day projection window SHALL be identified correctly, approximately every 14 days

### Requirement: Cumulative payroll deposits in projection
The system SHALL track and display the running total of all payroll deposits added through each day of the 365-day projection.

#### Scenario: Deposit accumulation
- **WHEN** a deposit date falls on or before a given projection day
- **THEN** that deposit's amount SHALL be included in the cumulative payroll total for that day and all subsequent days
