---
name: customer-research
description: Develops ICP definitions, buyer personas, jobs-to-be-done, voice of customer insights, and win/loss patterns. Use for audience research and customer understanding.
---

# Customer Research Skill

Deep customer understanding through structured research frameworks, powered by real customer data.

## Purpose

Build comprehensive customer intelligence that informs product, marketing, and sales strategies.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# CUSTOMER RESEARCH DATA SOURCES
# Configure the sources relevant to your research needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# CRM & Customer Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - customer_records
    - deal_history
    - win_loss_data
    - industry_segments
    - company_size_data
    - customer_lifecycle

# Product Usage & Analytics
- source: product_analytics
  connector: "{{MIXPANEL | AMPLITUDE | PENDO | HEAP}}"
  data:
    - user_behavior
    - feature_adoption
    - usage_patterns
    - cohort_analysis
    - retention_metrics

# Customer Feedback
- source: nps_surveys
  connector: "{{DELIGHTED | MEDALLIA | QUALTRICS | TYPEFORM}}"
  data:
    - nps_scores
    - survey_responses
    - feedback_themes
- source: review_sites
  sources:
    - g2
    - capterra
    - trustradius
  data:
    - customer_reviews
    - sentiment_analysis
    - competitive_mentions

# Conversation Intelligence
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - discovery_calls
    - win_loss_calls
    - objection_patterns
    - customer_language
    - competitive_mentions

# Support & Feedback
- source: support
  connector: "{{ZENDESK | INTERCOM | FRESHDESK}}"
  data:
    - ticket_themes
    - feature_requests
    - complaints
    - common_questions
- source: product_feedback
  connector: "{{PRODUCTBOARD | CANNY | USERVOICE}}"
  data:
    - feature_requests
    - voting_data
    - feedback_themes

# Customer Success
- source: customer_success
  connector: "{{GAINSIGHT | CHURNZERO | TOTANGO}}"
  data:
    - health_scores
    - churn_reasons
    - expansion_data
    - customer_segments

# Research Documents
- source: research_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Research/Customer Interviews/"
    - "/Research/Survey Results/"
    - "/Research/Personas/"
    - "/Research/ICP Documentation/"

# Marketing Intelligence
- source: marketing_analytics
  connector: "{{GOOGLE_ANALYTICS | HUBSPOT | MARKETO}}"
  data:
    - conversion_paths
    - content_engagement
    - lead_sources
    - attribution_data
```

### Output Destinations

```yaml
# Where to deliver customer research outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save research to knowledge base
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
    destination: "/Research/Customer Insights/"

  # Update CRM with ICP/persona data
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - update_segment_definitions
      - add_persona_tags

  # Share insights with team
  - type: slack
    connector: "{{SLACK}}"
    channel: "#customer-insights"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring customer research tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, aggregate voice of customer insights from NPS surveys,
G2 reviews, support tickets, and Gong calls to generate a monthly customer
insights report. Post to #customer-insights.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Voice of Customer Report**:
```
On the 1st of each month, aggregate VoC insights from NPS surveys, G2 reviews,
support tickets, and call recordings to generate a monthly customer insights
report. Share with #customer-insights.
```

**Weekly Feedback Digest**:
```
Every Monday at 8am, summarize customer feedback from the past week including
support themes, review trends, and call sentiment. Post a quick digest to
#customer-insights.
```

**Quarterly ICP Analysis**:
```
At the start of each quarter, analyze our customer data to validate and update
ICP definitions based on best customer characteristics and win patterns.
Update our ICP documentation and notify #product-marketing.
```

