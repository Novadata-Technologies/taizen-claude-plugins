---
name: competitive-intelligence
description: Produces competitor analysis, battlecards, comparison pages, and competitive positioning. Use for competitive research, sales enablement, or marketing content.
---

# Competitive Intelligence Skill

Comprehensive competitive analysis and sales enablement materials.

## Purpose

Equip teams with actionable competitive intelligence to win more deals and create compelling differentiation.

---

## Required Integrations

Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations.

### Data Sources

```yaml
# COMPETITIVE DATA SOURCES
# Uncomment and configure the sources you want to use

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history
    - email_archives

# Review & Comparison Sites
- source: g2
  enabled: true
- source: capterra
  enabled: true
- source: trustradius
  enabled: true
- source: gartner_peer_insights
  enabled: false

# Market Intelligence
- source: crunchbase
  enabled: true
- source: pitchbook
  enabled: false
- source: owler
  enabled: true

# Web & Content
- source: competitor_websites
  urls:
    - "{{COMPETITOR_1_URL}}"
    - "{{COMPETITOR_2_URL}}"
    - "{{COMPETITOR_3_URL}}"
- source: web_search
  enabled: true

# Social & Community
- source: linkedin
  enabled: true
- source: twitter
  enabled: true
- source: reddit
  subreddits:
    - "{{RELEVANT_SUBREDDIT_1}}"
    - "{{RELEVANT_SUBREDDIT_2}}"

# Internal Sources
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Competitive Intel/"
    - "/Sales Enablement/Battlecards/"
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - win_loss_notes
    - competitive_mentions
    - deal_outcomes_by_competitor
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - competitive_mentions
    - objection_patterns
    - win_loss_call_analysis

# News & SEC Filings
- source: sec_filings
  enabled: true
- source: news_feeds
  enabled: true
```

### Your Competitor List

```yaml
competitors:
  - name: "{{COMPETITOR_1_NAME}}"
    website: "{{COMPETITOR_1_URL}}"
    priority: primary
  - name: "{{COMPETITOR_2_NAME}}"
    website: "{{COMPETITOR_2_URL}}"
    priority: primary
  - name: "{{COMPETITOR_3_NAME}}"
    website: "{{COMPETITOR_3_URL}}"
    priority: secondary
```

### Output Destinations

```yaml
outputs:
  - type: display
    enabled: true

  - type: knowledge_base
    connector: "{{NOTION | CONFLUENCE | SLITE | GURU}}"
    destination: "/Competitive Intelligence/"

  - type: slack
    connector: "{{SLACK}}"
    channel: "#competitive-intel"

  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - update_competitor_field
      - add_competitive_notes
```

---

## Instructions for Claude

> **IMPORTANT**: Before executing this skill, you MUST validate the configuration above.

### Pre-Execution Checklist

1. **Check for placeholder values**: Scan the YAML configuration for any `{{...}}` placeholders. These indicate required configuration that the user must provide.

2. **Validate data sources**: For each data source with `enabled: true` or a `connector` field:
   - Verify the corresponding MCP server is connected and available
   - If a connector shows `{{OPTIONS}}`, ask the user which option they use
   - If paths or URLs contain `{{PLACEHOLDER}}`, ask the user to provide the actual values

3. **Validate competitor list**: The `competitors` section must have at least one competitor with actual values (not placeholders) before proceeding with competitive analysis.

4. **Validate output destinations**: For any output type beyond `display`, verify:
   - The connector is available as an MCP server
   - The destination path/channel is configured (not a placeholder)

### If Configuration is Incomplete

**Do not proceed with the skill.** Instead:

1. List the specific missing or placeholder values found
2. Explain what each value is needed for
3. Ask the user to provide the missing configuration
4. Offer to help them set up the required MCP integrations

