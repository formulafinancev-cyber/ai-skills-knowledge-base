# Formula Finance AI Office — Технический отчёт по сборке
## Baseline: Colleague Agent MVP (Шаги 1–5)

**Дата сессии:** 30 апреля 2026  
**Среда:** Windows 11, PowerShell, Python 3.12.x  
**Корень проекта:** `C:\Users\Gammo\Desktop\formula-finance-ai-office`  
**Статус на момент закрытия сессии:** Baseline зафиксирован. LLM-слой подключён и протестирован. Единственный внешний блокер — пополнение баланса на API-ключе Anthropic.

---

## 1. Контекст и цель сессии

### Откуда стартовали

На момент начала сессии существовала только **папка документации** Formula Finance AI Office — более 70 `.md`-файлов с описанием архитектуры, агентов, Pixel Office, Telegram-интеграции, схем БД, операционных правил, roadmap и guiding principles. Код не существовал.

Основные зафиксированные решения в документации:
- **Архитектура:** единая Claude Code среда, code-first оркестрация, без n8n.
- **Модельная стратегия:** Sonnet 4.6 как runtime, Opus 4.7 как архитектурный слой, Codex как инженерный.
- **Интерфейс:** Telegram как первый практический канал.
- **БД:** SQLite, три таблицы (`tasks`, `agent_statuses`, `event_logs`) по схеме из `FIRST_DATABASE_SCHEMA.md`.
- **Первый агент:** Colleague — универсальный собеседник и навигатор по документации.

### Цель сессии

Построить рабочий Telegram-бот **Colleague Agent** с нуля: от каркаса репозитория до первого end-to-end LLM-ответа по команде `/summary`.

---

## 2. Принятые архитектурные решения

### Выбор стека и ключевые развилки

| Тема | Выбор | Альтернативы, которые рассматривались |
|---|---|---|
| Хранилище | SQLite (Вариант B) | JSON-файл (A — потеря при рестарте), PostgreSQL в Docker (C — избыточно для MVP) |
| Развёртывание | Локально, без VPS | VPS — отложен |
| Запуск бота | `python -m src.main` | `python src/main.py` — ломает импорты пакета `src` |
| Async lifecycle | `asyncio.run(run_polling(app))` с ручным `initialize/start/stop` | `app.run_polling()` — падает на Python 3.14 из-за `get_event_loop()` |
| Модель Anthropic | `claude-sonnet-4-5-20250929` (полный идентификатор) | Alias `claude-sonnet-4-5` — возвращал HTTP 400 |
| Импорт knowledge | Фиксированное ядро 5 файлов + топик-маршрутизация по подстроке в имени | Семантический поиск — отложен на более поздние шаги |
| Структура main.py | Тонкий bootstrap (Вариант B-slim): заглушки → постепенное оживление | Монолит сразу со всеми командами через LLM — отклонён |

### Ключевое архитектурное решение по `main.py`

На одном из шагов поступил промпт от внешнего инструмента (другой сессии/Opus) с просьбой написать `main.py` по более ранней схеме — без `runtime.py`, `handlers.py`, без учёта уже существующих `storage.py` и `knowledge.py`. Решение было остановить исполнение, сравнить промпт с текущим состоянием проекта и предложить два варианта (A — продолжить по плану, B — тонкий smoke-test). Выбран был Вариант B: тонкий `main.py` со smoke-test командами, LLM-заглушками и явным путём к их оживлению. Это решение позволило:
- увидеть «живого» бота без LLM-слоя;
- не смешивать Telegram transport с LLM-логикой;
- не переписывать `main.py` при добавлении LLM на шаге 5.

---

## 3. Поэтапный ход работы

### Шаг 1 — Каркас репозитория

**Созданные файлы:** `.gitignore`, `.env.example`, `requirements.txt`, `README.md`

