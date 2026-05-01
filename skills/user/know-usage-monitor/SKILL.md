# Claude Code Usage Monitor — Real-Time Token Dashboard

## Trigger
Use when monitoring Claude Code token consumption in real-time, predicting session costs, tracking burn rate, or alerting on context window limits.

## What Is It
Python terminal dashboard reading local Claude Code JSONL files. ML-based predictions for remaining session budget. No external network calls — fully offline.

## Install
```bash
uv tool install claude-monitor
# or:
pip install claude-monitor --break-system-packages
```

## Launch
```bash
claude-monitor                   # interactive dashboard
claude-monitor --refresh 5       # refresh every 5 seconds
claude-monitor --session latest  # show only current session
claude-monitor --export daily    # export daily summary
```

## Dashboard Layout
```
┌─ Session Stats ─────────────────────────────────────────────────┐
│ Model: claude-sonnet-4-5    Session cost: $0.0847               │
│ Input:  145,230 tokens      Output: 22,180 tokens               │
│ Context window: ████████░░ 78% (155,980 / 200,000)             │
└─────────────────────────────────────────────────────────────────┘
┌─ Predictions ───────────────────────────────────────────────────┐
│ Estimated remaining tasks before compaction: ~8                 │
│ Projected session cost at current rate: $0.31                   │
│ Context reset predicted in: ~12 tool calls                      │
└─────────────────────────────────────────────────────────────────┘
┌─ Hourly Burn Rate ──────────────────────────────────────────────┐
│ 10:00 ████████████ 45K tokens                                   │
│ 11:00 ████████████████████ 78K tokens ← peak                   │
│ 12:00 ████████ 32K tokens                                       │
└─────────────────────────────────────────────────────────────────┘
┌─ Today's Summary ───────────────────────────────────────────────┐
│ Sessions: 8    Total tokens: 847K    Total cost: $2.14          │
│ Avg session: 106K tokens    Longest: 198K tokens                │
└─────────────────────────────────────────────────────────────────┘
```

## ML Predictions
Trains on your historical JSONL data to predict:
- When context window will reach 90% (trigger compact)
- Expected total session cost given current task
- Optimal model switch point (when to use Haiku vs Sonnet)

## Configuration (~/.claude-monitor/config.yaml)
```yaml
refresh_interval: 3         # seconds
warn_context_at: 75         # % context used → yellow
alert_context_at: 90        # % context used → red, bell
models:
  claude-sonnet-4-5:
    context_window: 200000
    cost_in: 3.00           # per M tokens
    cost_out: 15.00
  claude-haiku-4-5:
    context_window: 200000
    cost_in: 0.80
    cost_out: 4.00
```

## Auto-Update
```bash
uv tool upgrade claude-monitor    # upgrade to latest
```
Note: auto-update on start is enabled by default. Disable with `--no-auto-update`.

## Data Source
```
~/.claude/projects/*/sessions/*.jsonl
```
Reads only. No writes, no uploads, fully local.
