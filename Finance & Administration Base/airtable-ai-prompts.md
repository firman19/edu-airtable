# Airtable AI Prompts

Use these prompts with Airtable AI / Omni AI to create or revise the Finance & Administration Base.

Run the prompts in order. Review each result before continuing.

Source of truth: [Finance & Administration Base requirements](README.md).

## Base And Tables

```text
Create or revise an Airtable base named "EDU Passport Finance & Administration".

Purpose:
This base is for basic Finance and Administration MVP work: finance requests, monthly budget planning, summarized actuals, budget changes, compliance, contracts, registrations, and renewals.

Use exactly these tables:
- Finance Requests
- Budget Plans
- Budget Categories
- Budget Lines
- Compliance & Renewals

Keep the base simple. Do not create these tables:
- Operations
- Projects
- Tasks
- Contacts
- Opportunities
- Departments
- Vendors
- accounting transactions
- bank accounts
- document storage

Base rules:
- This is a private Finance MVP base. Do not place HR data in it.
- Department is a controlled single select maintained locally.
- Budget reporting currency is USD.
- Accounting, banking, tax, and secure-document systems remain authoritative outside Airtable.
- Store summarized monthly actuals, workflow data, references, and access-controlled URLs only.
- Never store credentials, card data, API keys, unrestricted identity documents, payment attachments, payroll, bank details, or transaction-level accounting records.
- Do not create cross-base synchronization.
- If a specified table or field already exists, revise it instead of creating a duplicate.

Create or revise these tables and fields.

1. Finance Requests
Use this table for purchase, expense, reimbursement, invoice, payment, budget-change, contract, and other finance/admin requests.

Fields:
- Request ID: autonumber or formula; stable primary identifier.
- Request Type: single select: Purchase, Expense, Reimbursement, Invoice, Payment, Budget Change, Contract, Other.
- Requester: collaborator or created-by.
- Vendor / Payee: single line text.
- Amount: currency.
- Currency: single select.
- Due Date: date.
- Approval Status: single select: Submitted, In Review, Approved, Rejected, Paid, Cancelled.
- Finance Owner: collaborator.
- Related Budget Line: link to one Budget Lines record; operationally required for Budget Change.
- Budget Adjustment Amount: USD currency; signed, positive to increase and negative to decrease.
- Approved Adjustment Value: currency formula:
  IF(
    AND(
      {Request Type} = "Budget Change",
      {Approval Status} = "Approved"
    ),
    {Budget Adjustment Amount},
    0
  )
- Accounting Reference: single line text.
- Secure Document URL: URL.

Request behavior:
- Keep approved Budget Change requests at Approved.
- Reserve Paid for payment-related requests.
- Rejected and Cancelled budget changes must contribute zero.

2. Budget Plans
Use this table for one Department x Fiscal Year x planning cycle.

Fields:
- Budget Plan Name: primary formula:
  {Department} & " - FY" & {Fiscal Year}
- Department: controlled single select.
- Fiscal Year: integer.
- Department Lead: collaborator.
- Finance Owner: collaborator.
- Currency: single select, USD only.
- Status: single select: Draft, Submitted, Approved, Active, Closed.
- Submitted Date: date.
- Approved Date: date.
- Approved By: collaborator.
- Budget Lines: backlink from Budget Lines.
- Total Baseline Plan: rollup Budget Lines -> Baseline Planned Amount, SUM(values).
- Total Approved Adjustments: rollup Budget Lines -> Approved Adjustments, SUM(values).
- Total Current Budget: rollup Budget Lines -> Current Budget, SUM(values).
- Total Committed: rollup Budget Lines -> Committed Amount, SUM(values).
- Total Actual Spend: rollup Budget Lines -> Actual Spend, SUM(values).
- Total Forecast: rollup Budget Lines -> Forecast Amount, SUM(values).
- Total Available Budget: rollup Budget Lines -> Available Budget, SUM(values).
- Total Variance: rollup Budget Lines -> Variance Amount, SUM(values).
- Notes: long text.

3. Budget Categories
Use this table for consistent company-wide budget categories.

Fields:
- Category Name: primary single line text.
- Category Code: unique single line text.
- Category Group: controlled single select.
- Active: checkbox.
- Accounting Mapping: single line text.
- Description: long text.
- Sort Order: integer.

Category behavior:
- The approved internal operator group controls categories.
- Only active categories should be available for new Budget Lines where Airtable supports linked-record filtering.

4. Budget Lines
Use this table for monthly budget planning and actuals. One record represents one Budget Plan x Budget Category x Month. Store the first day of the month.

Fields:
- Budget Line Name: primary formula:
  ARRAYJOIN({Department}) &
  " - " &
  ARRAYJOIN({Budget Category}) &
  " - " &
  DATETIME_FORMAT({Month}, "YYYY-MM")
- Budget Plan: link to one Budget Plans record.
- Budget Category: link to one Budget Categories record.
- Month: date.
- Quarter: formula:
  IF(
    {Month},
    "Q" & ROUNDUP(MONTH({Month}) / 3, 0)
  )
- Department: lookup Budget Plan -> Department.
- Department Lead: lookup Budget Plan -> Department Lead.
- Fiscal Year: lookup Budget Plan -> Fiscal Year.
- Currency: lookup Budget Plan -> Currency.
- Baseline Planned Amount: USD currency.
- Finance Requests: backlink from Finance Requests.
- Approved Adjustments: rollup Finance Requests -> Approved Adjustment Value, SUM(values).
- Current Budget: currency formula:
  {Baseline Planned Amount} + {Approved Adjustments}
- Committed Amount: USD currency.
- Actual Spend: USD currency.
- Forecast Amount: USD currency.
- Available Budget: currency formula:
  {Current Budget} - {Actual Spend} - {Committed Amount}
- Variance Amount: currency formula:
  {Current Budget} - {Actual Spend}
- Variance %: percent formula:
  IF(
    {Current Budget} = 0,
    BLANK(),
    {Variance Amount} / {Current Budget}
  )
- Over Budget Status: formula:
  IF(
    ({Actual Spend} + {Committed Amount}) > {Current Budget},
    "Over Budget",
    "Within Budget"
  )
- Close Status: single select: Open, Pending Reconciliation, Reconciled, Locked.
- Accounting Reference: single line text.
- Reconciled Date: date.
- Reconciled By: collaborator.
- Department Notes: long text.
- Finance Notes: long text.

Budget behavior:
- Monthly Budget Lines are the source for quarterly, annual, and YTD reporting.
- Do not create separate quarterly or annual budget amount fields or tables.
- During the MVP, the approved internal operator group can maintain planning, forecasts, approvals, adjustments, commitments, actuals, reconciliation, locking, and internal notes.
- Never overwrite an approved baseline. Use an approved Budget Change request.
- Actual Spend is one summarized monthly Department x Category value reconciled to accounting.

5. Compliance & Renewals
Use this table for contracts, registrations, licenses, insurance, tax filings, and other recurring obligations.

Fields:
- Item: primary single line text.
- Category: single select: Registration, License, Insurance, Contract, Tax, Filing, Other.
- Owner: collaborator.
- Authority / Vendor: single line text.
- Due Date: date.
- Status: single select: Upcoming, In Progress, Waiting, Completed, Overdue, Not Required.
- Last Completed Date: date.
- Secure Document URL: URL.

Create useful views without adding fields:
- Finance Requests: Submitted / In Review, Budget Changes, Payment Related, Due Soon.
- Budget Plans: Draft, Submitted, Approved / Active, Closed.
- Budget Categories: Active, Inactive.
- Budget Lines: Current Fiscal Year, Prior Month Open, Pending Reconciliation, Reconciled, Locked, Over Budget.
- Compliance & Renewals: Upcoming, Overdue, In Progress / Waiting, Completed.

Before finishing:
- Verify every formula, lookup, backlink, and rollup.
- Confirm no Budget Tracking table exists.
- Confirm no separate quarterly or annual budget table exists.
- Confirm no duplicate fields exist.
- Confirm no cross-base sync exists.
```

