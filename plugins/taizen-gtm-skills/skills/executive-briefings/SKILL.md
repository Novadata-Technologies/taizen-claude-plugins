---
name: executive-briefings
description: Preparation materials for C-level meetings, executive events, and advisory boards. Includes profiles, talking points, and strategic framing.
---

# Executive Briefings Skill

Prepare for high-stakes executive interactions with comprehensive briefing materials.

## Purpose

Ensure every executive interaction is impactful, builds relationship equity, and advances strategic objectives.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# EXECUTIVE BRIEFINGS DATA SOURCES
# Configure the sources relevant to your executive engagement needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# Executive Intelligence
- source: linkedin
  connector: "{{LINKEDIN_SALES_NAVIGATOR | LINKEDIN}}"
  data:
    - executive_profiles
    - career_history
    - recent_posts
    - connections
    - speaking_engagements

# Company Intelligence
- source: company_research
  sources:
    - crunchbase
    - news_search
    - sec_filings
  data:
    - company_news
    - earnings_calls
    - strategic_initiatives

# CRM & Relationship Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - account_history
    - executive_contacts
    - previous_interactions
    - open_opportunities
    - relationship_notes

# Call History
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - previous_executive_calls
    - key_topics
    - commitments_made
    - sentiment

# Calendar Context
- source: calendar
  connector: "{{GOOGLE_CALENDAR | OUTLOOK_CALENDAR}}"
  data:
    - meeting_details
    - attendees
    - agenda

# Internal Strategy Docs
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Sales/Strategic Accounts/"
    - "/Sales/Executive Engagement/"
    - "/Customer Success/Executive Sponsors/"
```

### Output Destinations

```yaml
# Where to deliver executive briefing outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to account folder
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales/Executive Briefings/"

  # Update CRM with notes
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - log_meeting_prep
      - update_contact_intel

  # Send brief before meeting
  - type: email
    connector: "{{GMAIL | OUTLOOK}}"
    action: draft_to_self
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule automated executive briefing preparation with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
48 hours before any meeting with a C-level or VP executive on my calendar,
automatically generate a comprehensive executive briefing including their
profile, company context, and relationship history. DM me on Slack.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Executive Meeting Auto-Prep**:
```
48 hours before any meeting with a CEO, CFO, CTO, CMO, or VP on my calendar,
automatically generate an executive briefing including their profile, company
context, relationship history, and recommended approach. Send it via Slack DM.
```

**QBR Executive Prep**:
```
When a QBR is scheduled, generate an executive briefing with relationship
history, account health, strategic talking points, and expansion opportunities.
Send to the CSM and save to our QBR Materials folder.
```

**Weekly Executive Engagement Summary**:
```
Every Monday at 8am, summarize all upcoming executive meetings this week
with key context and preparation priorities. Post to #executive-engagement.
```

**Post-Meeting Follow-Up**:
```
After any meeting with an executive ends, generate a follow-up email draft
and suggest CRM updates based on the meeting context. DM the meeting owner.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Calendar**: Link your Google Calendar or Outlook
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Generate executive briefing with profile and approach" |
| `schedule` | When to run (cron or trigger) | "48 hours before calendar events with VPs" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack DM, Google Drive" |
| `executive_levels` | Which titles to trigger on | "CEO, CFO, CTO, VP" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "executive-briefings"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Engagement Types

### 1. Executive Briefing Document

One-on-one or small group meetings with senior executives:

**Components**:
- **Executive Profile**: Background, priorities, communication style
- **Relationship History**: Previous interactions, agreements, open items
- **Business Context**: Their current challenges and strategic initiatives
- **Meeting Objectives**: What we want to achieve
- **Key Messages**: 2-3 points to land
- **Anticipated Questions**: What they'll likely ask
- **Ask/Commitment**: What we want from them

### 2. Event Talk Track

Sponsored events, dinners, or executive gatherings:

**Components**:
- **Event Context**: Format, attendees, your role
- **Conversation Starters**: Industry-relevant opening topics
- **Key Talking Points**: Messages to weave in naturally
- **Attendee Briefs**: Quick profiles of key attendees
- **Relationship Goals**: Connections to strengthen or create
- **Follow-Up Plan**: How to capitalize on the event

### 3. Executive Advisory Board Prep

Customer advisory boards and executive councils:

**Components**:
- **Board Composition**: Who's attending and their perspectives
- **Agenda & Objectives**: What the session aims to accomplish
- **Discussion Guide**: Questions to drive valuable dialogue
- **Input Needed**: Specific feedback or guidance sought
- **Sensitive Topics**: What to avoid or handle carefully
- **Action Planning**: How insights will be used

---

## Executive Communication Principles

**Do**:
- Lead with business impact, not features
- Use their time efficiently
- Bring an informed point of view
- Ask for something specific
- Follow up promptly

**Don't**:
- Waste time with basics they already know
- Read from slides
- Oversell or overpromise
- Ignore their questions to stick to script
- Leave without clear next steps

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Executive Meetings**
- "Prepare me for my meeting with the CFO at Acme Corp tomorrow"
- "Executive briefing for Sarah Chen, CHRO at TechCorp"
- "Help me prep for a call with the CEO of Nike"

**Event Prep**
- "Prepare talk tracks for the executive dinner at the conference"
- "Who should I prioritize at the industry event next week?"
- "Generate conversation starters for the CEO roundtable"

**Advisory Boards**
- "Help me prepare for our customer advisory board meeting"
- "Generate discussion guide for the executive council session"

**Follow-Up**
- "Help me draft a follow-up email to the CTO after our meeting"
- "What should I send to the executives I met at the event?"

---

## Output Format

### Executive Briefing

```markdown
## Executive Briefing: [Name], [Title] - [Company]

