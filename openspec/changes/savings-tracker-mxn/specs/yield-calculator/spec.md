## ADDED Requirements

### Requirement: Daily rate computation
The system SHALL compute each account's daily equivalent rate using the formula `dailyRate = (1 + annualRate / 100) ^ (1 / 365) - 1`.

#### Scenario: Rate calculation accuracy
- **WHEN** an account has an annual rate of 12%
- **THEN** the computed daily rate SHALL equal `(1.12)^(1/365) - 1` ≈ 0.031% per day

### Requirement: Per-account daily yield
The system SHALL compute each account's daily yield as `balance × dailyRate`, rounded to two decimal places for display.

#### Scenario: Daily yield display
- **WHEN** an account has a balance of MXN 10,000 and an annual rate of 12%
- **THEN** the displayed daily yield SHALL equal `10000 × ((1.12)^(1/365) - 1)`

### Requirement: Consolidated balance
The system SHALL compute and display the sum of all account balances as the total consolidated balance.

#### Scenario: Multi-account total
- **WHEN** the user has three accounts with balances of MXN 5,000, MXN 10,000, and MXN 15,000
- **THEN** the dashboard SHALL display a total of MXN 30,000

### Requirement: Weighted average yield rate
The system SHALL compute the portfolio's weighted average annual rate as `Σ(balance_i × rate_i) / Σ(balance_i)`.

#### Scenario: Weighted rate calculation
- **WHEN** account A has MXN 10,000 at 10% and account B has MXN 10,000 at 14%
- **THEN** the weighted average rate SHALL be 12%

#### Scenario: Single account
- **WHEN** only one account exists
- **THEN** the weighted average rate SHALL equal that account's annual rate

### Requirement: Estimated total daily yield
The system SHALL display the sum of all per-account daily yields as the estimated total daily yield.

#### Scenario: Total daily yield
- **WHEN** two accounts each yield MXN 5.00 per day
- **THEN** the dashboard SHALL show an estimated daily yield of MXN 10.00
