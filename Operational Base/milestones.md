# Milestones

# EDU Passport Operations Hub Implementation Milestones

## Milestone 1: Shared Foundation [complete]

Goal: Create the shared CRM and work-management foundation before adding department-specific workflows.

Todo:
- [x] Confirm the base name is `EDU Passport Operations Hub`.
- [x] Compare existing Airtable fields against [field-requirements.md](field-requirements.md).
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

Reference: [product-field-requirements.md](product-field-requirements.md).

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
- [x] Compare existing Airtable fields against [care-field-requirements.md](care-field-requirements.md).
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

## Milestone 4: Interfaces And Access Guardrails [current]

Goal: Make Airtable usable by each role through focused interfaces instead of raw tables.

Todo:
- [ ] Create `Care Service Desk`.
- [ ] Create `Scraped Listing Review`.
- [ ] Create `Product Request Submission`.
- [ ] Create `Product Triage`.
- [ ] Create `Engineering / Product Task Board`.
- [ ] Create `Bug Queue`.
- [ ] Create `QA Dashboard`.
- [ ] Create `Release Dashboard`.
- [ ] Create `Changelog View`.
- [ ] Create `Sales / Account Management View`.
- [ ] Create `Manager Dashboard`.
- [ ] Review existing `Executive Dashboard`, `My Tasks`, `Projects`, and `Marketing Interface`.
- [ ] Restrict non-Product users from editing Product decision fields where supported.
- [ ] Restrict non-Care users from editing Care-owned workflow fields where supported.
- [ ] Ensure each interface filters users into the right department/project context.

Done Criteria:
- Staff can do daily work from interfaces.
- Managers can see cross-department status.
- Product, Care, Sales/AM, Marketing, and Operations each have clear work surfaces.
- Access is guided by role-specific interfaces and field ownership.

## Milestone 5: Native Automations

Goal: Add lightweight native Airtable automations after tables and interfaces are stable.

Todo:
- [ ] Create urgent/high Product Request alert.
- [ ] Create urgent/high Care Ticket alert.
- [ ] Create Account Management view/filter for `Upsell Potential`.
- [ ] Create Scraped Listing existing-contact intervention queue.
- [ ] Create bug-related Product Request routing.
- [ ] Create QA failed alert.
- [ ] Create release-to-changelog automation.
- [ ] Review existing blog task generation automation.
- [ ] Review existing Creative Requests automation.
- [ ] Review recurring task automation.

Done Criteria:
- Urgent work alerts the right owner.
- Failed QA does not disappear silently.
- Released work creates or updates changelog records.
- Upsell and scraped listing workflows are visible without manual searching.

## Milestone 6: Validation And Reporting

Goal: Test the full system with realistic cross-team workflows and confirm management reporting works.

Todo:
- [ ] Test Care ticket for an existing contact.
- [ ] Test Care follow-up through related Task.
- [ ] Test Care product escalation process through notes/task handoff.
- [ ] Test Care upsell handoff to Sales/Account Management.
- [ ] Test Scraped Listing matching and intervention flow.
- [ ] Test Product request triage to project/task/bug.
- [ ] Test bug fix through QA and release.
- [ ] Test release to changelog.
- [ ] Test Manager Dashboard across departments.
- [ ] Check for duplicate task/contact records.
- [ ] Document gaps found during testing.

Done Criteria:
- Core Product and Care scenarios work end to end.
- Manager reporting shows shared progress across teams.
- The base has no duplicate Product Tasks or Care Contacts systems.
- Remaining gaps are documented as future improvements.

## Milestone 7: Sales / Account Management Pipeline

Goal: Add Opportunities only when Sales/Account Management is ready to manage a pipeline.

Todo:
- [ ] Confirm Sales/Account Management workflow requirements.
- [ ] Create Opportunities table if still needed.
- [ ] Link Opportunities to Organizations.
- [ ] Link Opportunities to Contacts when a primary person is known.
- [ ] Link Opportunities to Care Tickets when created from upsell potential.
- [ ] Link Opportunities to Scraped Listing when created from external posts.
- [ ] Define opportunity stage, owner, value, expected close date, and source fields.
- [ ] Create Sales / Account Management View.

Done Criteria:
- Upsell and scraped listing records can become managed pipeline items.
- Care can hand off qualified opportunities without owning the sales workflow.
- Opportunities are not used as a generic task or contact substitute.

## Milestone 8: Future Integrations

Goal: Add external system integrations only after the Airtable structure is stable.

Todo:
- [ ] Define platform-to-Airtable contact/account sync requirements.
- [ ] Define Airtable-to-EDU Inbox intervention requirements.
- [ ] Define Airtable-to-Brevo contact status sync requirements.
- [ ] Define WhatsApp notification requirements if still needed.
- [ ] Decide integration owner for each external system.
- [ ] Decide whether each integration uses Airtable native features, Make, n8n, API, or another provider.

Done Criteria:
- Integration requirements are clear before build.
- Native Airtable remains the source workflow.
- External tools enhance the system without becoming the first source of truth.

## Milestone 9: HR And Finance Planning

Goal: Plan HR and Finance separately because they likely need stronger access boundaries.

Todo:
- [ ] Gather HR requirements.
- [ ] Gather Finance requirements.
- [ ] Identify sensitive HR fields and workflows.
- [ ] Identify sensitive Finance fields and workflows.
- [ ] Decide whether HR needs its own base.
- [ ] Decide whether Finance needs its own base.
- [ ] Define what, if anything, should connect back to the Operations Hub.

Done Criteria:
- HR and Finance are not mixed into the Operations Hub by default.
- Sensitive data boundaries are clear.
- Any future cross-base connection is intentional.
