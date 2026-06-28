# Interface Requirements

# Milestone 4 Target Checklist

Goal: Make Airtable usable through focused role-specific interfaces instead of asking staff to work in raw tables.

Milestone 4 should stay simple and fit Airtable Free Plan limits where possible. If interface permissions are limited, use views, forms, field visibility, filtered pages, and team process rules as guardrails.

## Interface Principles

- Staff should see only the records and fields needed for daily work.
- Product decision fields should be editable by Product owners only where Airtable allows it.
- Care-owned workflow fields should be editable by Care owners only where Airtable allows it.
- Managers should get summary dashboards, not another work queue.
- Do not create duplicate task, contact, or pipeline tables just to make an interface.

## Existing Interfaces To Review

| Interface | Purpose | Status | Notes |
| --- | --- | --- | --- |
| Executive Dashboard | Management overview. | Existing / review | Check if it reflects shared Tasks, Projects, Product, and Care. |
| My Tasks | Personal task view. | Existing / review | Should filter by current Airtable user where possible. |
| Projects | Project planning and tracking. | Existing / review | Should show Roadmap, Department, Owner, Status, Due Date, and related Tasks. |
| Marketing Interface | Marketing workflow. | Existing / review | Keep Campaigns and Content as Marketing-specific surfaces. |

## Interfaces To Create Or Verify

| Interface | Primary Users | Main Tables | Required Views / Sections | Milestone 4 Status |
| --- | --- | --- | --- | --- |
| Care Service Desk | Care | Care Tickets, Contacts, Organizations, Tasks | Open tickets, urgent tickets, my tickets, resolved tickets, upsell potential. | To Build |
| Scraped Listing Review | Care | Scraped Listing, Contacts | New listings, matched contacts, no match yet, repeat posters, intervention notes. | To Build |
| Product Request Submission | All teams | Product Requests | Simple submission form/page with limited editable fields. | To Build |
| Product Triage | Product | Product Requests, Product Areas, Projects, Tasks | New requests, accepted requests, not planned, by product area, by priority. | To Build |
| Engineering / Product Task Board | Product/Tech | Tasks, Projects, Sprints, Product Areas | Product/engineering tasks grouped by status, owner, sprint, and product area. | To Build |
| Bug Queue | Product/Tech | Bugs & Issues, Tasks, QA & Testing | New bugs, high severity, in progress, fixed, QA needed, released. | To Build |
| QA Dashboard | Product/QA | QA & Testing, Bugs & Issues, Releases, Tasks | Not started, failed, blocked, passed, by release. | To Build |
| Release Dashboard | Product | Releases, QA & Testing, Changelog | Planning, QA, ready, released, changelog needed. | To Build |
| Changelog View | Product/Care/Marketing | Changelog, Releases | Internal notes, user-facing messages, published date. | To Build |
| Manager Dashboard | Managers | Projects, Tasks, Product Requests, Care Tickets, Releases | Cross-department status, overdue work, priority work, blockers, release/care summary. | To Build |

## Deferred Interface

| Interface | Reason |
| --- | --- |
| Sales / Account Management View | Defer until Opportunities or a clearer Sales/AM pipeline exists. For now, use `Care Tickets.Upsell Potential` view/filter. |

## Interface Builder Map

Use this section when Airtable asks you to add a page, choose a layout, then choose a source table.

### Executive Dashboard

| Page | Layout | Source Table |
| --- | --- | --- |
| Executive Overview | Dashboard | `Projects` |
| Projects Health | List / Grid | `Projects` |
| Tasks And Blockers | List / Grid | `Tasks` |
| Product Snapshot | Dashboard | `Product Requests` |
| Care Snapshot | Dashboard | `Care Tickets` |
| Releases And Changelog | Calendar | `Releases` |

### My Tasks

