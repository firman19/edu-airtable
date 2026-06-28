# Architecture

## Base
EDU Passport Operations Hub

## Operating Model
One shared base connects CRM, project management, task execution, Product workflows, Care workflows, Sales/Account Management, Marketing, and Operations.

```text
Roadmaps -> Projects -> Tasks
CRM records -> Requests / Tickets -> Projects / Tasks
Product Requests -> Projects / Tasks -> Bugs / QA -> Releases -> Changelog
Care Tickets -> Contacts / Organizations -> Tasks
Scraped Listing -> Contacts
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

## Deferred Tables
- Team Members
- Opportunities

Add Team Members later only if staff metadata, manager hierarchy, non-Airtable users, capacity planning, or historical staff records become necessary.

## Future Separate Setups
- HR
- Finance

## CRM Foundation
Organizations stores schools, businesses, vendors, partners, and other institutions. 
Contacts stores individual people. 
Opportunities is deferred for a later Sales/Account Management milestone. For now, use `Care Tickets.Upsell Potential` and `Scraped Listing` to capture signals without creating a separate pipeline table.

## Business Rules
- One shared Tasks table for all execution work.
- One shared Contacts table for CRM identity.
- Every Task belongs to one Project.
- Projects are the main container for initiatives.
- Product work uses shared Tasks, not a separate Product Tasks table.
- Care uses shared Contacts, not a separate Care Contacts table.
- Marketing uses Campaigns and Content.
- Product uses Sprints, Product Requests, Bugs, QA, Releases, and Changelog.
- Care uses Care Tickets and Scraped Listing.
- Use Airtable collaborator/user fields directly for owners and assignees.
- Interfaces guide department access and editing behavior.
- HR and Finance should be evaluated separately because of sensitive data.
