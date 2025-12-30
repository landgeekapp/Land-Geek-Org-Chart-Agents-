# Escalation Router Utility

## Purpose
Route escalations to the correct decision-maker with appropriate urgency.

## Routing Logic

```
function routeEscalation(trigger, context):

  # Determine target and SLA
  routing = getRoutingRules(trigger)

  # Build escalation package
  escalation = {
    from: context.agent,
    to: routing.target,
    trigger: trigger,
    priority: routing.priority,
    sla: routing.sla,
    created_at: now(),
    due_by: now() + routing.sla,
    context: context.details,
    recommendation: context.recommendation
  }

  # Send notification
  notify(routing.target, escalation)

  # Log escalation
  logEscalation(escalation)

  return escalation.id
```

## Routing Rules

```
routing_rules = {

  # Financial
  "spending_over_500": {
    target: "CEO",
    priority: "standard",
    sla: "24_hours"
  },
  "discount_over_10_percent": {
    target: "CEO",
    priority: "standard",
    sla: "24_hours"
  },

  # Client Issues
  "refund_request": {
    target: "CEO",
    priority: "high",
    sla: "4_hours"
  },
  "formal_complaint": {
    target: "CEO",
    priority: "high",
    sla: "2_hours"
  },
  "legal_concern": {
    target: "CEO",
    priority: "immediate",
    sla: "1_hour"
  },

  # HR
  "hiring_request": {
    target: "CEO",
    priority: "standard",
    sla: "1_week"
  },

  # Operations
  "system_issue": {
    target: "Head_of_Operations",
    priority: "high",
    sla: "4_hours"
  },
  "process_failure": {
    target: "Head_of_Operations",
    priority: "high",
    sla: "4_hours"
  },

  # Sales
  "upsell_opportunity": {
    target: "Head_of_Sales",
    priority: "standard",
    sla: "48_hours"
  },
  "referral_received": {
    target: "Head_of_Sales",
    priority: "high",
    sla: "24_hours"
  }
}
```

## Notification Template

```
Subject: [Priority] Escalation: {trigger_title}

From: {from_agent}
Priority: {priority}
Response needed by: {due_by}

## Situation
{context.situation}

## Background
{context.background}

## Impact
{context.impact}

## Recommendation
{recommendation}

## Action Required
Please respond by {due_by} with decision or questions.
```

## Tracking
- All escalations logged with timestamps
- SLA compliance tracked
- Monthly report on escalation patterns
- Alert if SLA breached
