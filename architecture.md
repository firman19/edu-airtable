# Architecture

## Base Portfolio

### Main Shared Base

`EDU Passport Operations Hub` is the main company-wide base for shared CRM, roadmaps, projects, tasks, Product, Marketing, Care, Operations, AI & Automation, and management reporting.

### Customer Lifecycle Base

`Care & Sales Base` owns Care/Growth/Sales customer lifecycle workflows, Opportunities, and Sales / Account Management handoffs. Do not create a duplicate Opportunities table in the Operations Hub.

### Restricted Corporate Services Workspace

`EDU Passport Corporate Services` contains two restricted workflow bases:

- [EDU Passport People & HR](People%20%26%20HR%20Base/README.md)
- [EDU Passport Finance & Administration](Finance%20%26%20Administration%20Base/README.md)

These bases are separate because employee, payroll, budget, contract, payment, and financial records require stronger visibility boundaries than role-specific editing rules inside a shared base.

## Operations Hub Operating Model

`Roadmaps -> Projects -> Tasks` remains the shared planning and execution spine.

```text
Roadmaps -> Projects -> Tasks
Tasks -> Subtasks through a self-link in Tasks
CRM records -> Requests / Tickets -> Projects / Tasks
Product Requests -> Projects / Tasks -> Bugs / QA -> Releases -> Changelog
Care Tickets -> Contacts / Organizations -> Tasks
Scraped Listing -> Contacts
AI & Automation Register -> Departments / Projects -> monitoring and review
```

## Shared Foundation Tables
- Departments
- Organizations
- Contacts
- Roadmaps
- Projects
- Tasks

## Product Tables
- Product Requests
- Product Areas
- Bugs & Issues
- QA & Testing
- Releases
- Changelog

## Care Tables
- Care Tickets
- Scraped Listing

## Department Workflow Tables
- Campaigns
- Content
- Sprints
- Creative Requests
- AI & Automation Register

## Tables Not Added To The Operations Hub
- Team Members
- Opportunities
- Employees
- HR Requests
- Finance Requests
- Budget Plans
- Budget Categories
- Budget Lines
- Compliance & Renewals

The Operations Hub continues using Airtable collaborator fields for owners and assignees. The HR-specific Employees table exists only inside the restricted People & HR base. Opportunities exists only inside the Care & Sales Base.

## Corporate Services Tables

People & HR:
- Employees
- HR Requests

Finance & Administration:
- Finance Requests
- Budget Plans
- Budget Categories
- Budget Lines
- Compliance & Renewals

Payroll, accounting, banking, and secure document systems remain authoritative. The Finance base stores USD plans and summarized monthly reconciled actuals, plus workflow state, approved metadata, references, and secure links rather than transaction-level records, credentials, or unrestricted sensitive documents.

## Cross-Base Rule

Milestone 8 launches without cross-base synchronization. A later sync requires explicit approval and must be one-way, non-sensitive, and field-allowlisted. Sensitive HR cases, employee compensation, medical or performance information, bank details, payment attachments, confidential notes, and detailed transactions must not sync into the Operations Hub.

## CRM Foundation

Organizations stores schools, businesses, vendors, partners, and other institutions.
Contacts stores individual people.
The Operations Hub uses `Care Tickets.Upsell Potential` and `Scraped Listing` to capture customer signals. Qualified Sales and Account Management pipeline work is handed to Opportunities in the separate Care & Sales Base.

## Business Rules
- One shared Tasks table is used for execution work inside the Operations Hub.
- Subtasks are records in the shared Tasks table, linked through `Parent Task`.
- One shared Contacts table is used for CRM identity inside the Operations Hub.
- Every Task and subtask belongs to one Project.
- Projects are the main container for initiatives.
- Support only one subtask level by default.
- Product work uses shared Tasks, not a Product Tasks table.
- Care uses shared Contacts, not a Care Contacts table.
- Marketing uses Campaigns and Content.
- Product uses Sprints, Product Requests, Bugs, QA, Releases, and Changelog.
- Care uses Care Tickets and Scraped Listing.
- Operations and non-sensitive administration use shared Roadmaps, Projects, and Tasks.
- AI & Automation is a dedicated department but still uses shared Roadmaps, Projects, and Tasks.
- The AI & Automation Register governs live AI use cases, automations, and integrations; it does not replace Tasks.
- Use Airtable collaborator/user fields directly for Operations Hub owners and assignees.
- Interfaces guide department access and editing behavior inside shared bases.
- Separate restricted bases provide HR and Finance visibility boundaries.
- Finance budgets use one monthly record per Department x Budget Category; quarterly, annual, and YTD totals are derived.
- USD is the Finance budget reporting currency for Milestone 8.
- Finance reconciles summarized monthly actuals from the authoritative accounting system.
- All department leads may view approved company-wide budget comparisons; Finance controls approvals, adjustments, commitments, actuals, reconciliation, and locking.
- Marketing owns only marketing-specific AI work that it builds and maintains; centrally delivered or maintained work belongs to AI & Automation.
