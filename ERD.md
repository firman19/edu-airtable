# EDU Passport Operations Hub

# Entity Relationship Diagram (ERD)

## Overview

```text
                              Departments
                                   |
                                   v
Roadmaps ---------------------> Projects ----------------------> Tasks
                                   |                              ^
                                   |                              |
             +---------------------+----------------------+-------+------+
             |                     |                      |              |
             v                     v                      v              v
        Campaigns               Content                 Sprints   Creative Requests

Organizations ---------> Contacts
        |                         |
        v                         v
                 Care Tickets              Product Requests
                                  |                 |
                                  v                 v
 Scraped Listing ------------> Contacts        Bugs & Issues
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

## Relationships

- Departments (1) -> Roadmaps (N)
- Departments (1) -> Projects (N)
- Departments (1) -> Tasks (N)
- Roadmaps (1) -> Projects (N)
- Projects (1) -> Tasks (N)
- Projects (1) -> Campaigns (N)
- Projects (1) -> Content (N)
- Projects (1) -> Sprints (N)
- Projects (1) -> Creative Requests (N)
- Projects (1) -> Product Requests (N, optional)
- Projects (1) -> Bugs & Issues (N, optional)
- Organizations (1) -> Contacts (N)
- Organizations (1) -> Care Tickets (N, optional)
- Contacts (1) -> Care Tickets (N)
- Contacts (1) -> Scraped Listing (N, optional)
- Care Tickets (1) -> Tasks (N, optional)
- Scraped Listing (N) -> Contacts (1, optional)
- Product Requests (1) -> Tasks (N, optional)
- Product Requests (N) -> Product Areas (1)
- Bugs & Issues (1) -> Tasks (N, optional)
- Bugs & Issues (1) -> QA & Testing (N)
- QA & Testing (N) -> Releases (1, optional)
- Releases (1) -> Changelog (N)

## Business Rules

1. The main base is EDU Passport Operations Hub.
2. One shared Tasks table is the execution source of truth.
3. One shared Contacts table is the CRM identity source of truth.
4. Every Task must belong to one Project.
5. Projects are the main container for initiatives.
6. Product Tasks are filtered records inside shared Tasks.
7. Care Contacts are records inside shared Contacts.
8. Product owns triage, priority, roadmap decisions, bugs, QA, releases, and changelog wording.
9. Care owns Care Tickets, Scraped Listing, and contact support details.
10. Interfaces provide workflow guardrails by role.
11. Use Airtable collaborator/user fields directly for owners and assignees.
12. Team Members is deferred unless staff metadata or manager hierarchy becomes necessary.
13. Opportunities is deferred until Sales/Account Management workflow is ready.
14. HR and Finance are planned as separate Airtable setups later.

## Tables

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
