---
description: Designs email nurture sequences, drip campaigns, and automated email flows. Use for lead nurturing, onboarding, and lifecycle marketing.
---

# Email Sequences Skill

Design automated email sequences that nurture leads and customers through their journey.

## Purpose

Create strategic email sequences that move subscribers toward desired actions while building relationship and trust.

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

## Usage

```
/taizen-gtm-skills:email-sequences nurture [trigger/audience]
/taizen-gtm-skills:email-sequences onboarding [product]
/taizen-gtm-skills:email-sequences re-engage [segment]
/taizen-gtm-skills:email-sequences event [event name]
```

## Output Format

### Full Sequence

```
# Email Sequence: [Sequence Name]

## Sequence Overview

| Attribute | Details |
|-----------|---------|
| Type | [Nurture/Onboarding/etc.] |
| Trigger | [What starts this sequence] |
| Audience | [Who receives it] |
| Goal | [Desired outcome] |
| Length | [# emails over # days] |

### Success Metrics
| Metric | Target |
|--------|--------|
| Open Rate | [%] |
| Click Rate | [%] |
| Conversion | [Action + %] |

---

## Email 1: [Email Name]

**Timing**: Immediately / Day 0
**Subject Line**: [Subject]
**Preview Text**: [Preview]
**Goal**: [What this email should accomplish]

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
**Subject Line**: [Subject]
**Preview Text**: [Preview]
**Goal**: [What this email should accomplish]

---

**Email Body**:

Hey [First Name],

[Content]

[CTA]

[Sign-off]

---

## Email 3: [Email Name]
[Continue pattern]

---

## Email 4: [Email Name]
[Continue pattern]

---

## Email 5: [Email Name]
[Continue pattern]

---

## Sequence Branching Logic

```
Email 1 sent
    ↓
    ├── Clicked CTA → [Tag: Engaged] → Continue sequence
    │
    └── No click (Day 3) → Email 2 sent
            ↓
            ├── Clicked → [Tag: Engaged] → Skip to Email 4
            │
            └── No click (Day 5) → Email 3 sent
```

---

## Exit Conditions
- Converts to [goal action] → Exit + tag
- Unsubscribes → Exit
- Completes sequence → Move to [next sequence]
- [Days] of no engagement → Move to re-engagement

---

## A/B Test Ideas
- Subject line: [Test A] vs [Test B]
- Send time: [Time A] vs [Time B]
- CTA: [Variation A] vs [Variation B]
```

### Individual Email

```
# Email: [Email Name]

## Email Details
- **Sequence**: [Parent sequence]
- **Position**: Email [#] of [total]
- **Timing**: [When sent]
- **Goal**: [Purpose of this email]

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

### Version A (Control)

Hey [First Name],

[Opening paragraph - hook and context]

[Body paragraph 1 - main value]

[Body paragraph 2 - supporting detail or story]

[Body paragraph 3 - connection to action]

[CTA sentence]

[CTA Button: "Text Here"]

Best,
[Name]

P.S. [Secondary hook or CTA]

---

### Version B (Test Variant)

[Alternative version with different angle/approach]

---

## Technical Setup
- **From**: [Name + email]
- **Reply-to**: [Email]
- **CTA URL**: [Link]
- **Tags to add**: [Tags on send]
- **Tags on click**: [Tags when clicked]
```

### Sequence Map

```
# Sequence Map: [Program Name]

## Entry Points

```
[Lead Form] ──────────→ Lead Nurture Sequence
                              ↓
[Demo Request] ───────→ High Intent Sequence
                              ↓
[Trial Signup] ───────→ Trial Onboarding Sequence
                              ↓
[Purchase] ───────────→ Customer Onboarding Sequence
```

## Sequence Flow

### Awareness Stage
**Sequence**: Educational Nurture
**Emails**: 5
**Duration**: 2 weeks
**Exit**: Books meeting OR completes sequence → Consideration stage

### Consideration Stage
**Sequence**: Product-focused Nurture
**Emails**: 4
**Duration**: 10 days
**Exit**: Starts trial OR completes sequence → Re-engagement

### Trial Stage
**Sequence**: Trial Activation
**Emails**: 7
**Duration**: Trial length
**Exit**: Converts OR trial expires → Trial extension/re-engage

### Customer Stage
**Sequence**: Onboarding → Adoption → Expansion
**Ongoing**: Lifecycle communications

## Global Rules
- No more than [X] emails per week per contact
- Always check suppression lists
- Honor unsubscribes across all sequences
- 24-hour minimum between emails
```
