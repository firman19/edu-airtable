# Care & Sales Base Manual Test Scenarios

## Summary

Use this checklist to manually test the Care & Sales Base in Airtable.

The tests validate:

- table relationships
- handoff fields
- Care and Sales interface behavior
- Growth lead-management behavior
- native Airtable v1 automations
- simple guardrails between Care-owned context and Sales-owned pipeline work
- future technical integration acceptance criteria

## Assumptions

- The base is the `Care & Sales Base`.
- Sales mainly updates `Opportunities`.
- Growth mainly updates lead-development fields on `Contacts`, `Scraped Feeds`, and `Opportunities`.
- Care mainly updates `Tickets & Care Pipeline` and `Scraped Feeds`.
- `Sales Handoff Status` exists on Care-side source tables.
- `opportunities` is the existing linked-record field from Care source tables to `Opportunities`.
- Airtable automations are native Airtable automations only.
- External integrations such as Brevo, WhatsApp, EDU Inbox, and platform sync are not part of the Airtable v1 tests.
- Future technical integration tests are acceptance checks only and are not expected to pass until the technical team builds the integrations.

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

## Opportunity Type Options

`Opportunities.Opportunity Type` should use these options:

| Type | Meaning |
| --- | --- |
| `Advert` | Paid advertising opportunity. |
| `Consulting` | Consulting or advisory opportunity. |
| `Sponsorship` | Sponsorship opportunity. |
| `Membership` | Membership or subscription opportunity. |
| `Upsell` | Expansion or upgrade from an existing user or account. |
| `Triggered Lead` | Opportunity created from scraped external activity. |

## Lead Source Type Options

`Lead Source Type` should use these options on `Contacts` and `Opportunities`:

| Source | Meaning |
| --- | --- |
| `Care Upsell` | Came from a Care ticket or support conversation. |
| `Triggered Lead` | Came from scraped external activity. |
| `Target Lead` | Manually researched or identified by Growth. |
| `Manual Research` | Created from manual prospecting. |
| `Referral` | Came from a referral. |

## Preferred Contact Method Options

`Contacts.Preferred Contact Method` already exists and should use these options:

- `Email`
- `WeChat`
- `WhatsApp`
- `Social Handle`
- `Phone`

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

## Growth Interface

### Growth / Lead Management

Use this interface for Growth-owned lead review and outreach follow-up.

Recommended pages:

- `Triggered Leads`
- `Target Leads`
- `Repeat Posters`
- `Existing Users to Message`

Primary tables:

- `Scraped Feeds`
- `Contacts`
- `Organizations`
- `Opportunities`

## Automation Views To Verify

Create dedicated automation views before testing automations.

| Table | View | Purpose |
| --- | --- | --- |
| `Tickets & Care Pipeline` | `AUTOMATION - Sales Ready Ticket Upsells` | Tickets ready to become opportunities. |
| `Scraped Feeds` | `AUTOMATION - Sales Ready Scraped Feeds` | Scraped leads ready to become opportunities. |
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

### 3. Sales Owner Daily Workflow from My Opportunities

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

### 4. Overdue Next Step Reminder View

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

### 5. Won Opportunity Cleanup

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

### 6. Lost Opportunity with Missing Lost Reason

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

### 7. Rejected Sales Handoff

**Purpose:** Confirm Sales can reject a Care handoff without creating pipeline noise.

**Interface to test from:** `Sales / Account Management` -> `Sales Handoffs`, then confirm from the matching Care interface.

**Starting table:** Any Care source table

**Setup data:**

- Create or choose a ticket or scraped feed record.
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

### 8. Contact Context Review

**Purpose:** Confirm Sales can review customer context before outreach.

**Interface to test from:** `Sales / Account Management` -> `Contact Context`

**Starting table:** `Contacts`

**Setup data:**

- Choose a contact with at least one linked Care source record or Opportunity.

**Steps:**

1. Open the `Sales / Account Management` interface.
2. Open `Contact Context`.
3. Open the contact record.
4. Review linked tickets, scraped feeds, and opportunities.

**Expected result:**

- Sales can see the contact's relevant history.
- Sales can open linked Opportunities.
- Sales can open linked Care source records for context.
- Sales does not need duplicate contact fields inside Opportunities.

**Result:**

- [ ] Pass
- [ ] Fail

### 9. Duplicate Opportunity Prevention

**Purpose:** Confirm automations do not create duplicate opportunities from the same source record.

**Interface to test from:** The relevant Care interface source page, plus the matching automation-ready table view.

**Starting table:** Any Care source table

**Setup data:**

- Create or choose a ticket or scraped feed record.
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

### 10. Opportunity Type and Lead Source Classification

**Purpose:** Confirm Growth and Sales can classify opportunities by sales category and lead source.

**Interface to test from:** `Sales / Account Management` -> `Pipeline Board`

**Starting table:** `Opportunities`

**Setup data:**

- Create or choose an Opportunity.
- Link a Contact.
- Link an Organization if known.

**Steps:**

