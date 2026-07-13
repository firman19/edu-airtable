# Care & Sales Base Manual Test Scenarios

## Summary

Use this checklist to manually test the Care & Sales Base in Airtable.

The tests validate:

- table relationships
- handoff fields
- Care and Sales interface behavior
- native Airtable v1 automations
- simple guardrails between Care-owned context and Sales-owned pipeline work

## Assumptions

- The base is the `Care & Sales Base`.
- Sales mainly updates `Opportunities`.
- Care mainly updates `Tickets & Care Pipeline`, `Scraped Feeds`, and `Customer Feedback`.
- `Sales Handoff Status` exists on Care-side source tables.
- `opportunities` is the existing linked-record field from Care source tables to `Opportunities`.
- Airtable automations are native Airtable automations only.
- External integrations such as Brevo, WhatsApp, EDU Inbox, and platform sync are not part of these tests.

## Opportunity Stage Options

`Opportunities.Stage` should use these options:

| Stage | Meaning |
| --- | --- |
| `New` | Opportunity was created and Sales has not fully reviewed it yet. |
| `Qualified` | Sales agrees this is worth pursuing. |
| `Discovery` | Sales is learning the need, budget, timing, decision maker, or context. |
| `Proposal` | Sales has sent pricing, offer, package, or next commercial option. |
| `Negotiation` | Customer is discussing details, price, scope, timing, or objections. |
| `Won` | Customer agreed or converted. |
| `Lost` | Opportunity is closed unsuccessfully. |
| `Nurture` | Not ready now, but worth keeping warm. |

## Care Interfaces

### Care Service Desk

Use this interface for support and service work.

Recommended pages:

- `My Tickets`
- `Urgent Tickets`
- `Upsell Potential`
- `Ticket Detail`

Primary tables:

- `Tickets & Care Pipeline`
- `Contacts`
- `Opportunities` for linked sales context only

### Scraped Feeds Review

Use this interface for reviewing external market signals.

Recommended pages:

- `New Feeds`
- `Needs Review`
- `Ready for Sales`
- `Reviewed Feeds`
- `Feed Detail`

Primary tables:

- `Scraped Feeds`
- `Contacts`
- `Opportunities` for linked sales context only

### Customer Feedback Review

Use this interface for reviewing customer comments, satisfaction signals, buying intent, and churn risk.

Recommended pages:

- `New Feedback`
- `Needs Review`
- `Ready for Sales`
- `Reviewed Feedback`
- `Feedback Detail`

Primary tables:

- `Customer Feedback`
- `Contacts`
- `Opportunities` for linked sales context only

## Sales Interface

### Sales / Account Management

Use this interface for Sales-owned pipeline work and Care handoff review.

Recommended pages:

- `My Opportunities`
- `Pipeline Board`
- `Sales Handoffs`
- `Contact Context`

Primary tables:

- `Opportunities`
- `Contacts`
- `Tickets & Care Pipeline` for handoff context only
- `Scraped Feeds` for handoff context only
- `Customer Feedback` for handoff context only

## Automation Views To Verify

Create dedicated automation views before testing automations.

| Table | View | Purpose |
| --- | --- | --- |
| `Tickets & Care Pipeline` | `AUTOMATION - Sales Ready Ticket Upsells` | Tickets ready to become opportunities. |
| `Scraped Feeds` | `AUTOMATION - Sales Ready Scraped Feeds` | Scraped leads ready to become opportunities. |
| `Customer Feedback` | `AUTOMATION - Sales Ready Customer Feedback` | Feedback records ready to become opportunities. |
| `Opportunities` | `AUTOMATION - Overdue Next Steps` | Open opportunities with overdue follow-up. |
| `Opportunities` | `Lost Opportunities Missing Lost Reason` | Closed lost opportunities missing reason. |

## Manual Test Scenarios

### 1. Ticket Upsell Handoff to Opportunity

**Purpose:** Confirm a Care ticket with upsell potential can become a linked Sales opportunity.

**Interface to test from:** `Care Service Desk` -> `Upsell Potential`

**Starting table:** `Tickets & Care Pipeline`

**Setup data:**

- Create or choose a `Contact`.
- Create a ticket linked to that contact.
- Set `upsell potential` to checked.
- Set `Sales Handoff Status` to `Ready for Sales`.
- Leave `opportunities` empty.

**Steps:**

1. Save the ticket.
2. Confirm the ticket appears in `AUTOMATION - Sales Ready Ticket Upsells`.
3. Run or wait for the native automation.
4. Open the created `Opportunities` record.
5. Open the source ticket again.

**Expected result:**

