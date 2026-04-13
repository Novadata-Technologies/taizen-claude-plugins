---
name: social-content
description: Creates social media posts, content calendars, and platform-specific content. Use for social media marketing and brand presence.
---

# Social Content Skill

Create engaging social media content across platforms.

## Purpose

Develop platform-optimized social content that builds brand awareness, engages audiences, and drives business results.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# SOCIAL CONTENT DATA SOURCES
# Configure the sources relevant to your social media marketing

# Social Media Performance
- source: social_analytics
  connector: "{{SPROUT_SOCIAL | HOOTSUITE | BUFFER | NATIVE_ANALYTICS}}"
  data:
    - post_performance
    - engagement_rates
    - best_posting_times
    - top_performing_content
    - audience_insights
    - competitor_benchmarks

# Brand & Voice Guidelines
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Social Media Guidelines/"
    - "/Marketing/Voice and Tone/"
    - "/Marketing/Approved Hashtags/"

# Content Library
- source: content_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Blog Posts/"
    - "/Marketing/Case Studies/"
    - "/Marketing/Webinars/"
    - "/Marketing/Product Updates/"

# Company News & Updates
- source: company_updates
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | SLACK}}"
  data:
    - product_launches
    - company_news
    - team_updates
    - event_calendar

# Customer Stories
- source: customer_content
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Customer Stories/"
    - "/Marketing/Testimonials/"
    - "/Marketing/User Generated Content/"

# Industry News
- source: industry_feeds
  enabled: true  # RSS feeds, Google Alerts
  topics:
    - "{{INDUSTRY_KEYWORD_1}}"
    - "{{INDUSTRY_KEYWORD_2}}"

# Visual Assets
- source: asset_library
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | DROPBOX | DAM}}"
  paths:
    - "/Marketing/Social Assets/"
    - "/Marketing/Graphics/"
    - "/Marketing/Videos/"
```

### Output Destinations

```yaml
# Where to deliver social content outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Push to social scheduling tool
  - type: social_scheduler
    connector: "{{SPROUT_SOCIAL | HOOTSUITE | BUFFER | LATER}}"
    actions:
      - create_draft_posts
      - schedule_posts
      - add_to_calendar

  # Save to content calendar
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Social Content Calendar/"

  # Design request for visuals
  - type: slack
    connector: "{{SLACK}}"
    channel: "#design-requests"
    template: social_visual_request
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
- Content topic or campaign theme
- Target platform (LinkedIn, Twitter, etc.)
- `display` output enabled (always available)

Enhanced functionality requires:
- Brand voice guidelines for tone
- Social media management platform for scheduling
- Analytics for performance optimization
- Content calendar for coordination

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring social content tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every Friday morning, generate next week's social content calendar based on
upcoming blog posts, events, and our best performing content types. Save
drafts to Buffer and post the calendar to #social-media.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Weekly Content Calendar**:
```
Every Friday at 9am, generate next week's social content calendar based on
upcoming content, events, and performance data. Save to Notion and create
draft posts in Sprout Social.
```

**Daily Performance Review**:
```
Every morning at 9am, review yesterday's social post performance and identify
what worked and what didn't. Post a quick summary to #social-media with
learnings.
```

**Blog to Social Repurposing**:
```
Whenever a new blog post is published, automatically create LinkedIn posts,
Twitter threads, and Instagram carousel concepts to promote it. Save drafts
to our social scheduler and DM the content owner.
```

**Event Promotion Sequence**:
```
When a new webinar or event is created, automatically generate a social
promotion sequence with pre-event, day-of, and post-event content for
LinkedIn and Twitter.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Social Tools**: Link your Sprout Social, Buffer, or Hootsuite
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Generate weekly social content calendar" |
| `schedule` | When to run (cron or trigger) | "every Friday at 9am" or "when blog is published" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #social-media, Buffer drafts, Notion" |
| `platforms` | Which social platforms | "LinkedIn, Twitter, Instagram" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "social-content"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Platform Guidelines

### LinkedIn

**Best Practices**:
- Professional but personable tone
- First line is the hook (shows in preview)
- Use line breaks for readability
- 1,200-1,500 characters optimal
- Native video/carousels outperform links
- Post frequency: 1-2x daily (business hours)

**Content Types That Work**:
- Industry insights and hot takes
- Personal stories with business lessons
- Data/research with commentary
- Carousel educational content
- Polls and questions
- Company/team milestones

### Twitter/X

**Best Practices**:
- Conversational, punchy tone
- Thread format for longer ideas
- Images increase engagement 150%
- Timing matters (lunch, evening)
- Engage with replies

**Content Types**:
- Hot takes and opinions
- Threads (educational, stories)
- Quote tweets with commentary
- Polls
- Behind-the-scenes

### Instagram

**Best Practices**:
- Visual-first platform
- Captions up to 2,200 chars
- First 125 chars show in preview
- Carousel posts have highest engagement
- Stories for real-time content
- Reels for discovery

### TikTok

**Best Practices**:
- Entertainment first
- Trend participation
- Authentic/unpolished preferred
- First 3 seconds critical
- Text overlays important

---

## Content Pillars

### Educational (40%)
- Tips and how-tos
- Industry insights
- Best practices
- Data and research

### Engaging (30%)
- Questions and polls
- Hot takes
- Behind-the-scenes
- Team/culture content

### Promotional (20%)
- Product features
- Customer stories
- Company news
- Events/webinars

### Curated (10%)
- Industry news with commentary
- Partner content
- User-generated content

---

## How to Use This Skill

Invoke with natural language describing what content you need:

**Individual Posts**
- "Write a LinkedIn post about our new product feature"
- "Create a Twitter thread on the top 5 trends in B2B sales"
- "Write an engaging LinkedIn post about this blog article: [link/title]"
- "Create a celebratory post - we just hit 10,000 customers"

**Content Calendars**
- "Create a social content calendar for October"
- "Build a week of LinkedIn content around our product launch"
- "Plan a month of social content for our awareness campaign"

**Repurposing**
- "Turn this blog post into social content for LinkedIn and Twitter"
- "Repurpose our webinar into a LinkedIn carousel and Twitter thread"
- "Create 10 social posts from this case study"

**Engagement**
- "Write a LinkedIn poll about [topic]"
- "Create a discussion-starting post for our community"
- "Generate conversation starters for Twitter"

**Platform Adaptation**
- "Adapt this LinkedIn post for Twitter"
- "Turn this Twitter thread into a LinkedIn article outline"

---

## Output Format

### LinkedIn Post

```markdown
# LinkedIn Post: [Topic]