1. Open the Opportunity.
2. Set `Opportunity Type` to one of `Advert`, `Consulting`, `Sponsorship`, `Membership`, `Upsell`, or `Triggered Lead`.
3. Set `Lead Source Type` to one of `Care Upsell`, `Triggered Lead`, `Target Lead`, `Manual Research`, or `Referral`.
4. Save the Opportunity.

**Expected result:**

- Opportunity saves with the selected `Opportunity Type`.
- Opportunity saves with the selected `Lead Source Type`.
- Opportunity remains visible in Sales pipeline views.
- Reporting can group opportunities by type and source.

**Result:**

- [ ] Pass
- [ ] Fail

### 11. Triggered Lead Contact Method Review

**Purpose:** Confirm Growth can review scraped lead contact channels and update the matched Contact's preferred contact method.

**Interface to test from:** `Growth / Lead Management` -> `Triggered Leads`

**Starting table:** `Scraped Feeds`

**Setup data:**

- Create or choose a scraped feed record.
- Set `Post Type` to `Job Post`, `Deal Post`, or `Event Post`.
- Fill at least one contact channel such as `Cleaned Email`, `WeChat ID`, `WhatsApp`, `Social Handle`, or `Phone`.

**Steps:**

1. Open the scraped feed in `Triggered Leads`.
2. Review the available contact channels.
3. Link or create the matched Contact if known.
4. On the matched Contact, set `Preferred Contact Method`.
5. Add notes or create/link an Opportunity if the lead becomes sales-ready.

**Expected result:**

- Scraped feed stores the raw lead context and available contact channels.
- Matched Contact links back to the scraped feed when known.
- Contact stores the preferred contact method.
- Growth can identify which channel to use next from the Contact.

**Result:**

- [ ] Pass
- [ ] Fail

### 12. Target Lead Tracking

**Purpose:** Confirm Growth can track manually researched target leads without creating a separate Target Leads table.

**Interface to test from:** `Growth / Lead Management` -> `Target Leads`

**Starting table:** `Contacts`

**Setup data:**

- Create or choose a Contact.
- Set user type to educator, business, or vendor.
- Fill at least one outreach channel such as email, social handle, WeChat, WhatsApp, or phone.

**Steps:**

1. Set `Lead Source Type` to `Target Lead` or `Manual Research`.
2. Set `Preferred Contact Method`.
3. Link the Contact to an Organization if known.
4. Create or link an Opportunity if the lead becomes sales-ready.

**Expected result:**

- Contact appears in `Target Leads`.
- Contact has a usable outreach channel.
- Contact has a preferred contact method.
- No duplicate target lead table is needed.
- Opportunity is created only when Sales/Growth has something to manage.

**Result:**

- [ ] Pass
- [ ] Fail

## Future Technical Integration Acceptance Tests

These scenarios validate the post-build technical integrations described in `care-sales-base.md`.

They are not required for the current Airtable-only v1 setup. Use them after the technical team connects the EDU platform, EDU Inbox, and Brevo to Airtable.

### 13. EDU Platform to Airtable Contact Sync

**Purpose:** Confirm EDU Passport user records automatically sync into Airtable Contacts.

**Interface to test from:** Airtable `Contacts` table, plus the EDU Passport admin/user system.

**Starting table:** `Contacts`

**Setup data:**

- Create or choose a test user in EDU Passport.
- Confirm the user has User ID, full name, email, user type, and account status.
- Confirm no matching Airtable Contact exists yet.

**Steps:**

1. Trigger or wait for the platform-to-Airtable sync.
2. Open the Airtable `Contacts` table.
3. Search by the user's email or platform user ID.
4. Compare synced fields against the EDU Passport source record.

**Expected result:**

- One new Contact is created in Airtable.
- Platform user ID maps to Airtable `Contact ID` or a dedicated platform ID field.
- Full name, email, user type, and platform status match the EDU Passport record.
- No manual import or export is needed.

**Result:**

- [ ] Pass
- [ ] Fail

### 14. Duplicate Prevention During Platform Sync

**Purpose:** Confirm platform sync updates existing Contacts instead of creating duplicate records.

**Interface to test from:** Airtable `Contacts` table, plus the EDU Passport admin/user system.

**Starting table:** `Contacts`

**Setup data:**

- Choose an existing Airtable Contact that matches an EDU Passport user by platform user ID or email.
- Change a profile field in EDU Passport, such as full name, user type, or account status.

**Steps:**

1. Trigger or wait for the platform-to-Airtable sync.
2. Search Airtable Contacts by email and platform user ID.
3. Review the existing Contact record.

**Expected result:**

- The existing Contact is updated.
- No duplicate Contact is created.
- Changed platform fields are reflected in Airtable.
- Existing linked tickets, scraped feeds, and opportunities remain attached to the same Contact.

**Result:**

- [ ] Pass
- [ ] Fail

### 15. Existing User Detection from Scraped Feeds

**Purpose:** Confirm Airtable can detect when a scraped external post belongs to an existing active EDU user.

**Interface to test from:** `Growth / Lead Management` -> `Existing Users to Message`

**Starting table:** `Scraped Feeds`

**Setup data:**

- Create or choose an active Contact synced from EDU Passport.
- Create a scraped feed record with `Cleaned Email` matching that Contact.
- Fill post context such as post type and source URL.

