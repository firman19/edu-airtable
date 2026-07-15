# Implementation

## Phase 1
Shared Foundation
- Departments [done]
- Roadmaps [done]
- Projects [done]
- Tasks [done]
- Organizations [done]
- Contacts [done]

## Phase 2
Department Workflows
- Marketing: Campaigns and Content [done]
- Product: Product Requests, Product Areas, Bugs & Issues, QA & Testing, Releases, Changelog [done]
- Care: Care Tickets and Scraped Listing [done]
- Product/Tech: Sprints [done]
- Operations: Creative Requests [done]

## Phase 3
Interfaces And Reporting
- Executive Dashboard [done]
- My Tasks [done]
- Projects [done]
- Marketing Interface [done]
- Product Request Submission [done]
- Product Triage [done]
- Engineering / Product Task Board [done]
- Bug Queue [done]
- QA Dashboard [done]
- Release Dashboard [done]
- Changelog View [done]
- Care Service Desk [done]
- Scraped Listing Review [done]
- Sales / Account Management View [done]
- Manager Dashboard [done]
- Cross-team validation and reporting [done]

## Phase 4
Native Automations
- Blog Task Generation [done]
- Creative Requests [done]
- Recurring Tasks [done]
- Urgent/high Product Request alert [done]
- Urgent/high Care Ticket alert [done]
- Upsell Potential Account Management view [done]
- Scraped Listing existing-contact intervention queue [done]
- Bug-related Product Request routing [done]
- QA failed alert [done]
- Released item to Changelog [done]

## Phase 5
Corporate Functions, Operations, And AI & Automation [current]
- Operations department and non-sensitive administration routing [planned]
- Operations Workspace interface [planned]
- AI & Automation department, roadmap, projects, and shared-task views [planned]
- AI & Automation Register [planned]
- AI & Automation Workspace interface [planned]
- Corporate Services restricted workspace [planned]
- [People & HR Base](People%20%26%20HR%20Base/README.md) [planned]
- [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md) [planned]
- Finance Requests budget-change linkage [planned]
- Budget Plans, Budget Categories, and monthly Budget Lines in USD [planned]
- Finance Request Portal, Budget Workspace, and Finance Admin interfaces [planned]
- Finance Admin monthly close and summarized accounting actual reconciliation [planned]
- Access and sensitive-data boundary testing [planned]
- No cross-base synchronization at launch [planned]

References:
- [Cross-base corporate functions requirements](company-functions-requirements.md)
- [People & HR Base](People%20%26%20HR%20Base/README.md)
- [Finance & Administration Base](Finance%20%26%20Administration%20Base/README.md)

## Phase 6
Future Integrations [planned]
- Platform to Airtable contact/account synchronization
- Airtable to EDU Inbox workflows
- Airtable to Brevo synchronization
- WhatsApp notifications
- Production monitoring, failure logging, retries, duplicate prevention, and maintenance ownership

## Boundaries
- Operations Hub Team Members table [deferred; continue using Airtable collaborator fields]
- [People & HR Employees table](People%20%26%20HR%20Base/README.md#employees) [planned as the approved HR-specific exception]
- Operations Hub Opportunities table [do not create]
- Care & Sales Base Opportunities table and Sales / Account Management pipeline [done]
- Payroll, accounting, banking, and secure document systems [authoritative outside Airtable]

## Workflows

Marketing:
Roadmap -> Project -> Campaign -> Content -> Tasks

Product:
Product Request -> Project / Bug / Task -> QA -> Release -> Changelog

Care:
Contact / Organization -> Care Ticket -> Task / Product Request / Bug

Scraped Listing:
Scraped Listing -> Contact match -> Care review / intervention

Sales / Account Management:
Care & Sales Base Contact / Organization -> Opportunity -> Sales follow-up

Operations:
Operations Roadmap -> Project -> shared Tasks

AI & Automation:
AI & Automation Roadmap -> Project -> shared Tasks
AI & Automation Register -> Related Project / Department Served -> monitoring and review

People & HR:
Employee -> HR Request -> restricted HR workflow

Finance & Administration:
Finance Request / Compliance item -> restricted review and approval workflow
Budget Plan -> monthly Department / Category Budget Lines -> quarterly / annual / YTD reporting
Budget Change Request -> approved adjustment -> Current Budget
Accounting monthly close -> summarized Actual Spend -> reconciliation -> lock
