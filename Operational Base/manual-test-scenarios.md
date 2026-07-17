# Operations Hub Manual Test Scenarios

## Summary

Use this checklist to manually test the EDU Passport Operations Hub in Airtable.

The tests validate:

- core department, roadmap, project, and task structure
- shared task execution and one-level subtasks
- Product workflow from request through release and changelog
- Marketing, AI & Automation, Product, and Care department task interfaces
- request submission interfaces
- roadmap and project planning interfaces
- page-level Add/Edit/Delete guardrails
- native Airtable MVP automations
- boundary guardrails for dedicated and restricted bases

## Assumptions

- The base is `EDU Passport Operations Hub`.
- The Operations Hub is the shared execution base for non-sensitive company work.
- Product, Marketing, Care, and AI & Automation use shared `Projects` and `Tasks` for department task execution.
- Care Dept is task-only inside the Operations Hub.
- Every Task belongs to one Project.
- Owners and assignees use Airtable collaborator/user fields directly.
- Care tickets, scraped listings, CRM records, Sales / Account Management, HR, and Finance workflows live outside this base.
- Airtable automations are native Airtable automations only.
- No cross-base sync is enabled.

## Interfaces

### Shared And Planning Interfaces

Recommended active interfaces:

- `Executive Dashboard`
- `My Tasks`
- `Roadmap & Projects`

Primary tables:

- `Departments`
- `Roadmaps`
- `Projects`
- `Tasks`

### Department Interfaces

Recommended active interfaces:

- `Marketing Dept`
- `AI & Automation Dept`
- `Product Dept`
- `Care Dept`

Primary tables:

- `Tasks`
- `Campaigns`, where already present
- `Creative Requests`, where already present
- `Bugs & Issues`
- `QA & Testing`
- `Releases`
- `Product Requests`
- `Sprints`, where already present
- `Changelog`

### Submission And Visibility Interfaces

Recommended active interfaces:

- `Product Request Submission`
- `Creative Request Submission`
- `Bug Reporting`
- `Releases`

Primary tables:

- `Product Requests`
- `Creative Requests`
- `Bugs & Issues`
- `Releases`

## Automation Views To Verify

Create or verify these table views before testing automations.

| Table | View | Purpose |
| --- | --- | --- |
| `Tasks` | `AUTOMATION - Due Soon Or Overdue Tasks` | Tasks that should appear in the daily task digest. |
| `Tasks` | `AUTOMATION - Blocked Tasks` | Blocked tasks that need owner or manager review. |
| `Projects` | `AUTOMATION - Blocked Projects` | Blocked projects that need review. |
| `Product Requests` | `AUTOMATION - Product Request Queue` | Product requests needing Product Dept review. |
| `Bugs & Issues` | `AUTOMATION - Critical Or New Bugs` | Important bugs needing Product review. |
| `QA & Testing` | `AUTOMATION - Failed Or Blocked QA` | QA records needing follow-up. |
| `Releases` | `AUTOMATION - QA Or Ready Releases` | Releases needing release review. |

## Manual Test Scenarios

### 1. Core Structure Setup

**Purpose:** Confirm Departments, Roadmaps, Projects, and Tasks support shared execution.

**Interface to test from:** `Roadmap & Projects`

**Starting tables:** `Departments`, `Roadmaps`, `Projects`, `Tasks`

**Setup data:**

- Use non-sensitive sample records only.
- Prepare one sample department, roadmap, project, and task.

**Steps:**

1. Confirm `Operations`, `AI & Automation`, `Product`, `Marketing`, and `Care` exist as active Departments.
2. Create or open one Roadmap linked to a Department.
3. Create or open one Project linked to that Roadmap and Department.
4. Create one Task linked to that Project.
5. Assign a collaborator in `Owner`.
6. Set Status, Priority, Start Date, and Due Date.

**Expected result:**

- Roadmap links to Department.
- Project links to Roadmap and Department.
- Task links to Project.
- Task owner uses a collaborator/user field.
- No orphan Task is created.

**Result:**

- [ ] Pass
- [ ] Fail

### 2. My Tasks And Shared Execution

**Purpose:** Confirm individual task owners can work from the shared Tasks table.

**Interface to test from:** `My Tasks`

**Starting table:** `Tasks`

**Setup data:**

- Create one open Task assigned to the test user.
- Create one open Task assigned to another user.
- Create one Done Task assigned to the test user.

**Steps:**

1. Open `My Tasks`.
2. Confirm `All tasks` can show the test user's Tasks in Calendar and List visualizations.
3. Confirm `Due this week`, `Open tasks`, and `Overdue` apply the correct date/status filters.
4. Confirm Add is enabled only on `All tasks`.
5. Confirm Edit and Delete are enabled on all My Tasks pages.
6. Change the Task status to `Ready for Review`.

