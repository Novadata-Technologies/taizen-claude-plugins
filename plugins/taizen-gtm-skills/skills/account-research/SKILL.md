---
name: account-research
description: Researches accounts, preps meeting briefs, maps buying committees, and runs health reviews. Use for account research, discovery prep, stakeholder mapping, or account health assessments.
---

# Account Research Skill

Comprehensive account intelligence for sales preparation and account management.

## Purpose

Provide actionable account intelligence to support sales preparation, stakeholder mapping, and ongoing account management.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# ACCOUNT RESEARCH DATA SOURCES
# Configure the sources relevant to your needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history
    - email_archives

# Company Intelligence
- source: linkedin
  connector: "{{LINKEDIN_SALES_NAVIGATOR | LINKEDIN}}"
  data:
    - company_profile
    - employee_data
    - recent_posts
    - job_openings
    - connections
- source: crunchbase
  enabled: true  # Funding, company data, news
- source: zoominfo
  connector: "{{ZOOMINFO}}"
  data:
    - company_data
    - org_chart
    - technographics
    - intent_signals
- source: clearbit
  connector: "{{CLEARBIT}}"
  data:
    - company_enrichment
    - technographics

# Company Website & News
- source: company_website
  url: "{{ACCOUNT_WEBSITE}}"
  pages:
    - about
    - leadership
    - careers
    - newsroom
    - blog
- source: news_search
  enabled: true  # Google News, press releases
- source: sec_filings
  enabled: true  # For public companies: 10-K, 10-Q, earnings calls

# CRM & Internal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - account_history
    - contact_records
    - opportunity_data
    - activity_history
    - previous_notes
    - related_accounts
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - previous_calls
    - key_topics
    - stakeholder_mentions
    - sentiment_analysis
- source: email_history
  connector: "{{GMAIL | OUTLOOK}}"
  data:
    - thread_history
    - engagement_patterns

# Internal Knowledge
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Sales/Account Plans/"
    - "/Customer Success/Account Notes/"
- source: support_tickets
  connector: "{{ZENDESK | INTERCOM | FRESHDESK}}"
  data:
    - ticket_history
    - satisfaction_scores
    - open_issues

# Social & Community
- source: twitter
  enabled: true  # Company and executive accounts
- source: glassdoor
  enabled: true  # Company culture, employee sentiment

# Intent & Signals
- source: intent_data
  connector: "{{BOMBORA | 6SENSE | DEMANDBASE}}"
  data:
    - topic_interest
    - buying_signals
    - competitor_research
```

### Output Destinations

```yaml
# Where to deliver account research outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Update CRM with research notes
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - update_account_notes
      - add_stakeholder_contacts
      - update_account_fields

  # Save to team docs
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales/Account Briefs/"

  # Share with team
  - type: slack
    connector: "{{SLACK}}"
    channel: "#account-updates"  # Or DM to account owner
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring account research tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Schedule an agent to research all my strategic accounts every Monday at 8am
and send the results to #strategic-accounts in Slack
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Pre-Meeting Preparation**:
```
Before any meeting with a prospect, automatically research the account and send
me a brief via Slack DM 24 hours before the meeting
```

**Weekly Account Updates**:
```
Every Monday morning, generate account briefs for Acme Corp, TechCorp, and
Stripe including recent news, trigger events, and stakeholder changes
```

**Account Health Monitoring**:
```
On the 1st of each month, run health checks on all accounts in my CRM with
ARR over $100k and alert me on Slack if any show risk signals
```

**New Account Research**:
```
Whenever a new account is created in Salesforce, automatically research the
company and populate the account fields with company intelligence
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Schedule Agent**: Describe your automation in natural language
4. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do
5. **Configure Outputs**: Specify where to deliver results (Slack, CRM, documents)

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Research account and generate brief" |
| `schedule` | When to run (cron or trigger) | "every Monday at 8am" or "before calendar events" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #channel, Google Drive folder" |
| `context` | Additional parameters | "account: Acme Corp" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "account-research"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

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

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Discovery Prep**
- "Research Acme Corp before my discovery call tomorrow"
- "Give me a full briefing on Stripe - I'm meeting their VP of Engineering"
- "What should I know about Nike before the QBR?"
- "I have a call with the CFO at TechCorp, what do I need to know?"

**Stakeholder Mapping**
- "Map the buying committee at Acme Corp"
- "Who are the key decision makers at Salesforce for a security product?"
- "Help me understand the org structure at Netflix - focus on their data team"
- "Who should I be talking to at IBM for an enterprise deal?"

**Account Health**
- "Give me a health check on our Acme Corp account"
- "What's the current state of our relationship with TechCorp?"
- "Are there any risk signals I should know about for Stripe?"
- "What expansion opportunities exist at our top 5 accounts?"

**Prospect Research**
- "Research Sarah Chen, VP of Product at Acme Corp - I'm reaching out cold"
- "Find me personalization hooks for the CTO at TechCorp"
- "What can you tell me about John Smith at IBM? Looking for warm intro paths"
- "Help me prepare for a meeting with the CMO - what do they care about?"

**Account Updates**
- "What's new with Acme Corp since our last call 2 weeks ago?"
- "Any recent news or changes at TechCorp I should know about?"
- "Pull the latest on our strategic accounts - looking for trigger events"

---

## Output Format

### Discovery Prep

```markdown
## Account Brief: [Company Name]