| Page | Layout | Source Table |
| --- | --- | --- |
| My Open Tasks | List / Grid | `Tasks` |
| Due This Week | Calendar or List / Grid | `Tasks` |
| Overdue | List / Grid | `Tasks` |
| Ready For Review | Kanban or List / Grid | `Tasks` |
| Recently Completed | List / Grid | `Tasks` |

### Projects

| Page | Layout | Source Table |
| --- | --- | --- |
| Active Projects | List / Grid | `Projects` |
| Project Timeline | Timeline or Calendar | `Projects` |
| Projects By Department | List / Grid | `Projects` |
| Projects By Roadmap | List / Grid | `Projects` |
| Project Detail | Record Review | `Projects` |

### Marketing Interface

| Page | Layout | Source Table |
| --- | --- | --- |
| Campaigns | List / Grid | `Campaigns` |
| Campaign Calendar | Calendar | `Campaigns` |
| Content Pipeline | Kanban or List / Grid | `Content` |
| Content Calendar | Calendar | `Content` |
| Marketing Tasks | List / Grid | `Tasks` |

### Care Service Desk

| Page | Layout | Source Table |
| --- | --- | --- |
| Open Tickets | List / Grid | `Care Tickets` |
| My Tickets | List / Grid | `Care Tickets` |
| Urgent Tickets | List / Grid | `Care Tickets` |
| Awaiting User Reply | List / Grid | `Care Tickets` |
| Resolved Tickets | List / Grid | `Care Tickets` |
| Upsell Potential | List / Grid | `Care Tickets` |
| Ticket Detail | Record Review | `Care Tickets` |

### Scraped Listing Review

| Page | Layout | Source Table |
| --- | --- | --- |
| New Listings | List / Grid | `Scraped Listing` |
| Missing Cleaned Email | List / Grid | `Scraped Listing` |
| No Match Yet | List / Grid | `Scraped Listing` |
| Existing User Matched | List / Grid | `Scraped Listing` |
| Repeat Posters | List / Grid | `Scraped Listing` |
| Recently Reviewed | List / Grid | `Scraped Listing` |

### Product Request Submission

| Page | Layout | Source Table |
| --- | --- | --- |
| Submit Request | Form | `Product Requests` |
| My Submitted Requests | List / Grid | `Product Requests` |
| Request Status | List / Grid | `Product Requests` |

### Product Triage

| Page | Layout | Source Table |
| --- | --- | --- |
| New Requests | List / Grid | `Product Requests` |
| Needs More Info | List / Grid | `Product Requests` |
| Accepted Requests | List / Grid | `Product Requests` |
| In Progress | Kanban or List / Grid | `Product Requests` |
| Released / Closed | List / Grid | `Product Requests` |
| Not Planned | List / Grid | `Product Requests` |
| By Product Area | List / Grid | `Product Requests` |

### Engineering / Product Task Board

| Page | Layout | Source Table |
| --- | --- | --- |
| Task Board | Kanban | `Tasks` |
| My Product Tasks | List / Grid | `Tasks` |
| By Sprint | Kanban or List / Grid | `Tasks` |
| By Product Area | List / Grid | `Tasks` |
| Bug Fix Tasks | List / Grid | `Tasks` |
| QA Related Tasks | List / Grid | `Tasks` |

### Bug Queue

| Page | Layout | Source Table |
| --- | --- | --- |
| New Bugs | List / Grid | `Bugs & Issues` |
| Critical / High Severity | List / Grid | `Bugs & Issues` |
| In Progress | Kanban or List / Grid | `Bugs & Issues` |
| Fixed Waiting For QA | List / Grid | `Bugs & Issues` |
| QA Passed | List / Grid | `Bugs & Issues` |
| Released Bugs | List / Grid | `Bugs & Issues` |

### QA Dashboard