**Expected result:**

- The interface shows the current user's actionable work.
- Status changes save on the shared Tasks record.
- Add/Edit/Delete behavior matches the interface requirements.
- No separate department-specific task table is used.

**Result:**

- [ ] Pass
- [ ] Fail

### 3. One-Level Subtasks

**Purpose:** Confirm subtasks work inside the shared Tasks table without creating a separate table.

**Interface to test from:** `Roadmap & Projects` or `My Tasks`

**Starting table:** `Tasks`

**Setup data:**

- Use one existing parent Task.

**Steps:**

1. Create two child Tasks.
2. Link each child Task to the same `Parent Task`.
3. Confirm each child Task still links to a Project.
4. Set one child Task to `Done`.
5. Leave one child Task open.
6. Review `Task Level`, `Subtask Count`, `Completed Subtask Count`, and `Subtask Progress` on the parent Task.

**Expected result:**

- Child records are normal Tasks.
- Each child Task has one Project.
- `Task Level` identifies child records as Subtask.
- Parent progress reflects one completed child out of two.
- No second-level nesting is used.

**Result:**

- [ ] Pass
- [ ] Fail

### 4. Product Request To Execution

**Purpose:** Confirm Product Requests can be submitted, reviewed in Product Dept, and linked to execution work.

**Interface to test from:** `Product Request Submission` and `Product Dept`

**Starting tables:** `Product Requests`, `Product Areas`, `Projects`, `Tasks`

**Setup data:**

- Use a non-sensitive product request example.
- Use one active Product Area.

**Steps:**

1. Submit a Product Request from `New Product Request`.
2. Confirm `Request Status` is List and Kanban and is read-only.
3. Open `Product Dept` -> `Product Request Pipeline`.
4. Set Status to `Under Review`.
5. Assign `Product Owner`.
6. Set Status to `Accepted`.
7. Link the request to an existing Project or create a Task linked to one Project.

**Expected result:**

- Product intake uses the submission interface.
- Product review uses Product Dept.
- Accepted work links to shared Projects or Tasks.
- No Product Triage interface or Product Tasks table is used.

**Result:**

- [ ] Pass
- [ ] Fail

### 5. Bug, QA, Release, Sprint, And Changelog Flow

**Purpose:** Confirm Product delivery surfaces are consolidated into Product Dept, Bug Reporting, and Releases.

**Interface to test from:** `Bug Reporting`, `Product Dept`, and `Releases`

**Starting tables:** `Bugs & Issues`, `Tasks`, `QA & Testing`, `Releases`, `Sprints`, `Changelog`

**Setup data:**

- Use a non-sensitive fake bug.
- Use one shared Task for the fix.

**Steps:**

1. Submit a bug from `Bug Reporting` -> `Report Bugs & Issues`.
2. Confirm `Bug Status` is List and Kanban and is read-only.
3. Open `Product Dept` -> `Bugs`.
4. Link the Bug to a shared Task where engineering work is needed.
5. Create a QA & Testing record from `Product Dept` -> `QA & Testing`.
6. Create or update a Sprint from `Product Dept` -> `Sprint`.
7. Create or update a Release from `Product Dept` -> `Release Pipeline`.
8. Confirm the separate `Releases` interface shows `Release Schedule` as read-only Kanban and Calendar.
9. Create a Changelog entry from `Product Dept` -> `Changelog`.

**Expected result:**

- Bug intake uses Bug Reporting.
- Product execution and QA use Product Dept.
- Release visibility uses the read-only Releases interface.
- Changelog is maintained in Product Dept.
- Removed Product interfaces are not needed for this flow.

**Result:**

- [ ] Pass
- [ ] Fail

### 6. Marketing Dept Interface

**Purpose:** Confirm Marketing work uses the requested Marketing Dept pages.

**Interface to test from:** `Marketing Dept`

**Starting tables:** `Tasks`, `Campaigns`, `Creative Requests`

**Setup data:**

- Use one Marketing Task.
- Use one `Marketing Operations` Project.
- Use one `EDU Blogs` Project.
- Use one Marketing Project that is neither `EDU Blogs` nor `Marketing Operations`.

**Steps:**

1. Confirm `All tasks` shows Marketing department Tasks in List view and does not allow Add.
2. Confirm `Campaign Calendar` shows Campaigns in List and Calendar and allows Add, Edit, and Delete.
3. Confirm `Ops Pipeline` shows Tasks under project `Marketing Operations` in Kanban, Calendar, and List.
4. Confirm `Content Pipeline` excludes project `EDU Blogs` and project `Marketing Operations`.
5. Confirm `Blog Pipeline` shows Tasks under project `EDU Blogs`.
6. Confirm `Creative Request Pipeline` shows Creative Requests in List and Kanban, allows Edit, and does not allow Add or Delete.

