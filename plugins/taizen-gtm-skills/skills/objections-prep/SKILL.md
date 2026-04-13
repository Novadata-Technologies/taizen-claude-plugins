---
name: objections-prep
description: Produces prep output for anticipated objections with response strategies and reframing techniques. Use when preparing for negotiations or objection-heavy conversations.
---

# Objections Prep Skill

Anticipate and prepare responses for common and deal-specific objections.

## Purpose

Equip sales teams with confident, effective responses to objections that advance the deal rather than stall it.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# OBJECTION HANDLING DATA SOURCES
# Configure the sources relevant to your objection preparation

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# Call Recording & Objection Patterns
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - objection_tracking
    - successful_responses
    - failed_responses
    - objection_by_competitor
    - objection_by_persona
    - objection_by_deal_stage

# CRM Deal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - lost_deal_reasons
    - stalled_deal_notes
    - competitive_fields
    - deal_stage_notes

# Competitive Intelligence
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitor_objections
    - win_loss_by_competitor
    - competitive_responses
- source: review_sites
  sources:
    - g2
    - capterra
    - trustradius
  data:
    - competitor_weaknesses
    - our_criticisms

# Internal Knowledge
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Sales Enablement/Objection Handling/"
    - "/Sales/Battlecards/"
    - "/Product/FAQ/"
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
  data:
    - objection_handling_guides
    - competitive_content

# Pricing & Packaging
- source: pricing_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Sales/Pricing/"
    - "/Finance/Discount Guidelines/"

# Customer Proof Points
- source: customer_stories
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Case Studies/"
    - "/Customer Success/Win Stories/"
```

### Output Destinations

```yaml
# Where to deliver objection prep outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to enablement library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales Enablement/Objection Handling/"

  # Quick reference via Slack
  - type: slack
    connector: "{{SLACK}}"
    action: dm_to_self  # Quick access during calls
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring objection prep tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, analyze objection patterns from last month's Gong
calls, identify new objection trends, and update our response playbooks. Alert
me if there are any new patterns or declining response effectiveness.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Objection Analysis**:
```
On the 1st of each month, analyze objection patterns from last month's calls,
identify new objection trends, and update our response playbooks. Post findings
to #sales-enablement.
```

**Weekly Competitive Objections**:
```
Every Monday at 9am, review competitive mentions and objections from last
week's calls and update our battlecards with new response strategies. Share
updates in #competitive-intel.
```

**Pre-Negotiation Prep**:
```
When a deal moves to negotiation stage in Salesforce, automatically generate
anticipated objections and response strategies based on the account, competitors
involved, and similar past deals. DM the deal owner.
```

**Objection Effectiveness Review**:
```
On the 15th of each month, correlate objection responses with deal outcomes
to identify which response strategies are actually winning deals. Share
insights with #sales-management.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Gong/Chorus**: Link your conversation intelligence platform
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Analyze objection patterns and update response playbooks" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when deal enters negotiation" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #sales-enablement, Google Drive" |
| `competitors` | Focus on specific competitors | "Salesforce, HubSpot" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "objections-prep"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
    - name: "competitive-intelligence"
      content: "<full content of competitive-intelligence SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context` and `competitive-intelligence`) and include them in `skill_content.referenced`.

---

## Objection Handling Framework

### The LAER Method

1. **Listen**: Let them finish, acknowledge the concern
2. **Acknowledge**: Show empathy, validate the concern is reasonable
3. **Explore**: Ask questions to understand the root cause
4. **Respond**: Address with evidence, reframe, or propose a path forward

### Common Objection Categories

**Price/Budget Objections**
- "It's too expensive"
- "We don't have budget"
- "Competitor X is cheaper"
- "We need to reduce costs, not add them"

**Timing Objections**
- "Not the right time"
- "We're too busy right now"
- "Maybe next quarter/year"
- "We just implemented something else"

**Authority Objections**
- "I need to check with my boss"
- "This requires executive approval"
- "Others need to be involved"

**Need Objections**
- "We're fine with what we have"
- "This isn't a priority"
- "We've tried this before"
- "Our situation is different"

**Trust Objections**
- "We've never heard of you"
- "You're too small/new"
- "Can you prove these claims?"
- "What if it doesn't work?"

**Competitive Objections**
- "We're already working with X"
- "X has more features"
- "X is the industry standard"

---

## Response Strategies

### Reframe the Objection
Transform the objection into a reason to buy:
- "Too expensive" → "Let's talk about the cost of the problem you're solving"

### Isolate the Objection
Confirm this is the only barrier:
- "If we could address [objection], would you be ready to move forward?"

### Feel-Felt-Found
Relate to similar customers:
- "I understand how you feel. Other [similar companies] felt the same way. What they found was..."

### Evidence & Proof
Counter with data:
- "Actually, our customers typically see [X]% improvement in [Y]"

### Question Back
Understand the real concern:
- "Help me understand - when you say it's too expensive, compared to what?"

---

## How to Use This Skill

