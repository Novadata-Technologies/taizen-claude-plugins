---
name: sales-playbook
description: Sales methodology framework covering deal stages, qualification criteria, and strategic selling approaches. Use for deal strategy and sales process guidance.
---

# Sales Playbook Skill

Strategic sales methodology and deal execution guidance.

## Purpose

Provide a consistent framework for running deals from qualification through close, incorporating proven sales methodologies and your team's best practices.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# SALES PLAYBOOK DATA SOURCES
# Configure the sources relevant to your sales process

# Enterprise Search (searches across all internal sources)
- source: enterprise_search
  connector: "{{GLEAN | MOVEWORKS | ELASTIC}}"
  data:
    - internal_docs
    - wiki_content
    - shared_drives
    - slack_history

# CRM & Deal Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - opportunity_records
    - stage_history
    - deal_fields
    - activity_history
    - win_loss_reasons
    - sales_process_data

# Conversation Intelligence
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - discovery_calls
    - demo_recordings
    - negotiation_calls
    - winning_patterns
    - deal_risk_signals

# Revenue Intelligence
- source: revenue_intelligence
  connector: "{{CLARI | AVISO | BOOSTUP}}"
  data:
    - deal_scores
    - pipeline_health
    - forecast_data
    - engagement_scores

# Sales Engagement
- source: sales_engagement
  connector: "{{OUTREACH | SALESLOFT | APOLLO}}"
  data:
    - sequence_performance
    - email_metrics
    - meeting_rates

# Internal Playbooks
- source: internal_docs
  connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION | CONFLUENCE}}"
  paths:
    - "/Sales/Playbooks/"
    - "/Sales/Methodology/"
    - "/Sales Enablement/Process/"
    - "/Sales/Qualification Frameworks/"
- source: sales_content
  connector: "{{SEISMIC | HIGHSPOT | SHOWPAD}}"
  data:
    - playbook_content
    - sales_plays
    - methodology_guides

# Competitive Intelligence
- source: competitive_intel
  connector: "{{KLUE | CRAYON | KOMPYTE}}"
  data:
    - competitive_plays
    - displacement_playbooks
```

### Output Destinations

```yaml
# Where to deliver playbook outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Update deal records
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - update_qualification_fields
      - add_deal_strategy_notes
      - update_next_steps
      - log_meddpicc_scores

  # Save strategies to docs
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Sales/Deal Strategies/"

  # Share in deal review channels
  - type: slack
    connector: "{{SLACK}}"
    channels:
      deal_reviews: "#deal-reviews"
      forecasting: "#forecasting"
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
- Sales methodology context OR deal situation
- `display` output enabled (always available)

Enhanced functionality requires:
- CRM for deal stages and pipeline data
- Sales methodology documentation
- Call recordings for best practice examples
- Win/loss analysis for pattern insights

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule recurring sales playbook and pipeline management tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
Every Thursday morning, prepare pipeline review reports for each rep including
deal health scores, risk flags, and recommended actions. Send to #deal-reviews.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Daily Deal Alerts**:
```
Every morning at 8am, check all active deals for risk signals including stuck
deals, missing qualification criteria, and engagement drops. DM the deal owner
on Slack if any issues are found.
```

**Weekly Pipeline Review**:
```
Every Thursday at 7am, prepare pipeline review summaries for each rep including
deal health scores, MEDDPICC gaps, and recommended actions. Save to Google Drive
and post to #deal-reviews.
```

**Qualification Analysis**:
```
Every Monday morning, run MEDDPICC assessments on all pipeline deals and identify
qualification gaps by stage. Update CRM records and alert sales management of
any critical gaps.
```

