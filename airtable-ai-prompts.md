# Airtable AI Prompts

Use these prompts with Airtable AI / Omni AI to create or revise the Care & Sales Base interfaces.

## Care Service Desk

```text
Create or revise an interface named “Care Service Desk” for the Care & Sales Base.

Purpose:
This interface is for Care agents to manage their daily support work, urgent tickets, and tickets that may become Sales opportunities.

Use these tables:
- Tickets & Care Pipeline
- Contacts
- Opportunities, for linked sales context only

Keep the interface simple. Create only these pages:

1. My Tickets
Use the Tickets & Care Pipeline table.
Filter where assigned agent is the current user.
Show active tickets first, where ticket status is not Resolved.
Sort by ticket priority, then created date.
Show:
- ticket ID
- associated contact
- issue type
- ticket priority
- ticket status
- created date
- last modified
- assigned agent
- escalated
- first response time
- upsell potential
- opportunities

2. Urgent Tickets
Use the Tickets & Care Pipeline table.
Filter where ticket priority is High or Urgent.
Show unresolved tickets first.
Show:
- ticket ID
- associated contact
- issue type
- ticket priority
- ticket status
- assigned agent
- created date
- first response time
- escalated
- resolution note

3. Upsell Potential
Use the Tickets & Care Pipeline table.
Filter where upsell potential is checked.
Show:
- ticket ID
- associated contact
- issue type
- ticket priority
- ticket status
- assigned agent
- customer feedback
- resolution note
- upsell potential
- opportunities

This page should help Care identify tickets that may become Sales opportunities.

4. Ticket Detail
Create a record detail or record review page for Tickets & Care Pipeline.
Show:
- ticket ID
- associated contact
- issue type
- ticket priority
- ticket status
- created date
- last modified
- assigned agent
- resolution note
- upsell potential
- escalated
- first response time
- satisfaction rating
- customer feedback
- opportunities

Interface behavior:
- Care should mainly work from Tickets & Care Pipeline.
- Care should be able to update ticket status, priority, assigned agent, resolution note, upsell potential, escalated, satisfaction rating, and customer feedback.
- Show the existing linked field “opportunities” so Care can see related Sales opportunities.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Scraped Feeds Review

```text
Create an interface named “Scraped Feeds Review” for the Care & Sales Base.

Purpose:
This interface is for the Care team to review scraped external market signals, clean contact information, match records to Contacts, and decide whether a scraped feed should be handed to Sales as an opportunity.

Use these tables:
- Scraped Feeds
- Contacts
- Opportunities, for linked sales context only

Keep the interface simple. Create these pages:

1. New Feeds
Use the Scraped Feeds table.
Show newly added scraped feed records that still need first review.
Show useful fields such as:
- post type
- source URL
- raw contact info
- cleaned email
- matched contact
- existing user cross-check
- repeat poster flag
- Sales Handoff Status
- opportunities
- notes

2. Needs Review
Use the Scraped Feeds table.
Show records that still need Care cleanup or matching.
Include records where cleaned email is empty, matched contact is empty, or existing user cross-check says No Match Yet, if those fields exist.
Show:
- post type
- source URL
- raw contact info
- cleaned email
- matched contact
- existing user cross-check
- repeat poster flag
- notes

3. Ready for Sales
Use the Scraped Feeds table.
Filter where Sales Handoff Status is Ready for Sales.
Show:
- post type
- source URL
- cleaned email
- matched contact
- existing user cross-check
- repeat poster flag
- Sales Handoff Status
- opportunities
- notes

This page should show scraped leads that are ready to become Sales opportunities.

4. Reviewed Feeds
Use the Scraped Feeds table.
Show records that have already been reviewed, handed off, accepted, rejected, or linked to an opportunity.
Show:
- post type
- source URL
- cleaned email
- matched contact
- Sales Handoff Status
- opportunities
- notes

5. Feed Detail
Create a record detail or record review page for Scraped Feeds.
Show all important context:
- post type
- source URL
- raw contact info
- cleaned email
- matched contact
- existing user cross-check
- repeat poster flag
- Sales Handoff Status
- opportunities
- notes

Interface behavior:
- Care should be able to review and update Scraped Feeds.
- Care should clean contact information, link matched contacts, update Sales Handoff Status, and add notes.
- Opportunities should be visible only as linked sales context.
- Use the existing linked field “opportunities” if it exists.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Customer Feedback Review

