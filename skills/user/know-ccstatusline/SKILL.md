# ccstatusline — Terminal Status Line for Claude Code

## Trigger
Use when configuring Claude Code terminal experience, monitoring token usage in real-time, or customizing the Claude Code status display.

## What Is ccstatusline
Customizable status line formatter for Claude Code CLI. Displays model info, git branch, token usage, cost, context window, and other metrics directly in terminal. No external API calls — reads local session files.

## Widgets Available
| Widget | Shows |
|--------|-------|
| `model` | Current model (Haiku/Sonnet/Opus) |
| `tokens` | Input + output tokens for session |
| `cost` | Session cost in USD |
| `context` | Context window usage % |
| `git` | Current git branch |
| `git-status` | Staged/unstaged changes |
| `compaction` | Context compaction status |
| `reset-timer` | Time until context auto-reset |
| `session` | Session ID (short) |
| `time` | Current time |

## Configuration (~/.ccstatusline.json)
```json
{
  "format": "{model} | {git} | {tokens} | {cost} | {context}",
  "separator": " | ",
  "theme": "powerline",
  "update_interval": 2,
  "widgets": {
    "cost": {"currency": "USD", "decimals": 4},
    "context": {"warn_at": 70, "critical_at": 90},
    "tokens": {"show_total": true}
  }
}
```

## Themes
- `default` — plain text
- `powerline` — Powerline symbols (requires Nerd Font)
- `minimal` — ultra-compact
- `detailed` — all metrics

## Install
```bash
npm install -g ccstatusline
ccstatusline --init    # creates default config + adds to Claude Code hooks
```

## Hook Integration (automatic after --init)
Added to `~/.claude/settings.json`:
```json
{
  "hooks": {
    "PostToolUse": ["ccstatusline --update"],
    "Notification": ["ccstatusline --flash"]
  }
}
```

## Typical Status Line
```
claude-sonnet-3-5 | feat/auth | ↑12.4K ↓2.1K | $0.0234 | ▓▓▓▓▓░░░░░ 52%
```

## Windows Support
See `docs/WINDOWS.md` — uses different terminal escape sequences. PowerShell and Windows Terminal both supported.

## Version 2.2.x Features
- GitLab support (in addition to GitHub)
- Reset timer widget (shows when context will auto-compress)
- Context compaction indicator
- Git diff stats widget
