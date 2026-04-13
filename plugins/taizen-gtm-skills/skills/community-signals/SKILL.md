---
description: Monitors and summarizes community feedback, social signals, and customer sentiment. Use for intelligence gathering and trend spotting.
---

# Community Signals Skill

Capture and analyze signals from customer communities, social media, and review sites.

## Purpose

Synthesize community feedback into actionable intelligence for product, marketing, and sales teams.

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

## Usage

```
/taizen-gtm-skills:community-signals digest [time period]
/taizen-gtm-skills:community-signals sentiment [topic]
/taizen-gtm-skills:community-signals competitive [competitor]
/taizen-gtm-skills:community-signals trends [industry/topic]
```

## Output Format

### Weekly Signal Digest

```
# Community Signals Digest: [Date Range]

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

**[Signal 2]**
[Same format]

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

**[Signal 2]**
[Same format]

### Themes in Negative Feedback
| Theme | Volume | Trend | Status |
|-------|--------|-------|--------|
| [Theme 1] | [#] | [↑↓→] | [Addressed/In progress/New] |
| [Theme 2] | [#] | [↑↓→] | [Status] |

---

## Competitive Intelligence

### Competitor Mentions

| Competitor | Mentions | Sentiment | Key Signal |
|------------|----------|-----------|------------|
| [Comp 1] | [#] | [Pos/Neg] | [Summary] |
| [Comp 2] | [#] | [Pos/Neg] | [Summary] |

### Competitive Conversations
- [Summary of notable comparison discussion]
- [Win/loss signal from community]

### Competitor News
- [Relevant competitor update]
- [Impact assessment]

---

## Market Trends

### Industry Signals

**[Trend 1]**: [Description]
- **Sources**: [Where observed]
- **Relevance**: [Why it matters to us]
- **Implication**: [What we should do]

**[Trend 2]**: [Description]
[Same format]

### Emerging Topics
- [Topic gaining traction]
- [New pain point being discussed]
- [Shift in buyer priorities]

---

## Review Site Summary

### New Reviews This Period

| Site | New Reviews | Avg Rating | Change |
|------|-------------|------------|--------|
| G2 | [#] | [X.X] | [↑↓→] |
| Capterra | [#] | [X.X] | [↑↓→] |
| TrustRadius | [#] | [X.X] | [↑↓→] |

### Notable Reviews

**Positive**:
> "[Quote]" — [Reviewer, Company] on [Site]

**Needs Attention**:
> "[Quote]" — [Reviewer, Company] on [Site]
> **Response Status**: [Responded/Pending]

---

## Action Items

### Immediate (This Week)
- [ ] [Action]: [Owner] — [Due]
- [ ] [Action]: [Owner] — [Due]

### Short-term (This Month)
- [ ] [Action]: [Owner]
- [ ] [Action]: [Owner]

### Strategic (Longer-term)
- [ ] [Initiative based on signals]
- [ ] [Product consideration]

---

## Signal Sources Monitored

| Source | Last Checked | Next Check |
|--------|--------------|------------|
| [Source 1] | [Date] | [Date] |
| [Source 2] | [Date] | [Date] |
```

### Topic Sentiment Analysis

```
# Sentiment Analysis: [Topic]

## Overview
- **Topic**: [Topic being analyzed]
- **Period**: [Date range]
- **Sources**: [Where signals came from]

## Sentiment Breakdown

| Sentiment | Volume | % of Total | Trend |
|-----------|--------|------------|-------|
| Positive | [#] | [%] | [↑↓→] |
| Neutral | [#] | [%] | [↑↓→] |
| Negative | [#] | [%] | [↑↓→] |

## Key Themes

### Positive Themes
1. **[Theme]**: [Description and examples]
2. **[Theme]**: [Description and examples]

### Negative Themes
1. **[Theme]**: [Description and examples]
2. **[Theme]**: [Description and examples]

## Representative Quotes

**Most Positive**:
> "[Quote]" — [Source]

**Most Negative**:
> "[Quote]" — [Source]

**Most Influential**:
> "[Quote]" — [Source with high reach]

## Recommendations

Based on this sentiment analysis:
1. [Recommendation 1]
2. [Recommendation 2]
3. [Recommendation 3]
```
