# People & HR Base Manual Test Scenarios

## Summary

Use this checklist to manually test the People & HR Base in Airtable.

The tests validate:

- employee lifecycle records
- HR request intake and triage
- HR administration interface behavior
- confidential-case guardrails
- native Airtable MVP automations
- secure-document and HRIS boundaries
- privacy and no-sync guardrails

## Assumptions

- The base is `EDU Passport People & HR`.
- HR and approved leadership have base-level access.
- Ordinary employees use interface-only request submission and permitted status views where supported.
- Payroll, HRIS, and secure document systems remain authoritative outside Airtable.
- Airtable stores workflow status, approved operational metadata, identifiers, and access-controlled links only.
- Airtable does not store payroll calculations, compensation records, bank details, full identity documents, passwords, API keys, unrestricted medical/performance details, or confidential attachments.
- Airtable automations are native Airtable automations only.
- No cross-base sync is enabled.

## Interfaces

### HR Request Portal

Use this interface for employee and manager request submission.

Recommended pages:

- `New HR Request`
- `My HR Requests`
- `Request Detail`

Primary tables:

- `HR Requests`
- `Employees` for linked employee context only where permitted

### HR Administration

Use this interface for HR-owned request review and employee lifecycle administration.

Recommended pages:

- `Request Triage`
- `Urgent And Waiting`
- `Employee Lifecycle`
- `Confidential Cases`
- `Request Detail`

Primary tables:

- `Employees`
- `HR Requests`

## Automation Views To Verify

Create or verify these table views before testing automations.

| Table | View | Purpose |
| --- | --- | --- |
| `HR Requests` | `AUTOMATION - Submitted Or In Review HR Requests` | Requests that should appear in the new request digest. |
| `HR Requests` | `AUTOMATION - Due Soon Or Waiting HR Requests` | Waiting, due-soon, or overdue requests that need HR attention. |
| `HR Requests` | `Confidential Cases` | Confidential cases requiring restricted HR review. |

## Manual Test Scenarios

### 1. Employee Record Setup

**Purpose:** Confirm HR can create an employee lifecycle record without creating an Operations Hub Team Members table.

**Interface to test from:** `HR Administration` -> `Employee Lifecycle`

**Starting table:** `Employees`

**Setup data:**

- Use non-sensitive sample employee data only.
- Do not upload full identity documents or payroll details.

**Steps:**

1. Create an Employees record.
2. Fill `Employee Name`, `Employment Status`, `Work Email`, `Department`, `Manager`, `Start Date`, and `HR Owner`.
3. Add an access-controlled `External Payroll / HR Record URL` only if a safe test URL is available.
4. Save the record.
5. Confirm no Team Members table is created in the People & HR Base or Operations Hub.

**Expected result:**

- The employee record saves.
- The record appears in the correct Employee Lifecycle view.
- No payroll calculations, compensation records, bank details, or full identity documents are stored in Airtable.
- No Operations Hub Team Members table is created.

**Result:**

- [ ] Pass
- [ ] Fail

### 2. HR Request Submission

**Purpose:** Confirm an employee or manager can submit an HR request without opening the underlying base.

**Interface to test from:** `HR Request Portal` -> `New HR Request`

**Starting table:** `HR Requests`

**Setup data:**

- Use a non-sensitive request example.
- Link to a sample Employees record if appropriate.

**Steps:**

1. Create a new HR Request.
2. Set `Request Type` to `Employee Document` or `Employee Change`.
3. Link `Employee` if applicable.
4. Fill `Requester`, `Priority`, and `Details`.
5. Save the request.
6. Open `My HR Requests`.

**Expected result:**

- The request saves with a stable `Request ID`.
- `Submitted Date` is populated.
- The requester can see permitted request status.
- The requester cannot browse the Employees table, other employees' requests, or Confidential Notes.

**Result:**

- [ ] Pass
- [ ] Fail

### 3. HR Request Triage

**Purpose:** Confirm HR can triage, assign, and complete a normal HR request.

**Interface to test from:** `HR Administration` -> `Request Triage`

**Starting table:** `HR Requests`

**Setup data:**

- Use an HR Request with `Status = Submitted`.

**Steps:**

1. Open the submitted HR Request.
2. Set `HR Owner`.
3. Set `Due Date`.
4. Change `Status` to `In Review`.
5. Add safe operational context in `Details`.
6. Change `Status` to `Approved`, then `Completed`.

**Expected result:**

- HR can update owner, due date, priority, and status.
- The request moves through Submitted -> In Review -> Approved -> Completed.
- Confidential Notes remain restricted to HR and approved leadership.

**Result:**

- [ ] Pass
- [ ] Fail

### 4. Confidential Case Handling

**Purpose:** Confirm confidential HR cases are visible only to authorized HR/leadership users.

**Interface to test from:** `HR Administration` -> `Confidential Cases`

**Starting table:** `HR Requests`

**Setup data:**

- Use a non-sensitive fake confidential case.
- Do not enter real medical, performance, disciplinary, compensation, or identity details.

