# Care Field Requirements

# Milestone 3 Target Schema Checklist

Sources:
- `docs/Airtable_ Care Department Blueprint.docx`
- `docs/Airtable_ Care Department Blueprint.pdf`

This checklist adapts the Care blueprint to the Operations Hub decisions:
- Do not create a separate Care Contacts table. Use shared `Contacts`.
- Do not create `Opportunities` in Milestone 3. Capture upsell with `Care Tickets.Upsell Potential`.
- Keep platform sync, Brevo sync, WhatsApp, and EDU Inbox automation as later integration work.
- Care execution work should use shared `Tasks` when follow-up work is needed.
- Care escalations to Product can be handled through shared `Tasks`, notes, or a later interface/process. Direct Product links are not required in Milestone 3.

For each field, mark one audit result:
- `Present`
- `Missing`
- `Rename`
- `Change Type`
- `Remove / Later`

## Shared Contacts: Care Fields

Purpose: Shared CRM identity for users, leads, educators, businesses, vendors, and contacts handled by Care.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Contact ID | Autonumber / unique ID | Yes | Existing shared contact identifier; can later map to platform user ID. | Present |
| Full Name | Single line text | Yes | Person name. | Present |
| Email | Email | Yes | Match key for platform/Brevo later. | Present |
| Organization | Linked record to Organizations | No | Person's school, company, vendor, or partner organization. | Present |
| User Type | Single select | Yes | Options from blueprint: Educator, Business, Vendor. | Present |
| Platform Status | Single select | Yes | Options from blueprint: Active User, Inactive, Non-User / Lead. | Present |
| Phone / WhatsApp | Phone | No | Outreach channel. | Present |
| WeChat ID | Single line text | No | Outreach channel. | Present |
| Source | Single select / text | No | Where this contact came from. | Present |
| Contact Owner | Collaborator / Airtable user | No | Owner responsible for follow-up. | Present |
| Notes | Long text | No | Care/customer context. | Present |

## Care Tickets

Purpose: Helpdesk and service operations center for Care issues, lifecycle support, and escalation.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Ticket ID | Autonumber | Yes | Unique support ticket reference. | Present |
| Associated Contact | Linked record to Contacts | Yes | Connect ticket to the shared CRM contact. | Present |
| Issue Type | Single select | Yes | Options: Technical Bug, Account Access, Profile Verification, Billing, Feature Request, General Inquiry. | Present |
| Ticket Priority | Single select | Yes | Options: Low, Medium, High, Urgent. | Present |
| Ticket Status | Single select | Yes | Options: New, In Progress, Awaiting User Reply, Resolved. | Present |
| Upsell Potential | Checkbox | Yes | Flags users who may be ready for Sales/Account Management later. | Present |
| Organization | Linked record to Organizations | No | Useful when the issue belongs to a school, business, vendor, or partner. | Present |
| Related Task | Linked record to Tasks | No | Use when follow-up execution work is needed. | Present |
| Owner | Collaborator / Airtable user | No | Care owner responsible for the ticket. | Present |
| Notes | Long text | No | Support context, resolution notes, or user history. | Present |

## Scraped Listing

Purpose: Review external job, deal, and event posts; clean contact information; match against existing users; route intervention.

| Field | Type | Required Now | Notes | Audit Result |
| --- | --- | --- | --- | --- |
| Post Type | Single select | Yes | Options: Job Post, Deal Post, Event Post. | Present |
| Source URL | URL | Yes | Direct link to external post. | Present |
| Raw Contact Info | Long text | Yes | Uncleaned scraped text containing handles, emails, or phone numbers. | Present |
| Cleaned Email | Email | Yes | Scrubbed email used for matching. | Present |
| Repeat Poster Flag | Formula / checkbox / rollup | No | Flags repeated external posting. | Present |
| Existing User Cross-Check | Link / lookup / formula | Yes | Shows whether cleaned email matches an existing contact/user. | Present |
| Notes | Long text | No | Review notes or intervention plan. | Present |
| Matched Contact | Linked record to Contacts | No | Existing or created contact after review. | Present |

## Deferred / Later Integration Items

- Platform -> Airtable contact sync: later integration phase.
- Airtable -> EDU Inbox intervention prompt: later integration phase.
- Airtable <-> Brevo status sync: later integration phase.
- WhatsApp automation: later integration phase if still needed.
- Opportunities / Sales Pipeline: deferred until Sales or Account Management workflow is ready.
- `Care Tickets.Related Product Request`: remove or skip for Milestone 3.
- `Care Tickets.Related Bug`: remove or skip for Milestone 3.
- `Scraped Listing.Feed / Lead Name`: remove or skip for Milestone 3.
- `Scraped Listing.Matched Organization`: remove or skip for Milestone 3.
- `Scraped Listing.Related Care Ticket`: remove or skip for Milestone 3.
- `Scraped Listing.Review Status`: remove or skip for Milestone 3.
- `Scraped Listing.Owner`: remove or skip for Milestone 3.

## Existing User Cross-Check Formula

Use this formula for `Existing User Cross-Check`:

```airtable
IF(
  {Cleaned Email} = "",
  "Missing cleaned email",
  IF(
    LEN({Matched Contact} & "") > 0,
    "Existing user matched",
    "No match yet"
  )
)
```

Note: Airtable formulas cannot search `Contacts` by email on their own. For Milestone 3, Care manually searches by `Cleaned Email` and fills `Matched Contact`. Automated matching is deferred to the automations/integrations milestones.

## Milestone 3 Completion Checklist

- [x] Shared Contacts has required Care fields.
- [x] Care Tickets exists.
- [x] Scraped Listing exists.
- [x] Care Tickets can link to Contacts and Organizations.
- [x] Care Tickets can link to Tasks when follow-up work is needed.
- [x] Scraped Listing can be reviewed, cleaned, and matched to Contacts.
- [x] Upsell Potential can be flagged without creating Opportunities yet.
- [x] Care workflow can move from ticket/scraped listing to resolution, escalation, or later handoff.