**Example response when config is incomplete:**
```
I found some configuration that needs to be completed before I can run this skill:

**Missing competitor information:**
- COMPETITOR_1_NAME, COMPETITOR_1_URL (required for primary competitor analysis)

**Unconfigured data sources:**
- CRM connector: Which do you use - Salesforce or HubSpot?
- Internal docs path: Where are your competitive intel docs stored?

**Output destinations:**
- Slack channel: What channel should I post competitive alerts to?

Please provide these values, or let me know if you'd like to skip certain data sources for now.
```

### Minimum Requirements

At minimum, this skill requires:
- At least one competitor name (can use web search for public info)
- `display` output enabled (always available)

Enhanced functionality requires:
- CRM connection for win/loss data
- Call recording integration for competitive mentions
- Internal docs access for existing battlecards

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring competitive intelligence tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Monitor all my competitors for news, funding, and product launches daily
and alert me in #competitive-intel when something significant happens
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Daily Competitor Monitoring**:
```
Every morning at 8am, check for new announcements from Competitor X, Y, and Z
including funding rounds, product launches, and leadership changes. Alert me
on Slack if anything significant happens.
```

**Weekly Competitive Digest**:
```
Every Monday, generate a competitive digest covering all primary competitors
with recent news, product updates, G2 review trends, and market positioning
changes. Send to #competitive-intel and save to our Notion wiki.
```

**Quarterly Battlecard Refresh**:
```
At the start of each quarter, update all our competitive battlecards with the
latest intelligence from G2 reviews, news, and our win/loss data. Notify the
sales enablement team when complete.
```

