---
description: Reviews content for quality, clarity, brand alignment, and effectiveness. Use for content QA before publishing.
---

# Content Reviewer Skill

Quality assurance review for all content before publishing.

## Purpose

Ensure content meets quality standards for clarity, accuracy, brand alignment, and effectiveness before it goes live.

## Review Dimensions

### 1. Clarity

**Readability Check**:
- Is the main point clear within the first paragraph?
- Are sentences concise (aim for 15-20 words average)?
- Is jargon explained or avoided?
- Does each paragraph have one main idea?
- Are transitions smooth between sections?

**Structure Check**:
- Is the content logically organized?
- Do headings accurately reflect content?
- Is information easy to scan?
- Is the length appropriate for the format?

### 2. Accuracy

**Fact Check**:
- Are all statistics accurate and sourced?
- Are quotes properly attributed?
- Are claims substantiated?
- Are links working and relevant?
- Is information current/not outdated?

**Technical Accuracy**:
- Are product features described correctly?
- Are technical terms used properly?
- Are processes/steps accurate?

### 3. Brand Alignment

**Voice Check**:
- Does the tone match brand guidelines?
- Is the language on-brand?
- Are we/they/you used consistently?
- Are banned words/phrases avoided?

**Visual Alignment**:
- Do images match brand style?
- Are colors/fonts correct?
- Is formatting consistent?

### 4. Effectiveness

**Goal Achievement**:
- Does content achieve its stated purpose?
- Is the CTA clear and compelling?
- Is the value proposition evident?
- Does it address audience needs?

**SEO (if applicable)**:
- Is the target keyword used appropriately?
- Are meta tags optimized?
- Are headers using keywords naturally?
- Are there internal/external links?

### 5. Legal/Compliance

**Compliance Check**:
- Are required disclaimers present?
- Are claims legally defensible?
- Is proper consent/attribution given?
- Are competitor mentions appropriate?

## Quality Levels

| Level | Description | Pass Criteria |
|-------|-------------|---------------|
| **Publish Ready** | No issues, ready to go live | All checks pass |
| **Minor Edits** | Small fixes needed | < 5 minor issues |
| **Needs Work** | Significant revisions required | Major issues present |
| **Reject** | Fundamental problems | Off-brand, inaccurate, or poor quality |

## Usage

```
/taizen-gtm-skills:content-reviewer [paste content]
/taizen-gtm-skills:content-reviewer blog [paste content]
/taizen-gtm-skills:content-reviewer landing-page [URL or content]
/taizen-gtm-skills:content-reviewer email [paste content]
```

## Output Format

### Content Review Report

```
# Content Review: [Content Title]

## Review Summary

| Attribute | Value |
|-----------|-------|
| Content Type | [Blog/Email/Landing Page/etc.] |
| Reviewer | [Name/Claude] |
| Review Date | [Date] |
| **Status** | **[Publish Ready / Minor Edits / Needs Work / Reject]** |

---

## Score Overview

| Dimension | Score | Notes |
|-----------|-------|-------|
| Clarity | [1-5] ⭐ | [Brief note] |
| Accuracy | [1-5] ⭐ | [Brief note] |
| Brand Alignment | [1-5] ⭐ | [Brief note] |
| Effectiveness | [1-5] ⭐ | [Brief note] |
| **Overall** | **[Avg]** | |

---

## Detailed Feedback

### Clarity

**What Works**:
- [Positive observation]
- [Positive observation]

**Needs Improvement**:
| Issue | Location | Recommendation |
|-------|----------|----------------|
| [Issue] | [Where] | [How to fix] |

**Specific Edits**:
- Current: "[Current text]"
  Suggested: "[Improved text]"

---

### Accuracy

**Verified**:
- [x] [Fact/claim checked]
- [x] [Fact/claim checked]

**Needs Verification**:
- [ ] [Claim to verify]: [Source needed]
- [ ] [Claim to verify]: [Source needed]

**Issues Found**:
| Issue | Location | Correction |
|-------|----------|------------|
| [Issue] | [Where] | [Correct information] |

---

### Brand Alignment

**On Brand**:
- [x] Tone matches guidelines
- [x] Language is appropriate
- [x] [Other brand element]

**Off Brand**:
| Issue | Current | On-Brand Alternative |
|-------|---------|---------------------|
| [Issue] | "[Current]" | "[Alternative]" |

---

### Effectiveness

**Strengths**:
- [What's working]
- [What's working]

**Opportunities**:
| Area | Current | Recommendation |
|------|---------|----------------|
| Headline | [Current] | [Stronger option] |
| CTA | [Current] | [Improvement] |
| Value Prop | [Current state] | [How to strengthen] |

---

### Technical/SEO (if applicable)

**SEO Checklist**:
- [ ] Primary keyword in title
- [ ] Keyword in first 100 words
- [ ] Meta description optimized
- [ ] Headers include keywords
- [ ] Internal links present
- [ ] Images have alt text

**Issues**:
| Issue | Recommendation |
|-------|----------------|
| [Issue] | [Fix] |

---

## Priority Fixes

### Must Fix (Before Publishing)
1. [Critical issue]: [How to fix]
2. [Critical issue]: [How to fix]

### Should Fix (Important)
1. [Important issue]: [How to fix]
2. [Important issue]: [How to fix]

### Nice to Have (Optional)
1. [Enhancement]: [Suggestion]
2. [Enhancement]: [Suggestion]

---

## Edited Version

[If minor edits, provide the corrected version here]

---

## Sign-Off

**Recommendation**: [Approve / Approve with edits / Revise and resubmit]

**Next Steps**:
1. [Action item]
2. [Action item]
```

### Quick Review

```
# Quick Review: [Content Title]

## Status: [Publish Ready / Minor Edits / Needs Work]

### Quick Hits
- ✅ [What's good]
- ✅ [What's good]
- ⚠️ [Concern]
- ❌ [Issue to fix]

### Must-Fix Items
1. [Fix needed]
2. [Fix needed]

### Suggested Improvements
- [Suggestion]
- [Suggestion]
```
