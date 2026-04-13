---
description: Researches accounts, preps meeting briefs, maps buying committees, and runs health reviews. Use for account research, discovery prep, stakeholder mapping, or account health assessments.
---

# Account Research Skill

Comprehensive account intelligence for sales preparation and account management.

## Purpose

Provide actionable account intelligence to support sales preparation, stakeholder mapping, and ongoing account management.

## Research Modes

### 1. Account Research & Discovery Prep

Deep-dive research for initial account engagement:

- **Company Overview**: Size, industry, locations, recent news
- **Business Priorities**: Strategic initiatives, challenges, growth areas
- **Technology Landscape**: Current vendors, tech stack, recent purchases
- **Financial Health**: Revenue trends, profitability, investments
- **Leadership**: Key executives, recent changes, backgrounds
- **Trigger Events**: M&A, leadership changes, expansions, earnings

### 2. Multi-Stakeholder Account Map

Map the buying committee and influence network:

- **Economic Buyer**: Budget authority and approval power
- **Technical Buyer**: Evaluates capabilities and fit
- **User Buyer**: Day-to-day users and champions
- **Coach**: Internal advocate who guides the sale
- **Influencers**: Others who impact the decision
- **Blockers**: Potential opponents or skeptics

### 3. Account Health Snapshot

Assess current account status and engagement:

- **Relationship Health**: Champion strength, executive access, breadth of relationships
- **Product Adoption**: Usage metrics, feature adoption, expansion opportunities
- **Risk Indicators**: Engagement decline, competitive threats, contract concerns
- **Growth Potential**: Whitespace, expansion triggers, upsell opportunities
- **Action Items**: Recommended next steps

### 4. Personalized Prospecting Research

Individual stakeholder research for outreach:

- **Professional Background**: Current role, career history, tenure
- **Priorities**: What they're focused on based on role and company context
- **Connections**: Shared connections, common interests, warm intro paths
- **Communication Style**: Preferred channels, engagement history
- **Personalization Hooks**: Recent posts, talks, publications, interests

## Usage

Specify research mode and account in `$ARGUMENTS`:

```
/taizen-gtm-skills:account-research discovery Acme Corp
/taizen-gtm-skills:account-research stakeholder-map Acme Corp
/taizen-gtm-skills:account-research health-check Acme Corp
/taizen-gtm-skills:account-research prospect Jane Smith, VP HR at Acme
```

## Output Format

### Discovery Prep
```
## Account Brief: [Company Name]

### Company Overview
- Industry: [Industry]
- Size: [Employees / Revenue]
- HQ: [Location]
- Key Facts: [Notable information]

### Strategic Priorities
1. [Priority 1]: [Evidence/Source]
2. [Priority 2]: [Evidence/Source]

### Key Stakeholders
| Name | Title | Relevance | Notes |
|------|-------|-----------|-------|
| [Name] | [Title] | [Why important] | [Background] |

### Trigger Events
- [Event 1]: [Date] - [Relevance]
- [Event 2]: [Date] - [Relevance]

### Competitive Landscape
- Current vendors: [List]
- Recent purchases: [List]

### Recommended Approach
[Strategy for engaging this account]

### Discovery Questions
1. [Question 1]
2. [Question 2]
3. [Question 3]
```
