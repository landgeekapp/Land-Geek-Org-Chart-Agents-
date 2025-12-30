# Head of Sales Agent Test Scenarios

## Scenario 1: Lead Qualification
**Input**: "New lead from Facebook ad, interested in Flight School, budget unknown"
**Expected behavior**: Ask qualifying questions, score lead, route appropriately

### Success Criteria
- [ ] Asks about budget/investment capacity
- [ ] Asks about timeline/urgency
- [ ] Asks about prior land investing experience
- [ ] Asks about goals/motivation
- [ ] Calculates lead quality score
- [ ] Routes based on score (≥7.5 = SQL, <7.5 = nurture)
- [ ] Logs interaction in CRM

---

## Scenario 2: Discount Request
**Input**: "Prospect wants 15% off Flight School"
**Expected behavior**: Escalate to CEO with recommendation (outside 10% authority)

### Success Criteria
- [ ] Recognizes 15% exceeds 10% authority limit
- [ ] Does NOT approve the discount independently
- [ ] Prepares escalation with:
  - [ ] Prospect details and history
  - [ ] Reason for discount request
  - [ ] Recommendation (approve/counter/deny)
  - [ ] Deal value and margin impact
- [ ] Escalates to CEO within protocol
- [ ] Offers alternative within authority (e.g., 10% + bonus)

---

## Scenario 3: Team Performance Issue
**Input**: "Closer conversion rate dropped from 30% to 20% this month"
**Expected behavior**: Analyze data, identify root cause, propose coaching plan

### Success Criteria
- [ ] Acknowledges the 10-point drop as significant
- [ ] Requests/analyzes supporting data:
  - [ ] Lead quality scores for the period
  - [ ] Individual rep performance breakdown
  - [ ] Call/demo recordings review
  - [ ] Pipeline stage drop-off analysis
- [ ] Identifies potential root causes
- [ ] Proposes specific coaching interventions
- [ ] Sets measurable improvement targets
- [ ] Does NOT escalate (within decision authority)
