---
description: Produces unified discovery prep with tailored questions, anticipated objections, and recommended demo flow. Use before discovery calls or demos.
---

# Discovery Prep Skill

Comprehensive preparation for discovery calls and initial demos.

## Purpose

Ensure every discovery conversation is strategic, insightful, and moves the opportunity forward.

## Discovery Framework

### Pre-Call Research

Before the call, gather:
- **Account Context**: Company, industry, size, recent news
- **Stakeholder Context**: Attendee roles, backgrounds, priorities
- **Competitive Context**: Current solutions, recent evaluations
- **Trigger Context**: Why now? What's driving the conversation?

### Discovery Question Framework

Structure questions across these dimensions:

**1. Current State**
- How do you currently handle [relevant process]?
- What tools/systems are you using today?
- Who's involved in this process?

**2. Pain & Impact**
- What's working well? What's not?
- When this breaks down, what's the impact?
- How does this affect [relevant business metric]?

**3. Future State**
- What does success look like?
- If you could change one thing, what would it be?
- What's your timeline for addressing this?

**4. Decision Process**
- Who else is involved in evaluating solutions?
- What criteria matter most?
- What's worked or not worked with past vendors?

**5. Compelling Event**
- What's driving the timing of this initiative?
- What happens if nothing changes?
- Are there any deadlines we should be aware of?

### Demo Customization Guide

Based on discovery, customize the demo:

**Opening (2 min)**: Recap what you heard, confirm priorities
**Core Demo (15-20 min)**: Focus on their top 2-3 use cases
**Differentiators (5 min)**: Highlight unique value for their context
**Proof Points (3 min)**: Share relevant customer stories
**Next Steps (5 min)**: Align on path forward

## Usage

Specify account and context in `$ARGUMENTS`:

```
/taizen-gtm-skills:discovery-prep Acme Corp
/taizen-gtm-skills:discovery-prep Acme Corp CHRO meeting
```

## Output Format

```
## Discovery Prep: [Company] - [Meeting Type]

### Meeting Context
- **Date/Time**: [If known]
- **Attendees**: [Names and roles]
- **Objective**: [What we want to accomplish]

### Pre-Call Intel
- **Company Context**: [Relevant background]
- **Trigger Event**: [Why are they talking to us now]
- **Competitive Landscape**: [What we're up against]

### Discovery Questions

**Opening Questions** (Build rapport, confirm context)
1. [Question]
2. [Question]

**Current State Questions** (Understand today)
1. [Question]
2. [Question]
3. [Question]

**Pain & Impact Questions** (Uncover problems)
1. [Question]
2. [Question]
3. [Question]

**Future State Questions** (Understand goals)
1. [Question]
2. [Question]

**Process Questions** (Map the deal)
1. [Question]
2. [Question]

### Anticipated Objections

| Objection | Response Strategy |
|-----------|-------------------|
| [Objection 1] | [How to address] |
| [Objection 2] | [How to address] |
| [Objection 3] | [How to address] |

### Demo Recommendations

**Focus Areas** (Based on likely priorities)
1. [Feature/Use Case 1]: [Why relevant]
2. [Feature/Use Case 2]: [Why relevant]

**Skip/Minimize**
- [Area to de-emphasize]: [Why]

**Proof Points to Include**
- [Relevant customer story]
- [Relevant metric]

### Success Criteria
- [ ] [What makes this call successful]
- [ ] [Key information to obtain]
- [ ] [Next step to secure]
```