**Prepared for**: [Rep Name]
**Upcoming Meeting**: [Date, Attendees]
**Data Sources Used**: [CRM, LinkedIn, News, etc.]

---

### Company Overview
- **Industry**: [Industry]
- **Size**: [Employees] | **Revenue**: [Amount]
- **Headquarters**: [Location]
- **Founded**: [Year]
- **Description**: [What they do in 1-2 sentences]

### Strategic Priorities

Based on earnings calls, news, and job postings:

1. **[Priority 1]**: [Evidence/Source]
2. **[Priority 2]**: [Evidence/Source]
3. **[Priority 3]**: [Evidence/Source]

### Recent News & Trigger Events

| Date | Event | Relevance |
|------|-------|-----------|
| [Date] | [Event] | [Why it matters for your conversation] |

### Technology Landscape

- **Current Stack**: [Known technologies]
- **Recent Purchases**: [Any recent vendor changes]
- **Intent Signals**: [Topics they're researching - from intent data]

### Key Stakeholders

| Name | Title | LinkedIn | Notes |
|------|-------|----------|-------|
| [Name] | [Title] | [Link] | [Background, tenure, priorities] |

### Your History with This Account

*From CRM and call recordings:*
- **Previous Interactions**: [Summary]
- **Open Opportunities**: [If any]
- **Key Topics Discussed**: [From Gong/Chorus]
- **Last Contact**: [Date and context]

### Recommended Approach

Based on the research, consider:
- **Lead with**: [Topic that aligns with their priorities]
- **Avoid**: [Any sensitive areas]
- **Ask about**: [Relevant discovery questions]

### Discovery Questions

Tailored to this account:

1. [Question based on their priorities/situation]
2. [Question based on recent news/changes]
3. [Question based on industry challenges]
4. [Question to understand their current state]
5. [Question to uncover pain points]

### Competitive Considerations

- **Current Vendors**: [Known competitive products]
- **Competitive Intel**: [Any known preferences or relationships]
```

### Stakeholder Map

```markdown
## Buying Committee: [Company Name]

### Decision Map

```
                    ┌─────────────────┐
                    │ ECONOMIC BUYER  │
                    │ [Name, Title]   │
                    │ Budget approval │
                    └────────┬────────┘
                             │
         ┌───────────────────┼───────────────────┐
         │                   │                   │
┌────────▼────────┐ ┌────────▼────────┐ ┌────────▼────────┐
│ TECHNICAL BUYER │ │   USER BUYER    │ │   INFLUENCER    │
│ [Name, Title]   │ │ [Name, Title]   │ │ [Name, Title]   │
│ Evaluates fit   │ │ End user/champ  │ │ Advisor         │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

### Stakeholder Details

#### [Name] - Economic Buyer
- **Title**: [Title]
- **LinkedIn**: [Link]
- **Background**: [Career history, tenure]
- **Priorities**: [What they care about]
- **Our Relationship**: [Engagement history from CRM]
- **Approach**: [How to engage them]

#### [Name] - Technical Buyer
[Same format]

#### [Name] - Champion/User Buyer
[Same format]

### Influence Dynamics

- **Who influences whom**: [Relationships and dynamics]
- **Potential blockers**: [Who might oppose]
- **Unknown stakeholders**: [Roles we haven't identified yet]

### Engagement Strategy

| Stakeholder | Next Action | Owner | Timeline |
|-------------|-------------|-------|----------|
| [Name] | [Action] | [Rep] | [When] |
```

### Account Health

```markdown
## Account Health: [Company Name]

**Overall Health Score**: [🟢 Green / 🟡 Yellow / 🔴 Red]
**ARR**: [Amount] | **Contract Renewal**: [Date]

---

### Health Indicators

| Factor | Status | Evidence |
|--------|--------|----------|
| Champion Strength | 🟢/🟡/🔴 | [Details] |
| Executive Relationship | 🟢/🟡/🔴 | [Details] |
| Product Adoption | 🟢/🟡/🔴 | [Usage metrics] |
| Support Sentiment | 🟢/🟡/🔴 | [Ticket trends, CSAT] |
| Engagement Level | 🟢/🟡/🔴 | [Meeting frequency, responsiveness] |
| Competitive Threat | 🟢/🟡/🔴 | [Any competitive mentions] |

### Risk Factors

- [Risk 1]: [Details and evidence]
- [Risk 2]: [Details and evidence]

### Growth Opportunities

- [Opportunity 1]: [Expansion potential]
- [Opportunity 2]: [Upsell opportunity]

### Recommended Actions

| Priority | Action | Owner |
|----------|--------|-------|
| High | [Action] | [Who] |
| Medium | [Action] | [Who] |

### Recent Activity

*From CRM, Gong, and support:*
- [Date]: [Activity]
- [Date]: [Activity]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Pre-meeting briefs** - Automatically generate account briefs before scheduled meetings (via calendar integration)
2. **Trigger alerts** - Notify you when strategic accounts have news, leadership changes, or funding events
3. **CRM enrichment** - Automatically update CRM records with researched information
4. **Weekly account digests** - Summarize activity and changes across your accounts via Slack
