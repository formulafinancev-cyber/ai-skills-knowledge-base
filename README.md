# Formula Finance AI Office — Skills & Knowledge Base

> Централизованное хранилище скиллов и базы знаний для агентов Formula Finance AI Office.

## Структура

```
ai-skills-knowledge-base/
├── skills/
│   ├── user/          # Скиллы разработки (16 скиллов)
│   ├── public/        # Публичные скиллы (8 скиллов)
│   └── examples/      # Примеры скиллов (22 скилла)
├── knowledge/
│   ├── project/       # Архитектурные документы (79 файлов)
│   ├── agents/        # Промпты агентов
│   └── business/      # Бизнес-контекст
└── INDEX.md
```

## Приоритетные скиллы для проекта

### 🟢 Обязательные (использовать сейчас)
| Скилл | Назначение |
|---|---|
| `skills/user/agency-agents` | Financial Analyst, Analytics Reporter, Finance Tracker |
| `skills/user/systematic-debugging` | Отладка runtime |
| `skills/user/verification-before-completion` | Проверка перед коммитом |
| `skills/user/writing-plans` | Декомпозиция перед кодом |
| `skills/user/executing-plans` | Исполнение с checkpoint'ами |
| `skills/user/using-superpowers` | Foundational |
| `skills/public/xlsx` | KPI, CRM, управленческая отчётность |
| `skills/public/pdf-reading` | Чтение клиентских документов |

### 🟡 Полезные (по задаче)
| Скилл | Когда |
|---|---|
| `skills/user/code-review-pr` | При добавлении каждого агента |
| `skills/user/test-driven-development` | handlers.py + runtime.py |
| `skills/user/brainstorming` | Перед проектированием нового агента |
| `skills/examples/mcp-builder` | Внешние интеграции (Этап 3) |
| `skills/examples/web-artifacts-builder` | Pixel Office UI (Этап 4) |
| `skills/public/docx` | КП, договоры |
| `skills/public/pptx` | Презентации |

## Стек проекта

```
Python 3.12 + python-telegram-bot 21.x
Anthropic API → claude-sonnet-4-5-20250929
SQLite: tasks / agent_statuses / event_logs / agent_learnings / agent_prompts
Telegram — основной интерфейс команды
```

## Текущий статус (май 2026)

- ✅ Шаги 1–5: каркас, config, db, storage, knowledge, prompts, llm, main, auth-guard
- ⏳ Шаг 6: `/next` и `/agent` через LLM
- 🔜 Шаг 7: handlers.py + runtime.py
- 🔜 Шаг 8+: динамические промпты, второй агент

---
*Обновлено: 2026-05-01*
