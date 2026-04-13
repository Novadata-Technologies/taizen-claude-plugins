---
name: brand-voice
description: Creates content aligned with brand voice guidelines. Ensures consistency in tone, language, and personality across all communications.
---

# Brand Voice Skill

Create and maintain consistent brand voice across all content.

## Purpose

Ensure every piece of content sounds authentically like your brand, maintaining consistency across channels, authors, and content types.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# BRAND VOICE DATA SOURCES
# Configure the sources relevant to your brand management needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Brand Guidelines & Assets
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Voice and Tone/"
    - "/Marketing/Messaging Framework/"
    - "/Marketing/Editorial Style Guide/"
    - "/Marketing/Do's and Don'ts/"

# Content Library (for examples)
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Published Content/"
    - "/Marketing/Email Templates/"
    - "/Marketing/Web Copy/"
    - "/Marketing/Social Media/"

# Content Performance
- source: analytics
  connector: "{{GOOGLE_ANALYTICS | HUBSPOT | MAILCHIMP}}"
  data:
    - content_engagement
    - email_performance
    - page_engagement

# Customer Voice
- source: customer_research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Voice of Customer/"
    - "/Research/Customer Language/"
```

### Output Destinations

```yaml
# Where to deliver brand voice outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to brand library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Brand Guidelines/"

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#brand-review"
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
- Existing content samples OR brand guidelines description
- `display` output enabled (always available)

Enhanced functionality requires:
- Brand guidelines document access
- Existing approved content library
- Style guide and tone documentation

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring brand voice tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, audit our recently published content for brand voice
consistency and identify any deviations or patterns. Alert me on Slack if there
are any off-brand issues.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Brand Audit**:
```
On the 1st of each month, audit recently published content for brand voice
consistency. Identify deviations and patterns, and share findings with
#brand-review.
```

**Content Brand Check**:
```
Whenever new content is submitted for review, automatically check it for
brand voice alignment and send feedback to the author via Slack DM.
```

**Quarterly Guide Refresh**:
```
At the start of each quarter, review our brand voice guide for relevance and
update it with new examples from our high-performing content. Notify #marketing
when complete.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Content Sources**: Link your CMS and document storage
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Audit published content for brand voice consistency" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when content submitted" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #brand-review, Google Drive" |
| `content_types` | Which content to focus on | "blog posts, landing pages, emails" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "brand-voice"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Brand Voice Framework

### 1. Voice Attributes

**Core Voice Dimensions**:

| Dimension | Spectrum |
|-----------|----------|
| Formal ←→ Casual | Where does your brand sit? |
| Serious ←→ Playful | What's the appropriate tone? |
| Technical ←→ Accessible | How much jargon is acceptable? |
| Reserved ←→ Enthusiastic | How much energy in the writing? |
| Traditional ←→ Innovative | How forward-looking? |

### 2. Voice Definition Template

**We Are**:
- [Trait 1]: [What this means in practice]
- [Trait 2]: [What this means in practice]
- [Trait 3]: [What this means in practice]

**We Are Not**:
- [Anti-trait 1]: [What to avoid]
- [Anti-trait 2]: [What to avoid]
- [Anti-trait 3]: [What to avoid]

### 3. Tone Adaptation

Voice stays consistent, tone adapts to context:

| Context | Tone Shift |
|---------|------------|
| Product launch | Excited, confident |
| Support content | Helpful, patient |
| Thought leadership | Authoritative, insightful |
| Error messages | Empathetic, clear |
| Social media | Conversational, timely |
| Legal/compliance | Precise, formal |

### 4. Language Guidelines

**Vocabulary**:
- Words we use: [List of on-brand terms]
- Words we avoid: [List of off-brand terms]
- Industry terms: [How we handle jargon]

**Grammar & Style**:
- Contractions: [Yes/No/When]
- Oxford comma: [Yes/No]
- Sentence length: [Guidance]
- Active vs passive voice: [Preference]
- Numbers: [Spelled out vs digits]

**Formatting**:
- Headlines: [Title case/Sentence case]
- CTAs: [Style guidance]
- Lists: [Punctuation rules]

---

## De-Slop Checklist

Remove these weak patterns:
- [ ] Excessive adverbs (very, really, actually)
- [ ] Filler phrases (in order to, due to the fact that)
- [ ] Passive voice (when active is clearer)
- [ ] Buzzwords without substance
- [ ] Clichés and overused phrases
- [ ] Unnecessarily complex words
- [ ] Hedging language (might, could, perhaps)

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Brand Voice Guide**
- "Create a brand voice guide for our company"
- "Document our tone and style guidelines"
- "Build a writer's guide with dos and don'ts"

**Content Review**
- "Review this content for brand voice alignment: [paste]"
- "Check if this email matches our brand guidelines"
- "Is this landing page copy on-brand?"

**Rewriting**
- "Rewrite this in our brand voice: [paste]"
- "Make this content more on-brand"
- "Adapt this for our social media voice"

**Channel Adaptation**
- "Adapt this content for our support documentation"
- "Rewrite this marketing copy for our executive audience"

---

## Output Format

### Brand Voice Guide

```markdown
# Brand Voice Guide: [Company Name]

