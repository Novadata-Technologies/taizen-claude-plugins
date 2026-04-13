---
description: Buyer persona profiles with priorities, language preferences, and objection patterns. Helps adapt messaging for different stakeholders.
---

# Buyer Profiles Skill

Adapt communications for specific buyer personas with guidance on priorities, language, and concerns.

## Purpose

Ensure messaging resonates with the target buyer by understanding their priorities, language, objections, and decision-making criteria.

## Executive Personas

### HR & Talent Executives

**CHRO (Chief Human Resources Officer)**
- **Priorities**: Workforce strategy, culture, talent retention, DEI, employer brand
- **Language**: Strategic workforce planning, human capital, employee experience
- **Metrics**: Retention rate, engagement scores, time-to-productivity, DEI metrics
- **Objections**: ROI clarity, change management burden, integration complexity

**CLO (Chief Learning Officer)**
- **Priorities**: Skills development, learning culture, career mobility, compliance
- **Language**: Upskilling, reskilling, learning pathways, competency frameworks
- **Metrics**: Course completion, skill acquisition, internal mobility, certification rates
- **Objections**: Content relevance, learner engagement, measurement of impact

**Chief Talent Officer / Head of TA**
- **Priorities**: Quality of hire, time-to-fill, candidate experience, employer brand
- **Language**: Talent pipeline, candidate journey, hiring velocity, talent density
- **Metrics**: Quality of hire, source effectiveness, offer acceptance rate
- **Objections**: ATS integration, recruiter adoption, candidate volume vs quality

**Executive HRBP**
- **Priorities**: Business alignment, change management, leadership development
- **Language**: Business partnership, organizational effectiveness, talent strategy
- **Metrics**: Business unit performance, leader readiness, succession strength
- **Objections**: Time investment, stakeholder buy-in, competing priorities

### Finance Executives

**CFO / Economic Buyer**
- **Priorities**: ROI, cost optimization, risk management, compliance
- **Language**: Total cost of ownership, payback period, risk-adjusted returns
- **Metrics**: ROI, NPV, payback period, cost per outcome
- **Objections**: Budget constraints, competing investments, proof of value

## Competitive Positioning

When dealing with competitive situations, consider:

1. **Differentiation**: What makes you unique vs. the competitor
2. **Strengths to emphasize**: Where you demonstrably outperform
3. **Weaknesses to address**: Where you need to neutralize or reframe
4. **Landmines to set**: Questions that expose competitor weaknesses
5. **Proof points**: Evidence that validates your advantages

## Usage

Specify the persona in `$ARGUMENTS`:

```
/taizen-gtm-skills:buyer-profiles CHRO
/taizen-gtm-skills:buyer-profiles CFO competitive-deal
```

## Output Format

```
## Persona Profile: [Title]

### Priorities
- [Priority 1]
- [Priority 2]

### Preferred Language
- Use: [Terms they respond to]
- Avoid: [Terms that don't resonate]

### Key Metrics They Care About
- [Metric 1]
- [Metric 2]

### Common Objections & Responses
| Objection | Response |
|-----------|----------|
| [Objection] | [How to address] |

### Recommended Approach
[Specific guidance for engaging this persona]
```