**Stage Validation**:
```
When a deal moves to a new stage in Salesforce, validate that it meets the exit
criteria for the previous stage. If criteria are missing, DM the deal owner with
what needs to be addressed.
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
| `task` | Natural language description of what to do | "Run MEDDPICC assessments on pipeline deals" |
| `schedule` | When to run (cron or trigger) | "every Thursday at 7am" or "when deal stage changes" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #deal-reviews, Google Drive, CRM update" |
| `filters` | Deal criteria | "deals closing this quarter over $50k" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "sales-playbook"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Sales Methodology Framework

### Deal Stages

| Stage | Definition | Exit Criteria |
|-------|------------|---------------|
| **Prospect** | Initial contact, validating fit | Confirmed meeting scheduled |
| **Qualify** | Understanding need, budget, authority, timeline | Qualified opportunity created |
| **Discover** | Deep dive on requirements, stakeholders, process | Clear needs documented |
| **Demonstrate** | Show solution fit, differentiate | Positive evaluation feedback |
| **Propose** | Present solution and pricing | Proposal delivered and reviewed |
| **Negotiate** | Address concerns, finalize terms | Agreement on terms |
| **Close** | Execute agreement | Signed contract |

### Qualification Framework (MEDDPICC)

| Criteria | Questions to Validate |
|----------|----------------------|
| **Metrics** | What business outcomes do they need to achieve? What does success look like quantified? |
| **Economic Buyer** | Who controls the budget? Who can say yes? |
| **Decision Criteria** | What factors will drive the decision? How will they evaluate options? |
| **Decision Process** | What are the steps to make a decision? Who's involved at each step? |
| **Paper Process** | What's required to execute a contract? Legal, procurement, security? |
| **Identify Pain** | What's the pain? Why does it matter? What happens if they don't act? |
| **Champion** | Who's advocating internally? Can they sell when you're not in the room? |
| **Competition** | Who else are they considering? What's their perception of alternatives? |

### Challenger Principles

**Teach**: Bring unique insights that reframe how they think about their business
**Tailor**: Adapt your message to resonate with each stakeholder's priorities
**Take Control**: Guide the conversation and decision process confidently

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Deal Strategy**
- "Help me build a strategy for the Acme Corp deal"
- "What's my path to close for the TechCorp opportunity?"
- "Review my deal and tell me what's missing"
- "How should I approach the negotiation with IBM?"

**Qualification**
- "Is the Acme deal qualified? Run MEDDPICC"
- "What qualification gaps do I have in my pipeline?"
- "Help me qualify this inbound lead from Nike"
- "Score my top 5 deals on qualification strength"

**Stage Advancement**
- "What do I need to do to move from discovery to demo?"
- "Am I ready to send a proposal to TechCorp?"
- "What's blocking this deal from closing?"
- "Review my deal stages - are they accurate?"

**Pipeline Review**
- "Prepare me for pipeline review - what are the risks?"
- "Which deals in my pipeline should I be worried about?"
- "Help me forecast accurately for this quarter"
- "What deals should I focus on this week?"

**Discovery Planning**
- "Build a discovery plan for my meeting with the VP of Sales at Acme"
- "What questions should I ask in my first call with Nike?"
- "Help me plan a multi-threaded discovery approach"

---

## Output Format

### Deal Strategy

```markdown
## Deal Strategy: [Company Name]

**Generated**: [Date]
**Data Sources Used**: [CRM, Gong, Revenue Intelligence, etc.]

---

### Opportunity Summary

| Attribute | Value |
|-----------|-------|
| Deal Size | $[Value] |
| Stage | [Current stage] |
| Days in Stage | [Days] |
| Total Sales Cycle | [Days] |
| Close Date | [Target] |
| Probability | [%] |
| Next Step | [Action] |

### Qualification Assessment (MEDDPICC)

*Based on CRM data, call recordings, and activity:*