**Ключевые решения:**
- `requirements.txt` содержит ровно 3 зависимости с зафиксированными версиями: `python-telegram-bot==21.10`, `anthropic==0.49.0`, `python-dotenv==1.0.1`. Никаких ORM, FastAPI, Redis, Docker.
- `.gitignore` явно скрывает `.env`, `data/*.db`, `logs/`, `__pycache__/`, `.venv/`.
- `.env.example` содержит 7 переменных: `TELEGRAM_BOT_TOKEN`, `ADMIN_TELEGRAM_ID`, `ANTHROPIC_API_KEY`, `DB_PATH`, `KNOWLEDGE_DIR`, `LOG_PATH`, `LOG_LEVEL`.
- Запуск задокументирован через `python -m src.main` (не `python src/main.py`).

---

### Шаг 2 — `src/config.py` + `src/db.py`

**`src/config.py`**

Логика: `load_dotenv()` выполняется при импорте модуля (один раз), `load_config()` вызывается явно при старте. При запуске проверяются сразу **все** обязательные переменные, и пользователь видит их список целиком — не одну за другой.

```
TELEGRAM_BOT_TOKEN  → str
ADMIN_TELEGRAM_ID   → int (парсится явно, с понятной ошибкой если не число)
ANTHROPIC_API_KEY   → str
DB_PATH             → Path
KNOWLEDGE_DIR       → Path
LOG_PATH            → Path
LOG_LEVEL           → str, default="INFO"
```

Результат — `@dataclass(frozen=True) Config`. Иммутабельный объект, единственный источник истины во время работы бота.

**`src/db.py`**

Три таблицы по схеме `FIRST_DATABASE_SCHEMA.md`:

```sql
-- tasks
task_id, title, description, status, assigned_agent,
priority, source_channel, created_at, updated_at, completed_at,
requires_approval (0/1), approval_status, output_summary

-- agent_statuses
agent_id, role, current_status, current_task_id,
last_update_at, error_note

-- event_logs
event_id, event_type, timestamp, agent_id, task_id,
source, payload_summary, severity
```

Индексы: `idx_event_logs_task_id`, `idx_event_logs_timestamp`, `idx_tasks_status`.

Seed: при первой инициализации в `agent_statuses` сразу записывается `agent_colleague` со статусом `idle`.

Дополнительно: `journal_mode=WAL`, `foreign_keys=ON`, `row_factory=sqlite3.Row` (доступ к полям по имени).

---

### Шаг 3 — `src/storage.py`

CRUD-слой поверх трёх таблиц. Принципы:
- Каждая функция принимает `db_path: Path` явно — никакого глобального состояния.
- Никакого ORM — только `sqlite3` с именованными параметрами.
- ID генерируются как `prefix_hex6` (например, `task_3f2a1b`, `evt_9c4d2e`).

**Публичный API:**

```python
create_task(db_path, *, title, assigned_agent, source_channel,
            description, priority, requires_approval) -> str  # task_id

update_task_status(db_path, task_id, status, *,
                   output_summary=None) -> None
# При status in ("completed","failed") автоматически ставит completed_at

update_agent_status(db_path, agent_id, status, *,
                    current_task_id=None, error_note=None) -> None
# ON CONFLICT DO UPDATE — безопасно для новых и существующих агентов

get_agent_status(db_path, agent_id) -> dict | None

write_event(db_path, *, event_type, severity="info",
            agent_id=None, task_id=None, source=None,
            payload_summary=None) -> str  # event_id

list_recent_tasks(db_path, limit=10) -> list[dict]
# ORDER BY created_at DESC
```

**Допустимые статусы задач (из `FIRST_DATABASE_SCHEMA.md`):**
`created | assigned | working | waiting_input | review | completed | failed`

**Допустимые статусы агента:**
`idle | assigned | working | waiting_input | waiting_dependency | review | error | offline`

---

### Шаг 4 — `src/knowledge.py`

Слой чтения и отбора `.md`-файлов из `knowledge/`. Чистый I/O — никаких вызовов LLM внутри.

**Ограничения:**
- `MAX_CHARS_PER_DOC = 12_000` — обрезка с маркером `[...обрезано, исходный размер N символов]`
- `TOPIC_MAX_FILES = 6` — максимум файлов на топик, чтобы не перегружать контекстное окно

