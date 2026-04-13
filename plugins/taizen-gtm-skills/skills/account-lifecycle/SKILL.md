---
description: Supports post-close account management with structured account plans, renewal playbooks, and expansion strategies. Use for account planning and growth.
---

# Account Lifecycle Skill

Strategic account management from onboarding through renewal and expansion.

## Purpose

Maximize customer lifetime value through structured account planning, proactive renewal management, and strategic expansion.

## Account Lifecycle Stages

### 1. Onboarding & Activation
- Implementation milestones
- Success criteria definition
- Stakeholder alignment
- Early value realization

### 2. Adoption & Value Realization
- Usage monitoring
- Success milestone tracking
- ROI documentation
- Relationship expansion

### 3. Renewal & Retention
- Renewal planning timeline
- Risk assessment
- Value reinforcement
- Contract optimization

### 4. Expansion & Growth
- Whitespace analysis
- Cross-sell/upsell opportunities
- New stakeholder engagement
- Strategic account development

## Account Plan Template

### Account Overview
- **Company**: Name, industry, size
- **Contract**: Value, term, renewal date
- **Health Score**: Current status and trend
- **Strategic Importance**: Tier, growth potential

### Success Metrics
- Agreed-upon success criteria
- Current performance vs. goals
- ROI delivered to date

### Stakeholder Map
- Champions, economic buyers, users
- Relationship strength by stakeholder
- Coverage gaps

### Objectives & Initiatives
- 90-day goals
- Quarterly objectives
- Annual strategic goals

### Risk & Opportunity
- Identified risks and mitigation
- Expansion opportunities
- Competitive threats

### Action Plan
- Near-term priorities
- Owner assignments
- Timeline and milestones

## Renewal & Expansion Playbook

### Renewal Timeline
- **T-180 days**: Health assessment, risk identification
- **T-120 days**: Value documentation, stakeholder alignment
- **T-90 days**: Renewal strategy, expansion scoping
- **T-60 days**: Commercial discussions, negotiation
- **T-30 days**: Contract finalization, signature
- **T-0**: Renewal complete, next cycle planning

### Expansion Triggers
- Usage thresholds exceeded
- New use cases identified
- Organizational changes
- Budget cycles
- Strategic initiatives alignment

### Churn Risk Indicators
- Declining engagement/usage
- Champion departure
- Unresolved issues
- Competitive activity
- Budget pressures
- Strategic shift away from your category

## Usage

Specify account and focus in `$ARGUMENTS`:

```
/taizen-gtm-skills:account-lifecycle plan Acme Corp
/taizen-gtm-skills:account-lifecycle renewal Acme Corp
/taizen-gtm-skills:account-lifecycle expansion Acme Corp
/taizen-gtm-skills:account-lifecycle health-check Acme Corp
```

## Output Format

### Account Plan
```
## Account Plan: [Company Name]

### Account Overview
| Attribute | Value |
|-----------|-------|
| Industry | [Industry] |
| Employees | [Count] |
| ARR | [Value] |
| Contract End | [Date] |
| Health Score | [Score/Status] |
| Account Tier | [Tier] |

### Executive Summary
[2-3 sentence overview of account status and priorities]

### Success Metrics
| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| [Metric] | [Target] | [Actual] | [Status] |

### Stakeholder Map
| Name | Role | Relationship | Priority Actions |
|------|------|--------------|------------------|
| [Name] | [Role] | [Strong/Medium/Weak] | [Action] |

### Strategic Objectives (12 months)
1. [Objective 1]: [Key results]
2. [Objective 2]: [Key results]
3. [Objective 3]: [Key results]

### 90-Day Priorities
| Priority | Owner | Due Date | Status |
|----------|-------|----------|--------|
| [Priority] | [Owner] | [Date] | [Status] |

### Risks & Mitigation
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk] | [H/M/L] | [H/M/L] | [Action] |

### Expansion Opportunities
| Opportunity | Value | Timeline | Next Step |
|-------------|-------|----------|-----------|
| [Opportunity] | [Value] | [Timeline] | [Action] |

### Key Meetings & Touchpoints
| Meeting | Frequency | Attendees | Purpose |
|---------|-----------|-----------|---------|
| [Meeting] | [Frequency] | [Who] | [Purpose] |
```

### Renewal Playbook
```
## Renewal Playbook: [Company Name]

### Renewal Overview
- **Renewal Date**: [Date]
- **Current ARR**: [Value]
- **Target Outcome**: [Renewal + expansion / Flat renewal / At-risk]
- **Days to Renewal**: [Days]

### Renewal Health Assessment
| Factor | Status | Notes |
|--------|--------|-------|
| Product Adoption | [Green/Yellow/Red] | [Details] |
| Stakeholder Relationships | [Green/Yellow/Red] | [Details] |
| Value Delivered | [Green/Yellow/Red] | [Details] |
| Competitive Threat | [Green/Yellow/Red] | [Details] |
| Budget/Priority | [Green/Yellow/Red] | [Details] |

### Value Story
[Summary of value delivered, ROI achieved, strategic impact]

### Renewal Strategy
- **Approach**: [Strategy]
- **Key Messages**: [What to emphasize]
- **Expansion Angle**: [If applicable]
- **Risk Mitigation**: [How to address concerns]

### Stakeholder Engagement Plan
| Stakeholder | Role in Renewal | Engagement Plan |
|-------------|-----------------|-----------------|
| [Name] | [Role] | [Plan] |

### Timeline & Actions
| Date | Action | Owner | Status |
|------|--------|-------|--------|
| [Date] | [Action] | [Owner] | [Status] |

### Negotiation Prep
- **Expected Asks**: [What they'll request]
- **Our Position**: [How we'll respond]
- **Walk-Away Point**: [Minimum acceptable terms]
- **BATNA**: [Our alternative if no deal]
```