| Criteria | Score | Evidence | Gap |
|----------|-------|----------|-----|
| **Metrics** | [🟢/🟡/🔴] | [What we know from calls/CRM] | [What we need] |
| **Economic Buyer** | [🟢/🟡/🔴] | [Who, access level, engagement] | [What we need] |
| **Decision Criteria** | [🟢/🟡/🔴] | [What they've told us] | [What we need] |
| **Decision Process** | [🟢/🟡/🔴] | [Steps, timeline, stakeholders] | [What we need] |
| **Paper Process** | [🟢/🟡/🔴] | [Legal, procurement, security] | [What we need] |
| **Identify Pain** | [🟢/🟡/🔴] | [Pain points, quantified impact] | [What we need] |
| **Champion** | [🟢/🟡/🔴] | [Who, strength, access] | [What we need] |
| **Competition** | [🟢/🟡/🔴] | [Who else, our position] | [What we need] |

**Overall Qualification Score**: [X/10]

### Conversation Insights

*From call recordings:*
- **Key Topics Discussed**: [From Gong topic tracking]
- **Sentiment Trend**: [How has it changed]
- **Questions They Asked**: [Signals of interest/concern]
- **Objections Raised**: [What came up]
- **Next Steps Mentioned**: [Commitments made]

### Strengths (Why We'll Win)

1. **[Strength 1]**: [Evidence from calls/engagement]
2. **[Strength 2]**: [Evidence]

### Risks (What Could Kill This Deal)

| Risk | Evidence | Likelihood | Mitigation |
|------|----------|------------|------------|
| [Risk 1] | [Signal from data] | [H/M/L] | [Action to take] |
| [Risk 2] | [Signal from data] | [H/M/L] | [Action to take] |

### Competitive Dynamics

- **Competitors**: [Who else is being evaluated]
- **Our Position**: [Where we stand]
- **Key Battleground**: [What will determine winner]
- **Competitive Play**: [Strategy to use]

### Gaps to Address

*Critical gaps preventing close:*

| Gap | Priority | Action to Close | Owner |
|-----|----------|-----------------|-------|
| [Gap 1] | [H/M/L] | [Specific action] | [Who] |
| [Gap 2] | [H/M/L] | [Specific action] | [Who] |

### Recommended Actions

| Action | Purpose | Owner | Due |
|--------|---------|-------|-----|
| [Action 1] | [Why this matters] | [Who] | [When] |
| [Action 2] | [Why this matters] | [Who] | [When] |
| [Action 3] | [Why this matters] | [Who] | [When] |

### Win Strategy

[2-3 sentence summary of how to win this deal, based on the analysis]

### Path to Close

```
[Current Stage] ──→ [Next Stage] ──→ [Next Stage] ──→ CLOSE
     │                    │                │
     ↓                    ↓                ↓
[Required action]   [Required action] [Required action]
```
```

### Stage Advancement Checklist

```markdown
## Stage Advancement: [Stage] → [Next Stage]

**Opportunity**: [Company Name]
**Current Stage Duration**: [Days]

---

### Current Stage Exit Criteria

| Criterion | Status | Evidence |
|-----------|--------|----------|
| [Criterion 1] | [✅/⚠️/❌] | [Proof from CRM/Gong] |
| [Criterion 2] | [✅/⚠️/❌] | [Proof from CRM/Gong] |
| [Criterion 3] | [✅/⚠️/❌] | [Proof from CRM/Gong] |

### Gaps Preventing Advancement

| Gap | Why It Matters | Action to Close | Owner |
|-----|----------------|-----------------|-------|
| [Gap] | [Impact] | [Action] | [Who] |

### Next Stage Entry Requirements

| Requirement | Current Status | How to Achieve |
|-------------|----------------|----------------|
| [Requirement 1] | [Status] | [Action] |
| [Requirement 2] | [Status] | [Action] |

### Recommended Next Steps

1. **[Step 1]**: [Purpose] - [Owner]
2. **[Step 2]**: [Purpose] - [Owner]

### Red Flags to Watch

*Based on deal patterns:*
- [Warning sign 1]: [What to do if you see this]
- [Warning sign 2]: [What to do if you see this]

### Stage Advancement Probability

Based on your data: Deals at this stage with this profile close **[X]%** of the time.

Factors improving your odds:
- [Positive signal]

Factors decreasing your odds:
- [Negative signal]
```

### Pipeline Review Prep

```markdown
## Pipeline Review Prep: [Rep Name]

**Period**: [Date range]
**Total Pipeline**: $[Value]
**Commit**: $[Value]
**Best Case**: $[Value]

---

### Pipeline Health Summary

| Metric | Actual | Target | Status |
|--------|--------|--------|--------|
| Coverage (vs Quota) | [X]x | [Target]x | [🟢/🟡/🔴] |
| Qualified Pipeline | $[Value] | $[Target] | [🟢/🟡/🔴] |
| Avg Deal Size | $[Value] | $[Target] | [🟢/🟡/🔴] |
| Avg Sales Cycle | [Days] | [Target] | [🟢/🟡/🔴] |
| Stage Conversion | [%] | [%] | [🟢/🟡/🔴] |

### Top Deals to Discuss

| Opportunity | Value | Stage | Close Date | Risk Level | Key Question |
|-------------|-------|-------|------------|------------|--------------|
| [Company 1] | $[X] | [Stage] | [Date] | [🟢/🟡/🔴] | [What to validate] |
| [Company 2] | $[X] | [Stage] | [Date] | [🟢/🟡/🔴] | [What to validate] |

### At-Risk Deals

*Deals with concerning signals:*

| Opportunity | Risk Signal | Evidence | Recommended Action |
|-------------|-------------|----------|-------------------|
| [Company] | [Risk type] | [From Gong/CRM] | [Action] |

### Stuck Deals

*Deals with no movement in [X] days:*

| Opportunity | Days Stuck | Last Activity | Unblock Action |
|-------------|------------|---------------|----------------|
| [Company] | [Days] | [Activity] | [Action] |

### Deals to Push/Pull

**Should Move Up (Accelerate)**:
- [Company]: [Why - strong signals]

**Should Move Out (Slip)**:
- [Company]: [Why - missing criteria]

### This Week's Focus

Based on pipeline analysis, prioritize:
1. [Deal/Action] - [Why]
2. [Deal/Action] - [Why]
3. [Deal/Action] - [Why]
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Deal alerts** - Notify when deals show risk signals or stall
2. **Stage validation** - Automatically check if stage criteria are met
3. **Weekly pipeline digest** - Summarize pipeline health and recommended actions
4. **Forecast assistance** - Flag deals that may slip based on patterns
5. **Coaching triggers** - Alert managers when reps need deal support
