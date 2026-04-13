---
name: pricing-packaging
description: Recommends pricing models, tier structures, value metrics, and pricing page guidance. Use for pricing strategy or packaging decisions.
---

# Pricing & Packaging Skill

Strategic pricing and packaging decisions that maximize value capture.

## Purpose

Develop pricing strategies and package structures that align with customer value while optimizing revenue.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# PRICING & PACKAGING DATA SOURCES
# Configure the sources relevant to your pricing decisions

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives

# Competitive Pricing
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitor_pricing
    - pricing_changes
    - packaging_models

# CRM Deal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - deal_pricing
    - discount_patterns
    - win_rates_by_price
    - deal_size_distribution

# Finance Data
- source: finance
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NETSUITE}}"
  paths:
    - "/Finance/Pricing Models/"
    - "/Finance/Cost Analysis/"
    - "/Revenue Operations/Pricing/"

# Customer Research
- source: customer_research
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Research/Pricing Research/"
    - "/Research/Willingness to Pay/"
    - "/Research/Value Studies/"

# Product Usage
- source: product_analytics
  connector: "{{MIXPANEL | AMPLITUDE | PENDO}}"
  data:
    - feature_usage
    - value_metrics
    - tier_utilization
```

### Output Destinations

```yaml
# Where to deliver pricing outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to pricing docs
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Revenue Operations/Pricing/"

  # Notify for review
  - type: slack
    connector: "{{SLACK}}"
    channel: "#pricing-committee"
```

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule pricing monitoring tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
At the start of each quarter, review our pricing effectiveness including
win rates by price point, discount patterns, and competitive positioning.
Share the analysis with #pricing-committee.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Quarterly Pricing Review**:
```
At the start of each quarter, review pricing effectiveness including win
rates, discount patterns, and competitive positioning. Save to our Pricing
Reviews folder and notify #pricing-committee.
```

**Competitive Pricing Alert**:
```
When a competitor changes their pricing, analyze the change and assess
the impact on our positioning. Alert #pricing-committee immediately.
```

**Monthly Discount Analysis**:
```
On the 1st of each month, analyze discount patterns by segment, rep, and
deal size to identify optimization opportunities. Share with #sales-leadership.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect CRM**: Link your Salesforce or HubSpot for deal data
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Review pricing effectiveness and discount patterns" |
| `schedule` | When to run (cron or trigger) | "quarterly" or "when competitor pricing changes" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #pricing-committee, Google Drive" |
| `competitors` | Which competitors to monitor | "Salesforce, HubSpot" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "pricing-packaging"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
    - name: "competitive-intelligence"
      content: "<full content of competitive-intelligence SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context` and `competitive-intelligence`) and include them in `skill_content.referenced`.

---

## Pricing Frameworks

### 1. Value-Based Pricing

**Value Metric Selection**:
The ideal value metric should be:
- Aligned with customer value (they pay more as they get more value)
- Predictable for customers (they can estimate costs)
- Scalable (grows with customer success)
- Easy to measure and track

**Common Value Metrics**:
| Model | Value Metric | Best For |
|-------|--------------|----------|
| Per User | Active users | Collaboration tools |
| Per Unit | Data volume, transactions | Infrastructure |
| Tiered | Feature access | Enterprise software |
| Usage | Consumption | API, metered services |
| Outcome | Results delivered | Performance-based |

### 2. Packaging Strategy

**Good-Better-Best Framework**:

| Tier | Purpose | Typical Features |
|------|---------|------------------|
| Good (Entry) | Land new customers | Core features, limited usage |
| Better (Growth) | Capture mid-market | More features, higher limits |
| Best (Enterprise) | Maximize value | All features, custom terms |

**Packaging Principles**:
- Each tier should have clear, compelling value
- Upgrade triggers should be natural (growth-based)
- Don't create "dead end" tiers
- Leave room for negotiation in enterprise

### 3. Pricing Page Best Practices

