# Decisions

001. One main base: EDU Passport Operations Hub.
Reason: CRM, PM, tasks, Product, Care, Sales, Marketing, and Operations need shared visibility and unified reporting.

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

012. HR and Finance will be planned as separate Airtable setups later.
Reason: They may contain sensitive employee, payroll, budget, or financial records.

013. Treat Brevo, WhatsApp, EDU Inbox, and platform sync as later integration phases.
Reason: Native Airtable structure should be stable before external integrations.

014. Use Airtable collaborator/user fields directly for owners and assignees.
Reason: Simpler than maintaining a Team Members table for Milestone 1.

015. Defer Team Members table.
Reason: Add it later only if manager hierarchy, staff metadata, non-Airtable users, capacity planning, or historical staff records become necessary.

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

022. Defer Opportunities until Sales/Account Management workflow is ready.
Reason: Current Care requirements can be handled with Care Tickets.Upsell Potential and Scraped Listing without creating a pipeline table in Milestone 1.

023. Product Tasks table remains deferred.
Reason: Product execution belongs in the shared Tasks table for unified reporting.

024. Product Roadmap table remains deferred.
Reason: Product initiatives should use shared Roadmaps and Projects unless a separate roadmap table becomes necessary later.

025. Keep Product Requests and Bugs internal for Milestone 2.
Reason: They gather internal team requests and issue reports; CRM links should only be added when a specific workflow needs them.

026. Product task fields are additions to shared Tasks, not a new table.
Reason: Product execution must remain part of the shared company task system.
