# Sample Workflow Automation Audit

## Scenario

A small operations team receives client requests through email, copies details into a spreadsheet, asks follow-up questions manually, and sends status updates from a shared inbox.

This sample is not a generic template for the buyer to fill out. It shows the kind of done-for-you analysis I deliver after reviewing the buyer's workflow notes, screenshots, exports, and constraints.

## Current Workflow Map

1. Client sends a request by email.
2. Coordinator reads the message and decides whether required fields are present.
3. Coordinator copies client name, request type, deadline, attachments, and notes into a spreadsheet.
4. If information is missing, coordinator replies manually.
5. When the request is accepted, coordinator assigns it to a team member.
6. Status updates are typed manually from the spreadsheet and sent from the shared inbox.
7. Manager checks the spreadsheet at the end of the day to find overdue or blocked items.

## Friction Points

- Intake quality depends on whoever reads the email first.
- Required data is validated after the client has already submitted the request.
- Spreadsheet rows do not reliably reflect email-thread state.
- Follow-up messages are inconsistent and hard to audit.
- Managers discover blockers late because status is not event-driven.

## Ranked Automation Opportunities

| Rank | Opportunity | Impact | Effort | Recommendation |
| --- | --- | --- | --- | --- |
| 1 | Structured intake form plus validation | High | Low | Build first |
| 2 | Email-to-tracker parser for legacy inbox requests | Medium | Medium | Add after form |
| 3 | Automated status digest for overdue or blocked requests | High | Low | Build alongside intake |
| 4 | Client-facing status portal | Medium | High | Later phase |

## Recommended Build

Build a structured intake and triage flow:

- Trigger: new form submission or tagged inbox message.
- Required inputs: client name, client email, request type, deadline, description, attachments, urgency, consent checkbox.
- Validation: reject or flag missing deadline, empty description, unsupported file type, or duplicate request.
- Storage: create one record in Airtable, Notion, Linear, or a spreadsheet depending on the team's existing tools.
- Assignment: route by request type and current workload.
- Notifications: send internal Slack/email notification and client confirmation.
- Digest: send daily list of overdue, blocked, and unassigned requests.

## Implementation Brief

Suggested no-code stack:

- Tally or Fillout for intake
- Airtable as request tracker
- Make or Zapier for routing
- Gmail or Outlook for confirmation email
- Slack or Teams for internal notifications

Core automation steps:

1. Receive intake submission.
2. Normalize request type and urgency.
3. Search tracker for duplicate by client email plus request title.
4. Create request record if no duplicate is found.
5. Assign owner by request type.
6. Send client confirmation with request ID.
7. Notify assigned owner.
8. Add record to daily digest filter if unassigned, blocked, or overdue.

## Guardrails

- Do not store passwords, API keys, payment card data, or private client secrets in form fields.
- Keep original email/file attachments in the system of record instead of copying sensitive values into automation logs.
- Log automation decisions, especially duplicate detection and assignment.
- Route high-risk or ambiguous requests to manual review.
- Include an easy manual override for assignment and status.

## Acceptance Checks

- A complete test submission creates exactly one tracker record.
- An incomplete test submission is rejected or routed to review with a clear reason.
- A duplicate submission does not create a second active request.
- Client confirmation includes request ID and expected next step.
- Assigned owner receives a notification with a direct tracker link.
- Daily digest includes overdue and blocked requests, and excludes completed requests.
- Sensitive test values are not copied into logs or public notifications.

## First Sprint Estimate

- Day 1: confirm intake fields, tracker schema, routing rules, and notification text.
- Day 2: build form, tracker, and core automation.
- Day 3: test duplicate handling, edge cases, and daily digest.
- Day 4: handoff docs, acceptance checklist, and owner training notes.

Estimated implementation size: one focused sprint after the audit/spec is approved.
