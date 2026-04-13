---
description: Creates ROI models, business cases, and value calculations. Also supports RFP/proposal responses with evidence-based justifications.
---

# ROI Builder Skill

Build compelling ROI models and business cases that justify investment.

## Purpose

Help sales teams quantify value and create persuasive business cases that resonate with economic buyers and procurement teams.

## Capabilities

### 1. ROI Model Development

Create customized return on investment models:

**Input Variables**:
- Current state costs (labor, tools, inefficiency)
- Implementation costs (licensing, services, change management)
- Time to value assumptions
- Risk adjustment factors

**Output Metrics**:
- Total ROI percentage
- Net Present Value (NPV)
- Payback period
- Internal Rate of Return (IRR)
- Total Cost of Ownership (TCO)

### 2. Business Case Framework

Structure a complete business case:

**Executive Summary**
- Problem statement
- Recommended solution
- Investment required
- Expected return

**Current State Analysis**
- Existing costs and inefficiencies
- Quantified pain points
- Risk of inaction

**Proposed Solution**
- What you're recommending
- Implementation approach
- Timeline and milestones

**Financial Analysis**
- Cost breakdown
- Benefit quantification
- ROI calculations
- Sensitivity analysis

**Risk Assessment**
- Implementation risks
- Mitigation strategies
- Contingency plans

### 3. Value Quantification

Translate qualitative benefits to financial impact:

| Benefit Type | Quantification Approach |
|--------------|------------------------|
| Time savings | Hours × Fully loaded cost × Frequency |
| Error reduction | Error rate × Cost per error × Volume |
| Revenue impact | Conversion lift × Deal value × Pipeline |
| Risk avoidance | Probability × Potential loss |
| Productivity | Output increase × Value per output |

### 4. RFP/Proposal Support

Build compelling proposal responses:

- Executive summary with value focus
- Solution alignment to requirements
- Pricing justification with ROI
- Implementation plan
- Risk mitigation
- References and proof points

## Usage

```
/taizen-gtm-skills:roi-builder model [use case or scenario]
/taizen-gtm-skills:roi-builder business-case [opportunity]
/taizen-gtm-skills:roi-builder calculate [specific metric]
/taizen-gtm-skills:roi-builder proposal [RFP requirements]
```

## Output Format

### ROI Model

```
## ROI Analysis: [Customer/Scenario]

### Assumptions
| Assumption | Value | Source |
|------------|-------|--------|
| [Assumption 1] | [Value] | [Where this comes from] |
| [Assumption 2] | [Value] | [Where this comes from] |

### Investment Summary
| Cost Category | Year 1 | Year 2 | Year 3 |
|---------------|--------|--------|--------|
| Software | $[X] | $[X] | $[X] |
| Implementation | $[X] | $[X] | $[X] |
| Internal Resources | $[X] | $[X] | $[X] |
| **Total Investment** | **$[X]** | **$[X]** | **$[X]** |

### Benefit Summary
| Benefit Category | Year 1 | Year 2 | Year 3 |
|------------------|--------|--------|--------|
| [Benefit 1] | $[X] | $[X] | $[X] |
| [Benefit 2] | $[X] | $[X] | $[X] |
| [Benefit 3] | $[X] | $[X] | $[X] |
| **Total Benefits** | **$[X]** | **$[X]** | **$[X]** |

### Key Metrics
| Metric | Value |
|--------|-------|
| 3-Year ROI | [X]% |
| Payback Period | [X] months |
| Net Present Value | $[X] |
| Total Cost of Ownership | $[X] |

### Sensitivity Analysis
| Scenario | ROI | Payback |
|----------|-----|---------|
| Conservative | [X]% | [X] months |
| Base Case | [X]% | [X] months |
| Optimistic | [X]% | [X] months |

### Key Drivers
1. [Driver 1]: [Sensitivity to changes]
2. [Driver 2]: [Sensitivity to changes]
```

### Business Case

```
## Business Case: [Initiative Name]

### Executive Summary
[2-3 paragraph overview: problem, solution, investment, return]

**Recommendation**: [Clear recommendation]
**Investment**: $[X] over [timeframe]
**Expected Return**: [X]% ROI, [X] month payback

---

### Problem Statement
[What challenge are we solving and why does it matter]

**Current Impact**:
- [Quantified pain 1]
- [Quantified pain 2]
- [Quantified pain 3]

**Cost of Inaction**: $[X] annually

---

### Proposed Solution
[What we're recommending]

**Key Components**:
1. [Component 1]
2. [Component 2]
3. [Component 3]

**Implementation Timeline**:
| Phase | Duration | Key Deliverables |
|-------|----------|------------------|
| [Phase 1] | [Duration] | [Deliverables] |

---

### Financial Analysis

**Total Investment**: $[X]

| Category | Amount |
|----------|--------|
| [Cost 1] | $[X] |
| [Cost 2] | $[X] |

**Projected Benefits**: $[X] over 3 years

| Benefit | Year 1 | Year 2 | Year 3 |
|---------|--------|--------|--------|
| [Benefit] | $[X] | $[X] | $[X] |

**Key Metrics**:
- ROI: [X]%
- Payback: [X] months
- NPV: $[X]

---

### Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | [H/M/L] | [H/M/L] | [Plan] |

---

### Recommendation

[Clear statement of recommendation and next steps]

**Approval Requested**: [What you need from the reader]
```