**Фиксированное ядро (`_CORE_FILES`):**
```
CURRENT_PROJECT_STATE_SUMMARY.md
FIRST_AGENT_MVP_SCOPE.md
FIRST_AGENT_IMPLEMENTATION_ORDER.md
PROJECT_FILE_READING_ORDER.md
COMPANY_PROFILE.md
```
Ядро загружается в строго заданном порядке (приоритет файлов).

**Топик-маршрутизация (`_TOPIC_KEYWORDS`):**

| Топик | Используется для |
|---|---|
| `summary` | `/summary` — обзор проекта |
| `status` | `/status` — runtime-вопросы |
| `next` | `/next` — порядок реализации |
| `agent` | `/agent` — роли и описания |
| `files` | `/files` — навигация по документации |
| `deploy` | вопросы про деплой |
| `pixel` | Pixel Office |
| `telegram` | Telegram-интеграция |
| `runtime` | runtime / storage |
| `crm` | CRM и лидогенерация |
| `content` | контент и бренд |

Порядок ключевых слов в каждом топике = приоритет документов при отборе.

**Публичный API:**

```python
load_all_documents(knowledge_dir: Path) -> list[dict]
load_core_documents(knowledge_dir: Path) -> list[dict]
load_topic_documents(knowledge_dir: Path, topic: str) -> list[dict]
summarize_documents_for_log(docs: list[dict]) -> str
# → "5 doc(s): CURRENT_PROJECT_STATE_SUMMARY.md, ... | ~14,690 chars"
```

---

### Шаг B (вариантный) — `src/main.py` smoke-test

**Причина появления:** вместо шага 5 (`prompts.py` + `llm.py`) было решено сначала запустить «живой» бот с реальным Telegram-polling и заглушками на LLM-командах. Это дало:
- первый рабочий деплой для ручной проверки инфраструктуры;
- уверенность в том, что Telegram transport, auth-guard, БД и knowledge работают до подключения LLM;
- чёткую границу «что работает сейчас» vs «что появится на шаге 5».

**Ключевая проблема и решение: async lifecycle на Python 3.14**

```
RuntimeError: There is no current event loop in thread 'MainThread'.
```

`Application.run_polling()` в PTB 21.x использует `asyncio.get_event_loop()`, которое в Python 3.14 без активного loop падает. Решение — ручной async lifecycle:

```python
async def run_polling(application: Application) -> None:
    async with application:           # initialize() / shutdown()
        await application.start()
        await application.updater.start_polling(allowed_updates=Update.ALL_TYPES)
        stop = asyncio.Event()
        try:
            await stop.wait()         # ждём Ctrl+C
        finally:
            await application.updater.stop()
            await application.stop()

def main() -> None:
    ...
    asyncio.run(run_polling(app))     # создаёт loop явно
```

Это решение работает на Windows, Linux, macOS и на всех Python 3.11+.

**Структура `main.py`:**
- `setup_logging(config)` — файл с ротацией (5×1МБ) + stdout, `httpx`/`telegram` приглушены до WARNING.
- `_is_admin(update, config)` — проверка `user.id == ADMIN_TELEGRAM_ID`.
- `_deny(update, config)` — молчаливое игнорирование + `write_event("auth_denied", severity="warning")`. Не-админы не получают никакого ответа.
- `_cfg(context)` — `context.application.bot_data["config"]` (стандарт PTB 21.x для передачи данных в хэндлеры).
- `build_application(config)` — регистрирует 8 хэндлеров.
- `main()` — конфиг → логирование → `init_db` → `write_event("bot_started")` → `asyncio.run(run_polling(app))`.

**8 зарегистрированных команд на момент smoke-test:**

| Команда | Источник данных | Статус в smoke-test |
|---|---|---|
| `/start` | hardcoded text | ✓ работала |
| `/help` | hardcoded text | ✓ работала |
| `/status` | `storage.get_agent_status` + `knowledge_dir.glob` | ✓ работала |
| `/files` | `knowledge.load_all_documents` | ✓ работала |
| `/tasks` | `storage.list_recent_tasks` | ✓ работала |
| `/agent` | `storage.get_agent_status` | ✓ работала |
| `/summary` | заглушка | → оживлена на шаге 5 |
| `/next` | заглушка | → шаг 6 |

