---
name: customer-advocacy
description: Manages customer reference programs, testimonial collection, reviews, and advocacy initiatives. Use for building proof points and customer evidence.
---

# Customer Advocacy Skill

Build and leverage a network of customer advocates for social proof and references.

## Purpose

Transform satisfied customers into active advocates who provide references, reviews, testimonials, and referrals.

---

## Required Integrations

> **Setup**: Connect these data sources to enable full functionality. Claude will prompt you to connect any missing integrations when you use this skill.

### Data Sources

```yaml
# CUSTOMER ADVOCACY DATA SOURCES
# Configure the sources relevant to your advocacy program

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
    - nps_scores
    - health_scores
    - advocacy_status
    - customer_outcomes

# CRM Data
- source: crm
  connector: "{{SALESFORCE | HUBSPOT}}"
  data:
    - customer_records
    - reference_requests
    - advocacy_activities

# Reference Management
- source: reference_platform
  connector: "{{ORCA | SALESFORCE_REFERENCE | POINTNRELEASE}}"
  data:
    - active_references
    - reference_requests
    - reference_history

# Call Recordings (for quotes)
- source: call_recordings
  connector: "{{GONG | CHORUS | CLARI}}"
  data:
    - customer_calls
    - quotable_moments

# Review Sites
- source: review_sites
  sources:
    - g2
    - capterra
    - trustradius
  data:
    - review_status
    - ratings
```

### Output Destinations

```yaml
# Where to deliver advocacy outputs
outputs:
  # Always available - display in Claude UI
  - type: display
    enabled: true

  # Save to advocacy program docs
  - type: documents
    connector: "{{GOOGLE_DRIVE | SHAREPOINT | NOTION}}"
    destination: "/Customer Success/Advocacy Program/"

  # Update CRM
  - type: crm
    connector: "{{SALESFORCE | HUBSPOT}}"
    actions:
      - log_advocacy_activity
      - update_reference_status

  # Notify team
  - type: slack
    connector: "{{SLACK}}"
    channels:
      advocacy: "#customer-advocacy"
      references: "#reference-requests"
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
- Advocacy program goal (references, testimonials, reviews, etc.)
- `display` output enabled (always available)

Enhanced functionality requires:
- CRM for customer health and relationship data
- Customer success platform for NPS and satisfaction scores
- Review platform connections for tracking
- Reference management system access

---

## Scheduling & Automation with Taizen

> **Automate this skill**: Schedule advocacy program tasks with [Taizen](https://usetaizen.com). Create a free account to set up automated agents that run on your schedule.

### How It Works

The Taizen MCP server accepts natural language requests to schedule agents. Simply describe what you want to automate:

```
On the 1st of each month, identify new advocacy candidates based on NPS scores,
health scores, and recent success metrics. Post the list to #customer-advocacy.
```

Taizen will:
1. Read this skill's definition to understand the capabilities
2. Create a recurring agent with your specified schedule
3. Execute the task and deliver results to your configured destinations

### Example Natural Language Requests

**Monthly Advocate Candidate Scan**:
```
On the 1st of each month, identify new advocacy candidates based on NPS scores,
health scores, and recent success metrics. Post to #customer-advocacy and save
to our Advocacy Pipeline folder.
```

**Quarterly Review Request Campaign**:
```
At the start of each quarter, generate personalized review request emails for
customers eligible for G2 and Capterra reviews. Save the email drafts and
notify #customer-advocacy.
```

**Reference Request Matcher**:
```
When a reference request is created in Salesforce, automatically find the best
matching references based on industry, use case, and persona. DM the requester
with the top 3 matches.
```

**Weekly Reference Activity Report**:
```
Every Friday at 9am, summarize reference activity for the week including
completed calls, feedback received, and reference capacity. Post to
#customer-advocacy.
```

### Setting Up Taizen Automation

1. **Create Account**: Sign up at [usetaizen.com](https://usetaizen.com)
2. **Connect MCP**: Add the Taizen MCP integration in your Claude settings and authenticate
3. **Connect Customer Success**: Link your Gainsight or ChurnZero
4. **Schedule Agent**: Describe your automation in natural language
5. **Taizen Reads Skill**: The agent receives this skill's full definition to understand what it can do

### Technical Details

When scheduling via Taizen MCP, Claude will:
1. Read this SKILL.md file to get the full skill definition
2. Call Taizen MCP with the skill content included

| Parameter | Description | Example |
|-----------|-------------|---------|
| `task` | Natural language description of what to do | "Identify advocacy candidates from high-NPS customers" |
| `schedule` | When to run (cron or trigger) | "on the 1st of each month" or "when reference request created" |
| `skill_content` | Object containing primary skill and referenced skills | See structure below |
| `outputs` | Where to send results | "Slack #customer-advocacy, Google Drive" |
| `criteria` | Candidate selection criteria | "NPS 9+, active for 6+ months" |

**skill_content structure:**
```yaml
skill_content:
  primary:
    name: "customer-advocacy"
    content: "<full content of this SKILL.md>"
  referenced:
    - name: "product-context"
      content: "<full content of product-context SKILL.md>"
