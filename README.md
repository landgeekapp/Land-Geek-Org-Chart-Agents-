# Land Geek AI Agents

AI agent system for The Land Geek organization, designed to support operations with role-specific agents that maintain company values and decision-making guardrails.

## Quick Start

1. Each agent has a dedicated folder in `agents/` with:
   - `system-prompt.md` - Role identity, KPIs, responsibilities
   - `.cursorrules` - Cursor IDE integration rules

2. Reference the base template for universal context:
   - `prompts/system-prompts/base-template.md`

3. Test agents using scenarios in `tests/`

## Project Structure

```
landgeek-agents/
├── agents/                    # Individual agent configurations
│   ├── ceo/
│   ├── head-of-operations/
│   ├── head-of-sales/
│   ├── head-of-marketing/
│   ├── client-success-manager/
│   └── shared/                # Cross-agent protocols
│
├── prompts/
│   ├── system-prompts/        # Base templates
│   └── guardrails/            # Role-specific constraints
│
├── tools/
│   ├── integrations/          # CRM, email, etc.
│   └── utilities/             # Helper functions
│
├── knowledge/
│   ├── scorecards/            # KPI definitions per role
│   ├── sops/                  # Standard operating procedures
│   └── company-context/       # Company info, products, values
│
├── tests/                     # Agent test scenarios
└── config/                    # Configuration files
```

## Agents

| Agent | Mission | Key Decisions |
|-------|---------|---------------|
| **CEO** | Strategic vision & sustainable growth | All major expenditures, hiring, partnerships |
| **Head of Operations** | Operational excellence & scale | Process improvements <$500, documentation |
| **Head of Sales** | Revenue through value delivery | Discounts ≤10%, lead routing, team targets |
| **Head of Marketing** | Lead generation & brand authority | Content, campaigns, budget allocation ≤20% |
| **Client Success** | Client retention & satisfaction | Support prioritization, proactive outreach |

## Core Values (F.R.E.E.)

- **Focus & Flow**: Don't sweat the small stuff, stay focused
- **Real Work & Relationships**: Do meaningful work with people you respect
- **Excellence Always**: Bring your best—details create trust
- **Evolve Constantly**: Kaizen mindset. Keep improving, every day

## Universal Guardrails

1. Never make financial commitments without CEO approval
2. Never share proprietary methodologies externally
3. Always escalate client complaints to appropriate leadership
4. Maintain confidentiality of student/client data
5. Stay within your role's decision-making authority

## Usage with Cursor

Each agent folder contains a `.cursorrules` file. When working in that context:

1. Open the agent's folder in Cursor
2. The rules automatically apply to AI assistance
3. Reference knowledge files using `@` notation

## Testing Agents

Run scenarios from `tests/` to validate agent behavior:

1. Present the input scenario to the agent
2. Check responses against success criteria
3. Verify guardrails are respected
4. Confirm escalations happen when required

## Handoff Protocols

See `agents/shared/communication-protocol.md` for:
- Sales → Client Success (new clients)
- Marketing → Sales (qualified leads)
- Client Success → Sales (upsells, referrals)
- All → CEO (escalations with SLAs)
