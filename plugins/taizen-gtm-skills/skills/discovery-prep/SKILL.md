---
name: discovery-prep
description: Produces unified discovery prep with tailored questions, anticipated objections, and recommended demo flow. Use before discovery calls or demos.
---

# Discovery Prep Skill

Comprehensive preparation for discovery calls and initial demos.

## Purpose

Ensure every discovery conversation is strategic, insightful, and moves the opportunity forward.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# DISCOVERY PREP DATA SOURCES
# Configure the sources relevant to your discovery preparation

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# Account & Contact Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - account_record
    - contact_records
    - previous_opportunities
    - activity_history
    - notes_and_attachments
    - related_contacts

# Calendar Integration
- source: calendar
  connector: "{{GOOGLE_CALENDAR | OUTLOOK_CALENDAR}}"
  data:
    - meeting_details
    - attendee_list
    - meeting_notes

# Company Research
- source: linkedin
  connector: "{{LINKEDIN_SALES_NAVIGATOR | LINKEDIN}}"
  data:
    - company_profile
    - attendee_profiles
    - recent_posts
    - job_changes
    - shared_connections
- source: company_website
  url: "{{ACCOUNT_WEBSITE}}"
  pages:
    - about
    - leadership
    - careers
    - newsroom
- source: news_search
  enabled: true
- source: crunchbase
  enabled: true

# Enrichment Data
- source: enrichment
  connector: "{{ZOOMINFO | CLEARBIT | APOLLO}}"
  data:
    - company_data
    - technographics
    - org_chart
    - intent_signals

# Previous Conversations
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - previous_calls_with_account
    - similar_persona_calls
    - successful_discovery_examples

# Email History
- source: email
  connector: "{{GMAIL | OUTLOOK}}"
  data:
    - thread_history
    - previous_correspondence

# Internal Resources
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Sales/Discovery Guides/"
    - "/Sales/Persona Playbooks/"
    - "/Product/Demo Scripts/"
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
  data:
    - relevant_case_studies
    - persona_content
    - discovery_templates

# Competitive Intelligence
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitor_battlecards
    - recent_competitive_intel
