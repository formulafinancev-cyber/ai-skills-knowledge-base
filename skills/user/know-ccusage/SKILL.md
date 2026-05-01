# ccusage — Claude Code Token Usage Analyzer

## Trigger
Use when analyzing Claude Code session costs, tracking token burn rate, comparing model costs, understanding spend patterns, or reporting usage to team.

## What Is ccusage
CLI tool analyzing Claude Code token usage from local JSONL files (`~/.claude/projects/`). No API calls, no credentials, reads only local files. Incredibly fast.

## Commands
```bash
npx ccusage@latest                    # daily summary table
npx ccusage@latest --daily            # breakdown by day
npx ccusage@latest --monthly          # breakdown by month
npx ccusage@latest --session          # breakdown by session
npx ccusage@latest --project          # breakdown by project
npx ccusage@latest --model            # breakdown by model (Haiku/Sonnet/Opus)
npx ccusage@latest --since 2025-01-01 # filter by date
npx ccusage@latest --json             # machine-readable output
npx ccusage@latest --live             # real-time monitor (updates every 5s)
```

## Output Format
```
┌─────────────┬──────────────┬──────────────┬──────────┬──────────┐
│ Date        │ Input Tokens │ Output Tokens│ Cost USD │ Sessions │
├─────────────┼──────────────┼──────────────┼──────────┼──────────┤
│ 2025-05-01  │    245,230   │    38,120    │  $2.14   │    8     │
│ 2025-04-30  │    189,450   │    22,870    │  $1.58   │    5     │
└─────────────┴──────────────┴──────────────┴──────────┴──────────┘
```

## MCP Integration (ccusage/mcp)
Expose usage data to Claude Desktop:
```bash
npm install -g @ccusage/mcp
```
Configure `claude_desktop_config.json`:
```json
{"ccusage": {"command": "ccusage-mcp"}}
```
Then ask Claude: "How much have I spent on Claude Code this month?"

## Multi-Tool Family
| Package | Tracks |
|---------|-------|
| `ccusage` | Claude Code |
| `@ccusage/codex` | OpenAI Codex |
| `@ccusage/opencode` | OpenCode |
| `@ccusage/amp` | Amp CLI |
| `@ccusage/pi` | pi-agent |

## Data Location
Claude Code stores session logs at:
```
~/.claude/projects/{project-hash}/sessions/{session-id}.jsonl
```
ccusage reads these directly — no network, no auth required.

## Cost Calculation
Uses current Anthropic pricing per model:
- claude-haiku-3-5: $0.80/$4.00 per M tokens (in/out)
- claude-sonnet-3-5: $3.00/$15.00 per M tokens
- claude-opus-3-5: $15.00/$75.00 per M tokens

## Useful Queries
```bash
# This month's cost
npx ccusage@latest --monthly --since $(date +%Y-%m-01)

# Most expensive sessions
npx ccusage@latest --session --sort cost --desc | head -10

# Model cost comparison
npx ccusage@latest --model

# Export to CSV
npx ccusage@latest --json | jq -r '.[] | [.date,.cost] | @csv'
```

## Install (permanent)
```bash
npm install -g ccusage
ccusage --daily
```
