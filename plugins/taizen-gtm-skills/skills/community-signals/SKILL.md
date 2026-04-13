---
name: community-signals
description: Monitors and summarizes community feedback, social signals, and customer sentiment. Use for intelligence gathering and trend spotting.
---

# Community Signals Skill

Capture and analyze signals from customer communities, social media, and review sites.

## Purpose

Synthesize community feedback into actionable intelligence for product, marketing, and sales teams.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# COMMUNITY SIGNALS DATA SOURCES
# Configure the sources relevant to your community monitoring

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - slack_history

# Social Listening
- source: social_listening
  connector: "{{SPROUT_SOCIAL | HOOTSUITE | BRANDWATCH}}"
  data:
    - brand_mentions
    - competitor_mentions
    - sentiment_data
    - influencer_activity

# Review Sites
- source: review_sites
  sources:
    - g2
    - capterra
    - trustradius
    - gartner_peer_insights
  data:
    - reviews
    - ratings
    - competitive_comparisons

# Community Platforms
- source: community
  connector: "{{DISCOURSE | SLACK | DISCORD | CIRCLE}}"
  data:
    - discussions
    - feature_requests
    - user_feedback

# Support Data
- source: support
  connector: "{{ZENDESK | INTERCOM | FRESHDESK}}"
  data:
    - ticket_themes
    - customer_feedback
    - satisfaction_scores

# NPS/Survey Data
- source: surveys
  connector: "{{DELIGHTED | TYPEFORM | SURVEYMONKEY}}"
  data:
    - nps_scores
    - verbatim_responses
    - satisfaction_trends
```

### Output Destinations

```yaml
# Where to deliver community signal outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save reports
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Community Intelligence/"

  # Alert channels
  - type: slack
    connector: "{{SLACK}}"
    channels:
      signals: "#community-signals"
      competitive: "#competitive-intel"
      escalations: "#customer-escalations"
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
- Brand/product name to monitor
- `display` output enabled (always available)
- Web search provides public social mentions without additional setup

Enhanced functionality requires:
- Social listening platform connection
- Community platform access (Discord, Slack communities)
- Review site integrations (G2, Capterra)
- Reddit/Twitter API access for deeper analysis

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule community monitoring tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every morning at 8am, scan community channels, reviews, and social for notable
signals from the past 24 hours. Alert me on Slack if there are any negative
sentiment spikes, competitor mentions, or influencer activity.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Daily Signal Scan**:
```
Every morning at 8am, scan community channels, reviews, and social for notable
signals from the past 24 hours. Post to #community-signals and alert me if
there are negative sentiment spikes or competitor mentions.
```

**Weekly Community Digest**:
```
Every Monday at 9am, generate a weekly community signals digest with sentiment
trends, top themes, and action items. Share with #community-signals.
```

**New Review Alert**:
```
When a new customer review is posted on G2 or Capterra, analyze it and alert
#reviews if it's negative or mentions a competitor. Include suggested response.
```

