# Vibe Kanban — Kanban Board for Multi-Agent Coding

## Trigger
Use when planning and managing parallel coding agent tasks, reviewing AI-generated diffs, orchestrating multiple agents across a project, or managing a team using Claude Code + other agents.

## What Is Vibe Kanban
Kanban board to plan + review coding agent work. Issues on board → agent executes in workspace (branch + terminal + dev server) → review diffs inline → merge. Supports 10+ coding agents.

**⚠️ Note:** Project announced sunsetting as of April 2026. May not receive future updates.

## Supported Agents
Claude Code, Codex, Gemini CLI, GitHub Copilot, Amp, Cursor, OpenCode, Factory Droid, CCR, Qwen Code

## Core Concepts

### Issues
- Created on kanban board (like GitHub Issues)
- Have: title, description, acceptance criteria, labels, assignee (agent)
- States: Backlog → Ready → In Progress → Review → Done

### Workspaces
- Each issue gets an isolated workspace: git branch + terminal + dev server
- Agent executes in workspace without affecting other work
- Multiple workspaces run in parallel

### Review Flow
```
Issue assigned to agent
  └─► Agent executes in workspace
        └─► Workspace shows: live terminal output + running app preview
              └─► Agent marks "ready for review"
                    └─► Reviewer sees: diff + inline comment UI
                          └─► Approve → merge PR
                           └─► Request changes → agent continues
```

## Key Features
- **Built-in browser** with devtools, inspect mode, device emulation
- **Inline diff comments** — leave feedback directly on code changes
- **AI PR descriptions** — auto-generated from workspace diff
- **Preview URLs** — each workspace gets a local preview URL

## Quick Start
```bash
npx vibe-kanban          # start local server (port 3000)
# Opens http://localhost:3000 in browser
```

## Workflow
```
1. Create issue: "Implement user preferences modal"
2. Assign to Claude Code
3. Open workspace → agent starts working
4. Watch live terminal + preview
5. Agent completes → diff review
6. Leave inline comments if needed
7. Approve + create PR
8. Merge
```

## Team Usage
- Issues visible to all team members
- Workspaces can be shared via local network
- Note: PostHog analytics present but defaults disabled

## Alternative (actively maintained)
Since Vibe Kanban is sunsetting, consider:
- `subtask` — CLI-based parallel worktree management (actively maintained)
- `ccpm` — spec-driven with GitHub Issues integration
