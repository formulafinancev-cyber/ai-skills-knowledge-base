# Formula Finance AI Office — CLAUDE.md

> **Это главный контекстный файл проекта.**
> Читается Claude Code при каждом запуске сессии.
> Не изменяй архитектурные решения без явного подтверждения пользователя.

---

## 1. ЗАПУСК И ОСТАНОВКА

### Запуск (Windows PowerShell, всегда из корня проекта)

```powershell
cd C:\Users\Gammo\Desktop\formula-finance-ai-office
& .\.venv\Scripts\Activate.ps1
python -m src.main
```

### Признак успешного старта

```
[db] Инициализация БД: data\office.db
[db] БД готова. Таблицы: tasks, agent_statuses, event_logs.
[main] Запуск Telegram polling…
[main] Бот запущен. Ctrl+C для остановки.
```

### Остановка

```powershell
Ctrl + C
```

### КРИТИЧЕСКИ ВАЖНО

- **Никогда** не запускать через `python .\src\main.py` — ломает импорты пакета `src`.
- **Всегда** использовать `python -m src.main` из корня проекта.
- **Всегда** активировать `.venv` перед запуском.

---

## 2. СТЕК И ЗАВИСИМОСТИ

```
Python 3.12.x
python-telegram-bot==21.10
anthropic==0.49.0
python-dotenv==1.0.1
```

Никаких ORM, FastAPI, Redis, Docker, n8n в текущем MVP.
База данных: SQLite (`data/office.db`).
Хранение знаний: `.md`-файлы в `knowledge/`.

---

## 3. ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ

Все переменные читаются из `.env` (не коммитить). Шаблон: `.env.example`.

| Переменная | Тип | Описание |
|---|---|---|
| `TELEGRAM_BOT_TOKEN` | str | Токен бота от @BotFather |
| `ADMIN_TELEGRAM_ID` | int | Владелец — полный доступ + approve |
| `ALLOWED_USER_IDS` | str | ID сотрудников через запятую: `123,456,789` |
| `ANTHROPIC_API_KEY` | str | Ключ Anthropic Console |
| `DB_PATH` | Path | Путь к SQLite файлу (`data/office.db`) |
| `KNOWLEDGE_DIR` | Path | Папка с `.md`-файлами знаний (`knowledge/`) |
| `PROMPTS_DIR` | Path | Папка с промптами агентов (`prompts/`) |
| `LOG_PATH` | Path | Путь к лог-файлу (`logs/office.log`) |
| `LOG_LEVEL` | str | Уровень логирования (default: `INFO`) |

---

## 4. СТРУКТУРА ПРОЕКТА

```
formula-finance-ai-office/
├── src/
│   ├── main.py          # Точка входа: Telegram bootstrap + команды
│   ├── config.py        # Конфиг (@dataclass frozen=True, load_config())
│   ├── db.py            # Инициализация SQLite (таблицы + seed)
│   ├── storage.py       # CRUD поверх БД
│   ├── knowledge.py     # Загрузка .md-файлов из knowledge/
│   ├── prompts.py       # Сборка system prompt и user prompt
│   └── llm.py           # Async-обёртка над Anthropic SDK
├── knowledge/           # Файлы знаний для контекста агентов
├── prompts/             # System prompts агентов (редактируемые)
│   ├── agent_colleague.md
│   ├── agent_analyst.md
│   └── ...
├── data/                # SQLite (в .gitignore)
├── logs/                # Лог-файлы (в .gitignore)
├── .env                 # Секреты (в .gitignore)
├── .env.example         # Шаблон переменных
├── requirements.txt     # Зависимости
├── README.md
└── CLAUDE.md            # Этот файл
```

---

## 5. АРХИТЕКТУРА СИСТЕМЫ

### Тип архитектуры

**Unified multi-agent AI operating system** на базе Claude Code.
Один связный рабочий контекст, несколько специализированных агентных ролей, общая база знаний, общие правила.

### Слои системы

```
[Telegram Group]          ← взаимодействие команды с агентами
    ↓
[Colleague / Coordinator] ← точка входа для команды / диспетчер владельца
    ↓
[Specialist Agents]       ← специализированные роли
    ↓
[Shared Knowledge]        ← .md-файлы в knowledge/
    ↓
[Prompts Layer]           ← prompts/ — редактируемые system prompts
    ↓
[Storage Layer]           ← SQLite: tasks / agent_statuses / event_logs / agent_learnings / agent_prompts
    ↓
[LLM Layer]               ← Anthropic API (async)
```

### Жёстко зафиксированные архитектурные решения

- Одна shared Claude Code среда.
- **n8n НЕ используется** как слой оркестрации.
- Code-first оркестрация — логика в Python.
- Telegram группа — основной рабочий интерфейс всей команды.
- SQLite как хранилище состояния.
- Модульный рост: один файл — одна ответственность.

---

## 6. МОДЕЛЬНАЯ СТРАТЕГИЯ

```
Sonnet 4.6  → ежедневный runtime всех агентов
Opus 4.7    → архитектура, сложный код, prompt engineering
Codex       → реализация, рефакторинг, интеграции
```

**Идентификатор runtime модели:** `claude-sonnet-4-5-20250929`
> Только полный идентификатор с датой. Alias без даты → HTTP 400.

---

## 7. БАЗА ДАННЫХ

SQLite. Пять таблиц.

### tasks
`task_id, title, status, assigned_agent, priority, source_channel, created_at, completed_at, output_summary`

**Статусы:** `created → assigned → working → waiting_input → review → completed / failed`

### agent_statuses
`agent_id, role, current_status, current_task_id, last_update_at, error_note`

**Статусы:** `idle → assigned → working → waiting_input → waiting_dependency → review → error → offline`

### event_logs
`event_id, event_type, timestamp, agent_id, task_id, source, payload_summary, severity`

### agent_learnings (самообучение)

```sql
CREATE TABLE IF NOT EXISTS agent_learnings (
    id TEXT PRIMARY KEY,
    agent_id TEXT NOT NULL,
    task_id TEXT,
    topic TEXT,
    learning TEXT NOT NULL,
    source TEXT,
    quality TEXT DEFAULT 'ok',
    created_at TEXT NOT NULL
);
```

### agent_prompts (динамические промпты)

```sql
CREATE TABLE IF NOT EXISTS agent_prompts (
    agent_id TEXT PRIMARY KEY,
    prompt TEXT NOT NULL,
    updated_at TEXT NOT NULL,
    updated_by TEXT,
    version INTEGER DEFAULT 1
);
```

**Настройки:** `journal_mode=WAL`, `foreign_keys=ON`, `row_factory=sqlite3.Row`.

---

## 8. АГЕНТНЫЕ РОЛИ

| Роль | Агент ID | Ответственность |
|---|---|---|
| **Coordinator** | `agent_coordinator` | Диспетчер владельца, утренний брифинг, маршрутизация |
| **Colleague** | `agent_colleague` | Точка входа для команды, навигация, универсальный помощник |
| **Scout** | `agent_scout` | Лидогенерация, поиск, квалификация |
| **Content Strategist** | `agent_content` | Контентная стратегия, планирование |
| **Analyst** | `agent_analyst` | Аналитика, финансовый анализ |
| **CRM Agent** | `agent_crm` | CRM-поддержка, pipeline |
| **Proposal Agent** | `agent_proposal` | КП и коммерческие предложения |
| **Tech / DevOps** | `agent_tech` | Техническая реализация, интеграции |
| **Metrics / KPI** | `agent_kpi` | Метрики, KPI, дашборды |
| **Legal & Regulatory** | `agent_legal` | Налоги, регуляторика, комплаенс |
| **Designer / Media** | `agent_designer` | Дизайн, медиа, визуальный контент |
| **Publisher** | `agent_publisher` | Публикация, распределение контента |

---

## 9. КОД: КЛЮЧЕВЫЕ МОДУЛИ

### `src/llm.py`
`async ask_claude(*, system, user, api_key, model, max_tokens) → str`
`DEFAULT_MODEL = "claude-sonnet-4-5-20250929"`
5 веток ошибок через `LLMError`. Бот никогда не падает.

### `src/storage.py`
CRUD без ORM. `db_path: Path` в каждую функцию. ID как `prefix_hex6`.

### `src/knowledge.py`
`MAX_CHARS_PER_DOC = 12_000`, `TOPIC_MAX_FILES = 6`.
Топик-маршрутизация по ключевым словам в имени файла.

### `src/main.py`
Тонкий bootstrap. Auth guard: `ADMIN_TELEGRAM_ID` + `ALLOWED_USER_IDS`.
Lifecycle: `create_task → working → LLM → completed/failed → idle`.
Агент **всегда** возвращается в `idle` — даже при ошибке.

---

## 10. БЕЗОПАСНОСТЬ

| Аспект | Реализация |
|---|---|
| Владелец | `ADMIN_TELEGRAM_ID` — полный доступ + approve sensitive задач |
| Команда | `ALLOWED_USER_IDS` — рабочие задачи через Colleague |
| Чужие | Молча игнорируются, пишется `auth_denied` в event_logs |
| API-ключ | Никогда в логах, коде, репозитории — только в `.env` |
| Stack trace | Никогда в Telegram — только через `LLMError` |
| Telegram limit | 4096 символов — обрезка при 4000 с `[...обрезано]` |

---

## 11. ТЕКУЩИЙ СТАТУС

### ✅ Готово (шаги 1–5, сессия 30 апреля 2026)
Каркас, config, db, storage, knowledge, prompts, llm, main, auth-guard, `/summary` end-to-end.

### ⏳ Блокер
Пополнение баланса API-ключа Anthropic.

### 🔜 Следующие шаги
- **Шаг 6:** `/next` и `/agent` через LLM
- **Шаг 7:** `handlers.py` + `runtime.py`
- **Шаг 8+:** динамические промпты, второй агент, Telegram группа

---

## 12. ОБЩИЕ ПРАВИЛА РАБОТЫ

**Иерархия источников правды:**
```
1. Зафиксированные решения проекта
2. Файлы в knowledge/
3. Этот CLAUDE.md
4. Последнее решение пользователя в чате
5. Общие best practices
```

Правила: структура перед реализацией · file-first · один файл — одна ответственность · спрашивай при неоднозначности · простота перед сложностью.

---

## 13. ДИАГНОСТИКА

| Проблема | Причина | Решение |
|---|---|---|
| `ModuleNotFoundError: No module named 'src'` | `python .\src\main.py` | `python -m src.main` |
| `400 invalid_request_error` | Alias без даты | `claude-sonnet-4-5-20250929` |
| `400 credit balance is too low` | Нулевой баланс | Пополнить Anthropic Console |
| `Conflict: terminated by other getUpdates` | Два экземпляра | Ctrl+C во всех, один перезапуск |
| Агент завис в `working` | Exception без cleanup | SQL UPDATE статуса вручную |

### Ручной сброс статуса агента

```python
import sqlite3
c = sqlite3.connect('data/office.db')
c.execute("""UPDATE agent_statuses
             SET current_status='idle', current_task_id=NULL, error_note=NULL
             WHERE agent_id='agent_colleague'""")
c.commit()
```

### Быстрая проверка БД

```python
import sqlite3
c = sqlite3.connect('data/office.db')
c.row_factory = sqlite3.Row
dict(c.execute("SELECT * FROM agent_statuses WHERE agent_id='agent_colleague'").fetchone())
[dict(r) for r in c.execute("SELECT event_type, severity FROM event_logs ORDER BY timestamp DESC LIMIT 5")]
```

---

## 14. ПРИНЦИПЫ КОДА

- Тонкий `main.py` — только bootstrap.
- Явная передача `db_path: Path` в каждую функцию.
- Все ошибки LLM — только через `LLMError`.
- Агент всегда возвращается в `idle` — даже при ошибке.
- Каждый agent handler изолирован — своя try/except цепочка.
- Логируй метрики, не секреты.

---

## 15. PIXEL OFFICE (финальный этап — for fun)

Pixel Office строится **В САМОМ КОНЦЕ** — после того как:
- все агенты запущены и работают стабильно в продакшне;
- все тесты пройдены;
- команда работает с системой без сбоев.

**Не возвращаться к этому разделу до финальной стабилизации проекта.**

Когда придёт время — читать в таком порядке:
```
PIXEL_OFFICE_CONCEPT.md → PIXEL_OFFICE_ARCHITECTURE.md →
PIXEL_OFFICE_ROOM_MAP.md → PIXEL_OFFICE_EVENT_MODEL.md →
PIXEL_OFFICE_STATE_SYNC.md → PIXEL_OFFICE_REFERENCES.md
```

---

### Готовые референсы — НЕ строить с нуля

Вместо разработки с нуля — взять за основу один из этих репозиториев и адаптировать под Formula Finance.

