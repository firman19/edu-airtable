# Finance & Administration Base Manual Test Scenarios

## Summary

Use this checklist to manually test the Finance & Administration Base in Airtable.

The tests validate:

- request intake and review
- monthly budget planning and rollups
- budget-change formulas and rollups
- summarized actuals and month-close workflow
- compliance and renewal tracking
- native Airtable MVP automations
- privacy and no-sync guardrails

## Assumptions

- The base is `EDU Passport Finance & Administration`.
- The MVP uses one small approved internal operator group.
- Accounting, banking, tax, and secure document systems remain authoritative outside Airtable.
- Airtable stores summarized monthly actuals, workflow status, metadata, references, and access-controlled URLs only.
- Airtable does not store transaction-level accounting records, bank details, credentials, payment attachments, payroll, or unrestricted identity/legal documents.
- Airtable automations are native Airtable automations only.
- No cross-base sync is enabled.

## Interfaces

### Finance Request Portal

Use this interface for basic request submission and review.

Recommended pages:

- `New Request`
- `Request List`
- `Request Detail`
- `Budget Change Request`

Primary tables:

- `Finance Requests`
- `Budget Lines` for Budget Change context only

### Budget Workspace

Use this interface for budget overview, planning, and budget changes.

Recommended pages:

- `Budget Overview`
- `Budget Planning`
- `Budget Changes`

Primary tables:

- `Budget Plans`
- `Budget Categories`
- `Budget Lines`
- `Finance Requests` for Budget Change context only

### Finance Admin

Use this interface for request review, month close, compliance, and budget setup.

Recommended pages:

- `Request Review`
- `Month Close`
- `Compliance & Renewals`
- `Budget Setup`

Primary tables:

- `Finance Requests`
- `Budget Plans`
- `Budget Categories`
- `Budget Lines`
- `Compliance & Renewals`

## Automation Views To Verify

Create or verify these table views before testing automations.

| Table | View | Purpose |
| --- | --- | --- |
| `Finance Requests` | `AUTOMATION - Submitted Or In Review Requests` | Requests that should appear in the daily digest. |
| `Budget Plans` | `AUTOMATION - Submitted Budget Plans` | Submitted plans that need review. |
| `Budget Lines` | `AUTOMATION - Over Budget Lines` | Budget lines that should appear in the daily digest. |
| `Budget Lines` | `AUTOMATION - Prior Month Open Close` | Prior-month lines still Open or Pending Reconciliation. |
| `Compliance & Renewals` | `AUTOMATION - Due Or Overdue Compliance` | Compliance items due soon or overdue. |

## Manual Test Scenarios

### 1. Finance Request Intake

**Purpose:** Confirm a basic finance request can be submitted and reviewed.

**Interface to test from:** `Finance Request Portal` -> `New Request`

**Starting table:** `Finance Requests`

**Setup data:**

- Use non-sensitive sample data only.
- Prepare a sample vendor/payee name.
- Do not attach payment documents or banking details.

**Steps:**

1. Create a Finance Request.
2. Set `Request Type` to `Purchase`.
3. Fill `Requester`, `Vendor / Payee`, `Amount`, `Currency`, and `Due Date`.
4. Set `Approval Status` to `Submitted`.
5. Open `Finance Admin` -> `Request Review`.
6. Change `Approval Status` to `In Review`.
7. Assign `Finance Owner`.

**Expected result:**

- The request saves with a stable `Request ID`.
- The request appears in `Request List` and `Request Review`.
- No bank details, transaction records, or payment attachments are stored in Airtable.

**Result:**

- [ ] Pass
- [ ] Fail

### 2. Budget Plan And Monthly Lines

**Purpose:** Confirm monthly Budget Lines roll up to a Budget Plan.

**Interface to test from:** `Budget Workspace` -> `Budget Planning`

**Starting tables:** `Budget Plans`, `Budget Categories`, `Budget Lines`

**Setup data:**

- Create or choose one active Budget Category.
- Use USD for the Budget Plan.

**Steps:**

1. Create a Budget Plan for one department and fiscal year.
2. Set Status to `Draft`.
3. Create at least two monthly Budget Lines linked to the plan and category.
4. Set `Month` to the first day of each month.
5. Enter `Baseline Planned Amount` on each Budget Line.
6. Open the Budget Plan rollup fields.

**Expected result:**

- Budget Lines link to the Budget Plan.
- `Quarter` is calculated from `Month`.
- `Total Baseline Plan` rolls up monthly baseline amounts.
- No separate quarterly or annual budget records are required.

**Result:**

- [ ] Pass
- [ ] Fail

### 3. Budget Change Approval

**Purpose:** Confirm approved Budget Change requests adjust Current Budget without overwriting the baseline.

**Interface to test from:** `Budget Workspace` -> `Budget Changes`

**Starting tables:** `Finance Requests`, `Budget Lines`

**Setup data:**

- Use an existing Budget Line with a Baseline Planned Amount.

**Steps:**

1. Create a Finance Request.
2. Set `Request Type` to `Budget Change`.
3. Link `Related Budget Line`.
4. Enter a positive `Budget Adjustment Amount`.
5. Set `Approval Status` to `Approved`.
6. Check the linked Budget Line.
7. Repeat with a negative adjustment.
8. Create one rejected Budget Change as a control.

**Expected result:**

- Approved positive and negative changes appear in `Approved Adjustments`.
- `Current Budget` equals `Baseline Planned Amount + Approved Adjustments`.
- Rejected or Cancelled changes contribute zero.
- `Baseline Planned Amount` is not overwritten.

