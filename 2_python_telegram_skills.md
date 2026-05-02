# SKILLS: Python, Telegram, SQL
# Содержит: gb-telegram, jf-python-pro, jf-sql-pro, jf-debugging-wizard, jf-pandas-pro

---
## SKILL: gb-telegram

---
name: telegram
description: This skill should be used when fetching, searching, downloading, sending, editing, or publishing messages on Telegram. Use for queries like "show my Telegram messages", "search Telegram for...", "get unread messages", "send a message to...", "edit that message", "publish this draft to klodkot", or "add Telegram messages to my notes".
---

# Telegram Message Skill

Fetch, search, download, send, and publish Telegram messages with flexible filtering and output options.

## Prerequisites

Authentication must be configured in `~/.telegram_dl/`. Run `setup` command to check status or get instructions:

```bash
python3 scripts/telegram_fetch.py setup
```

If not configured, follow these steps:
1. Get API credentials from https://my.telegram.org/auth
2. Clone telegram_dl: https://github.com/glebis/telegram_dl
3. Run `python telegram_dl.py` and follow interactive prompts
4. Verify with `python3 scripts/telegram_fetch.py setup`

## Quick Start

Run the script at `scripts/telegram_fetch.py` with appropriate commands:

```bash
# List available chats
python3 scripts/telegram_fetch.py list

# Get recent messages
python3 scripts/telegram_fetch.py recent --limit 20

# Search messages
python3 scripts/telegram_fetch.py search "meeting"

# Get unread messages
python3 scripts/telegram_fetch.py unread
```

## Commands

### List Chats

To see available Telegram chats:

```bash
python3 scripts/telegram_fetch.py list
python3 scripts/telegram_fetch.py list --limit 50
python3 scripts/telegram_fetch.py list --search "AI"
python3 scripts/telegram_fetch.py list --search "claude code глеб + саши" --exact
```

**Options:**
- `--search "text"`: Filter by substring match (case-insensitive)
- `--exact`: Require exact name match instead of substring (use with --search)
- `--limit N`: Max chats to retrieve (default: 30, increase if chat not found)

**Important:** If you're looking for a specific chat by exact name and it's not found, increase `--limit` to 100 or 200, as the chat may not be in the most recent 30.

Returns JSON with chat IDs, names, types, and unread counts.

### Fetch Recent Messages

To get recent messages:

```bash
# From all chats (last 50 messages across top 10 chats)
python3 scripts/telegram_fetch.py recent

# From specific chat
python3 scripts/telegram_fetch.py recent --chat "Tool Building Ape"
python3 scripts/telegram_fetch.py recent --chat-id 123456789

# With limits
python3 scripts/telegram_fetch.py recent --limit 100
python3 scripts/telegram_fetch.py recent --days 7
```

### Search Messages

To search message content:

```bash
# Global search across all chats
python3 scripts/telegram_fetch.py search "project deadline"

# Search in specific chat
python3 scripts/telegram_fetch.py search "meeting" --chat-id 123456789

# Limit results
python3 scripts/telegram_fetch.py search "important" --limit 20
```

### Fetch Unread Messages

To get only unread messages:

```bash
python3 scripts/telegram_fetch.py unread
python3 scripts/telegram_fetch.py unread --chat-id 123456789
```

### Send Messages

To send a message to a chat:

```bash
# Send to existing chat by name
python3 scripts/telegram_fetch.py send --chat "John Doe" --text "Hello!"

# Send to username (works even without prior conversation)
python3 scripts/telegram_fetch.py send --chat "@username" --text "Hello!"

# Reply to a specific message (use message ID from recent/search output)
python3 scripts/telegram_fetch.py send --chat "Tool Building Ape" --text "Thanks!" --reply-to 12345

# Send to a forum topic (for groups with topics enabled)
python3 scripts/telegram_fetch.py send --chat "Group Name" --text "Hello topic!" --topic 12

# Send with markdown formatting (converts **bold**, _italic_, [links](url) to Telegram HTML)
python3 scripts/telegram_fetch.py send --chat "@username" --text "**Bold** and _italic_ text" --markdown
```

**Formatting (`--markdown` flag):**
- Without `--markdown`: text is sent as-is (plain text, no formatting)
- With `--markdown`: converts markdown to Telegram HTML (`**bold**` -> bold, `_italic_` -> italic, `[text](url)` -> link, `## Header` -> bold, `* item` -> arrow list)
- **IMPORTANT**: Always use `--markdown` when sending draft content that contains markdown formatting
- The `publish` command handles markdown conversion automatically; the `send` command does NOT unless `--markdown` is specified

### Send Files

To send images, documents, or videos:

```bash
# Send an image
python3 scripts/telegram_fetch.py send --chat "John Doe" --file "/path/to/image.jpg"

# Send document with caption
python3 scripts/telegram_fetch.py send --chat "@username" --file "report.pdf" --text "Here's the report"

# Reply with media
python3 scripts/telegram_fetch.py send --chat "Group" --file "screenshot.png" --reply-to 12345
```

**Chat resolution order:**
1. `@username` - Resolves Telegram username directly
2. Numeric ID - Resolves chat by Telegram ID
3. Name match - Fuzzy search in existing dialogs

Returns JSON with send status, resolved chat name, message ID, and file info (for media).

### Edit Messages

To edit an existing message:

```bash
# Edit a message by ID
python3 scripts/telegram_fetch.py edit --chat "@mentalhealthtech" --message-id 76 --text "Updated text"

# Edit in a group/channel
python3 scripts/telegram_fetch.py edit --chat "Mental health tech" --message-id 123 --text "Corrected content"
```

**Note:** You can only edit your own messages. Telegram formatting (**bold**, etc.) is preserved.

Returns JSON with edit status and message ID.

### Download Attachments

To download media files from a chat:

```bash
# Download last 5 attachments from a chat (default)
python3 scripts/telegram_fetch.py download --chat "Tool Building Ape"

# Download last 10 attachments
python3 scripts/telegram_fetch.py download --chat "Project Group" --limit 10

# Download to custom directory
python3 scripts/telegram_fetch.py download --chat "@username" --output "/path/to/folder"

# Download from specific message
python3 scripts/telegram_fetch.py download --chat "John Doe" --message-id 12345
```

**Default output:** `~/Downloads/telegram_attachments/`

Returns JSON with download results (file names, paths, sizes).

### Fetch Forum Thread Messages

To get messages from a specific forum thread (topics in groups):

```bash
# Fetch from thread 174 in Claude Code Lab
python3 scripts/telegram_fetch.py thread --chat-id -1003237581133 --thread-id 174

# Fetch with custom limit
python3 scripts/telegram_fetch.py thread --chat-id -1003237581133 --thread-id 174 --limit 50

# Save to file
python3 scripts/telegram_fetch.py thread --chat-id -1003237581133 --thread-id 174 -o ~/thread.md

# Append to daily note
python3 scripts/telegram_fetch.py thread --chat-id -1003237581133 --thread-id 174 --to-daily

# JSON output
python3 scripts/telegram_fetch.py thread --chat-id -1003237581133 --thread-id 174 --json
```

**Messages are sorted newest first** (reverse chronological order).

**How to find thread ID:**
- Forum topic IDs appear in the thread URL: `https://t.me/c/CHAT_ID/THREAD_ID`
- Use `recent` command on the chat to see message IDs in threads

Returns markdown or JSON with all messages from the specified thread.

### Publish Draft to Channel

To publish a draft from the klodkot channel to Telegram:

```bash
# Dry run (preview without sending)
python3 scripts/telegram_fetch.py publish --draft "Channels/klodkot/drafts/20260122-anthropic-consciousness-question.md" --dry-run

# Publish to channel
python3 scripts/telegram_fetch.py publish --draft "Channels/klodkot/drafts/20260122-anthropic-consciousness-question.md"
```

**Workflow:**
1. Parses draft frontmatter and body
2. Validates channel field (must be "klodkot")
3. Extracts media references from frontmatter `video:` field and wikilinks
4. Resolves media paths in `Channels/klodkot/attachments/` or `Sources/`
5. Strips draft headers (e.g., "# Title - Telegram Draft")
6. Appends footer if not present: "**[КЛОДКОТ](https://t.me/klodkot)** — Claude Code и другие агенты: инструменты, кейсы, вдохновение"
7. Sends to @klodkot channel (multiple media as album)
8. Updates frontmatter with `published_date`, `telegram_message_id`
9. Moves file from `drafts/` to `published/`
10. Updates channel index with new entry at top

**Media handling:**
- Frontmatter: `video: filename.mp4`
- Wikilinks: `[[filename.mp4]]`, `[[image.png|alt text]]`
- Multiple media sent as Telegram album

**Safety:**
- `--dry-run` shows preview without sending
- Validates before sending
- Rollback on send failure (file not moved)
- Warnings on post-publish errors (file sent but move/index update failed)

**Returns:** JSON with publish status, message ID, warnings (if any)

## Output Options

### Default (Markdown to stdout)

By default, outputs formatted markdown suitable for Claude to read and summarize.

### JSON Format

Add `--json` flag for structured data:

```bash
python3 scripts/telegram_fetch.py recent --json
```

### Append to Obsidian Daily Note

Add messages to today's daily note in the vault:

```bash
python3 scripts/telegram_fetch.py recent --to-daily
python3 scripts/telegram_fetch.py search "project" --to-daily
```

Appends to `~/Brains/brain/Daily/YYYYMMDD.md`

### Append to Person's Note

Add messages to a specific person's note:

```bash
python3 scripts/telegram_fetch.py recent --chat "John Doe" --to-person "John Doe"
```

Creates or appends to `~/Brains/brain/{PersonName}.md`

### Save to File (Token-Efficient)

Save messages directly to file without consuming context tokens:

```bash
# Save 100 messages to markdown file
python3 scripts/telegram_fetch.py recent --chat "AGENCY: Community" --limit 100 -o ~/chat_archive.md

# Save with media files downloaded to same folder
python3 scripts/telegram_fetch.py recent --chat "Project Group" --limit 50 -o ~/project/archive.md --with-media

# Save search results to file
python3 scripts/telegram_fetch.py search "meeting" -o ~/meetings.md
```

Returns JSON with save status (file path, message count, media download results) - minimal token usage.

## Example User Requests

When user asks:

- "Show my recent Telegram messages" -> `recent --limit 20`
- "What Telegram messages did I get today?" -> `recent --days 1`
- "Search Telegram for messages about the project" -> `search "project"`
- "Get unread messages from Tool Building Ape" -> `unread` + filter output
- "Add my Telegram messages to daily note" -> `recent --to-daily`
- "What chats do I have on Telegram?" -> `list`
- "Find the exact chat named X" -> `list --search "X" --exact --limit 200`
- "Send hello to John on Telegram" -> `send --chat "John" --text "Hello!"`
- "Message @username on Telegram" -> `send --chat "@username" --text "..."`
- "Reply to that message with thanks" -> `send --chat "..." --text "Thanks!" --reply-to <id>`
- "Send this image to John" -> `send --chat "John" --file "/path/to/image.jpg"`
- "Send report.pdf with caption" -> `send --chat "..." --file "report.pdf" --text "Here's the report"`
- "Send to topic 12 in Group" -> `send --chat "Group" --text "..." --topic 12`
- "Download attachments from Tool Building Ape" -> `download --chat "Tool Building Ape"`
- "Download last 10 files from Project Group" -> `download --chat "Project Group" --limit 10`
- "Save last 100 messages from AGENCY to file" -> `recent --chat "AGENCY: Community" --limit 100 -o ~/agency.md`
- "Archive chat with media" -> `recent --chat "Group" -o ~/archive.md --with-media`
- "Edit that message" -> `edit --chat "..." --message-id <id> --text "new text"`
- "Fix the typo in message 123" -> `edit --chat "..." --message-id 123 --text "corrected text"`
- "Is Telegram configured?" -> `setup`
- "How do I set up Telegram?" -> `setup` (returns instructions if not configured)
- "Publish this draft to klodkot" -> `publish --draft "Channels/klodkot/drafts/...md"`
- "Preview this draft before publishing" -> `publish --draft "..." --dry-run`

## Rate Limiting

The script includes built-in rate limiting (0.1s between messages) and handles Telegram's FloodWaitError automatically with backoff.

## Dependencies

Requires Python packages:
- `telethon` - Telegram API client
- `pyyaml` - YAML parsing for draft frontmatter

Install with: `pip install telethon pyyaml`

---
## SKILL: jf-python-pro

---
name: python-pro
description: Use when building Python 3.11+ applications requiring type safety, async programming, or robust error handling. Generates type-annotated Python code, configures mypy in strict mode, writes pytest test suites with fixtures and mocking, and validates code with black and ruff. Invoke for type hints, async/await patterns, dataclasses, dependency injection, logging configuration, and structured error handling.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: language
  triggers: Python development, type hints, async Python, pytest, mypy, dataclasses, Python best practices, Pythonic code
  role: specialist
  scope: implementation
  output-format: code
  related-skills: fastapi-expert, devops-engineer
---

# Python Pro

Modern Python 3.11+ specialist focused on type-safe, async-first, production-ready code.

## When to Use This Skill

- Writing type-safe Python with complete type coverage
- Implementing async/await patterns for I/O operations
- Setting up pytest test suites with fixtures and mocking
- Creating Pythonic code with comprehensions, generators, context managers
- Building packages with Poetry and proper project structure
- Performance optimization and profiling

## Core Workflow

1. **Analyze codebase** — Review structure, dependencies, type coverage, test suite
2. **Design interfaces** — Define protocols, dataclasses, type aliases
3. **Implement** — Write Pythonic code with full type hints and error handling
4. **Test** — Create comprehensive pytest suite with >90% coverage
5. **Validate** — Run `mypy --strict`, `black`, `ruff`
   - If mypy fails: fix type errors reported and re-run before proceeding
   - If tests fail: debug assertions, update fixtures, and iterate until green
   - If ruff/black reports issues: apply auto-fixes, then re-validate

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Type System | `references/type-system.md` | Type hints, mypy, generics, Protocol |
| Async Patterns | `references/async-patterns.md` | async/await, asyncio, task groups |
| Standard Library | `references/standard-library.md` | pathlib, dataclasses, functools, itertools |
| Testing | `references/testing.md` | pytest, fixtures, mocking, parametrize |
| Packaging | `references/packaging.md` | poetry, pip, pyproject.toml, distribution |

## Constraints

### MUST DO
- Type hints for all function signatures and class attributes
- PEP 8 compliance with black formatting
- Comprehensive docstrings (Google style)
- Test coverage exceeding 90% with pytest
- Use `X | None` instead of `Optional[X]` (Python 3.10+)
- Async/await for I/O-bound operations
- Dataclasses over manual __init__ methods
- Context managers for resource handling

### MUST NOT DO
- Skip type annotations on public APIs
- Use mutable default arguments
- Mix sync and async code improperly
- Ignore mypy errors in strict mode
- Use bare except clauses
- Hardcode secrets or configuration
- Use deprecated stdlib modules (use pathlib not os.path)

## Code Examples

### Type-annotated function with error handling
```python
from pathlib import Path

def read_config(path: Path) -> dict[str, str]:
    """Read configuration from a file.

    Args:
        path: Path to the configuration file.

    Returns:
        Parsed key-value configuration entries.

    Raises:
        FileNotFoundError: If the config file does not exist.
        ValueError: If a line cannot be parsed.
    """
    config: dict[str, str] = {}
    with path.open() as f:
        for line in f:
            key, _, value = line.partition("=")
            if not key.strip():
                raise ValueError(f"Invalid config line: {line!r}")
            config[key.strip()] = value.strip()
    return config
```