**Win/Loss Analysis**:
```
On the 1st of each month, analyze competitive patterns from our CRM win/loss
data and update our positioning recommendations accordingly.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Schedule Agent**: Describe your automation in natural language
4. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do
5. **Configure Outputs**: Specify where to deliver results (Slack, Notion, CRM)

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Monitor competitors for news and product launches" |
| `schedule` | When to run (cron or trigger) | "daily at 8am" or "every Monday" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #competitive-intel, Notion wiki" |
| `competitors` | Which competitors to monitor | "Competitor X, Y, Z" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "competitive-intelligence"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Competitive Analysis Framework

### 1. Competitor Overview

For each competitor, analyze:

**Company Profile**
- Founded, funding, size, growth trajectory
- Target market and positioning
- Recent news, acquisitions, pivots

**Product Analysis**
- Core capabilities and features
- Pricing model and packaging
- Technology and integrations
- Roadmap direction (if known)

**GTM Strategy**
- Sales motion (self-serve, sales-led, hybrid)
- Marketing approach and channels
- Key messages and positioning
- Customer segments they target

**Strengths & Weaknesses**
- Where they win (and why)
- Where they lose (and why)
- Customer complaints and churn reasons

### 2. Battlecard Framework

```
┌─────────────────────────────────────────┐
│ COMPETITOR: [Name]                      │
│ Last Updated: [Date]                    │
├─────────────────────────────────────────┤
│ QUICK HITS                              │
│ • Founded: [Year] | HQ: [Location]      │
│ • Funding: [Amount] | Employees: [#]    │
│ • Target: [Market segment]              │
├─────────────────────────────────────────┤
│ POSITIONING                             │
│ How they position: [Their message]      │
│ Our counter: [Our differentiation]      │
├─────────────────────────────────────────┤
│ LANDMINES (Questions to ask)            │
│ • [Question that exposes their weakness]│
├─────────────────────────────────────────┤
│ STRENGTHS TO ACKNOWLEDGE                │
│ • [Strength] → [How we neutralize]      │
├─────────────────────────────────────────┤
│ WEAKNESSES TO EXPLOIT                   │
│ • [Weakness] → [Proof point]            │
├─────────────────────────────────────────┤
│ WIN THEMES                              │
│ • [Why customers choose us over them]   │
└─────────────────────────────────────────┘
```

### 3. Comparison Matrix

| Capability | Us | Competitor A | Competitor B |
|------------|-----|--------------|--------------|
| [Feature] | ✓ | Partial | ✗ |

---

## Deliverable Types

- **Sales Battlecard** - One-page quick reference for sales conversations
- **Marketing Comparison Page** - Web content for "vs" or "alternative to" pages
- **Competitive Brief** - Deep-dive analysis for strategy and product teams
- **Win/Loss Competitive Analysis** - Pattern analysis from deals won and lost
- **Competitive Alert** - Notification when competitor makes major moves

---

## How to Use This Skill

Invoke with natural language:

**Battlecards**
- "Create a battlecard for Salesforce"
- "I need a quick competitive summary for my call with Acme - they're also looking at HubSpot"
- "Build me a battlecard comparing us to Zendesk, focus on enterprise features"

**Competitive Analysis**
- "What's the latest on Competitor X? Any recent funding or product news?"
- "Analyze Gong's positioning and how we should differentiate"
- "Deep dive on Monday.com - I need to understand their pricing and target market"

**Comparison Content**
- "Create a comparison page: us vs Asana for project management"
- "Help me write an 'alternative to Notion' landing page"
- "Build a feature comparison matrix for our top 3 competitors"

**Landscape Overview**
- "Give me an overview of the CRM competitive landscape"
- "Who are the main players in our space and how do they position?"

**Win/Loss Analysis**
- "Analyze our win/loss data against Competitor X from the last quarter"
- "Why are we losing deals to HubSpot? Pull insights from Gong calls and CRM notes"

---

## Output Format

### Battlecard Output

```markdown
# Battlecard: [Competitor Name]

**Confidence Level**: [High/Medium/Low]
**Last Updated**: [Date]
**Data Sources Used**: [List sources]

---

## At a Glance

| Attribute | Details |
|-----------|---------|
| Founded | [Year] |
| Headquarters | [Location] |
| Funding/Revenue | [Amount] |
| Employees | [Count] |
| Key Customers | [Names] |

## Their Positioning

**Tagline**: [Their tagline]
**Core Message**: [How they position]
**Target Buyer**: [Who they sell to]

## Our Differentiation

**When competing against [Competitor], lead with**:
1. [Key differentiator 1]
2. [Key differentiator 2]
3. [Key differentiator 3]

## Discovery Landmines

| Question | Why It Helps |
|----------|--------------|
| "[Question]" | [Exposes this weakness] |

## Feature Comparison

| Capability | Us | [Competitor] | Notes |
|------------|-----|--------------|-------|
| [Feature] | ✓ | ✗ | [Context] |

## Their Strengths (Acknowledge & Neutralize)

| Strength | Our Response |
|----------|--------------|
| [Strength] | [How we address] |

## Their Weaknesses (Exploit)

| Weakness | Our Advantage | Proof Point |
|----------|---------------|-------------|
| [Weakness] | [Our strength] | [Evidence] |

## What Customers Say

**Positive about them**:
- "[Quote from G2/Capterra]"

**Negative about them**:
- "[Quote from G2/Capterra]"

## Win/Loss Insights

- **Why we win**: [Pattern from won deals]
- **Why we lose**: [Pattern from lost deals]
- **Key objections**: [Common objections]

## Common Objections

| Objection | Response |
|-----------|----------|
| "They have [feature]" | [How we respond] |

## Win Stories

**[Customer Name]**: [Why they chose us over competitor]
```

### Comparison Page Output

```markdown
# [Your Product] vs [Competitor]: [Year] Comparison

## Overview
[2-3 paragraph comparison overview]

## Quick Comparison

| | [Your Product] | [Competitor] |
|--|----------------|--------------|
| Best For | [Use case] | [Use case] |
| Pricing | [Model] | [Model] |
| Key Strength | [Strength] | [Strength] |

## Detailed Comparison

### [Category 1]
[Your approach vs their approach]

### [Category 2]
[Your approach vs their approach]

## When to Choose [Your Product]
- [Scenario 1]
- [Scenario 2]

## When [Competitor] Might Be Better
[Honest assessment - builds credibility]

## The Bottom Line
[Summary recommendation]
```
