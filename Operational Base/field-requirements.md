# Field Requirements

# Milestone 1 Target Schema Checklist

Use this document to compare your current Airtable fields against the target structure for Milestone 1.

For each field, mark one audit result:
- `Present`
- `Missing`
- `Rename`
- `Change Type`
- `Remove / Later`

## Audit Rules

- Keep the schema simple.
- Do not create separate Product Tasks or Care Contacts tables.
- Prefer linked records over duplicate text fields when the data already belongs to another table.
- Required fields should be enforced by Airtable field settings, interface forms, or process rules.
- Add optional fields only when they support current workflows.
- Use Airtable collaborator/user fields directly for owners and assignees.
- Defer a Team Members table unless staff metadata, manager hierarchy, non-Airtable users, capacity planning, or historical staff records become necessary.
- You listed `Related Content` twice on Tasks; keep one field only.

## Current Airtable Field Snapshot

These are the latest fields provided for the existing foundation tables.

Departments:
- Department Name
- Department Lead
- Status
- Description
- Projects
- Tasks
- Roadmaps
- Team Member

Roadmaps:
- Roadmap Name
- Owner
- Status
- Year
- Quarter
- Department
- Start Date
- End Date
- Related Projects
- Goals
- Description

Projects:
- Project Name
- Department
- Roadmap
- Owner
- Status
- Priority
- Start Date
- Due Date
- Description
- Related Tasks
- Related Campaigns
- Related Contents
- Sprint
- Creative Requests

Tasks:
- Task Name
- Project
- Department
- Owner
- Status
- Priority
- Start Date
- Due Date
- Description
- Attachments
- Related Campaign
- Related Content
- Related Creative Request
- Milestone
- Sprint
- Related Account (current name; recommended rename to Related Organization)
- Related Contact
- Created By
- Created
- Last Update

## Departments

Purpose: Stores the company departments used to classify roadmaps, projects, tasks, and reporting.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Department Name | Single line text | Yes | Primary field. Examples: Marketing, Sales, Product, Care, Operations, Leadership. | Present |
| Department Lead | Collaborator / Airtable user | No | Person accountable for the department. | Present |
| Status | Single select | Yes | Options: Active, Inactive. | Present |
| Description | Long text | No | Short explanation of department scope. | Present |
| Projects | Linked records to Projects | Auto/backlink | Backlink from Projects. | Present |
| Tasks | Linked records to Tasks | Auto/backlink | Backlink from Tasks. | Present |
| Roadmaps | Linked records to Roadmaps | Auto/backlink | Backlink from Roadmaps. | Present |
| Team Member | Collaborator / Airtable user | No | Filled with Airtable users for department membership/reference. This is a field, not a Team Members table. | Present |

## Roadmaps

Purpose: Stores strategic themes or time-bound plans that group projects.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Roadmap Name | Single line text | Yes | Primary field. | Present |
| Owner | Collaborator / Airtable user | Yes | Accountable owner. | Present |
| Status | Single select | Yes | Options: Planned, Active, Paused, Complete, Archived. | Present |
| Year | Number or single select | Yes | Planning year. | Present |
| Quarter | Single select | No | Options: Q1, Q2, Q3, Q4, H1, H2, Full Year. | Present |
| Department | Linked record to Departments | Yes | Department responsible for the roadmap. | Present |
| Start Date | Date | No | Optional planning date. | Present |
| End Date | Date | No | Optional planning date. | Present |
| Related Projects | Linked records to Projects | Auto/backlink | Backlink from Projects. | Present |
| Goals | Long text | No | Strategic goals or outcomes for the roadmap. | Present |
| Description | Long text | No | Strategic context. | Present |

## Projects

