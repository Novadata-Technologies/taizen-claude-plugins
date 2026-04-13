---
name: gtm-messaging
description: Core messaging guidelines and value framing principles for consistent GTM communications. Reference this for any customer-facing content.
---

# GTM Messaging Skill

Core messaging principles that ensure consistency across all go-to-market outputs.

## Purpose

Ensure all GTM communications align with established value propositions, messaging frameworks, and brand voice guidelines.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# GTM MESSAGING DATA SOURCES
# Configure the sources for your messaging foundations

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Messaging Documentation
- source: messaging_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Marketing/Messaging Framework/"
    - "/Marketing/Value Propositions/"
    - "/Marketing/Brand Guidelines/"
    - "/Product Marketing/Positioning/"

# Customer Research
- source: customer_research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Voice of Customer/"
    - "/Research/Win-Loss/"
    - "/Research/Persona Research/"

# Sales Enablement
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
  data:
    - approved_messaging
    - sales_decks
    - talk_tracks
```

### Output Destinations

```yaml
# Where to deliver messaging outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to messaging library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Messaging/"
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
- Content to align OR messaging goal
- `display` output enabled (always available)

Enhanced functionality requires:
- Messaging framework documentation
- Value proposition library
- Brand voice guidelines
- Approved sales content for reference

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule messaging consistency and alignment tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
At the start of each quarter, audit recent content for messaging consistency
and identify any drift from our approved frameworks. Share findings with
#product-marketing.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Quarterly Messaging Audit**:
```
At the start of each quarter, audit recent content for messaging consistency
and identify drift from approved frameworks. Save the audit to our Messaging
Audits folder and notify #product-marketing.
```

**Messaging Update Alert**:
```
When our messaging docs are updated, summarize the changes and notify the
GTM team on Slack so everyone stays aligned.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Document Storage**: Link your Google Drive, Notion, or SharePoint
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Audit content for messaging consistency" |
| `schedule` | When to run (cron or trigger) | "quarterly" or "when messaging docs updated" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #product-marketing, Google Drive" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "gtm-messaging"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Core Frameworks

### Value Proposition Structure

When articulating value, follow this hierarchy:

1. **Strategic Value** (C-level): Business transformation, competitive advantage, market leadership
2. **Operational Value** (VP/Director): Efficiency gains, risk reduction, scalability
3. **Tactical Value** (Manager/IC): Time savings, ease of use, immediate ROI

### Messaging Hierarchy

1. **Primary Message**: The single most important thing to communicate
2. **Supporting Points**: 2-3 proof points that reinforce the primary message
3. **Evidence**: Data, case studies, testimonials that validate claims

### Value Framing Principles

- **Lead with outcomes**, not features
- **Quantify impact** whenever possible (%, $, time)
- **Connect to business priorities** (growth, efficiency, risk)
- **Acknowledge current state** before presenting future state
- **Use customer language**, not internal jargon

---

## How to Use This Skill

When creating any GTM content, reference these foundations to ensure:

1. **Consistency**: Messages align across all touchpoints
2. **Clarity**: Value is immediately understandable
3. **Credibility**: Claims are substantiated with evidence
4. **Relevance**: Content speaks to audience priorities

Invoke with natural language:
- "Apply messaging guidelines to this email"
- "Check this content against our value framework"
- "Help me frame this feature announcement"

---

## Output Format

When applying messaging foundations, structure outputs as:

```markdown
## Key Message
[Primary value statement]

## Supporting Points
1. [Point 1 with evidence]
2. [Point 2 with evidence]
3. [Point 3 with evidence]

## Proof Points
- [Relevant metric or case study]
- [Customer quote or testimonial]
```