## Finance Request Portal

```text
Create or revise an interface named "Finance Request Portal" for the Finance & Administration Base.

Purpose:
This interface is for approved internal operators to submit and review basic finance/admin requests.

Use these tables:
- Finance Requests
- Budget Lines, for Budget Change context only

Keep the interface simple. Create only these pages:

1. New Request
Use the Finance Requests table.
Create a form or simple entry page for new finance/admin requests.
Show:
- Request Type
- Requester
- Vendor / Payee
- Amount
- Currency
- Due Date
- Related Budget Line
- Budget Adjustment Amount
- Secure Document URL

2. Request List
Use the Finance Requests table.
Show Submitted and In Review requests first.
Sort by Due Date, then Approval Status.
Show:
- Request ID
- Request Type
- Requester
- Vendor / Payee
- Amount
- Currency
- Due Date
- Approval Status
- Finance Owner
- Accounting Reference

3. Request Detail
Create a record detail or record review page for Finance Requests.
Show:
- Request ID
- Request Type
- Requester
- Vendor / Payee
- Amount
- Currency
- Due Date
- Approval Status
- Finance Owner
- Related Budget Line
- Budget Adjustment Amount
- Approved Adjustment Value
- Accounting Reference
- Secure Document URL

4. Budget Change Request
Use the Finance Requests table.
Show requests where Request Type is Budget Change.
Show:
- Request ID
- Approval Status
- Related Budget Line
- Budget Adjustment Amount
- Approved Adjustment Value
- Amount
- Currency
- Due Date
- Finance Owner

Interface behavior:
- Approved internal operators should be able to create and update Finance Requests.
- Budget Change requests should link to one Budget Line and use a signed Budget Adjustment Amount.
- Keep source documents in the external document system and store only access-controlled URLs or references when needed.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Budget Workspace

```text
Create or revise an interface named "Budget Workspace" for the Finance & Administration Base.