Invoke with natural language describing your situation:

**General Objection Prep**
- "Prepare me for common objections in enterprise deals"
- "What objections should I expect in a discovery call?"
- "Help me handle pricing objections"

**Deal-Specific**
- "I'm about to have a negotiation call with Acme Corp - what objections should I expect?"
- "The TechCorp deal is stalled - they said they need to 'think about it'. How do I respond?"
- "Prep me for objections from a CFO"

**Competitor-Specific**
- "How do I handle objections when competing against Salesforce?"
- "They're considering Competitor X - what will they object to about us?"
- "Prepare responses for 'Competitor X has more features'"

**Scenario-Specific**
- "Prepare me to handle 'we don't have budget right now'"
- "How do I respond when they say 'we need to involve procurement'?"
- "What do I say when the champion goes quiet?"

---

## Output Format

```markdown
## Objection Prep: [Context]

**Prepared for**: [Situation/Deal/Persona]
**Data Sources Used**: [Gong patterns, competitive intel, etc.]

---

### Top Objections to Expect

*Based on [data source - e.g., "similar deals in Gong", "this persona", "competitive situation"]:*

---

**Objection 1: "[Exact objection phrasing]"**

**Frequency**: [How often this comes up - from Gong data]
**Root Cause**: [Why they're really saying this]
**Stage It Appears**: [When in deal cycle]

**Response Strategy**: [Which approach to use]

**Sample Response**:
> "I appreciate you sharing that. [Acknowledge]. Help me understand - [explore question]?"
>
> [After they respond]
>
> "That makes sense. What we've found with [similar company] is [evidence]. Would it help if [offer]?"

**Follow-Up Questions**:
- "[Question to dig deeper]"
- "[Question to understand real concern]"

**Proof Points**:
- [Customer name]: [Result that counters this objection]
- [Stat]: [Data point that addresses concern]

**What's Worked** (from top performers):
- [Example of successful response from Gong]

**What Hasn't Worked**:
- [Common mistake to avoid]

---

**Objection 2: "[Exact objection phrasing]"**

[Same format]

---

**Objection 3: "[Exact objection phrasing]"**

[Same format]

---

### Proactive Objection Prevention

Address these before they come up:

| Concern | When to Address | How to Preempt |
|---------|-----------------|----------------|
| [Topic 1] | [Moment in conversation] | "[What to say proactively]" |
| [Topic 2] | [Moment in conversation] | "[What to say proactively]" |

---

### If the Objection Is Real

When the objection is legitimate (not a smokescreen):

**Acknowledge honestly**:
> "[How to acknowledge without killing the deal]"

**Pivot to value**:
> "[How to refocus on what matters]"

**Alternative path forward**:
- [Option 1 to keep deal alive]
- [Option 2 to keep deal alive]

**When to walk away**:
- [Signals that this isn't a fit]
- [How to exit gracefully]

---

### Practice Scenarios

**Scenario 1: [Situation]**
- **Setup**: [Context]
- **They say**: "[Objection]"
- **You say**: "[Response]"
- **They say**: "[Follow-up pushback]"
- **You say**: "[How to continue]"
- **Goal**: [Desired outcome]

**Scenario 2: [Situation]**
[Same format]

---

### Quick Reference Card

For use during calls:

| Objection | Quick Response | Key Proof Point |
|-----------|----------------|-----------------|
| "[Short version]" | "[One-liner response]" | "[Customer/stat]" |
| "[Short version]" | "[One-liner response]" | "[Customer/stat]" |
| "[Short version]" | "[One-liner response]" | "[Customer/stat]" |
```

---

### Competitive Objection Handler

```markdown
## Competitive Objections: vs [Competitor Name]

**Last Updated**: [Date]
**Data Sources**: [Gong win/loss, G2 reviews, battlecards]

---

### Common Objections When Competing Against [Competitor]

**"[Competitor] has [feature]"**

**Reality Check**: [Is this true? Nuance?]

**Response**:
> "[How to handle]"

**Landmine Question**:
> "[Question that exposes the limitation of their feature]"

**Proof Point**:
- [Customer who switched and why]

---

**"[Competitor] is cheaper"**

**Reality Check**: [TCO analysis, hidden costs]

**Response**:
> "[How to handle]"

**Value Calculator**: [Link to ROI tool if available]

---

**"[Competitor] is the industry standard"**

**Response**:
> "[How to handle]"

**Counter-Examples**:
- [Major customer who chose us]

---

### Wins Against [Competitor]

*From CRM and Gong:*

| Customer | Why They Chose Us | Key Quote |
|----------|-------------------|-----------|
| [Name] | [Reason] | "[Quote]" |
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Real-time objection coaching** - Surface suggested responses during live calls (via Gong/Chorus integration)
2. **Pattern detection** - Alert when new objection patterns emerge across team
3. **Win/loss correlation** - Identify which objection responses lead to wins vs losses
4. **Competitive alerts** - Update objection handlers when competitors make changes
