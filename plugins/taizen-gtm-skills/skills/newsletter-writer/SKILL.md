---
name: newsletter-writer
description: Creates customer newsletters, product updates, and email communications. Use for ongoing customer engagement and retention marketing.
---

# Newsletter Writer Skill

Create engaging newsletters and email communications for customers and prospects, informed by your content and performance data.

## Purpose

Develop compelling email content that keeps audiences engaged, informed, and connected to your brand.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# NEWSLETTER DATA SOURCES
# Configure the sources relevant to your newsletter creation

# Email Performance Data
- source: email_platform
  connector: "{{HUBSPOT | MAILCHIMP | KLAVIYO | CUSTOMER_IO | CONVERTKIT}}"
  data:
    - past_newsletter_performance
    - open_rates_by_subject
    - click_rates_by_content
    - best_send_times
    - subscriber_segments
    - unsubscribe_patterns

# Content Library (to curate from)
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Blog Posts/"
    - "/Marketing/Case Studies/"
    - "/Marketing/Resources/"
    - "/Marketing/Webinars/"
- source: blog
  url: "{{YOUR_BLOG_URL}}"
  data:
    - recent_posts
    - popular_posts

# Product Updates
- source: product_updates
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE | PRODUCTBOARD}}"
  paths:
    - "/Product/Release Notes/"
    - "/Product/Feature Announcements/"
    - "/Product/Roadmap/"

# Company News & Events
- source: company_updates
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Company/News/"
    - "/Marketing/Events/"
    - "/Company/Announcements/"

# Customer Stories
- source: customer_stories
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Customer Spotlights/"
    - "/Marketing/Case Studies/"
    - "/Marketing/Testimonials/"

# Brand Guidelines
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Email Templates/"
    - "/Marketing/Voice and Tone/"

# Industry News (for curation)
- source: industry_feeds
  enabled: true
  sources:
    - rss_feeds
    - google_alerts
  topics:
    - "{{INDUSTRY_KEYWORD_1}}"
    - "{{INDUSTRY_KEYWORD_2}}"
```

### Output Destinations

```yaml
# Where to deliver newsletter outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Push to email platform
  - type: email_platform
    connector: "{{HUBSPOT | MAILCHIMP | KLAVIYO | CUSTOMER_IO}}"
    actions:
      - create_email_draft
      - schedule_send

  # Save to content archive
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Newsletters/"

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#marketing-review"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring newsletter tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every Tuesday at 9am, generate a draft of our weekly newsletter pulling from
recent blog posts, product updates, and customer stories. Save the draft to
HubSpot and post to #marketing-review for feedback.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Weekly Newsletter Draft**:
```
Every Tuesday at 9am, generate a draft of our weekly newsletter pulling from
recent blog posts, product updates, and customer stories. Create a draft in
HubSpot and post to #marketing-review.
```

**Monthly Customer Newsletter**:
```
On the 1st of each month, create our monthly customer newsletter with product
updates, customer spotlights, and upcoming events. Save as a draft in our
email platform for review.
```

**Post-Send Performance Analysis**:
```
48 hours after we send a newsletter, automatically analyze the performance
including open rates, click rates, and top clicked links. Post insights to
#marketing-content.
```

**Quarterly Newsletter Retrospective**:
```
At the start of each quarter, review last quarter's newsletter performance,
identify our top performing content and subject lines, and update our best
practices doc with learnings.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Email Platform**: Link your HubSpot, Mailchimp, or Klaviyo
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Generate weekly newsletter draft from recent content" |
| `schedule` | When to run (cron or trigger) | "every Tuesday at 9am" or "48 hours after newsletter sent" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "HubSpot draft, Slack #marketing-review" |
| `newsletter_type` | Type of newsletter | "weekly digest", "monthly customer update" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "newsletter-writer"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Newsletter Types

### 1. Customer Newsletter

**Purpose**: Keep customers engaged and informed
**Frequency**: Monthly or bi-weekly
**Content Mix**:
- Product updates and tips
- Customer success stories
- Educational content
- Community highlights
- Upcoming events

### 2. Product Update

**Purpose**: Announce new features and improvements
**Frequency**: As needed (major releases)
**Content Mix**:
- What's new
- How to use it
- Why it matters
- What's coming next

### 3. Thought Leadership

**Purpose**: Build authority and trust
**Frequency**: Weekly or bi-weekly
**Content Mix**:
- Industry insights
- Original research
- Expert perspectives
- Curated content

### 4. Event/Webinar Promotion

**Purpose**: Drive registrations
**Frequency**: As needed
**Content Mix**:
- Event details
- Speaker highlights
- Key takeaways preview
- Registration CTA

### 5. Nurture Sequence

**Purpose**: Move prospects through funnel
**Frequency**: Automated based on triggers
**Content Mix**:
- Educational content
- Social proof
- Product information
- Soft CTAs

---

## Newsletter Best Practices

### Subject Lines

**Formulas That Work**:
- **Curiosity**: "The one thing top [role]s do differently"
- **Benefit**: "How to [achieve result] in [timeframe]"
- **News**: "[Topic] just changed. Here's what it means"
- **List**: "[Number] ways to [achieve outcome]"
- **Question**: "Are you making this [topic] mistake?"

**Guidelines**:
- 40-60 characters
- Front-load important words
- Avoid spam triggers
- Test variations

### Email Structure

**Inverted Pyramid**:
1. Hook (why open)
2. Value (why care)
3. Details (what to know)
4. CTA (what to do)

**Scannable Format**:
- Clear headers
- Short paragraphs (2-3 sentences)
- Bullet points
- Bold key phrases
- Single clear CTA

---

## How to Use This Skill

Invoke with natural language describing the newsletter you need:

**Customer Newsletters**
- "Write our monthly customer newsletter - pull from recent blog posts and product updates"
- "Create this week's newsletter featuring our new case study"
- "Draft a newsletter about our upcoming user conference"

**Product Updates**
- "Write a product update email announcing our new dashboard feature"
- "Create a release notes email for version 2.0"
- "Draft a feature spotlight email for our AI capabilities"

**Thought Leadership**
- "Write a thought leadership newsletter on the future of [industry]"
- "Create a weekly digest curating the best articles on [topic]"
- "Draft an insights newsletter based on our recent survey data"

**Promotions**
- "Write a webinar promotion email for our upcoming event"
- "Create an event invitation for our annual conference"
- "Draft a series of emails promoting our new e-book"

---

## Output Format

### Customer Newsletter

```markdown
# Newsletter: [Edition Name/Number]