Purpose:
This interface is for approved internal operators to manage the basic MVP budget workflow: overview, planning, and budget changes.

Use these tables:
- Budget Plans
- Budget Categories
- Budget Lines
- Finance Requests, for Budget Change context only

Keep the interface simple. Create only these pages:

1. Budget Overview
Use the Budget Lines and Budget Plans tables.
Show approved and active budget summaries, monthly totals, YTD totals, variance, and over-budget lines.
Show:
- Budget Plan
- Department
- Fiscal Year
- Budget Category
- Month
- Quarter
- Baseline Planned Amount
- Approved Adjustments
- Current Budget
- Committed Amount
- Actual Spend
- Forecast Amount
- Available Budget
- Variance Amount
- Variance %
- Over Budget Status

2. Budget Planning
Use the Budget Plans and Budget Lines tables.
Show planning and forecast records for the current fiscal year first.
Show:
- Budget Plan Name
- Department
- Fiscal Year
- Status
- Finance Owner
- Budget Category
- Month
- Baseline Planned Amount
- Forecast Amount
- Department Notes
- Notes

3. Budget Changes
Use Finance Requests and Budget Lines.
Show Budget Change requests and the linked Budget Line context.
Show:
- Request ID
- Approval Status
- Related Budget Line
- Budget Adjustment Amount
- Approved Adjustment Value
- Current Budget
- Baseline Planned Amount
- Approved Adjustments
- Finance Owner
- Due Date

Interface behavior:
- Approved internal operators should be able to review and update budget planning, forecasts, notes, and Budget Change requests during the MVP.
- Quarterly, annual, and YTD reporting should come from monthly Budget Lines.
- Do not silently overwrite approved baselines; use Budget Change requests for post-approval changes.
- Do not create separate quarterly or annual budget tables.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Finance Admin

```text
Create or revise an interface named "Finance Admin" for the Finance & Administration Base.

Purpose:
This interface is for approved internal operators to handle basic request review, month close, compliance, and budget setup.

Use these tables:
- Finance Requests
- Budget Plans
- Budget Categories
- Budget Lines
- Compliance & Renewals

Keep the interface simple. Create only these pages:

1. Request Review
Use the Finance Requests table.
Show Submitted and In Review requests first.
Show:
- Request ID
- Request Type
- Requester
- Vendor / Payee
- Amount
- Currency
- Due Date
- Approval Status
- Finance Owner
- Accounting Reference

2. Month Close
Use the Budget Lines table.
Show records where Close Status is Open or Pending Reconciliation first.
Show:
- Budget Line Name
- Department
- Budget Category
- Month
- Actual Spend
- Committed Amount
- Accounting Reference
- Close Status
- Reconciled Date
- Reconciled By
- Finance Notes

3. Compliance & Renewals
Use the Compliance & Renewals table.
Show Upcoming, Overdue, In Progress, and Waiting records first.
Show:
- Item
- Category
- Owner
- Authority / Vendor
- Due Date
- Status
- Last Completed Date
- Secure Document URL

4. Budget Setup
Use the Budget Plans and Budget Categories tables.
Show active setup records first.
Show:
- Budget Plan Name
- Department
- Fiscal Year
- Status
- Finance Owner
- Category Name
- Category Code
- Category Group
- Active
- Accounting Mapping
- Sort Order

Interface behavior:
- Approved internal operators should be able to update request status, owner, due dates, monthly actuals, reconciliation status, compliance status, and budget setup records.
- Month Close should support Open -> Pending Reconciliation -> Reconciled -> Locked.
- Never show or import transaction-level accounting records, bank data, credentials, payroll, unrestricted identity/legal documents, or payment attachments.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Native Automations

```text
Create simple native Airtable automations for the Finance & Administration Base.

