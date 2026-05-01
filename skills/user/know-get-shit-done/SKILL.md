# GSD (Get Shit Done) — Context Engineering + Spec-Driven Dev

## Trigger
Use when starting a new project with Claude Code, fighting context rot in long sessions, building spec-driven workflows, or managing multi-agent task execution.

## What Is GSD
Lightweight meta-prompting + context engineering system. Solves context rot — quality degradation as Claude fills context window. Works across Claude Code, OpenCode, Gemini CLI, Codex, Cursor, Windsurf, Copilot, and 10+ others.

**Core insight:** Complexity lives in the system, not in your workflow. Behind the scenes: XML prompt formatting, subagent orchestration, state management. What you see: a few commands that work.

## Commands Reference

### Project Setup
| Command | Purpose |
|---------|---------|
| `/gsd-new-project` | Initialize GSD planning structure for new project |
| `/gsd-map-codebase` | Scan + index existing codebase state (use first when returning to project) |
| `/gsd-init` | Bootstrap GSD in current directory |

### Planning
| Command | Purpose |
|---------|---------|
| `/gsd-spec` | Create detailed spec from rough idea (XML-formatted for Claude) |
| `/gsd-plan` | Break spec into ordered task list with dependencies |
| `/gsd-prd` | Generate full PRD with acceptance criteria |
| `/gsd-roadmap` | Strategic feature roadmap |

### Execution
| Command | Purpose |
|---------|---------|
| `/gsd-task [task-id]` | Execute specific task with full context injection |
| `/gsd-next` | Execute next pending task in plan |
| `/gsd-parallel` | Spawn subagents for independent tasks |
| `/gsd-checkpoint` | Save current state, compress context |

### Context Management
| Command | Purpose |
|---------|---------|
| `/gsd-context` | Load full project context for new session |
| `/gsd-compress` | Compress current context window (anti-rot) |
| `/gsd-handoff` | Prepare context handoff for new Claude session |
| `/gsd-status` | Show project state, completed/pending tasks |

### Review & Ship
| Command | Purpose |
|---------|---------|
| `/gsd-review` | Code review with project context |
| `/gsd-test` | Run tests with failure analysis |
| `/gsd-ship` | Prepare release: changelog, PR description |

## Context Rot Prevention
```
Problem: As context window fills → instruction following degrades
GSD solution:
  1. /gsd-checkpoint every N tasks → compress + save state
  2. Fresh Claude session → /gsd-context → restore full context in <1min
  3. XML-structured prompts → more reliable instruction parsing
  4. State in files (not context) → survives session resets
```

## File Structure
```
.gsd/
  project.xml         ← project spec + goals (XML for Claude parsing)
  tasks/
    pending/          ← tasks to execute
    in-progress/      ← active tasks
    completed/        ← done tasks with outcomes
  context/
    codebase-map.md   ← indexed codebase state
    decisions.md      ← architectural decisions log
    handoffs/         ← context handoff snapshots
```

## Returning to Existing Project
```bash
/gsd-map-codebase     ← scan current codebase state
/gsd-new-project      ← init GSD planning with map as context
/gsd-status           ← see what's pending
/gsd-next             ← continue from where you left off
```

## Install
```bash
npx get-shit-done-cc@latest
```
Works on Mac, Windows, Linux. No global install required.
