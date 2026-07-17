# Airtable AI Prompts

Use these prompts with Airtable AI / Omni AI to create or revise the EDU Passport Operations Hub.

Run the prompts in order. Review each result before continuing.

Source of truth: [Operations Hub requirements](README.md).

## Base And Core Tables

```text
Create or revise an Airtable base named "EDU Passport Operations Hub".

Purpose:
This base is the main shared execution hub for non-sensitive company work: departments, roadmaps, projects, tasks, Product, Marketing, Operations, AI & Automation, and cross-department reporting.

Use these core execution tables:
- Departments
- Roadmaps
- Projects
- Tasks

Do not create these tables:
- Team Members
- Opportunities
- Contacts
- Organizations
- Care Tickets
- Scraped Listing
- HR Requests
- Employees
- Finance Requests
- Budget Plans
- Budget Lines
- accounting transactions
- bank accounts
- document storage

Base rules:
- One shared Tasks table is the execution source of truth.
- Every Task must link to one Project.
- Projects link to Roadmaps and Departments.
- Roadmaps link to Departments.
- Use collaborator / Airtable user fields directly for owners and assignees.
- Do not create HR, Finance, Care, CRM, Sales pipeline, payroll, banking, accounting, or secure-document workflows in this base.
- Do not create cross-base synchronization.
- If a specified table or field already exists, revise it instead of creating a duplicate.

Create or revise these tables and fields.

1. Departments
Use this table for company departments used by roadmaps, projects, tasks, and reporting.

Fields:
- Department Name: primary single line text.
- Department Lead: collaborator.
- Status: single select: Active, Inactive.
- Description: long text.
- Projects: backlink from Projects.
- Tasks: backlink from Tasks, if Tasks links directly to Departments.
- Roadmaps: backlink from Roadmaps.
- Team Member: collaborator field only, not a separate table.

Required department records:
- Marketing
- Product
- Operations
- AI & Automation
- Leadership

2. Roadmaps
Use this table for strategic plans and time-bound themes.

Fields:
- Roadmap Name: primary single line text.
- Owner: collaborator.
- Status: single select: Planned, Active, Paused, Complete, Archived.
- Year: number or single select.
- Quarter: single select: Q1, Q2, Q3, Q4, H1, H2, Full Year.
- Department: linked record to Departments.
- Start Date: date.
- End Date: date.
- Related Projects: backlink from Projects.
- Goals: long text.
- Description: long text.

3. Projects
Use this table as the central planning container. Every Task belongs to one Project.

Fields:
- Project Name: primary single line text.
- Department: linked record to Departments.
- Roadmap: linked record to Roadmaps.
- Owner: collaborator.
- Status: single select: Not Started, In Progress, Blocked, Done, Archived.
- Priority: single select: Urgent, High, Medium, Low.
- Start Date: date.
- Due Date: date.
- Description: long text.
- Related Tasks: backlink from Tasks.
- Related Campaigns: linked records to Campaigns, if Campaigns already exists.
- Related Contents: linked records to Content, if Content already exists.
- Sprint: linked record to Sprints, if Sprints already exists.
- Creative Requests: linked records to Creative Requests, if Creative Requests already exists.

4. Tasks
Use this table for all non-sensitive execution work.

Fields:
- Task Name: primary single line text.
- Project: linked record to Projects; required.
- Department: linked record to Departments or lookup from Project.
- Owner: collaborator.
- Status: single select: To Do, In Progress, Blocked, Ready for Review, Done, Archived.
- Priority: single select: Urgent, High, Medium, Low.
- Start Date: date.
- Due Date: date.
- Description: long text.
- Attachments: attachment.
- Related Campaign: linked record to Campaigns, if Campaigns already exists.
- Related Content: linked record to Content, if Content already exists.
- Related Creative Request: linked record to Creative Requests, if Creative Requests already exists.
- Milestone: single select or linked record.
- Sprint: linked record to Sprints, if Sprints already exists.
- Created By: created by.
- Created: created time.
- Last Update: last modified time.

Add one-level subtask support:
- Parent Task: linked record to Tasks; limit to one parent task.
- Subtasks: backlink from Parent Task.
- Task Level: formula:
  IF({Parent Task}, "Subtask", "Task")
- Task Complete Flag: formula:
  IF({Status} = "Done", 1, 0)
- Subtask Count: count linked records in Subtasks.
- Completed Subtask Count: rollup Subtasks -> Task Complete Flag using SUM(values).
- Subtask Progress: formula, formatted as percent:
  IF({Subtask Count} = 0, BLANK(), {Completed Subtask Count} / {Subtask Count})

Task behavior:
- Subtasks are normal records in Tasks, not a separate table.
- Every subtask must still link to a Project.
- Use Parent Task only for one level of nesting.
- Use Description for small checklist items instead of creating unnecessary subtasks.

Create useful views without adding fields:
- Tasks: My Open Tasks.
- Tasks: Overdue Tasks.
- Tasks: Blocked Tasks.
- Tasks: Ready for Review.
- Tasks: Subtasks.
- Projects: Active Projects.
- Projects: Blocked Projects.
- Roadmaps: Active Roadmaps.
- Departments: Active Departments.

Before finishing:
- Confirm every Task has a Project.
- Confirm no Team Members table exists.
- Confirm no Opportunities, Care, CRM, HR, Finance, accounting, banking, or document-storage tables exist.
- Confirm no duplicate fields exist.
- Confirm no cross-base sync exists.
```

## Product Workflow

```text
Create or revise the Product workflow in the EDU Passport Operations Hub.

Purpose:
Product work uses dedicated Product workflow tables for intake, triage, bugs, QA, releases, and changelog, while execution remains visible in shared Projects and Tasks.

Use these tables:
- Product Requests
- Product Areas
- Bugs & Issues
- QA & Testing
- Releases
- Changelog
- Projects
- Tasks

Do not create a separate Product Tasks table.
Do not create a separate Product Roadmap table.
Do not create Care, CRM, Sales, HR, or Finance workflow tables.

Create or revise these Product tables and fields.

1. Product Requests
Fields:
- Request ID: autonumber.
- Summary: primary single line text.
- Details: long text.
- Submitted By: collaborator or text.
- Source Team: single select: Care, Marketing, Growth, Product, Leadership, User.
- Request Type: single select: Feature Request, Bug, UX Issue, Data Issue, Content Issue, Operational Request.
- Product Area: linked record to Product Areas.
- Priority: single select: Urgent, High, Medium, Low.
- Impact: single select: One user, Multiple users, Key account, Revenue impact, Blocking workflow.
- Status: single select: New, Under Review, Needs More Info, Accepted, In Progress, Released, Not Planned, Closed.
- Product Owner: collaborator.
- Related Project: linked record to Projects.
- Related Task: linked record to Tasks.
- Final Decision / Notes: long text.

2. Product Areas
Fields:
- Product Area Name: primary single line text.
- Owner: collaborator.
- Status: single select: Active, Inactive.
- Description: long text.
- Product Requests: backlink from Product Requests.
- Bugs & Issues: backlink from Bugs & Issues.
- Tasks: linked records to Tasks, if Tasks links to Product Areas.

3. Bugs & Issues
Fields:
- Bug ID: autonumber.
- Bug Summary: primary single line text.
- Product Area: linked record to Product Areas.
- Severity: single select: Critical, High, Medium, Low.
- Status: single select: New, Confirmed, In Progress, Fixed, QA Passed, Released, Cannot Reproduce.
- Reported By: collaborator or text.
- Related Task: linked record to Tasks.
- Reproduction Steps: long text.
- Expected Behavior: long text.
- Actual Behavior: long text.
- Attachments: attachment.
- Release: linked record to Releases.
- QA & Testing: backlink from QA & Testing.

4. QA & Testing
Fields:
- Test Case ID: autonumber.
- Test Name: primary single line text.
- Related Task: linked record to Tasks.
- Related Bug: linked record to Bugs & Issues.
- Related Release: linked record to Releases.
- Tester: collaborator.
- QA Status: single select: Not Started, Passed, Failed, Blocked.
- Test Steps: long text.
- Actual: long text.
- Result: long text or single select.
- Tested Date: date.

5. Releases
Fields:
- Release ID: autonumber.
- Release Name: primary single line text.
- Release Status: single select: Planning, QA, Ready, Released, Rolled Back.
- Release Date: date.
- Teams to Notify: multiple select: Care, Marketing, Growth, Leadership, Users.
- Release Notes: long text.
- QA & Testing: backlink from QA & Testing.
- Changelog: backlink from Changelog.

6. Changelog
Fields:
- Changelog Title: primary single line text.
- Release: linked record to Releases.
- Audience: single select: Internal, Care, Marketing, Growth, Users.
- Summary: long text.
- Recommended Message: long text.
- Owner: collaborator.
- Published Date: date.

Add Product-related fields to Tasks if missing:
- Task Type: single select: Product, Design, Engineering, Data, QA, General.
- Related Product Request: linked record to Product Requests.
- Related Bug: linked record to Bugs & Issues.
- QA & Testing: linked records to QA & Testing.
- Product Areas: linked records to Product Areas.

Create useful views without adding fields:
- Product Requests: New / Under Review.
- Product Requests: Accepted / In Progress.
- Bugs & Issues: New / Confirmed.
- Bugs & Issues: Critical / High.
- QA & Testing: Failed / Blocked.
- Releases: Planning / QA / Ready.
- Changelog: Unpublished.

Before finishing:
- Confirm accepted Product Requests can link to a Project or Task.
- Confirm bug fixes can link to shared Tasks.
- Confirm QA can link to Tasks, Bugs, and Releases.
- Confirm Releases can link to Changelog.
- Confirm no Product Tasks table or Product Roadmap table exists.
```