### Dataclass with validation
```python
from dataclasses import dataclass, field

@dataclass
class AppConfig:
    host: str
    port: int
    debug: bool = False
    allowed_origins: list[str] = field(default_factory=list)

    def __post_init__(self) -> None:
        if not (1 <= self.port <= 65535):
            raise ValueError(f"Invalid port: {self.port}")
```

### Async pattern
```python
import asyncio
import httpx

async def fetch_all(urls: list[str]) -> list[bytes]:
    """Fetch multiple URLs concurrently."""
    async with httpx.AsyncClient() as client:
        tasks = [client.get(url) for url in urls]
        responses = await asyncio.gather(*tasks)
        return [r.content for r in responses]
```

### pytest fixture and parametrize
```python
import pytest
from pathlib import Path

@pytest.fixture
def config_file(tmp_path: Path) -> Path:
    cfg = tmp_path / "config.txt"
    cfg.write_text("host=localhost\nport=8080\n")
    return cfg

@pytest.mark.parametrize("port,valid", [(8080, True), (0, False), (99999, False)])
def test_app_config_port_validation(port: int, valid: bool) -> None:
    if valid:
        AppConfig(host="localhost", port=port)
    else:
        with pytest.raises(ValueError):
            AppConfig(host="localhost", port=port)
```

### mypy strict configuration (pyproject.toml)
```toml
[tool.mypy]
python_version = "3.11"
strict = true
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true
```

Clean `mypy --strict` output looks like:
```
Success: no issues found in 12 source files
```
Any reported error (e.g., `error: Function is missing a return type annotation`) must be resolved before the implementation is considered complete.

## Output Templates

When implementing Python features, provide:
1. Module file with complete type hints
2. Test file with pytest fixtures
3. Type checking confirmation (mypy --strict passes)
4. Brief explanation of Pythonic patterns used

## Knowledge Reference

Python 3.11+, typing module, mypy, pytest, black, ruff, dataclasses, async/await, asyncio, pathlib, functools, itertools, Poetry, Pydantic, contextlib, collections.abc, Protocol