**Created**: [Date]
**Data Sources Used**: [LinkedIn, CRM, News, Gong, etc.]

---

### Executive Profile
- **Background**: [Career history, education, notable achievements]
- **Tenure**: [Time in role, time at company]
- **Priorities**: [What they're focused on - from news, LinkedIn, calls]
- **Communication Style**: [How they prefer to engage]
- **Hot Buttons**: [What to emphasize, what to avoid]

### Recent Activity
*From LinkedIn, news, and internal data:*
- [Recent post or activity]
- [News mention or company announcement]
- [Relevant career milestone]

### Relationship Context
- **History**: [Previous interactions from CRM]
- **Current Status**: [Relationship health]
- **Open Items**: [Commitments, pending items]
- **Champions/Detractors**: [Internal allies and blockers]

### Company Context
- **Recent News**: [Relevant headlines]
- **Strategic Priorities**: [From earnings, news, job postings]
- **Challenges**: [Known issues they're facing]

---

### Meeting Objectives
1. [Primary objective]
2. [Secondary objective]
3. [Tertiary objective]

### Key Messages
1. [Message 1]: [Supporting point]
2. [Message 2]: [Supporting point]
3. [Message 3]: [Supporting point]

### Anticipated Questions & Responses
| Question | Response |
|----------|----------|
| [Question they'll likely ask] | [How to respond] |
| [Question they'll likely ask] | [How to respond] |

### The Ask
- **Primary Ask**: [What we want]
- **Fallback Ask**: [If primary isn't achievable]
- **Give to Get**: [What we're offering in return]

### Meeting Flow
1. [Opening - 2 min]: [What to say/do]
2. [Context Setting - 3 min]: [What to cover]
3. [Core Discussion - 15 min]: [Key topics]
4. [Ask/Commitment - 5 min]: [How to position]
5. [Close - 2 min]: [Next steps]

### Risk Factors
- [Risk 1]: [Mitigation]
- [Risk 2]: [Mitigation]

### Success Criteria
- [ ] [What makes this meeting successful]
- [ ] [Specific outcome to achieve]

---

### Quick Reference Card

**Open with**: "[Personalized opener based on recent activity]"
**Key question**: "[Most important question to ask]"
**Main message**: "[Core point to land]"
**Ask for**: "[Specific commitment]"
**Avoid**: "[Topics to steer away from]"
```

### Event Talk Track

```markdown
## Event Prep: [Event Name]

**Created**: [Date]
**Data Sources Used**: [Attendee list, LinkedIn, CRM, etc.]

---

### Event Overview
- **Event**: [Name and type]
- **Date/Time**: [When]
- **Format**: [Dinner, cocktails, conference, etc.]
- **Your Role**: [Host, sponsor, attendee]

### Key Attendees

| Name | Title | Company | Priority | Intel |
|------|-------|---------|----------|-------|
| [Name] | [Title] | [Company] | [High/Med/Low] | [Key context] |

### Conversation Starters
1. [Industry topic that's timely and relevant]
2. [Shared challenge executives are facing]
3. [Recent news worth discussing]

### Key Messages to Weave In
- [Message 1]: [When/how to introduce naturally]
- [Message 2]: [When/how to introduce naturally]

### Relationship Goals
- **Strengthen**: [Existing relationships to deepen]
- **Create**: [New connections to make]
- **Repair**: [Any relationships needing attention]

### Follow-Up Plan
| Attendee | Follow-Up Action | Timeline |
|----------|------------------|----------|
| [Name] | [Specific action] | [When] |
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Auto-prep for executive meetings** - Generate briefings when executive meetings appear on calendar
2. **Executive alerts** - Notify when executives post on LinkedIn or appear in news
3. **Relationship tracking** - Monitor engagement frequency with key executives
4. **Follow-up reminders** - Prompt for follow-ups after executive interactions
5. **Event preparation** - Automatically research attendees before events