- One new Opportunity is created.
- Opportunity `Stage` is `New`.
- Opportunity links to the same contact.
- Opportunity source identifies the ticket or care upsell.
- Ticket `opportunities` links to the new Opportunity.
- Ticket `Sales Handoff Status` becomes `Handoff Created`.

**Result:**

- [ ] Pass
- [ ] Fail

### 2. Scraped Feed Handoff to Opportunity

**Purpose:** Confirm a reviewed scraped feed can become a linked Sales opportunity.

**Interface to test from:** `Scraped Feeds Review` -> `Ready for Sales`

**Starting table:** `Scraped Feeds`

**Setup data:**

- Create or choose a `Contact`.
- Create a scraped feed record with source details.
- Link or identify the matched contact.
- Set `Sales Handoff Status` to `Ready for Sales`.
- Leave `opportunities` empty.

**Steps:**

1. Save the scraped feed record.
2. Confirm it appears in `AUTOMATION - Sales Ready Scraped Feeds`.
3. Run or wait for the native automation.
4. Open the created Opportunity.
5. Open the source scraped feed again.

**Expected result:**

- One new Opportunity is created.
- Opportunity `Stage` is `New`.
- Opportunity source is `Scraped Feed`.
- Opportunity links to the matched contact.
- Scraped feed `opportunities` links to the new Opportunity.
- Scraped feed `Sales Handoff Status` becomes `Handoff Created`.

**Result:**

- [ ] Pass
- [ ] Fail

### 3. Customer Feedback Handoff to Opportunity

**Purpose:** Confirm sales-relevant customer feedback can become a linked Sales opportunity.

**Interface to test from:** `Customer Feedback Review` -> `Ready for Sales`

**Starting table:** `Customer Feedback`

**Setup data:**

- Create or choose a `Contact`.
- Create customer feedback that shows buying intent, expansion potential, or renewal risk.
- Link the feedback to the contact.
- Set `Sales Handoff Status` to `Ready for Sales`.
- Leave `opportunities` empty.

**Steps:**

1. Save the feedback record.
2. Confirm it appears in `AUTOMATION - Sales Ready Customer Feedback`.
3. Run or wait for the native automation.
4. Open the created Opportunity.
5. Open the source feedback record again.

**Expected result:**

- One new Opportunity is created.
- Opportunity `Stage` is `New`.
- Opportunity source is `Customer Feedback`.
- Opportunity links to the same contact.
- Feedback `opportunities` links to the new Opportunity.
- Feedback `Sales Handoff Status` becomes `Handoff Created`.

**Result:**

- [ ] Pass
- [ ] Fail

### 4. Sales Owner Daily Workflow from My Opportunities

**Purpose:** Confirm Sales can use `My Opportunities` as a daily work queue.

**Interface to test from:** `Sales / Account Management` -> `My Opportunities`

**Starting table:** `Opportunities`

**Setup data:**

- Create or choose an Opportunity.
- Set `Owner` to the current Sales user.
- Set `Stage` to an open stage, such as `New`, `Qualified`, or `Discovery`.
- Fill `Next Step`.
- Fill `Next Step Due`.

**Steps:**

1. Open the `Sales / Account Management` interface.
2. Open `My Opportunities`.
3. Confirm the Opportunity appears.
4. Update `Next Step`.
5. Update `Next Step Due`.
6. Move `Stage` to the next appropriate stage.

**Expected result:**

- The Opportunity appears only for the assigned owner.
- Sales can update Sales-owned fields.
- Updated `Next Step`, `Next Step Due`, and `Stage` save correctly.
- Linked Care source records remain available for context.

**Result:**

- [ ] Pass
- [ ] Fail

### 5. Overdue Next Step Reminder View

**Purpose:** Confirm overdue opportunities enter the automation view for reminders.

**Interface to test from:** `Sales / Account Management` -> `My Opportunities`, plus the `AUTOMATION - Overdue Next Steps` table view.

**Starting table:** `Opportunities`

**Setup data:**

- Create or choose an Opportunity.
- Set `Owner` to a valid Airtable collaborator.
- Set `Stage` to an open stage, not `Won`, `Lost`, or `Nurture`.
- Fill `Next Step`.
- Set `Next Step Due` to a date before today.

**Steps:**

1. Save the Opportunity.
2. Open `AUTOMATION - Overdue Next Steps`.
3. Confirm the Opportunity appears.
4. Run or wait for the reminder automation.

**Expected result:**

- Opportunity appears in `AUTOMATION - Overdue Next Steps`.
- Owner receives the configured Airtable notification or email.
- Opportunity leaves the view after `Next Step Due` is updated to today or a future date, or after stage changes to `Won`, `Lost`, or `Nurture`.

**Result:**

- [ ] Pass
- [ ] Fail

### 6. Won Opportunity Cleanup

