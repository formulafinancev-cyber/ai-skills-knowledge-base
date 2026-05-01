# Understand Anything — Codebase Interactive Knowledge Base

## Trigger
Use when onboarding to a new codebase, building internal docs from code, or creating a queryable knowledge base from an existing project.

## What Is It
TypeScript monorepo that transforms any codebase into an interactive knowledge base. Tree-sitter analysis + React dashboard + multi-agent pipeline. Stores knowledge in `.understand-anything/` within the project.

## How It Works
```
1. Parse phase:    tree-sitter → AST extraction → symbol map
2. Analyze phase:  multi-agent → understand relationships, patterns, intent
3. Index phase:    store in local JSON/SQLite
4. Query phase:    React dashboard or Claude integration → ask questions
```

## Key Features
- **Symbol map**: every function, class, interface, type with docstrings extracted
- **Dependency graph**: what imports what, call chains
- **Pattern detection**: identifies architectural patterns (repository, factory, singleton, etc.)
- **Intent inference**: "this function validates JWT tokens" from code analysis
- **Interactive dashboard**: filterable, searchable React UI on localhost

## Setup
```bash
git clone https://github.com/Lum1104/Understand-Anything ~/.claude/skills/understand-anything
cd ~/.claude/skills/understand-anything
pnpm install
pnpm build
```

## Usage
```bash
# In any project directory:
npx understand-anything analyze .
npx understand-anything analyze ./src --output ./docs/knowledge

# Launch dashboard:
npx understand-anything dashboard --port 4000
# Opens http://localhost:4000

# Query from CLI:
npx understand-anything query "how does authentication work"
npx understand-anything query "what are all the database write operations"
npx understand-anything query "show me the error handling patterns"
```

## Dashboard Features
- Search across all symbols + intent descriptions
- Filter by: file, module, pattern type, complexity
- Dependency graph visualization (D3.js)
- Pattern report: identified architectural patterns
- "Unknown" panel: code without clear intent (refactoring candidates)

## Output Structure
```
.understand-anything/
  symbols.json         ← all symbols with metadata
  dependencies.json    ← import/call graph
  patterns.json        ← identified patterns
  intents.json         ← LLM-inferred intent for each symbol
  knowledge.db         ← SQLite for fast queries
```

## Integration with Claude Code
Place `UNDERSTAND_ANYTHING.md` in project root:
```markdown
## Codebase Knowledge
This project has been analyzed. Key findings:
- Auth: JWT-based, see auth/middleware.ts
- DB: Repository pattern, 12 repositories in db/repositories/
- Patterns: Factory for service creation, Observer for events
```
Claude reads this at session start for instant context.

## Requirements
- Node.js 18+, pnpm
- External npm deps installed locally (no network in operation)