**Steps:**

1. Trigger or wait for the matching workflow.
2. Open the scraped feed record.
3. Review the matched Contact.
4. Open `Existing Users to Message`.

**Expected result:**

- Scraped feed is matched to the existing Contact.
- Existing user cross-check indicates a match.
- Record appears in `Existing Users to Message`.
- Care or Growth can clearly see that intervention is required.

**Result:**

- [ ] Pass
- [ ] Fail

### 16. EDU Inbox Message Trigger and Logging

**Purpose:** Confirm Care or Growth can send a predefined EDU Inbox reminder from the Airtable workflow and retain communication history.

**Interface to test from:** `Growth / Lead Management` -> `Existing Users to Message`

**Starting table:** `Scraped Feeds`

**Setup data:**

- Choose a scraped feed matched to an active EDU user.
- Confirm the record is marked as requiring intervention.
- Confirm an approved EDU Inbox message template exists.

**Steps:**

1. Trigger the `Send EDU Reminder` action from the Airtable workflow.
2. Confirm the message is delivered in EDU Inbox.
3. Return to Airtable and review the source scraped feed or linked Contact.

**Expected result:**

- EDU Inbox message is sent without manual copy/paste.
- Message template is used correctly.
- Message activity is logged in Airtable or the connected communication history.
- Intervention status updates clearly after sending.

**Result:**

- [ ] Pass
- [ ] Fail

### 17. Airtable to Brevo Segmentation Sync

**Purpose:** Confirm Airtable contact status changes update Brevo marketing segments.

**Interface to test from:** Airtable `Contacts` table, plus Brevo.

**Starting table:** `Contacts`

**Setup data:**

- Choose a Contact with an email address.
- Confirm the Contact exists or can be created in Brevo.
- Note the current Brevo list or segment membership.

**Steps:**

1. Update Airtable fields used for segmentation, such as `User Type` or `Platform Status`.
2. Trigger or wait for the Airtable-to-Brevo sync.
3. Open Brevo and review the contact's segment membership.

**Expected result:**

- Brevo receives the updated Airtable contact fields.
- Contact is added to the correct marketing segment.
- Contact is removed from segments that no longer apply.
- No manual list management is needed.

**Result:**

- [ ] Pass
- [ ] Fail

### 18. Brevo to Airtable Engagement Sync

**Purpose:** Confirm Brevo engagement data syncs back into Airtable for Care, Growth, and Sales context.

**Interface to test from:** Airtable `Contacts` table, plus Brevo.

**Starting table:** `Contacts`

**Setup data:**

- Choose a Contact with an email address.
- Confirm the Contact has Brevo activity, such as campaign participation or last email activity.

**Steps:**

1. Trigger or wait for the Brevo-to-Airtable sync.
2. Open the Contact in Airtable.
3. Review email engagement fields.

**Expected result:**

- Airtable shows Brevo engagement context.
- Campaign participation and last email activity are visible if those fields exist.
- Synced marketing context helps Care, Growth, and Sales understand recent communication.

**Result:**

- [ ] Pass
- [ ] Fail

### 19. Integration Error Handling and Monitoring

**Purpose:** Confirm failed technical integrations produce visible errors and can be recovered safely.

**Interface to test from:** Airtable integration monitoring view, automation logs, or the technical team's monitoring dashboard.

**Starting table:** Any connected table

**Setup data:**

- Choose a non-production test record.
- Prepare a controlled failure case, such as invalid email, missing required platform ID, or temporarily disabled test credential.

**Steps:**

1. Trigger the integration with the controlled failure.
2. Review the integration log or monitoring dashboard.
3. Correct the source issue.
4. Retry or wait for the recovery workflow.

**Expected result:**

- Failure is logged with enough detail to diagnose the issue.
- Failed records do not create duplicates.
- Corrected records can sync successfully.
- Care, Growth, Sales, or the technical team can see when manual attention is required.

**Result:**

- [ ] Pass
- [ ] Fail

## Final Sign-Off

Use this section after all Airtable v1 tests are complete.

| Area | Result | Notes |
| --- | --- | --- |
| Table relationships |  |  |
| Care interfaces |  |  |
| Sales interface |  |  |
| Ticket handoff automation |  |  |
| Scraped feed handoff automation |  |  |
| Overdue reminder automation |  |  |
| Closed opportunity cleanup |  |  |
| Duplicate prevention |  |  |
| Opportunity categorization |  |  |
| Triggered lead contact method review |  |  |
| Target lead tracking |  |  |

Reviewer:

Date:

## Future Integration Sign-Off

Use this section only after the technical integrations are built.

| Area | Result | Notes |
| --- | --- | --- |
| EDU Platform to Airtable Contact sync |  |  |
| Platform sync duplicate prevention |  |  |
| Existing user detection from scraped feeds |  |  |
| EDU Inbox message trigger and logging |  |  |
| Airtable to Brevo segmentation sync |  |  |
| Brevo to Airtable engagement sync |  |  |
| Integration error handling and monitoring |  |  |

Reviewer:

Date:
