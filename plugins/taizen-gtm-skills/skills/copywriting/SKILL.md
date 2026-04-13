---
name: copywriting
description: Writes marketing copy for landing pages, ads, CTAs, and promotional content. Use for conversion-focused copy that drives action.
---

# Copywriting Skill

Create persuasive copy that converts visitors into leads and customers.

## Purpose

Write clear, compelling copy that communicates value and motivates action across all marketing touchpoints.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# COPYWRITING DATA SOURCES
# Configure the sources relevant to your copywriting needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Brand & Messaging Guidelines
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Messaging Framework/"
    - "/Marketing/Voice and Tone/"
    - "/Marketing/Value Propositions/"

# Product Information
- source: product_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Product/Feature Documentation/"
    - "/Product/Benefits/"
    - "/Product/Use Cases/"

# Customer Research
- source: customer_research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Customer Interviews/"
    - "/Research/Voice of Customer/"
    - "/Research/Persona Documents/"

# Performance Data
- source: analytics
  connector: "{{GOOGLE_ANALYTICS | MIXPANEL | AMPLITUDE}}"
  data:
    - landing_page_performance
    - conversion_rates
    - bounce_rates
    - top_performing_pages

# Ad Performance
- source: ad_platforms
  connector: "{{GOOGLE_ADS | FACEBOOK_ADS | LINKEDIN_ADS}}"
  data:
    - top_performing_ads
    - ad_copy_performance
    - ctr_benchmarks

# Existing Copy Library
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Landing Pages/"
    - "/Marketing/Ad Copy/"
    - "/Marketing/Email Templates/"

# Website Content
- source: website
  url: "{{YOUR_WEBSITE_URL}}"
  pages:
    - homepage
    - product_pages
    - pricing
    - about

# Customer Testimonials & Proof
- source: proof_points
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Testimonials/"
    - "/Marketing/Case Studies/"
    - "/Marketing/Social Proof/"
```

### Output Destinations

```yaml
# Where to deliver copywriting outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to content library
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Copy/"

  # Push to CMS (if direct integration exists)
  - type: cms
    connector: "{{WEBFLOW | WORDPRESS | CONTENTFUL}}"
    action: create_draft

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#marketing-content"
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
- Content brief or topic to write about
- Target audience or use case
- `display` output enabled (always available)

Enhanced functionality requires:
- Brand voice guidelines for tone consistency
- Messaging framework for value prop alignment
- Approved copy examples for style matching
- Product documentation for accuracy

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring copywriting tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, analyze landing page performance data, identify pages
with low conversion rates, and generate copy improvement recommendations. Post
findings to #marketing-content.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Landing Page Review**:
```
On the 1st of each month, analyze landing page performance data, identify
underperforming pages with high bounce rates or low conversions, and generate
copy improvement recommendations. Alert me on Slack with the findings.
```

**Ad Copy Refresh**:
```
Every two weeks, generate new ad copy variations based on our top performing
ads and any recent messaging updates. Save to Google Drive and post to
#paid-media for review.
```

**Campaign Copy Generation**:
```
When a new campaign brief is submitted, automatically generate landing page
copy, ad variations, and email copy aligned with our brand guidelines. DM the
requester with the drafts.
```

**Quarterly Value Prop Review**:
```
At the start of each quarter, review and update our value propositions based
on latest customer research, win/loss data, and competitive positioning. Notify
#product-marketing when complete.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Analytics**: Link your Google Analytics or conversion data
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Analyze landing page performance and suggest copy improvements" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when campaign brief submitted" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #marketing-content, Google Drive" |
| `pages` | Which pages to focus on | "all landing pages" or "pricing page" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "copywriting"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Copywriting Frameworks

### 1. AIDA (Attention-Interest-Desire-Action)

Classic framework for any persuasive content:

- **Attention**: Grab them with a headline/hook
- **Interest**: Keep them reading with relevance
- **Desire**: Build want with benefits and proof
- **Action**: Tell them exactly what to do

### 2. PAS (Problem-Agitate-Solution)

Effective for pain-focused copy:

- **Problem**: Name the problem they face
- **Agitate**: Amplify the pain/consequences
- **Solution**: Present your solution as the answer

### 3. BAB (Before-After-Bridge)

Great for transformation messaging:

- **Before**: Where they are now (pain state)
- **After**: Where they could be (dream state)
- **Bridge**: How you get them there

### 4. 4 Ps (Promise-Picture-Proof-Push)

Strong for landing pages:

- **Promise**: Bold claim/outcome
- **Picture**: Paint the vivid future
- **Proof**: Back it up with evidence
- **Push**: Clear call to action

---

## Copy Elements

### Headlines

**Headline Formulas**:
- How to [Achieve Desirable Outcome]
- [Number] Ways to [Get Benefit]
- The Secret to [Achieving Goal]
- Why [Surprising Statement]
- [Do This], [Get This Result]
- Stop [Pain Point]. Start [Benefit].
- [Outcome] Without [Typical Obstacle]

**4 U's of Headlines**:
- Useful (provides value)
- Urgent (creates timeliness)
- Unique (differentiates)
- Ultra-specific (concrete, not vague)

### CTAs (Calls to Action)

**CTA Best Practices**:
- Action-oriented verbs (Get, Start, Try, Discover)
- Benefit-focused (Get My Free Guide vs. Submit)
- Create urgency when appropriate
- Reduce friction (Free, No Credit Card)
- One primary CTA per section/page

**CTA Examples by Goal**:
| Goal | Weak | Strong |
|------|------|--------|
| Download | Submit | Get My Free Guide |
| Demo | Request Demo | See It in Action |
| Trial | Start Trial | Start Free Trial |
| Purchase | Buy Now | Get Started Today |
| Contact | Contact Us | Talk to an Expert |

### Value Propositions

**Value Prop Formula**:
We help [target customer] [achieve outcome] by/with [unique approach] unlike [alternative].

---

## How to Use This Skill

Invoke with natural language describing what copy you need:

**Headlines**
- "Write 10 headline options for our new product landing page"
- "Create headlines for a B2B SaaS homepage targeting CTOs"
- "Generate A/B test headline variations for our pricing page"

**Landing Pages**
- "Write copy for a landing page promoting our free trial"
- "Create a landing page for our webinar registration"
- "Write a product page for our enterprise solution"

**Ad Copy**
- "Create Google Ads copy for our CRM product"
- "Write LinkedIn ad variations targeting HR leaders"
- "Generate Facebook ad copy for our e-book download"

**CTAs**
- "Give me 5 CTA button options for our demo request page"
- "Create compelling CTAs for our pricing page"

**Improvements**
- "Review and improve this landing page copy: [paste]"
- "Make this headline more compelling: [paste]"
- "Rewrite this value proposition to be clearer"

---

## Output Format

### Landing Page Copy

```markdown
# Landing Page Copy: [Page Name/Offer]

