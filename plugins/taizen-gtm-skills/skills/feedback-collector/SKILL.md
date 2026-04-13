---
description: Captures skill corrections and suggestions for continuous improvement. Runs silently to log issues without interrupting workflow.
---

# Feedback Collector Skill

Silent feedback capture for skill improvement.

## Purpose

This is a **silent feedback collection skill** that logs user corrections, suggestions, and issues for review by skill owners.

## When This Skill Activates

This skill should be invoked when:
- User explicitly flags a correction ("That's not right", "Actually...", "The correct answer is...")
- User provides feedback on skill output ("This could be better if...", "Missing...", "Inaccurate...")
- User identifies outdated information
- User suggests improvements

## Feedback Capture Format

When feedback is detected, log the following:

```json
{
  "timestamp": "[ISO timestamp]",
  "skill_invoked": "[Which skill was being used]",
  "user_context": "[User role/context if known]",
  "feedback_type": "[correction|suggestion|bug|outdated]",
  "original_output": "[Summary of what the skill produced]",
  "user_feedback": "[Exact user feedback]",
  "suggested_correction": "[If applicable, the correct information]",
  "severity": "[high|medium|low]"
}
```

## Feedback Categories

### Corrections
- Factual errors in skill output
- Outdated information
- Incorrect frameworks or methodologies
- Wrong competitive information

### Suggestions
- Missing information that should be included
- Better ways to structure output
- Additional use cases to support
- New personas or industries to add

### Bugs
- Skill not responding as expected
- Output format issues
- Missing expected sections
- Error conditions

## Output Behavior

This skill is **silent** - it does not produce visible output to the user.

Instead:
1. Acknowledge the user's feedback naturally in conversation
2. Log the feedback in the specified format
3. If possible, incorporate the correction into the current response
4. Continue assisting the user

## Feedback Routing

Feedback should be logged to:
- A shared document or database accessible to skill owners
- Slack channel for real-time awareness (if configured)
- Batch review queue for periodic skill updates

## Quality Signals

Track these metrics from feedback:
- **Correction rate**: How often users correct skill output
- **Feedback sentiment**: Positive vs. negative feedback
- **Common issues**: Repeated problems across users
- **Skill usage**: Which skills generate most feedback

## Usage

This skill is automatically invoked when feedback patterns are detected. It can also be explicitly called:

```
/taizen-gtm-skills:feedback-collector [feedback details]
```

## Continuous Improvement Process

1. **Collect**: Gather feedback through this skill
2. **Aggregate**: Batch similar feedback items
3. **Prioritize**: Rank by frequency and severity
4. **Update**: Modify skills based on feedback
5. **Validate**: Confirm fixes address the issues
6. **Communicate**: Inform users of improvements
