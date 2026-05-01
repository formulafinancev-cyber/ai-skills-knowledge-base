# Everything Claude Code — Agent Performance System

## Trigger
Use when optimizing Claude Code sessions: token reduction, memory persistence across sessions, security scanning, multi-language projects, agent orchestration patterns.

## What Is It
Anthropic Hackathon Winner. 157K+ stars. Performance optimization system for AI agent harnesses. Production-ready agents, skills, hooks, rules, MCP configs evolved over 10+ months of daily use. Works across Claude Code, Codex, Cursor, OpenCode, Gemini.

## Core Systems

### 1. Token Optimization
- Model selection per task type (Haiku for simple, Sonnet/Opus for complex)
- System prompt slimming: remove redundant instructions, compress context
- Background processes: move non-critical work to async hooks
- `CLAUDE.md` trimming patterns to reduce per-session overhead

### 2. Memory Persistence (Hooks)
Hooks that automatically save/load context across sessions:
```
PreToolUse hook  → inject saved context before each tool call
PostToolUse hook → capture patterns/decisions after completion
SessionEnd hook  → compress + save session learnings
SessionStart hook → load relevant prior context
```
Key files: `~/.claude/hooks/`, session state in `~/.claude/memory/`

### 3. Continuous Learning Pattern
```
Task completes → PM Agent extracts patterns → saves to knowledge base
Error occurs   → PM Agent root causes     → creates prevention checklist
Monthly        → PM Agent prunes old docs  → refreshes knowledge base
```

### 4. Security (AgentShield)
29 lifecycle hooks covering:
- `.env` access blocking
- Destructive command interception
- SQL injection pattern detection in generated code
- Secrets scanning before commit
- GITHUB_TOKEN and API key exposure prevention

### 5. Agent Roles (activate with `@agent-name`)
| Agent | Purpose |
|-------|---------|
| `@agent-backend-architect` | API design, DB schema, service architecture |
| `@agent-frontend-architect` | React/Vue/Svelte component patterns |
| `@agent-security-engineer` | Vulnerability analysis, threat modeling |
| `@agent-performance-engineer` | Profiling, bottleneck identification |
| `@agent-quality-engineer` | Test strategy, coverage, flakiness |
| `@agent-refactoring-expert` | Code smell detection, clean architecture |
| `@agent-devops-architect` | CI/CD, infra, deployment patterns |
| `@agent-pm-agent` | Post-impl documentation, meta-learning |
| `@agent-technical-writer` | Docs, ADRs, changelogs |
| `@agent-requirements-analyst` | PRD creation, scope definition |
| `@agent-root-cause-analyst` | Systematic debugging |

### 6. Hermes Operator (v2.0)
Cross-harness abstraction layer — same skill definitions work across:
Claude Code, Codex, Cursor, OpenCode, Gemini CLI

## Key Patterns

### Context Rot Prevention
Context degrades as window fills. Mitigation:
1. Fresh context windows per logical task (not per session)
2. Structured handoff: save state → new session → load state
3. `CLAUDE.md` as single source of truth for project context

### Multi-Language Hook Rules
Rules files per ecosystem: `.py`, `.jsx`, `.ts`, `.go`, `.java`, `.rs`, `.rb`, `.php`
Each file carries language-specific linting, testing, and security rules.

### Parallelization Pattern
```
Analyze task → identify independent subtasks
→ spawn N subagents via worktrees
→ each subagent gets isolated git branch
→ parent monitors → merges on completion
```

## Install
```bash
npx ecc-universal@latest   # cross-platform installer
# or
git clone https://github.com/affaan-m/everything-claude-code
cp -r everything-claude-code/.claude/ ~/.claude/
```

## Warning
Reads ANTHROPIC_API_KEY and GITHUB_TOKEN from env. MCP integrations connect to external services. Review hooks before production use.