| Репозиторий | Звёзды | Что даёт | Приоритет |
|---|---|---|---|
| [paulrobello/claude-office](https://github.com/paulrobello/claude-office) | 312 | Python backend + WebSocket + TypeScript. Босс-агент, субагенты, доска задач, контекстное окно. Ближе всего к нашей архитектуре. | ⭐⭐⭐ |
| [rolandal/pixel-agents-standalone](https://github.com/rolandal/pixel-agents-standalone) | — | Форк pixel-agents как веб-приложение в браузере. localhost:3456, без VS Code. React + Canvas + WebSocket. Лучший старт для веб-версии. | ⭐⭐⭐ |
| [pablodelucca/pixel-agents](https://github.com/pablodelucca/pixel-agents) | 7 159 | VS Code расширение. Каждый агент = персонаж с анимацией. Протестировано на Windows. Редактор офиса встроен. | ⭐⭐ |
| [harishkotra/agent-office](https://github.com/harishkotra/agent-office) | — | Агенты ходят к столам, думают, выполняют задачи. Память между сессиями. | ⭐⭐ |

### Рекомендуемый стек для нашего Pixel Office

```
Backend:  Python (уже есть) + WebSocket (события из SQLite → фронтенд)
Frontend: React + Canvas 2D (на базе rolandal/pixel-agents-standalone)
Данные:   SQLite agent_statuses → WebSocket → анимация персонажей
```

### Что адаптировать под Formula Finance

- 12 персонажей = 12 агентов (Coordinator, Colleague, Analyst и др.)
- 10 комнат согласно PIXEL_OFFICE_ROOM_MAP.md
- Брендинг: тёмная тема, цвета Formula Finance
- Данные из БД: статусы агентов уже есть в `agent_statuses`

### Ключевое преимущество

Вся инфраструктура для Pixel Office **уже готова** в проекте:
- `agent_statuses` в SQLite — статусы всех агентов в реальном времени
- `event_logs` — история событий для анимации
- `agent_learnings` — активность агентов

Pixel Office = красивый фронтенд поверх того что уже работает.

---

## 16. ФАЙЛЫ ЗНАНИЙ (knowledge/)

Скопировать туда:
`CURRENT_PROJECT_STATE_SUMMARY.md`, `FIRST_AGENT_MVP_SCOPE.md`,
`FIRST_AGENT_IMPLEMENTATION_ORDER.md`, `PROJECT_FILE_READING_ORDER.md`,
`COMPANY_PROFILE.md`, `ARCHITECTURE_OVERVIEW.md`, `MODEL_STRATEGY.md`.

---

## 17. БИЗНЕС-КОНТЕКСТ FORMULA FINANCE

**Основатель:** Екатерина Кочеткова — практикующий CFO, 22 года опыта (Магнит, Соллерс, HoReCa-сети, ОАЭ/Турция).
**Слоган:** «Ваша прибыль — наш алгоритм»
**Сайт:** https://formulafinance.ru/

### Что делаем
Финансовый аудит и диагностика · управленческая отчётность и KPI · финансовое моделирование · планирование и прогнозирование · автоматизация (Bitrix24, iiko, 1C) · финансовый отдел под ключ · инвестиционный анализ · обучение и наставничество.

### HoReCa
Одно из основных направлений — 30+ кейсов. Комплексная проверка: финансы, операционные процессы, команда, юридический блок. Работаем с любыми направлениями бизнеса.

### Опыт
100+ аудитов · 73+ компании (отчётность с нуля) · 30+ компаний (автоматизация) · 20+ инвест-проектов · 12 отраслей

### Рынок
Россия + ОАЭ и Турция (с 2022).

### Типичные боли клиентов
Кассовые разрывы · низкая рентабельность · слабая отчётность · отсутствие стратегии · конфликты с регуляторами · потребность в инвестициях.

### Тон
Практичный, структурированный, спокойно-профессиональный. «Стратегия вместо шаблонов. Прозрачность и контроль.»

### Тарифы
Не в CLAUDE.md. Агенты подтягивают из `PRICING.md` по запросу.

---

## 18. НАВИГАЦИОННАЯ КАРТА ПРОЕКТА

### 🏗 Архитектура и фундамент
`PROJECT_OVERVIEW.md` · `ARCHITECTURE_OVERVIEW.md` · `MODEL_STRATEGY.md` · `AGENT_MAP.md` · `AGENT_MAP_AND_ROLES.md` · `FOLDER_STRUCTURE.md` · `PROJECT_GUIDING_PRINCIPLES.md`

### 📋 Правила работы
`SHARED_RULES.md` · `NAMING_CONVENTIONS.md` · `FILE_USAGE_RULES.md` · `TASK_ROUTING_RULES.md` · `HANDOFF_RULES.md`

### 🏢 Бизнес-контекст
`COMPANY_PROFILE.md` · `SERVICES_OVERVIEW.md` · `PRICING.md` · `POSITIONING.md` · `FAQ.md` · `CASE_LIBRARY.md` · `PROPOSAL_BLOCKS.md`

### 🎯 Продажи и CRM
`ICP_DEFINITION.md` · `LEAD_QUALIFICATION_RULES.md` · `CRM_STRUCTURE.md` · `TEMPLATE_PROPOSAL.md` · `TEMPLATE_CLIENT_BRIEF.md`

### 📊 Аналитика, KPI, отчётность
`KPI_DICTIONARY.md` · `REPORTING_STRUCTURE.md` · `TEMPLATE_REPORT.md` · `TEMPLATE_SUMMARY.md`

### ✍️ Контент и бренд
`BRAND_VOICE.md` · `CONTENT_PILLARS.md` · `CONTENT_SOURCE_LIST.md` · `AGENT_CHANNELS_AND_INTERFACES.md`

### ⚖️ Юридическое
`LEGAL_MONITORING_SOURCES.md`

### 🤖 Агенты — спецификации и файлы знаний

> Главный файл: `AGENT_MAP_AND_ROLES.md`

| Агент | agent_id | Ключевые файлы знаний |
|---|---|---|
| **Coordinator** | `agent_coordinator` | `SHARED_RULES.md`, `TASK_ROUTING_RULES.md`, `HANDOFF_RULES.md` |
| **Colleague** | `agent_colleague` | `COMPANY_PROFILE.md`, `SERVICES_OVERVIEW.md`, `FAQ.md`, `PROJECT_FILE_READING_ORDER.md` |
| **Scout** | `agent_scout` | `ICP_DEFINITION.md`, `LEAD_QUALIFICATION_RULES.md`, `CRM_STRUCTURE.md`, `CASE_LIBRARY.md` |
| **CRM Agent** | `agent_crm` | `CRM_STRUCTURE.md`, `LEAD_QUALIFICATION_RULES.md`, `TEMPLATE_CLIENT_BRIEF.md` |
| **Proposal Agent** | `agent_proposal` | `PROPOSAL_BLOCKS.md`, `TEMPLATE_PROPOSAL.md`, `PRICING.md`, `CASE_LIBRARY.md` |
| **Analyst** | `agent_analyst` | `KPI_DICTIONARY.md`, `REPORTING_STRUCTURE.md`, `TEMPLATE_REPORT.md` |
| **Metrics / KPI** | `agent_kpi` | `KPI_DICTIONARY.md`, `REPORTING_STRUCTURE.md`, `TEMPLATE_REPORT.md` |
| **Legal** | `agent_legal` | `LEGAL_MONITORING_SOURCES.md`, `TEMPLATE_SUMMARY.md` |
| **Content** | `agent_content` | `CONTENT_PILLARS.md`, `BRAND_VOICE.md`, `POSITIONING.md`, `CASE_LIBRARY.md` |
| **Publisher** | `agent_publisher` | `BRAND_VOICE.md`, `CONTENT_PILLARS.md`, `TEMPLATE_SUMMARY.md` |
| **Tech / DevOps** | `agent_tech` | `ARCHITECTURE_OVERVIEW.md`, `MODEL_STRATEGY.md`, `ENV_VARIABLES_SPEC.md` |
| **Designer** | `agent_designer` | `BRAND_VOICE.md`, `POSITIONING.md`, `CONTENT_PILLARS.md` |

### 🤖 Первый агент (Colleague)
`FIRST_AGENT_MVP_SCOPE.md` · `FIRST_AGENT_IMPLEMENTATION_ORDER.md` · `FIRST_AGENT_BUILD_PLAN.md` · `2__FIRST_AGENT_SYSTEM_PROMPT.md` · `1__TELEGRAM_BOT_COMMAND_SPEC.md` · `PROJECT_FOLDER_LOADING_RULES.md` · `PROJECT_FILE_READING_ORDER.md`

### 🔧 Технический стек и деплой
`TELEGRAM_INTEGRATION_OVERVIEW.md` · `ENV_VARIABLES_SPEC.md` · `FIRST_DATABASE_SCHEMA.md` · `FIRST_AGENT_RUNTIME_LOOP.md` · `BOT_MESSAGE_FLOW.md` · `TASK_AND_STATUS_STORAGE_MODEL.md` · `ERROR_HANDLING_AND_LOGGING.md` · `DOCKER_COMPOSE_FIRST_SETUP.md` · `BEGINNER_SERVER_STEP_BY_STEP.md` · `FIRST_DEPLOY_CHECKLIST.md` · `SERVER_DEPLOYMENT_BLUEPRINT.md` · `MCP_AND_API_CONNECTION_MAP.md` · `SECURITY_AND_ACCESS_CONTROL.md`

### 🎮 Pixel Office
`PIXEL_OFFICE_CONCEPT.md` · `PIXEL_OFFICE_ARCHITECTURE.md` · `PIXEL_OFFICE_ROOM_MAP.md` · `PIXEL_OFFICE_AGENT_STATUSES.md` · `PIXEL_OFFICE_EVENT_MODEL.md` · `PIXEL_OFFICE_EVENT_ENVELOPE.md` · `PIXEL_OFFICE_JSON_SCHEMA.md` · `PIXEL_OFFICE_UI_PANELS.md` · `PIXEL_OFFICE_STATE_SYNC.md` · `PIXEL_OFFICE_REFERENCES.md`

### 📈 Статус и roadmap
`CURRENT_PROJECT_STATE_SUMMARY.md` · `IMPLEMENTATION_PHASES.md` · `STAGED_IMPLEMENTATION_STRATEGY.md` · `FUTURE_ROADMAP.md` · `FINAL_PROJECT_INDEX.md` · `BUILD_SESSION_REPORT.md`

### 📄 Шаблоны
`TEMPLATE_MEETING_NOTE.md` · `TEMPLATE_SUMMARY.md` · `TEMPLATE_REPORT.md` · `TEMPLATE_PROPOSAL.md` · `TEMPLATE_CLIENT_BRIEF.md`

---

## 19. АГЕНТЫ: ПРОМПТЫ, СКИЛЛЫ И САМООБУЧЕНИЕ

### А. ДИНАМИЧЕСКИЕ ПРОМПТЫ (Вариант В — зафиксированное решение)

**Архитектура:** Telegram для скорости + файл для надёжности.

```
/set_prompt colleague [текст]
    ↓
Сохраняется в БД (agent_prompts) + в файл prompts/agent_colleague.md
    ↓
При перезапуске бот читает файл → промпт не теряется никогда
```

**Команды управления промптами (только для ADMIN):**

| Команда | Действие |
|---|---|
| `/set_prompt [agent_id] [текст]` | Обновить промпт агента на лету |
| `/get_prompt [agent_id]` | Показать текущий активный промпт |
| `/reset_prompt [agent_id]` | Вернуть базовый промпт из `prompts/` |
| `/prompt_history [agent_id]` | Показать последние 5 версий промпта |

**Логика загрузки промпта (приоритет):**
```
1. БД (agent_prompts) — если есть обновлённая версия
2. prompts/agent_{id}.md — файл на диске
3. Встроенный базовый промпт из prompts.py — fallback
```

**Реализация в `src/prompts.py`:**
```python
def load_agent_prompt(db_path, agent_id, prompts_dir) -> str:
    # 1. Попытка из БД
    prompt = get_agent_prompt_from_db(db_path, agent_id)
    if prompt:
        return prompt
    # 2. Попытка из файла
    prompt_file = prompts_dir / f"agent_{agent_id}.md"
    if prompt_file.exists():
        return prompt_file.read_text(encoding="utf-8")
    # 3. Fallback — базовый промпт
    return DEFAULT_PROMPTS.get(agent_id, DEFAULT_SYSTEM_PROMPT)
```

---

### Б. ПАТТЕРН САМООБУЧЕНИЯ (все агенты)

Основан на ACE-loop (Agentic Context Engineering, arXiv 2025):
**Generator → Reflector → Curator → Memory Injection** (+10.6% benchmark).

```
BEFORE task:  load_relevant_learnings(agent_id, topic) → inject как <past_learnings>
AFTER task:   Reflector: "Что сработало? Что нет?" → save_learning()
ПЕРИОДИЧЕСКИ: Curator: обобщить 10 уроков → update knowledge/learnings_{agent_id}.md
```

**Правила:** агент НЕ меняет промпт сам · уроки в БД и файл · human review раз в неделю · критические паттерны → Coordinator.

---

### В. GITHUB SKILLS ПО АГЕНТАМ

#### Универсальные (все агенты)
`obra/systematic-debugging` · `Piebald-AI/claude-code-system-prompts` (memory synthesis) · `ComposioHQ/awesome-claude-skills` (prompt engineering) · локальные: brainstorming, verification, writing-plans

#### Специфические

| Агент | Скиллы | Источник |
|---|---|---|
| **Colleague** | Personal assistant, daily briefing | `OpenPaw` via `npx pawmode` |
| **Analyst / KPI** | CFO advisory, FP&A mentor | `alirezarezvani/claude-skills` |
| **Scout / CRM** | Sales agent, lead scoring | `wondelai/skills`, `@clawfu/mcp-skills` |
| **Proposal** | Copywriting, Hormozi, Cialdini | `wondelai/skills` → marketing/CRO |
| **Content** | Ogilvy, Cialdini, Schwartz (169 skills) | `@clawfu/mcp-skills` |
| **Legal** | Compliance checklists | `alirezarezvani/claude-skills` |
| **Tech** | TDD, subagents, security | `obra/superpowers`, `trailofbits/` |
| **Publisher** | Humanizer (37 AI patterns) | `rohitg00/awesome-claude-code-toolkit` |

---

### Г. БАЗОВЫЕ SYSTEM PROMPTS

> Формат: Role → Context → Rules → Output → Memory Hook.
> Загружаются из `prompts/`. Редактируются через `/set_prompt` в Telegram.

---

#### COORDINATOR
```
You are the Coordinator of Formula Finance AI Office.
Route tasks, track priorities, prevent chaos. Do NOT do specialist work.

Company: FormulaFinance — financial consulting, CFO-as-a-service, Russia + UAE/Turkey.

Rules:
- Task received → identify right agent → route it.
- Unclear → ask ONE question, then route.
- Multiple agents needed → sequence explicitly.
- Morning briefing: collect all agent statuses → send summary to owner.
- Never absorb specialist work. Always delegate.

Output: ROUTE TO / TASK / PRIORITY / DEPENDENCY / HUMAN NEEDED

Memory: Review <past_learnings> before complex routing.
```

---

#### COLLEAGUE
```
You are Colleague — internal assistant and team entry point for Formula Finance.

All team members (not only the owner) talk to you first.
You route their requests to the right specialist agent.

Company: FormulaFinance — «Ваша прибыль — наш алгоритм».
Founder: Екатерина Кочеткова, CFO, 22 years experience.

Rules:
- Team members → you understand their request → route to right agent.
- Answer general questions from knowledge files. Never invent facts.
- Communicate in the same language as the user (RU/EN).
- Be concise. Business tone. No fluff.
- Do NOT do specialist work (legal, KPI, proposals, code).

Output: direct answer → source file → suggested next step OR route to agent.

Memory: Load <past_learnings>. Note what routing patterns work best.
```

---

#### SCOUT
```
You are Scout — lead generation agent of Formula Finance.
Target: businesses needing financial clarity. HoReCa is a strong vertical.
ICP: real revenue, growing complexity, weak financial visibility.

Rules: Match ICP. Structure every lead. Never contact anyone — only research.

Output per lead: Company / Industry / Pain signal / ICP fit / Source / Action

Memory: Track which industries convert best.
```

---

#### CRM AGENT
```
You are CRM Agent — commercial memory of Formula Finance.
Stages: Lead → Qualified → Brief → Proposal → Negotiation → Won/Lost/Hold

Rules: Every lead has a stage + next action + date. Flag stuck > 14 days.

Output: Lead / Stage / Last action / Next action / Risk flag

Memory: Track which transitions take longest. Update after Won/Lost.
```

---

#### PROPOSAL AGENT
```
You are Proposal Agent — commercial offer specialist of Formula Finance.
Tone: practical, structured, calm. No hype.
Pricing: load from PRICING.md on demand.

Rules:
- Start with CLIENT'S pain, not our services.
- Use PROPOSAL_BLOCKS.md and CASE_LIBRARY.md.
- HoReCa: lead with 30+ cases credibility.
- End with clear next step.

Output: Ситуация → Проблема → Решение → Этапы → Результат → Следующий шаг.

Memory: Track which structures get accepted. Which cases resonate per industry.
```

---

#### ANALYST
```
You are Analyst — structured reasoning agent. You interpret, not just list.

Rules:
- Every analysis ends: "What does this mean for the business?"
- Label: facts vs inferences vs assumptions.
- Financial analysis: always consider liquidity, profitability, risk.

Output: Context / Findings / Interpretation / Risks / Recommendation

Memory: Track frameworks that work best per business type.
```

---

#### METRICS / KPI AGENT
```
You are Metrics/KPI Agent — measurement system designer.
Every KPI: name, formula, source, frequency, owner.
HoReCa KPIs: food cost %, labor cost %, table turnover, revenue/seat.
Ask always: "What decision will this metric enable?"

Output: Group / KPI / Formula / Source / Frequency / Owner / Alert threshold

Memory: Track which KPIs clients find useful. Track what gets ignored.
```

---

#### LEGAL & REGULATORY ADVISOR
```
You are Legal & Regulatory Advisor of Formula Finance.
Focus: Russian tax law, ФНС, ФСБУ, employment law, UAE/Turkey basics, HoReCa licensing.

Rules: Cite source + date. Confirm/draft/rumor. Rate impact. Plain language.
Never definitive conclusions — recommend professional review.
Escalate critical → Coordinator immediately.

Output: Topic / Source + date / Status / Impact / Business meaning / Action

Memory: Track which areas generate most alerts. Track which led to action.
```

---

#### CONTENT STRATEGIST
```
You are Content Strategist of Formula Finance.
Voice: structured, intelligent, practical, calm. Never hyped.
Audience: business owners, CEOs, CFOs needing financial clarity.

Rules: Every idea connects to real client pain. Use CONTENT_PILLARS.md.
HoReCa content: leverage 30+ cases credibility.

Output: Theme / Pain / Format / Channel / Hook / CTA

Memory: Track which themes generate leads. Track best formats per channel.
```

---

#### PUBLISHER
```
You are Publisher — content release specialist of Formula Finance.

Rules: Adapt per channel (Telegram ≠ LinkedIn ≠ website).
Remove AI patterns: vary sentence length, lead with most interesting point.
Telegram: max 1000 chars. Emoji sparingly. Never publish without approval.

Output: Channel / Ready text / Hashtags / Best time / Approval status

Memory: Track best response per format and channel.
```

---

#### TECH / DEVOPS AGENT
```
You are Tech/DevOps Agent — engineering layer of Formula Finance AI Office.
Stack: Python 3.12, PTB 21.10, anthropic 0.49.0, SQLite. No n8n.
Priority: Clarity → Simplicity → Scalability → Maintainability → Control.

Rules:
- Read existing code before writing new code.
- Run: python -m src.main (never python src/main.py).
- Secrets NEVER in code or logs.
- Plan before implementing: assumptions → plan → confirm → execute.

Output: Problem / Approach / Files affected / Risks / Test

Memory: Track failure modes and fixes. Track architectural decisions + WHY.
```

---

#### DESIGNER / MEDIA AGENT
```
You are Designer/Media Agent of Formula Finance.
Brand: dark, structured, financial. Clean lines. Trust through clarity.

Rules: Every visual serves communication. No hype, no clutter.
Data viz should simplify, not impress.

Output: Purpose / Format / Visual concept / Brand check

Memory: Track which formats get best response.
```

---

## 20. OPERATIONS PLAYBOOK И MULTI-USER МОДЕЛЬ

### А. МОДЕЛЬ ДОСТУПА (два уровня)

```
OWNER (ADMIN_TELEGRAM_ID = владелец)
├── Полный доступ ко всем агентам
├── Команды /set_prompt, /reset_prompt, /approve, /reject
├── Утренний брифинг от Coordinator
└── Прямое обращение к любому агенту

TEAM (ALLOWED_USER_IDS = сотрудники, 2-3 человека)
├── Обращаются к Colleague — он маршрутизирует
├── Получают результат в группе
└── Не имеют доступа к настройке системы
```

### Б. TELEGRAM ГРУППА — МОДЕЛЬ РАБОТЫ

```
[Formula Finance AI Office — Telegram Group]

Сотрудник → пишет Colleague (на RU или EN)
           → Colleague понимает задачу
           → маршрутизирует нужному агенту
           → возвращает результат в группу

Владелец  → может писать любому агенту напрямую
           → может запросить брифинг: /brief или "дай брифинг на сегодня"
           → Coordinator собирает статусы + задачи → отправляет сводку
```

**Важно для настройки группы:**
- В BotFather: `/setprivacy` → `Disable` (иначе бот не видит сообщения в группе)
- Бот добавляется в группу как Admin
- Сотрудники пишут свободным текстом — не нужны команды со слешем

### В. УТРЕННИЙ БРИФИНГ

Брифинг — по запросу владельца, не по расписанию.
```
Владелец: /brief
Coordinator: собирает статусы агентов + активные задачи + приоритеты дня
           → отправляет структурированную сводку
```
Токены тратятся только в момент запроса — фоновой активности нет.

### Г. ЭТАПЫ ЗАПУСКА

```
Этап 1 — Локально, только владелец
└── Запуск агентов, тестирование, правка промптов через /set_prompt

Этап 2 — Локально + команда (2-3 человека)
└── Совместное тестирование, отлов багов
└── Бот работает в рабочие часы (команда предупреждена)
└── Критерии перехода: см. секцию 21

Этап 3 — Переезд на VPS
└── Только после стабильной недели на Этапе 2
└── Бот работает 24/7, 365 дней

Этап 4 — Pixel Office
└── Только после того как вся система стабильна без сбоев
```

### Д. ДОБАВЛЕНИЕ НОВОГО ПОЛЬЗОВАТЕЛЯ

```
[ ] Получить Telegram ID
[ ] Добавить в ALLOWED_USER_IDS в .env через запятую
[ ] Перезапустить бота: Ctrl+C → python -m src.main
[ ] Пользователь пишет /start в группу
[ ] Проверить в логах: нет auth_denied для этого ID
```

### Е. ДОБАВЛЕНИЕ НОВОГО АГЕНТА (чеклист)

```
[ ] 1. Написать system prompt → сохранить в prompts/agent_{id}.md
[ ] 2. Создать knowledge/learnings_{agent_id}.md (пустой)
[ ] 3. Добавить agent_id в seed db.py
[ ] 4. Создать handler в main.py / handlers.py
[ ] 5. Добавить топик в knowledge.py (_TOPIC_KEYWORDS)
[ ] 6. Добавить routing в Colleague (он знает про нового агента)
[ ] 7. Протестировать: задача → статус working → idle в БД
[ ] 8. Проверить изоляцию: падение нового не роняет других
[ ] 9. Обновить секции 8 и 18 в CLAUDE.md
[ ] 10. Зафиксировать в BUILD_SESSION_REPORT.md
```

### Ж. ЕЖЕДНЕВНАЯ И ЕЖЕНЕДЕЛЬНАЯ ПРОВЕРКА

**Ежедневно (2 мин):**
```
/status → агент отвечает?
Логи → нет ERROR?
agent_statuses → все в idle?
```

**Еженедельно (15 мин):**
```
knowledge/learnings_*.md → просмотр уроков, удаление дублей
event_logs → повторяющиеся ошибки?
prompts/ → актуальны ли промпты?
CLAUDE.md → нужны ли обновления?
BUILD_SESSION_REPORT.md → зафиксированы ли решения?
```

---

## 21. ТИПОВЫЕ ОТКАЗЫ И ОПЕРАТИВНЫЕ РЕШЕНИЯ

### А. КАРТА ОТКАЗОВ

#### LLM / Anthropic API

| Симптом | Причина | Решение | Время |
|---|---|---|---|
| `400 credit balance too low` | Нулевой баланс | Пополнить Anthropic Console | 5 мин |
| `400 invalid_request_error` | Неверный model ID | `claude-sonnet-4-5-20250929` в llm.py | 2 мин |
| `401 AuthenticationError` | Неверный API ключ | Проверить `.env` | 2 мин |
| `429 RateLimitError` | Слишком много запросов | Подождать 60 сек + retry с backoff | 1 мин |
| Пустой ответ модели | Контекст слишком большой | Уменьшить MAX_CHARS_PER_DOC | 5 мин |
| Ответ невпопад | Промпт деградировал | `/get_prompt` → проверить → `/set_prompt` | 15 мин |

#### Telegram / Сеть

| Симптом | Причина | Решение | Время |
|---|---|---|---|
| `TimedOut: Pool timeout` | Connection pool исчерпан | Добавить `pool_timeout` в ApplicationBuilder | 10 мин |
| Бот не видит сообщения в группе | Privacy mode включён | BotFather: `/setprivacy` → Disable | 2 мин |
| `Conflict: terminated by other getUpdates` | Два экземпляра | Ctrl+C везде → один перезапуск | 1 мин |
| Сообщения теряются при перезапуске | Pending updates | `drop_pending_updates=True` при старте | 5 мин |

#### State / База данных

| Симптом | Причина | Решение | Время |
|---|---|---|---|
| Агент завис в `working` | Exception без cleanup | SQL UPDATE вручную (см. секцию 13) | 2 мин |
| `database is locked` | Два процесса пишут | WAL включён. Проверить второй процесс | 5 мин |
| Промпт слетел после перезапуска | Хранился только в памяти | Вариант В: всегда БД + файл | — |
| Схема БД устарела | Код обновился | Добавить таблицу вручную или пересоздать | 15 мин |

#### Knowledge / Промпты

| Симптом | Причина | Решение | Время |
|---|---|---|---|
| Агент без контекста проекта | `knowledge/` пуста | Скопировать `.md` файлы | 5 мин |
| Файл не загружается | Encoding / имя файла | UTF-8, Latin имена файлов | 10 мин |
| Промпт не применился | Не сохранился в файл | Проверить `prompts/agent_{id}.md` | 5 мин |

### Б. ИЗОЛЯЦИЯ АГЕНТОВ — КРИТИЧЕСКИ ВАЖНО

Каждый agent handler — своя try/except цепочка:

```python
async def cmd_analyst(update, context):
    cfg = _cfg(context)
    try:
        # работа агента analyst
        ...
    except LLMError as e:
        await update.message.reply_text(f"❌ Analyst: {e}")
        update_agent_status(cfg.db_path, "agent_analyst", "idle")
    except Exception as e:
        logger.exception("[analyst] unexpected failure")
        await update.message.reply_text("❌ Внутренняя ошибка Analyst.")
        update_agent_status(cfg.db_path, "agent_analyst", "idle")
    # agent_colleague продолжает работать независимо ✅
```

**Правило:** падение одного агента = только его статус `error` → `idle`. Остальные работают.

### В. КРИТЕРИИ ПЕРЕХОДА МЕЖДУ ЭТАПАМИ

#### Этап 1 → Этап 2

```
✅ 3+ агента стабильно работают 7 дней подряд
✅ Все категории отказов из секции 21 протестированы вручную
✅ Для каждого отказа: процедура восстановления < 5 мин
✅ Падение одного агента не роняет других — проверено
✅ /set_prompt и /get_prompt работают корректно
✅ Логи читаемы и информативны
✅ BUILD_SESSION_REPORT.md обновлён
```

#### Этап 2 → Этап 3 (VPS)

```
✅ Команда работала с системой неделю без помощи владельца
✅ Нет критических падений за 7 дней
✅ ALLOWED_USER_IDS настроен и протестирован
✅ Privacy mode отключён в BotFather
✅ Backup отработан минимум 1 раз
✅ Git репозиторий актуален
```

### Г. МОНИТОРИНГ НА VPS

После переезда добавить `systemd` автоперезапуск:

```ini
[Unit]
Description=Formula Finance AI Office Bot
After=network.target

[Service]
WorkingDirectory=/home/user/formula-finance-ai-office
ExecStart=/home/user/formula-finance-ai-office/.venv/bin/python -m src.main
Restart=always
RestartSec=10
EnvironmentFile=/home/user/formula-finance-ai-office/.env

[Install]
WantedBy=multi-user.target
```

Это решает 80% проблем автоматически без участия человека.

---

## 22. GIT WORKFLOW

### Первоначальная настройка (один раз)

```powershell
cd C:\Users\Gammo\Desktop\formula-finance-ai-office
git init
git add .
git commit -m "initial: Formula Finance AI Office baseline"
# Создать приватный репозиторий на GitHub
git remote add origin https://github.com/{username}/formula-finance-ai-office.git
git push -u origin main
```

### Правила работы с Git

```
НИКОГДА не коммитить: .env, data/*.db, logs/
ВСЕГДА проверять: git status перед коммитом
ВСЕГДА работать: в feature ветке для новых агентов/фич
ВСЕГДА писать: понятный commit message
```

### Стандартный workflow

```powershell
# Новая фича / агент
git checkout -b feature/agent-analyst

# Работа...

# Коммит
git add src/
git commit -m "feat: add analyst agent with LLM integration"

# Merge в main после тестирования
git checkout main
git merge feature/agent-analyst
git push origin main
```

### Формат commit messages

```
feat: добавить нового агента Analyst
fix: исправить зависание агента в статусе working
prompt: обновить system prompt для Colleague
docs: обновить CLAUDE.md секция 21
refactor: выделить handlers.py из main.py
```

### Что в .gitignore (обязательно)

```
.env
data/
logs/
__pycache__/
.venv/
*.pyc
```

### При работе с разработчиком

```
1. Дать доступ к GitHub репозиторию (Settings → Collaborators)
2. Разработчик делает git clone
3. Создаёт свою ветку
4. Pull Request → ты ревьюишь → merge
```

---

## 23. ROADMAP ЭТАПОВ

```
ЭТАП 1 — Локально, только владелец
├── Шаг 6:  /next и /agent через LLM
├── Шаг 7:  handlers.py + runtime.py
├── Шаг 8:  динамические промпты (/set_prompt, /get_prompt)
├── Шаг 9:  таблица agent_learnings (самообучение)
├── Шаг 10: второй агент (Analyst или KPI)
├── Шаг 11: третий агент (CRM или Scout)
└── Критерий выхода: 3+ агента стабильно 7 дней

ЭТАП 2 — Локально + команда (2-3 человека)
├── Telegram группа + Privacy mode off
├── ALLOWED_USER_IDS в .env
├── Colleague как точка входа для команды
├── Coordinator + утренний брифинг
└── Критерий выхода: команда неделю без помощи владельца

ЭТАП 3 — VPS (24/7)
├── git clone на сервер
├── systemd автоперезапуск
├── Backup автоматизация
└── Все оставшиеся агенты

ЭТАП 4 — Pixel Office (for fun)
└── Только после полной стабилизации Этапа 3
```

---

*Версия: 1 мая 2026 — финальная сборка.*
*Следующий шаг: Шаг 6 — /next и /agent через LLM + Git инициализация.*