## Marketing And Creative Workflow

```text
Create or revise the Marketing and Creative workflow surfaces in the EDU Passport Operations Hub.

Purpose:
Marketing can use Campaigns, Content, and Creative Requests for marketing-specific planning and intake where those tables already exist, but execution work remains in shared Tasks.

Use these tables where they already exist:
- Campaigns
- Content
- Creative Requests
- Projects
- Tasks

Do not create duplicate Campaigns, Content, Creative Requests, or Marketing Tasks tables.
Do not create Care, CRM, Sales pipeline, HR, or Finance workflow tables.

If Campaigns already exists, verify it can show:
- campaign name
- status
- owner
- date fields already used in Airtable
- related Projects or Tasks where already configured

If Content already exists, verify it can show:
- content title
- status
- channel
- owner
- date fields already used in Airtable
- related Campaign or Task where already configured

If Creative Requests already exists, verify it can show:
- request title or name
- requester
- owner
- status
- priority
- due date
- related Project or Task where already configured

Task behavior:
- Marketing execution tasks use the shared Tasks table.
- Creative follow-up tasks use the shared Tasks table.
- Use Related Campaign, Related Content, and Related Creative Request on Tasks where those fields exist.
- Do not create separate execution tables for Marketing tasks or Creative tasks.

Create useful views without adding fields:
- Tasks: Marketing Open Tasks.
- Tasks: Marketing Overdue Tasks.
- Tasks: Creative Request Follow-Up.
- Campaigns: Active Campaigns, if Campaigns exists.
- Content: Content Pipeline, if Content exists.

Before finishing:
- Confirm Campaigns, Content, and Creative Requests are not duplicated.
- Confirm execution work is represented in shared Tasks.
- Confirm every Marketing or Creative task links to one Project.
```

## Operations And AI Automation

```text
Create or revise Operations and AI & Automation structures in the EDU Passport Operations Hub.

Purpose:
Operations manages non-sensitive administration through shared Projects and Tasks. AI & Automation manages company-wide AI use cases, automations, integrations, reporting, and operational delivery through a dedicated department, shared Projects and Tasks.

Use these tables:
- Departments
- Roadmaps
- Projects
- Tasks

Do not create separate Operations, AI & Automation, HR, Finance, Care, CRM, or Sales pipeline bases or tables.

Department setup:
- Confirm one active Departments record named Operations.
- Confirm one active Departments record named AI & Automation.
- Assign Department Lead values where known.

Operations behavior:
- Create or use purpose-specific Operations Projects for non-sensitive administration, vendor coordination, equipment, facilities, recurring work, approvals, renewals, blockers, and overdue tasks.
- Do not use a permanent miscellaneous project when a purpose-specific or annual project would be clearer.
- Do not store restricted HR, Finance, Care, CRM, Sales, banking, payroll, tax, legal, or secure-document details in Operations tasks.

AI & Automation behavior:
- AI, automation, integration, reporting, and operating work should link to a Project.
- Build, testing, launch, review, and maintenance work should be tracked in shared Tasks.
- Do not store credentials, API keys, passwords, source-system secrets, or restricted implementation details in Airtable.

Create useful views without adding fields:
- Tasks: Operations Open Tasks.
- Tasks: AI & Automation Open Tasks.

Before finishing:
- Confirm Operations and AI & Automation use shared Projects and Tasks.
- Confirm no credentials, API keys, passwords, or secrets are stored.
- Confirm no restricted Corporate Services records are copied into the Operations Hub.
```

## Interfaces

