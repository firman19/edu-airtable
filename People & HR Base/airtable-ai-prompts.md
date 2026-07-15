# Airtable AI Prompts

Use these prompts with Airtable AI / Omni AI to create or revise the People & HR Base.

Run the prompts in order. Review each result before continuing.

Source of truth: [People & HR Base requirements](README.md).

## Base And Tables

```text
Create or revise an Airtable base named "EDU Passport People & HR".

Purpose:
This base is for restricted People and HR workflows: employee lifecycle administration, recruitment, onboarding, offboarding, leave, employee document requests, employee-change requests, and confidential HR cases.

Use exactly these tables:
- Employees
- HR Requests

Keep the base simple. Do not create these tables:
- Operations
- Projects
- Tasks
- Contacts
- Opportunities
- Departments
- Team Members
- Payroll calculations
- Compensation records
- Bank accounts
- Document storage

Base rules:
- This is a restricted HR base. Do not place Finance data in it.
- Payroll, HRIS, and secure-document systems remain authoritative outside Airtable.
- Airtable stores workflow status, approved operational metadata, identifiers, and access-controlled links only.
- Never store banking credentials, full identity documents, passwords, API keys, payroll calculations, authoritative compensation records, unrestricted medical/performance details, or confidential attachments.
- Do not create cross-base synchronization.
- If a specified table or field already exists, revise it instead of creating a duplicate.

Create or revise these tables and fields.

1. Employees
Use this table for HR-specific employee lifecycle references.

Fields:
- Employee Name: primary single line text.
- Employment Status: single select: Candidate, Active, Leave, Exiting, Former.
- Work Email: email.
- Department: single select or text; no cross-base sync at launch.
- Manager: single line text or collaborator.
- Start Date: date.
- End Date: date.
- HR Owner: collaborator.
- External Payroll / HR Record URL: URL.

Employee behavior:
- Employees is the approved HR-specific exception to the deferred Operations Hub Team Members table.
- Do not sync this table into the Operations Hub.
- Use External Payroll / HR Record URL only for access-controlled source-system references.

2. HR Requests
Use this table for recruitment, onboarding, offboarding, leave, document, employee-change, confidential case, and other HR requests.

Fields:
- Request ID: autonumber or formula; stable primary identifier.
- Request Type: single select: Recruitment, Onboarding, Offboarding, Leave, Employee Document, Employee Change, Confidential Case, Other.
- Employee: linked record to Employees; required when the request concerns an employee.
- Requester: collaborator or created-by.
- HR Owner: collaborator.
- Status: single select: Submitted, In Review, Waiting, Approved, Rejected, Completed, Cancelled.
- Priority: single select: Low, Normal, High, Urgent.
- Submitted Date: created time.
- Due Date: date.
- Details: long text.
- Confidential Notes: long text.
- Secure Document URL: URL.

Request behavior:
- Manage the request lifecycle on HR Requests.
- Do not create a general HR Tasks table.
- Create only sanitized coordination Tasks in the Operations Hub when another department must act.
- Keep Confidential Notes visible only to HR and approved leadership where Airtable permissions support it.

Create useful views without adding fields:
- Employees: Candidates, Active, Leave, Exiting, Former.
- HR Requests: Submitted / In Review, Waiting, Urgent, Due Soon, Completed, Confidential Cases.

Before finishing:
- Confirm no Team Members table exists in this base.
- Confirm no payroll calculation, compensation, bank-account, or document-storage table exists.
- Confirm no duplicate fields exist.
- Confirm no cross-base sync exists.
```

## HR Request Portal

```text
Create or revise an interface named "HR Request Portal" for the People & HR Base.

Purpose:
This interface is for employees and managers to submit HR requests and see permitted request status.

Use these tables:
- HR Requests
- Employees, for linked employee context only where permitted

Keep the interface simple. Create only these pages:

1. New HR Request
Use the HR Requests table.
Create a form or simple entry page for new HR requests.
Show:
- Request Type
- Employee
- Requester
- Priority
- Details
- Secure Document URL

2. My HR Requests
Use the HR Requests table.
Show the requester's permitted submitted requests where Airtable permissions support it.
Show:
- Request ID
- Request Type
- Employee
- Status
- Priority
- Submitted Date
- Due Date
- HR Owner

3. Request Detail
Create a record detail or record review page for HR Requests.
Show permitted non-confidential status context:
- Request ID
- Request Type
- Employee
- Requester
- Status
- Priority
- Submitted Date
- Due Date
- HR Owner
- Details, only where appropriate
- Secure Document URL, only where appropriate

Interface behavior:
- Employees and managers should be able to submit HR Requests without opening the underlying base.
- Ordinary employees should not browse the Employees table, other employees' requests, or Confidential Notes.
- Keep source documents in the secure document system and store only access-controlled URLs or references when needed.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## HR Administration

```text
Create or revise an interface named "HR Administration" for the People & HR Base.