| Page | Layout | Source Table |
| --- | --- | --- |
| QA Queue | List / Grid | `QA & Testing` |
| Not Started | List / Grid | `QA & Testing` |
| Failed | List / Grid | `QA & Testing` |
| Blocked | List / Grid | `QA & Testing` |
| Passed | List / Grid | `QA & Testing` |
| By Release | List / Grid | `QA & Testing` |
| QA Calendar | Calendar | `QA & Testing` |

### Release Dashboard

| Page | Layout | Source Table |
| --- | --- | --- |
| Release Pipeline | Kanban or List / Grid | `Releases` |
| Release Calendar | Calendar | `Releases` |
| In QA | List / Grid | `Releases` |
| Ready To Release | List / Grid | `Releases` |
| Released | List / Grid | `Releases` |
| Changelog Needed | List / Grid | `Releases` |

### Changelog View

| Page | Layout | Source Table |
| --- | --- | --- |
| Draft / Internal Changes | List / Grid | `Changelog` |
| User-Facing Messages | List / Grid | `Changelog` |
| By Audience | List / Grid | `Changelog` |
| Published Entries | List / Grid | `Changelog` |
| Changelog Calendar | Calendar | `Changelog` |

### Manager Dashboard

| Page | Layout | Source Table |
| --- | --- | --- |
| Manager Overview | Dashboard | `Projects` |
| Work By Department | List / Grid | `Tasks` |
| Open High Priority Work | List / Grid | `Tasks` |
| Overdue Work | List / Grid | `Tasks` |
| Product Intake | Dashboard or List / Grid | `Product Requests` |
| Care Summary | Dashboard or List / Grid | `Care Tickets` |
| Bug Summary | Dashboard or List / Grid | `Bugs & Issues` |
| Release Summary | Dashboard or List / Grid | `Releases` |

### Sales / Account Management View

Status: Deferred.

| Page | Layout | Source Table |
| --- | --- | --- |
| Upsell Potential | List / Grid | `Care Tickets` |

## Access Guardrails

Use these as process/interface rules even if Airtable plan limits prevent strict field-level permissions:

| Area | Guardrail |
| --- | --- |
| Product Requests | Non-Product users can submit requests and view status; Product owns priority, status, product owner, related project/task, and final decision. |
| Bugs & Issues | Product/Tech owns severity, status, fix task, QA, and release linkage. |
| QA & Testing | QA/Product owns QA status, actual result, tested date, and release linkage. |
| Releases / Changelog | Product owns release status and changelog wording. |
| Care Tickets | Care owns ticket priority, status, owner, notes, and upsell potential. |
| Scraped Listing | Care owns cleaned email, matched contact, cross-check result, and review notes. |
| Tasks | Assignees update their own task progress; managers/product/care leads review filtered boards. |

## Detailed Interface Requirements

### Executive Dashboard

Purpose: Give leadership a quick operating snapshot without asking them to inspect raw tables.

Primary users: Managers, leadership.

Main data:
- `Projects`
- `Tasks`
- `Product Requests`
- `Care Tickets`
- `Releases`

Required sections:
- Active projects by department.
- Overdue tasks.
- High/Urgent tasks.
- Product requests by status and priority.
- Open Care tickets by priority/status.
- Upcoming or recently released releases.

Pages and layouts:

| Page | Primary Layout | Primary Table To Select | Supporting Elements | Purpose |
| --- | --- | --- | --- | --- |
| Executive Overview | Dashboard | `Projects` | Number cards, charts, compact lists from multiple tables | One-screen leadership summary. |
| Projects Health | List / Grid | `Projects` | Group by `Department`, then `Status`; record detail side panel | Show whether department work is moving. |
| Tasks And Blockers | List / Grid | `Tasks` | Filtered exception lists; group by `Department` or `Owner` | Surface overdue, urgent, and blocked execution work. |
| Product Snapshot | Dashboard + List | `Product Requests` | Number cards, charts, filtered lists from Product tables | Track product intake, bugs, QA pressure, and releases. |
| Care Snapshot | Dashboard + List | `Care Tickets` | Number cards, charts, filtered lists from Care tables | Track customer support pressure and upsell signals. |
| Releases And Changelog | Calendar + List | `Releases` | Calendar by `Release Date`; list of changelog records | Show what changed, what is coming, and who needs notice. |

