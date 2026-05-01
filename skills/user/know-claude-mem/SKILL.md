# claude-mem — Persistent Memory Compression for Claude Code

## Trigger
Use when Claude Code needs to remember context across sessions, compress long conversation history, or maintain project knowledge that survives session resets.

## What Is claude-mem
Persistent memory system for Claude Code. Auto-captures sessions, compresses with AI (Haiku), stores in local SQLite + Chroma vector DB, injects relevant context into future sessions. Solves the fundamental problem: Claude forgets everything when you close the terminal.

## How It Works
```
Session runs
  └─► PostToolUse hook captures tool calls + results
        └─► Session ends → Haiku compresses to key facts
              └─► Stored: SQLite (structured) + Chroma (vector)
                    └─► Next session starts → relevant memories injected
                          └─► Claude has context from past work
```

## Memory Types
| Type | What's Stored | Retrieval |
|------|--------------|-----------|
| Episodic | "Fixed auth bug on 2025-04-15, was race condition in token refresh" | Temporal |
| Semantic | "This codebase uses repository pattern, not active record" | Semantic search |
| Procedural | "To deploy: run ./deploy.sh --env prod --tag {version}" | Keyword |
| Project | Architecture decisions, recurring patterns, gotchas | Always injected |

## Key Commands
```bash
claude-mem status              # show memory stats + recent entries
claude-mem search "auth"       # semantic search across memories
claude-mem add "note text"     # manually add a memory
claude-mem forget "topic"      # remove memories about topic
claude-mem export              # export all memories to markdown
claude-mem import file.md      # import memories from markdown
claude-mem compress            # force compression of recent session
claude-mem clear               # ⚠️ delete all memories
```

## Memory Injection
At session start, claude-mem injects into CLAUDE.md:
```markdown
## Remembered Context (claude-mem)
- Last worked on: auth refactor (completed 2025-04-15)
- Known pattern: Settings sheet has 12 dependents — change carefully
- Architecture decision: BDR adapter reads row[2] not row[1] (ADR-003)
- Recurring bug: nested function declarations break GAS Rhino — use var
```

## Configuration (~/.claude-mem/config.json)
```json
{
  "compression_model": "claude-haiku-3-5",
  "max_memories": 500,
  "injection_limit": 2000,
  "auto_compress": true,
  "compression_threshold": 10
}
```

## OpenClaw Mode
Streams session context to Slack/Discord/Telegram via webhooks (optional, disabled by default). Enable only if you want team memory sharing.

## Install
```bash
/plugin install claude-mem
# or:
curl -sSL https://cmem.ai/install | bash   # ⚠️ curl-pipe-bash, review first
```

## Storage Location
```
~/.claude-mem/
  memories.db          ← SQLite: structured memories
  chroma/              ← Chroma: vector embeddings
  sessions/            ← raw session captures before compression
  exports/             ← markdown exports
```

## Privacy Note
All processing local (Haiku API call for compression only). No data sent to claude-mem servers. Compression uses your own Anthropic API key.
