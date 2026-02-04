# User Stories & Acceptance Criteria
**Project:** Polaris – Claims Modernisation
**Sprint:** 1 (Foundation & Data Migration)

---

## Story 1: Citizen Claim Submission
**As a** Citizen applying for financial support,
**I want to** save my application progress and return to it later,
**So that** I do not lose my data if I need to find supporting documents.

### Acceptance Criteria 1: Successful Save
* **Given** the user is on the "Financial Details" section of the claim form
* **And** the user has entered valid data into all mandatory fields
* **When** they click the "Save and Exit" button
* **Then** the system should store the current application state in the cloud database
* **And** display a "Progress Saved" reference code to the user.

### Acceptance Criteria 2: Validation Error
* **Given** the user has left the "National Insurance Number" (NINO) field blank
* **When** they attempt to click "Save and Exit"
* **Then** the system should prevent the save action
* **And** highlight the missing field with the error message: "Standard DWP-GOV-UK Error: NINO is required."

---

## Story 2: Automated Savings Threshold Check
**As a** Claims Processing Engine,
**I want to** automatically flag applications where declared savings exceed the statutory threshold (£16,000),
**So that** Case Managers do not waste time manually reviewing ineligible claims.

### Acceptance Criteria 1: Above Threshold Rejection
* **Given** a new claim payload is received via API
* **And** the `total_savings` data field value is greater than £16,000
* **When** the "Eligibility Rules Service" processes the claim
* **Then** the claim status should automatically update to `AUTO_REJECT`
* **And** a notification should be sent to the claimant explaining the capital limits.

---

## Story 3: Legacy Historical Data View
**As a** DWP Case Manager,
**I want to** view a read-only history of the claimant's previous interactions from the Legacy Mainframe system within the new web portal,
**So that** I can make informed decisions without logging into two separate screens.

### Acceptance Criteria 1: Data Federation
* **Given** the Case Manager is viewing a Claimant Profile in the new portal
* **When** they navigate to the "History" tab
* **Then** the system should query the Legacy Mainframe interface
* **And** display the last 5 years of case notes in reverse chronological order.

### Acceptance Criteria 2: Read-Only Integrity
* **Given** the legacy notes are displayed
* **When** the Case Manager attempts to edit a historical note
* **Then** the field should be "Read Only" / Greyed out
* **And** no changes shall be written back to the legacy database.