Builder order:

| Page | Select Layout | Select Table |
| --- | --- | --- |
| Executive Overview | Dashboard | `Projects` |
| Projects Health | List / Grid | `Projects` |
| Tasks And Blockers | List / Grid | `Tasks` |
| Product Snapshot | Dashboard | `Product Requests` |
| Care Snapshot | Dashboard | `Care Tickets` |
| Releases And Changelog | Calendar | `Releases` |

Note: For dashboard-style pages, choose the best primary table first, then add extra elements/charts/lists from other tables after the page is created.

Page build details:

| Page | Recommended Layout Details |
| --- | --- |
| Executive Overview | Use summary/dashboard layout. Top row: active projects, overdue tasks, urgent work, open Care tickets, upcoming releases. Middle row: charts for projects by department, tasks by status, Product Requests by status, Care Tickets by priority. Bottom row: compact lists for overdue tasks, urgent/high work, and next releases. |
| Projects Health | Use list/grid layout. Show active projects grouped by `Department`, then `Status`. Add filtered sections for projects due soon and at-risk/overdue projects. Use record detail panel to show related tasks. |
| Tasks And Blockers | Use list/grid layout. Show overdue tasks, high/urgent tasks, and tasks due this week. Group by `Department` or `Owner`. If `Blocker Reason` was removed, use `Description` or `Status = Blocked` for blocker context. |
| Product Snapshot | Use dashboard plus list layout. Add number cards for new requests, accepted requests, high-priority requests, open bugs, failed/blocked QA, and releases in planning/QA. Add lists for high-severity bugs, QA needing attention, and upcoming releases. |
| Care Snapshot | Use dashboard plus list layout. Add number cards for new/open tickets, urgent tickets, awaiting reply, resolved this week, and upsell potential. Add lists for urgent tickets, stale tickets, and upsell potential records. |
| Releases And Changelog | Use calendar layout for releases by `Release Date`. Add list layout below for releases without changelog, recently released items, and changelog records needing copy. |

Avoid these layouts for Executive Dashboard:
- Gallery: not useful for dense operational reporting.
- Kanban: better for team work queues than executive reporting.
- Calendar-only dashboard: useful for releases, but too narrow for the full executive view.

Key fields to show:
- Projects: `Project Name`, `Department`, `Owner`, `Status`, `Priority`, `Due Date`.
- Tasks: `Task Name`, `Project`, `Department`, `Owner`, `Status`, `Priority`, `Due Date`.
- Product Requests: `Summary`, `Source Team`, `Request Type`, `Priority`, `Impact`, `Status`, `Product Owner`.
- Care Tickets: `Ticket ID`, `Associated Contact`, `Organization`, `Issue Type`, `Ticket Priority`, `Ticket Status`, `Owner`.
- Releases: `Release Name`, `Release Status`, `Release Date`, `Teams to Notify`.

Filters:
- Hide archived/done records by default.
- Show overdue tasks where `Due Date` is before today and `Status` is not done.
- Show high-priority work where `Priority` or `Ticket Priority` is `High` or `Urgent`.

Guardrails:
- Dashboard should be mostly read-only for managers unless they own the record.
- Use it for monitoring, not daily task editing.
- Keep record creation out of the Executive Dashboard except for manager-owned follow-up tasks that are linked to a project.
- Use detail pages for inspection only; edits should happen in the team-specific interfaces.

### My Tasks

Purpose: Give each staff member a simple personal execution list.

Primary users: All staff.

Main data:
- `Tasks`

Required sections:
- My open tasks.
- Due this week.
- Overdue.
- Ready for review.
- Completed recently.

