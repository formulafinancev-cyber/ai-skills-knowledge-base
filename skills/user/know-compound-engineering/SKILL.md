# Compound Engineering — Each Unit Makes the Next Easier

## Trigger
Use when planning features with AI, doing code review, debugging, documenting learnings, or building a knowledge base that improves future AI sessions.

## Philosophy
**80% planning + review, 20% execution.** Traditional dev accumulates debt. Compound engineering inverts: each brainstorm sharpens the plan, each plan shrinks execution, each review catches patterns not just bugs, each compound note means the next agent doesn't relearn the same lesson.

## Commands (37 skills, 51 agents)

### Upstream (before the loop)
| Command | Purpose |
|---------|---------|
| `/ce-strategy` | Create/maintain `STRATEGY.md` — product target, approach, persona, metrics, tracks. Read by all other commands as grounding. |
| `/ce-ideate` | Generate + critically evaluate big ideas before choosing. Produces ranked ideation artifact. |

### Core Loop
| Command | Purpose |
|---------|---------|
| `/ce-brainstorm` | Interactive Q&A → right-sized requirements doc |
| `/ce-plan` | Requirements doc → detailed implementation plan |
| `/ce-work` | Execute plan with worktrees + task tracking |
| `/ce-debug` | Reproduce failure → trace root cause → fix |
| `/ce-code-review` | Multi-agent review before merge |
| `/ce-doc-review` | Documentation quality review |
| `/ce-compound` | Document learnings → reusable patterns for future agents |

### Read-Side
| Command | Purpose |
|---------|---------|
| `/ce-product-pulse [24h\|7d\|30d]` | Time-windowed report: usage, performance, errors, followups. Saved to `docs/pulse-reports/`. |

## Typical Cycle
```bash
/ce-brainstorm "make background job retries safer"
/ce-plan docs/brainstorms/background-job-retry-safety-requirements.md
/ce-work
/ce-code-review
/ce-compound          ← captures: what worked, what didn't, patterns found
```

## Bug Investigation Cycle
```bash
/ce-debug "checkout webhook sometimes creates duplicate invoices"
/ce-code-review
/ce-compound
```

## File Structure Created
```
STRATEGY.md                    ← product anchor (all commands read this)
docs/brainstorms/              ← requirements docs from /ce-brainstorm
docs/plans/                    ← implementation plans from /ce-plan
docs/compound/                 ← reusable patterns from /ce-compound
docs/pulse-reports/            ← time-windowed pulse reports
```

## Compounding Effect
```
Session 1: /ce-compound → "learned: retry with jitter, not fixed delay"
Session 2: /ce-plan reads compound/ → plan already includes jitter
Session 3: /ce-brainstorm reads compound/ → avoids known failure modes
Result: each cycle is faster and higher quality than the last
```

## Setup
```bash
/ce-setup    ← run in any project, checks env, installs tools, bootstraps config
```

## Install
```bash
/plugin marketplace add https://github.com/EveryInc/compound-engineering-plugin
```
Source: https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents
