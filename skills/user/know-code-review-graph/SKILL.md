# code-review-graph — Token-Efficient Code Context via MCP

## Trigger
Use when reviewing PRs, debugging, or asking Claude about specific code — especially in large codebases where loading entire directories wastes tokens.

## What Is It
MCP server building a structural code map using Tree-sitter AST. Tracks changes incrementally. Provides AI with precise context — reads only what matters. Average 8.2× token reduction across 6 real repos.

## Installation
```bash
pip install code-review-graph
code-review-graph install    # auto-detects + configures all your AI tools
code-review-graph build      # parse your codebase
```
`install` detects: Codex, Claude Code, Cursor, Windsurf, Zed, Continue, OpenCode, Antigravity, Qwen, Qoder, Kiro — configures all automatically.

## MCP Tools Provided
```
get_file_structure(path)           → directory tree with symbol counts
get_symbols(file)                  → functions, classes, imports in file
get_symbol_details(file, symbol)   → full symbol with body + context
find_references(symbol)            → all files using this symbol
get_changed_files(base_branch)     → diff from base (for PR review)
get_dependency_graph(file)         → what this file imports/exports
search_symbols(query)              → fuzzy search across all symbols
get_call_graph(function)           → what calls this, what it calls
```

## PR Review Pattern
```
# Instead of: "read all changed files" → 40K tokens
# Use:
get_changed_files("main")          → list of changed files
get_symbols(changed_file)          → symbols changed
get_symbol_details(file, fn_name)  → just the relevant function
find_references(changed_fn)        → what breaks if signature changes
```

## Incremental Updates
```bash
code-review-graph update           # process only changed files (fast)
code-review-graph build --full     # full rebuild (on major refactors)
```
Git hooks auto-update on commit.

## Token Reduction Examples
| Scenario | Without | With | Savings |
|----------|---------|------|---------|
| "Fix bug in auth" | 8.2K tokens | 1.1K tokens | 87% |
| "Review PR" | 24K tokens | 3.8K tokens | 84% |
| "Refactor interface" | 45K tokens | 6.2K tokens | 86% |

## Data Storage
All local — SQLite database in `.code-review-graph/` in project root. No external services, no API keys.

## Supported Languages
Python, JavaScript, TypeScript, Go, Rust, Java, C, C++, Ruby, C#, PHP, Swift, Kotlin

## MCP Config (manual, Claude Code)
```json
{
  "code-review-graph": {
    "command": "code-review-graph",
    "args": ["mcp", "--project", "/path/to/project"]
  }
}
```