**Created**: [Date]
**Data Sources Used**: [Brand docs, content library, etc.]

---

## Our Voice

### In One Sentence
[Company] sounds like [description of how we come across].

### Voice Attributes

| Attribute | What It Means | In Practice |
|-----------|---------------|-------------|
| [Attribute 1] | [Definition] | [Example] |
| [Attribute 2] | [Definition] | [Example] |
| [Attribute 3] | [Definition] | [Example] |
| [Attribute 4] | [Definition] | [Example] |

### We Are / We Aren't

| We Are | We Aren't |
|--------|-----------|
| [Trait] | [Opposite] |
| [Trait] | [Opposite] |
| [Trait] | [Opposite] |

---

## Tone by Context

| Content Type | Tone | Example |
|--------------|------|---------|
| Marketing | [Tone] | "[Sample sentence]" |
| Product | [Tone] | "[Sample sentence]" |
| Support | [Tone] | "[Sample sentence]" |
| Social | [Tone] | "[Sample sentence]" |
| Executive | [Tone] | "[Sample sentence]" |

---

## Language Guide

### Words We Love
| Word | Why | Instead Of |
|------|-----|------------|
| [Word] | [Reason] | [Alternative] |

### Words We Avoid
| Avoid | Why | Use Instead |
|-------|-----|-------------|
| [Word] | [Reason] | [Better option] |

### Industry Terms
| Term | Our Usage | Notes |
|------|-----------|-------|
| [Term] | [How we use it] | [Context] |

---

## Style Rules

### Grammar
- **Contractions**: [Guidance]
- **Oxford comma**: [Yes/No]
- **Em dashes**: [Usage]
- **Exclamation points**: [When appropriate]

### Formatting
- **Headlines**: [Case style]
- **CTAs**: [Style]
- **Numbers**: [Rules]
- **Dates**: [Format]

---

## Examples

### Good Examples

**Marketing Copy**:
✅ "[Good example that embodies our voice]"

**Product Copy**:
✅ "[Good example that embodies our voice]"

**Error Message**:
✅ "[Good example that embodies our voice]"

### Examples to Avoid

**Too Formal**:
❌ "[Example that's off-brand - too formal]"
✅ "[Rewritten to be on-brand]"

**Too Casual**:
❌ "[Example that's off-brand - too casual]"
✅ "[Rewritten to be on-brand]"

**Too Jargon-Heavy**:
❌ "[Example that's off-brand - too technical]"
✅ "[Rewritten to be on-brand]"
```

### Content Review

```markdown
# Brand Voice Review: [Content Title]

**Created**: [Date]
**Data Sources Used**: [Brand guidelines, etc.]

---

## Overview
- **Content Type**: [Type]
- **Target Audience**: [Audience]
- **Channel**: [Where it will appear]

## Voice Assessment

| Attribute | On-Brand? | Notes |
|-----------|-----------|-------|
| [Attribute 1] | ✅/⚠️/❌ | [Feedback] |
| [Attribute 2] | ✅/⚠️/❌ | [Feedback] |
| [Attribute 3] | ✅/⚠️/❌ | [Feedback] |

**Overall**: [On-brand / Needs work / Off-brand]

## Specific Feedback

### Strong Elements
- [What works well]
- [What works well]

### Needs Adjustment
| Current | Issue | Suggested |
|---------|-------|-----------|
| "[Current text]" | [Problem] | "[Revised text]" |
| "[Current text]" | [Problem] | "[Revised text]" |

### De-Slop Opportunities
- [ ] [Weak phrase to strengthen]
- [ ] [Filler to remove]
- [ ] [Passive to make active]

## Rewritten Version

[Full revised content that's fully on-brand]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Content validation** - Automatically check submitted content for brand voice alignment
2. **Style enforcement** - Flag off-brand language patterns before publishing
3. **Consistency audits** - Regularly review published content for voice drift
4. **Example library** - Build and maintain a library of on-brand examples from high-performing content
