---
description: Generates personalized outreach sequences for cold, warm, event-based, re-engagement, and executive contexts. Use when creating prospecting emails or sequences.
---

# Outreach Templates Skill

Generate personalized, high-converting outreach for any sales context.

## Purpose

Create compelling, personalized outreach that drives engagement across different scenarios and buyer stages.

## Outreach Types

### 1. BDR Cold Outreach

Initial outreach to new prospects with no prior engagement:

**Structure**:
- **Hook**: Personalized opening that demonstrates research
- **Problem**: Articulate a relevant challenge they likely face
- **Insight**: Share a perspective or data point that adds value
- **Bridge**: Connect the problem to your solution (light touch)
- **CTA**: Clear, low-friction ask

**Best Practices**:
- Keep under 100 words
- One clear CTA
- No attachments on first touch
- Personalize beyond [First Name]

### 2. BDR Event Follow-Up

Follow-up after events, webinars, or content engagement:

**Structure**:
- **Reference**: Specific mention of the event/content
- **Value Add**: Additional insight related to the event topic
- **Connection**: How your solution relates to their interest
- **CTA**: Offer to continue the conversation

### 3. Warm & Re-Engagement

Reaching out to warm leads or re-engaging dormant contacts:

**Structure**:
- **Context**: Reference previous interaction or relationship
- **Update**: What's new or changed since last contact
- **Relevance**: Why reaching out now makes sense
- **CTA**: Rekindle the conversation

### 4. Executive Outreach

High-touch outreach to senior executives:

**Structure**:
- **Credibility**: Establish relevance quickly (referral, peer company, insight)
- **Strategic Frame**: Business-level challenge or opportunity
- **Proof Point**: Brief evidence of impact with similar executives
- **Ask**: Executive-appropriate request (brief call, peer introduction)

**Best Practices**:
- Maximum 75 words
- Lead with business impact, not product
- Reference peer companies or executives
- Respect their time in the CTA

### 5. Post-Event Follow-Up

Follow-up after meetings, demos, or significant interactions:

**Structure**:
- **Thank You**: Acknowledge their time
- **Recap**: Key points discussed or agreed upon
- **Next Steps**: Clear action items with owners
- **Value Add**: Additional resource or insight

## Usage

Specify outreach type and context in `$ARGUMENTS`:

```
/taizen-gtm-skills:outreach-templates cold [prospect details]
/taizen-gtm-skills:outreach-templates event-followup [event + prospect]
/taizen-gtm-skills:outreach-templates re-engage [contact + context]
/taizen-gtm-skills:outreach-templates executive [executive + company]
/taizen-gtm-skills:outreach-templates post-meeting [meeting context]
```

## Output Format

```
## Outreach: [Type] - [Prospect/Company]

### Subject Line Options
1. [Option 1]
2. [Option 2]
3. [Option 3]

### Email Body

[Full email text]

### Follow-Up Sequence

**Day 3 - Follow-Up 1:**
[Brief follow-up]

**Day 7 - Follow-Up 2:**
[Value-add follow-up]

**Day 14 - Break-Up:**
[Final attempt with clear close]

### LinkedIn Touch (Optional)
[Connection request or InMail text]

### Personalization Notes
- [Specific element to customize]
- [Research point to incorporate]
```