**Created**: [Date]
**Data Sources Used**: [Performance data, brand guidelines, etc.]

---

## Post Details
- **Hook Type**: [Question/Statement/Data/Story]
- **Content Pillar**: [Educational/Engaging/Promotional]
- **Goal**: [Awareness/Engagement/Traffic/Leads]

### Performance Context
*Based on your LinkedIn data:*
- Your avg engagement rate: [%]
- Best performing hook style: [Type]
- Best posting time: [Time]

---

## Post Copy

[Hook: First line that appears in preview - make it count]

[Blank line for readability]

[Body paragraph 1: Set up the context or problem]

[Body paragraph 2: Share the insight, story, or value]

[Body paragraph 3: Key takeaway or learning]

[Blank line]

[CTA: Question or call to action to drive comments]

---

#hashtag1 #hashtag2 #hashtag3 #hashtag4 #hashtag5

---

## Visual Recommendation
[Image/carousel/video suggestion with creative direction]

## Engagement Strategy
- **Best time to post**: [Time based on your data]
- **First comment**: [Comment to post immediately to boost engagement]
- **Tag**: [Anyone to tag?]

## Alternative Version
[A/B test variant with different hook]
```

### Twitter/X Thread

```markdown
# Twitter Thread: [Topic]

**Created**: [Date]

---

## Thread Overview
- **Topic**: [What it's about]
- **Length**: [Number of tweets]
- **Goal**: [What we want readers to do/learn]

---

## Thread

**Tweet 1 (Hook)**
[Compelling opening that promises value - under 280 chars]

🧵

↓

**Tweet 2**
[First point - clear and punchy]

↓

**Tweet 3**
[Second point with detail or example]

↓

**Tweet 4**
[Third point - build momentum]

↓

**Tweet 5**
[Fourth point or pivot]

↓

**Tweet 6 (Conclusion)**
[Summary + CTA]

If this was helpful:
• Follow @[handle] for more
• Retweet tweet 1 to share

---

## Media Suggestions
- Tweet [#]: [Image/GIF suggestion]

## Engagement Strategy
- **Best time to post**: [Time]
- **Engagement**: Reply to comments within first hour
```

### Content Calendar

```markdown
# Social Content Calendar: [Month/Period]

**Created**: [Date]
**Data Sources Used**: [Performance analytics, content library, etc.]

---

## Monthly Overview

**Theme**: [Overarching theme if any]

**Key Dates**:
- [Date]: [Event/Holiday/Launch]
- [Date]: [Event/Holiday/Launch]

## Content Mix Target
Based on your best performing content:
- Educational: [X] posts ([%])
- Engaging: [X] posts ([%])
- Promotional: [X] posts ([%])
- Curated: [X] posts ([%])

---

## Week 1: [Date Range]

### Monday - [Date]
| Platform | Post Type | Topic | Pillar | Asset Needed | Status |
|----------|-----------|-------|--------|--------------|--------|
| LinkedIn | [Type] | [Topic] | [Pillar] | [Yes/No] | Draft |
| Twitter | [Type] | [Topic] | [Pillar] | [Yes/No] | Draft |

**LinkedIn Post**:
> [Full post copy]

**Twitter Post**:
> [Full tweet]

### Tuesday - [Date]
[Same format]

### Wednesday - [Date]
[Same format]

### Thursday - [Date]
[Same format]

### Friday - [Date]
[Same format]

---

## Week 2: [Date Range]
[Same structure]

---

## Visual Assets Needed

| Post Date | Platform | Asset Description | Dimensions | Designer |
|-----------|----------|-------------------|------------|----------|
| [Date] | LinkedIn | [Description] | 1200x627 | [Name] |
| [Date] | Twitter | [Description] | 1600x900 | [Name] |

---

## Content Backlog
Ideas for future weeks:
- [ ] [Idea 1]
- [ ] [Idea 2]
- [ ] [Idea 3]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Performance-informed content** - Use your actual engagement data to guide content creation
2. **Optimal timing** - Schedule posts based on when your audience is most active
3. **Direct scheduling** - Push drafts to Sprout Social, Hootsuite, or Buffer
4. **Content repurposing** - Automatically adapt content across platforms
5. **Calendar sync** - Keep your content calendar updated in Notion/Sheets
6. **Design briefs** - Auto-generate design requests in Slack for visual assets
