# AI Skills & Knowledge Base

Полная коллекция скиллов и knowledge-файлов для Claude.ai и Claude Code.

## Структура

```
skills/
  user/       — 200 установленных скиллов
  public/     — официальные Anthropic скиллы
  examples/   — примеры скиллов
knowledge/    — дополнительные knowledge-файлы
```

## Статистика

| Категория | Кол-во |
|-----------|--------|
| user skills | 200 |
| public skills | 16 |
| example skills | 44 |
| **ИТОГО** | **260** |

## Префиксы скиллов

| Префикс | Источник |
|---------|---------|
| `agency-agents`, `brainstorming`, `systematic-debugging` и др. | obra/superpowers + custom |
| `jf-*` | jeffallan/claude-skills (66 full-stack скиллов) |
| `ar-*` | alirezarezvani/claude-skills (finance, C-level, PM) |
| `gb-*` | glebis/claude-skills (44 инструментальных скилла) |
| `know-*` | Knowledge-скиллы (синтез из продуктов без SKILL.md) |
| `acc-*` | awesome-claude-code resources |
| `superclaude-*` | SuperClaude Framework |

## Ключевые скиллы для FFA/HoReCa

- `master-router` — маршрутизатор, читать первым
- `agency-agents` — FFA-специфичные агенты
- `ar-finance` — финансовый аналитик
- `ar-c-level-advisor` — CEO/CFO советник
- `gb-tufte-report` — Tufte-стиль дашборды
- `gb-tdd` — multi-agent TDD
- `code-review-excellence` — code review по 16 языкам

## Установка

```bash
git clone https://github.com/formulafinancev-cyber/ai-skills-knowledge-base.git
cp -r ai-skills-knowledge-base/skills/user/* ~/.claude/skills/
```
