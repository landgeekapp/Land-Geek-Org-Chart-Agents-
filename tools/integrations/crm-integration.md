# CRM Integration Template

## Overview
Template for integrating agent actions with the CRM system.

## Human Approval Gates

**DRAFT-ONLY MODE** (requires human approval before execution):
- `CREATE_DEAL`: Agent proposes, human confirms
- `CLOSE_DEAL`: Agent recommends, human executes
- `ASSIGN_LEAD`: Agent suggests, human approves reassignment

**AUTO-EXECUTE** (agent can perform independently):
- `GET_CONTACT`: Read-only, safe
- `LOG_ACTIVITY`: Documentation only
- `SCORE_LEAD`: Internal scoring, reversible

**REQUIRES REVIEW** (logged for audit, can be auto-executed):
- `UPDATE_CONTACT`: Logged with before/after
- `UPDATE_DEAL`: Logged with change history
- `QUALIFY_LEAD`: Logged with reasoning

### Approval Workflow
```
Agent Action → Draft Created → Notification Sent → Human Reviews → Approve/Reject → Execute/Discard
```

### Draft Format
```
DRAFT_ACTION:
  action_type: CREATE_DEAL
  proposed_by: agent_id
  proposed_at: timestamp
  parameters: {...}
  reasoning: "Why this action is recommended"
  status: pending_approval
  expires_at: timestamp + 24h
```

## Available Actions

### Contact Management
```
CREATE_CONTACT:
  required: email, first_name, last_name
  optional: phone, source, lead_score

UPDATE_CONTACT:
  required: contact_id
  fields: any contact field

GET_CONTACT:
  by: email | contact_id | phone
```

### Lead Management
```
SCORE_LEAD:
  contact_id: required
  score: 1-10
  factors: {budget, timeline, experience, engagement, goal_clarity}

QUALIFY_LEAD:
  contact_id: required
  status: MQL | SQL | Unqualified
  notes: optional

ASSIGN_LEAD:
  contact_id: required
  owner_id: required
  reason: optional
```

### Pipeline Management
```
CREATE_DEAL:
  contact_id: required
  product: Toolkit | FlightSchool | Wholesale
  value: number
  stage: initial stage

UPDATE_DEAL:
  deal_id: required
  stage: new stage
  notes: optional

CLOSE_DEAL:
  deal_id: required
  outcome: Won | Lost
  reason: if lost
```

### Activity Logging
```
LOG_ACTIVITY:
  contact_id: required
  type: Call | Email | Meeting | Note
  description: required
  outcome: optional
```

## Webhook Triggers

### Inbound (CRM → Agent)
- `new_lead`: New lead created
- `lead_scored`: Lead score updated
- `deal_stage_changed`: Pipeline movement
- `deal_closed`: Deal won or lost

### Outbound (Agent → CRM)
- After qualification decisions
- After deal updates
- After activity completion

## Error Handling
- Retry failed requests 3x with exponential backoff
- Log all failures for Operations review
- Alert on critical failures (deal creation, close)

## Audit Trail
All CRM actions are logged with:
- Timestamp
- Agent ID
- Action type
- Before/after state (for updates)
- Human approver (if applicable)
- Reasoning provided

Retention: 90 days minimum
