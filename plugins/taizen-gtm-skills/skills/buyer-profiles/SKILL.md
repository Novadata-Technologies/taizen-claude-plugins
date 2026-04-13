---
name: buyer-profiles
description: Buyer persona profiles with priorities, language preferences, and objection patterns. Helps adapt messaging for different stakeholders.
---

# Buyer Profiles Skill

Adapt communications for specific buyer personas with guidance on priorities, language, and concerns, informed by real conversation data.

## Purpose

Ensure messaging resonates with the target buyer by understanding their priorities, language, objections, and decision-making criteria.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# BUYER PROFILES DATA SOURCES
# Configure the sources relevant to your buyer research

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# Conversation Intelligence (Primary Source)
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - calls_by_persona
    - objection_patterns
    - questions_asked
    - winning_talk_tracks
    - language_analysis
    - sentiment_by_persona

# CRM Deal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - deals_by_persona
    - win_rates_by_title
    - deal_velocity_by_persona
    - objections_logged

# Research & Documentation
- source: research_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Research/Personas/"
    - "/Research/Customer Interviews/"
    - "/Sales Enablement/Persona Playbooks/"
    - "/Marketing/Messaging/"

# Marketing Engagement
- source: marketing_analytics
  connector: "{{HUBSPOT | MARKETO | GOOGLE_ANALYTICS}}"
  data:
    - content_engagement_by_persona
    - email_performance_by_segment
    - conversion_paths

# Customer Success Insights
- source: customer_success
  connector: "{{GAINSIGHT | CHURNZERO | TOTANGO}}"
  data:
    - persona_health_patterns
    - churn_by_buyer_type
    - expansion_by_persona

# External Research
- source: linkedin
  enabled: true
  data:
    - role_insights
    - career_paths
    - common_skills
- source: job_postings
  enabled: true
  data:
    - responsibilities
    - requirements
    - reporting_structures
```

### Output Destinations

```yaml
# Where to deliver buyer profile outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to enablement library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales Enablement/Buyer Profiles/"

  # Quick reference via Slack
  - type: slack
    connector: "{{SLACK}}"
    action: dm_to_self  # Quick lookup before calls
```
---

## Instructions for Claude

> **IMPORTANT**: Before executing this skill, you MUST validate the configuration above.

### Pre-Execution Checklist

1. **Check for placeholder values**: Scan the YAML configuration for any `{{...}}` placeholders. These indicate required configuration that the user must provide.

2. **Validate data sources**: For each data source listed:
   - If a `connector` field shows `{{OPTIONS}}` format, ask the user which option they use
   - If URLs, paths, or names contain `{{PLACEHOLDER}}`, ask the user to provide actual values
   - Verify any required MCP servers are connected and available

3. **Validate output destinations**: For any output type beyond `display`:
   - Confirm the connector is available as an MCP server
   - Ensure destination paths/channels are configured (not placeholders)

### If Configuration is Incomplete

**Do not proceed with the skill.** Instead:

1. List the specific missing or placeholder values found
2. Explain what each value is needed for
3. Ask the user to provide the missing configuration
4. Offer to help them set up the required MCP integrations

**Example response when config is incomplete:**
```
Before I can run this skill, I need some configuration:

**Missing values:**
- [List specific {{PLACEHOLDER}} values found]

**MCP connections needed:**
- [List required connectors not yet available]

