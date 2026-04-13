---
name: email-sequences
description: Designs email nurture sequences, drip campaigns, and automated email flows. Use for lead nurturing, onboarding, and lifecycle marketing.
---

# Email Sequences Skill

Design automated email sequences that nurture leads and customers through their journey.

## Purpose

Create strategic email sequences that move subscribers toward desired actions while building relationship and trust.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# EMAIL SEQUENCE DATA SOURCES
# Configure the sources relevant to your email marketing

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Email Platform & Performance Data
- source: email_platform
  connector: "{{HUBSPOT | MARKETO | KLAVIYO | MAILCHIMP | ACTIVECAMPAIGN | CUSTOMER_IO}}"
  data:
    - existing_sequences
    - email_performance
    - open_rates
    - click_rates
    - conversion_rates
    - unsubscribe_rates
    - a_b_test_results
    - segment_performance

# CRM & Contact Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - lead_stages
    - lifecycle_stages
    - contact_properties
    - deal_data
    - conversion_paths

# Website & Conversion Data
- source: analytics
  connector: "{{GOOGLE_ANALYTICS | MIXPANEL | AMPLITUDE}}"
  data:
    - conversion_funnels
    - landing_page_performance
    - email_to_conversion_paths

# Content Assets
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Email Templates/"
    - "/Marketing/Content Library/"
    - "/Marketing/Case Studies/"
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
  data:
    - email_templates
    - case_studies
    - one_pagers

# Brand & Messaging
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Messaging/"
    - "/Marketing/Voice and Tone/"

# Product Information
- source: product_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Product/Feature Documentation/"
    - "/Product/Release Notes/"
```

### Output Destinations

```yaml
# Where to deliver email sequence outputs
outputs:
  # Always available - display in Claude UI (copy/paste)
  - type: display
    enabled: true

  # Push directly to email platform
  - type: email_platform
    connector: "{{HUBSPOT | MARKETO | KLAVIYO | MAILCHIMP}}"
    actions:
      - create_sequence_draft
      - create_email_drafts
      - update_existing_sequence

  # Save to content library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Email Sequences/"

  # Notify team for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#marketing-content"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring email sequence tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every Monday morning, analyze our email sequence performance from the past week,
identify underperforming emails, and suggest improvements. Send the report to
#marketing-content on Slack.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Weekly Performance Review**:
```
Every Monday at 9am, analyze email sequence performance from the past week,
identify emails with below-average open or click rates, and suggest subject
line and content improvements. Post findings to #marketing-content.
```

**Monthly A/B Test Analysis**:
```
On the 1st of each month, review all A/B test results from the past month,
document what we learned about subject lines and CTAs, and update our email
best practices doc in Notion.
```

**Quarterly Sequence Audit**:
```
At the start of each quarter, audit all active email sequences for performance,
relevance, and alignment with current messaging. Flag any sequences with low
engagement or outdated content.
```

**New Blog to Nurture**:
```
Whenever a new blog post is published, generate a 3-email nurture sequence to
promote the content to subscribers who haven't engaged recently. Save drafts
to HubSpot.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Email Platform**: Link your HubSpot, Marketo, or email tool
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Analyze email sequence performance and suggest improvements" |
| `schedule` | When to run (cron or trigger) | "every Monday at 9am" or "when blog is published" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #marketing-content, Notion, email platform" |
| `sequence_type` | Type of sequence to focus on | "nurture", "onboarding", "re-engagement" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "email-sequences"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Email Sequence Types

### 1. Lead Nurture Sequence

**Purpose**: Convert leads to opportunities
**Trigger**: Form submission, content download, trial signup
**Length**: 5-8 emails over 2-4 weeks

**Structure**:
1. Welcome + immediate value
2. Educational content (problem awareness)
3. Social proof (how others succeeded)
4. Product connection (how we help)
5. Case study (specific results)
6. Objection handling
7. Direct offer
8. Final chance/breakup

### 2. Onboarding Sequence

**Purpose**: Activate new users/customers
**Trigger**: Account creation, purchase
**Length**: 5-7 emails over 2 weeks

**Structure**:
1. Welcome + first steps
2. Quick win guidance
3. Key feature introduction
4. Best practices
5. Check-in + support offer
6. Advanced tips
7. Success milestone celebration

### 3. Re-engagement Sequence

**Purpose**: Revive inactive contacts
**Trigger**: No engagement for X days
**Length**: 3-4 emails

**Structure**:
1. We miss you + value reminder
2. What's new + fresh content
3. Special offer or incentive
4. Final email + unsubscribe option

### 4. Event/Webinar Sequence

**Purpose**: Drive registrations and attendance
**Trigger**: Registration or target list
**Length**: 4-6 emails

**Structure**:
- Pre-event: Invitation, reminder (week), reminder (day)
- Post-event: Recording, resources, next steps

### 5. Post-Purchase/Trial Sequence

**Purpose**: Ensure success, drive expansion
**Trigger**: Purchase or trial start
**Length**: Varies by trial length/product

---

## Email Design Principles

### Subject Line Best Practices

**Effective Patterns**:
- Curiosity gap: "The one thing I wish I knew..."
- How-to: "How to [achieve result] in [timeframe]"
- Numbers: "5 ways to improve [outcome]"
- Questions: "Are you making this mistake?"
- Personalization: "[Name], quick question"
- Urgency: "Ending soon: [offer]"

**Subject Line Rules**:
- 40-60 characters
- Preview text complements (doesn't repeat)
- Test variations
- Avoid spam triggers

### Email Structure

**Template**:
```
[Greeting]