**Created**: [Date]
**Data Sources Used**: [Brand guidelines, customer research, etc.]

---

## Page Purpose
- **Goal**: [Primary conversion goal]
- **Audience**: [Who this is for]
- **Offer**: [What they get]
- **Key Message**: [From your messaging framework]

---

## Hero Section

### Headline Options
1. [Option 1 - benefit focused]
2. [Option 2 - problem focused]
3. [Option 3 - outcome focused]

**Recommended**: [Which one and why]

### Subhead
[Supporting statement that expands on the headline]

### Hero CTA
[Button text] → [Where it goes]

### Trust Bar
[Logos: Customer 1, Customer 2, Customer 3]
[Or: "Trusted by X,000+ companies"]

---

## Problem Section

### Section Header
[Header that names the pain]

### Problem Copy
[2-3 paragraphs that agitate the pain, show you understand, make them feel seen]

*Voice of Customer Quote*:
> "[Actual quote from customer research that captures the pain]"

---

## Solution Section

### Section Header
[Header that introduces your approach]

### Solution Copy
[2-3 paragraphs explaining how you solve it - using your actual value props]

### Key Benefits
- **[Benefit 1]**: [Brief explanation]
- **[Benefit 2]**: [Brief explanation]
- **[Benefit 3]**: [Brief explanation]

---

## Social Proof Section

### Customer Quote
> "[Testimonial from your testimonial database]"
> — [Name, Title, Company]

### Results/Stats
- [Stat 1 from your case studies]
- [Stat 2]
- [Stat 3]

---

## FAQ Section

### [Common question 1]
[Answer - objection handling]

### [Common question 2]
[Answer]

---

## Final CTA Section

### Header
[Compelling close]

### Body Copy
[Final pitch - summarize value, reduce risk]

### CTA Button
[Button text]

### Risk Reversal
[Guarantee, free trial, no commitment, etc.]

---

## Meta Information
- **Page Title**: [SEO title - 60 chars]
- **Meta Description**: [Meta description - 160 chars]
```

### Ad Copy

```markdown
# Ad Copy: [Campaign/Product]

**Created**: [Date]
**Data Sources Used**: [Ad performance data, brand guidelines, etc.]

---

## Campaign Details
- **Platform**: [Google/Facebook/LinkedIn/etc.]
- **Objective**: [Awareness/Traffic/Conversions]
- **Audience**: [Who we're targeting]
- **Offer**: [What we're promoting]

### Performance Context
*Based on your ad performance data:*
- **Best performing hook style**: [From your data]
- **Top CTR ads used**: [Pattern from your data]

---

## Ad Variations

### Variation 1: [Approach - e.g., "Benefit-focused"]

**Headline**: [Headline text]
**Description**: [Description text]
**CTA**: [Button/action]
**Visual Direction**: [Image/video guidance]

**Why this approach**: [Based on what's worked]

---

### Variation 2: [Approach - e.g., "Problem-focused"]

**Headline**: [Headline text]
**Description**: [Description text]
**CTA**: [Button/action]
**Visual Direction**: [Image/video guidance]

---

### Variation 3: [Approach - e.g., "Social proof"]

**Headline**: [Headline text]
**Description**: [Description text]
**CTA**: [Button/action]
**Visual Direction**: [Image/video guidance]

---

## Character Counts
| Element | Variation 1 | Variation 2 | Variation 3 | Limit |
|---------|-------------|-------------|-------------|-------|
| Headline | [X] | [X] | [X] | [Limit] |
| Description | [X] | [X] | [X] | [Limit] |

## A/B Test Recommendation
Test [Variation X] vs [Variation Y] first because [reason based on your data].
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Brand consistency** - Automatically apply your brand voice and messaging guidelines
2. **Performance-informed** - Use your actual conversion data to inform copy decisions
3. **Proof point insertion** - Pull relevant testimonials and stats from your database
4. **A/B test generation** - Create test variants based on what's worked before
5. **Multi-platform adaptation** - Repurpose copy for different channels with proper formatting
