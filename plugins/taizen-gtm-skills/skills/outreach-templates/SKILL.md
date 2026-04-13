---
name: outreach-templates
description: Generates personalized outreach sequences for cold, warm, event-based, re-engagement, and executive contexts. Use when creating prospecting emails or sequences.
---

# Outreach Templates Skill

Generate personalized, high-converting outreach for any sales context.

## Purpose

Create compelling, personalized outreach that drives engagement across different scenarios and buyer stages.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# OUTREACH TEMPLATES DATA SOURCES
# Configure the sources relevant to your outreach needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Prospect Research
- source: linkedin
  connector: "{{LINKEDIN_SALES_NAVIGATOR | LINKEDIN}}"
  data:
    - prospect_profiles
    - recent_activity
    - shared_connections
    - company_news

# CRM Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - lead_records
    - account_data
    - engagement_history
    - past_outreach

# Enrichment Data
- source: enrichment
  connector: "{{ZOOMINFO | CLEARBIT | APOLLO}}"
  data:
    - contact_data
    - company_data
    - technographics
    - intent_signals

# Sales Engagement
- source: sales_engagement
  connector: "{{OUTREACH | SALESLOFT | APOLLO}}"
  data:
    - sequence_performance
    - email_analytics
    - best_performing_templates

# Messaging Guidelines
- source: messaging_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Sales Enablement/Email Templates/"
    - "/Marketing/Value Propositions/"
```

### Output Destinations

```yaml
# Where to deliver outreach outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Push to sales engagement platform
  - type: sales_engagement
    connector: "{{OUTREACH | SALESLOFT}}"
    action: create_sequence

  # Save templates
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales Enablement/Outreach Templates/"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule outreach optimization tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every Monday at 9am, analyze outreach performance from last week, identify
top performing templates, and suggest improvements. Post findings to
#sales-enablement.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Weekly Performance Review**:
```
Every Monday at 9am, analyze outreach performance from last week, identify
top performers, and suggest template improvements. Post to #sales-enablement
and save to our Outreach Analytics folder.
```

**Event Follow-Up Generator**:
```
When we attend an event, automatically generate personalized follow-up
sequences for the attendees. Create the sequences in Outreach and DM the
BDR owner.
```

**Monthly Template Refresh**:
```
On the 1st of each month, review and refresh outreach templates based on
performance data and messaging updates. Save to our Templates folder and
notify #sales-enablement.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Sales Engagement**: Link your Outreach or SalesLoft
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Analyze outreach performance and suggest improvements" |
| `schedule` | When to run (cron or trigger) | "every Monday at 9am" or "when event attended" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #sales-enablement, Outreach sequences" |
| `outreach_type` | Type of outreach | "cold", "event follow-up", "re-engagement" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "outreach-templates"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Outreach Types

### 1. BDR Cold Outreach

Initial outreach to new prospects with no prior engagement:

**Structure**:
- **Hook**: Personalized opening that demonstrates research
- **Problem**: Articulate a relevant challenge they likely face
- **Insight**: Share a perspective or data point that adds value
- **Bridge**: Connect the problem to your solution (light touch)
- **CTA**: Clear, low-friction ask

**Best Practices**:
- Keep under 100 words
- One clear CTA
- No attachments on first touch
- Personalize beyond [First Name]

### 2. BDR Event Follow-Up

Follow-up after events, webinars, or content engagement:

**Structure**:
- **Reference**: Specific mention of the event/content
- **Value Add**: Additional insight related to the event topic
- **Connection**: How your solution relates to their interest
- **CTA**: Offer to continue the conversation

### 3. Warm & Re-Engagement

Reaching out to warm leads or re-engaging dormant contacts:

**Structure**:
- **Context**: Reference previous interaction or relationship
- **Update**: What's new or changed since last contact
- **Relevance**: Why reaching out now makes sense
- **CTA**: Rekindle the conversation

### 4. Executive Outreach

High-touch outreach to senior executives:

**Structure**:
- **Credibility**: Establish relevance quickly (referral, peer company, insight)
- **Strategic Frame**: Business-level challenge or opportunity
- **Proof Point**: Brief evidence of impact with similar executives
- **Ask**: Executive-appropriate request (brief call, peer introduction)

**Best Practices**:
- Maximum 75 words
- Lead with business impact, not product
- Reference peer companies or executives
- Respect their time in the CTA

### 5. Post-Event Follow-Up

Follow-up after meetings, demos, or significant interactions:

**Structure**:
- **Thank You**: Acknowledge their time
- **Recap**: Key points discussed or agreed upon
- **Next Steps**: Clear action items with owners
- **Value Add**: Additional resource or insight

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Cold Outreach**
- "Write a cold email to the VP of Sales at TechCorp"
- "Create a 3-email cold sequence for fintech CFOs"

**Event Follow-Up**
- "Generate follow-up for prospects who attended our webinar"
- "Create post-conference outreach for booth visitors"

**Re-Engagement**
- "Re-engage this dormant lead: [context]"
- "Write a re-engagement sequence for closed-lost opportunities"

**Executive Outreach**
- "Create executive outreach for the CTO at Nike"
- "Write a referral-based email to the CHRO"

---

## Output Format

```markdown
## Outreach: [Type] - [Prospect/Company]

**Created**: [Date]
**Data Sources Used**: [LinkedIn, CRM, enrichment, etc.]

---

### Subject Line Options
1. [Option 1]
2. [Option 2]
3. [Option 3]

### Email Body

[Full email text]

### Follow-Up Sequence

**Day 3 - Follow-Up 1:**
[Brief follow-up]

**Day 7 - Follow-Up 2:**
[Value-add follow-up]

**Day 14 - Break-Up:**
[Final attempt with clear close]

### LinkedIn Touch (Optional)
[Connection request or InMail text]

### Personalization Notes
- [Specific element to customize]
- [Research point to incorporate]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Sequence generation** - Create multi-touch sequences based on persona
2. **Performance optimization** - Suggest improvements based on analytics
3. **Event automation** - Auto-generate follow-ups for event attendees
4. **Personalization at scale** - Pull prospect data to personalize templates
