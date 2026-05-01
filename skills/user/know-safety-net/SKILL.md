# safety-net — Destructive Command Guard for Claude Code

## Trigger
Use when setting up Claude Code safety hooks, or when Claude Code needs to know which commands are blocked and why.

## What Is It
Rust-based PreToolUse hook that blocks destructive git and filesystem commands before execution. AST-based command parsing. Single runtime dependency. Purely defensive — no telemetry, no network.

## Blocked Command Categories

### Git (catastrophic)
```bash
git push --force              # BLOCKED (use --force-with-lease)
git push -f                   # BLOCKED
git reset --hard HEAD~N       # BLOCKED (unless explicit)
git clean -fd                 # BLOCKED
git rebase -i HEAD~N          # WARNING (requires confirmation)
```

### Filesystem
```bash
rm -rf /                      # BLOCKED
rm -rf ~                      # BLOCKED
rm -rf ./important_dir        # WARNING → confirmation required
find . -delete                # BLOCKED
chmod -R 777                  # WARNING
```

### Database
```bash
DROP TABLE                    # BLOCKED in production contexts
TRUNCATE TABLE                # WARNING → confirmation
DELETE FROM table             # WARNING without WHERE clause
```

### Cloud / Infrastructure
```bash
terraform destroy             # WARNING → confirmation required
kubectl delete namespace      # WARNING
aws s3 rm --recursive         # WARNING
```

## Safe Alternatives Suggested
| Blocked | Suggested Safe Alternative |
|---------|---------------------------|
| `git push -f` | `git push --force-with-lease` |
| `rm -rf dir` | `mv dir /tmp/backup-$(date +%s)` |
| `git reset --hard` | `git stash` then `git reset --soft` |
| `DROP TABLE` | `ALTER TABLE ... RENAME TO ...` first |

## Install
```bash
cargo install dcg
dcg init    # adds PreToolUse hook to ~/.claude/settings.json
```
Or without Rust:
```bash
git clone https://github.com/kenryu42/claude-code-safety-net
./install.sh
```

## Configuration
```toml
# ~/.dcg/config.toml
[rules]
allow_force_push = false
allow_rm_rf = false
require_backup_before_drop = true
production_branches = ["main", "master", "prod"]

[confirmation]
timeout_seconds = 10
require_explicit = true
```

## Hook Output
```
⚠️  BLOCKED: Destructive command detected
Command: git push --force origin main
Reason: Force push to main branch is permanently blocked
Safe alternative: git push --force-with-lease origin main

Type 'CONFIRM' within 10s to override (not recommended):
```

## Why This Matters for AI Agents
Claude Code can generate and execute commands autonomously. Without safety-net:
- A buggy refactor might `git reset --hard` losing work
- Cleanup code might `rm -rf` wrong directory
- Migration script might `DROP TABLE` on production DB

safety-net adds a final guardrail at the OS/git level, independent of LLM behavior.