**Information Architecture**:
1. Clear tier names that convey value
2. Prominent pricing (don't hide it)
3. Feature comparison that highlights differences
4. Social proof (customer logos, testimonials)
5. Clear CTAs for each tier
6. FAQ section for common questions

**Psychological Pricing**:
- Anchor high, negotiate down
- Use charm pricing ($99 vs $100) for SMB
- Use round numbers for enterprise
- Show annual savings prominently
- Include a "most popular" indicator

### 4. Competitive Pricing Analysis

| Competitor | Model | Entry Price | Enterprise | Notes |
|------------|-------|-------------|------------|-------|
| [Comp 1] | [Model] | [Price] | [Price] | [Notes] |

**Positioning Options**:
- Premium: Price above market, justify with value
- Competitive: Price at market, compete on value
- Penetration: Price below market, gain share
- Value: Lower price, different segment

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Pricing Strategy**
- "Develop a pricing strategy for our new product"
- "Recommend pricing model for our enterprise tier"

**Packaging**
- "Design tier structure for our SaaS product"
- "How should we package our add-on features?"

**Competitive Analysis**
- "Analyze competitor pricing in our market"
- "How does our pricing compare to alternatives?"

**Pricing Page**
- "Review our pricing page for best practices"
- "Suggest improvements to our pricing presentation"

---

## Output Format

### Pricing Strategy

```markdown
# Pricing Strategy: [Product Name]

**Created**: [Date]
**Data Sources Used**: [Competitive intel, CRM data, etc.]

---

## Strategic Context

### Market Position
- **Current Position**: [Where we are]
- **Target Position**: [Where we want to be]
- **Competitive Landscape**: [How others price]

### Value Delivered
- **Quantified Value**: [$ impact for customer]
- **Value Drivers**: [What creates value]
- **Value Metric**: [Best metric to align price with value]

## Recommended Pricing Model

### Value Metric: [Chosen Metric]
**Rationale**: [Why this metric aligns with value]

### Pricing Structure

| Element | Details |
|---------|---------|
| Model | [Subscription/Usage/Hybrid] |
| Billing | [Monthly/Annual/Multi-year] |
| Minimum | [Floor price or commitment] |

## Package Structure

### Tier Overview

| Tier | Target Segment | Starting Price | Value Metric |
|------|----------------|----------------|--------------|
| Starter | [Segment] | $[Price]/mo | [Metric] |
| Professional | [Segment] | $[Price]/mo | [Metric] |
| Enterprise | [Segment] | Custom | [Metric] |

### Tier Details

#### Starter
- **Target**: [Who this is for]
- **Price**: $[X]/month per [metric]
- **Includes**:
  - [Feature 1]
  - [Feature 2]
  - [Limit 1]
- **Upgrade Trigger**: [When they should upgrade]

#### Professional
- **Target**: [Who this is for]
- **Price**: $[X]/month per [metric]
- **Includes**:
  - Everything in Starter, plus:
  - [Feature 3]
  - [Feature 4]
- **Upgrade Trigger**: [When they should upgrade]

#### Enterprise
- **Target**: [Who this is for]
- **Price**: Custom / Contact Sales
- **Includes**:
  - Everything in Professional, plus:
  - [Enterprise features]

## Pricing Levers

### Discounts
| Type | Amount | Criteria |
|------|--------|----------|
| Annual prepay | [%] off | Pay annually |
| Multi-year | [%] off | 2-3 year commit |
| Volume | [%] off | [Threshold] |

## Competitive Positioning

| vs. [Competitor] | Their Price | Our Price | Our Position |
|------------------|-------------|-----------|--------------|
| Entry | $[X] | $[X] | [Rationale] |
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Competitive monitoring** - Alert on competitor pricing changes
2. **Win rate analysis** - Correlate pricing with deal outcomes
3. **Discount optimization** - Identify discount patterns to improve
4. **Tier utilization** - Track which tiers customers choose and why
