# Subtask — Parallel Git Worktree Agent Orchestration

## Trigger
Use when executing multiple independent tasks in parallel with Claude Code, managing subagents across git worktrees, or tracking multi-agent progress with a TUI.

## What Is Subtask
CLI + Claude Code skill for creating tasks, spawning subagents in isolated git worktrees, tracking progress, reviewing work, and merging. Each task = separate branch = no conflicts. Claude can interrupt and message subagents mid-execution.

## Core Concept
```
Main Claude → drafts tasks → each task gets git worktree
                           → subagent executes in isolation
                           → main Claude monitors + reviews
                           → merges on approval
```

## Workflow
```bash
# 1. Draft tasks (Claude uses skill)
subtask draft fix/auth-bug "Fix auth token refresh race condition"
subtask draft feat/api-metrics "Add Prometheus metrics to all endpoints"
subtask draft feat/ui-redesign "Redesign dashboard with new design system"

# 2. Run tasks
subtask run fix/auth-bug       # spawns subagent in worktree
subtask run-all                # runs all pending tasks in parallel

# 3. Monitor
subtask list                   # show all tasks with status
subtask tui                    # launch interactive TUI
subtask log fix/auth-bug       # show subagent output

# 4. Review
subtask diff fix/auth-bug      # show changes
subtask review fix/auth-bug    # Claude reviews the work
subtask request-changes fix/auth-bug "Add unit tests"  # send feedback to subagent

# 5. Merge
subtask merge fix/auth-bug     # merge to current branch
subtask merge-all              # merge all approved tasks
```

## Task States
```
draft      → defined, not started
working    → subagent actively executing
replied    → subagent finished, awaiting review
approved   → reviewed, ready to merge
merged     → integrated into main branch
blocked    → subagent waiting for input
failed     → execution error
```

## TUI Layout
```
┌─ Tasks ──────────────────┐ ┌─ Diff ─────────────────────────────┐
│ ● fix/auth-bug  [replied]│ │ @@ -45,7 +45,12 @@                 │
│ ○ feat/metrics  [working]│ │ + const token = await refresh()    │
│ ○ feat/ui       [draft]  │ │ + if (!token) throw new AuthError  │
└──────────────────────────┘ └────────────────────────────────────┘
┌─ Conversation ───────────────────────────────────────────────────┐
│ Main: Please add retry logic with exponential backoff            │
│ Sub:  Done, added 3 retries with jitter. See auth.ts:78          │
└──────────────────────────────────────────────────────────────────┘
```

## Interrupting Subagents
Main Claude can send messages to running subagents:
```bash
subtask message feat/metrics "Use histogram not counter for latency"
```
Subagent receives message, adjusts work, continues.

## Codex Subagents
```bash
subtask run fix/auth-bug --agent codex    # use Codex instead of Claude
```

## Install
```bash
curl -fsSL https://subtask.dev/install.sh | bash
subtask install    # add skill to Claude Code
```

## Use Case: FFA Parallel Development
```bash
subtask draft fix/bdr-parser "Fix _readSettings column index bug"
subtask draft fix/iiko-bank "Add missing bank key to CFG.IIKO.LABELS"
subtask draft feat/health-check "Implement M10 Health Check dashboard"
subtask run-all
# Three fixes developed in parallel, merged independently
```
