---
name: content-reviewer
description: Reviews content for quality, clarity, brand alignment, and effectiveness. Use for content QA before publishing.
---

# Content Reviewer Skill

Quality assurance review for all content before publishing.

## Purpose

Ensure content meets quality standards for clarity, accuracy, brand alignment, and effectiveness before it goes live.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# CONTENT REVIEWER DATA SOURCES
# Configure the sources relevant to your content QA needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Brand & Style Guidelines
- source: brand_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Marketing/Brand Guidelines/"
    - "/Marketing/Voice and Tone/"
    - "/Marketing/Editorial Style Guide/"

# Product Information (for accuracy checks)
- source: product_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Product/Feature Documentation/"
    - "/Product/Pricing/"
    - "/Product/Capabilities/"

# Legal/Compliance Guidelines
- source: legal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Legal/Marketing Guidelines/"
    - "/Legal/Disclaimers/"
    - "/Legal/Compliance Requirements/"

# SEO Data (for optimization checks)
- source: seo_tools
  connector: "{{AHREFS | SEMRUSH | MOZ | GOOGLE_SEARCH_CONSOLE}}"
  data:
    - keyword_data
    - seo_requirements

# Performance Data (for effectiveness context)
- source: analytics
  connector: "{{GOOGLE_ANALYTICS | HUBSPOT}}"
  data:
    - content_performance
    - conversion_rates
```

### Output Destinations

```yaml
# Where to deliver content review outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save review to content workflow
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Marketing/Content Reviews/"

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#content-review"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule automated content review workflows with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Whenever content is submitted for review, automatically check it for quality,
clarity, brand alignment, accuracy, and SEO compliance. Send the review
feedback to the author via Slack DM.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Content Submission Review**:
```
Whenever new content is submitted for review, automatically check it for
quality, clarity, brand alignment, accuracy, and SEO compliance. DM the
author with feedback and save the review to our Content Reviews folder.
```

**Weekly Published Content Audit**:
```
Every Friday at 10am, audit content published this week for quality issues
and generate a summary report. Post to #content-review.
```

**Pre-Launch QA Check**:
```
When content is staged for publishing, run a final QA check and alert the
content owner via Slack DM if there are any critical issues, accuracy problems,
or brand violations.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect CMS**: Link your content management system
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Review content for quality, clarity, and brand alignment" |
| `schedule` | When to run (cron or trigger) | "when content submitted" or "every Friday at 10am" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack DM to author, Google Drive" |
| `review_focus` | Which aspects to prioritize | "SEO compliance", "brand alignment" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "content-reviewer"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
    - name: "brand-voice"
      content: "<full content of brand-voice SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context` and `brand-voice`) and include them in `skill_content.referenced`.

---

## Review Dimensions

### 1. Clarity

**Readability Check**:
- Is the main point clear within the first paragraph?
- Are sentences concise (aim for 15-20 words average)?
- Is jargon explained or avoided?
- Does each paragraph have one main idea?
- Are transitions smooth between sections?

**Structure Check**:
- Is the content logically organized?
- Do headings accurately reflect content?
- Is information easy to scan?
- Is the length appropriate for the format?

### 2. Accuracy

**Fact Check**:
- Are all statistics accurate and sourced?
- Are quotes properly attributed?
- Are claims substantiated?
- Are links working and relevant?
- Is information current/not outdated?

**Technical Accuracy**:
- Are product features described correctly?
- Are technical terms used properly?
- Are processes/steps accurate?

### 3. Brand Alignment

**Voice Check**:
- Does the tone match brand guidelines?
- Is the language on-brand?
- Are we/they/you used consistently?
- Are banned words/phrases avoided?

**Visual Alignment**:
- Do images match brand style?
- Are colors/fonts correct?
- Is formatting consistent?

### 4. Effectiveness

**Goal Achievement**:
- Does content achieve its stated purpose?
- Is the CTA clear and compelling?
- Is the value proposition evident?
- Does it address audience needs?

**SEO (if applicable)**:
- Is the target keyword used appropriately?
- Are meta tags optimized?
- Are headers using keywords naturally?
- Are there internal/external links?

### 5. Legal/Compliance

**Compliance Check**:
- Are required disclaimers present?
- Are claims legally defensible?
- Is proper consent/attribution given?
- Are competitor mentions appropriate?

---

## Quality Levels