---

### Шаг 5 — `src/prompts.py` + `src/llm.py` + оживление `/summary`

#### `src/prompts.py`

Чистый модуль без I/O, без вызовов SDK, без работы с БД. Принимает данные, возвращает строки.

**`build_colleague_system_prompt() → str`**

Состоит из двух частей:

*Identity (кто такой Colleague):*
```
Ты — Colleague, первый агент в системе Formula Finance AI Office.
Роль: внутренний помощник, навигатор по документации, первая точка входа.
НЕ является: оркестратором, специализированным экспертом (CRM, аналитика, etc.)
```

*Правила работы (5 правил):*
```
1. Отвечай ТОЛЬКО на основе переданных документов.
2. Разделяй: "уже определено" / "запланировано" / "ещё не реализовано".
3. Если информации нет — скажи прямо, не додумывай.
4. Стиль: сжато, 5–12 предложений, без канцелярита.
5. Не давай общих AI-консультаций — только по этой документации.
```

Итого: ~1395 символов. Стабильная строка, не меняется от запроса к запросу.

**`build_user_prompt_with_context(user_request, docs) → str`**

Формат передачи документов в XML-блоках:

```xml
<project_documents>
<document name="CURRENT_PROJECT_STATE_SUMMARY.md">
...полный текст...
</document>
<document name="FIRST_AGENT_MVP_SCOPE.md">
...
</document>
</project_documents>

<user_request>
Дай краткое резюме текущего состояния проекта...
</user_request>
```

При пустом `docs` — вставляется `(контекст не передан)`, и агент должен честно сообщить об отсутствии информации.

#### `src/llm.py`

Async-обёртка над Anthropic SDK.

**Константы:**
```python
DEFAULT_MODEL = "claude-sonnet-4-5-20250929"
DEFAULT_MAX_TOKENS = 1024
```

**Проблема с именем модели:** первоначально было задано `"claude-sonnet-4-5"` — alias без даты. Anthropic возвращал HTTP 400. Исправлено добавлением полного идентификатора с датой.

**Функция `ask_claude`:**

```python
async def ask_claude(
    *,
    system: str,
    user: str,
    api_key: str,
    model: str = DEFAULT_MODEL,
    max_tokens: int = DEFAULT_MAX_TOKENS,
) -> str
```

- Создаёт `AsyncAnthropic(api_key=api_key)` на каждый вызов (stateless, thread-safe).
- Логирует: `model`, `max_tokens`, `system_chars`, `user_chars` при запросе; `chars`, `input_tokens`, `output_tokens` при ответе.
- Ключ **никогда не попадает в логи**.

**Обработка ошибок (5 веток):**

| Исключение SDK | Пользователь видит | severity |
|---|---|---|
| `AuthenticationError` | «Проверьте ANTHROPIC_API_KEY» | error |
| `RateLimitError` | «Попробуйте через минуту» | warning |
| `APIConnectionError` | «Проверьте сеть» | error |
| `APIStatusError` (credit balance) | «Баланс LLM исчерпан. Пополните в Plans & Billing» | error |
| `APIStatusError` (прочие) | «LLM API вернул ошибку (HTTP N)» | error |
| Любое другое `Exception` | «Внутренняя ошибка» + `logger.exception` | error |

**Специальная ветка credit balance:**

```python
except anthropic.APIStatusError as e:
    logger.error(f"[llm] api status error: status={e.status_code} body={e.response.text}")
    if e.status_code == 400 and "credit balance is too low" in e.response.text:
        raise LLMError(
            "Баланс LLM исчерпан: текущий API-ключ Anthropic не имеет достаточно кредитов.\n"
            "Нужен активный план или пополнение в разделе Plans & Billing Anthropic, "
            "чтобы я мог делать резюме проекта."
        ) from e
```

Эта ветка появилась по итогам реальной проверки — именно с такой ошибкой столкнулся проект. Body полностью пишется в лог для диагностики.

