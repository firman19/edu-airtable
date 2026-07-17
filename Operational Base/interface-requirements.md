# Interface Requirements

# Operations Hub Interface Model

Goal: Make Airtable usable through focused role-specific interfaces instead of asking staff to work in raw tables.

This document is the source of truth for Operations Hub interfaces, pages, visualizations, page filters, and page-level Add/Edit/Delete guardrails.

## Interface Principles

- Staff should work from department or role-specific interfaces.
- One shared `Tasks` table remains the execution source of truth.
- Every Task must belong to one Project.
- Interface page permissions are Airtable interface guardrails, not schema fields.
- Department task interfaces may create and edit Tasks only from project-filtered pipeline pages.
- Read-only status pages should disable Add, Edit, and Delete.
- Care Dept inside the Operations Hub is task-only.
- Care tickets, scraped listings, CRM context, Opportunities, and Sales / Account Management pipeline belong in the separate Care & Sales Base.
- HR and Finance restricted workflows belong in the restricted Corporate Services bases.

## Active Interfaces

| Interface | Primary Users | Main Tables | Purpose |
| --- | --- | --- | --- |
| Executive Dashboard | Leadership and managers | Tasks | Read-only operating exception view. |
| My Tasks | All staff | Tasks | Personal task management. |
| Marketing Dept | Marketing | Tasks, Campaigns, Creative Requests | Marketing execution and campaign visibility. |
| AI & Automation Dept | AI & Automation | Tasks | AI and automation department execution. |
| Product Dept | Product | Tasks, Bugs & Issues, QA & Testing, Releases, Product Requests, Sprints, Changelog | Product execution and delivery workflow. |
| Care Dept | Care | Tasks | Care department task execution only. |
| Product Request Submission | All teams | Product Requests | Product request intake and status visibility. |
| Creative Request Submission | All teams | Creative Requests | Creative request intake and status visibility. |
| Bug Reporting | All teams | Bugs & Issues | Bug intake and status visibility. |
| Releases | All teams | Releases | Read-only release schedule visibility. |
| Roadmap & Projects | Leads and project owners | Roadmaps, Projects | Roadmap and project planning. |

## Externalized Interfaces

These are not active Operations Hub interfaces:

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

Care Service Desk and Scraped Listing Review belong in the Care & Sales Base. Product workflow work is consolidated into Product Dept, Product Request Submission, Bug Reporting, Releases, and Roadmap & Projects.

## Interface Builder Map

Use this section when Airtable asks you to add a page, choose a layout, then choose a source table.

### Executive Dashboard

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| Department tasks | Tasks | List | Group or filter by Department; hide Done and Archived by default. | No | No | No |
| Open High Priority tasks | Tasks | List | Priority is High or Urgent; Status is not Done or Archived. | No | No | No |
| Overdue tasks | Tasks | List | Due Date is before today; Status is not Done or Archived. | No | No | No |

### My Tasks

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| All tasks | Tasks | Calendar, List | Owner is current Airtable user where possible. | Yes | Yes | Yes |
| Due this week | Tasks | Calendar, List | Owner is current Airtable user where possible; Due Date is this week; Status is not Done or Archived. | No | Yes | Yes |
| Open tasks | Tasks | Calendar, List | Owner is current Airtable user where possible; Status is not Done or Archived. | No | Yes | Yes |
| Overdue | Tasks | Calendar, List | Owner is current Airtable user where possible; Due Date is before today; Status is not Done or Archived. | No | Yes | Yes |

### Marketing Dept

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| All tasks | Tasks | List | Department is Marketing. | No | Yes | Yes |
| Campaign Calendar | Campaigns | List, Calendar | All Campaigns. | Yes | Yes | Yes |
| Ops Pipeline | Tasks | Kanban, Calendar, List | Project is Marketing Operations. | Yes | Yes | Yes |
| Content Pipeline | Tasks | Kanban, Calendar, List | Department is Marketing; Project is not EDU Blogs and not Marketing Operations. | Yes | Yes | Yes |
| Blog Pipeline | Tasks | Kanban, Calendar, List | Project is EDU Blogs. | Yes | Yes | Yes |
| Creative Request Pipeline | Creative Requests | List, Kanban | Active Creative Requests. | No | Yes | No |

### AI & Automation Dept

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| All tasks | Tasks | List | Department is AI & Automation. | No | Yes | No |
| Ops Pipeline | Tasks | Kanban, Calendar, List | Project is AI & Automation Ops. | Yes | Yes | Yes |
| SM Posting Pipeline | Tasks | Kanban, Calendar, List | Project is SM Posting. | Yes | Yes | Yes |
| Internal Report Pipeline | Tasks | Kanban, Calendar, List | Project is Internal Report. | Yes | Yes | Yes |