```text
Create or revise Operations Hub interfaces.

Purpose:
Interfaces should make the shared Operations Hub usable for leadership, individual task owners, Marketing, AI & Automation, Product, Care task execution, request submitters, and project owners without creating separate execution tables.

Page permissions below are Airtable interface permissions and process guardrails. They are not new schema fields.

Create or revise only these active interfaces and pages.

1. Executive Dashboard
Use Tasks.
Pages:
- Department tasks: List. Filter or group by Department. Add No, Edit No, Delete No.
- Open High Priority tasks: List. Filter Priority is High or Urgent and Status is not Done or Archived. Add No, Edit No, Delete No.
- Overdue tasks: List. Filter Due Date is before today and Status is not Done or Archived. Add No, Edit No, Delete No.

2. My Tasks
Use Tasks.
Pages:
- All tasks: Calendar and List. Filter Owner is current Airtable user where possible. Add Yes, Edit Yes, Delete Yes.
- Due this week: Calendar and List. Filter Owner is current Airtable user where possible, Due Date is this week, and Status is not Done or Archived. Add No, Edit Yes, Delete Yes.
- Open tasks: Calendar and List. Filter Owner is current Airtable user where possible and Status is not Done or Archived. Add No, Edit Yes, Delete Yes.
- Overdue: Calendar and List. Filter Owner is current Airtable user where possible, Due Date is before today, and Status is not Done or Archived. Add No, Edit Yes, Delete Yes.

3. Marketing Dept
Use Tasks, Campaigns, and Creative Requests where those tables already exist.
Pages:
- All tasks: Tasks, List. Filter Department is Marketing. Add No, Edit Yes, Delete Yes.
- Campaign Calendar: Campaigns, List and Calendar. Show all Campaigns. Add Yes, Edit Yes, Delete Yes.
- Ops Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is Marketing Operations. Add Yes, Edit Yes, Delete Yes.
- Content Pipeline: Tasks, Kanban, Calendar, and List. Filter Department is Marketing and Project is not EDU Blogs and not Marketing Operations. Add Yes, Edit Yes, Delete Yes.
- Blog Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is EDU Blogs. Add Yes, Edit Yes, Delete Yes.
- Creative Request Pipeline: Creative Requests, List and Kanban. Add No, Edit Yes, Delete No.

4. AI & Automation Dept
Use Tasks.
Pages:
- All tasks: Tasks, List. Filter Department is AI & Automation. Add No, Edit Yes, Delete No.
- Ops Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is AI & Automation Ops. Add Yes, Edit Yes, Delete Yes.
- SM Posting Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is SM Posting. Add Yes, Edit Yes, Delete Yes.
- Internal Report Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is Internal Report. Add Yes, Edit Yes, Delete Yes.

5. Product Dept
Use Tasks, Bugs & Issues, QA & Testing, Releases, Product Requests, Sprints, and Changelog.
Pages:
- All tasks: Tasks, List. Filter Department is Product. Add No, Edit Yes, Delete No.
- Bugs: Bugs & Issues and linked Tasks, List and Kanban. Add/Edit/Delete not specified.
- QA & Testing: QA & Testing, List and Kanban. Add Yes, Edit Yes, Delete Yes.
- Ops Pipeline: Releases, Kanban. Add Yes, Edit Yes, Delete Yes.
- Release Pipeline: Releases, Kanban and Calendar. Add Yes, Edit Yes, Delete Yes.
- Product Request Pipeline: Product Requests, List and Kanban. Add No, Edit Yes, Delete No.
- Sprint: Sprints, List and Calendar. Add Yes, Edit Yes, Delete Yes.
- Changelog: Changelog, List. Add Yes, Edit Yes, Delete Yes.

Create Release Pipeline only once.

6. Care Dept
Use Tasks only.
Pages:
- All tasks: Tasks, List. Filter Department is Care. Add No, Edit Yes, Delete No.
- Ops Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is Care Operations. Add Yes, Edit Yes, Delete Yes.
- EDU Academy Pipeline: Tasks, Kanban, Calendar, and List. Filter Project is EDU Academy. Add Yes, Edit Yes, Delete Yes.

Do not add Care Tickets, Scraped Listing, Contacts, Organizations, Opportunities, Sales, or Account Management pages to Care Dept.

7. Product Request Submission
Use Product Requests.
Pages:
- New Product Request: Form. Add Yes, Edit No, Delete No.
- Request Status: List and Kanban. Add No, Edit No, Delete No.

8. Creative Request Submission
Use Creative Requests.
Pages:
- New Creative Request: Form. Add Yes, Edit No, Delete No.
- Request Status: List and Kanban. Add No, Edit No, Delete No.

9. Bug Reporting
Use Bugs & Issues.
Pages:
- Report Bugs & Issues: Form. Add Yes, Edit No, Delete No.
- Bug Status: List and Kanban. Add No, Edit No, Delete No.

10. Releases
Use Releases.
Pages:
- Release Schedule: Kanban and Calendar. Add No, Edit No, Delete No.

11. Roadmap & Projects
Use Roadmaps and Projects.
Pages:
- Active Roadmaps: Roadmaps, List. Filter Status is not Archived. Add Yes, Edit Yes, Delete Yes.
- Active Projects: Projects, List. Filter Status is not Archived. Add Yes, Edit Yes, Delete Yes.
- Project Calendar: Projects, Calendar. Filter Status is not Archived. Add No, Edit Yes, Delete No.
- Project by Department: Projects, List. Group by Department and filter Status is not Archived. Add No, Edit Yes, Delete No.

Remove or stop using these active Operations Hub interfaces:
- Product Triage
- Bug Queue
- QA Dashboard
- Release Dashboard
- AI & Automation Workspace
- Operations Workspace
- Manager Dashboard
- Changelog View
- Care Service Desk
- Scraped Listing Review

Interface behavior:
- Keep layouts practical and work-focused.
- Do not expose restricted HR or Finance details.
- Care Dept must be task-only.
- Do not add Care, CRM, scraped listing, Sales pipeline, or Account Management workflow pages.
- New Tasks created from department pipeline pages must link to the filtered Project.
- Do not create duplicate fields.
- If a suggested field does not exist and is not required, skip it instead of adding complexity.
```