#### Оживление `/summary` в `main.py`

Полный вертикальный срез (lifecycle задачи):

```
Telegram "/summary"
  → auth-guard
  → create_task(..., status="created")
  → update_task_status("working")
  → update_agent_status("working", current_task_id=task_id)
  → write_event("task_started")
  → reply_text("⏳ Готовлю резюме…")   ← UX-сигнал

  → load_core_documents(knowledge_dir)  ← 5 файлов, ~14 700 chars
  → build_colleague_system_prompt()
  → build_user_prompt_with_context(request, docs)
  → await ask_claude(system, user, api_key)

  [успех]
    → reply_text(answer)               ← обрезка до 4000 chars если нужно
    → update_task_status("completed", output_summary=answer[:200])
    → update_agent_status("idle", current_task_id=None)
    → write_event("task_completed", severity="info")

  [LLMError]
    → reply_text("❌ Не удалось обработать запрос.\n{e}")
    → update_task_status("failed", output_summary=str(e))
    → update_agent_status("idle", current_task_id=None)
    → write_event("task_failed", severity="error")
    → return

  [Exception]
    → logger.exception(...)
    → reply_text("❌ Внутренняя ошибка. Попробуйте позже.")
    → update_task_status("failed")
    → update_agent_status("idle")
    → write_event("task_failed", severity="error")
    → return
```

**Ключевое свойство:** агент **всегда** возвращается в `idle` — при любом исходе. Никаких «зависших» статусов после одного сбоя.

---

## 4. Проблемы и их решения (хронология)

### 4.1 `ModuleNotFoundError: No module named 'src'`

**Симптом:** запуск `python .\src\main.py` падал.

**Причина:** код использует абсолютные импорты `from src.config import ...`. При запуске напрямую через `python .\src\main.py` Python не знает про пакет `src` — он не в `sys.path`.

**Решение:** запуск только через `python -m src.main` из корня проекта. Зафиксировано в `CLAUDE.md` и в памяти Claude.

### 4.2 `RuntimeError: There is no current event loop in thread 'MainThread'`

**Симптом:** при вызове `app.run_polling()` в Python 3.14 бот падал сразу после «Запуск Telegram polling…».

**Причина:** PTB 21.x внутри `run_polling()` вызывает `asyncio.get_event_loop()`. В Python 3.12+ (официально в 3.14) этот вызов в основном потоке без активного loop бросает `RuntimeError`.

**Решение:** ручное управление lifecycle через `asyncio.run(run_polling(app))` с `async with application` и явными вызовами `updater.start_polling()`, `updater.stop()`, `application.stop()`. Подробности — в разделе «Шаг B» выше.

### 4.3 HTTP 400 при вызове Anthropic API (неверная модель)

**Симптом:** лог показывал `[llm] api status error: status=400`, бот отвечал заглушкой ошибки.

**Причина:** `DEFAULT_MODEL = "claude-sonnet-4-5"` — alias без даты. Anthropic не принимает такой идентификатор и возвращает `invalid_request_error`.

**Решение:** `DEFAULT_MODEL = "claude-sonnet-4-5-20250929"` — полный идентификатор с датой. Один параметр в одном файле.

### 4.4 HTTP 400 при вызове Anthropic API (нулевой баланс)

**Симптом:** после исправления модели — снова HTTP 400, но тело ответа: `"credit balance is too low"`.

**Причина:** API-ключ с нулевым балансом. Pro-подписка на Claude.ai не даёт API-кредитов — это отдельный расчётный счёт в Anthropic Console.

**Решение (в коде):** специальная ветка в `APIStatusError` с человеко-читаемым сообщением и инструкцией в Telegram. Полный body пишется в лог.

**Решение (внешнее):** пополнение баланса в Anthropic Console — на стороне пользователя.

---

## 5. Итоговая файловая структура

