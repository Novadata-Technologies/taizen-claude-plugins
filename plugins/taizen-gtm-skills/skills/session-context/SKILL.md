---
description: Establishes user role and team context at session start to personalize outputs. Runs silently without producing visible output.
disable-model-invocation: false
---

# Session Context Skill

Automatically gather context about the current user to personalize all subsequent outputs.

## Purpose

Identify the current user and gather context about their role, team, and responsibilities to personalize all subsequent interactions and outputs.

## Workflow

1. **Identify User**: Search for the user's first and last name in available context (environment variables, git config, or ask if needed)

2. **Determine Role**: Based on user identification, determine:
   - Job title and function (Sales, Marketing, Customer Success, etc.)
   - Team or department
   - Seniority level
   - Key responsibilities

3. **Set Session Context**: Store this context to inform all subsequent skill outputs:
   - Adapt language and terminology to user's expertise level
   - Focus on metrics and outcomes relevant to their role
   - Tailor recommendations to their sphere of influence

## Context Variables to Set

- `user_name`: Full name of the user
- `user_role`: Job title/function
- `user_team`: Department or team
- `user_seniority`: Level (IC, Manager, Director, VP, C-level)
- `user_focus_areas`: Primary responsibilities

## Output Behavior

This skill is **silent** - it does not produce visible output to the user. Instead, it sets internal context that other skills will reference.

When context is successfully gathered, proceed with the user's original request using the established context.

If unable to determine user context, proceed with reasonable defaults for a GTM professional.