```text
Create an interface named “Customer Feedback Review” for the Care & Sales Base.

Purpose:
This interface is for the Care team to review customer feedback, identify satisfaction issues, buying intent, expansion potential, renewal risk, and feedback that should be handed to Sales as an opportunity.

Use these tables:
- Customer Feedback
- Contacts
- Opportunities, for linked sales context only

Keep the interface simple. Create only these pages:

1. New Feedback
Use the Customer Feedback table.
Show newly submitted feedback that needs first review.
Show useful fields such as:
- associated contact
- feedback type
- satisfaction rating
- feedback text
- created date
- assigned agent
- Sales Handoff Status
- opportunities
- notes

2. Needs Review
Use the Customer Feedback table.
Show feedback that still needs Care review, triage, or follow-up.
Include records where the feedback is not resolved, not reviewed, or does not yet have a clear next action, if those fields exist.
Show:
- associated contact
- feedback type
- satisfaction rating
- feedback text
- assigned agent
- Sales Handoff Status
- opportunities
- notes

3. Ready for Sales
Use the Customer Feedback table.
Filter where Sales Handoff Status is Ready for Sales.
This page should show feedback that indicates buying intent, expansion potential, or renewal risk.
Show:
- associated contact
- feedback type
- satisfaction rating
- feedback text
- Sales Handoff Status
- opportunities
- notes

4. Reviewed Feedback
Use the Customer Feedback table.
Show feedback that has already been reviewed, resolved, handed off, accepted, rejected, or linked to an opportunity.
Show:
- associated contact
- feedback type
- satisfaction rating
- feedback text
- Sales Handoff Status
- opportunities
- notes

5. Feedback Detail
Create a record detail or record review page for Customer Feedback.
Show all important context:
- associated contact
- feedback type
- satisfaction rating
- feedback text
- created date
- assigned agent
- Sales Handoff Status
- opportunities
- notes

Interface behavior:
- Care should be able to review and update Customer Feedback.
- Care should identify whether feedback needs follow-up, resolution, or Sales handoff.
- Opportunities should be visible only as linked sales context.
- Use the existing linked field “opportunities” if it exists.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```

## Sales / Account Management

```text
Create or revise an interface named “Sales / Account Management” for the Care & Sales Base.

Purpose:
This interface is for Sales and Account Management to manage opportunities, review Care handoffs, and understand contact context before outreach.

Sales mainly works from the Opportunities table.
Care source tables should be visible only as handoff/context.

Use these tables:
- Opportunities
- Contacts
- Tickets & Care Pipeline, for handoff context only
- Scraped Feeds, for handoff context only
- Customer Feedback, for handoff context only

Keep the interface simple. Create only these pages:

1. My Opportunities
Use the Opportunities table.
Filter where Owner is the current user.
Show open opportunities first, where Stage is not Won and not Lost.
Sort by Next Step Due ascending.
Show:
- Opportunity Name
- Primary Contact
- Owner
- Stage
- Estimated Value
- Probability
- Expected Close Date
- Next Step
- Next Step Due
- Source
- Notes

This should be the daily Sales work queue.

2. Pipeline Board
Use the Opportunities table.
Create a kanban-style page grouped by Stage.
Show these stages:
- New
- Qualified
- Discovery
- Proposal
- Negotiation
- Won
- Lost
- Nurture

Show these fields on cards:
- Opportunity Name
- Primary Contact
- Owner
- Estimated Value
- Expected Close Date
- Next Step
- Next Step Due
- Source

3. Sales Handoffs
Create a page that helps Sales review records handed off from Care.
Show sales-ready records from these source tables if possible:
- Tickets & Care Pipeline where Sales Handoff Status is Ready for Sales or upsell potential is checked
- Scraped Feeds where Sales Handoff Status is Ready for Sales
- Customer Feedback where Sales Handoff Status is Ready for Sales

Show useful fields from source records:
- associated contact or matched contact
- Sales Handoff Status
- opportunities
- notes
- source details
- customer feedback or resolution note, if available

This page is for reviewing Care signals before creating or accepting an Opportunity.

4. Contact Context
Use the Contacts table.
Create a record review or list page so Sales can review customer context before outreach.
Show:
- Full Name
- Email
- Organization, if available
- User Type
- Platform Status
- Phone / WhatsApp
- WeChat ID
- Contact Owner
- Notes
- linked Tickets & Care Pipeline records
- linked Scraped Feeds
- linked Customer Feedback
- linked Opportunities

Interface behavior:
- Sales should primarily edit Opportunities.
- Sales can review Care source tables for context.
- Do not duplicate contact information inside Opportunities if it can be linked to Contacts.
- Use existing fields only.
- Do not create duplicate fields.
- If a suggested field does not exist, skip it instead of creating a new field.
```