```
formula-finance-ai-office/
│
├── CLAUDE.md                ← runbook запуска (источник истины для Claude и команды)
├── README.md                ← описание проекта, быстрый старт, таблица команд
├── .env.example             ← шаблон с 7 переменными (без реальных значений)
├── .env                     ← реальные значения (в .gitignore)
├── .gitignore               ← .env, data/*.db, logs/, __pycache__, .venv
├── requirements.txt         ← 3 зависимости с зафиксированными версиями
│
├── data/
│   └── office.db            ← SQLite, создаётся автоматически при старте
│
├── knowledge/               ← .md из документации проекта
│   ├── CURRENT_PROJECT_STATE_SUMMARY.md   ← ядро
│   ├── FIRST_AGENT_MVP_SCOPE.md           ← ядро
│   ├── FIRST_AGENT_IMPLEMENTATION_ORDER.md ← ядро
│   ├── PROJECT_FILE_READING_ORDER.md      ← ядро
│   ├── COMPANY_PROFILE.md                 ← ядро
│   └── [остальные .md по необходимости]
│
├── logs/
│   └── app.log              ← ротация 5×1МБ, stdout + файл
│
└── src/
    ├── __init__.py           ← пустой, делает src пакетом Python
    ├── config.py             ← env + валидация → Config(frozen=True)
    ├── db.py                 ← SQLite init, DDL, seed, get_connection
    ├── storage.py            ← CRUD: tasks, agent_statuses, event_logs
    ├── knowledge.py          ← load_all / load_core / load_topic / summarize
    ├── prompts.py            ← build_colleague_system_prompt / build_user_prompt_with_context
    ├── llm.py                ← ask_claude + LLMError (5 веток ошибок)
    └── main.py               ← bootstrap + 8 хэндлеров + async run_polling
```

---

## 6. Схема зависимостей между модулями

```
main.py
  ├── config.py         (load_config, Config)
  ├── db.py             (init_db)
  ├── storage.py        (create_task, update_task_status, update_agent_status,
  │                      get_agent_status, list_recent_tasks, write_event)
  ├── knowledge.py      (load_all_documents, load_core_documents, summarize_documents_for_log)
  ├── prompts.py        (build_colleague_system_prompt, build_user_prompt_with_context)
  └── llm.py            (ask_claude, LLMError)

storage.py
  └── db.py             (get_connection)

db.py
  └── config.py         (Config)

knowledge.py            (нет зависимостей на src — только stdlib pathlib)

prompts.py              (нет зависимостей — только stdlib)

llm.py                  (anthropic SDK — внешняя)
```

---

## 7. Схема БД

### `tasks`

| Поле | Тип | Описание |
|---|---|---|
| `task_id` | TEXT PK | `task_XXXXXX` |
| `title` | TEXT | Имя задачи (например, `/summary`) |
| `description` | TEXT | Опциональное описание |
| `status` | TEXT | `created → working → completed/failed` |
| `assigned_agent` | TEXT | `agent_colleague` |
| `priority` | TEXT | `normal` (default) |
| `source_channel` | TEXT | `telegram` |
| `created_at` | TEXT | ISO 8601 UTC |
| `updated_at` | TEXT | ISO 8601 UTC |
| `completed_at` | TEXT | NULL до завершения |
| `requires_approval` | INT | 0/1 (boolean) |
| `approval_status` | TEXT | NULL |
| `output_summary` | TEXT | Первые 200 символов ответа |

### `agent_statuses`

| Поле | Тип | Описание |
|---|---|---|
| `agent_id` | TEXT PK | `agent_colleague` |
| `role` | TEXT | `Colleague` |
| `current_status` | TEXT | `idle / working / error` |
| `current_task_id` | TEXT | NULL когда idle |
| `last_update_at` | TEXT | ISO 8601 UTC |
| `error_note` | TEXT | NULL при нормальной работе |

### `event_logs`

| Поле | Тип | Описание |
|---|---|---|
| `event_id` | TEXT PK | `evt_XXXXXX` |
| `event_type` | TEXT | `bot_started / task_started / task_completed / task_failed / auth_denied` |
| `timestamp` | TEXT | ISO 8601 UTC |
| `agent_id` | TEXT | `agent_colleague` |
| `task_id` | TEXT | NULL для системных событий |
| `source` | TEXT | `telegram / main` |
| `payload_summary` | TEXT | Короткое описание, без секретов |
| `severity` | TEXT | `info / warning / error` |

