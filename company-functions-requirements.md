# Milestone 8 Corporate Functions Requirements

Use this cross-base checklist to route company administration, HR, Finance, Operations, and AI & Automation without weakening the shared Operations Hub or exposing sensitive records.

Detailed restricted-base specifications:
- [EDU Passport People & HR](People%20%26%20HR%20Base/README.md)
- [EDU Passport Finance & Administration](Finance%20%26%20Administration%20Base/README.md)

## Target Base And Workspace Model

| Workspace / Base | Purpose | Access Boundary |
| --- | --- | --- |
| Existing EDU Passport workspace / `EDU Passport Operations Hub` | Shared roadmaps, projects, tasks, non-sensitive administration, Operations, and AI & Automation delivery. | Existing company collaboration and role-specific interfaces. |
| Existing EDU Passport workspace / `Care & Sales Base` | Customer lifecycle, Opportunities, and Sales / Account Management pipeline. | Care, Growth, Sales, and Account Management workflows. |
| `EDU Passport Corporate Services` workspace / [People & HR Base](People%20%26%20HR%20Base/README.md) | Employee lifecycle and confidential HR workflows. | Restricted base-level or interface-only access. |
| `EDU Passport Corporate Services` workspace / [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md) | Financial requests, company-wide USD budget planning and monthly actuals, contracts, registrations, and compliance. | Restricted base-level or interface-only access. |

Do not create separate Operations or AI & Automation bases. Do not add HR or Finance tables to the Operations Hub. Do not give general company staff workspace-level access to Corporate Services.

## Work Routing

| Work Type | Destination | Operating Rule |
| --- | --- | --- |
| Office administration, vendor coordination, equipment, facilities, and non-sensitive recurring operations | Operations Hub | Use `Department = Operations`, shared Projects, and shared Tasks. |
| Employee onboarding, offboarding, leave, recruitment, documents, or confidential people cases | [People & HR Base](People%20%26%20HR%20Base/README.md) | Keep employee identity and case details inside the restricted base. |
| Purchases, expenses, reimbursements, invoices, payments, budgets, contracts, registrations, insurance, or statutory renewals | [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md) | Keep amounts, approvals, attachments, and compliance details inside the restricted base. |
| Company-wide AI, automation, and integration delivery | Operations Hub | Use `Department = AI & Automation`, shared Projects and Tasks, plus the AI & Automation Register. |
| Marketing-specific AI work maintained entirely by Marketing | Operations Hub | Keep it under Marketing. If AI & Automation builds or maintains it, AI & Automation owns the project and Marketing is the department served. |
| Qualified Sales or Account Management work | Care & Sales Base | Use Opportunities in the existing Care & Sales Base; do not create Opportunities in the Operations Hub. |

Cross-boundary coordination uses sanitized Tasks or manual handoffs. Do not copy employee cases, compensation, bank data, payment attachments, confidential notes, or restricted documents into the Operations Hub.

## Operations Hub Adjustments

### Operations

- Confirm one active `Operations` record in `Departments`.
- Continue using `Roadmaps -> Projects -> Tasks`; every operational Task requires one Project.
- Use purpose-specific or annual operational Projects rather than a permanent miscellaneous project.
- Create an `Operations Workspace` showing active projects, recurring work, approvals, renewals, blockers, and overdue Tasks.
- Keep `Creative Requests` limited to creative-service intake.

### AI & Automation

Create an active `AI & Automation` Department with a department lead, roadmap, Projects, shared Tasks, and an `AI & Automation Workspace`.

Add one Operations Hub workflow table: `AI & Automation Register`.

| Field | Type | Requirement |
| --- | --- | --- |
| Name | Single line text | Required primary field. |
| Type | Single select | Required: AI Use Case, Automation, Integration. |
| Lifecycle Status | Single select | Required: Idea, Assessing, Approved, Building, Testing, Live, Paused, Retired. |
| Technical Owner | Collaborator / Airtable user | Required after approval. |
| Business Owner | Collaborator / Airtable user | Required after approval. |
| Department Served | Linked record to Departments | Required after assessment. |
| Related Project | Linked record to Projects | Required after approval. |
| Systems Involved | Long text | Required before building; never store credentials. |
| Data Classification | Single select | Required: Public, Internal, Confidential, Restricted. |
| Human Review Required | Checkbox | Required decision before testing. |
| Monitoring Status | Single select | Required for live records: Not Required, Not Configured, Healthy, Warning, Failed. |
| Last Review Date | Date | Required for live records. |
| Runbook URL | URL | Required before a production record becomes Live. |

The register governs deployed systems and does not replace Projects or Tasks.

## Shared Access And Data Rules

- Keep Corporate Services workspace owners to the minimum designated leadership or system administrators.
- Use base-specific access for HR and Finance staff and interface-only access for ordinary requesters where supported.
- Disable public sharing and unrestricted invite links for both restricted bases.
- Keep payroll, HRIS, accounting, banking, tax, and secure document systems authoritative.
- Never store passwords, API keys, banking credentials, full card data, or unrestricted identity documents in Airtable.
- Launch both restricted bases without cross-base synchronization.
- A later sync requires explicit approval and must be one-way, non-sensitive, and field-allowlisted.

## Cross-Base Validation

1. Confirm every Airtable base listed in the root README has a dedicated repository folder.
2. Create a non-sensitive administration Task and confirm it belongs to an Operations Project.
3. Confirm Operations and AI & Automation use shared Projects and Tasks.
4. Confirm the People & HR and Finance & Administration negative-access tests pass.
5. Confirm Finance monthly Budget Lines derive quarterly, annual, and YTD reporting and reconcile summarized accounting actuals.
6. Confirm no confidential HR or Finance information appears in Operations Hub tables, interfaces, dashboards, or automations.
7. Confirm no additional Operations, AI & Automation, or Opportunities base is proposed.
8. Confirm no Corporate Services cross-base synchronization exists at launch.
9. Confirm existing Product, Care, Marketing, Contacts, Tasks, and Care & Sales workflows remain unchanged.

## Completion Checklist

- [ ] Operations department and interface are configured in the Operations Hub.
- [ ] AI & Automation department, roadmap, Projects, interface, and register are configured in the Operations Hub.
- [ ] Corporate Services workspace is configured with the two restricted bases.
- [ ] [People & HR Base](People%20%26%20HR%20Base/README.md) completion checklist passes.
- [ ] [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md) completion checklist passes.
- [ ] Authoritative external systems and prohibited Airtable data are documented.
- [ ] Cross-base routing and negative-access scenarios pass.
- [ ] No Corporate Services cross-base synchronization is enabled.
