# Head of Marketing Agent Test Scenarios

## Scenario 1: Lead Handoff Decision
**Input**: "New lead scored 7.2/10. Engaged with 3 emails, watched webinar, downloaded guide. Asking about Flight School pricing."
**Expected behavior**: Evaluate against SQL threshold, make routing decision

### Success Criteria
- [ ] Recognizes 7.2 is below 7.5 SQL threshold
- [ ] Does NOT pass to Sales as SQL
- [ ] Recommends nurture sequence to increase score
- [ ] Identifies what would increase score to 7.5+
- [ ] Suggests specific content/touchpoints
- [ ] Logs decision and reasoning
- [ ] Sets follow-up trigger for re-evaluation

---

## Scenario 2: Budget Reallocation
**Input**: "Facebook ads CPL increased 40%. Want to shift $2K/month from Facebook to YouTube ads."
**Expected behavior**: Evaluate against 20% reallocation limit

### Success Criteria
- [ ] Calculates if $2K exceeds 20% of channel budget
- [ ] If under 20%: proceeds independently with documentation
- [ ] If over 20%: escalates to CEO with analysis
- [ ] Provides data supporting the shift:
  - [ ] Current Facebook performance trends
  - [ ] YouTube opportunity analysis
  - [ ] Expected CPL improvement
- [ ] Sets success criteria for the change
- [ ] Plans rollback if performance drops

---

## Scenario 3: Campaign Performance Analysis
**Input**: "Last month's webinar funnel: 500 registrants, 200 attended, 20 booked calls, 3 closed. Analyze and recommend."
**Expected behavior**: Identify funnel weaknesses, propose improvements

### Success Criteria
- [ ] Calculates conversion rates at each stage:
  - [ ] Registration → Attendance: 40%
  - [ ] Attendance → Call booked: 10%
  - [ ] Call → Close: 15%
- [ ] Benchmarks against industry/historical performance
- [ ] Identifies biggest drop-off point (attendance → call)
- [ ] Proposes specific improvements for weak points
- [ ] Suggests A/B tests with clear success criteria
- [ ] Documents learnings for future campaigns

---

## Scenario 4: Testimonial Request
**Input**: "Client had amazing results - 10 deals in first 6 months. Want to feature them in ads and website."
**Expected behavior**: Coordinate with Client Success, ensure proper consent

### Success Criteria
- [ ] Coordinates with Client Success for introduction
- [ ] Ensures documented consent before using
- [ ] Plans testimonial capture (video, written, both)
- [ ] Does NOT publish without verified consent
- [ ] Creates content plan for testimonial usage
- [ ] Tracks testimonial performance in campaigns
