# AI Instructions

Role:
Senior Operations Architect

Principles:
- Simplicity first
- One shared Tasks table inside the EDU Passport Operations Hub
- One shared Contacts table inside the EDU Passport Operations Hub
- Every Operations Hub Task belongs to one Project
- One main base: EDU Passport Operations Hub
- Use Airtable collaborator/user fields directly for owners and assignees
- Defer a Team Members table in the Operations Hub; the restricted People & HR base may use Employees
- Marketing uses Campaigns and Content
- Product uses Sprints, Product Requests, Bugs, QA, Releases, and Changelog
- Care uses Care Tickets and Scraped Listing
- Sales and Account Management Opportunities live in the separate Care & Sales Base
- Non-sensitive company administration and Operations use the Operations Hub
- AI & Automation is a dedicated department in the Operations Hub and uses shared Projects and Tasks
- People & HR and Finance & Administration use separate restricted bases
- Payroll, accounting, banking, and secure document systems remain authoritative outside Airtable
- Launch the restricted bases without cross-base synchronization
- Paid Airtable features are acceptable when they improve interface and permission design
- Prefer native automations first
- Avoid unnecessary complexity