```

> **Note to Claude**: When a user asks to schedule this skill with Taizen, read this entire SKILL.md file and pass it as `skill_content.primary`. Also read any referenced background skills (like `product-context`) and include them in `skill_content.referenced`.

---

## Advocacy Program Framework

### 1. Advocacy Tiers

| Tier | Activities | Value to Company | Value to Customer |
|------|------------|------------------|-------------------|
| **Bronze** | Reviews, testimonials | Social proof | Recognition |
| **Silver** | References, case studies | Sales enablement | Visibility |
| **Gold** | Speaking, advisory | Thought leadership | Network access |
| **Platinum** | Co-marketing, referrals | Pipeline generation | Partnership benefits |

### 2. Advocacy Activities

**Low Effort (Bronze)**:
- G2/Capterra reviews
- Short testimonial quotes
- Social media engagement
- Logo permission
- NPS promoter response

**Medium Effort (Silver)**:
- Reference calls
- Case study participation
- Video testimonial
- Quote for press release
- Analyst reference

**High Effort (Gold)**:
- Conference speaking
- Webinar participation
- Blog post authorship
- Advisory board membership
- Podcast guest

**Strategic (Platinum)**:
- Customer referrals
- Co-marketing campaigns
- Joint press releases
- Product co-development
- Executive sponsorship

### 3. Advocate Identification

**Signals to Watch**:
- High NPS scores (9-10)
- Product usage champions
- Unsolicited praise
- Social media mentions
- Support interactions
- Renewal without negotiation
- Expansion purchases

**Qualification Criteria**:
- Achieved measurable results
- Has authority to speak publicly
- Willing to be identified
- Represents target customer profile
- Good relationship with team

### 4. Testimonial Collection

**Testimonial Types**:
| Type | Format | Use Cases |
|------|--------|-----------|
| Quote | 1-2 sentences | Website, collateral |
| Video | 30-60 seconds | Website, social, events |
| Written | 2-3 paragraphs | Case studies, PR |
| Audio | 2-3 minutes | Podcasts, sales |

**Quote Formula**:
"[Specific challenge we faced] → [How product helped] → [Quantified result or emotion]"

---

## How to Use This Skill

Invoke with natural language describing what you need:

**Program Design**
- "Design a customer advocacy program"
- "Create advocacy tier structure and benefits"

**Testimonial Requests**
- "Generate a testimonial request email for Acme Corp"
- "Create video testimonial script for TechCorp"

**Review Requests**
- "Write a G2 review request email for our top customers"
- "Generate personalized review requests for Q4"

**Reference Matching**
- "Find a reference for a prospect in fintech evaluating for their sales team"
- "Who are our best references for enterprise HR buyers?"

---

## Output Format

### Testimonial Request

```markdown
# Testimonial Request: [Customer Name]

**Created**: [Date]
**Data Sources Used**: [CRM, NPS, Gong, etc.]

---

## Request Details
- **Customer**: [Company]
- **Contact**: [Name, Title]
- **Ask**: [Type of testimonial]
- **Use Case**: [Where it will be used]

## Outreach Email

**Subject**: Quick favor – share your experience?

Hi [Name],

I hope this finds you well! I wanted to reach out because [specific positive thing about their experience – reference a win, metric, or recent conversation].

We're working on [specific project: website refresh, campaign, etc.], and your story would really resonate with [target audience]. Would you be open to providing a brief testimonial?

**What we're looking for**:
- [Specific ask: 2-3 sentences / 30-second video / etc.]
- Focus on: [specific topic or result]

**Timeline**: [When needed]

I can make this as easy as possible – happy to draft something for your review, or we can do a quick 5-minute call and I'll write it up.

Let me know what works best for you!

Best,
[Your name]

---

## Draft Testimonial (for review)

**Option 1 (Challenge-focused)**:
"Before [Product], we struggled with [challenge]. Now, [specific improvement]. I'd recommend it to any [role] looking to [outcome]."

**Option 2 (Results-focused)**:
"Since implementing [Product], we've seen [specific metric]. The [specific feature] has been a game-changer for our team."

---

## Approval Process
- [ ] Customer approves quote text
- [ ] Customer approves attribution (name, title, company)
- [ ] Marketing confirms usage rights
```

---

## Automation Options

When configured with integrations, this skill can:

1. **Advocate identification** - Flag high-NPS customers as advocacy candidates
2. **Automated outreach** - Send personalized review and testimonial requests
3. **Reference matching** - Find best references for specific prospect needs
4. **Activity tracking** - Log advocacy activities in CRM
5. **Capacity management** - Track reference fatigue and availability