[Documentation](https://jeffallan.github.io/claude-skills/skills/language/python-pro/)

---
## SKILL: jf-sql-pro

---
name: sql-pro
description: Optimizes SQL queries, designs database schemas, and troubleshoots performance issues. Use when a user asks why their query is slow, needs help writing complex joins or aggregations, mentions database performance issues, or wants to design or migrate a schema. Invoke for complex queries, window functions, CTEs, indexing strategies, query plan analysis, covering index creation, recursive queries, EXPLAIN/ANALYZE interpretation, before/after query benchmarking, or migrating queries between database dialects (PostgreSQL, MySQL, SQL Server, Oracle).
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: language
  triggers: SQL optimization, query performance, database design, PostgreSQL, MySQL, SQL Server, window functions, CTEs, query tuning, EXPLAIN plan, database indexing
  role: specialist
  scope: implementation
  output-format: code
  related-skills: devops-engineer
---

# SQL Pro

## Core Workflow

1. **Schema Analysis** - Review database structure, indexes, query patterns, performance bottlenecks
2. **Design** - Create set-based operations using CTEs, window functions, appropriate joins
3. **Optimize** - Analyze execution plans, implement covering indexes, eliminate table scans
4. **Verify** - Run `EXPLAIN ANALYZE` and confirm no sequential scans on large tables; if query does not meet sub-100ms target, iterate on index selection or query rewrite before proceeding
5. **Document** - Provide query explanations, index rationale, performance metrics

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Query Patterns | `references/query-patterns.md` | JOINs, CTEs, subqueries, recursive queries |
| Window Functions | `references/window-functions.md` | ROW_NUMBER, RANK, LAG/LEAD, analytics |
| Optimization | `references/optimization.md` | EXPLAIN plans, indexes, statistics, tuning |
| Database Design | `references/database-design.md` | Normalization, keys, constraints, schemas |
| Dialect Differences | `references/dialect-differences.md` | PostgreSQL vs MySQL vs SQL Server specifics |

## Quick-Reference Examples

### CTE Pattern
```sql
-- Isolate expensive subquery logic for reuse and readability
WITH ranked_orders AS (
    SELECT
        customer_id,
        order_id,
        total_amount,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) AS rn
    FROM orders
    WHERE status = 'completed'          -- filter early, before the join
)
SELECT customer_id, order_id, total_amount
FROM ranked_orders
WHERE rn = 1;                           -- latest completed order per customer
```

### Window Function Pattern
```sql
-- Running total and rank within partition — no self-join required
SELECT
    department_id,
    employee_id,
    salary,
    SUM(salary)  OVER (PARTITION BY department_id ORDER BY hire_date) AS running_payroll,
    RANK()       OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank
FROM employees;
```

### EXPLAIN ANALYZE Interpretation
```sql
-- PostgreSQL: always use ANALYZE to see actual row counts vs. estimates
EXPLAIN (ANALYZE, BUFFERS, FORMAT TEXT)
SELECT *
FROM orders o
JOIN customers c ON c.id = o.customer_id
WHERE o.created_at > NOW() - INTERVAL '30 days';
```
Key things to check in the output:
- **Seq Scan on large table** → add or fix an index
- **actual rows ≫ estimated rows** → run `ANALYZE <table>` to refresh statistics
- **Buffers: shared hit** vs **read** → high `read` count signals missing cache / index

### Before / After Optimization Example
```sql
-- BEFORE: correlated subquery, one execution per row (slow)
SELECT order_id,
       (SELECT SUM(quantity) FROM order_items oi WHERE oi.order_id = o.id) AS item_count
FROM orders o;

-- AFTER: single aggregation join (fast)
SELECT o.order_id, COALESCE(agg.item_count, 0) AS item_count
FROM orders o
LEFT JOIN (
    SELECT order_id, SUM(quantity) AS item_count
    FROM order_items
    GROUP BY order_id
) agg ON agg.order_id = o.id;

-- Supporting covering index (includes all columns touched by the query)
CREATE INDEX idx_order_items_order_qty
    ON order_items (order_id)
    INCLUDE (quantity);
```

## Constraints

### MUST DO
- Analyze execution plans before recommending optimizations
- Use set-based operations over row-by-row processing
- Apply filtering early in query execution (before joins where possible)
- Use EXISTS over COUNT for existence checks
- Handle NULLs explicitly in comparisons and aggregations
- Create covering indexes for frequent queries
- Test with production-scale data volumes

### MUST NOT DO
- Use SELECT * in production queries
- Use cursors when set-based operations work
- Ignore platform-specific optimizations when targeting a specific dialect
- Implement solutions without considering data volume and cardinality

## Output Templates

When implementing SQL solutions, provide:
1. Optimized query with inline comments
2. Required indexes with rationale
3. Execution plan analysis
4. Performance metrics (before/after)
5. Platform-specific notes if applicable

[Documentation](https://jeffallan.github.io/claude-skills/skills/language/sql-pro/)

---
## SKILL: jf-debugging-wizard

---
name: debugging-wizard
description: Parses error messages, traces execution flow through stack traces, correlates log entries to identify failure points, and applies systematic hypothesis-driven methodology to isolate and resolve bugs. Use when investigating errors, analyzing stack traces, finding root causes of unexpected behavior, troubleshooting crashes, or performing log analysis, error investigation, or root cause analysis.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: quality
  triggers: debug, error, bug, exception, traceback, stack trace, troubleshoot, not working, crash, fix issue
  role: specialist
  scope: analysis
  output-format: analysis
  related-skills: test-master, fullstack-guardian, monitoring-expert
---

# Debugging Wizard

Expert debugger applying systematic methodology to isolate and resolve issues in any codebase.

## Core Workflow

1. **Reproduce** - Establish consistent reproduction steps
2. **Isolate** - Narrow down to smallest failing case
3. **Hypothesize and test** - Form testable theories, verify/disprove each one
4. **Fix** - Implement and verify solution
5. **Prevent** - Add tests/safeguards against regression

## Reference Guide

Load detailed guidance based on context:

<!-- Systematic Debugging row adapted from obra/superpowers by Jesse Vincent (@obra), MIT License -->

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Debugging Tools | `references/debugging-tools.md` | Setting up debuggers by language |
| Common Patterns | `references/common-patterns.md` | Recognizing bug patterns |
| Strategies | `references/strategies.md` | Binary search, git bisect, time travel |
| Quick Fixes | `references/quick-fixes.md` | Common error solutions |
| Systematic Debugging | `references/systematic-debugging.md` | Complex bugs, multiple failed fixes, root cause analysis |

## Constraints

### MUST DO
- Reproduce the issue first
- Gather complete error messages and stack traces
- Test one hypothesis at a time
- Document findings for future reference
- Add regression tests after fixing
- Remove all debug code before committing

### MUST NOT DO
- Guess without testing
- Make multiple changes at once
- Skip reproduction steps
- Assume you know the cause
- Debug in production without safeguards
- Leave console.log/debugger statements in code

## Common Debugging Commands

**Python (pdb)**
```bash
python -m pdb script.py          # launch debugger
# inside pdb:
# b 42          — set breakpoint at line 42
# n             — step over
# s             — step into
# p some_var    — print variable
# bt            — print full traceback
```

**JavaScript (Node.js)**
```bash
node --inspect-brk script.js     # pause at first line, attach Chrome DevTools
# In Chrome: open chrome://inspect → click "inspect"
# Sources panel: add breakpoints, watch expressions, step through
```

**Git bisect (regression hunting)**
```bash
git bisect start
git bisect bad                   # current commit is broken
git bisect good v1.2.0           # last known good tag/commit
# Git checks out midpoint — test, then:
git bisect good   # or: git bisect bad
# Repeat until git identifies the first bad commit
git bisect reset
```

**Go (delve)**
```bash
dlv debug ./cmd/server           # build & attach
# (dlv) break main.go:55
# (dlv) continue
# (dlv) print myVar
```

## Output Templates

When debugging, provide:
1. **Root Cause**: What specifically caused the issue
2. **Evidence**: Stack trace, logs, or test that proves it
3. **Fix**: Code change that resolves it
4. **Prevention**: Test or safeguard to prevent recurrence

[Documentation](https://jeffallan.github.io/claude-skills/skills/quality/debugging-wizard/)

---
## SKILL: jf-pandas-pro

---
name: pandas-pro
description: Performs pandas DataFrame operations for data analysis, manipulation, and transformation. Use when working with pandas DataFrames, data cleaning, aggregation, merging, or time series analysis. Invoke for data manipulation tasks such as joining DataFrames on multiple keys, pivoting tables, resampling time series, handling NaN values with interpolation or forward-fill, groupby aggregations, type conversion, or performance optimization of large datasets.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: data-ml
  triggers: pandas, DataFrame, data manipulation, data cleaning, aggregation, groupby, merge, join, time series, data wrangling, pivot table, data transformation
  role: expert
  scope: implementation
  output-format: code
  related-skills: python-pro
---

# Pandas Pro

Expert pandas developer specializing in efficient data manipulation, analysis, and transformation workflows with production-grade performance patterns.

## Core Workflow

1. **Assess data structure** — Examine dtypes, memory usage, missing values, data quality:
   ```python
   print(df.dtypes)
   print(df.memory_usage(deep=True).sum() / 1e6, "MB")
   print(df.isna().sum())
   print(df.describe(include="all"))
   ```
2. **Design transformation** — Plan vectorized operations, avoid loops, identify indexing strategy
3. **Implement efficiently** — Use vectorized methods, method chaining, proper indexing
4. **Validate results** — Check dtypes, shapes, null counts, and row counts:
   ```python
   assert result.shape[0] == expected_rows, f"Row count mismatch: {result.shape[0]}"
   assert result.isna().sum().sum() == 0, "Unexpected nulls after transform"
   assert set(result.columns) == expected_cols
   ```
5. **Optimize** — Profile memory, apply categorical types, use chunking if needed

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| DataFrame Operations | `references/dataframe-operations.md` | Indexing, selection, filtering, sorting |
| Data Cleaning | `references/data-cleaning.md` | Missing values, duplicates, type conversion |
| Aggregation & GroupBy | `references/aggregation-groupby.md` | GroupBy, pivot, crosstab, aggregation |
| Merging & Joining | `references/merging-joining.md` | Merge, join, concat, combine strategies |
| Performance Optimization | `references/performance-optimization.md` | Memory usage, vectorization, chunking |

## Code Patterns

### Vectorized Operations (before/after)

```python
# ❌ AVOID: row-by-row iteration
for i, row in df.iterrows():
    df.at[i, 'tax'] = row['price'] * 0.2

# ✅ USE: vectorized assignment
df['tax'] = df['price'] * 0.2
```

### Safe Subsetting with `.copy()`

```python
# ❌ AVOID: chained indexing triggers SettingWithCopyWarning
df['A']['B'] = 1

# ✅ USE: .loc[] with explicit copy when mutating a subset
subset = df.loc[df['status'] == 'active', :].copy()
subset['score'] = subset['score'].fillna(0)
```

### GroupBy Aggregation

```python
summary = (
    df.groupby(['region', 'category'], observed=True)
    .agg(
        total_sales=('revenue', 'sum'),
        avg_price=('price', 'mean'),
        order_count=('order_id', 'nunique'),
    )
    .reset_index()
)
```

### Merge with Validation

```python
merged = pd.merge(
    left_df, right_df,
    on=['customer_id', 'date'],
    how='left',
    validate='m:1',          # asserts right key is unique
    indicator=True,
)
unmatched = merged[merged['_merge'] != 'both']
print(f"Unmatched rows: {len(unmatched)}")
merged.drop(columns=['_merge'], inplace=True)
```

### Missing Value Handling

```python
# Forward-fill then interpolate numeric gaps
df['price'] = df['price'].ffill().interpolate(method='linear')

# Fill categoricals with mode, numerics with median
for col in df.select_dtypes(include='object'):
    df[col] = df[col].fillna(df[col].mode()[0])
for col in df.select_dtypes(include='number'):
    df[col] = df[col].fillna(df[col].median())
```

### Time Series Resampling

```python
daily = (
    df.set_index('timestamp')
    .resample('D')
    .agg({'revenue': 'sum', 'sessions': 'count'})
    .fillna(0)
)
```

### Pivot Table

```python
pivot = df.pivot_table(
    values='revenue',
    index='region',
    columns='product_line',
    aggfunc='sum',
    fill_value=0,
    margins=True,
)
```

### Memory Optimization

```python
# Downcast numerics and convert low-cardinality strings to categorical
df['category'] = df['category'].astype('category')
df['count'] = pd.to_numeric(df['count'], downcast='integer')
df['score'] = pd.to_numeric(df['score'], downcast='float')
print(df.memory_usage(deep=True).sum() / 1e6, "MB after optimization")
```

## Constraints

### MUST DO
- Use vectorized operations instead of loops
- Set appropriate dtypes (categorical for low-cardinality strings)
- Check memory usage with `.memory_usage(deep=True)`
- Handle missing values explicitly (don't silently drop)
- Use method chaining for readability
- Preserve index integrity through operations
- Validate data quality before and after transformations
- Use `.copy()` when modifying subsets to avoid SettingWithCopyWarning

### MUST NOT DO
- Iterate over DataFrame rows with `.iterrows()` unless absolutely necessary
- Use chained indexing (`df['A']['B']`) — use `.loc[]` or `.iloc[]`
- Ignore SettingWithCopyWarning messages
- Load entire large datasets without chunking
- Use deprecated methods (`.ix`, `.append()` — use `pd.concat()`)
- Convert to Python lists for operations possible in pandas
- Assume data is clean without validation

## Output Templates

When implementing pandas solutions, provide:
1. Code with vectorized operations and proper indexing
2. Comments explaining complex transformations
3. Memory/performance considerations if dataset is large
4. Data validation checks (dtypes, nulls, shapes)

[Documentation](https://jeffallan.github.io/claude-skills/skills/data-ml/pandas-pro/)