**Expected result:**

- Marketing Dept replaces Marketing Interface.
- Marketing execution remains in shared Tasks.
- Project filters route work into the correct pipeline pages.
- Add/Edit/Delete behavior matches the interface requirements.

**Result:**

- [ ] Pass
- [ ] Fail

### 7. AI & Automation Dept Interface

**Purpose:** Confirm AI & Automation has department task pages without using the removed workspace interface.

**Interface to test from:** `AI & Automation Dept`

**Starting tables:** `Departments`, `Projects`, `Tasks`

**Setup data:**

- Use sample Projects named `AI & Automation Ops`, `SM Posting`, and `Internal Report`.
- Use non-sensitive sample Tasks only.

**Steps:**

1. Confirm `All tasks` shows AI & Automation department Tasks and does not allow Add or Delete.
2. Confirm `Ops Pipeline` filters to project `AI & Automation Ops`.
3. Confirm `SM Posting Pipeline` filters to project `SM Posting`.
4. Confirm `Internal Report Pipeline` filters to project `Internal Report`.
5. Confirm the three pipeline pages support Kanban, Calendar, and List and allow Add, Edit, and Delete.

**Expected result:**

- AI & Automation Dept replaces AI & Automation Workspace.
- Department-wide review and project pipeline pages are separated.
- New pipeline Tasks still link to one Project.

**Result:**

- [ ] Pass
- [ ] Fail

### 8. Care Dept Task Interface

**Purpose:** Confirm Care Dept is task-only inside the Operations Hub.

**Interface to test from:** `Care Dept`

**Starting tables:** `Departments`, `Projects`, `Tasks`

**Setup data:**

- Use sample Projects named `Care Operations` and `EDU Academy`.
- Use non-sensitive Care department Tasks only.

**Steps:**

1. Confirm `All tasks` shows Care department Tasks and does not allow Add or Delete.
2. Confirm `Ops Pipeline` filters to project `Care Operations`.
3. Confirm `EDU Academy Pipeline` filters to project `EDU Academy`.
4. Confirm the two pipeline pages support Kanban, Calendar, and List and allow Add, Edit, and Delete.
5. Confirm the interface does not include Care Tickets, Scraped Listing, Contacts, Organizations, Opportunities, Sales, or Account Management pages.

**Expected result:**

- Care Dept contains only shared Task pages.
- Care workflow records remain outside the Operations Hub.
- New pipeline Tasks still link to one Project.

**Result:**

- [ ] Pass
- [ ] Fail

### 9. Roadmap & Projects Interface

**Purpose:** Confirm planning pages replace the old Projects interface.

**Interface to test from:** `Roadmap & Projects`

**Starting tables:** `Roadmaps`, `Projects`

**Setup data:**

- Use non-sensitive sample Roadmaps and Projects.

**Steps:**

1. Confirm `Active Roadmaps` is a List and allows Add, Edit, and Delete.
2. Confirm `Active Projects` is a List and allows Add, Edit, and Delete.
3. Confirm `Project Calendar` is a Calendar and allows Edit but not Add or Delete.
4. Confirm `Project by Department` is a List grouped or filtered by Department and allows Edit but not Add or Delete.

**Expected result:**

- Roadmap & Projects replaces the old Projects interface.
- Planning pages expose only Roadmaps and Projects.
- Add/Edit/Delete behavior matches the interface requirements.

**Result:**

- [ ] Pass
- [ ] Fail

### 10. Executive Dashboard Read-Only Pages

**Purpose:** Confirm Executive Dashboard is a read-only exception view.

**Interface to test from:** `Executive Dashboard`

**Starting table:** `Tasks`

**Setup data:**

- One open Task for each Department.
- One High or Urgent open Task.
- One overdue open Task.

**Steps:**

1. Confirm `Department tasks` is a List and shows Tasks by Department.
2. Confirm `Open High Priority tasks` is a List and shows High or Urgent open Tasks.
3. Confirm `Overdue tasks` is a List and shows overdue open Tasks.
4. Confirm Add, Edit, and Delete are disabled on all three pages.

**Expected result:**

- Executive Dashboard is read-only.
- Leadership can inspect exception queues without changing records.

**Result:**

- [ ] Pass
- [ ] Fail

### 11. Submission Interfaces

**Purpose:** Confirm submission interfaces provide form intake and read-only status pages.

**Interface to test from:** `Product Request Submission`, `Creative Request Submission`, and `Bug Reporting`

**Starting tables:** `Product Requests`, `Creative Requests`, `Bugs & Issues`

