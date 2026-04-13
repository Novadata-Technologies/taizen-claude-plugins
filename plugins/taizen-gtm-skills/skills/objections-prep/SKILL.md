---
description: Produces prep output for anticipated objections with response strategies and reframing techniques. Use when preparing for negotiations or objection-heavy conversations.
---

# Objections Prep Skill

Anticipate and prepare responses for common and deal-specific objections.

## Purpose

Equip sales teams with confident, effective responses to objections that advance the deal rather than stall it.

## Objection Handling Framework

### The LAER Method

1. **Listen**: Let them finish, acknowledge the concern
2. **Acknowledge**: Show empathy, validate the concern is reasonable
3. **Explore**: Ask questions to understand the root cause
4. **Respond**: Address with evidence, reframe, or propose a path forward

### Common Objection Categories

**Price/Budget Objections**
- "It's too expensive"
- "We don't have budget"
- "Competitor X is cheaper"
- "We need to reduce costs, not add them"

**Timing Objections**
- "Not the right time"
- "We're too busy right now"
- "Maybe next quarter/year"
- "We just implemented something else"

**Authority Objections**
- "I need to check with my boss"
- "This requires executive approval"
- "Others need to be involved"

**Need Objections**
- "We're fine with what we have"
- "This isn't a priority"
- "We've tried this before"
- "Our situation is different"

**Trust Objections**
- "We've never heard of you"
- "You're too small/new"
- "Can you prove these claims?"
- "What if it doesn't work?"

**Competitive Objections**
- "We're already working with X"
- "X has more features"
- "X is the industry standard"

## Response Strategies

### Reframe the Objection
Transform the objection into a reason to buy:
- "Too expensive" → "Let's talk about the cost of the problem you're solving"

### Isolate the Objection
Confirm this is the only barrier:
- "If we could address [objection], would you be ready to move forward?"

### Feel-Felt-Found
Relate to similar customers:
- "I understand how you feel. Other [similar companies] felt the same way. What they found was..."

### Evidence & Proof
Counter with data:
- "Actually, our customers typically see [X]% improvement in [Y]"

### Question Back
Understand the real concern:
- "Help me understand - when you say it's too expensive, compared to what?"

## Usage

Specify context in `$ARGUMENTS`:

```
/taizen-gtm-skills:objections-prep [objection or context]
/taizen-gtm-skills:objections-prep pricing objections for enterprise deals
/taizen-gtm-skills:objections-prep competitor X displacement
```

## Output Format

```
## Objection Prep: [Context]

### Likely Objections

**1. [Objection]**
- **Root Cause**: [Why they're really saying this]
- **Response Strategy**: [Approach to use]
- **Sample Response**: "[What to say]"
- **Follow-Up Question**: "[Question to ask]"
- **Proof Point**: [Evidence to support your response]

**2. [Objection]**
- **Root Cause**: [Why they're really saying this]
- **Response Strategy**: [Approach to use]
- **Sample Response**: "[What to say]"
- **Follow-Up Question**: "[Question to ask]"
- **Proof Point**: [Evidence to support your response]

### Proactive Objection Prevention

Address these before they come up:
- [Topic 1]: [How to preemptively address]
- [Topic 2]: [How to preemptively address]

### If the Objection Is Real

When the objection is legitimate (not a smokescreen):
- [How to acknowledge and pivot]
- [Alternative path forward]
- [When to walk away gracefully]

### Practice Scenarios

**Scenario 1**: [Situation]
- Objection: "[What they say]"
- Your response: "[What you say]"
- Their likely response: "[What they say next]"
- Your follow-up: "[How to continue]"
```
