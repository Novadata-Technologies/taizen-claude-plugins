---
description: Creates customer newsletters, product updates, and email communications. Use for ongoing customer engagement and retention marketing.
---

# Newsletter Writer Skill

Create engaging newsletters and email communications for customers and prospects.

## Purpose

Develop compelling email content that keeps audiences engaged, informed, and connected to your brand.

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

### Engagement Elements

- Personal greeting
- Relevant imagery
- Social proof snippets
- Interactive elements
- P.S. line for secondary CTA

## Usage

```
/taizen-gtm-skills:newsletter-writer customer [topic/theme]
/taizen-gtm-skills:newsletter-writer product-update [feature/release]
/taizen-gtm-skills:newsletter-writer event [event details]
/taizen-gtm-skills:newsletter-writer nurture [stage/topic]
```

## Output Format

### Customer Newsletter

```
# Newsletter: [Edition Name/Number]

## Email Details
- **Audience**: [Segment]
- **Send Date**: [Date]
- **Subject Line**: [Primary]
- **Preview Text**: [Preview]

---

## Subject Line Options
1. [Option 1]
2. [Option 2]
3. [Option 3]

## Preview Text Options
1. [Option 1]
2. [Option 2]

---

## Email Content

### Header
[Logo + Edition identifier]

### Opening

Hey [First Name],

[1-2 sentence hook that's timely and relevant]

[Brief intro to what's in this edition]

---

### Section 1: [Featured Content]

**[Headline]**

[2-3 paragraphs of valuable content]

[CTA Button: "Read More" / "Learn How" / etc.]

---

### Section 2: [Product/Feature Highlight]

**[New Feature/Tip Name]**

[Brief description of what it is and why it matters]

- [Benefit 1]
- [Benefit 2]
- [Benefit 3]

[CTA: "Try It Now" / "See How It Works"]

---

### Section 3: [Customer Spotlight]

**[Customer Name]: [Headline Result]**

> "[Customer quote about their success]"

[Brief context on their achievement]

[CTA: "Read the Full Story"]

---

### Section 4: [Quick Hits / Resources]

**Worth Your Time:**

📚 [Resource 1]: [Brief description] → [Link]
🎙 [Resource 2]: [Brief description] → [Link]
📊 [Resource 3]: [Brief description] → [Link]

---

### Section 5: [Upcoming Events]

**Don't Miss:**

🗓 [Event 1]: [Date] – [Brief description]
🗓 [Event 2]: [Date] – [Brief description]

[CTA: "See All Events"]

---

### Closing

[Personal sign-off, looking forward to next time, etc.]

[Your Name]
[Title]

P.S. [Secondary CTA or teaser for next edition]

---

### Footer
[Unsubscribe | Preferences | Social Links | Address]
```

### Product Update Email

```
# Product Update: [Feature/Release Name]

## Email Details
- **Audience**: [All customers / Segment]
- **Subject Line**: [Primary]
- **Preview Text**: [Preview]

---

## Subject Line Options
1. New: [Feature Name] is here
2. Introducing [Feature Name] – [Key Benefit]
3. You asked, we built: [Feature Name]

---

## Email Content

### Header
🚀 Product Update

### Headline
**[Feature Name]: [One-line benefit statement]**

### Opening

Hey [First Name],

We're excited to announce [Feature Name] – [brief description of what it does and why it matters].

[1-2 sentences on the problem this solves or opportunity it creates]

---

### What's New

**[Feature/Capability 1]**
[Brief description + benefit]

**[Feature/Capability 2]**
[Brief description + benefit]

**[Feature/Capability 3]**
[Brief description + benefit]

[Screenshot or GIF if applicable]

---

### How to Get Started

1. [Step 1]
2. [Step 2]
3. [Step 3]

[CTA Button: "Try It Now"]

---

### Learn More

- 📖 [Documentation link]
- 🎥 [Video walkthrough link]
- 💬 [Support/community link]

---

### Coming Soon

We're not stopping here. Here's what's on the roadmap:
- [Upcoming feature 1]
- [Upcoming feature 2]

---

### Feedback Welcome

Have thoughts on [Feature Name]? We'd love to hear from you. [Feedback link]

[Sign-off]

---

### Footer
[Standard footer]
```

### Nurture Email

```
# Nurture Email: [Sequence Name] - Email [#]

## Sequence Context
- **Trigger**: [What triggers this email]
- **Goal**: [What this email should accomplish]
- **Next Email**: [What comes next]

## Email Details
- **Delay**: [Days after trigger/previous email]
- **Subject Line**: [Primary]
- **Preview Text**: [Preview]

---

## Subject Line Options
1. [Option 1]
2. [Option 2]
3. [Option 3]

---

## Email Content

Hey [First Name],

[Hook related to their trigger/behavior]

[Value-add content – educational, not salesy]

[Brief mention of how your product relates]

**[Key takeaway or tip]**

[Soft CTA appropriate to their stage]

[Sign-off]

P.S. [Additional value or next step hint]

---

## Performance Targets
- Open Rate: [Target %]
- Click Rate: [Target %]
- Conversion: [Target action]
```