**Setup data:**

- Use non-sensitive sample submissions.

**Steps:**

1. Submit a Product Request from `New Product Request`.
2. Confirm `Request Status` is read-only in Product Request Submission.
3. Submit a Creative Request from `New Creative Request`.
4. Confirm `Request Status` is read-only in Creative Request Submission.
5. Submit a bug from `Report Bugs & Issues`.
6. Confirm `Bug Status` is read-only in Bug Reporting.

**Expected result:**

- Form pages allow new submissions.
- Status pages do not allow Add, Edit, or Delete.
- Submitters cannot change triage or implementation fields from status pages.

**Result:**

- [ ] Pass
- [ ] Fail

### 12. Native Automation Checks

**Purpose:** Confirm native automations surface shared execution work without changing records automatically.

**Interface to test from:** Airtable Automations and automation source views.

**Starting tables:** `Tasks`, `Projects`, `Product Requests`, `Bugs & Issues`, `QA & Testing`, `Releases`

**Setup data:**

- One due-soon or overdue Task.
- One Blocked Task.
- One Blocked Project.
- One Product Request needing Product Dept review.
- One Critical or High Bug.
- One Failed or Blocked QA record.
- One Release in QA or Ready status.

**Steps:**

1. Open each automation source view.
2. Confirm the sample records appear in the expected views.
3. Run or wait for the relevant native automations.
4. Review notification content.
5. Confirm no automation changed approval, status, archive, or completion fields automatically.

**Expected result:**

- Review items appear in the correct source views.
- Notifications include only compact work context and record links.
- Automations do not update records automatically.
- Notifications do not include credentials, restricted HR/Finance details, banking data, payment attachments, or secure documents.

**Result:**

- [ ] Pass
- [ ] Fail

### 13. Removed Interface Check

**Purpose:** Confirm removed or externalized interfaces are not active Operations Hub interfaces.

**Interface to test from:** Airtable Interfaces list.

**Starting tables:** Not applicable.

**Setup data:**

- Use the Airtable interface list.

**Steps:**

1. Confirm `Product Triage` is not active.
2. Confirm `Bug Queue` is not active.
3. Confirm `QA Dashboard` is not active.
4. Confirm `Release Dashboard` is not active.
5. Confirm `AI & Automation Workspace` is not active.
6. Confirm `Operations Workspace` is not active.
7. Confirm `Manager Dashboard` is not active.
8. Confirm `Changelog View` is not active.
9. Confirm `Care Service Desk` is not active in the Operations Hub.
10. Confirm `Scraped Listing Review` is not active in the Operations Hub.

**Expected result:**

- Removed interface names are not active Operations Hub interfaces.
- Care Service Desk and Scraped Listing Review are handled outside this base.

**Result:**

- [ ] Pass
- [ ] Fail

### 14. Boundary Guardrails

**Purpose:** Confirm dedicated and restricted workflows stay out of the Operations Hub.

**Interface to test from:** Airtable base settings, table list, interfaces, and sample records.

**Starting tables:** All Operations Hub tables.

**Setup data:**

- Use existing non-sensitive sample records.

**Steps:**

1. Confirm no Team Members table exists.
2. Confirm no Opportunities table exists.
3. Confirm no Care, CRM, scraped listing, HR, Finance, accounting, banking, payroll, or document-storage workflow table exists.
4. Confirm no cross-base sync is enabled.
5. Search sample Tasks, Projects, dashboards, interfaces, and automations for restricted HR or Finance details.
6. Search sample Tasks, Projects, dashboards, interfaces, and automations for Care ticket, CRM, scraped listing, or Sales / Account Management pipeline details.
7. Confirm any handoff from a dedicated or restricted base is sanitized and contains only the action needed for shared execution.

**Expected result:**

- Dedicated and restricted workflows remain outside the Operations Hub.
- Shared Tasks contain only non-sensitive coordination details.
- No prohibited data appears in Operations Hub records, dashboards, interfaces, or automations.
- No cross-base synchronization exists.

**Result:**

- [ ] Pass
- [ ] Fail

## Test Summary

| Scenario | Result | Notes |
| --- | --- | --- |
| Core structure setup |  |  |
| My Tasks and shared execution |  |  |
| One-level subtasks |  |  |
| Product request to execution |  |  |
| Bug, QA, release, sprint, and changelog flow |  |  |
| Marketing Dept interface |  |  |
| AI & Automation Dept interface |  |  |
| Care Dept task interface |  |  |
| Roadmap & Projects interface |  |  |
| Executive Dashboard read-only pages |  |  |
| Submission interfaces |  |  |
| Native automation checks |  |  |
| Removed interface check |  |  |
| Boundary guardrails |  |  |
