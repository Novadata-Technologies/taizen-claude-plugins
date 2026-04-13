---
name: case-study-builder
description: Creates compelling customer case studies from interviews, data, and research. Use for customer story development, reference programs, or marketing content.
---

# Case Study Builder Skill

Create compelling customer success stories that drive credibility and conversions.

## Purpose

Transform customer wins into persuasive case studies that demonstrate value and build trust with prospects.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# CASE STUDY BUILDER DATA SOURCES
# Configure the sources relevant to your customer story development

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Customer Success Data
- source: customer_success
  connector: "{{GAINSIGHT | CHURNZERO | TOTANGO}}"
  data:
    - customer_health
    - success_metrics
    - nps_scores
    - customer_outcomes

# CRM Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - customer_records
    - deal_history
    - implementation_details
    - stakeholder_contacts

# Call Recordings
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - customer_calls
    - success_conversations
    - customer_quotes

# Product Usage
- source: product_analytics
  connector: "{{MIXPANEL | AMPLITUDE | PENDO}}"
  data:
    - feature_adoption
    - usage_metrics
    - engagement_scores

# Existing Case Studies
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Case Studies/"
    - "/Customer Success/Success Stories/"
```

### Output Destinations

```yaml
# Where to deliver case study outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to marketing library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Case Studies/"

  # Push to CMS
  - type: cms
    connector: "{{WORDPRESS | WEBFLOW | CONTENTFUL}}"
    action: create_draft

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#customer-marketing"
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
- Customer name and use case context
- Key outcomes or results to highlight
- `display` output enabled (always available)

Enhanced functionality requires:
- CRM for customer journey and deal data
- Customer success platform for metrics and outcomes
- Interview transcripts or call recordings
- Existing case study templates

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule tasks for building case studies with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, identify customers with strong success metrics and
high NPS scores as case study candidates. Post the list to #customer-marketing.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Case Study Candidate Identification**:
```
On the 1st of each month, identify customers with strong success metrics and
high NPS scores as case study candidates. Post the list to #customer-marketing
and save to our Case Study Pipeline folder.
```

**Interview Prep Automation**:
```
When a case study interview is scheduled, automatically generate interview
prep including customer background, success metrics, and tailored questions.
DM the interviewer with the prep materials.
```

**Draft from Interview Recording**:
```
When a customer interview is completed in Gong, automatically generate a
case study draft from the recording and customer data. Post the draft to
#customer-marketing for review.
```

**Quarterly Case Study Review**:
```
At the start of each quarter, review existing case studies for outdated
information and identify which ones need a refresh. Share findings with
#customer-marketing.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Customer Success**: Link your Gainsight or ChurnZero
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Identify case study candidates from top NPS customers" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when interview scheduled" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #customer-marketing, Google Drive" |
| `criteria` | Customer selection criteria | "NPS 9+, health score green" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "case-study-builder"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Case Study Framework

### 1. Story Arc Structure

**The Classic Narrative**:
1. **Challenge**: What problem did they face?
2. **Solution**: How did they solve it (with your product)?
3. **Results**: What outcomes did they achieve?

**The Hero's Journey** (for deeper stories):
1. **Status Quo**: Where they started
2. **Catalyst**: What triggered change
3. **Journey**: The implementation experience
4. **Transformation**: The new reality
5. **Future**: What's next

### 2. Essential Elements

**Credibility Builders**:
- Named customer and contact
- Specific role and company context
- Quantified results (%, $, time)
- Timeline and scope
- Third-party validation

**Emotional Elements**:
- Personal stakes for the champion
- Organizational pressure
- Moment of realization
- Sense of accomplishment

### 3. Case Study Types

| Type | Length | Use Case |
|------|--------|----------|
| Snapshot | 1 page | Quick proof, sales leave-behind |
| Standard | 2-3 pages | Website, gated content |
| Deep Dive | 4-6 pages | Enterprise sales, analyst briefings |
| Video | 2-3 min | Website, events, social |
| Slide | 5-10 slides | Sales presentations, webinars |

### 4. Interview Guide

**Background Questions**:
- Tell me about your role and responsibilities
- Describe your organization and what you do
- What was the landscape before [solution]?

**Challenge Questions**:
- What challenges were you facing?
- What was the impact of these challenges?
- What had you tried before?
- What made you decide to look for a solution?

**Solution Questions**:
- How did you find [company]?
- What stood out during evaluation?
- How was the implementation process?
- How do you use the product day-to-day?

**Results Questions**:
- What results have you seen?
- Can you quantify the impact?
- What surprised you?
- How has your team's experience changed?

**Future Questions**:
- What's next for your team?
- Would you recommend [product]? To whom?
- What advice would you give others?

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Case Study Creation**
- "Create a case study for Acme Corp"
- "Generate a snapshot case study for our website"
- "Build a video case study script for TechCorp"

**Interview Prep**
- "Prepare me for the case study interview with Nike tomorrow"
- "Generate interview questions for a fintech customer story"

**From Notes**
- "Create a case study from these interview notes: [paste]"
- "Turn this call transcript into a case study draft"

---

## Output Format

### Full Case Study

```markdown
# [Customer Name]: [Headline That Captures the Win]

**Created**: [Date]
**Data Sources Used**: [CRM, Gong, Customer Success, etc.]

---

## At a Glance

| | |
|--|--|
| **Company** | [Name, brief description] |
| **Industry** | [Industry] |
| **Size** | [Employees or revenue] |
| **Use Case** | [Primary use case] |

### Results Highlights

| Metric | Result |
|--------|--------|
| [Metric 1] | [XX% improvement] |
| [Metric 2] | [$XX saved/generated] |
| [Metric 3] | [XX hours/days saved] |

---

## The Challenge

[2-3 paragraphs describing the situation before, the pain points, and what was at stake]

> "[Quote from customer about the challenge]"
> — [Name], [Title], [Company]

### Key Challenges
- [Challenge 1]
- [Challenge 2]
- [Challenge 3]

---

## The Solution

[2-3 paragraphs about how they discovered your solution, the evaluation process, and implementation]

### Why [Your Product]
- [Reason 1]
- [Reason 2]
- [Reason 3]

### Implementation Highlights
- **Timeline**: [How long]
- **Scope**: [What was implemented]
- **Team**: [Who was involved]

> "[Quote about the solution or implementation]"
> — [Name], [Title]

---

## The Results

[2-3 paragraphs about the outcomes achieved, with specific metrics and examples]

### Quantified Impact

| Before | After | Improvement |
|--------|-------|-------------|
| [Metric] | [Metric] | [% change] |
| [Metric] | [Metric] | [% change] |

### Qualitative Wins
- [Outcome 1]
- [Outcome 2]
- [Outcome 3]

> "[Quote about results]"
> — [Name], [Title]

---

## What's Next

[Brief paragraph about future plans and expansion]

---

## About [Customer Company]

[Boilerplate about the customer]

---

*Ready to achieve similar results? [CTA]*
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Candidate identification** - Flag customers with strong success metrics as case study candidates
2. **Interview preparation** - Generate tailored interview guides based on customer data
3. **Draft generation** - Create case study drafts from call recordings
4. **Refresh alerts** - Identify outdated case studies that need updating
5. **Distribution** - Push approved case studies to CMS and sales content platforms