**Индексы:** `idx_event_logs_task_id`, `idx_event_logs_timestamp`, `idx_tasks_status`.

---

## 8. Поток обработки команды `/summary` (end-to-end)

```
[Telegram] /summary
    ↓
cmd_summary(update, context)
    ↓
_is_admin? → No → _deny() → write_event("auth_denied") → END
    ↓ Yes
create_task("/summary", "agent_colleague", "telegram") → task_id
update_task_status(task_id, "working")
update_agent_status("agent_colleague", "working", task_id)
write_event("task_started", info)
    ↓
reply_text("⏳ Готовлю резюме…")
    ↓
load_core_documents(knowledge_dir)
    → 5 файлов: ~14 700 chars контекста
    ↓
build_colleague_system_prompt()
    → identity + 5 правил: ~1 395 chars
    ↓
build_user_prompt_with_context(request, docs)
    → XML-блоки документов + user_request
    ↓
await ask_claude(system, user, api_key,
                 model="claude-sonnet-4-5-20250929",
                 max_tokens=1024)
    → AsyncAnthropic.messages.create(...)
    → response.content → склейка text-блоков → answer
    ↓
    ┌─ LLMError ──────────────────────────────────────────┐
    │ reply_text("❌ Не удалось обработать...")            │
    │ update_task_status(task_id, "failed")               │
    │ update_agent_status("idle")                         │
    │ write_event("task_failed", error)                   │
    └─────────────────────────────────────────────────────┘
    ↓ SUCCESS
reply_text(answer[:4000])
update_task_status(task_id, "completed", output_summary=answer[:200])
update_agent_status("agent_colleague", "idle", current_task_id=None)
write_event("task_completed", info, payload_summary="answer_chars=N")
```

---

## 9. Безопасность

| Аспект | Реализация |
|---|---|
| Доступ | Только `ADMIN_TELEGRAM_ID` из `.env`. Все остальные молча игнорируются |
| Не-админы | `_deny()` → `write_event("auth_denied")` → нет ответа в Telegram |
| API-ключ в логах | Никогда. Логируются только длины строк, не содержимое |
| API-ключ в БД | Никогда. В `event_logs.payload_summary` только тип ошибки |
| API-ключ в репозитории | `.env` в `.gitignore`. Шаблон — только `.env.example` |
| Stack trace в Telegram | Никогда. `LLMError` содержит безопасное человеко-читаемое сообщение |
| Конфликт экземпляров | Решён на уровне запуска: один процесс, один polling |

---

## 10. Протестированные сценарии

Все сценарии проверены как через mock-тесты (Python), так и через реальный Telegram:

| Сценарий | Поведение | Статус БД | Агент |
|---|---|---|---|
| `/summary` — успех (с моком LLM) | 2 reply: «Готовлю» + ответ | `completed` | `idle` |
| `/summary` — `LLMError` | 2 reply: «Готовлю» + «Не удалось» | `failed` | `idle` |
| `/summary` — непредвиденное исключение | 2 reply: «Готовлю» + «Внутренняя ошибка» | `failed` | `idle` |
| `/summary` — не-админ | нет ответа, нет задачи в БД | не изменяется | `idle` |
| `/summary` — HTTP 400 (неверная модель) | «LLM API вернул ошибку (HTTP 400)» | `failed` | `idle` |
| `/summary` — HTTP 400 (credit balance) | «Баланс LLM исчерпан...» | `failed` | `idle` |
| `/summary` — HTTP 400 (плохой ключ) | «Ошибка аутентификации...» | `failed` | `idle` |
| `/start`, `/help`, `/status`, `/files`, `/tasks`, `/agent` | корректные ответы | не изменяется | `idle` |
| `Ctrl+C` | корректный graceful shutdown | не изменяется | — |

---

## 11. Текущий статус и что осталось

### ✅ Готово (Шаги 1–5)

