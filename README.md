# EDU Airtable Documentation

This repository documents the Airtable operating architecture for EDU Passport.

## Bases

- [Operational Base](Operational%20Base/README.md): main company operations hub for shared CRM, roadmaps, projects, tasks, Product, Marketing, Care, Operations, AI & Automation, and management reporting.
- [Care & Sales Base](Care%20%26%20Sales%20Base/README.md): customer lifecycle base for Care, Growth, Sales, Account Management, Opportunities, and sales handoffs.
- [People & HR Base](People%20%26%20HR%20Base/README.md): restricted employee-lifecycle and confidential HR workflow base.
- [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md): restricted finance-request, company-wide USD budget planning/actuals, contract, registration, and compliance workflow base.

## Portfolio Docs

- [Architecture](architecture.md): full Airtable base portfolio and operating model.
- [ERD](ERD.md): cross-base boundaries and Operations Hub relationships.
- [Decisions](decisions.md): durable architecture and implementation decisions.
- [Implementation](implementation.md): phased implementation status.
- [Milestones](milestones.md): milestone checklist and current phase.
- [Milestone 8 Corporate Functions Requirements](company-functions-requirements.md): Operations, AI & Automation, HR, and Finance routing.
- [Changelog](CHANGELOG.md): documentation and architecture changes.

## Read Order

1. [AGENTS.md](AGENTS.md)
2. [Architecture](architecture.md)
3. [ERD](ERD.md)
4. [Implementation](implementation.md)
5. [Milestones](milestones.md)
6. [Milestone 8 Corporate Functions Requirements](company-functions-requirements.md)
7. [Operational Base](Operational%20Base/README.md)
8. [Care & Sales Base](Care%20%26%20Sales%20Base/README.md)
9. [People & HR Base](People%20%26%20HR%20Base/README.md)
10. [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md)

## Workspace Model

- Existing EDU Passport workspace: shared operational and customer-lifecycle bases.
- `EDU Passport Corporate Services` workspace: restricted People & HR and Finance & Administration bases with base-specific or interface-only access.
- Payroll, accounting, banking, and secure document systems remain authoritative for sensitive records and transactions.

## Source Materials

The `docs/` folder contains original source materials and blueprints used to design the Airtable structures.

## AI Working Instructions

`AGENTS.md` contains the working instructions for AI assistants collaborating on this documentation.
