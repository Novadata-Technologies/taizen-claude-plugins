# Taizen Claude Plugins

A marketplace of Claude plugins for **sales**, **sales enablement**, **product marketing**, and **customer marketing** teams. Purpose-built skills for GTM excellence.

## Overview

This repository contains a Claude plugin marketplace with **30+ comprehensive skills** for go-to-market teams. The skills work with Claude Cowork, Claude Code, and the Claude Plugins Marketplace.

## Installation

### Claude Code (CLI)

```bash
# Add the marketplace
/plugin marketplace add Novadata-Technologies/taizen-claude-plugins

# Install the GTM skills plugin
/plugin install taizen-gtm-skills@taizen-plugins
```

### Claude Desktop / Cowork

1. Open Claude Desktop
2. Navigate to Plugins
3. Add marketplace: `Novadata-Technologies/taizen-claude-plugins`
4. Install `taizen-gtm-skills`

### Local Development

```bash
# Test locally with Claude Code
claude --plugin-dir ./plugins/taizen-gtm-skills

# Validate the plugin
/plugin validate .
```

## Available Skills

### Foundation & Context (3 skills)

| Skill | Description |
|-------|-------------|
| `product-context` | Creates foundational PMM context (positioning, audience, messaging, voice) - **run first** |
| `session-context` | **(Silent)** Establishes user role and context to personalize outputs |
| `feedback-collector` | **(Silent)** Captures skill corrections for continuous improvement |

### Product Marketing (6 skills)

| Skill | Description |
|-------|-------------|
| `messaging-positioning` | Builds positioning statements, value props, message houses |
| `competitive-intelligence` | Produces competitor analysis, battlecards, and comparison pages |
| `customer-research` | Develops ICP, personas, JTBD, and voice of customer insights |
| `go-to-market` | Plans launches, campaigns, and cross-functional execution |
| `pricing-packaging` | Recommends pricing models, tier structures, and value metrics |
| `industry-insights` | Vertical market intelligence (Healthcare, Retail, Financial Services, etc.) |

### Customer Marketing (4 skills)

| Skill | Description |
|-------|-------------|
| `case-study-builder` | Creates customer case studies from interviews and data |
| `customer-advocacy` | Manages reference programs, testimonials, and advocacy initiatives |
| `community-signals` | Monitors community feedback, social signals, and sentiment |
| `newsletter-writer` | Creates customer newsletters and email communications |

### Content Marketing (6 skills)

| Skill | Description |
|-------|-------------|
| `brand-voice` | Ensures consistent brand voice across all content |
| `seo-content` | Creates SEO-optimized articles and web content |
| `social-content` | Creates social media posts and content calendars |
| `email-sequences` | Designs nurture sequences and automated email flows |
| `copywriting` | Writes marketing copy for landing pages, ads, and CTAs |
| `content-reviewer` | Reviews content for quality and brand alignment |

### Sales Enablement (8 skills)

| Skill | Description |
|-------|-------------|
| `sales-playbook` | Sales methodology framework with deal stages and qualification criteria |
| `account-research` | Researches accounts, maps stakeholders, preps meeting briefs |
| `discovery-prep` | Creates discovery questions and demo guidance |
| `objections-prep` | Prepares responses for anticipated objections |
| `outreach-templates` | Generates personalized outreach sequences |
| `executive-briefings` | Preps for C-level meetings and executive events |
| `buyer-profiles` | Buyer personas with priorities, language, and objection patterns |
| `roi-builder` | Creates ROI models, business cases, and proposal support |

### Account Management (3 skills)

| Skill | Description |
|-------|-------------|
| `account-lifecycle` | Supports account plans, renewals, and expansion strategies |
| `sales-coaching` | Deal reviews, win/loss analysis, and rep coaching frameworks |
| `gtm-messaging` | Core messaging guidelines and value framing principles |

## Usage Examples

Skills activate automatically based on your request. Just ask Claude naturally.

> **Claude Code users**: You can also invoke skills directly with `/skill-name`

### Product Marketing

```
"Help me create foundational product context for our platform"
"Build a positioning statement for our analytics feature"
"Create a battlecard comparing us to Competitor X"
"Plan a go-to-market launch for our Q3 release"
"Recommend a pricing strategy for our enterprise tier"
```

Claude Code: `/product-context`, `/messaging-positioning`, `/competitive-intelligence`, `/go-to-market`, `/pricing-packaging`

### Customer Marketing

```
"Create a case study for our Acme Corp implementation"
"Design a customer advocacy and reference program"
"Summarize community signals from the past month"
"Write a customer newsletter for this quarter"
```

