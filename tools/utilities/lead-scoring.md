# Lead Scoring Utility

## Purpose
Calculate and assign lead quality scores for routing decisions.

## Scoring Algorithm

### Input Factors

```
factors = {
  budget: {
    weight: 0.25,
    scoring: {
      "unknown": 3,
      "<5000": 2,
      "5000-10000": 5,
      "10000-15000": 7,
      ">15000": 10
    }
  },
  timeline: {
    weight: 0.20,
    scoring: {
      "someday": 2,
      ">12_months": 4,
      "6-12_months": 6,
      "3-6_months": 8,
      "<3_months": 10
    }
  },
  experience: {
    weight: 0.15,
    scoring: {
      "none": 3,
      "interested": 5,
      "real_estate_adjacent": 7,
      "land_investor": 9,
      "experienced_investor": 10
    }
  },
  engagement: {
    weight: 0.20,
    scoring: {
      "single_touch": 2,
      "multiple_emails": 5,
      "content_download": 6,
      "webinar_registered": 7,
      "webinar_attended": 9,
      "demo_requested": 10
    }
  },
  goal_clarity: {
    weight: 0.20,
    scoring: {
      "vague": 2,
      "general_interest": 5,
      "specific_goal": 8,
      "specific_with_timeline": 10
    }
  }
}
```

### Calculation

```
function calculateLeadScore(factors):
  total = 0
  for factor in factors:
    score = factor.scoring[factor.value]
    weighted = score * factor.weight
    total += weighted
  return round(total, 1)
```

### Output Categories

```
function categorize(score):
  if score >= 7.5:
    return "SQL"  # Pass to Sales
  elif score >= 5.0:
    return "MQL"  # Nurture sequence
  else:
    return "Unqualified"  # Low-touch
```

## Usage Example

```
lead_data = {
  budget: "10000-15000",      # 7 × 0.25 = 1.75
  timeline: "3-6_months",      # 8 × 0.20 = 1.60
  experience: "interested",    # 5 × 0.15 = 0.75
  engagement: "webinar_attended", # 9 × 0.20 = 1.80
  goal_clarity: "specific_goal"   # 8 × 0.20 = 1.60
}

score = calculateLeadScore(lead_data)
# Result: 7.5 → SQL
```

## Integration Points
- Called by Marketing after qualification form
- Called by Sales during discovery
- Updates CRM lead score field
- Triggers routing automation
