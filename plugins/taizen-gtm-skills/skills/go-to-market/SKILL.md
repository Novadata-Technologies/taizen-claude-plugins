---
name: go-to-market
description: Plans product launches, campaigns, cross-functional GTM execution, and enablement. Use for launch planning or campaign development.
---

# Go-to-Market Skill

Comprehensive GTM planning for launches, campaigns, and market entry, coordinating across teams and tools.

## Purpose

Orchestrate successful go-to-market execution through structured planning, cross-functional alignment, and enablement.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# GO-TO-MARKET DATA SOURCES
# Configure the sources relevant to your GTM planning

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# Product Information
- source: product_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Product/Roadmap/"
    - "/Product/Feature Specs/"
    - "/Product/Release Notes/"
- source: product_management
  connector: "{{PRODUCTBOARD | JIRA | ASANA | LINEAR}}"
  data:
    - release_schedule
    - feature_details
    - dependencies

# Marketing Assets & Performance
- source: marketing_content
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
  paths:
    - "/Marketing/Campaigns/"
    - "/Marketing/Content Library/"
    - "/Marketing/Brand Guidelines/"
- source: marketing_analytics
  connector: "{{HUBSPOT | MARKETO | GOOGLE_ANALYTICS}}"
  data:
    - campaign_performance
    - channel_effectiveness
    - conversion_data

# Sales Enablement
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD | GOOGLE_DRIVE}}"
  paths:
    - "/Sales Enablement/"
    - "/Sales/Playbooks/"
    - "/Sales/Collateral/"
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - pipeline_data
    - deal_velocity
    - win_rates
    - competitive_data

# Customer Success
- source: customer_success
  connector: "{{GAINSIGHT | CHURNZERO | TOTANGO}}"
  data:
    - adoption_metrics
    - customer_health
    - expansion_data

# Communication & Coordination
- source: project_management
  connector: "{{ASANA | MONDAY | NOTION}}"
  data:
    - project_timelines
    - task_assignments
    - dependencies

# Competitive Intelligence
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitor_launches
    - market_positioning
```

### Output Destinations

```yaml
# Where to deliver GTM planning outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save plans to project management
  - type: project_management
    connector: "{{ASANA | MONDAY | NOTION}}"
    actions:
      - create_project
      - create_tasks
      - set_milestones

  # Save to documentation
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/GTM Plans/"

  # Notify stakeholders
  - type: slack
    connector: "{{SLACK}}"
    channels:
      launches: "#product-launches"
      marketing: "#marketing"
      sales: "#sales-enablement"

  # Create sales enablement
  - type: sales_enablement
    connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
    actions:
      - create_playbook_draft
      - upload_content
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
- Product or feature to launch
- Target market or audience
- `display` output enabled (always available)

Enhanced functionality requires:
- Product documentation for feature details
- Messaging framework for positioning alignment
- Competitive intelligence for differentiation
- Customer research for audience validation

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring GTM planning and tracking tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every day during our product launch, check launch readiness status, identify
blockers, and send a daily standup update to #product-launches on Slack.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Launch Countdown Tracker**:
```
Every morning at 9am, check the status of our Q2 product launch, identify any
blockers or missed deadlines, and post a readiness update to #product-launches.
Alert me if any critical dependencies are at risk.
```

**Weekly GTM Review**:
```
Every Friday at 8am, prepare a GTM review summary including launch status,
campaign metrics progress, and cross-functional action items. Post to
#gtm-team and save to our GTM Plans folder.
```

**Post-Launch Analysis**:
```
When we complete a product launch, automatically generate a post-launch analysis
report comparing metrics vs targets, documenting learnings, and recommending
next steps. Save to our Launch Retrospectives folder.
```

**Quarterly Planning Kickoff**:
```
At the start of each quarter, prepare a GTM planning brief covering upcoming
launches, resource requirements, and timeline. Share with #leadership.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Project Tools**: Link your Asana, Monday, or Notion
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Check launch readiness and identify blockers" |
| `schedule` | When to run (cron or trigger) | "every morning at 9am" or "when launch completes" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #product-launches, Notion" |
| `launch` | Which launch to track | "Q2 AI Feature Launch" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "go-to-market"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
    - name: "messaging-positioning"
      content: "<full content of messaging-positioning SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context` and `messaging-positioning`) and include them in `skill_content.referenced`.

---

## GTM Planning Frameworks

### 1. Launch Planning

**Launch Tiers**:

| Tier | Scope | Timeline | Investment |
|------|-------|----------|------------|
| Tier 1 | Major launch, new product/market | 8-12 weeks | Full GTM |
| Tier 2 | Significant feature, expansion | 4-6 weeks | Moderate |
| Tier 3 | Minor update, enhancement | 2-3 weeks | Light touch |

**Launch Components**:
- Messaging and positioning
- Sales enablement
- Marketing campaigns
- Customer communications
- Partner/channel activation
- PR and analyst relations
- Success metrics

### 2. Campaign Planning

**Campaign Brief Elements**:
- Objective and success metrics
- Target audience and segments
- Key messages and offers
- Channels and tactics
- Timeline and milestones
- Budget and resources
- Measurement plan

### 3. Cross-Functional GTM

**Stakeholder Alignment**:
| Team | Role | Deliverables | Timeline |
|------|------|--------------|----------|
| Product | Feature readiness | Release, docs | T-4 weeks |
| Marketing | Demand gen | Campaigns, content | T-2 weeks |
| Sales | Pipeline execution | Training, outreach | T-1 week |
| CS | Customer success | Adoption plan | T+1 week |

### 4. Sales Enablement

**Enablement Package**:
- Positioning and messaging guide
- Competitive battlecards
- Discovery questions
- Demo script and flow
- Objection handling
- Pricing and packaging
- Customer references

---

## GTM Strategies

### New Product Launch
- Build awareness and credibility
- Generate initial pipeline
- Secure early wins and references
- Iterate based on feedback

### Market Expansion
- Adapt positioning for new segment
- Develop segment-specific content
- Train/hire for new motion
- Build relevant case studies

### Competitive Displacement
- Target competitor install base
- Develop migration messaging
- Create switching incentives
- Build competitive proof points

### Upsell/Cross-sell
- Identify expansion triggers
- Create upgrade paths
- Enable CS/AM teams
- Automate opportunity identification

---

## How to Use This Skill

Invoke with natural language describing the GTM initiative:

**Launch Planning**
- "Create a GTM plan for our new AI feature launching next month"
- "Build a Tier 1 launch plan for our enterprise product"
- "Plan a feature launch for the analytics dashboard"
- "What do we need for a successful product launch?"

**Campaign Development**
- "Create a campaign brief for our Q2 awareness push"
- "Build a demand gen campaign targeting healthcare"
- "Plan an ABM campaign for our top 50 accounts"
- "Design a competitive displacement campaign against Competitor X"

**Enablement Planning**
- "Create an enablement plan for the sales team on our new product"
- "What training materials do we need for the launch?"
- "Build a competitive battlecard for the launch"

**Cross-Functional Coordination**
- "Create a cross-functional GTM timeline for the launch"
- "What stakeholders need to be involved and when?"
- "Build a RACI for our product launch"

---

## Output Format

### Launch Plan

