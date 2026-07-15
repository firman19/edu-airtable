# Milestones

# EDU Passport Airtable Portfolio Implementation Milestones

## Milestone 1: Shared Foundation [complete]

Goal: Create the shared CRM and work-management foundation before adding department-specific workflows.

Todo:
- [x] Confirm the base name is `EDU Passport Operations Hub`.
- [x] Compare existing Airtable fields against [field-requirements.md](Operational%20Base/field-requirements.md).
- [x] Create or verify `Departments`.
- [x] Create or verify `Roadmaps`.
- [x] Create or verify `Projects`.
- [x] Create or verify `Tasks`.
- [x] Create `Organizations`.
- [x] Create `Contacts`.
- [x] Link `Projects` to `Roadmaps`.
- [x] Link `Projects` to `Departments`.
- [x] Link `Tasks` to `Projects`.
- [x] Link `Tasks` to `Departments`.
- [x] Link `Contacts` to `Organizations`.
- [x] Add required-field rules or equivalent interface guardrails for `Task -> Project`.

Done Criteria:
- Every task can be reported by project, department, and owner.
- Contacts and Organizations are the shared CRM source of truth.
- Upsell and triggered-lead signals can be captured without a separate pipeline table.
- No duplicate task or contact tables exist for Product or Care.
- No Team Members table is required for Milestone 1.

## Milestone 2: Product Workflow [complete]

Goal: Build Product intake, triage, bug, QA, release, and changelog workflows while keeping execution in shared Tasks.

Reference: [product-field-requirements.md](Operational%20Base/product-field-requirements.md).

Todo:
- [x] Create `Product Requests`.
- [x] Create `Product Areas`.
- [x] Create `Bugs & Issues`.
- [x] Create `QA & Testing`.
- [x] Create `Releases`.
- [x] Create `Changelog`.
- [x] Link `Product Requests` to `Product Areas`.
- [x] Link `Product Requests` to `Projects`.
- [x] Link `Product Requests` to shared `Tasks`.
- [x] Link `Bugs & Issues` to shared `Tasks`.
- [x] Link `Bugs & Issues` to `QA & Testing`.
- [x] Link `QA & Testing` to `Releases`.
- [x] Link `Releases` to `Changelog`.
- [x] Configure Product status options for request triage.
- [x] Configure bug severity/status options.
- [x] Configure QA result/status options.
- [x] Configure release status options.
- [x] Validate request-to-triage-to-task/bug-to-QA-to-release-to-changelog workflow.

Done Criteria:
- A request can move from submission to triage, task/bug linkage, QA, release, changelog, and closure.
- Product execution work is visible in the shared `Tasks` table.
- Product decisions are visible to other teams without letting them overwrite decision fields.

## Milestone 3: Care Workflow [complete]

Goal: Build Care support, customer lifecycle, upsell, and triggered-lead workflows using shared CRM records.

Todo:
- [x] Compare existing Airtable fields against [care-field-requirements.md](Operational%20Base/care-field-requirements.md).
- [x] Create `Care Tickets`.
- [x] Create `Scraped Listing`.
- [x] Link `Care Tickets` to `Contacts`.
- [x] Link `Care Tickets` to `Organizations`.
- [x] Link `Care Tickets` to shared `Tasks`.
- [x] Link `Scraped Listing` to `Contacts`.
- [x] Configure ticket issue type, priority, and status options.
- [x] Add `Upsell Potential` flag on `Care Tickets`.
- [x] Add fields for scraped source, raw contact info, cleaned email, repeat poster flag, and existing-user cross-check.

Done Criteria:
- Care can create and resolve support tickets against shared contacts/organizations.
- Care can use related Tasks and notes for follow-up or later escalation.
- Upsell signals can be prepared for later Sales/Account Management handoff.
- Scraped listings can be reviewed, cleaned, and matched.

## Milestone 4: Interfaces And Access Guardrails [complete]

Goal: Make Airtable usable by each role through focused interfaces instead of raw tables.

Todo:
- [x] Create `Care Service Desk`.
- [x] Create `Scraped Listing Review`.
- [x] Create `Product Request Submission`.
- [x] Create `Product Triage`.
- [x] Create `Engineering / Product Task Board`.
- [x] Create `Bug Queue`.
- [x] Create `QA Dashboard`.
- [x] Create `Release Dashboard`.
- [x] Create `Changelog View`.
- [x] Create `Sales / Account Management View`.
- [x] Create `Manager Dashboard`.
- [x] Review existing `Executive Dashboard`, `My Tasks`, `Projects`, and `Marketing Interface`.
- [x] Restrict non-Product users from editing Product decision fields where supported.
- [x] Restrict non-Care users from editing Care-owned workflow fields where supported.
- [x] Ensure each interface filters users into the right department/project context.

Done Criteria:
- Staff can do daily work from interfaces.
- Managers can see cross-department status.
- Product, Care, Sales/AM, Marketing, and Operations each have clear work surfaces.
- Access is guided by role-specific interfaces and field ownership.

## Milestone 5: Native Automations [complete]

Goal: Add lightweight native Airtable automations after tables and interfaces are stable.

Todo:
- [x] Create urgent/high Product Request alert.
- [x] Create urgent/high Care Ticket alert.
- [x] Create Account Management view/filter for `Upsell Potential`.
- [x] Create Scraped Listing existing-contact intervention queue.
- [x] Create bug-related Product Request routing.
- [x] Create QA failed alert.
- [x] Create release-to-changelog automation.
- [x] Review existing blog task generation automation.
- [x] Review existing Creative Requests automation.
- [x] Review recurring task automation.