**Result:**

- [ ] Pass
- [ ] Fail

### 4. Month Close With Summarized Actuals

**Purpose:** Confirm operators can enter summarized actuals and reconcile a month without importing transactions.

**Interface to test from:** `Finance Admin` -> `Month Close`

**Starting table:** `Budget Lines`

**Setup data:**

- Use an existing prior-month Budget Line.
- Prepare a non-sensitive accounting reference.

**Steps:**

1. Set `Close Status` to `Open`.
2. Enter `Actual Spend`.
3. Enter `Committed Amount` if applicable.
4. Add `Accounting Reference`.
5. Change `Close Status` to `Pending Reconciliation`.
6. Fill `Reconciled Date` and `Reconciled By`.
7. Change `Close Status` to `Reconciled`, then `Locked`.

**Expected result:**

- `Available Budget`, `Variance Amount`, `Variance %`, and `Over Budget Status` calculate correctly.
- The record can move through Open -> Pending Reconciliation -> Reconciled -> Locked.
- No transaction-level accounting records or bank data are imported.

**Result:**

- [ ] Pass
- [ ] Fail

### 5. Compliance And Renewals Tracking

**Purpose:** Confirm compliance obligations can be tracked from upcoming through completion.

**Interface to test from:** `Finance Admin` -> `Compliance & Renewals`

**Starting table:** `Compliance & Renewals`

**Setup data:**

- Use a non-sensitive sample compliance item.

**Steps:**

1. Create a Compliance & Renewals record.
2. Set Category, Owner, Authority / Vendor, Due Date, and Status.
3. Set one sample to `Upcoming`.
4. Set one sample to `Overdue`.
5. Update one sample to `Completed` and fill `Last Completed Date`.

**Expected result:**

- Upcoming and overdue items are visible in the interface.
- Completed items can be recorded.
- Secure document links are access-controlled references only.

**Result:**

- [ ] Pass
- [ ] Fail

### 6. Daily Admin Digest

**Purpose:** Confirm the daily digest identifies active Finance review items.

**Interface to test from:** Airtable Automations and source table views.

**Starting tables:** `Finance Requests`, `Budget Plans`, `Budget Lines`, `Compliance & Renewals`

**Setup data:**

- One Finance Request with `Approval Status = Submitted`.
- One Finance Request with `Approval Status = In Review`.
- One Budget Plan with `Status = Submitted`.
- One Budget Line with `Over Budget Status = Over Budget`.
- One due or overdue Compliance & Renewals record.
- One completed Compliance & Renewals record as a control.

**Steps:**

1. Open the automation source views.
2. Confirm active records appear in the relevant views.
3. Run or wait for `Finance - Daily Admin Digest`.
4. Review the notification content.

**Expected result:**

- Active review items are included.
- Completed compliance records are excluded.
- The digest does not include Finance Notes, secure links, credentials, banking data, transaction-level data, or confidential attachments.
- The automation does not update approval, payment, reconciliation, or lock statuses.

**Result:**

- [ ] Pass
- [ ] Fail

### 7. Monthly Close Reminder

**Purpose:** Confirm the fifth-day reminder identifies unreconciled prior-month Budget Lines.

**Interface to test from:** Airtable Automations and `AUTOMATION - Prior Month Open Close`

**Starting table:** `Budget Lines`

**Setup data:**

- One prior-month Budget Line with `Close Status = Open`.
- One prior-month Budget Line with `Close Status = Pending Reconciliation`.
- One prior-month Budget Line with `Close Status = Reconciled`.
- One prior-month Budget Line with `Close Status = Locked`.

**Steps:**

1. Open `AUTOMATION - Prior Month Open Close`.
2. Confirm only Open and Pending Reconciliation records appear.
3. Run or wait for `Finance - Monthly Close Reminder`.
4. Review the reminder content.

**Expected result:**

- Only Open and Pending Reconciliation records are included.
- Reconciled and Locked records are excluded.
- The automation does not change `Actual Spend` or `Close Status`.

**Result:**

- [ ] Pass
- [ ] Fail

### 8. Privacy And No-Sync Guardrails

**Purpose:** Confirm Finance data stays private and does not leak into the Operations Hub.

**Interface to test from:** Airtable sharing/settings and Operations Hub spot check.

**Starting tables:** All Finance & Administration tables.

**Setup data:**

- Use existing non-sensitive test records.

**Steps:**

1. Confirm public sharing is disabled.
2. Confirm unrestricted invite links are disabled.
3. Confirm no cross-base sync is enabled.
4. Confirm no Finance tables are synced into the Operations Hub.
5. Search test records for bank details, credentials, payment attachments, payroll, unrestricted identity/legal documents, and transaction-level accounting rows.

**Expected result:**

- No public share link exists.
- No unrestricted invite link exists.
- No cross-base sync exists.
- No sensitive prohibited data is stored in Airtable.
- Operations Hub does not expose Finance amounts, confidential notes, banking data, payment attachments, restricted contracts, or tax records.

**Result:**

- [ ] Pass
- [ ] Fail

## Test Summary

| Scenario | Result | Notes |
| --- | --- | --- |
| Finance request intake |  |  |
| Budget plan and monthly lines |  |  |
| Budget change approval |  |  |
| Month close with summarized actuals |  |  |
| Compliance and renewals tracking |  |  |
| Daily admin digest |  |  |
| Monthly close reminder |  |  |
| Privacy and no-sync guardrails |  |  |
