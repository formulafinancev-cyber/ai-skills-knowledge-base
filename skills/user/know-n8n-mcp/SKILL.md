# n8n-MCP — AI Access to n8n Workflow Automation

## Trigger
Use when building, debugging, or explaining n8n workflows via Claude. Reference n8n node properties, operations, templates, or community integrations.

## What Is n8n-MCP
MCP server providing AI assistants with comprehensive n8n node documentation. 1,505 nodes (812 core + 693 community), 2,709 workflow templates, 2,646 real-world config examples.

**⚠️ NEVER edit production n8n workflows directly with AI. Always test in dev first.**

## Available MCP Tools (when server is running)

### Node Discovery
```
n8n_list_nodes              → list all available nodes with filtering
n8n_search_nodes            → semantic search: "send email", "http request"
n8n_get_node_info           → full node schema: inputs, outputs, properties
n8n_get_node_operations     → list all operations a node supports
n8n_get_node_examples       → real workflow configs using this node
```

### Workflow Templates
```
n8n_search_templates        → search 2,709 templates by description
n8n_get_template            → fetch specific template with full workflow JSON
n8n_list_templates          → browse by category, trigger type, use case
```

### Documentation
```
n8n_get_node_documentation  → official docs for node (87% coverage)
n8n_get_ai_nodes            → list 265 AI-capable tool variants
```

## Key n8n Concepts for AI Assistance

### Node Types
| Type | Examples | Purpose |
|------|---------|---------|
| Trigger | Webhook, Schedule, Gmail Trigger | Start workflow |
| Action | HTTP Request, Code, Set | Execute operations |
| Flow | IF, Switch, Merge, Split | Control flow |
| AI | AI Agent, LLM Chain, Vector Store | AI operations |
| Integration | Slack, Postgres, Google Sheets | External services |

### Expression Syntax
```javascript
{{ $json.fieldName }}              // current node output
{{ $node["NodeName"].json.field }} // specific node output
{{ $now.toISO() }}                 // current timestamp
{{ $workflow.id }}                 // workflow metadata
{{ $input.all() }}                 // all input items
{{ $input.first().json.id }}       // first item field
```

### Error Handling Pattern
```json
{
  "continueOnFail": true,
  "onError": "continueRegularOutput"
}
```

### Workflow JSON Structure
```json
{
  "nodes": [
    {
      "id": "uuid",
      "name": "Node Name",
      "type": "n8n-nodes-base.httpRequest",
      "parameters": { ... },
      "position": [x, y]
    }
  ],
  "connections": {
    "Node Name": {
      "main": [[{"node": "Next Node", "type": "main", "index": 0}]]
    }
  }
}
```

## Common Patterns

### HTTP → Transform → Store
```
Webhook → HTTP Request → Code (transform) → Postgres/Sheets
```

### AI Agent Workflow
```
Trigger → AI Agent (with tools: HTTP, Code, DB) → Response → Slack/Email
```

### Error Notification
```
Any Node [onError] → Slack/Email "Workflow failed: {{ $execution.error.message }}"
```

## Deploy MCP Server
```bash
npx n8n-mcp          # local, no config needed
# or Docker:
docker run -p 3000:3000 ghcr.io/czlonkowski/n8n-mcp
```
Configure in Claude Code `~/.claude/mcp.json`:
```json
{"n8n-mcp": {"command": "npx", "args": ["n8n-mcp"]}}
```

## Safety Rules
1. **Never** connect AI directly to production n8n instance
2. Always export workflow backup before AI edits
3. Test in dev n8n instance first
4. Use `Execute Workflow` node for AI-triggered workflows, not direct API