Key fields to show:
- `Task Name`
- `Project`
- `Department`
- `Owner`
- `Status`
- `Priority`
- `Start Date`
- `Due Date`
- `Description`
- `Attachments`

Filters:
- `Owner` is current Airtable user where possible.
- Exclude done/archived tasks from the default open view.

Guardrails:
- Staff should update `Status`, `Description`, and attachments as needed.
- Project, Department, and CRM links should usually be edited by leads/managers.

### Projects

Purpose: Give project owners and managers a clean project planning surface.

Primary users: Managers, department leads, project owners.

Main data:
- `Projects`
- `Tasks`
- `Roadmaps`

Required sections:
- Active projects.
- Projects by department.
- Projects by roadmap.
- Overdue projects.
- Project detail with related tasks.

Key fields to show:
- `Project Name`
- `Department`
- `Roadmap`
- `Owner`
- `Status`
- `Priority`
- `Start Date`
- `Due Date`
- `Description`
- `Related Tasks`

Filters:
- Hide archived projects by default.
- Allow grouping by `Department`, `Roadmap`, and `Owner`.

Guardrails:
- Every task should remain linked to a project.
- Avoid creating tasks directly from unrelated places unless the project link is filled.

### Marketing Interface

Purpose: Keep Marketing execution focused on Campaigns, Content, and related Tasks.

Primary users: Marketing.

Main data:
- `Campaigns`
- `Content`
- `Tasks`
- `Projects`

Required sections:
- Active campaigns.
- Content calendar/list.
- Marketing tasks.
- Creative request follow-up if needed.

Key fields to show:
- Campaigns: campaign name/status/owner/date fields already used in Airtable.
- Content: content title/status/channel/date fields already used in Airtable.
- Tasks: `Task Name`, `Project`, `Related Campaign`, `Related Content`, `Owner`, `Status`, `Due Date`.

Filters:
- Show Marketing department tasks.
- Show active campaigns/content by default.

Guardrails:
- Marketing should use Campaigns and Content for marketing-specific planning.
- Execution work still lives in shared `Tasks`.

### Care Service Desk

Purpose: Give Care a daily helpdesk workspace.

Primary users: Care lead, Care agents.

Main data:
- `Care Tickets`
- `Contacts`
- `Organizations`
- `Tasks`

Required sections:
- New tickets.
- My open tickets.
- Urgent/high priority tickets.
- Awaiting user reply.
- Resolved tickets.
- Upsell potential.
- Ticket detail page.

Key fields to show:
- `Ticket ID`
- `Associated Contact`
- `Organization`
- `Issue Type`
- `Ticket Priority`
- `Ticket Status`
- `Upsell Potential`
- `Related Task`
- `Owner`
- `Notes`

Filters:
- Open tickets: `Ticket Status` is not `Resolved`.
- My tickets: `Owner` is current Airtable user.
- Urgent queue: `Ticket Priority` is `High` or `Urgent`.
- Upsell queue: `Upsell Potential` is checked.

Editable fields:
- Care can edit `Issue Type`, `Ticket Priority`, `Ticket Status`, `Upsell Potential`, `Related Task`, `Owner`, and `Notes`.

Guardrails:
- Care should not need to work from raw Contacts unless updating customer details.
- Product escalation in Milestone 3 should happen through notes and/or related shared Tasks.

### Scraped Listing Review

Purpose: Let Care review external listings, clean contact info, match contacts, and decide intervention.

Primary users: Care.

Main data:
- `Scraped Listing`
- `Contacts`

Required sections:
- New scraped listings.
- Missing cleaned email.
- No match yet.
- Existing user matched.
- Repeat posters.
- Recently reviewed.

Key fields to show:
- `Post Type`
- `Source URL`
- `Raw Contact Info`
- `Cleaned Email`
- `Repeat Poster Flag`
- `Existing User Cross-Check`
- `Matched Contact`
- `Notes`

