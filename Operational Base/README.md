# EDU Passport Operations Hub

## Purpose

Build the main company-wide Airtable hub for shared CRM, roadmaps, project management, task management, Product, Marketing, Care, Operations, AI & Automation, and cross-department reporting.

## Base Strategy

- Main shared base: `EDU Passport Operations Hub`.
- Sales and Account Management pipeline: implemented in the separate `Care & Sales Base`; do not create duplicate Opportunities in the Operations Hub.
- Restricted workspace: `EDU Passport Corporate Services`.
- Restricted workflow bases: [EDU Passport People & HR](../People%20%26%20HR%20Base/README.md) and [EDU Passport Finance & Administration](../Finance%20%26%20Administration%20Base/README.md).
- Non-sensitive administration stays under Operations in the Operations Hub.
- Payroll, accounting, banking, and secure document systems remain authoritative.

## Current Status

- Shared foundation and department workflows: Complete
- Interfaces and access guardrails: Complete
- Native automations: Complete
- Validation and reporting: Complete
- Sales / Account Management pipeline: Complete in Care & Sales Base
- Corporate functions, Operations, and AI & Automation: Current
- Future integrations: Planned

## Resume Context

Current Phase: Milestone 8 - Corporate Functions, Operations, And AI & Automation

Next:
- Confirm the Operations department and non-sensitive administration routing.
- Create the dedicated AI & Automation department, roadmap, interface, and register in the Operations Hub.
- Create the restricted Corporate Services workspace.
- Create the [People & HR](../People%20%26%20HR%20Base/README.md) and [Finance & Administration](../Finance%20%26%20Administration%20Base/README.md) bases.
- Configure base-specific or interface-only access and test sensitive-data boundaries.
- Launch without cross-base synchronization.

Constraints:
- One shared Tasks table remains the execution source of truth inside the Operations Hub.
- Every Operations Hub Task belongs to one Project.
- Paid Airtable features are acceptable when they improve interface and permission design.
- Prefer native automations first.
- Use interface guardrails inside shared bases and separate restricted bases when confidentiality requires data isolation.
- Do not store credentials, authoritative payroll/accounting records, or unrestricted sensitive documents in Airtable.

Portfolio Read Order:
1. [Repository README](../README.md)
2. [Architecture](../architecture.md)
3. [ERD](../ERD.md)
4. [Implementation](../implementation.md)
5. [Milestones](../milestones.md)
6. [Milestone 8 Corporate Functions Requirements](../company-functions-requirements.md)

Operations Hub Build Docs:
1. [Field Requirements](field-requirements.md)
2. [Product Field Requirements](product-field-requirements.md)
3. [Care Field Requirements](care-field-requirements.md)
4. [Interface Requirements](interface-requirements.md)
