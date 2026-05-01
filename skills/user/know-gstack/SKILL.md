# gstack — Virtual Engineering Team (Garry Tan / YC)

## Trigger
Use when building features, reviewing code, shipping to production, running security audits, or QA testing with Claude Code. Reference any `/gstack` command pattern below.

## What Is gstack
Open-source software factory by Garry Tan (YC President). 23 specialists + 8 power tools as Markdown slash commands. Transforms Claude Code into a virtual engineering team: CEO, eng manager, designer, code reviewer, QA lead, security officer, release engineer. MIT licensed.

**Result claimed:** 810× productivity increase vs baseline (normalized logical lines/day).

## Slash Commands Reference

### Planning
| Command | Purpose |
|---------|---------|
| `/office-hours` | Describe what you're building → structured product feedback |
| `/plan-ceo-review` | Strategic review of feature idea |
| `/plan-eng-review` | Architecture + technical feasibility |
| `/plan-design-review` | Design quality, catch AI slop |
| `/plan-devex-review` | Developer experience review |
| `/autoplan` | Auto-generate full implementation plan |
| `/ce-brainstorm` | Interactive Q&A requirements gathering |

### Execution
| Command | Purpose |
|---------|---------|
| `/review` | Full code review on current branch changes |
| `/ship` | Prepare PR: lint, test, changelog, description |
| `/land-and-deploy` | Merge + deploy pipeline |
| `/canary` | Canary deployment pattern |
| `/careful` | Enable conservative/careful mode |
| `/freeze` / `/unfreeze` | Lock/unlock codebase changes |
| `/guard` | Enable change guard pre-commit hook |

### Quality & Security
| Command | Purpose |
|---------|---------|
| `/qa [url]` | Browser-based QA on staging URL |
| `/qa-only [url]` | QA without other checks |
| `/cso` | Chief Security Officer: OWASP Top 10 + STRIDE threat model |
| `/benchmark` | Performance benchmarks |
| `/investigate [issue]` | Root cause investigation |

### Knowledge & Tooling
| Command | Purpose |
|---------|---------|
| `/browse [url]` | Web browsing (preferred over MCP Chrome tools) |
| `/retro` | Sprint retrospective + learnings capture |
| `/document-release` | Release changelog and docs |
| `/learn` | Extract session learnings into reusable knowledge |
| `/codex` | Spawn Codex subagent for parallel work |

## Full Delivery Cycle
```
/office-hours          ← articulate product vision
/autoplan              ← generate structured plan
[implement the plan]
/review                ← catch bugs pre-merge
/qa https://staging    ← browser QA
/cso                   ← security audit
/ship                  ← prepare PR
/land-and-deploy       ← merge + deploy
/document-release      ← changelog
/retro                 ← capture learnings
```

## Security Audit Only
```
/cso                   ← OWASP Top 10 + STRIDE full audit
/review                ← code-level security + logic review
```

## Install (Claude Code CLI only)
```bash
git clone --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```
Requirements: Claude Code CLI, Git, Bun v1.0+

## Warnings
- `/setup-browser-cookies` imports local browser session cookies — use carefully
- Auto-update runs hourly (throttled, network-failure-safe)
- `/browse` makes external network calls — expected by design