Filters:
- Missing email: `Cleaned Email` is empty.
- Matched: `Existing User Cross-Check` is `Existing user matched`.
- No match: `Existing User Cross-Check` is `No match yet`.
- Repeat posters: `Repeat Poster Flag` indicates repeat.

Editable fields:
- Care can edit `Cleaned Email`, `Matched Contact`, and `Notes`.

Guardrails:
- Care manually fills `Matched Contact` for now.
- Automated email matching is deferred to Milestone 5 or later integrations.

### Product Request Submission

Purpose: Give non-Product teams a simple way to submit requests without editing Product decision fields.

Primary users: All teams.

Main data:
- `Product Requests`

Required sections:
- New request form.
- My submitted requests, if submitter tracking supports it.
- Request status lookup.

Fields for submitters:
- `Summary`
- `Details`
- `Submitted By`
- `Source Team`
- `Request Type`
- `Product Area`
- `Impact`

Fields hidden or read-only for non-Product users:
- `Priority`
- `Status`
- `Product Owner`
- `Related Project`
- `Related Task`
- `Final Decision / Notes`

Guardrails:
- Non-Product users submit context and view status.
- Product owns triage and final decisions.

### Product Triage

Purpose: Give Product one place to review, prioritize, accept, reject, or route incoming requests.

Primary users: Product owners.

Main data:
- `Product Requests`
- `Product Areas`
- `Projects`
- `Tasks`

Required sections:
- New requests.
- Needs more info.
- Accepted.
- In progress.
- Released/closed.
- Not planned.
- By product area.
- By priority/impact.

Key fields to show:
- `Request ID`
- `Summary`
- `Details`
- `Submitted By`
- `Source Team`
- `Request Type`
- `Product Area`
- `Priority`
- `Impact`
- `Status`
- `Product Owner`
- `Related Project`
- `Related Task`
- `Final Decision / Notes`

Editable fields:
- Product can edit all triage and decision fields.

Guardrails:
- Accepted requests should link to a `Project` or `Task` when execution begins.
- Small accepted requests can link directly to shared `Tasks`.

### Engineering / Product Task Board

Purpose: Give Product/Tech a board for execution work that still uses shared `Tasks`.

Primary users: Product, engineering/tech.

Main data:
- `Tasks`
- `Projects`
- `Sprints`
- `Product Areas`
- `Product Requests`
- `Bugs & Issues`
- `QA & Testing`

Required sections:
- Product/engineering task board by status.
- My product tasks.
- Tasks by sprint.
- Tasks by product area.
- Bug fix tasks.
- QA-related tasks.

Key fields to show:
- `Task Name`
- `Project`
- `Department`
- `Owner`
- `Status`
- `Priority`
- `Due Date`
- `Sprint`
- `Task Type`
- `Product Areas`
- `Related Product Request`
- `Related Bug`
- `QA & Testing`

Filters:
- Product/Tech department tasks.
- Or `Task Type` is Product, Engineering, Data, Design, or QA.

Guardrails:
- Do not create a Product Tasks table.
- All execution work stays in shared `Tasks`.

### Bug Queue

Purpose: Give Product/Tech a focused bug tracking surface.

Primary users: Product, engineering/tech.

Main data:
- `Bugs & Issues`
- `Tasks`
- `QA & Testing`
- `Releases`

Required sections:
- New bugs.
- Critical/high severity.
- In progress.
- Fixed waiting for QA.
- QA passed.
- Released.

Key fields to show:
- `Bug ID`
- `Bug Summary`
- `Product Area`
- `Severity`
- `Status`
- `Reported By`
- `Related Task`
- `Reproduction Steps`
- `Expected Behavior`
- `Actual Behavior`
- `Attachments`
- `Release`
- `QA & Testing`

Guardrails:
- Bugs should link to a shared `Task` when engineering work is needed.
- QA should be tracked in `QA & Testing`, not only in bug notes.

### QA Dashboard