```markdown
# GTM Launch Plan: [Product/Feature Name]

**Created**: [Date]
**Data Sources Used**: [Product roadmap, CRM, marketing analytics, etc.]

---

## Launch Overview

| Attribute | Details |
|-----------|---------|
| Launch Date | [Date] |
| Launch Tier | [1/2/3] |
| Target Segment | [Audience] |
| Primary Goal | [Objective] |
| Launch Owner | [Name] |
| Stakeholders | [List] |

---

## Launch Objectives & Metrics

| Objective | Metric | Target | Tracking |
|-----------|--------|--------|----------|
| Awareness | [Metric] | [Target] | [How measured] |
| Pipeline | [Metric] | [Target] | [How measured] |
| Adoption | [Metric] | [Target] | [How measured] |
| Revenue | [Metric] | [Target] | [How measured] |

---

## Positioning & Messaging

### Core Message
[Primary launch message - one sentence]

### Elevator Pitch
[30-second explanation of what it is and why it matters]

### Key Value Props
1. **[Value prop 1]**: [Supporting detail]
2. **[Value prop 2]**: [Supporting detail]
3. **[Value prop 3]**: [Supporting detail]

### Target Personas
- **Primary**: [Persona] - [Why they care]
- **Secondary**: [Persona] - [Why they care]

### Competitive Positioning
- **Against [Competitor 1]**: [Differentiation]
- **Against [Competitor 2]**: [Differentiation]

---

## Cross-Functional Plan

### Product Team
| Deliverable | Owner | Due Date | Status |
|-------------|-------|----------|--------|
| Feature complete | [Name] | [Date] | [Status] |
| Documentation | [Name] | [Date] | [Status] |
| Release notes | [Name] | [Date] | [Status] |

### Marketing Team
| Deliverable | Owner | Due Date | Status |
|-------------|-------|----------|--------|
| Messaging guide | [Name] | [Date] | [Status] |
| Landing page | [Name] | [Date] | [Status] |
| Blog post | [Name] | [Date] | [Status] |
| Email campaigns | [Name] | [Date] | [Status] |
| Social content | [Name] | [Date] | [Status] |
| Paid campaigns | [Name] | [Date] | [Status] |

### Sales Team
| Deliverable | Owner | Due Date | Status |
|-------------|-------|----------|--------|
| Sales training | [Name] | [Date] | [Status] |
| Pitch deck | [Name] | [Date] | [Status] |
| Demo script | [Name] | [Date] | [Status] |
| Competitive battlecard | [Name] | [Date] | [Status] |
| Pricing guide | [Name] | [Date] | [Status] |

### Customer Success Team
| Deliverable | Owner | Due Date | Status |
|-------------|-------|----------|--------|
| Customer comms | [Name] | [Date] | [Status] |
| Adoption playbook | [Name] | [Date] | [Status] |
| Training materials | [Name] | [Date] | [Status] |

---

## Marketing Campaign Plan

### Awareness Tactics

| Channel | Tactic | Audience | Budget | Timing |
|---------|--------|----------|--------|--------|
| Email | [Campaign] | [Segment] | [Budget] | [Date] |
| Social | [Campaign] | [Audience] | [Budget] | [Date] |
| Content | [Campaign] | [Audience] | [Budget] | [Date] |
| Paid | [Campaign] | [Audience] | [Budget] | [Date] |
| PR | [Campaign] | [Audience] | [Budget] | [Date] |

### Content Assets

| Asset | Purpose | Owner | Due |
|-------|---------|-------|-----|
| Blog post | Announcement | [Owner] | [Date] |
| Video | Product overview | [Owner] | [Date] |
| Case study | Social proof | [Owner] | [Date] |
| Webinar | Education | [Owner] | [Date] |

---

## Sales Enablement Package

### Training Plan
- **Session 1**: [Date] - [Topic] - [Format]
- **Session 2**: [Date] - [Topic] - [Format]

### Sales Assets Checklist
- [ ] Pitch deck with new messaging
- [ ] One-pager / leave-behind
- [ ] Demo script and environment
- [ ] Competitive battlecard
- [ ] Pricing and packaging guide
- [ ] FAQ document
- [ ] Customer references

### Talk Tracks

**Opening**: "[How to introduce the new capability]"

**Discovery Questions**:
1. "[Question to uncover need]"
2. "[Question to quantify impact]"

**Objection Responses**:
- "[Common objection]" → "[Response]"

---

## Customer Communications

### Existing Customer Strategy

| Segment | Message | Channel | Timing |
|---------|---------|---------|--------|
| [Segment] | [Message] | [Email/In-app/CSM] | [When] |

### New Customer Strategy
- [How new customers will learn about this]

---

## Timeline

### T-6 Weeks: Planning
- [ ] Finalize positioning and messaging
- [ ] Align stakeholders on plan
- [ ] Begin content creation
- [ ] Brief PR/analysts (if applicable)

### T-4 Weeks: Development
- [ ] Create marketing assets
- [ ] Develop sales materials
- [ ] Prepare customer communications
- [ ] Set up tracking and measurement

### T-2 Weeks: Enablement
- [ ] Conduct sales training
- [ ] Brief CS team
- [ ] Stage all content
- [ ] Final reviews

### T-1 Week: Final Prep
- [ ] Final stakeholder reviews
- [ ] Systems and tools ready
- [ ] Launch rehearsal
- [ ] Prepare day-of communications

### Launch Day
- [ ] Execute launch sequence
- [ ] Send communications
- [ ] Monitor metrics and social
- [ ] Address issues in real-time

### T+1 Week: Momentum
- [ ] Follow-up campaigns
- [ ] Share early wins
- [ ] Address feedback

### T+4 Weeks: Optimization
- [ ] Analyze results vs goals
- [ ] Gather feedback from all teams
- [ ] Iterate on messaging/approach
- [ ] Publish retrospective

---

## Risk Register

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| [Risk] | [H/M/L] | [H/M/L] | [Plan] | [Who] |

---

## Success Criteria

**Launch Success** (30 days):
- [ ] [Metric 1]: [Target]
- [ ] [Metric 2]: [Target]
- [ ] [Metric 3]: [Target]

**Sustained Success** (90 days):
- [ ] [Metric 1]: [Target]
- [ ] [Metric 2]: [Target]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Project creation** - Auto-create launch projects in Asana/Monday with tasks and owners
2. **Timeline tracking** - Monitor progress against milestones
3. **Asset coordination** - Track content creation across teams
4. **Enablement distribution** - Push materials to Seismic/Highspot
5. **Launch notifications** - Coordinate communications across Slack channels
6. **Metrics dashboards** - Pull performance data post-launch