**Purpose:** Confirm won opportunities are closed cleanly.

**Interface to test from:** `Sales / Account Management` -> `Pipeline Board`

**Starting table:** `Opportunities`

**Setup data:**

- Create or choose an open Opportunity.
- Ensure `Closed Date` is empty.

**Steps:**

1. Change `Stage` to `Won`.
2. Save the Opportunity.
3. Run or wait for the cleanup automation.

**Expected result:**

- Opportunity `Stage` is `Won`.
- `Closed Date` is filled with today's date.
- Opportunity no longer appears in open pipeline views.
- Opportunity appears in the closed stage area of `Pipeline Board`.

**Result:**

- [ ] Pass
- [ ] Fail

### 7. Lost Opportunity with Missing Lost Reason

**Purpose:** Confirm lost opportunities without a reason are visible for cleanup.

**Interface to test from:** `Sales / Account Management` -> `Pipeline Board`, plus the `Lost Opportunities Missing Lost Reason` table view.

**Starting table:** `Opportunities`

**Setup data:**

- Create or choose an open Opportunity.
- Ensure `Lost Reason` is empty.

**Steps:**

1. Change `Stage` to `Lost`.
2. Save the Opportunity.
3. Run or wait for the cleanup automation if configured.
4. Open `Lost Opportunities Missing Lost Reason`.
5. Fill `Lost Reason`.

**Expected result:**

- Opportunity `Stage` is `Lost`.
- `Closed Date` is filled if cleanup automation is active.
- Opportunity appears in `Lost Opportunities Missing Lost Reason` until `Lost Reason` is filled.
- Opportunity leaves the missing-reason view after `Lost Reason` is filled.

**Result:**

- [ ] Pass
- [ ] Fail

### 8. Rejected Sales Handoff

**Purpose:** Confirm Sales can reject a Care handoff without creating pipeline noise.

**Interface to test from:** `Sales / Account Management` -> `Sales Handoffs`, then confirm from the matching Care interface.

**Starting table:** Any Care source table

**Setup data:**

- Create or choose a ticket, scraped feed, or feedback record.
- Set `Sales Handoff Status` to `Ready for Sales`.
- Leave `opportunities` empty.

**Steps:**

1. Sales reviews the source record.
2. Sales determines it is not a valid opportunity.
3. Set `Sales Handoff Status` to `Rejected`.
4. Add a short reason in notes if available.

**Expected result:**

- No Opportunity is created.
- Source record remains available as historical context.
- Source record no longer appears in sales-ready handoff views.
- Care can see that Sales rejected the handoff.

**Result:**

- [ ] Pass
- [ ] Fail

### 9. Contact Context Review

**Purpose:** Confirm Sales can review customer context before outreach.

**Interface to test from:** `Sales / Account Management` -> `Contact Context`

**Starting table:** `Contacts`

**Setup data:**

- Choose a contact with at least one linked Care source record or Opportunity.

**Steps:**

1. Open the `Sales / Account Management` interface.
2. Open `Contact Context`.
3. Open the contact record.
4. Review linked tickets, scraped feeds, feedback records, and opportunities.

**Expected result:**

- Sales can see the contact's relevant history.
- Sales can open linked Opportunities.
- Sales can open linked Care source records for context.
- Sales does not need duplicate contact fields inside Opportunities.

**Result:**

- [ ] Pass
- [ ] Fail

### 10. Duplicate Opportunity Prevention

**Purpose:** Confirm automations do not create duplicate opportunities from the same source record.

**Interface to test from:** The relevant Care interface source page, plus the matching automation-ready table view.

**Starting table:** Any Care source table

**Setup data:**

- Create or choose a ticket, scraped feed, or feedback record.
- Set `Sales Handoff Status` to `Ready for Sales`.
- Link an existing Opportunity in `opportunities`.

**Steps:**

1. Save the source record.
2. Confirm the record does not appear in its automation-ready view.
3. Run or wait for relevant automations.
4. Check the `Opportunities` table.

**Expected result:**

- No duplicate Opportunity is created.
- Source record remains linked to the existing Opportunity.
- Automation-ready views require `opportunities` to be empty before creating a new Opportunity.

**Result:**

- [ ] Pass
- [ ] Fail

## Final Sign-Off

Use this section after all tests are complete.

| Area | Result | Notes |
| --- | --- | --- |
| Table relationships |  |  |
| Care interfaces |  |  |
| Sales interface |  |  |
| Ticket handoff automation |  |  |
| Scraped feed handoff automation |  |  |
| Customer feedback handoff automation |  |  |
| Overdue reminder automation |  |  |
| Closed opportunity cleanup |  |  |
| Duplicate prevention |  |  |

Reviewer:

Date:
