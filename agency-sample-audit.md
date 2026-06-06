# White-Label Agency Sample Audit

## Use Case

This sample shows the kind of first-pass audit/spec draft I can produce for an automation agency from anonymized discovery notes.

The agency owns the client relationship, pricing, implementation, and final review. I provide a clean delivery artifact that helps the agency qualify the lead, scope the build, and reduce senior consultant drafting time.

## Client Scenario

An agency prospect runs a B2B service business with five sales reps. New leads arrive from a website form, direct email, referrals, and LinkedIn messages. Reps manually copy information into a CRM, ask qualifying questions in separate email threads, and prepare proposals from a shared document template.

The prospect wants fewer missed follow-ups, faster proposal turnaround, and better visibility into which leads are ready for sales calls.

## Current Workflow Map

1. Lead arrives from website form, inbox, referral, or LinkedIn message.
2. Sales coordinator checks whether the lead has budget, timeline, service type, and company size.
3. Missing fields are requested manually by email.
4. Qualified leads are copied into the CRM.
5. Sales rep creates a discovery call task.
6. After the call, notes are copied into a proposal template.
7. Proposal draft is reviewed by the sales manager.
8. Final proposal is emailed to the lead.
9. Follow-up reminders are created manually.

## Friction Points

- Lead quality is judged inconsistently because intake sources do not share one qualification schema.
- Reps spend time rewriting the same qualification and proposal language.
- CRM records are often created after the first conversation, so early lead context is lost.
- Follow-up timing depends on manual reminders.
- Managers cannot quickly see which proposals are blocked by missing client information.

## Recommended Automation Opportunities

| Rank | Opportunity | Value | Effort | Risk | Recommendation |
| --- | --- | --- | --- | --- | --- |
| 1 | Unified lead qualification record | High | Low | Low | Build first |
| 2 | Proposal draft generator from discovery notes | High | Medium | Medium | Build second |
| 3 | Follow-up reminder and stalled-lead digest | Medium | Low | Low | Build alongside CRM hygiene |
| 4 | Lead-source scoring dashboard | Medium | Medium | Low | Later phase |

## Top Build Brief

### Build

Unified lead intake and proposal-prep workflow.

### Goal

Every lead should enter one structured qualification record before a rep spends time on manual proposal work. Discovery notes should produce a review-ready proposal draft, not a final unsupervised client send.

### Trigger

- New website form submission
- Email tagged `new-lead`
- Manual intake form completed by sales coordinator

### Inputs

- Lead name
- Company
- Email
- Source
- Service interest
- Budget range
- Desired timeline
- Decision maker status
- Discovery notes
- Existing pain points

### Outputs

- CRM record
- Sales rep task
- Qualification score
- Missing-info checklist
- Proposal draft outline
- Follow-up reminder
- Manager digest for stalled proposals

## Suggested Implementation Stack

The agency can adapt this to its preferred tools. For a typical no-code build:

- CRM: HubSpot, Pipedrive, Airtable, or SmartSuite
- Intake: Fillout, Tally, Typeform, or CRM-native form
- Automation: Make, Zapier, n8n, or native CRM workflow
- Drafting: OpenAI-compatible LLM step with a locked proposal prompt
- Review: Google Docs, Notion, or CRM deal notes
- Notification: Slack, Teams, Gmail, or Outlook

## Data Model Notes

### Lead Record

- `lead_id`
- `source`
- `company`
- `contact_name`
- `contact_email`
- `service_interest`
- `budget_range`
- `timeline`
- `qualification_status`
- `missing_fields`
- `assigned_rep`
- `next_follow_up_at`

### Proposal Draft Record

- `proposal_id`
- `lead_id`
- `discovery_summary`
- `recommended_scope`
- `estimated_timeline`
- `open_questions`
- `approval_status`
- `review_owner`

## Prompt Skeleton

Use this as an agency-side starting point, not as an unsupervised final proposal generator.

```text
You are drafting an internal proposal outline for a B2B services agency.

Use only the provided discovery notes and CRM fields.
Do not invent pricing, timelines, guarantees, client names, or technical facts.
If information is missing, add it to Open Questions.

Return:
1. Client context
2. Problem summary
3. Recommended scope
4. Implementation phases
5. Risks and dependencies
6. Open questions
7. Review checklist
```

## Guardrails

- Do not auto-send proposals to leads.
- Do not use private credentials or raw customer records in prompt logs.
- Keep proposal generation behind human review.
- Show missing fields rather than fabricating them.
- Keep all price, legal, compliance, and guarantee language under agency control.
- Log which source fields were used to create the draft.

## Acceptance Checks

- A complete lead intake creates one CRM record with all required fields.
- An incomplete lead intake creates a missing-info checklist instead of a proposal draft.
- Discovery notes produce a proposal outline with open questions clearly separated.
- The draft never invents pricing, client claims, or deadlines absent from the source fields.
- A manager can identify stalled proposals from a daily digest.
- A rep can see the next follow-up date without checking email manually.
- Test data with fake API keys or sensitive values is not copied into proposal text or notifications.

## Agency Handoff Notes

This draft is designed for an agency to adapt before client delivery:

- Replace generic stack references with the agency's preferred toolset.
- Add client-specific screenshots or redacted CRM fields.
- Confirm qualification fields with the sales lead before implementation.
- Add implementation estimates only after the agency reviews system access and constraints.

## Suggested Resale Positioning

This audit can be packaged as:

- a paid discovery artifact,
- a pre-build implementation brief,
- a sales enablement cleanup plan,
- or a white-label first draft before a senior consultant finalizes scope.

The highest-value next sale is usually the implementation sprint, not the audit itself. The audit should make that sprint easier to scope, approve, and hand off.