| Level | Description | Pass Criteria |
|-------|-------------|---------------|
| **Publish Ready** | No issues, ready to go live | All checks pass |
| **Minor Edits** | Small fixes needed | < 5 minor issues |
| **Needs Work** | Significant revisions required | Major issues present |
| **Reject** | Fundamental problems | Off-brand, inaccurate, or poor quality |

---

## How to Use This Skill

Invoke with natural language describing the content to review:

**General Review**
- "Review this blog post for quality and brand alignment: [paste]"
- "QA check this landing page before we publish"
- "Review this email for clarity and effectiveness"

**Specific Focus**
- "Check this content for accuracy against our product docs"
- "Review this for SEO compliance"
- "Check this press release for legal/compliance issues"

**Quick Review**
- "Quick review of this social post"
- "Fast QA on this email subject line and preview"

---

## Output Format

### Content Review Report

```markdown
# Content Review: [Content Title]

**Created**: [Date]
**Data Sources Used**: [Brand guidelines, product docs, etc.]

---

## Review Summary

| Attribute | Value |
|-----------|-------|
| Content Type | [Blog/Email/Landing Page/etc.] |
| Reviewer | [Name/Claude] |
| Review Date | [Date] |
| **Status** | **[Publish Ready / Minor Edits / Needs Work / Reject]** |

---

## Score Overview

| Dimension | Score | Notes |
|-----------|-------|-------|
| Clarity | [1-5] ⭐ | [Brief note] |
| Accuracy | [1-5] ⭐ | [Brief note] |
| Brand Alignment | [1-5] ⭐ | [Brief note] |
| Effectiveness | [1-5] ⭐ | [Brief note] |
| **Overall** | **[Avg]** | |

---

## Detailed Feedback

### Clarity

**What Works**:
- [Positive observation]
- [Positive observation]

**Needs Improvement**:
| Issue | Location | Recommendation |
|-------|----------|----------------|
| [Issue] | [Where] | [How to fix] |

**Specific Edits**:
- Current: "[Current text]"
  Suggested: "[Improved text]"

---

### Accuracy

**Verified**:
- [x] [Fact/claim checked]
- [x] [Fact/claim checked]

**Needs Verification**:
- [ ] [Claim to verify]: [Source needed]
- [ ] [Claim to verify]: [Source needed]

**Issues Found**:
| Issue | Location | Correction |
|-------|----------|------------|
| [Issue] | [Where] | [Correct information] |

---

### Brand Alignment

**On Brand**:
- [x] Tone matches guidelines
- [x] Language is appropriate
- [x] [Other brand element]

**Off Brand**:
| Issue | Current | On-Brand Alternative |
|-------|---------|---------------------|
| [Issue] | "[Current]" | "[Alternative]" |

---

### Effectiveness

**Strengths**:
- [What's working]
- [What's working]

**Opportunities**:
| Area | Current | Recommendation |
|------|---------|----------------|
| Headline | [Current] | [Stronger option] |
| CTA | [Current] | [Improvement] |
| Value Prop | [Current state] | [How to strengthen] |

---

### Technical/SEO (if applicable)

**SEO Checklist**:
- [ ] Primary keyword in title
- [ ] Keyword in first 100 words
- [ ] Meta description optimized
- [ ] Headers include keywords
- [ ] Internal links present
- [ ] Images have alt text

**Issues**:
| Issue | Recommendation |
|-------|----------------|
| [Issue] | [Fix] |

---

## Priority Fixes

### Must Fix (Before Publishing)
1. [Critical issue]: [How to fix]
2. [Critical issue]: [How to fix]

### Should Fix (Important)
1. [Important issue]: [How to fix]
2. [Important issue]: [How to fix]

### Nice to Have (Optional)
1. [Enhancement]: [Suggestion]
2. [Enhancement]: [Suggestion]

---

## Edited Version

[If minor edits, provide the corrected version here]

---

## Sign-Off

**Recommendation**: [Approve / Approve with edits / Revise and resubmit]

**Next Steps**:
1. [Action item]
2. [Action item]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Automatic review triggers** - Review content when submitted to staging/review queue
2. **Accuracy validation** - Cross-reference claims against product documentation
3. **Brand compliance** - Automated brand voice and style checking
4. **SEO validation** - Check against keyword requirements and SEO best practices
5. **Workflow integration** - Update content status in your CMS/workflow tool