**Monthly Sentiment Report**:
```
On the 1st of each month, generate a monthly sentiment analysis with trends,
competitive intelligence, and strategic recommendations. Share with #marketing.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Social Tools**: Link your social listening and review platforms
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Scan for community signals and sentiment trends" |
| `schedule` | When to run (cron or trigger) | "every morning at 8am" or "when new review posted" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #community-signals, Notion" |
| `sources` | Which sources to monitor | "G2, Reddit, Twitter, Slack community" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "community-signals"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Signal Sources

### 1. Community Channels

**Owned Communities**:
- Customer Slack/Discord
- Community forums
- User groups
- Customer advisory boards

**External Communities**:
- Reddit (relevant subreddits)
- LinkedIn groups
- Industry forums
- Stack Overflow
- GitHub discussions

### 2. Review Sites

**B2B Software**:
- G2
- Capterra
- TrustRadius
- Gartner Peer Insights
- Software Advice

**General**:
- Trustpilot
- BBB
- Industry-specific sites

### 3. Social Media

**Platforms**:
- LinkedIn (company, executives)
- Twitter/X
- YouTube comments
- Industry podcasts

**Signals to Track**:
- Brand mentions
- Competitor mentions
- Industry trends
- Influencer opinions
- Customer sentiment

### 4. Support & Feedback

**Sources**:
- Support tickets
- Feature requests
- NPS verbatims
- Survey responses
- Sales call notes

---

## Analysis Framework

### Sentiment Categories

| Category | Indicators | Action |
|----------|------------|--------|
| **Positive** | Praise, recommendations, success stories | Amplify, case study |
| **Neutral** | Questions, comparisons, evaluations | Engage, educate |
| **Negative** | Complaints, frustrations, churn signals | Address, escalate |
| **Competitive** | Competitor mentions, comparisons | Intel, battlecard |

### Theme Clustering

Group signals into themes:
- Product features/gaps
- Customer experience
- Pricing/value
- Competitive positioning
- Market trends

### Signal Strength

| Strength | Criteria |
|----------|----------|
| **High** | Multiple sources, influential voices, recurring |
| **Medium** | Several mentions, specific feedback |
| **Low** | One-off mentions, low influence |

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Signal Digest**
- "Generate this week's community signals digest"
- "What are people saying about us on G2?"
- "Summarize Reddit discussions about our category"

**Sentiment Analysis**
- "Analyze sentiment around our latest feature launch"
- "What's the sentiment trend over the past month?"

**Competitive Intelligence**
- "What are people saying about Competitor X?"
- "How are we being compared to competitors on review sites?"

**Trend Spotting**
- "What emerging topics are trending in our community?"
- "Identify new pain points customers are discussing"

---

## Output Format

### Weekly Signal Digest

```markdown
# Community Signals Digest: [Date Range]

**Created**: [Date]
**Data Sources Used**: [G2, Reddit, Slack community, etc.]

---

## Executive Summary

**Overall Sentiment**: [Positive/Neutral/Negative trend]
**Key Theme**: [Most important signal this period]
**Action Needed**: [Top priority item]

---

## Signal Overview

| Category | Volume | Trend | Highlight |
|----------|--------|-------|-----------|
| Positive | [#] | [↑↓→] | [Key example] |
| Neutral | [#] | [↑↓→] | [Key example] |
| Negative | [#] | [↑↓→] | [Key example] |
| Competitive | [#] | [↑↓→] | [Key example] |

---

## Positive Signals

### Wins & Praise

**[Signal 1]**
- **Source**: [Where]
- **Signal**: [What was said]
- **Reach**: [Influence/reach]
- **Action**: [Amplify/Case study/Thank]

### Success Stories
- [Customer] shared [result] on [platform]
- [Influencer] recommended us for [use case]

---

## Negative Signals

### Issues & Complaints

**[Signal 1]**
- **Source**: [Where]
- **Signal**: [What was said]
- **Severity**: [High/Medium/Low]
- **Root Cause**: [If known]
- **Action**: [Response/Escalation]
- **Owner**: [Who handles]

### Themes in Negative Feedback
| Theme | Volume | Trend | Status |
|-------|--------|-------|--------|
| [Theme 1] | [#] | [↑↓→] | [Addressed/In progress/New] |

---

## Competitive Intelligence

### Competitor Mentions

| Competitor | Mentions | Sentiment | Key Signal |
|------------|----------|-----------|------------|
| [Comp 1] | [#] | [Pos/Neg] | [Summary] |

---

## Action Items

### Immediate (This Week)
- [ ] [Action]: [Owner] — [Due]

### Short-term (This Month)
- [ ] [Action]: [Owner]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Real-time alerts** - Notify on negative reviews, competitor mentions, or sentiment spikes
2. **Automated digests** - Generate daily/weekly signal summaries
3. **Review response** - Draft responses to customer reviews
4. **Trend tracking** - Monitor sentiment trends over time
5. **Competitive alerts** - Flag competitive intelligence for battlecard updates
