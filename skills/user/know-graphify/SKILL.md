# graphify — Codebase Knowledge Graph

## Trigger
Use when needing to understand a large/unfamiliar codebase, find architectural patterns, trace dependencies, analyze relationships across files, or build a queryable knowledge map from mixed sources (code, PDFs, images, docs).

## What Is graphify
AI coding skill that builds a queryable knowledge graph from any folder. AST extraction for 25 languages + LLM semantic extraction + Leiden community detection + interactive HTML visualization. 71.5× fewer tokens per query vs reading raw files.

**Invoke:** Type `/graphify` in Claude Code, Codex, OpenCode, Cursor, Gemini CLI.

## Core Command
```bash
/graphify .                    # analyze current directory
/graphify ./src                # analyze specific folder
/graphify . --depth 3          # limit traversal depth
/graphify . --exclude vendor   # exclude folders (or use .graphifyignore)
```

## Output Files
```
graphify-out/
├── graph.html       ← interactive visualization (open in browser)
│                      click nodes, search, filter by community
├── GRAPH_REPORT.md  ← god nodes, surprising connections, questions
├── graph.json       ← persistent graph (re-query without re-running)
└── cache/           ← SHA256 cache (re-runs only process changed files)
```

## Supported Input Types
| Type | Extraction Method |
|------|-----------------|
| Code (25 languages) | Tree-sitter AST (deterministic) |
| SQL files | AST → tables, views, FK, JOIN relationships |
| YAML/Helm/K8s | Semantic extraction |
| Markdown/Docs | LLM semantic extraction |
| PDF | Text extraction + concept mapping |
| Images/Screenshots | Vision model extraction |
| Audio/Video | Whisper transcription + domain-aware prompt |

## Supported Languages (AST)
Python, JS, TS, Go, Rust, Java, C, C++, Ruby, C#, Kotlin, Scala, PHP, Swift, Lua, Zig, PowerShell, Elixir, Objective-C, Julia, Verilog, SystemVerilog, Vue, Svelte, Dart

## .graphifyignore
```
# .graphifyignore
node_modules/
dist/
vendor/
*.generated.py
.git/
```

## GRAPH_REPORT.md Contents
- **God nodes:** highly connected entities (architectural hotspots)
- **Community clusters:** related code grouped by Leiden algorithm
- **Surprising connections:** unexpected dependencies
- **Suggested questions:** what to investigate next
- **Orphan nodes:** isolated code (dead code candidates)

## Query Patterns (after graph is built)
```
/graphify "what handles authentication?"
/graphify "find all database write operations"
/graphify "show me the payment processing flow"
/graphify "which modules are most coupled?"
/graphify "what depends on the Config class?"
```

## Install
```bash
pip install graphifyy --break-system-packages
graphify install    # sets up Claude Code skill + hooks
```

## Use Case: FFA Codebase Analysis
```bash
/graphify .                         # map all 6000+ lines
# Identifies: CFG god node, onOpen entry points, BDR/iiko adapter clusters
# GRAPH_REPORT.md shows: Settings sheet has 12 dependents (high-risk change)
# Surprising connection: renderSales → _readSettings (unexpected coupling)
```

## Performance
- 71.5× fewer tokens per query vs reading raw files
- Incremental: only re-processes changed files (SHA256 cache)
- Persistent: `graph.json` survives session resets