Claude Code: `/case-study-builder`, `/customer-advocacy`, `/community-signals`, `/newsletter-writer`

### Content Marketing

```
"Create an SEO content brief for 'sales automation tools'"
"Write a LinkedIn post about our product update"
"Design a nurture email sequence for trial signups"
"Write landing page copy for our free trial"
"Review this blog post for brand voice and quality"
```

Claude Code: `/seo-content`, `/social-content`, `/email-sequences`, `/copywriting`, `/content-reviewer`

### Sales Enablement

```
"Give me deal strategy guidance for this enterprise opportunity"
"Build an ROI model for reducing manual data entry"
"Research Acme Corp before my discovery call"
"Prep discovery questions for a meeting with their CHRO"
"What should I know about selling to a CFO?"
"Write a cold outreach sequence for Jane Smith, VP HR at Acme"
"Prep me for an executive briefing with Acme's CEO"
"Analyze why we lost the TechCorp deal"
```

Claude Code: `/sales-playbook`, `/roi-builder`, `/account-research`, `/discovery-prep`, `/buyer-profiles`, `/outreach-templates`, `/executive-briefings`, `/sales-coaching`

## Scheduling with Taizen

Automate recurring GTM tasks with [Taizen](https://usetaizen.com). Connect the Taizen MCP server and describe what you want to schedule in natural language:

```
"Every Monday morning, research my upcoming discovery calls and prep briefings"
"At the start of each quarter, audit our content for messaging consistency"
"When a new competitor is mentioned in Slack, create a competitive summary"
"Weekly, summarize community signals and post to #product-marketing"
```

### How It Works

1. **Sign up** at [usetaizen.com](https://usetaizen.com)
2. **Connect** the Taizen MCP integration in your Claude settings
3. **Describe** your automation in natural language
4. **Taizen runs** your scheduled agents and delivers results to Slack, Google Drive, Notion, or other destinations

## Repository Structure

```
taizen-claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace catalog
├── plugins/
│   └── taizen-gtm-skills/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin metadata
│       ├── .mcp.json             # MCP server integrations
│       └── skills/
│           │
│           │── # Foundation
│           ├── product-context/
│           ├── session-context/
│           ├── feedback-collector/
│           │
│           │── # Product Marketing
│           ├── messaging-positioning/
│           ├── competitive-intelligence/
│           ├── customer-research/
│           ├── go-to-market/
│           ├── pricing-packaging/
│           ├── industry-insights/
│           │
│           │── # Customer Marketing
│           ├── case-study-builder/
│           ├── customer-advocacy/
│           ├── community-signals/
│           ├── newsletter-writer/
│           │
│           │── # Content Marketing
│           ├── brand-voice/
│           ├── seo-content/
│           ├── social-content/
│           ├── email-sequences/
│           ├── copywriting/
│           ├── content-reviewer/
│           │
│           │── # Sales Enablement
│           ├── sales-playbook/
│           ├── account-research/
│           ├── discovery-prep/
│           ├── objections-prep/
│           ├── outreach-templates/
│           ├── executive-briefings/
│           ├── buyer-profiles/
│           ├── roi-builder/
│           │
│           │── # Account Management
│           ├── account-lifecycle/
│           ├── sales-coaching/
│           └── gtm-messaging/
│
├── README.md
└── LICENSE
```

## Customization

### Adding Your Own Context

The skills are designed to work out of the box but become more powerful with your organization's specific:

- **Product positioning** and value propositions
- **Buyer personas** with your terminology and research
- **Industry verticals** you serve
- **Competitive battlecards** and positioning
- **Case studies** and proof points
- **Brand voice** guidelines

**Recommended approach**:
1. Fork this repository
2. Run `/taizen-gtm-skills:product-context` to create your foundational context
3. Save outputs to a context file that other skills can reference
4. Modify skill definitions to incorporate your proprietary data

### Creating Custom Skills

1. Create a new directory under `plugins/taizen-gtm-skills/skills/`
2. Add a `SKILL.md` file with frontmatter:

```markdown
---
name: skill-name
description: Brief description of what this skill does
---

# Skill Name

[Skill instructions and templates]
```

3. Run `/reload-plugins` to pick up changes

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with `claude --plugin-dir ./plugins/taizen-gtm-skills`
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Support

- **Issues**: [GitHub Issues](https://github.com/Novadata-Technologies/taizen-claude-plugins/issues)
- **Documentation**: [Claude Plugins Docs](https://code.claude.com/docs/en/plugins)

---

Built for GTM teams by [Taizen](https://usetaizen.com)