Please provide these values, or let me know which data sources you'd like to skip.
```

### Minimum Requirements

At minimum, this skill requires:
- Target persona role (e.g., "CFO", "VP of Engineering")
- `display` output enabled (always available)
- Web search provides general persona insights without additional setup

Enhanced functionality requires:
- CRM for win/loss patterns by persona
- Call recordings for objection patterns and language
- Customer research docs for validated persona data

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring buyer profile tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, analyze last month's Gong calls and CRM data to
update our buyer persona profiles with new objection patterns and winning
talk tracks. Post updates to #sales-enablement.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Persona Insights**:
```
On the 1st of each month, analyze last month's call recordings and deal data
to update persona objection patterns and winning talk tracks. Alert me if
there are any new objection patterns or shifts in priorities.
```

**Pre-Call Persona Briefs**:
```
Before any meeting with a prospect, look up the attendees' titles and send
me a quick persona brief with their priorities, common objections, and
recommended questions via Slack DM 30 minutes before the call.
```

**Quarterly Persona Review**:
```
At the start of each quarter, do a comprehensive review of all buyer personas
with updated insights from Gong, CRM, and marketing data. Create a summary
deck and post to #sales-enablement.
```

**Emerging Persona Detection**:
```
When new title patterns start appearing frequently in our deals, analyze the
emerging buyer persona and create a draft profile with what we know so far.
Alert the sales enablement team.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Call Intelligence**: Link your Gong, Chorus, or Clari
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Update persona objection patterns from Gong data" |
| `schedule` | When to run (cron or trigger) | "monthly on the 1st" or "before calendar events" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #sales-enablement, Google Drive" |
| `personas` | Which personas to focus on | "CFO, VP Sales, IT Director" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "buyer-profiles"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Your Buyer Profiles Configuration

```yaml
# Configure the buyer personas relevant to your business
# This should reflect your actual target buyers

personas:
  executive:
    - title: "{{EXECUTIVE_TITLE_1}}"  # e.g., "CHRO", "CFO", "CTO"
      role: economic_buyer
    - title: "{{EXECUTIVE_TITLE_2}}"
      role: economic_buyer

  management:
    - title: "{{MANAGER_TITLE_1}}"  # e.g., "VP of Sales", "Director of HR"
      role: decision_maker
    - title: "{{MANAGER_TITLE_2}}"
      role: influencer

  practitioner:
    - title: "{{PRACTITIONER_TITLE_1}}"  # e.g., "Sales Manager", "HR Manager"
      role: user_buyer
    - title: "{{PRACTITIONER_TITLE_2}}"
      role: champion

  technical:
    - title: "{{TECHNICAL_TITLE_1}}"  # e.g., "IT Director", "Solutions Architect"
      role: technical_buyer
```

---

## Persona Framework

### Role in Purchase

| Role | Definition | How to Engage |
|------|------------|---------------|
| **Economic Buyer** | Controls budget, signs off | Lead with ROI, strategic value |
| **Technical Buyer** | Evaluates capabilities, integrations | Lead with features, security, scale |
| **User Buyer** | Will use the product daily | Lead with UX, efficiency, ease |
| **Champion** | Internal advocate | Equip them to sell internally |
| **Influencer** | Shapes opinion but doesn't decide | Build relationship, provide ammunition |
| **Blocker** | May oppose the purchase | Neutralize concerns, find common ground |

### Persona Components

- **Priorities**: What they care about most
- **Metrics**: How they're measured
- **Language**: Terms that resonate
- **Objections**: Common concerns
- **Fears**: Underlying anxieties
- **Influences**: Who they trust

---

## How to Use This Skill

Invoke with natural language describing the persona you need guidance on:

**Persona Lookup**
- "Tell me how to sell to a CFO"
- "What does a VP of Sales care about?"
- "How do I approach a CHRO?"
- "Give me a profile on IT Directors"

**Specific Guidance**
- "What objections will I get from a CFO?"
- "What language resonates with HR leaders?"
- "How do CHROs make buying decisions?"
- "What metrics matter to a VP of Marketing?"

**Competitive Deals**
- "How do I position against Competitor X when talking to a CFO?"
- "What concerns will a technical buyer have about switching?"

**Meeting Prep**
- "I'm meeting with a CTO tomorrow - quick prep on their priorities"
- "Prepare me to present to a CHRO"

**Multi-Stakeholder**
- "I have a CFO and CHRO in the same meeting - how do I balance messaging?"
- "How do I navigate between the economic buyer and technical buyer?"

---

## Output Format

