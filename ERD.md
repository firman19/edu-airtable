# EDU Passport Airtable Architecture

# Entity Relationship Diagram (ERD)

## Operations Hub Overview

```text
                              Departments
                                   |
                                   v
Roadmaps ---------------------> Projects ----------------------> Tasks
                                   |                              ^
                                   |                              |
             +---------------------+----------------------+-------+------------------+
             |                     |                      |                          |
             v                     v                      v                          v
        Campaigns               Content                 Sprints             Creative Requests
             |
             |                         AI & Automation Register
             |                              |             |
             +------------------------------+-------------+
                                            |
                                            v
                                   Department / Project

Tasks -- Parent Task self-link --> Tasks / Subtasks

Organizations ---------> Contacts
        |                    |       |
        v                    v       v
   Care Tickets <-------- Contacts  Scraped Listing

Product Requests -------> Projects / Tasks
        |
        v
   Bugs & Issues
        |
        v
   QA & Testing
        |
        v
     Releases
        |
        v
    Changelog
```

## Base Boundaries

```text
Existing EDU Passport workspace
|
+-- EDU Passport Operations Hub
|   +-- Shared CRM, Roadmaps, Projects, Tasks
|   +-- Product, Marketing, Care, Operations, AI & Automation
|   +-- No Opportunities, Employees, HR Requests, or Finance tables
|
+-- Care & Sales Base
    +-- Customer lifecycle workflows
    +-- Opportunities and Sales / Account Management pipeline

Restricted EDU Passport Corporate Services workspace
|
+-- EDU Passport People & HR
|   +-- Employees
|   +-- HR Requests
|
+-- EDU Passport Finance & Administration
    +-- Finance Requests
    +-- Budget Plans
    +-- Budget Categories
    +-- Budget Lines
    +-- Compliance & Renewals
```

Restricted-base documentation:
- [EDU Passport People & HR](People%20%26%20HR%20Base/README.md)
- [EDU Passport Finance & Administration](Finance%20%26%20Administration%20Base/README.md)

Finance budget relationships:
- Budget Plans (1) -> Budget Lines (N)
- Budget Categories (1) -> Budget Lines (N)
- Budget Lines (1) -> Finance Requests (N, optional Budget Change requests)

There is no cross-base synchronization for the Corporate Services bases at Milestone 8 launch. Cross-boundary work uses sanitized process handoffs, not confidential record copies.

## Operations Hub Relationships

- Departments (1) -> Roadmaps (N)
- Departments (1) -> Projects (N)
- Departments (1) -> Tasks (N)
- Departments (1) -> AI & Automation Register records served (N)
- Roadmaps (1) -> Projects (N)
- Projects (1) -> Tasks (N)
- Projects (1) -> Campaigns (N)
- Projects (1) -> Content (N)
- Projects (1) -> Sprints (N)
- Projects (1) -> Creative Requests (N)
- Projects (1) -> AI & Automation Register records (N)
- Projects (1) -> Product Requests (N, optional)
- Projects (1) -> Bugs & Issues (N, optional)
- Tasks (1) -> Tasks (N, optional subtasks through Parent Task)
- Organizations (1) -> Contacts (N)
- Organizations (1) -> Care Tickets (N, optional)
- Contacts (1) -> Care Tickets (N)
- Contacts (1) -> Scraped Listing (N, optional)
- Care Tickets (1) -> Tasks (N, optional)
- Product Requests (1) -> Tasks (N, optional)
- Product Requests (N) -> Product Areas (1)
- Bugs & Issues (1) -> Tasks (N, optional)
- Bugs & Issues (1) -> QA & Testing (N)
- QA & Testing (N) -> Releases (1, optional)
- Releases (1) -> Changelog (N)

## Business Rules

1. The main operational base is EDU Passport Operations Hub.
2. One shared Tasks table is the Operations Hub execution source of truth.
3. One shared Contacts table is the Operations Hub CRM identity source of truth.
4. Every Operations Hub Task and subtask belongs to one Project.
5. Projects are the main container for initiatives.
6. Subtasks are regular Tasks linked through `Parent Task` and support one level by default.
7. Product Tasks remain filtered records inside shared Tasks.
8. Care Contacts remain records inside shared Contacts.
9. Interfaces provide workflow guardrails by role inside shared bases.
10. Operations and non-sensitive administration use shared Roadmaps, Projects, and Tasks.
11. AI & Automation is a dedicated department and uses shared Roadmaps, Projects, and Tasks.
12. The AI & Automation Register governs systems; it does not replace Tasks.
13. Opportunities and the Sales / Account Management pipeline live in the separate Care & Sales Base.
14. Employees and HR Requests live only in the restricted People & HR base.
15. Finance Requests, Budget Plans, Budget Categories, Budget Lines, and Compliance & Renewals live only in the restricted Finance & Administration base.
16. Payroll, accounting, banking, and secure document systems remain authoritative.
17. Corporate Services bases launch without cross-base synchronization.
18. Any later cross-base summary must be explicitly approved, one-way, non-sensitive, and field-allowlisted.
19. Finance budget reporting uses USD monthly Department x Budget Category records.
20. Quarterly, annual, and YTD values are derived from monthly Budget Lines rather than entered separately.
21. Actual Spend is summarized and reconciled monthly from the authoritative accounting system; transaction-level accounting data remains outside Airtable.
22. Department leads may view approved company-wide budgets and edit their own planning/forecast fields; Finance controls approvals, adjustments, commitments, actuals, reconciliation, and locking.

## Operations Hub Tables

- Departments
- Organizations
- Contacts
- Roadmaps
- Projects
- Tasks
- Product Requests
- Product Areas
- Bugs & Issues
- QA & Testing
- Releases
- Changelog
- Care Tickets
- Scraped Listing
- Campaigns
- Content
- Sprints
- Creative Requests
- AI & Automation Register

Documentation:
- [Cross-base Milestone 8 requirements](company-functions-requirements.md)
- [People & HR Base schema and tests](People%20%26%20HR%20Base/README.md)
- [Finance & Administration Base schema and tests](Finance%20%26%20Administration%20Base/README.md)
