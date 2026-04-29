## ADDED Requirements

### Requirement: Add savings account
The system SHALL allow the user to create a new savings account by providing an entity name, current balance in MXN, and annual yield rate as a percentage.

#### Scenario: Successful account creation
- **WHEN** the user fills in entity name, balance, and annual rate and submits the form
- **THEN** the account SHALL be saved to `localStorage` under the key `savings_accounts` and appear immediately in the account list

#### Scenario: Missing required field
- **WHEN** the user submits the form with any field empty or invalid
- **THEN** the system SHALL prevent submission and highlight the invalid field

### Requirement: Edit savings account inline
The system SHALL allow the user to edit an existing account's name, balance, or rate directly in the account list without navigating to a separate page.

#### Scenario: Inline edit commit
- **WHEN** the user modifies a field value in the account row and confirms
- **THEN** the updated value SHALL be persisted to `localStorage` and all derived metrics SHALL recalculate immediately

#### Scenario: Inline edit cancel
- **WHEN** the user cancels an in-progress edit
- **THEN** the field SHALL revert to its previous value and nothing SHALL be written to storage

### Requirement: Delete savings account
The system SHALL allow the user to permanently remove a savings account.

#### Scenario: Successful deletion
- **WHEN** the user activates the delete action for an account
- **THEN** the account SHALL be removed from `localStorage` and the dashboard SHALL update all totals immediately

### Requirement: Persist accounts across sessions
The system SHALL save all accounts to `localStorage` so they survive page reloads and browser restarts.

#### Scenario: Reload persistence
- **WHEN** the user reloads the page
- **THEN** all previously saved accounts SHALL appear with their last-saved values
