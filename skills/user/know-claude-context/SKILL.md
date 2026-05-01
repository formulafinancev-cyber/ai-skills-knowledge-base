# claude-context (Zilliz) — Semantic Codebase Search via MCP

## Trigger
Use when working with large codebases where full directory loading is expensive, or when Claude needs to find relevant code across millions of lines without reading everything.

## What Is It
MCP plugin adding semantic code search to Claude Code. Indexes codebase into Zilliz Cloud vector DB using OpenAI embeddings. 8.2× average token reduction across large repos. Instead of loading entire directories, retrieves only semantically relevant code.

## How It Works
```
1. Index phase:    code-review-graph build → AST parse → chunk → embed → Zilliz
2. Query phase:    Claude asks question → semantic search → top-K chunks returned
3. Context phase:  only relevant chunks injected into Claude context window
```

## MCP Tools (when configured)
```
search_code(query, limit)       → semantic search across codebase
get_file_content(path)          → fetch specific file
list_files(pattern)             → filtered file listing
get_symbols(file)               → functions/classes in file
find_references(symbol)         → where symbol is used
```

## Usage Pattern
```
Instead of: "read all files in src/" → 50K tokens
With claude-context: "find auth logic" → 2K tokens of relevant code
```

## When to Use
- Codebase > 50K lines: semantic search pays off
- "Find all places where X is called"
- "Show me how Y is implemented"
- "What handles error Z in this codebase"
- Refactoring across many files

## Setup Requirements
- Zilliz Cloud account (free tier available): cloud.zilliz.com
- OpenAI API key (for embedding model)
- Node.js 20+

## Install
```bash
npm install -g @zilliz/claude-context-mcp
```
Configure `~/.claude/mcp.json`:
```json
{
  "claude-context": {
    "command": "claude-context-mcp",
    "env": {
      "MILVUS_URI": "https://your-cluster.zilliz.com",
      "MILVUS_TOKEN": "your-token",
      "OPENAI_API_KEY": "sk-..."
    }
  }
}
```

## Index Your Codebase
```bash
npx @zilliz/claude-context-core index ./src
npx @zilliz/claude-context-core index . --exclude "node_modules,dist"
```

## Cost Profile
- Indexing: ~$0.002 per 1K tokens (OpenAI embeddings, one-time)
- Queries: ~$0.0001 per search (tiny)
- Storage: free tier covers ~10M tokens on Zilliz

## Limitations
- Sends code to OpenAI (embeddings) and Zilliz Cloud — not air-gapped
- Requires re-indexing after significant codebase changes
- Best for semantic search, not exact string matching (use grep for that)