Purpose: Central planning container. Every task belongs to one project.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Project Name | Single line text | Yes | Primary field. | Present |
| Department | Linked record to Departments | Yes | Department responsible for the project. | Present |
| Roadmap | Linked record to Roadmaps | Yes | Strategic parent. | Present |
| Owner | Collaborator / Airtable user | Yes | Project owner. | Present |
| Status | Single select | Yes | Options: Not Started, In Progress, Blocked, Done, Archived. | Present |
| Priority | Single select | Yes | Options: Urgent, High, Medium, Low. | Present |
| Start Date | Date | No | Optional. | Present |
| Due Date | Date | No | Target completion date. | Present |
| Description | Long text | No | Scope and expected outcome. | Present |
| Related Tasks | Linked records to Tasks | Auto/backlink | Backlink from Tasks. | Present |
| Related Campaigns | Linked records to Campaigns | Auto/backlink | Existing Marketing workflow. | Present |
| Related Contents | Linked records to Content | Auto/backlink | Existing Marketing workflow. | Present |
| Sprint | Linked record to Sprints | No | Existing Product/Tech workflow. Consider renaming to `Related Sprints` if multiple sprints can link to one project. | Present |
| Creative Requests | Linked records to Creative Requests | Auto/backlink | Existing Operations workflow. | Present |

## Tasks

Purpose: One shared execution table for all departments.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Task Name | Single line text | Yes | Primary field. | Present |
| Project | Linked record to Projects | Yes | Required. No orphan tasks. | Present |
| Department | Linked record to Departments or lookup from Project | Yes | Use a direct link if teams need filtering/editing; use lookup if it should always follow Project. | Present |
| Owner | Collaborator / Airtable user | Yes | Direct assignee/owner used for My Tasks and ownership reporting. | Present |
| Status | Single select | Yes | Options: To Do, In Progress, Blocked, Ready for Review, Done, Archived. | Present |
| Priority | Single select | Yes | Options: Urgent, High, Medium, Low. | Present |
| Start Date | Date | No | Useful for planning. | Present |
| Due Date | Date | No | Needed for My Tasks and reminders. | Present |
| Description | Long text | No | Task details. | Present |
| Attachments | Attachment | No | Supporting files, screenshots, briefs, or references. | Present |
| Related Campaign | Linked record to Campaigns | No | Marketing context. | Present |
| Related Content | Linked record to Content | No | Marketing/content context. Keep one field only. | Present |
| Related Creative Request | Linked record to Creative Requests | No | Operations/creative context. | Present |
| Milestone | Single select or linked record | No | Use for project milestone grouping if needed. Do not confuse with the documentation milestone file. | Present |
| Sprint | Linked record to Sprints | No | Product/tech sprint context. | Present |
| Related Organization | Linked record to Organizations | No | CRM organization context. Rename current `Related Account` field to this. | Rename |
| Created By | Created by | No | Audit field. | Present |
| Created | Created time | No | Audit field. | Present |
| Last Update | Last modified time | No | Audit field. | Present |
| Related Contact | Linked record to Contacts | No | Person-level CRM context. | Present |
| Parent Task | Linked record to Tasks | No | Self-link for one-level subtasks. Limit to one linked parent task. | Missing |
| Subtasks | Linked records to Tasks | Auto/backlink | Reciprocal field from `Parent Task`; shows child tasks under a parent task. | Missing |
| Task Level | Formula | No | Formula: `IF({Parent Task}, "Subtask", "Task")`. Use for grouping/filtering. | Missing |
| Task Complete Flag | Formula | No | Formula: `IF({Status} = "Done", 1, 0)`. Used by parent task progress rollups. | Missing |
| Subtask Count | Count | No | Count linked records in `Subtasks`. | Missing |
| Completed Subtask Count | Rollup | No | Roll up `Subtasks -> Task Complete Flag` with `SUM(values)`. | Missing |
| Subtask Progress | Formula | No | Formula: `IF({Subtask Count} = 0, BLANK(), {Completed Subtask Count} / {Subtask Count})`; format as percent. | Missing |
| Blocker Reason | Long text | No | Not needed. Use `Description` for blocker notes when needed. | Remove / Later |