**Created**: [Date]
**Data Sources Used**: [Email performance, content library, etc.]

---

## Email Details
- **Audience**: [Segment]
- **Send Date**: [Date]
- **Send Time**: [Time - based on your best performing times]

### Performance Context
*Based on your newsletter data:*
- Average open rate: [%]
- Average click rate: [%]
- Best performing content type: [Type]

---

## Subject Line Options

1. [Option 1] - [Why this might work based on your data]
2. [Option 2]
3. [Option 3]

**A/B Test Recommendation**: Test [Option X] vs [Option Y]

## Preview Text Options

1. [Preview that complements subject 1]
2. [Preview that complements subject 2]

---

## Email Content

### Header
[Logo + Edition identifier: e.g., "The Monthly Update | April 2025"]

---

### Opening

Hey [First Name],

[1-2 sentence hook that's timely and relevant - connects to what's happening in their world]

[Brief intro to what's in this edition - create anticipation]

---

### Section 1: [Featured Content]

**[Headline - benefit-focused]**

[2-3 paragraphs of valuable content - pulled from your blog/resources]

[Key insight or takeaway]

**[CTA Button: "Read More" / "Learn How" / etc.]**

---

### Section 2: [Product/Feature Highlight]

**[What's New: Feature Name]**

[Brief description of what it is and why it matters to them]

✓ [Benefit 1]
✓ [Benefit 2]
✓ [Benefit 3]

**[CTA: "Try It Now" / "See How It Works"]**

---

### Section 3: [Customer Spotlight]

**How [Customer Name] achieved [Result]**

> "[Customer quote about their success]"
> — [Name], [Title] at [Company]

[Brief context on their achievement - 2-3 sentences]

**[CTA: "Read the Full Story"]**

---

### Section 4: [Quick Hits / Resources]

**Worth Your Time:**

📚 **[Resource 1 Title]**: [One-line description]
→ [Read it]

🎙 **[Resource 2 Title]**: [One-line description]
→ [Listen/Watch]

📊 **[Resource 3 Title]**: [One-line description]
→ [Download]

---

### Section 5: [Upcoming Events]

**Don't Miss:**

🗓 **[Event 1]** | [Date]
[One-line description]
→ [Register]

🗓 **[Event 2]** | [Date]
[One-line description]
→ [Save your spot]

---

### Closing

[Personal sign-off - human and warm]

[Looking forward to next time / invitation to reply / etc.]

[Your Name]
[Title]

P.S. [Secondary CTA or teaser for next edition]

---

### Footer
[Unsubscribe] | [Email Preferences] | [Social Links]
[Company Address]

---

## Technical Details

- **From Name**: [Name]
- **From Email**: [email]
- **Reply-To**: [email]
- **Preheader**: [Preview text]

## Tracking

- UTM Campaign: [campaign name]
- Primary CTA Goal: [What you're measuring]
```

### Product Update Email

```markdown
# Product Update: [Feature/Release Name]

**Created**: [Date]

---

## Email Details
- **Audience**: [All customers / Specific segment]
- **Timing**: [Immediate / Scheduled]

---

## Subject Line Options

1. 🚀 New: [Feature Name] is here
2. Introducing [Feature Name] – [Key Benefit]
3. You asked, we built: [Feature Name]

## Preview Text
[Complement subject - expand on the benefit]

---

## Email Content

### Header
🚀 Product Update

---

### Headline
**[Feature Name]: [One-line benefit statement]**

---

### Opening

Hey [First Name],

We're excited to announce [Feature Name] – [brief description of what it does and why it matters].

[1-2 sentences on the problem this solves or opportunity it creates - connect to customer feedback if applicable]

---

### What's New

**[Capability 1]**
[Brief description + benefit - how it helps them]

**[Capability 2]**
[Brief description + benefit]

**[Capability 3]**
[Brief description + benefit]

[Visual: Screenshot or GIF showing the feature]

---

### How to Get Started

Getting started is easy:

1. [Step 1]
2. [Step 2]
3. [Step 3]

**[CTA Button: "Try It Now"]**

---

### Learn More

📖 **Documentation**: [Step-by-step guide]
🎥 **Video Walkthrough**: [2-minute overview]
💬 **Questions?**: [Reach out to support]

---

### Coming Soon

We're not stopping here. Here's what's on the roadmap:
- [Upcoming feature 1]
- [Upcoming feature 2]

---

### We Want Your Feedback

Have thoughts on [Feature Name]? We'd love to hear from you.
→ [Share Feedback]

[Sign-off]
[Your Name]

---

### Footer
[Standard footer]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Content curation** - Automatically pull recent blog posts, case studies, and product updates
2. **Performance-informed** - Use your actual open/click rates to optimize subject lines and content
3. **Direct publishing** - Push drafts directly to HubSpot, Mailchimp, or Klaviyo
4. **Optimal timing** - Schedule sends based on your best performing send times
5. **A/B test setup** - Configure subject line tests in your email platform
6. **Archive management** - Save sent newsletters to your content library
