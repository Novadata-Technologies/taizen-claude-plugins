---
name: roi-builder
description: Creates ROI models, business cases, and value calculations. Also supports RFP/proposal responses with evidence-based justifications.
---

# ROI Builder Skill

Build compelling ROI models and business cases that justify investment.

## Purpose

Help sales teams quantify value and create persuasive business cases that resonate with economic buyers and procurement teams.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# ROI BUILDER DATA SOURCES
# Configure the sources relevant to your value selling needs

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Customer Success Data
- source: customer_success
  connector: "{{GAINSIGHT | CHURNZERO | TOTANGO}}"
  data:
    - customer_outcomes
    - success_metrics
    - roi_achieved
    - implementation_timelines

# CRM Deal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - won_deals
    - deal_values
    - implementation_costs
    - time_to_value_data

# Case Studies & Proof Points
- source: proof_points
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Case Studies/"
    - "/Customer Success/Success Stories/"
    - "/Sales/ROI Examples/"
    - "/Sales/Proof Points/"

# Product & Pricing
- source: pricing_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Sales/Pricing/"
    - "/Finance/Cost Models/"
    - "/Product/Implementation/"

# Industry Benchmarks
- source: research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Industry Benchmarks/"
    - "/Research/ROI Studies/"
    - "/Research/Analyst Reports/"

# ROI Calculator/Tools
- source: roi_tools
  connector: "{{GOOGLE_SHEETS | EXCEL | INTERNAL_TOOL}}"
  data:
    - calculator_models
    - benchmark_data
    - assumption_defaults
```

### Output Destinations

```yaml
# Where to deliver ROI outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to deal folder
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales/Business Cases/"

  # Update CRM with value data
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - update_value_fields
      - attach_business_case
      - log_roi_calculation

  # Share with team
  - type: slack
    connector: "{{SLACK}}"
    channel: "#deal-support"
```
---

## Instructions for Claude

> **IMPORTANT**: Before executing this skill, you MUST validate the configuration above.

### Pre-Execution Checklist

1. **Check for placeholder values**: Scan the YAML configuration for any `{{...}}` placeholders. These indicate required configuration that the user must provide.

2. **Validate data sources**: For each data source listed:
   - If a `connector` field shows `{{OPTIONS}}` format, ask the user which option they use
   - If URLs, paths, or names contain `{{PLACEHOLDER}}`, ask the user to provide actual values
   - Verify any required MCP servers are connected and available

3. **Validate output destinations**: For any output type beyond `display`:
   - Confirm the connector is available as an MCP server
   - Ensure destination paths/channels are configured (not placeholders)

### If Configuration is Incomplete

**Do not proceed with the skill.** Instead:

1. List the specific missing or placeholder values found
2. Explain what each value is needed for
3. Ask the user to provide the missing configuration
4. Offer to help them set up the required MCP integrations

**Example response when config is incomplete:**
```
Before I can run this skill, I need some configuration:

**Missing values:**
- [List specific {{PLACEHOLDER}} values found]

**MCP connections needed:**
- [List required connectors not yet available]

Please provide these values, or let me know which data sources you'd like to skip.
```

### Minimum Requirements

At minimum, this skill requires:
- Use case or value driver to model
- Target customer context (size, industry)
- `display` output enabled (always available)

Enhanced functionality requires:
- Customer success data for validated outcomes
- Case studies for proof points
- Industry benchmarks for credibility
- CRM for deal-specific customization

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring ROI and business case tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
When a deal moves to proposal stage in Salesforce, automatically generate an
ROI model and business case for the account. DM the deal owner and attach
the business case to the CRM record.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Deal Business Case Generation**:
```
When a deal moves to proposal stage in Salesforce, automatically generate
an ROI model and business case for the account. Send to the deal owner
via Slack and attach to the CRM record.
```

**Monthly Benchmark Update**:
```
On the 1st of each month, update our ROI benchmarks and proof points based
on the latest customer success data. Post updates to #sales-enablement.
```

**Quarterly Value Story Compilation**:
```
At the start of each quarter, compile value stories and ROI results from
closed deals for use in future business cases. Share with #customer-success.
```

**RFP Support**:
```
When we receive a new RFP, automatically generate the value-focused sections
including ROI justification and business case framework. DM the RFP owner
with the draft content.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect CRM**: Link your Salesforce or HubSpot
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Generate ROI model and business case" |
| `schedule` | When to run (cron or trigger) | "when deal enters proposal stage" or "monthly" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack DM, CRM attachment, Google Drive" |
| `deal_context` | Deal information | "account, deal size, industry" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "roi-builder"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

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

---

## How to Use This Skill

Invoke with natural language describing what you need:

**ROI Models**
- "Build an ROI model for a 500-person company evaluating our solution"
- "Calculate ROI for the Acme Corp deal - they have 50 sales reps"
- "Create a TCO comparison vs their current solution"

**Business Cases**
- "Create a business case for the TechCorp opportunity"
- "Help me build an executive presentation with financial justification"
- "Generate a business case template for enterprise deals"

**Value Quantification**
- "Help me quantify the value of time savings for a 20-person team"
- "Calculate the impact of reducing error rates by 30%"
- "What's the revenue impact of improving conversion by 5%?"

**RFP/Proposal Support**
- "Generate ROI section for this RFP response"
- "Create value justification for our pricing proposal"

---

## Output Format

### ROI Model

```markdown
## ROI Analysis: [Customer/Scenario]

**Created**: [Date]
**Data Sources Used**: [Customer success data, benchmarks, etc.]

---

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

### Proof Points
*From similar customers:*
- [Customer]: [Result achieved]
- [Customer]: [Result achieved]
```

### Business Case

```markdown
## Business Case: [Initiative Name]

**Created**: [Date]
**Data Sources Used**: [Customer data, benchmarks, proof points]

---

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

---

## Automation Options

When configured with integrations, this skill can:

1. **Auto-generate business cases** - Create business cases when deals reach proposal stage
2. **Benchmark updates** - Keep ROI benchmarks current from customer success data
3. **Value tracking** - Document actual ROI achieved for use in future deals
4. **Calculator integration** - Pull from and update ROI calculator tools
5. **Proof point library** - Automatically tag and organize value stories
