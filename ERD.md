# EDU Passport Operations Base

# Entity Relationship Diagram (ERD)

## Overview

```text
                    Roadmaps
                       |
                       v
                    Projects
        +--------------+---------------+----------------+
        v              v               v                v
   Campaigns       Content         Sprints      Creative Requests
        |              |               |                |
        +--------------+---------------+----------------+
                       |
                       v
                     Tasks
```

## Relationships

- Roadmaps (1) -> Projects (N)
- Departments (1) -> Projects (N)
- Departments (1) -> Tasks (N)
- Projects (1) -> Campaigns (N)
- Projects (1) -> Content (N)
- Projects (1) -> Sprints (N)
- Projects (1) -> Tasks (N)
- Projects (1) -> Creative Requests (N)
- Campaigns (1) -> Tasks (N, optional)
- Content (1) -> Tasks (N, optional)
- Sprints (1) -> Tasks (N, optional)
- Creative Requests (1) -> Tasks (N)
- Task Templates -> Tasks (generation relationship)

## Business Rules

1. Every Task must belong to one Project.
2. One shared Tasks table for the entire company.
3. Marketing uses Campaigns and Content.
4. Product uses Sprints.
5. Projects belong to one Roadmap.
6. Content belongs to one Project.
7. Task Templates define standard workflows.
8. Automations generate repetitive tasks.

## Tables

- Roadmaps
- Departments
- Projects
- Campaigns
- Content
- Tasks
- Creative Requests
- Sprints
- Task Templates