### Product Dept

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| All tasks | Tasks | List | Department is Product. | No | Yes | No |
| Bugs | Bugs & Issues, Tasks | List, Kanban | Bugs and linked Tasks. | Not specified | Not specified | Not specified |
| QA & Testing | QA & Testing | List, Kanban | Active QA records. | Yes | Yes | Yes |
| Ops Pipeline | Releases | Kanban | Active Releases. | Yes | Yes | Yes |
| Release Pipeline | Releases | Kanban, Calendar | Active and scheduled Releases. | Yes | Yes | Yes |
| Product Request Pipeline | Product Requests | List, Kanban | Active Product Requests. | No | Yes | No |
| Sprint | Sprints | List, Calendar | Active Sprints. | Yes | Yes | Yes |
| Changelog | Changelog | List | All Changelog records. | Yes | Yes | Yes |

### Care Dept

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| All tasks | Tasks | List | Department is Care. | No | Yes | No |
| Ops Pipeline | Tasks | Kanban, Calendar, List | Project is Care Operations. | Yes | Yes | Yes |
| EDU Academy Pipeline | Tasks | Kanban, Calendar, List | Project is EDU Academy. | Yes | Yes | Yes |

### Product Request Submission

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| New Product Request | Product Requests | Form | New submissions only. | Yes | No | No |
| Request Status | Product Requests | List, Kanban | Submitted requests and status views. | No | No | No |

### Creative Request Submission

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| New Creative Request | Creative Requests | Form | New submissions only. | Yes | No | No |
| Request Status | Creative Requests | List, Kanban | Submitted requests and status views. | No | No | No |

### Bug Reporting

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| Report Bugs & Issues | Bugs & Issues | Form | New submissions only. | Yes | No | No |
| Bug Status | Bugs & Issues | List, Kanban | Submitted bugs and status views. | No | No | No |

### Releases

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| Release Schedule | Releases | Kanban, Calendar | Active and scheduled Releases. | No | No | No |

### Roadmap & Projects

| Page | Source Table | Visualization | Filter | Add | Edit | Delete |
| --- | --- | --- | --- | --- | --- | --- |
| Active Roadmaps | Roadmaps | List | Status is not Archived. | Yes | Yes | Yes |
| Active Projects | Projects | List | Status is not Archived. | Yes | Yes | Yes |
| Project Calendar | Projects | Calendar | Status is not Archived; calendar by Due Date or project date field. | No | Yes | No |
| Project by Department | Projects | List | Group by Department; Status is not Archived. | No | Yes | No |

## Page Guardrails

### Task Pages

- Task creation is enabled only on pages where Add is Yes.
- New Tasks created from department pipeline pages must link to the filtered Project.
- Task records should show `Task Name`, `Project`, `Department`, `Owner`, `Status`, `Priority`, `Start Date`, `Due Date`, `Task Level`, `Parent Task`, `Description`, and relevant department links.
- Subtasks stay in shared `Tasks`; use `Parent Task` for one-level nesting and avoid separate subtask tables.
- Every subtask must still link to one Project.

### Request Submission Pages

- Form pages create records.
- Status pages are read-only.
- Request submitters should not edit triage, owner, priority, decision, release, or implementation fields unless separately authorized.

### Department Pages

- `All tasks` pages are department-wide review pages. They allow editing but do not allow adding records.
- Pipeline pages are project-specific work queues and may allow Add, Edit, and Delete when requested.
- Product Dept consolidates product triage, bugs, QA, releases, sprints, product requests, and changelog into one department interface.
- Care Dept is limited to shared Tasks for Care department execution.

### Boundary Rules

- Do not create a Product Tasks table.
- Do not create a Marketing Tasks table.
- Do not create a Care Tickets page in the Operations Hub.
- Do not create Scraped Listing, Contacts, Organizations, Opportunities, Sales, or Account Management pages in the Operations Hub.
- Do not expose HR or Finance restricted records in Operations Hub interfaces.

## Completion Checklist

- [ ] Executive Dashboard has Department tasks, Open High Priority tasks, and Overdue tasks as read-only list pages.
- [ ] My Tasks has All tasks, Due this week, Open tasks, and Overdue pages with requested Add/Edit/Delete settings.
- [ ] Marketing Interface is replaced by Marketing Dept.
- [ ] AI & Automation Workspace is replaced by AI & Automation Dept.
- [ ] Engineering / Product Task Board is replaced by Product Dept.
- [ ] Care Dept exists and contains only task pages.
- [ ] Product Request Submission remains available with New Product Request and read-only Request Status.
- [ ] Creative Request Submission exists.
- [ ] Bug Reporting exists.
- [ ] Releases exists with read-only Release Schedule.
- [ ] Roadmap & Projects replaces the old Projects interface.
- [ ] Removed interfaces are not used as active Operations Hub interfaces.
- [ ] Care Service Desk and Scraped Listing Review are kept outside the Operational Base interface model.
- [ ] Every task-creation page still requires a Project.
- [ ] No duplicate Product Tasks, Marketing Tasks, Opportunities, Care, CRM, HR, or Finance workflow tables are introduced.
