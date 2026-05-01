# CCPM — Spec-Driven Project Management Agent

## Trigger
Use when planning features with AI agents, managing multi-agent parallel work, syncing tasks to GitHub Issues, preventing context loss between sessions, or structuring PRDs into executable tasks.

## What Is CCPM
Spec-driven development for AI agents. Turns ideas into PRDs → epics → GitHub Issues → parallel agent execution. Full traceability at every step. Works with Claude Code, Codex, OpenCode, Factory, Amp, Cursor.

**Core problem solved:** Context evaporates between sessions. Parallel work creates conflicts. Requirements drift from verbal decisions. Progress invisible until the end.

## Workflow Pipeline
```
Idea
  └─► /ccpm-brainstorm    → guided Q&A → structured PRD
        └─► /ccpm-epic     → PRD → epic breakdown
              └─► /ccpm-task → epics → GitHub Issues (atomic, executable)
                    └─► /ccpm-parallel → spawn N agents in git worktrees
                          └─► /ccpm-merge → conflict-free merge with traceability
```

## Slash Commands
| Command | Purpose |
|---------|---------|
| `/ccpm-brainstorm` | Guided Q&A to create PRD from rough idea |
| `/ccpm-epic` | Break PRD into epics (large logical chunks) |
| `/ccpm-task` | Decompose epic into atomic GitHub Issues |
| `/ccpm-parallel` | Spawn parallel subagents in isolated worktrees |
| `/ccpm-status` | Show progress across all active issues |
| `/ccpm-merge` | Merge parallel work with conflict resolution |
| `/ccpm-retro` | Post-sprint retrospective + pattern capture |
| `/ccpm-context` | Load full project context for new session |

## Example Interaction
```
User: "I want to build a notification system"

CCPM:
  → /ccpm-brainstorm (asks: real-time? email? in-app? user prefs?)
  → Creates NOTIFICATION_PRD.md
  → /ccpm-epic → 4 epics: backend, frontend, email, preferences
  → /ccpm-task → 12 GitHub Issues with acceptance criteria
  → /ccpm-parallel → 3 agents working in parallel on 3 issues
  → Each agent commits to feature/issue-{N} branch
  → /ccpm-merge → squash merge with full traceability
```

## GitHub Issues Integration
- Each task = 1 GitHub Issue with: acceptance criteria, dependencies, effort estimate
- Labels: `ccpm:epic`, `ccpm:task`, `ccpm:blocked`, `ccpm:in-progress`
- Issues closed automatically on merge
- Full audit trail: PRD → Epic → Issue → Commit

## Parallel Execution System
```
Main agent creates worktrees:
  /worktrees/feature-auth/
  /worktrees/feature-notifications/
  /worktrees/feature-payments/

Each subagent:
  - Gets isolated git worktree (no conflicts)
  - Has full context: PRD + epic + specific issue
  - Reports progress via /ccpm-status
  - Requests review via /ccpm-review-request
```

## Context Persistence Pattern
```
Session start: /ccpm-context → loads PRD + open issues + last decisions
Session end:   CCPM auto-saves: decisions made, blockers, next steps
New session:   context restored in <30 seconds
```

## Install
```bash
curl -sSL https://automaze.io/ccpm/install | bash
# or manually:
git clone https://github.com/automazeio/ccpm ~/.claude/skills/ccpm
```

## Core Principle: No Vibe Coding
Requirements MUST be written before implementation. CCPM enforces: no `/ccpm-parallel` without a completed Issue. No Issue without an Epic. No Epic without a PRD.