**Win/Loss Trend Analysis**:
```
On the 1st of each month, analyze last month's closed deals for win/loss
patterns by competitor, segment, and persona. Alert me if there are emerging
competitive threats or new loss patterns.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Data Sources**: Link your CRM, Gong, and feedback tools
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Aggregate VoC insights and generate monthly report" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when new review posted" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #customer-insights, Notion" |
| `focus` | Research focus area | "VoC", "ICP", "win/loss" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "customer-research"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Research Frameworks

### 1. Ideal Customer Profile (ICP)

Define the companies most likely to succeed with your product:

**Firmographic Criteria**
- Industry/vertical
- Company size (employees, revenue)
- Geography
- Growth stage
- Technology stack

**Behavioral Signals**
- Buying triggers and timing
- Current solutions in use
- Budget indicators
- Decision-making patterns

**Success Indicators**
- What makes customers successful
- Common characteristics of best customers
- Red flags and disqualifiers

### 2. Buyer Personas

**Persona Components**:

- **Demographics**: Title, role, reporting structure
- **Responsibilities**: Day-to-day, quarterly goals, KPIs
- **Challenges**: What keeps them up at night
- **Goals**: Professional and personal aspirations
- **Buying Behavior**: How they research, evaluate, decide
- **Objections**: Common concerns and hesitations
- **Channels**: Where they get information
- **Influences**: Who they trust and listen to

### 3. Jobs to Be Done (JTBD)

**Job Statement Format**:
When [situation], I want to [motivation], so I can [expected outcome].

**Job Layers**:
- Functional job (practical task)
- Emotional job (how they want to feel)
- Social job (how they want to be perceived)

**Forces of Progress**:
- Push: Pain with current solution
- Pull: Attraction to new solution
- Anxiety: Fear of change
- Habit: Comfort with status quo

### 4. Voice of Customer (VoC)

**Sources**:
- Customer interviews
- Support tickets and feedback
- Reviews (G2, Capterra, etc.)
- Sales call recordings
- NPS and survey responses
- Social media and community

**Analysis Framework**:
- Themes and patterns
- Language and terminology used
- Emotional indicators
- Feature requests and gaps
- Competitive mentions

### 5. Win/Loss Insights

**Win Analysis**:
- Why did they choose us?
- What was the decisive factor?
- Who championed us internally?
- What would have lost the deal?

**Loss Analysis**:
- Why did we lose?
- Who won and why?
- What could we have done differently?
- Was it ever winnable?

---

## How to Use This Skill

Invoke with natural language describing the research you need:

**ICP Development**
- "Define our ideal customer profile based on our best customers"
- "Analyze our customer data to identify ICP patterns"
- "What characteristics do our most successful customers share?"
- "Build an ICP for our enterprise segment"

**Persona Research**
- "Create a buyer persona for VP of Sales"
- "What do we know about how CHROs buy software?"
- "Develop personas for our top 3 buyer types"
- "Update our CMO persona with recent interview data"

**Jobs to Be Done**
- "What jobs are our customers hiring us to do?"
- "Analyze the jobs to be done for our scheduling feature"
- "Map the forces of progress for switching from our competitor"

**Voice of Customer**
- "What are customers saying about our product?"
- "Analyze the themes from our recent NPS responses"
- "What language do customers use to describe their problems?"
- "Pull voice of customer insights for our messaging update"

**Win/Loss Analysis**
- "Why are we winning deals against Competitor X?"
- "Analyze our lost deals this quarter - what patterns do you see?"
- "What factors predict deal success?"
- "Review our win/loss data for enterprise deals"

---

## Output Format

### ICP Definition

```markdown
# Ideal Customer Profile: [Product/Segment]

**Created**: [Date]
**Data Sources Used**: [CRM analysis, customer success data, win/loss, etc.]

---

## Summary

*Based on analysis of [X] customers and [Y] deals:*

[2-3 sentence summary of the ideal customer]

---

## Firmographics

| Attribute | Ideal | Acceptable | Disqualifier |
|-----------|-------|------------|--------------|
| Industry | [Ideal industries] | [OK to pursue] | [Avoid] |
| Employee Count | [Range] | [Range] | [Outside this] |
| Revenue | [Range] | [Range] | [Outside this] |
| Geography | [Regions] | [Regions] | [Regions to avoid] |
| Growth Stage | [Stage] | [Stages] | [Stages to avoid] |

## Behavioral Signals

### Buying Triggers
*From win analysis and call recordings:*
- **[Trigger 1]**: [How to identify - data points]
- **[Trigger 2]**: [How to identify]
- **[Trigger 3]**: [How to identify]

### Technology Indicators
*From technographics and deal data:*
- **Must Have**: [Technologies that correlate with success]
- **Nice to Have**: [Good signals]
- **Red Flag**: [Technologies that predict churn]

### Intent Signals
- [Signal 1]: [What it means]
- [Signal 2]: [What it means]

## Success Indicators

### Best Customer Characteristics
*From customer success data and product usage:*
1. **[Characteristic 1]**: [Evidence - X% of top customers have this]
2. **[Characteristic 2]**: [Evidence]
3. **[Characteristic 3]**: [Evidence]

### Warning Signs
*From churn analysis:*
- **[Red flag 1]**: [Correlation with churn]
- **[Red flag 2]**: [Correlation with churn]

## Scoring Model

| Criteria | Weight | 3 Points | 2 Points | 1 Point | 0 Points |
|----------|--------|----------|----------|---------|----------|
| [Criteria 1] | [%] | [Ideal] | [Good] | [OK] | [Poor] |
| [Criteria 2] | [%] | [Ideal] | [Good] | [OK] | [Poor] |
| [Criteria 3] | [%] | [Ideal] | [Good] | [OK] | [Poor] |

