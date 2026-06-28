# Product Field Requirements

# Milestone 2 Target Schema Checklist

Source: `docs/EDU_Airtable_Product_Blueprint.xlsm`

This checklist adapts the Product blueprint to the Operations Hub decisions:
- Do not create a separate `Product Tasks` table. Use shared `Tasks` with Product/Product-Tech context.
- Do not create a separate `Product Roadmap` table. Use shared `Roadmaps` and `Projects`.
- Product Requests and Bugs are internal workflow records. Do not link them directly from Contacts by default.
- Product Requests do not need Related Organization, Related Contact, or Related Bug fields for this phase.
- Bugs do not need Related Product Request, Related Organization, or Related Contact fields for this phase.
- Releases do not need direct Related Projects, Related Tasks, Related Bugs, Release Owner, or QA Records fields for this phase.
- Product execution must remain visible in the shared `Tasks` table.

For each field, mark one audit result:
- `Present`
- `Missing`
- `Rename`
- `Change Type`
- `Remove / Later`

## Product Requests

Purpose: Internal intake for feature requests, bug reports, UX issues, data issues, content issues, and operational product needs.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Request ID | Autonumber | Yes | Unique request reference. | Present |
| Summary | Single line text | Yes | Primary human-readable request title. | Present |
| Details | Long text | Yes | Context, examples, screenshots, links, user quotes, or notes. | Present |
| Submitted By | Collaborator / text | Yes | Person who submitted the request. | Present |
| Source Team | Single select | Yes | Options: Care, Marketing, Growth, Product, Leadership, User. | Present |
| Request Type | Single select | Yes | Options: Feature Request, Bug, UX Issue, Data Issue, Content Issue, Operational Request. | Present |
| Product Area | Linked record to Product Areas | Yes | Use linked Product Areas instead of free text. | Present |
| Priority | Single select | Yes | Options: Urgent, High, Medium, Low. | Present |
| Impact | Single select | Yes | Options: One user, Multiple users, Key account, Revenue impact, Blocking workflow. | Present |
| Status | Single select | Yes | Options: New, Under Review, Needs More Info, Accepted, In Progress, Released, Not Planned, Closed. | Present |
| Product Owner | Collaborator / Airtable user | Required after triage | Owner responsible for triage or follow-up. | Present |
| Related Project | Linked record to Projects | No | Use when request becomes initiative/project work. | Present |
| Related Task | Linked record to Tasks | No | Use for small accepted requests executed as tasks. | Present |
| Final Decision / Notes | Long text | No | Closure reason, release note, or not-planned explanation. | Present |

## Product Areas

Purpose: Reference taxonomy for consistent product area names and ownership.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Product Area Name | Single line text | Yes | Primary field. Examples: Jobs, Listings, Claim Flow, Feed, Admin Panel, Messaging, User Profile, Search, Billing, Other. | Present |
| Owner | Collaborator / Airtable user | No | Product owner for this area. | Present |
| Status | Single select | No | Options: Active, Inactive. | Present |
| Description | Long text | No | Area scope and boundaries. | Present |
| Product Requests | Linked records to Product Requests | Auto/backlink | Backlink from Product Requests. | Present |
| Bugs & Issues | Linked records to Bugs & Issues | Auto/backlink | Backlink from Bugs. | Present |
| Tasks | Linked records to Tasks | Auto/backlink | Backlink from shared Tasks, if Tasks link to Product Areas. | Present |

## Bugs & Issues

Purpose: Confirmed bugs, platform issues, reproduction steps, affected users, and resolution status.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Bug ID | Autonumber | Yes | Unique bug reference. | Present |
| Bug Summary | Single line text | Yes | Primary field. | Present |
| Product Area | Linked record to Product Areas | Yes | Area affected. | Present |
| Severity | Single select | Yes | Options: Critical, High, Medium, Low. | Present |
| Status | Single select | Yes | Options: New, Confirmed, In Progress, Fixed, QA Passed, Released, Cannot Reproduce. | Present |
| Reported By | Collaborator / text | No | Original reporter. | Present |
| Related Task | Linked record to Tasks | No | Shared execution task for the fix. | Present |
| Reproduction Steps | Long text | Required for confirmed bugs | Steps needed to reproduce the issue. | Present |
| Expected Behavior | Long text | No | What should happen. | Present |
| Actual Behavior | Long text | No | What actually happened. | Present |
| Attachments | Attachment | No | Screenshots, recordings, logs. | Present |
| Release | Linked record to Releases | No | Release where bug fix ships. | Present |
| QA & Testing | Linked records to QA & Testing | Auto/backlink | Backlink from QA records that test this bug. | Present |

