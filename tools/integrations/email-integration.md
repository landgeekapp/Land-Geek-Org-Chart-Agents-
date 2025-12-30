# Email Integration Template

## Overview
Template for integrating agent actions with the email marketing platform.

## Human Approval Gates

**DRAFT-ONLY MODE** (requires human approval before execution):
- `SEND_BROADCAST`: Agent drafts, human approves and sends
- `SEND_TRANSACTIONAL`: Agent drafts, human reviews template/variables
- `TRIGGER_AUTOMATION`: Agent recommends, human confirms (for sales/upsell automations)

**AUTO-EXECUTE** (agent can perform independently):
- `ADD_TAGS`: Safe, reversible
- `REMOVE_TAGS`: Safe, reversible (except unsubscribe tags)
- `UPDATE_SUBSCRIBER`: Field updates, logged

**REQUIRES REVIEW** (logged for audit, can be auto-executed):
- `ADD_SUBSCRIBER`: Logged, must have consent documentation
- `REMOVE_SUBSCRIBER`: Logged with reason

### Approval Workflow
```
Agent Action → Draft Created → Preview Generated → Human Reviews → Approve/Reject → Send/Discard
```

### Draft Format
```
DRAFT_EMAIL:
  action_type: SEND_BROADCAST
  proposed_by: agent_id
  proposed_at: timestamp
  recipients: segment description + count
  template: template_id
  variables: {...}
  preview_link: generated preview URL
  compliance_check: passed/failed/warnings
  status: pending_approval
  expires_at: timestamp + 24h
```

### Pre-Send Compliance Check
Before any email send (draft or auto):
- [ ] Unsubscribe link present
- [ ] Physical address included
- [ ] Subject line reviewed for deception
- [ ] Earnings claims have disclaimers
- [ ] Testimonials have documented consent

## Available Actions

### Subscriber Management
```
ADD_SUBSCRIBER:
  email: required
  first_name: optional
  last_name: optional
  tags: optional array
  list_id: required

REMOVE_SUBSCRIBER:
  email: required
  list_id: required

UPDATE_SUBSCRIBER:
  email: required
  fields: any subscriber field
  tags_add: optional array
  tags_remove: optional array
```

### Tagging
```
ADD_TAGS:
  email: required
  tags: array of tag names

REMOVE_TAGS:
  email: required
  tags: array of tag names

Common Tags:
  - lead_source:{source}
  - product_interest:{product}
  - lead_score:{tier}
  - customer:{product}
  - engaged
  - at_risk
```

### Automation Triggers
```
TRIGGER_AUTOMATION:
  email: required
  automation_id: required

Common Automations:
  - welcome_sequence
  - nurture_sequence
  - onboarding_{product}
  - reengagement
  - upsell_{from}_{to}
```

### Email Sending
```
SEND_TRANSACTIONAL:
  email: required
  template_id: required
  variables: object

SEND_BROADCAST:
  segment_id: required
  template_id: required
  schedule: datetime | immediate
```

## Webhook Triggers

### Inbound (Email Platform → Agent)
- `email_opened`: Track engagement
- `link_clicked`: Track interest signals
- `unsubscribed`: Update CRM
- `bounced`: Flag for cleanup

## Compliance
- Honor unsubscribes immediately
- Include unsubscribe link in all marketing emails
- Maintain consent records
- Follow CAN-SPAM / GDPR requirements
- See: knowledge/company-context/brand-voice-compliance.md

## Audit Trail
All email actions are logged with:
- Timestamp
- Agent ID
- Action type
- Recipient count (for broadcasts)
- Template used
- Human approver (if applicable)
- Send status and delivery metrics

Retention: 2 years for compliance