Purpose: Let QA/Product track what needs testing and what failed.

Primary users: Product, QA, engineering leads.

Main data:
- `QA & Testing`
- `Tasks`
- `Bugs & Issues`
- `Releases`

Required sections:
- Not started.
- Failed.
- Blocked.
- Passed.
- By release.
- By tester.

Key fields to show:
- `Test Case ID`
- `Test Name`
- `Related Task`
- `Related Bug`
- `Related Release`
- `Tester`
- `QA Status`
- `Test Steps`
- `Actual`
- `Result`
- `Tested Date`

Filters:
- Failed/blocked queue should be easy to find.
- Release-specific QA should filter by `Related Release`.

Guardrails:
- QA results should update `QA Status`, `Actual`, `Result`, and `Tested Date`.
- Failed QA should remain visible for Milestone 5 automation.

### Release Dashboard

Purpose: Give Product a simple release readiness and history view.

Primary users: Product owners, managers.

Main data:
- `Releases`
- `QA & Testing`
- `Changelog`

Required sections:
- Planning.
- In QA.
- Ready.
- Released.
- Rolled back.
- Changelog needed.

Key fields to show:
- `Release ID`
- `Release Name`
- `Release Status`
- `Release Date`
- `Teams to Notify`
- `Release Notes`
- `QA & Testing`
- `Changelog`

Guardrails:
- Release should not be marked `Released` until QA status is acceptable and changelog is ready when needed.
- Release ownership is handled by process/notes for now; no `Release Owner` field needed.

### Changelog View

Purpose: Help Product write and share release/change messaging with Care, Marketing, and internal teams.

Primary users: Product, Care, Marketing, managers.

Main data:
- `Changelog`
- `Releases`

Required sections:
- Draft/internal changes.
- User-facing messages.
- By audience.
- Published entries.

Key fields to show:
- `Changelog Title`
- `Release`
- `Audience`
- `Summary`
- `Recommended Message`
- `Owner`
- `Published Date`

Guardrails:
- Product owns final wording.
- Care and Marketing can use recommended messages but should not overwrite Product decision wording unless assigned.

### Manager Dashboard

Purpose: Give managers a cross-department view of work health.

Primary users: Managers, leadership.

Main data:
- `Projects`
- `Tasks`
- `Care Tickets`
- `Product Requests`
- `Bugs & Issues`
- `Releases`

Required sections:
- Work by department.
- Open high-priority work.
- Overdue tasks/projects.
- Product intake status.
- Care ticket status.
- Bug severity summary.
- Release status summary.
- Upsell potential count/list.

Key fields to show:
- Department, owner, status, priority, due dates, and linked records needed to drill into work.

Filters:
- Hide archived records.
- Show active/open records by default.

Guardrails:
- Managers should be able to inspect and follow up, but daily editing should happen in team-specific interfaces.

### Sales / Account Management View

Status: Deferred for now.

Current substitute:
- Create a filtered view or section for `Care Tickets` where `Upsell Potential` is checked.

Reason:
- `Opportunities` is deferred until Sales/Account Management workflow is defined.

## Milestone 4 Completion Checklist

- [ ] Existing interfaces reviewed.
- [ ] Care Service Desk exists.
- [ ] Scraped Listing Review exists.
- [ ] Product Request Submission exists.
- [ ] Product Triage exists.
- [ ] Engineering / Product Task Board exists.
- [ ] Bug Queue exists.
- [ ] QA Dashboard exists.
- [ ] Release Dashboard exists.
- [ ] Changelog View exists.
- [ ] Manager Dashboard exists.
- [ ] Sales / Account Management View is deferred or replaced with Upsell Potential view.
- [ ] Non-Product users have a simple request submission path.
- [ ] Care users have a daily service desk path.
- [ ] Managers can see cross-department work without raw-table cleanup.
- [ ] Interfaces use filtered views and field visibility as guardrails.
