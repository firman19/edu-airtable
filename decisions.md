# Decisions

001. One main operational base: EDU Passport Operations Hub.
Reason: CRM, PM, tasks, Product, Care, Marketing, Operations, and AI & Automation need shared visibility and unified reporting; restricted corporate functions and the Sales pipeline use purpose-specific bases.

002. One shared Tasks table.
Reason: Unified execution reporting and no duplicate department task systems.

003. Every Task requires a Project.
Reason: Prevent orphan records and keep execution tied to initiatives.

004. One shared Contacts table.
Reason: Care, Product, Sales, and Growth need the same customer identity source.

005. Use Organizations for schools, businesses, vendors, partners, and other institutions.
Reason: Schools, businesses, vendors, and other organizations need shared CRM context.

006. Product Tasks are records in shared Tasks.
Reason: Product execution must be reportable with company-wide work.

007. Care Contacts are records in shared Contacts.
Reason: Care should not maintain a duplicate CRM.

008. Marketing uses Campaigns and Content.
Product uses Sprints, Product Requests, Bugs, QA, Releases, and Changelog.
Care uses Care Tickets and Scraped Listing.

009. Removed Roles table.
Reason: Simpler maintenance.

010. Use role-specific interfaces for workflow guardrails.
Reason: Staff should work in simple department interfaces instead of raw tables.

011. Paid Airtable features are acceptable when they improve interface and permission design.
Reason: Access and role-specific workflows matter more than staying strictly on the Free Plan.

012. HR and Finance use separate restricted Airtable bases in the EDU Passport Corporate Services workspace.
Reason: Employee, payroll, budget, contract, payment, and financial records require stronger visibility boundaries than editing restrictions inside the shared Operations Hub.

013. Treat Brevo, WhatsApp, EDU Inbox, and platform sync as Milestone 9 integration work.
Reason: Native Airtable structure and corporate-function access boundaries should be stable before external integrations.

014. Use Airtable collaborator/user fields directly for owners and assignees.
Reason: Simpler than maintaining a Team Members table for Milestone 1.

015. Defer a Team Members table in the Operations Hub.
Reason: Operations Hub ownership continues using collaborator fields. The restricted People & HR base may use an Employees table because staff metadata and employee lifecycle history are HR-specific requirements.

016. Use latest Airtable field audit as the Milestone 1 comparison baseline.
Reason: Departments, Roadmaps, Projects, and Tasks already have working fields that should be checked before adding new structure.

017. Organizations represents institutions, not individual people.
Reason: Contacts are people; Organizations groups contacts, care context, projects, and later opportunity reporting.

018. Department.Team Member is an Airtable user/collaborator field, not a Team Members table.
Reason: Department membership can be tracked simply with Airtable users while the separate Team Members table remains deferred.

019. Rename Accounts / Companies to Organizations.
Reason: Organizations is clearer across Sales, Care, Product, schools, businesses, vendors, and partners.

020. Rename Deals / Sales Pipeline to Opportunities.
Reason: Opportunities covers sales, upsell, account management, triggered leads, and revenue potential without sounding sales-only.

021. Do not link Contacts directly to Product Requests or Bugs & Issues for Milestone 1.
Reason: Product Requests and Bugs & Issues are internal team workflows; connect them through Care Tickets, Tasks, Organizations, or later workflow-specific links only when needed.

022. Do not create Opportunities in the Operations Hub.
Reason: The Sales and Account Management pipeline is implemented in the separate Care & Sales Base; the Operations Hub retains Care signals without duplicating the pipeline table.

023. Product Tasks table remains deferred.
Reason: Product execution belongs in the shared Tasks table for unified reporting.

024. Product Roadmap table remains deferred.
Reason: Product initiatives should use shared Roadmaps and Projects unless a separate roadmap table becomes necessary later.

025. Keep Product Requests and Bugs internal for Milestone 2.
Reason: They gather internal team requests and issue reports; CRM links should only be added when a specific workflow needs them.

026. Product task fields are additions to shared Tasks, not a new table.
Reason: Product execution must remain part of the shared company task system.

027. Implement subtasks through a self-link in the shared Tasks table.
Reason: Subtasks need execution ownership and reporting, but a separate Subtasks table would duplicate the task system.

028. Support only one subtask level by default.
Reason: Task -> subtask is enough for execution tracking, while deep nesting makes Airtable views, rollups, and ownership reporting harder to maintain.

029. Milestones 4 through 7 are complete, and Milestone 8 is the current milestone.
Reason: Interfaces, native automations, validation/reporting, and the Sales / Account Management pipeline have been completed; corporate-function boundaries are the next implementation priority.

030. Non-sensitive company administration and Operations remain in the Operations Hub.
Reason: Shared Roadmaps, Projects, and Tasks already provide the required execution and reporting model without another base or general Operations table.

031. AI & Automation is a dedicated department in the Operations Hub.
Reason: Company-wide AI and automation require stable ownership and reporting but still benefit from shared Projects and Tasks.

032. Use an AI & Automation Register for governed systems.
Reason: Live AI use cases, automations, and integrations need owners, data classification, human-review decisions, monitoring state, review dates, and runbooks without becoming a duplicate task system.

033. Create a restricted Corporate Services workspace with People & HR and Finance & Administration bases.
Reason: Two bases provide clear HR and Finance access boundaries while avoiding a separate base for every administrative workflow.

034. Keep payroll, accounting, banking, and secure document systems authoritative.
Reason: Airtable should coordinate requests, approvals, status, metadata, and reporting rather than become the payroll engine, accounting ledger, bank, credential store, or unrestricted document repository.

035. Launch Milestone 8 without cross-base synchronization.
Reason: Sensitive data should not propagate by default. Any later sync must be explicitly approved, one-way, non-sensitive, and field-allowlisted.

036. Marketing owns only marketing-specific AI work that it builds and maintains.
Reason: Company-wide or centrally delivered AI and automation belongs to AI & Automation; the served department is recorded separately from technical ownership.

037. Cross-boundary coordination Tasks must be sanitized.
Reason: The Operations Hub may track non-sensitive actions, but employee cases, compensation, bank data, payment attachments, and confidential financial details stay in the restricted source base.

038. Use monthly Department x Budget Category records as the Finance budget source of truth.
Reason: One monthly grain supports consistent quarterly, annual, and YTD reporting without duplicate period totals.

039. Use USD as the Milestone 8 budget reporting currency.
Reason: All department budget comparisons and rollups require one consistent reporting currency.

040. Keep the accounting system authoritative for actual spending.
Reason: Finance posts or imports summarized reconciled monthly actuals into Airtable without duplicating transaction-level accounting or banking data.

041. Allow all department leads to view approved company-wide budget comparisons.
Reason: Shared visibility supports company-wide planning and accountability while the restricted Finance base still protects detailed workflows and control fields.

042. Use shared controlled editing for budget planning.
Reason: Department leads edit their own draft planning, active forecasts, and notes; Finance can edit all departments and exclusively controls approvals, adjustments, commitments, actuals, reconciliation, and locking.

043. Preserve approved budget baselines.
Reason: Post-approval changes use signed Budget Change requests that roll into Current Budget instead of overwriting Baseline Planned Amount.

044. Maintain Department as a controlled Finance-base single select for Milestone 8.
Reason: Department reporting is required, but cross-base Departments synchronization remains intentionally disabled at launch.