**Tier A (Prioritize)**: Score 80+
**Tier B (Pursue)**: Score 60-79
**Tier C (Opportunistic)**: Score 40-59
**Disqualify**: Score <40

## Validation Data

- **Analysis based on**: [X] customers over [time period]
- **Win rate for Tier A**: [%]
- **Average deal size for Tier A**: [$]
- **Retention rate for Tier A**: [%]
```

### Buyer Persona

```markdown
# Buyer Persona: [Name/Title]

**Created**: [Date]
**Data Sources Used**: [Interviews, Gong calls, surveys, etc.]

---

## Quick Profile

| Attribute | Details |
|-----------|---------|
| Common Titles | [Titles] |
| Reports To | [Typical reporting] |
| Team Size | [Range] |
| Experience | [Years in role] |
| Role in Purchase | [Decision maker/Influencer/User] |

## Representative Quote

*From customer interviews:*
> "[Quote that captures their mindset]"

---

## Day in the Life

### Primary Responsibilities
*From job postings, interviews, and call recordings:*
- [Key responsibility 1]
- [Key responsibility 2]
- [Key responsibility 3]

### Success Metrics
*What they're measured on:*
- [Metric 1]
- [Metric 2]
- [Metric 3]

### Tools They Use Daily
- **[Category]**: [Common tools]
- **[Category]**: [Common tools]

---

## Psychology

### Goals & Aspirations
- **Professional**: [Career goals - from interviews]
- **Personal**: [Personal motivations]

### Challenges & Pain Points
*From VoC analysis:*
1. **[Challenge 1]**: [Impact on their work]
   - Voice of customer: "[Actual quote]"
2. **[Challenge 2]**: [Impact]
   - Voice of customer: "[Actual quote]"
3. **[Challenge 3]**: [Impact]

### Fears & Anxieties
- **[Fear 1]**: [How it manifests in buying behavior]
- **[Fear 2]**: [How it manifests]

---

## Buying Behavior

### Information Sources
*From marketing analytics and interviews:*
- [Where they research - with data on engagement]
- [Who they trust]

### Decision Criteria
*From win/loss analysis:*
1. **[Criterion 1]**: [Importance level]
2. **[Criterion 2]**: [Importance level]
3. **[Criterion 3]**: [Importance level]

### Common Objections
*From Gong analysis:*

| Objection | Frequency | Root Cause | Response |
|-----------|-----------|------------|----------|
| "[Objection]" | [% of deals] | [Why they say this] | [How to address] |

---

## Messaging That Resonates

### Language They Use
*From call recordings and reviews:*
- [Term they use]
- [How they describe the problem]

### Do Say
- [Message that works - with evidence]

### Don't Say
- [What doesn't resonate - with evidence]

---

## Engagement Strategy

### Best Channels
*From marketing analytics:*
- **[Channel 1]**: [Engagement data]
- **[Channel 2]**: [Engagement data]

### Content Preferences
*From content engagement:*
- [Format 1]: [Performance data]
- [Format 2]: [Performance data]

### Conversation Starters
- [Topic that resonates]
- [Topic that resonates]
```

### Voice of Customer Report

```markdown
# Voice of Customer Report: [Topic/Product Area]

**Created**: [Date]
**Data Sources Used**: [G2, NPS, Support, Gong, etc.]

---

## Summary

Analysis of [X] data points across [sources]:
[Key findings in 2-3 sentences]

---

## Theme Analysis

### Theme 1: [Theme Name]

**Mentions**: [Count] ([%] of total)
**Sentiment**: [Positive/Neutral/Negative]

**Representative Quotes**:
> "[Quote 1]" - [Source]
> "[Quote 2]" - [Source]

**Implications**:
- [What this means for product]
- [What this means for messaging]

### Theme 2: [Theme Name]
[Same format]

### Theme 3: [Theme Name]
[Same format]

---

## Competitive Mentions

| Competitor | Mentions | Context | Our Opportunity |
|------------|----------|---------|-----------------|
| [Competitor] | [Count] | [What they say] | [How to respond] |

---

## Language Patterns

### Words Customers Use
- "[Word/phrase]" - [frequency]
- "[Word/phrase]" - [frequency]

### Recommended Messaging Updates
Based on VoC, consider:
- [Recommendation 1]
- [Recommendation 2]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Automated ICP refresh** - Regularly analyze customer data to update ICP definitions
2. **VoC monitoring** - Continuously aggregate customer feedback across sources
3. **Win/loss triggers** - Auto-generate analysis when deals close
4. **Persona updates** - Flag when new data suggests persona updates are needed
5. **Competitive tracking** - Monitor competitive mentions in customer feedback