## Native Automations

```text
Create simple native Airtable automations for the EDU Passport Operations Hub.

Purpose:
Automations should improve visibility for shared execution work without replacing human review or creating external integrations.

Use these tables:
- Tasks
- Projects
- Product Requests
- Bugs & Issues
- QA & Testing
- Releases

Keep automations simple. Create only native Airtable automations.

1. Operations Hub - Daily Task Digest
Schedule daily at a documented approved time and timezone.
Find Tasks where:
- Status is not Done or Archived.
- Due Date is today, overdue, or inside the approved reminder window.
Notify Task Owner when available.

2. Operations Hub - Blocked Work Digest
Schedule daily.
Find Tasks where:
- Status is Blocked.
Find Projects where:
- Status is Blocked.
Notify the owner or designated fallback.

3. Product Dept - Review Digest
Schedule daily.
Find Product Requests where:
- Status is New, Under Review, or Needs More Info.
Find Bugs & Issues where:
- Status is New or Confirmed.
- Severity is Critical or High, where available.
Notify Product Owner or designated fallback.

4. QA And Release Review Digest
Schedule daily during active release periods.
Find QA & Testing records where:
- QA Status is Failed or Blocked.
Find Releases where:
- Release Status is QA or Ready.
Notify Tester, Owner, or designated fallback where available.

Automation behavior:
- Use native Airtable automation actions only.
- Do not use scripts or external integration tools.
- Do not approve, complete, archive, or otherwise update records automatically.
- Do not create cross-base sync.
- Do not send credentials, API keys, secure links, banking data, payroll data, HR case details, Finance details, or restricted documents in notifications.
- Do not create duplicate automations.
```

## Manual Security And Acceptance Checks

```text
Review the EDU Passport Operations Hub before launch.

Purpose:
These checks keep the shared Operations Hub focused on non-sensitive execution and prevent dedicated or restricted workflows from leaking into it.

Check these items:
- Every active Task links to one Project.
- Projects link to Roadmaps and Departments.
- Roadmaps link to Departments.
- Owners and assignees use collaborator / Airtable user fields.
- No Team Members table exists.
- No Opportunities table exists.
- No Care, CRM, scraped listing, HR, Finance, accounting, banking, payroll, or document-storage workflow table exists.
- Operations uses shared Projects and Tasks for non-sensitive administration.
- AI & Automation uses a Departments record, shared Projects, and shared Tasks.
- Product execution uses shared Tasks, not a Product Tasks table.
- Marketing execution uses shared Tasks, not a Marketing Tasks table.
- Restricted HR and Finance details are not copied into Tasks, Projects, dashboards, interfaces, or automations.
- Care, CRM, and Sales / Account Management details are not copied into Tasks, Projects, dashboards, interfaces, or automations.
- Credentials, passwords, API keys, banking details, payment attachments, payroll records, and unrestricted secure documents are not stored in Airtable.
- No cross-base sync exists.
- Test with non-sensitive sample records before enabling automations.

Review behavior:
- Do not create duplicate fields.
- If a suggested field or view does not exist and is not required for the MVP, skip it instead of adding complexity.
```