Purpose:
These automations should help the approved internal operator group review finance/admin work without creating noisy real-time alerts.

Use these tables:
- Finance Requests
- Budget Plans
- Budget Lines
- Compliance & Renewals

Keep automations simple. Create only these automations:

1. Finance - Daily Admin Digest
Schedule this automation daily at a documented approved time and timezone.

Find records for a concise review digest:
- Finance Requests where Approval Status is Submitted or In Review.
- Budget Plans where Status is Submitted.
- Budget Lines where Over Budget Status is Over Budget.
- Compliance & Renewals where Status is not Completed and not Not Required, and Due Date is within the approved reminder window or overdue.

Digest behavior:
- Notify the relevant Finance Owner when available, otherwise notify the designated fallback operator.
- Include compact grouped sections for requests, budget plans, over-budget lines, and compliance items.
- Include only record names, owner, department or category context, due date or month, status, amount fields needed for review, and record links.
- Direct operators to handle records from Finance Admin and Budget Workspace.

2. Finance - Monthly Close Reminder
Schedule this automation monthly on the fifth calendar day at a documented approved time and timezone.

Find Budget Lines where:
- Month is in the immediately previous calendar month.
- Close Status is Open or Pending Reconciliation.

Reminder behavior:
- Notify the Finance Owner when available, otherwise notify the designated fallback operator.
- Include Budget Line Name, Department, Budget Category, Month, Close Status, Accounting Reference, and record link.
- Ask operators to reconcile summarized actuals and move the line to Reconciled, then Locked.

Automation behavior:
- Use native Airtable automation actions only.
- Do not use scripts or external integration tools.
- Do not approve, reject, pay, reconcile, lock, or otherwise update records automatically.
- Do not modify baseline, adjustment, commitment, actual, formula, rollup, or reconciliation fields automatically.
- Do not include Finance Notes, Secure Document URL, bank data, transaction-level data, credentials, or confidential attachments in notifications.
- Do not create duplicate automations.
```

## Budget Change Verification

```text
Audit the approved Budget Change relationship in the Finance & Administration Base.

Purpose:
This is a formula and rollup check, not an automation.

Confirm:
- Finance Requests.Approved Adjustment Value returns Budget Adjustment Amount only for an Approved Budget Change; otherwise zero.
- Budget Lines.Approved Adjustments rolls up Approved Adjustment Value using SUM(values).
- Budget Lines.Current Budget equals Baseline Planned Amount plus Approved Adjustments.
- No automation copies an adjustment into Baseline Planned Amount or Approved Adjustments.
- Rejected or Cancelled changes contribute zero.
- Positive and negative signed adjustments both work.
- Approved Budget Change requests remain Approved, not Paid.

Verification behavior:
- Do not create an automation for approved adjustments.
- Keep approved adjustments formula and rollup based.
- Create fields only if the required formula, link, or rollup is missing.
- Do not create duplicate fields.
```

## Manual Security And Acceptance Checks

```text
Review the Finance & Administration Base before launch.

Purpose:
These checks keep the MVP private, simple, and safe while there is no dedicated Finance department yet.

Check these items:
- Keep the base private in the Corporate Services workspace.
- Use one small approved internal operator group while there is no dedicated Finance department.
- Let that group use Budget Workspace and Finance Admin during MVP setup.
- Keep public sharing and unrestricted invite links disabled.
- Do not store bank details, credentials, transaction-level accounting data, payment attachments, payroll, or unrestricted identity/legal documents.
- Confirm there is no cross-base sync.
- Test with non-sensitive sample records before enabling automations.
- Reconcile one monthly Department x Category sample to accounting without importing transactions.
- Confirm approved baselines cannot be silently overwritten.
- Revisit role-specific permissions when a dedicated Finance owner or department exists.

Review behavior:
- Do not create duplicate fields.
- If a suggested field or view does not exist and is not required for the MVP, skip it instead of adding complexity.
```