---
name: code-review-pr
description: Use when reviewing pull requests, performing automated code review on PRs, checking CLAUDE.md compliance, scanning for bugs, or when user says /code-review
---

# Code Review PR

## Overview

Automated pull request code review using multiple parallel agents with confidence-based scoring to filter false positives. Adapted from the official Anthropic Claude Code plugin by Boris Cherny.

## When to Use

- User asks to review a pull request
- User runs `/code-review` or `/code-review --comment`
- User asks to check PR for bugs or guideline compliance
- Before merging non-trivial PRs

## When NOT to Use

- Closed or draft PRs
- Trivial automated PRs (dependency bumps, formatting-only)
- PRs that already have a code review from you

## Requirements

- Git repository with GitHub remote
- GitHub CLI (`gh`) installed and authenticated
- CLAUDE.md files (optional, improves guideline checking)

## Command

```
/code-review [--comment]
```

- Without `--comment`: output review to terminal only
- With `--comment`: post review as a GitHub PR comment

## Workflow

Follow these steps precisely:

### Step 1: Eligibility Check (Haiku agent)

Check if the PR: (a) is closed, (b) is draft, (c) doesn't need review (automated/trivial), or (d) already has your review. If any → stop.

### Step 2: Gather CLAUDE.md Files (Haiku agent)

Return file paths (not contents) of all relevant CLAUDE.md files: root CLAUDE.md + any CLAUDE.md files in directories modified by the PR.

### Step 3: Summarize PR (Haiku agent)

View the PR and return a summary of the change.

### Step 4: Parallel Review — Launch 5 Sonnet Agents

Each agent returns a list of issues with description + reason (e.g. "CLAUDE.md adherence", "bug", "historical context").

| Agent | Task |
|-------|------|
| **#1 CLAUDE.md compliance** | Audit changes against CLAUDE.md guidelines. Only consider CLAUDE.md files scoped to modified file paths. Note: CLAUDE.md is guidance for code-writing, not all instructions apply during review. |
| **#2 Bug scanner** | Shallow scan for obvious bugs in the diff only. No extra context. Focus on significant bugs, ignore nitpicks and likely false positives. |
| **#3 History analyzer** | Read git blame and history of modified code, identify bugs in light of historical context. |
| **#4 PR history** | Read previous PRs that touched these files, check for comments that may apply to the current PR. |
| **#5 Code comments** | Read code comments in modified files, verify changes comply with inline guidance. |

All agents receive the PR title and description for context about author intent.

### Step 5: Confidence Scoring — Parallel Haiku Agents (one per issue)

Each agent scores an issue 0–100 using this rubric (give verbatim to agent):

| Score | Meaning |
|-------|---------|
| **0** | False positive. Doesn't stand up to light scrutiny, or is pre-existing. |
| **25** | Might be real, but could be false positive. Couldn't verify. Stylistic issues not explicitly in CLAUDE.md. |
| **50** | Verified real, but may be a nitpick or rarely hit in practice. Not very important relative to the PR. |
| **75** | Double-checked and very likely real. Will be hit in practice. Existing approach insufficient. Directly impacts functionality or directly mentioned in CLAUDE.md. |
| **100** | Absolutely certain. Confirmed real, will happen frequently. Evidence directly confirms this. |

For CLAUDE.md issues: agent must verify the CLAUDE.md actually calls out that specific issue.

### Step 6: Filter

Remove all issues scored < 80. If nothing remains → stop (or post "no issues" if `--comment`).

### Step 7: Re-check Eligibility (Haiku agent)

Repeat step 1 to confirm PR still eligible.

### Step 8: Output / Comment

**Terminal output (no `--comment`):** List issues with brief descriptions. If none: "No issues found. Checked for bugs and CLAUDE.md compliance."

**With `--comment`:** Use `gh pr comment` to post. Format:

```
### Code review

Found N issues:

1. <description> (CLAUDE.md says "<quote>")

<github-permalink>

2. <description> (bug due to <reason>)

<github-permalink>

🤖 Generated with [Claude Code](https://claude.ai/code)

- If this code review was useful, please react with 👍. Otherwise, react with 👎.
```

Or if no issues:

```
### Code review

No issues found. Checked for bugs and CLAUDE.md compliance.

🤖 Generated with [Claude Code](https://claude.ai/code)
```

## Link Format (Critical)

Links must follow this exact format or GitHub Markdown rendering breaks:

```
https://github.com/OWNER/REPO/blob/FULL_SHA/path/file.ext#L<start>-L<end>
```

- Must use **full SHA** (not abbreviated, not `$(git rev-parse HEAD)`)
- Must use `#L` notation with line range
- Provide at least 1 line of context before and after (e.g. commenting on lines 5–6 → link to `L4-L7`)
- Repo name must match the repo being reviewed

## False Positive Examples (for steps 4 & 5)

Issues to filter out:

- Pre-existing issues not introduced by this PR
- Looks like a bug but isn't actually one
- Pedantic nitpicks a senior engineer wouldn't flag
- Issues a linter/typechecker/compiler would catch (imports, types, formatting, tests)
- General code quality (test coverage, docs, security) unless required by CLAUDE.md
- CLAUDE.md violations explicitly silenced in code (lint ignore comments)
- Intentional functionality changes related to the broader change
- Real issues on lines the user did not modify

## Notes

- Do NOT build, typecheck, or run tests — CI handles that separately
- Use `gh` CLI for all GitHub interactions (not web fetch)
- Make a todo list before starting
- Cite and link every flagged issue (link CLAUDE.md references)
- Keep output brief, no emojis in comments
- Use Opus-tier agents for bugs/logic, Sonnet for CLAUDE.md compliance, Haiku for scoring/eligibility

## Confidence Threshold

Default: **80**. Adjust by changing the filter threshold in step 6.

## Customization

Add more agents in step 4 for:
- Security-focused review
- Performance analysis
- Accessibility checking
- Documentation quality