**Steps:**

1. Create an HR Request.
2. Set `Request Type` to `Confidential Case`.
3. Set `Priority`.
4. Add safe placeholder text in `Details`.
5. Add safe placeholder text in `Confidential Notes`.
6. Confirm the record appears in `Confidential Cases`.
7. Test with an ordinary employee or limited-access test user if available.

**Expected result:**

- HR and approved leadership can review the case.
- Ordinary employees cannot see Confidential Notes.
- Ordinary employees cannot browse other employees' requests.
- No confidential attachments or full identity documents are stored in Airtable.

**Result:**

- [ ] Pass
- [ ] Fail

### 5. Sanitized Operations Coordination

**Purpose:** Confirm HR can coordinate with another team without exposing employee case details.

**Interface to test from:** `HR Administration` plus Operations Hub task interface.

**Starting table:** `HR Requests`

**Setup data:**

- Use a non-sensitive onboarding or offboarding request.

**Steps:**

1. Open an HR Request that requires Operations or IT action.
2. Create a task in the Operations Hub.
3. Include only sanitized action wording.
4. Do not include employee case details, compensation, medical/performance information, confidential notes, secure links, or attachments.
5. Return to the HR Request and record that coordination was started.

**Expected result:**

- The Operations Hub task contains only sanitized coordination information.
- Sensitive HR details remain inside the People & HR Base or authoritative external systems.
- No cross-base sync is created.

**Result:**

- [ ] Pass
- [ ] Fail

### 6. New Request Digest

**Purpose:** Confirm the new request digest identifies active HR requests without exposing confidential details.

**Interface to test from:** Airtable Automations and `AUTOMATION - Submitted Or In Review HR Requests`

**Starting table:** `HR Requests`

**Setup data:**

- One HR Request with `Status = Submitted`.
- One HR Request with `Status = In Review`.
- One HR Request with `Status = Completed` as a control.

**Steps:**

1. Open the automation source view.
2. Confirm Submitted and In Review records appear.
3. Confirm Completed records do not appear.
4. Run or wait for `HR - New Request Digest`.
5. Review the notification content.

**Expected result:**

- Submitted and In Review requests are included.
- Completed requests are excluded.
- The notification does not include Details, Confidential Notes, Secure Document URL, identity documents, payroll data, medical/performance details, or attachments.
- The automation does not update request status.

**Result:**

- [ ] Pass
- [ ] Fail

### 7. Due Soon And Waiting Reminder

**Purpose:** Confirm due-soon, overdue, and waiting requests are surfaced for HR follow-up.

**Interface to test from:** Airtable Automations and `AUTOMATION - Due Soon Or Waiting HR Requests`

**Starting table:** `HR Requests`

**Setup data:**

- One request with `Status = Waiting`.
- One request with `Status = Submitted` and a due date inside the reminder window.
- One request with `Status = In Review` and an overdue due date.
- One request with `Status = Completed` as a control.

**Steps:**

1. Open the automation source view.
2. Confirm Waiting, due-soon, and overdue records appear.
3. Confirm Completed records do not appear.
4. Run or wait for `HR - Due Soon And Waiting Reminder`.
5. Review the reminder content.

**Expected result:**

- Waiting, due-soon, and overdue requests are included.
- Completed requests are excluded.
- Overdue records are clearly identifiable.
- The automation does not approve, reject, complete, cancel, or update records automatically.

**Result:**

- [ ] Pass
- [ ] Fail

### 8. Privacy And No-Sync Guardrails

**Purpose:** Confirm HR data stays private and does not leak into the Operations Hub.

**Interface to test from:** Airtable sharing/settings and Operations Hub spot check.

**Starting tables:** `Employees`, `HR Requests`

**Setup data:**

- Use existing non-sensitive test records.

**Steps:**

1. Confirm public sharing is disabled.
2. Confirm unrestricted invite links are disabled.
3. Confirm no cross-base sync is enabled.
4. Confirm Employees and HR Requests are not synced into the Operations Hub.
5. Confirm ordinary employees cannot browse Employees, other employees' requests, or Confidential Notes.
6. Search test records for payroll calculations, compensation records, bank details, full identity documents, passwords, API keys, unrestricted medical/performance details, and confidential attachments.

**Expected result:**

- No public share link exists.
- No unrestricted invite link exists.
- No cross-base sync exists.
- Ordinary employees see only permitted request context.
- No prohibited sensitive data is stored in Airtable.
- Operations Hub does not expose HR cases, confidential notes, compensation, medical/performance information, or identity documents.

**Result:**

- [ ] Pass
- [ ] Fail

## Test Summary

| Scenario | Result | Notes |
| --- | --- | --- |
| Employee record setup |  |  |
| HR request submission |  |  |
| HR request triage |  |  |
| Confidential case handling |  |  |
| Sanitized Operations coordination |  |  |
| New request digest |  |  |
| Due soon and waiting reminder |  |  |
| Privacy and no-sync guardrails |  |  |
