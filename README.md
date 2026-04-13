# Taizen Claude Plugins

A marketplace of Claude plugins for **sales**, **product marketing**, and **customer marketing** teams. Purpose-built skills for GTM excellence.

## Overview

This repository contains a Claude plugin marketplace with **30 comprehensive skills** for go-to-market teams. The skills are designed to work with Claude Code, Claude Desktop (via Cowork), and the Claude Plugins Marketplace.

## Installation

### Claude Code (CLI)

```bash
# Add the marketplace
/plugin marketplace add taizen-ai/taizen-claude-plugins

# Install the GTM skills plugin
/plugin install taizen-gtm-skills@taizen-plugins
```

### Claude Desktop / Cowork

1. Open Claude Desktop
2. Navigate to Plugins
3. Add marketplace: `taizen-ai/taizen-claude-plugins`
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

### Product Marketing

```bash
# Create foundational product context (do this first!)
/taizen-gtm-skills:product-context

# Develop positioning for a new product
/taizen-gtm-skills:messaging-positioning positioning statement for [product]

# Research a competitor
/taizen-gtm-skills:competitive-intelligence battlecard [competitor name]

# Plan a product launch
/taizen-gtm-skills:go-to-market launch [product/feature]

# Develop pricing strategy
/taizen-gtm-skills:pricing-packaging strategy [product]
```

### Customer Marketing

```bash
# Create a customer case study
/taizen-gtm-skills:case-study-builder [customer name]

# Prep for case study interview
/taizen-gtm-skills:case-study-builder interview-prep [customer]

# Design customer advocacy program
/taizen-gtm-skills:customer-advocacy program-design

# Generate community signals digest
/taizen-gtm-skills:community-signals digest [time period]
```

### Content Marketing

```bash
# Create SEO content brief
/taizen-gtm-skills:seo-content brief [keyword/topic]

# Write LinkedIn post
/taizen-gtm-skills:social-content post linkedin [topic]

# Create email nurture sequence
/taizen-gtm-skills:email-sequences nurture [trigger/audience]

# Write landing page copy
/taizen-gtm-skills:copywriting landing-page [product/offer]

# Review content before publishing
/taizen-gtm-skills:content-reviewer [paste content]
```

### Sales Enablement

```bash
# Get deal strategy guidance
/taizen-gtm-skills:sales-playbook deal-strategy [opportunity details]

# Build ROI model for a deal
/taizen-gtm-skills:roi-builder model [use case]

# Research an account
/taizen-gtm-skills:account-research discovery Acme Corp

# Prepare for a discovery meeting
/taizen-gtm-skills:discovery-prep Acme Corp CHRO meeting

# Get buyer profile guidance
/taizen-gtm-skills:buyer-profiles CHRO

# Generate cold outreach
/taizen-gtm-skills:outreach-templates cold Jane Smith, VP HR at Acme Corp

# Prep for executive meeting
/taizen-gtm-skills:executive-briefings meeting CFO at Acme Corp

# Analyze a lost deal
/taizen-gtm-skills:sales-coaching loss-analysis [deal details]
```

## Repository Structure

```
taizen-claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace catalog
├── plugins/
│   └── taizen-gtm-skills/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin metadata
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

## Inspired By

This plugin was inspired by excellent work in the community:
- [pmalliance/product-marketing-skills](https://github.com/pmalliance/product-marketing-skills)
- [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)
- [timescale/marketing-skills](https://github.com/timescale/marketing-skills)
- [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)

## License

MIT License - see [LICENSE](LICENSE) for details.

## Support

- **Issues**: [GitHub Issues](https://github.com/taizen-ai/taizen-claude-plugins/issues)
- **Documentation**: [Claude Plugins Docs](https://code.claude.com/docs/en/plugins)

---

Built for GTM teams by [Taizen](https://taizen.ai)