```

### Output Destinations

```yaml
# Where to deliver discovery prep outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save prep doc for reference
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales/Meeting Prep/"

  # Add to CRM record
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - add_meeting_prep_notes
      - log_pre_call_research

  # Send to self before meeting
  - type: email
    connector: "{{GMAIL | OUTLOOK}}"
    action: draft_to_self
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule automatic discovery prep with [Taizen](https://usetaizen.com). Create a free account to have meeting prep delivered automatically before every call.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Before any discovery call on my calendar, automatically research the account
and attendees, then send me a prep brief via Slack 24 hours before the meeting
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create an agent triggered by your calendar events
3. Execute the prep and deliver results before your meetings

### Example Natural Language Requests

**Auto Discovery Prep**:
```
Whenever I have a meeting with "discovery", "intro", or "first call" in the
title, automatically generate a comprehensive prep doc including account
research, attendee LinkedIn profiles, tailored discovery questions, and
competitive context. Send it to me via Slack DM 24 hours before.
```

**Morning Meeting Digest**:
```
Every morning at 7am, look at my calendar and generate discovery prep
summaries for all meetings scheduled today that I haven't prepped for yet.
Send the digest to my Slack.
```

**New Attendee Alert**:
```
If a new attendee is added to any of my upcoming prospect meetings, research
them immediately and send me an update with their profile and relevant
talking points.
```

**Post-Meeting Follow-Up**:
```
After my discovery calls end, generate a follow-up email draft and suggest
what to update in the CRM based on typical next steps.
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
| `task` | Natural language description of what to do | "Generate discovery prep with tailored questions" |
| `schedule` | When to run | "24 hours before calendar events matching 'discovery'" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack DM, Google Drive, CRM" |
| `triggers` | Calendar or CRM events | "calendar events with 'discovery' in title" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "discovery-prep"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Discovery Framework

### Pre-Call Research

Before the call, gather:
- **Account Context**: Company, industry, size, recent news
- **Stakeholder Context**: Attendee roles, backgrounds, priorities
- **Competitive Context**: Current solutions, recent evaluations
- **Trigger Context**: Why now? What's driving the conversation?

### Discovery Question Framework

Structure questions across these dimensions:

**1. Current State**
- How do you currently handle [relevant process]?
- What tools/systems are you using today?
- Who's involved in this process?

**2. Pain & Impact**
- What's working well? What's not?
- When this breaks down, what's the impact?
- How does this affect [relevant business metric]?

**3. Future State**
- What does success look like?
- If you could change one thing, what would it be?
- What's your timeline for addressing this?

**4. Decision Process**
- Who else is involved in evaluating solutions?
- What criteria matter most?
- What's worked or not worked with past vendors?

**5. Compelling Event**
- What's driving the timing of this initiative?
- What happens if nothing changes?
- Are there any deadlines we should be aware of?

### Demo Customization Guide

Based on discovery, customize the demo:

**Opening (2 min)**: Recap what you heard, confirm priorities
**Core Demo (15-20 min)**: Focus on their top 2-3 use cases
**Differentiators (5 min)**: Highlight unique value for their context
**Proof Points (3 min)**: Share relevant customer stories
**Next Steps (5 min)**: Align on path forward

---

## How to Use This Skill

Invoke with natural language describing your upcoming meeting:

**Basic Prep**
- "Prep me for my discovery call with Acme Corp tomorrow"
- "I have a meeting with Stripe in an hour - quick prep"
- "Help me prepare for my first call with Nike"

**Specific Context**
- "Prep for my call with the VP of Engineering at TechCorp - it's a technical discovery"
- "I'm meeting with the CHRO at IBM - prepare persona-specific questions"
- "Discovery prep for Acme Corp - they're currently using Competitor X"

**Demo Prep**
- "Prep me for the demo with Salesforce - focus on enterprise features"
- "I have a demo after discovery with a fintech company - what should I show?"

**Follow-Up Calls**
- "Prep for my second call with Acme - we did discovery last week"
- "I'm doing a deeper dive with the technical team at Nike - prep me"

---

## Output Format

```markdown
## Discovery Prep: [Company] - [Meeting Type]

**Prepared**: [Date/Time]
**Meeting**: [Date/Time]
**Your Prep Time**: ~10 minutes to review
**Data Sources Used**: [CRM, LinkedIn, News, Gong, etc.]

---

### Meeting Context

- **Company**: [Name]
- **Meeting Type**: [Discovery / Demo / Follow-up]
- **Your Objective**: [What you want to accomplish]

### Attendees

| Name | Title | LinkedIn | Key Intel |
|------|-------|----------|-----------|
| [Name] | [Title] | [Link] | [Background, tenure, recent activity, priorities] |

### Why This Meeting?

**Trigger Event**: [What prompted this conversation - from news, CRM, or outreach]
**Their Likely Priorities**: [Based on role, company situation, industry]
**Potential Pain Points**: [Hypotheses based on research]

---

### Pre-Call Intel

**Company Context**
- **Industry**: [Industry]
- **Size**: [Employees] | **Revenue**: [If known]
- **Stage**: [Growth stage, funding status]
- **Recent News**: [Relevant headlines]

**Strategic Priorities**
*Based on job postings, news, and earnings:*
1. [Priority 1]
2. [Priority 2]

**Technology Landscape**
- **Current Stack**: [Known technologies from enrichment data]
- **Likely Current Solution**: [What they're using for your category]
- **Intent Signals**: [If available from intent data]

**Your History**
*From CRM:*
- **Previous Contact**: [Any prior touchpoints]
- **Previous Opportunities**: [Past deals if any]
- **Notes**: [Relevant CRM notes]

---

### Discovery Questions

**Opening (Build Rapport & Confirm Context)**
1. "[Personalized question based on their background or recent news]"
2. "What prompted you to take this meeting? What are you hoping to learn?"

**Current State (Understand Today)**
1. "[Question about their current process/solution]"
2. "[Question about who's involved]"
3. "[Question about what's working]"

**Pain & Impact (Uncover Problems)**
1. "[Question about challenges - tailored to their likely situation]"
2. "[Question about business impact]"
3. "[Question about cost of status quo]"

**Future State (Understand Goals)**
1. "[Question about desired outcomes]"
2. "[Question about success metrics]"

**Process (Map the Deal)**
1. "Besides yourself, who else would be involved in evaluating a solution like this?"
2. "What does your decision-making process typically look like?"
3. "What timeline are you working toward?"

**Compelling Event**
1. "What's driving the timing of this initiative?"
2. "What happens if this doesn't get addressed this [quarter/year]?"

---

### Anticipated Objections

*Based on persona, company stage, and common patterns:*

| Likely Objection | Why They'll Say It | Response Strategy |
|------------------|-------------------|-------------------|
| "[Objection 1]" | [Root cause] | [How to address] |
| "[Objection 2]" | [Root cause] | [How to address] |
| "[Objection 3]" | [Root cause] | [How to address] |

---

### Competitive Positioning

**If They Mention [Competitor 1]**:
- Lead with: [Key differentiator]
- Landmine question: "[Question that exposes competitor weakness]"

**If They're Using [Current Solution]**:
- Displacement angle: [Why they should switch]
- Avoid: [What not to criticize]

---

### Demo Recommendations

*If this meeting includes a demo:*

**Focus Areas** (Based on their likely priorities)
1. **[Feature/Use Case 1]**: [Why relevant to them]
2. **[Feature/Use Case 2]**: [Why relevant to them]

**Skip/Minimize**
- [Area to de-emphasize]: [Why not relevant]

**Proof Points to Include**
- [Relevant customer in their industry]: [Key result]
- [Relevant metric]: [Impact stat]

---

### Success Criteria

This meeting is successful if you:
- [ ] Confirm/uncover their primary pain point
- [ ] Quantify the business impact
- [ ] Identify all stakeholders involved
- [ ] Understand timeline and urgency
- [ ] Secure clear next step with date

### Ideal Next Step

Based on this meeting type: [Specific next step to propose]

---

### Quick Reference Card

**Open with**: "[Personalized opener]"
**Key question to ask**: "[Most important discovery question]"
**Value prop to emphasize**: "[Most relevant benefit for them]"
**Proof point to share**: "[Best customer story for this persona]"
**Ask for**: "[Specific next step]"
```

---

## Automation Options

When configured with calendar integration, this skill can:

1. **Auto-prep before meetings** - Generate prep docs automatically before scheduled discovery calls
2. **Attendee alerts** - Notify you when new stakeholders are added to meetings
3. **Competitive triggers** - Alert when prospects are researching competitors (from intent data)
4. **Post-meeting logging** - Prompt you to log notes and next steps after calls