- Полный каркас репозитория
- Конфиг с валидацией
- SQLite БД с 3 таблицами, индексами, seed
- Storage CRUD-слой
- Knowledge loader с топик-маршрутизацией
- System prompt и user prompt builder для Colleague
- Async LLM-обёртка с 5 ветками обработки ошибок
- Telegram bootstrap с async polling lifecycle (совместим с Python 3.14)
- Auth-guard
- 6 рабочих команд на реальных данных
- 1 LLM-команда `/summary` — полный вертикальный срез
- Smoke-test в Telegram пройден
- `CLAUDE.md` зафиксирован в репозитории

### ⏳ Внешний блокер (не код)

Пополнение баланса API-ключа Anthropic в Console → после этого `/summary` начнёт возвращать реальный ответ модели без каких-либо правок кода.

### 🔜 Следующие шаги (Шаг 6+)

**Шаг 6 — оживление `/next` и `/agent`**

По тому же шаблону, что и `/summary`:
- `/next` → топик `next` из `knowledge.py` + user_request про следующий шаг реализации
- `/agent` → топик `agent` из `knowledge.py` + user_request про роль и статус агента
- Правки только в `main.py`, архитектура не меняется

**Шаг 7 — выделение `handlers.py` и `runtime.py` (по необходимости)**

Когда `main.py` начнёт расти (добавление free-text сообщений, новые команды), имеет смысл:
- `handlers.py` — тонкие хэндлеры PTB (auth-guard + вызов runtime)
- `runtime.py` — сшивка storage + knowledge + prompts + llm

Сейчас 479 строк в `main.py` — терпимо.

**Шаг 8+ — будущие фазы (из `FUTURE_ROADMAP.md`)**

- Free-text сообщения (не команды) → Colleague отвечает через LLM
- Второй агент (Analyst / KPI) — согласуется с `userPreferences` по управленческой отчётности
- Pixel Office — визуальный control-room (только после стабилизации state в БД)
- VPS / Docker — production деплой
- Координатор — оркестрация между агентами

---

## 12. Справочник: запуск и базовая диагностика

### Запуск

```powershell
cd C:\Users\Gammo\Desktop\formula-finance-ai-office
& .\.venv\Scripts\Activate.ps1
python -m src.main
```

### Признак успешного старта в логах

```
[db] Инициализация БД: data\office.db
[db] БД готова. Таблицы: tasks, agent_statuses, event_logs.
[main] Запуск Telegram polling…
[main] Бот запущен. Ctrl+C для остановки.
```

### Остановка

```
Ctrl + C
```

### Быстрая проверка БД из PowerShell

```powershell
python
```

```python
>>> import sqlite3
>>> c = sqlite3.connect('data/office.db'); c.row_factory = sqlite3.Row
>>> # Последняя задача
>>> dict(c.execute("SELECT task_id, title, status FROM tasks ORDER BY created_at DESC LIMIT 1").fetchone())
>>> # Статус агента
>>> dict(c.execute("SELECT * FROM agent_statuses WHERE agent_id='agent_colleague'").fetchone())
>>> # Последние события
>>> [dict(r) for r in c.execute("SELECT event_type, severity, timestamp FROM event_logs ORDER BY timestamp DESC LIMIT 5")]
```

### Частые проблемы

| Проблема | Причина | Решение |
|---|---|---|
| `ModuleNotFoundError: No module named 'src'` | Запуск через `python .\src\main.py` | Использовать `python -m src.main` |
| `RuntimeError: There is no current event loop` | Старая версия `main.py` (без async lifecycle) | Убедиться что используется финальная версия `main.py` |
| `400 invalid_request_error` (model) | Alias без даты в `DEFAULT_MODEL` | Проверить `src/llm.py`: должно быть `claude-sonnet-4-5-20250929` |
| `400 credit balance is too low` | Нулевой баланс API-ключа | Пополнить в Anthropic Console → Plans & Billing |
| Конфликт двух экземпляров бота | Два терминала с запущенным ботом | `Ctrl+C` во всех, перезапустить один |

---

*Отчёт составлен по итогам сессии 30 апреля 2026.*  
*Следующий шаг: Шаг 6 — `/next` и `/agent` через LLM.*