Done Criteria:
- Urgent work alerts the right owner.
- Failed QA does not disappear silently.
- Released work creates or updates changelog records.
- Upsell and scraped listing workflows are visible without manual searching.

## Milestone 6: Validation And Reporting [complete]

Goal: Test the full system with realistic cross-team workflows and confirm management reporting works.

Todo:
- [x] Test Care ticket for an existing contact.
- [x] Test Care follow-up through related Task.
- [x] Test Care product escalation process through notes/task handoff.
- [x] Test Care upsell handoff to Sales/Account Management.
- [x] Test Scraped Listing matching and intervention flow.
- [x] Test Product request triage to project/task/bug.
- [x] Test bug fix through QA and release.
- [x] Test release to changelog.
- [x] Test Manager Dashboard across departments.
- [x] Check for duplicate task/contact records.
- [x] Document gaps found during testing.

Done Criteria:
- Core Product and Care scenarios work end to end.
- Manager reporting shows shared progress across teams.
- The base has no duplicate Product Tasks or Care Contacts systems.
- Remaining gaps are documented as future improvements.

## Milestone 7: Sales / Account Management Pipeline [complete]

Goal: Provide a Sales and Account Management pipeline without duplicating Opportunities in the Operations Hub.

Implementation: Completed in the separate [Care & Sales Base](Care%20%26%20Sales%20Base/README.md), which owns customer-lifecycle Opportunities and sales handoffs.

Todo:
- [x] Confirm Sales/Account Management workflow requirements.
- [x] Create `Opportunities` in the Care & Sales Base.
- [x] Link Opportunities to Organizations.
- [x] Link Opportunities to Contacts when a primary person is known.
- [x] Link Opportunities to Care Tickets when created from upsell potential.
- [x] Link Opportunities to Scraped Feeds when created from external posts.
- [x] Define opportunity stage, owner, value, expected close date, and source fields.
- [x] Create Sales / Account Management interfaces in the Care & Sales Base.

Done Criteria:
- Upsell and scraped listing records can become managed pipeline items.
- Care can hand off qualified opportunities without owning the sales workflow.
- Opportunities are not used as a generic task or contact substitute.
- The Operations Hub does not contain a duplicate Opportunities table.

## Milestone 8: Corporate Functions, Operations, And AI & Automation [current]

Goal: Establish clear operating and access boundaries for company administration, HR, Finance, Operations, and the dedicated AI & Automation division.

References:
- [Cross-base corporate functions requirements](company-functions-requirements.md)
- [People & HR Base](People%20%26%20HR%20Base/README.md)
- [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md)

Todo:
- [ ] Confirm `Operations` as the department for non-sensitive company administration and operational execution.
- [ ] Create the `AI & Automation` department, roadmap, projects, shared-task views, and interface in the Operations Hub.
- [ ] Create the `AI & Automation Register` in the Operations Hub.
- [ ] Create the restricted `EDU Passport Corporate Services` workspace.
- [ ] Create the restricted [EDU Passport People & HR](People%20%26%20HR%20Base/README.md) base.
- [ ] Create the restricted [EDU Passport Finance & Administration](Finance%20%26%20Administration%20Base/README.md) base.
- [ ] Create Finance Requests budget-change fields and approved-adjustment linkage.
- [ ] Create Budget Plans, Budget Categories, and monthly Department x Category Budget Lines in USD.
- [ ] Create Finance Request Portal, Budget Workspace, and Finance Admin interfaces.
- [ ] Configure all-department approved-budget visibility, own-department planning/forecast editing, and Finance-only control fields.
- [ ] Configure the Finance daily admin digest and monthly-close reminder automations.
- [ ] Configure base-specific or interface-only access for HR and Finance workflows.
- [ ] Confirm payroll, accounting, banking, and secure document systems remain authoritative.
- [ ] Test the routing rules and sensitive-data boundaries.
- [ ] Launch without cross-base synchronization.

Done Criteria:
- Non-sensitive administration and Operations use shared Projects and Tasks in the Operations Hub.
- AI & Automation has dedicated ownership without creating a duplicate task system.
- HR and Finance workflows are isolated in two restricted bases.
- Sensitive employee, payroll, banking, and detailed financial data does not appear in the Operations Hub.
- Any future cross-base summary is explicitly approved, non-sensitive, one-way, and field-allowlisted.
- Every department can plan monthly budgets by category and compare approved monthly, quarterly, annual, and YTD results.
- Finance can reconcile summarized monthly actuals from the accounting system without importing transaction-level or banking data.
- Approved budget baselines remain intact and post-approval changes use Budget Change requests.

## Milestone 9: Future Integrations [planned]

Goal: Add external system integrations only after the Airtable structure and corporate-function boundaries are stable.

Todo:
- [ ] Define platform-to-Airtable contact/account synchronization requirements.
- [ ] Define Airtable-to-EDU Inbox workflow requirements.
- [ ] Define Airtable-to-Brevo synchronization requirements.
- [ ] Define WhatsApp notification requirements if still needed.
- [ ] Assign an owner for each integration.
- [ ] Select Airtable native features, Make, n8n, API, or another provider for each integration.
- [ ] Define production monitoring, failure logging, retries, duplicate prevention, and maintenance ownership.

Done Criteria:
- Integration requirements, ownership, data mappings, and failure behavior are clear before build.
- Production integrations are monitored and recover safely without creating duplicates.
- External systems enhance Airtable workflows without replacing the agreed system of record.
