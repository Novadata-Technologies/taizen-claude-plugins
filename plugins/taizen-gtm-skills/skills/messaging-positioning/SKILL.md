---
name: messaging-positioning
description: Builds positioning statements, value propositions, message houses, and persona-specific messaging. Use for positioning development or messaging refresh.
---

# Messaging & Positioning Skill

Develop compelling positioning and messaging frameworks that differentiate your product.

## Purpose

Create clear, differentiated positioning and messaging that resonates with target audiences and stands out from competitors.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# MESSAGING & POSITIONING DATA SOURCES
# Configure the sources relevant to your positioning development

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Existing Positioning
- source: positioning_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Product Marketing/Positioning/"
    - "/Marketing/Messaging Framework/"
    - "/Marketing/Brand Guidelines/"

# Customer Research
- source: customer_research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Customer Interviews/"
    - "/Research/Win-Loss Analysis/"
    - "/Research/Persona Research/"
    - "/Research/Voice of Customer/"

# Competitive Intelligence
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitor_positioning
    - competitor_messaging
    - market_positioning

# Call Recordings (customer language)
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - customer_language
    - objection_patterns
    - winning_messages
```

### Output Destinations

```yaml
# Where to deliver positioning outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to positioning library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Product Marketing/Positioning/"

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#product-marketing"
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
- Product or feature to position
- Target audience or segment
- `display` output enabled (always available)

Enhanced functionality requires:
- Customer research for validated insights
- Competitive intelligence for differentiation
- Win/loss data for proof points
- Existing positioning docs for alignment

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule positioning and messaging tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
At the start of each quarter, review our current positioning against market
changes, competitive moves, and customer feedback. Share the analysis with
#product-marketing.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Quarterly Positioning Review**:
```
At the start of each quarter, review our current positioning against market
changes, competitive moves, and customer feedback. Save to our Positioning
Reviews folder and notify #product-marketing.
```

**Competitive Positioning Alert**:
```
When a competitor changes their messaging or positioning, analyze the change
and recommend how we should respond. Alert #competitive-intel.
```

**New Feature Positioning**:
```
When we launch a new feature, automatically develop positioning and messaging
for it based on the target persona. Save to our Feature Messaging folder and
notify #product-marketing.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Competitive Intel**: Link your Klue, Crayon, or Kompyte
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Review positioning against competitive changes" |
| `schedule` | When to run (cron or trigger) | "quarterly" or "when competitor changes messaging" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #product-marketing, Notion" |
| `competitors` | Which competitors to monitor | "Salesforce, HubSpot" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "messaging-positioning"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Positioning Frameworks

### 1. Classic Positioning Statement

**Template**:
For [target customer] who [has this need/want], [Product] is a [category] that [key benefit]. Unlike [competitive alternative], [Product] [key differentiator].

**Example**:
For HR leaders who struggle to retain frontline workers, Acme is a career mobility platform that creates clear paths to advancement. Unlike traditional tuition reimbursement, Acme delivers personalized career journeys that drive measurable retention.

### 2. Category Design

When creating or redefining a category:

- **Category Name**: What do we call this new space?
- **Category Story**: Why does this category need to exist now?
- **Category POV**: What's our unique perspective on this category?
- **Category Criteria**: What defines a leader in this category?

### 3. Value Proposition Canvas

**Customer Profile**:
- Jobs to be done (functional, social, emotional)
- Pains (obstacles, risks, negative outcomes)
- Gains (desired outcomes, benefits, aspirations)

**Value Map**:
- Products & services (what you offer)
- Pain relievers (how you address pains)
- Gain creators (how you create gains)

### 4. Message House Framework

```
┌─────────────────────────────────────────┐
│           BRAND PROMISE                 │
│     (Core value / Tagline)              │
├─────────────┬───────────┬───────────────┤
│  PILLAR 1   │  PILLAR 2 │   PILLAR 3    │
│  Message    │  Message  │   Message     │
├─────────────┼───────────┼───────────────┤
│  Proof      │  Proof    │   Proof       │
│  Points     │  Points   │   Points      │
└─────────────┴───────────┴───────────────┘
         FOUNDATION / CREDIBILITY
         (Awards, stats, customers)
```

---

## Messaging Development

### Persona-Specific Messaging

Adapt core messages for each audience:

| Element | Executive | Manager | End User |
|---------|-----------|---------|----------|
| Focus | Strategic impact | Operational efficiency | Daily experience |
| Metrics | Revenue, market position | Team productivity, costs | Time savings, ease |
| Language | Business outcomes | Process improvement | Practical benefits |
| Proof | ROI, peer companies | Implementation ease | User testimonials |

### Messaging by Funnel Stage

**Awareness**: Problem-focused, educational
**Consideration**: Solution-focused, comparative
**Decision**: Proof-focused, risk-reduction
**Retention**: Value realization, expansion

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Positioning Development**
- "Create a positioning statement for our new product"
- "Develop a message house for enterprise buyers"
- "Build persona-specific messaging for CHRO"

**Positioning Refresh**
- "Refresh our positioning based on recent competitive changes"
- "Update messaging for our new market segment"

**Competitive Positioning**
- "How should we position against Competitor X?"
- "Develop differentiation messaging for RFPs"

---

## Output Format

```markdown
## Positioning & Messaging: [Product/Initiative]

**Created**: [Date]
**Data Sources Used**: [Customer research, competitive intel, etc.]

---

### Positioning Statement
[Full positioning statement using template]

### Core Value Proposition
**Headline**: [Compelling one-liner]
**Subhead**: [Supporting detail]
**Body**: [2-3 sentences expanding on value]

### Message House

#### Brand Promise
[Core promise / tagline]

#### Message Pillars

| Pillar | Key Message | Supporting Points | Proof |
|--------|-------------|-------------------|-------|
| [Theme] | [Message] | [Details] | [Evidence] |

#### Foundation
[Credibility elements: awards, stats, logos]

### Persona Messaging

#### [Persona 1: Title]
- **Primary Message**: [What resonates most]
- **Key Proof Points**: [Most relevant evidence]
- **Objection to Address**: [Likely concern]
- **Call to Action**: [Appropriate next step]

### Elevator Pitches

**10-Second Pitch**
[Shortest version for cocktail party]

**30-Second Pitch**
[Standard networking version]

**2-Minute Pitch**
[Full context with proof points]

### Competitive Positioning

| vs. [Competitor] | Our Position | Key Differentiator |
|------------------|--------------|-------------------|
| [Comp 1] | [Position] | [What makes us different] |
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Competitive monitoring** - Alert when competitors change positioning
2. **Messaging consistency** - Check content against approved messaging
3. **Customer language** - Extract positioning insights from call recordings
4. **Win/loss correlation** - Identify which messages win deals