[Hook - why should they read?]

[Body - value delivery]

[CTA - single, clear action]

[Sign-off]

[P.S. - secondary CTA or curiosity hook]
```

**Formatting**:
- Short paragraphs (2-3 sentences)
- One idea per paragraph
- Use white space
- Bold key phrases
- Single CTA per email (or primary/secondary)

---

## How to Use This Skill

Invoke with natural language describing the sequence you need:

**Nurture Sequences**
- "Create a lead nurture sequence for people who download our pricing guide"
- "Build a 5-email nurture sequence for enterprise prospects"
- "Design a sequence for leads who attended our webinar but didn't book a demo"

**Onboarding Sequences**
- "Create an onboarding sequence for new trial users"
- "Build a welcome sequence for new customers"
- "Design a 7-day onboarding flow for our SaaS product"

**Re-engagement**
- "Create a re-engagement sequence for leads who went cold"
- "Build a win-back campaign for churned customers"
- "Design a sequence for prospects who ghosted after the demo"

**Event/Campaign**
- "Create a webinar promotion sequence for our upcoming event"
- "Build a product launch email sequence"
- "Design a holiday promotion campaign"

**Optimization**
- "Review and improve our current trial onboarding sequence"
- "Analyze our nurture sequence performance and suggest improvements"
- "Create A/B test variations for our welcome email"

---

## Output Format

### Full Sequence

```markdown
# Email Sequence: [Sequence Name]

**Created**: [Date]
**Data Sources Used**: [Email platform performance, CRM, etc.]

---

## Sequence Overview

| Attribute | Details |
|-----------|---------|
| Type | [Nurture/Onboarding/Re-engagement/etc.] |
| Trigger | [What starts this sequence] |
| Audience | [Who receives it] |
| Goal | [Desired outcome] |
| Length | [# emails over # days] |

### Benchmark Data

*Based on your historical performance:*
- **Average Open Rate**: [%] (your sequences)
- **Average Click Rate**: [%] (your sequences)
- **Conversion Rate**: [%] (this sequence type)

### Success Metrics

| Metric | Target | How to Measure |
|--------|--------|----------------|
| Open Rate | [%] | [Email platform] |
| Click Rate | [%] | [Email platform] |
| Conversion | [Action + %] | [CRM/Analytics] |

---

## Email 1: [Email Name]

**Timing**: Immediately / Day 0
**Goal**: [What this email should accomplish]

### Subject Line Options
1. [Option 1 - primary]
2. [Option 2 - A/B test variant]

### Preview Text
[Preview text that complements subject]

---

**Email Body**:

Hey [First Name],

[Opening hook - why they should care]

[Value delivery - 2-3 short paragraphs]

[Clear CTA]

[Sign-off]
[Name]

P.S. [Optional secondary hook]

---

**CTA Button**: [Button text]
**Link**: [Where it goes]

---

## Email 2: [Email Name]

**Timing**: Day [X] / [X] days after Email 1
**Goal**: [What this email should accomplish]
**Condition**: [If any - e.g., "If didn't click Email 1"]

### Subject Line Options
1. [Option 1]
2. [Option 2]

### Preview Text
[Preview text]

---

**Email Body**:

Hey [First Name],

[Content]

[CTA]

[Sign-off]

---

[Continue for all emails in sequence...]

---

## Email 3: [Email Name]
[Same format]

---

## Email 4: [Email Name]
[Same format]

---

## Email 5: [Email Name]
[Same format]

---

## Sequence Logic & Branching

```
Trigger: [What starts the sequence]
    ↓
Email 1 sent
    ↓
    ├── Clicked CTA → [Tag: Engaged] → [Next action]
    │
    └── No click (Day 3) → Email 2 sent
            ↓
            ├── Clicked → [Tag: Engaged] → [Action]
            │
            └── No click (Day 5) → Email 3 sent
```

---

## Exit Conditions

| Condition | Action |
|-----------|--------|
| Converts to [goal] | Exit + tag "[tag name]" |
| Unsubscribes | Exit sequence |
| Completes sequence | Move to [next sequence] |
| [Days] no engagement | Move to re-engagement |

---

## A/B Test Plan

**Test 1**: Subject Lines
- Control: [Subject A]
- Variant: [Subject B]
- Sample: [% of audience]
- Winner criteria: Open rate after 24 hours

**Test 2**: CTA Placement
- Control: [CTA at end]
- Variant: [CTA mid-email]
- Winner criteria: Click rate

---

## Implementation Checklist

- [ ] Create sequence in [email platform]
- [ ] Set up trigger/enrollment criteria
- [ ] Configure sending schedule
- [ ] Set up goal tracking
- [ ] Create suppression rules
- [ ] Set up A/B tests
- [ ] QA all links and personalization
- [ ] Review with team
- [ ] Schedule activation
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Performance analysis** - Pull actual open/click rates to inform new sequence design
2. **A/B test recommendations** - Suggest tests based on historical performance patterns
3. **Direct publishing** - Push sequence drafts directly to your email platform
4. **Sequence audits** - Analyze existing sequences and recommend improvements
5. **Competitive analysis** - Compare your sequences to industry benchmarks
