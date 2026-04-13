---
description: Deal reviews, win/loss analysis, and rep coaching frameworks. Helps identify patterns and improve sales execution.
---

# Sales Coaching Skill

Structured frameworks for deal analysis and rep development.

## Purpose

Enable continuous improvement of sales performance through win/loss analysis, deal retrospectives, and coaching frameworks.

## Enablement Modes

### 1. Win/Loss Analysis Framework

Structured analysis of closed opportunities:

**Win Analysis**
- What were the key factors in winning?
- Which messages/value props resonated?
- Who were the champions and how did we engage them?
- What competitive dynamics existed?
- What can we replicate?

**Loss Analysis**
- What were the primary reasons for losing?
- Where in the process did we lose momentum?
- What objections went unaddressed?
- What would we do differently?
- What can we learn?

**No-Decision Analysis**
- Why did the prospect go dark or delay?
- What signals did we miss?
- How could we have created more urgency?
- What qualification gaps existed?

### 2. Sales Coaching & Skills Assessment

Framework for manager-rep coaching conversations:

**Skill Areas**
- Discovery & qualification
- Value articulation
- Objection handling
- Negotiation & closing
- Account management
- Pipeline management
- Executive engagement

**Coaching Conversation Structure**
1. **Observe**: Review recent calls, deals, metrics
2. **Diagnose**: Identify skill gaps and patterns
3. **Discuss**: Collaborative conversation about performance
4. **Plan**: Specific actions for improvement
5. **Follow-up**: Track progress and reinforce

### 3. Deal Coaching

Real-time guidance on active opportunities:

- Deal qualification assessment
- Strategy recommendations
- Next best action
- Risk identification
- Resource deployment suggestions

## Usage

Specify mode and context in `$ARGUMENTS`:

```
/taizen-gtm-skills:sales-coaching win-analysis [deal details]
/taizen-gtm-skills:sales-coaching loss-analysis [deal details]
/taizen-gtm-skills:sales-coaching skill-assessment [rep or skill area]
/taizen-gtm-skills:sales-coaching deal-review [opportunity details]
```

## Output Format

### Win/Loss Analysis
```
## Win/Loss Analysis: [Company Name] - [Outcome]

### Deal Overview
| Attribute | Value |
|-----------|-------|
| Company | [Name] |
| Deal Size | [Value] |
| Sales Cycle | [Days] |
| Outcome | [Won/Lost/No Decision] |
| Close Date | [Date] |
| Rep | [Name] |

### Key Factors

**Primary Reason for [Outcome]**
[Main factor that determined the outcome]

**Contributing Factors**
1. [Factor 1]: [Details]
2. [Factor 2]: [Details]
3. [Factor 3]: [Details]

### Process Analysis

| Stage | What Happened | What Worked | What Didn't |
|-------|---------------|-------------|-------------|
| Discovery | [Details] | [Positives] | [Negatives] |
| Qualification | [Details] | [Positives] | [Negatives] |
| Demo/Eval | [Details] | [Positives] | [Negatives] |
| Proposal | [Details] | [Positives] | [Negatives] |
| Negotiation | [Details] | [Positives] | [Negatives] |

### Competitive Dynamics
- **Competitors Involved**: [List]
- **Our Positioning**: [How we differentiated]
- **Competitive Outcome**: [Who won and why]

### Stakeholder Analysis
| Stakeholder | Role | Sentiment | Impact on Deal |
|-------------|------|-----------|----------------|
| [Name] | [Role] | [+/-/Neutral] | [How they influenced] |

### Lessons Learned
1. [Lesson 1]: [Actionable takeaway]
2. [Lesson 2]: [Actionable takeaway]
3. [Lesson 3]: [Actionable takeaway]

### Recommendations
- **For this account**: [If applicable, next steps]
- **For similar deals**: [How to apply learnings]
- **For the team**: [Broader implications]
```

### Coaching Session
```
## Coaching Session: [Rep Name]

### Performance Overview
- **Period**: [Time period]
- **Key Metrics**: [Relevant numbers]
- **Trend**: [Improving/Stable/Declining]

### Skill Assessment
| Skill Area | Rating | Evidence | Priority |
|------------|--------|----------|----------|
| Discovery | [1-5] | [Observations] | [H/M/L] |
| Value Articulation | [1-5] | [Observations] | [H/M/L] |
| Objection Handling | [1-5] | [Observations] | [H/M/L] |
| Closing | [1-5] | [Observations] | [H/M/L] |
| Account Management | [1-5] | [Observations] | [H/M/L] |

### Strengths to Leverage
1. [Strength 1]: [How to leverage]
2. [Strength 2]: [How to leverage]

### Development Areas
1. [Area 1]: [Specific behaviors to change]
2. [Area 2]: [Specific behaviors to change]

### Action Plan
| Action | Timeline | Support Needed | Success Measure |
|--------|----------|----------------|-----------------|
| [Action] | [When] | [What help] | [How to measure] |

### Coaching Questions
Use these to guide the conversation:
1. [Question about self-assessment]
2. [Question about specific situation]
3. [Question about goals]
4. [Question about obstacles]
5. [Question about commitment]

### Follow-Up Plan
- **Next Check-In**: [Date]
- **Focus Areas**: [What to review]
- **Metrics to Track**: [What to measure]
```