Subtask rules:
- Subtasks are normal records in `Tasks`, not a separate table.
- Every subtask must still have a `Project`.
- Use `Parent Task` only for one level of nesting: task -> subtask.
- A subtask may have its own `Owner`, `Status`, `Priority`, `Start Date`, and `Due Date`.
- Keep tiny checklist items inside `Description`; create subtasks only when separate ownership, dates, status, or reporting are needed.

## Organizations

Purpose: Shared CRM table for organizations such as schools, businesses, vendors, partners, and other institutions.

Function:
- Groups multiple Contacts under one organization.
- Connects Sales/Account Management opportunities to the organization.
- Lets Care and Product see organization-level context instead of only individual people.
- Supports reporting by school, business, vendor, partner, or key account.
- Prevents duplicate organization names being scattered across Tasks, Tickets, Product Requests, and future opportunity records.

Example:
- `Organization`: Bright Future School
- `Contacts`: principal, teacher, admin staff
- `Care Tickets`: onboarding issue from the school admin
- `Tasks`: follow-up tasks for Care or Sales

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Organization Name | Single line text | Yes | Primary field. | Present |
| Organization Type | Single select | Yes | Options: School, Business, Vendor, Partner, Other. | Present |
| Status | Single select | Yes | Options: Lead, Active, Inactive, Churned, Partner. | Present |
| Owner | Collaborator / Airtable user | No | Sales/AM or relationship owner. | Present |
| Website | URL | No | Organization website. | Present |
| Main Email | Email | No | General contact email. | Present |
| Main Phone | Phone number | No | General phone. | Present |
| Notes | Long text | No | Relationship context. | Present |
| Contacts | Linked records to Contacts | Auto/backlink | Backlink from Contacts. | Present |
| Projects | Linked records to Projects | No | Optional if organization-specific projects are needed. | Present |

## Contacts

Purpose: Shared CRM identity table for people across Care, Product, Sales, and Growth.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Full Name | Single line text | Yes | Primary field. | Present |
| Email | Email | Yes | Main matching key when available. | Present |
| Organization | Linked record to Organizations | No | Organization relationship. | Present |
| User Type | Single select | Yes | Options: Educator, Business, Vendor, Admin, Other. | Present |
| Platform Status | Single select | Yes | Options: Active User, Inactive, Non-User Lead, Suspended, Deleted. | Present |
| Phone / WhatsApp | Phone number | No | Care/Growth outreach. | Present |
| WeChat ID | Single line text | No | Care/Growth outreach. | Present |
| Contact Owner | Collaborator / Airtable user | No | Sales/AM/Care owner if applicable. | Present |
| Source | Single select | No | Options: Platform, Manual, Scraped, Import, Referral. | Present |
| Notes | Long text | No | Relationship/support context. | Present |
| Care Tickets | Linked records to Care Tickets | Later/backlink | Add in Milestone 3. | Present |

## Deferred: Opportunities

Purpose: Later Sales/Account Management pipeline for sales, upsell, account management, triggered lead, and revenue opportunities.

Do not create this table in Milestone 1. Use Care Tickets.Upsell Potential and Scraped Listing for now.

## Milestone 1 Completion Checklist

- [x] All six Milestone 1 tables exist or are intentionally deferred.
- [x] Required fields are present or marked for creation.
- [x] Field types match the target schema or have a documented reason to differ.
- [x] `Tasks` links to `Projects`.
- [x] `Projects` links to `Roadmaps`.
- [x] `Projects` links to `Departments`.
- [x] `Roadmaps` links to `Departments`.
- [x] `Contacts` links to `Organizations`.
- [x] No duplicate Product Tasks table is created.
- [x] No duplicate Care Contacts table is created.
- [x] Owner/assignee fields use Airtable collaborator/user fields directly.
- [x] Team Members table is not created for Milestone 1.
- [x] Opportunities table is not created for Milestone 1.
- [ ] Tasks support one-level subtasks through `Parent Task` and `Subtasks`.