Purpose:
This interface is for HR and approved leadership to triage, assign, review, and complete HR work.

Use these tables:
- Employees
- HR Requests

Keep the interface simple. Create only these pages:

1. Request Triage
Use the HR Requests table.
Show Submitted and In Review requests first.
Show:
- Request ID
- Request Type
- Employee
- Requester
- Status
- Priority
- Submitted Date
- Due Date
- HR Owner

2. Urgent And Waiting
Use the HR Requests table.
Show urgent, high-priority, waiting, and overdue requests first.
Show:
- Request ID
- Request Type
- Employee
- Status
- Priority
- Due Date
- HR Owner
- Details

3. Employee Lifecycle
Use the Employees table.
Show Candidate, Active, Leave, Exiting, and Former employees.
Show:
- Employee Name
- Employment Status
- Work Email
- Department
- Manager
- Start Date
- End Date
- HR Owner
- External Payroll / HR Record URL

4. Confidential Cases
Use the HR Requests table.
Show requests where Request Type is Confidential Case.
Show:
- Request ID
- Employee
- Requester
- Status
- Priority
- Due Date
- HR Owner
- Details
- Confidential Notes
- Secure Document URL

5. Request Detail
Create a record detail or record review page for HR Requests.
Show:
- Request ID
- Request Type
- Employee
- Requester
- HR Owner
- Status
- Priority
- Submitted Date
- Due Date
- Details
- Confidential Notes
- Secure Document URL

Interface behavior:
- HR and approved leadership should be able to triage new requests, assign HR owners, update due dates, update approvals, and complete requests.
- HR and approved leadership can open access-controlled payroll, HRIS, or document-system links.
- Do not expose confidential HR notes or employee cases to ordinary employees.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Native Automations

```text
Create simple native Airtable automations for the People & HR Base.

Purpose:
These automations should help HR and approved leadership review HR work without exposing confidential details.

Use these tables:
- HR Requests

Keep automations simple. Create only these automations:

1. HR - New Request Digest
Schedule this automation daily at a documented approved time and timezone.

Find HR Requests where:
- Status is Submitted or In Review.

Digest behavior:
- Notify the HR Owner when available, otherwise notify the designated HR fallback.
- Include compact grouped sections for new and in-review requests.
- Include Request ID, Request Type, Status, Priority, Due Date, HR Owner, and record link.
- Do not include Details, Confidential Notes, Secure Document URL, identity documents, payroll data, medical/performance details, or attachments in the notification.

2. HR - Due Soon And Waiting Reminder
Schedule this automation daily at a documented approved time and timezone.

Find HR Requests where:
- Status is Waiting, Submitted, or In Review.
- Due Date is within the approved reminder window or overdue.

Reminder behavior:
- Notify the HR Owner when available, otherwise notify the designated HR fallback.
- Include Request ID, Request Type, Status, Priority, Due Date, HR Owner, and record link.
- Clearly identify overdue records.

Automation behavior:
- Use native Airtable automation actions only.
- Do not use scripts or external integration tools.
- Do not approve, reject, complete, cancel, or otherwise update records automatically.
- Do not create Operations Hub Tasks automatically.
- Do not include confidential notes, secure links, identity documents, payroll data, medical/performance details, or attachments in notifications.
- Do not create duplicate automations.
```

## Manual Security And Acceptance Checks

```text
Review the People & HR Base before launch.

Purpose:
These checks keep HR workflows private and prevent sensitive employee information from leaking into the Operations Hub.

Check these items:
- Keep the base in the restricted Corporate Services workspace.
- Limit base-level access to HR and approved leadership.
- Give ordinary employees interface-only access to request submission and permitted request status where supported.
- Disable public sharing and unrestricted invite links.
- Confirm ordinary employees cannot browse Employees, other employees' requests, or Confidential Notes.
- Confirm payroll, HRIS, and secure document systems remain authoritative.
- Confirm no payroll calculations, compensation records, bank details, full identity documents, passwords, API keys, or unrestricted confidential attachments are stored in Airtable.
- Confirm no cross-base sync exists.
- Test with non-sensitive sample records before enabling automations.
- Confirm any Operations Hub coordination Task is sanitized and contains no employee case details, compensation, medical/performance information, or confidential attachments.
- Remove a test user from approved access and confirm their HR visibility is removed.

Review behavior:
- Do not create duplicate fields.
- If a suggested field or view does not exist and is not required for the MVP, skip it instead of adding complexity.
```