```markdown
## Buyer Profile: [Title]

**Generated**: [Date]
**Data Sources Used**: [Gong analysis, CRM data, etc.]

---

### At a Glance

| Attribute | Details |
|-----------|---------|
| Common Titles | [Variations of this role] |
| Reports To | [Typical reporting structure] |
| Team Size | [Typical direct reports] |
| Role in Purchase | [Economic buyer / Technical buyer / User / Influencer] |
| Deal Involvement | [When they typically engage in the sales process] |

---

### Priorities

*Based on analysis of [X] conversations with this persona:*

1. **[Priority 1]**: [Evidence from calls/data]
2. **[Priority 2]**: [Evidence]
3. **[Priority 3]**: [Evidence]

### Key Metrics They Care About

- [Metric 1]: [Why it matters to them]
- [Metric 2]: [Why it matters]
- [Metric 3]: [Why it matters]

---

### How They Buy

**Research Behavior**:
- [How they gather information]
- [Who they consult]

**Decision Criteria** (ranked by importance from deal data):
1. [Criterion 1]
2. [Criterion 2]
3. [Criterion 3]

**Typical Questions They Ask**:
*From Gong analysis:*
- "[Question 1]" - [How to respond]
- "[Question 2]" - [How to respond]

---

### Language & Messaging

**Terms That Resonate**:
*Based on successful calls:*
- [Term 1]: [Context]
- [Term 2]: [Context]

**Terms to Avoid**:
- [Term 1]: [Why it doesn't work]

**Value Prop for This Persona**:
"[Persona-specific value statement]"

---

### Common Objections

*From Gong objection tracking:*

| Objection | Frequency | Root Cause | Best Response |
|-----------|-----------|------------|---------------|
| "[Objection 1]" | [% of calls] | [Why they say it] | [What works] |
| "[Objection 2]" | [% of calls] | [Why they say it] | [What works] |

### Underlying Fears

- **[Fear 1]**: [How it manifests] → [How to address]
- **[Fear 2]**: [How it manifests] → [How to address]

---

### Engagement Strategy

**Best Channels**:
*From marketing data:*
- [Channel]: [Engagement rate]

**Content That Works**:
- [Content type 1]: [Performance data]
- [Content type 2]: [Performance data]

**Meeting Tips**:
- [Tip based on call analysis]
- [Tip based on call analysis]

**Discovery Questions**:
1. "[Question tailored to their priorities]"
2. "[Question about their metrics]"
3. "[Question about their challenges]"

---

### What Top Performers Do

*Based on analysis of won deals with this persona:*

**Opening**: [How top reps open with this persona]
**Demo Focus**: [What to emphasize]
**Closing**: [How top reps close]

**Winning Talk Track**:
> "[Example from successful calls]"

---

### Competitive Positioning

**When Competing Against [Competitor]**:
- Lead with: [Differentiator that matters to this persona]
- Avoid: [What not to say]
- Landmine: "[Question that helps us]"

---

### Quick Reference Card

For use before/during calls:

| Speak To | Avoid | Ask About | Prove With |
|----------|-------|-----------|------------|
| [Topic] | [Topic] | [Topic] | [Proof point] |
```

---

## Multi-Stakeholder Guidance

When multiple personas are involved:

```markdown
## Multi-Stakeholder Playbook: [CFO + CHRO / etc.]

### Meeting Dynamics

**[Persona 1]** cares about: [Priorities]
**[Persona 2]** cares about: [Priorities]

### Balancing Act

- **Open with**: [Something that appeals to both]
- **Address [Persona 1] first**: [Topic]
- **Then pivot to [Persona 2]**: [Topic]
- **Bridge them with**: [Shared interest]

### Watch For

- **Conflict areas**: [Where their priorities may clash]
- **How to navigate**: [Strategy]

### Ask

- "[Question for Persona 1]" → then "[Question for Persona 2]"
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Real-time persona lookup** - Quick reference before calls via Slack
2. **Talk track suggestions** - Surface winning approaches based on persona
3. **Objection intelligence** - Continuously update objection patterns from Gong
4. **Win pattern analysis** - Identify what top performers do with each persona
5. **Persona detection** - Automatically identify persona type from calendar/CRM