## QA & Testing

Purpose: Test cases, QA results, blockers, and release validation.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Test Case ID | Autonumber | Yes | Unique test reference. | Present |
| Test Name | Single line text | Yes | Primary field. | Present |
| Related Task | Linked record to Tasks | No | Shared task being tested. | Present |
| Related Bug | Linked record to Bugs & Issues | No | Bug being tested. | Present |
| Related Release | Linked record to Releases | No | Release being validated. | Present |
| Tester | Collaborator / Airtable user | Yes | Person responsible for QA. | Present |
| QA Status | Single select | Yes | Options: Not Started, Passed, Failed, Blocked. | Present |
| Test Steps | Long text | No | What QA should verify. | Present |
| Actual | Long text | No | Actual QA observation during testing. | Present |
| Result | Long text / single select | No | Final result or outcome recorded by QA. | Present |
| Tested Date | Date | No | Date test was run. | Present |

## Releases

Purpose: Release batches, launch status, included work, QA status, and team notification needs.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Release ID | Autonumber | Yes | Unique release reference. | Present |
| Release Name | Single line text | Yes | Primary field. | Present |
| Release Status | Single select | Yes | Options: Planning, QA, Ready, Released, Rolled Back. | Present |
| Release Date | Date | No | Target or actual release date. | Present |
| Teams to Notify | Multiple select | Yes | Options: Care, Marketing, Growth, Leadership, Users. | Present |
| Release Notes | Long text | No | Internal readiness notes. | Present |
| QA & Testing | Linked records to QA & Testing | Auto/backlink | QA records related to this release. | Present |
| Changelog | Linked records to Changelog | Auto/backlink | Changelog entries for this release. | Present |

## Changelog

Purpose: Internal and user-facing explanations of what changed and what teams should say.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Changelog Title | Single line text | Yes | Primary field. | Present |
| Release | Linked record to Releases | Yes | Release this message belongs to. | Present |
| Audience | Single select | Yes | Options: Internal, Care, Marketing, Growth, Users. | Present |
| Summary | Long text | Yes | What changed, in plain language. | Present |
| Recommended Message | Long text | No | Reusable wording for teams. | Present |
| Owner | Collaborator / Airtable user | Yes | Person responsible for final wording. | Present |
| Published Date | Date | No | Date message is published/sent. | Present |

## Existing Tasks Table: Product Fields

Purpose: These are optional fields to add to the existing shared `Tasks` table. Do not create a new Product Tasks table.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Task Type | Single select | No | Options: Product, Design, Engineering, Data, QA, General. Add if useful for Product task boards. | Present |
| Related Product Request | Linked record to Product Requests | No | Use for accepted requests. | Present |
| Related Bug | Linked record to Bugs & Issues | No | Use for bug fix tasks. | Present |
| QA & Testing | Linked records to QA & Testing | No | Use when a task has related QA records. | Present |
| Product Areas | Linked records to Product Areas | No | Use when Product tasks need product-area grouping. | Present |

## Deferred / Adapted Product Blueprint Items

- `Product Tasks` table: do not create. Use shared `Tasks`.
- `Product Roadmap` table: do not create. Use shared `Roadmaps` and `Projects`.
- Direct `Contacts -> Product Requests` backlink: do not add by default.
- Direct `Contacts -> Bugs & Issues` backlink: do not add by default.
- `Blocker / Failure Notes` on QA & Testing: do not add; use `Actual` and `Result` for failure notes.
- `Release Owner` on Releases: do not add; release ownership can be handled through workflow or notes for now.
- `Related Release` on Tasks: do not add; use QA/Release-side links when needed.
- `Dependencies` on Tasks: do not add in this phase.
- Release back-links to Projects, Tasks, and Bugs: do not add in this phase; use existing links from those records when needed.

## Milestone 2 Completion Checklist

- [x] Product Requests exists.
- [x] Product Areas exists.
- [x] Bugs & Issues exists.
- [x] QA & Testing exists.
- [x] Releases exists.
- [x] Changelog exists.
- [x] Shared Tasks has Product-related links where needed.
- [x] Product Requests can link to Product Areas, Projects, and Tasks.
- [x] Bugs can link to Product Areas, Tasks, QA, and Releases.
- [x] QA can link to Tasks, Bugs, and Releases.
- [x] Releases can link to Changelog.
- [x] Product workflow can move from request to triage to task/bug to QA to release to changelog.
