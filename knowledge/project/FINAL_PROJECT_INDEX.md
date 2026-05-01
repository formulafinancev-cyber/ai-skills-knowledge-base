# FINAL PROJECT INDEX

## Purpose
This file is the top-level index for the Formula Finance AI Office project.

Its purpose is to show:
- what exists in the project;
- where to look for specific topics;
- what is MVP-critical vs. future expansion.

## Main Principle
Always start from this index when a new model or a new human opens the project.

## 1. Project Overview & Identity

These files answer “что это вообще за проект”:

- COMPANY_PROFILE.md  
- SERVICES_OVERVIEW.md  
- POSITIONING.md  
- FORMULA_FINANCE_PROJECT_INDEX.txt  
- CURRENT_PROJECT_STATE_SUMMARY.md  

Use these first to understand:
- кто такая Formula Finance;
- какие услуги и продукты уже описаны;
- что уже сделано в этом репозитории.

## 2. Pixel Office Concept Layer

These files define the visual “AI‑офис” концепт:

- PIXEL_OFFICE_CONCEPT.md  
- PIXEL_OFFICE_ARCHITECTURE.md  
- PIXEL_OFFICE_ROOM_MAP.md  
- PIXEL_OFFICE_AGENT_STATUSES.md  
- PIXEL_OFFICE_EVENT_MODEL.md  
- PIXEL_OFFICE_EVENT_ENVELOPE.md  
- PIXEL_OFFICE_JSON_SCHEMA.md  
- PIXEL_OFFICE_UI_PANELS.md  
- PIXEL_OFFICE_STATE_SYNC.md  
- PIXEL_OFFICE_REFERENCES.md  
- EXTERNAL_PIXEL_OFFICE_LINKS.md  

Read these when:
- нужно понимать визуальный офис;
- нужен event‑driven подход и синхронизация состояния;
- проект идёт дальше MVP бота к визуальному контрол-руму.

## 3. Agent System & Roles

These files описывают роли и этапы внедрения агентов:

- AGENT_MAP_AND_ROLES.md  
- IMPLEMENTATION_PHASES.md  
- FIRST_AGENT_BUILD_PLAN.md  
- FIRST_AGENT_MVP_SCOPE.md  
- FIRST_AGENT_IMPLEMENTATION_ORDER.md  

Use these when:
- нужно понять, какие агенты планируются;
- что именно делает первый агент (Colleague);
- в каком порядке вообще эволюционирует система.

## 4. Telegram & First Agent Behavior

Эти файлы описывают интерфейс и поведение первого агента:

- TELEGRAM_INTEGRATION_OVERVIEW.md  
- TELEGRAM_BOT_COMMAND_SPEC.md  
- FIRST_AGENT_SYSTEM_PROMPT.md  
- PROJECT_FOLDER_LOADING_RULES.md  
- PROJECT_FILE_READING_ORDER.md  

Use these when:
- вопрос про команды бота;
- как агент читает папку проекта;
- как ограничен контекст, чтобы не перегружать модель.

## 5. Runtime, Storage & Flow

Эти файлы описывают живой цикл работы и хранение состояния:

- TASK_AND_STATUS_STORAGE_MODEL.md  
- FIRST_DATABASE_SCHEMA.md  
- BOT_MESSAGE_FLOW.md  
- FIRST_AGENT_RUNTIME_LOOP.md  
- ERROR_HANDLING_AND_LOGGING.md  
- ENV_VARIABLES_SPEC.md  

Use these when:
- вопрос про то, как устроен runtime;
- как хранятся задачи и статусы;
- как устроены ошибки и логи.

## 6. Deployment & Operations

Эти файлы описывают первый deploy и эксплуатацию:

- SERVER_DEPLOYMENT_BLUEPRINT.md  
- BEGINNER_SERVER_STEP_BY_STEP.md  
- DOCKER_COMPOSE_FIRST_SETUP.md  
- FIRST_DEPLOY_CHECKLIST.md  

Use these when:
- нужно поднять первый рабочий контур;
- настроить VPS, Docker, Compose;
- проверить, что всё запускается и рестартится.

## 7. Integration & APIs

These files описывают внешние соединения:

- MCP_AND_API_CONNECTION_MAP.md  

Use this when:
- нужно понять, какие внешние интеграции планируются;
- какие MCP/API нужны и зачем;
- что точно не надо подключать в MVP.

## 8. How To Read This Project (For Models)

When a model starts working with this repository, recommended order is:

1. FINAL_PROJECT_INDEX.md  
2. CURRENT_PROJECT_STATE_SUMMARY.md  
3. FIRST_AGENT_MVP_SCOPE.md  
4. FIRST_AGENT_IMPLEMENTATION_ORDER.md  
5. PROJECT_FILE_READING_ORDER.md  

Then:
- для Telegram‑вопросов → раздел 4;
- для runtime/storage → раздел 5;
- для deploy → раздел 6;
- для Pixel Office и визуализации → раздел 2;
- для архитектуры агентов в целом → раздел 3.

## 9. MVP vs. Future Expansion

### MVP-Critical Files
These are required to build and run the first working bot:

- FIRST_AGENT_MVP_SCOPE.md  
- FIRST_AGENT_IMPLEMENTATION_ORDER.md  
- TELEGRAM_BOT_COMMAND_SPEC.md  
- FIRST_AGENT_SYSTEM_PROMPT.md  
- PROJECT_FOLDER_LOADING_RULES.md  
- PROJECT_FILE_READING_ORDER.md  
- TASK_AND_STATUS_STORAGE_MODEL.md  
- FIRST_DATABASE_SCHEMA.md  
- BOT_MESSAGE_FLOW.md  
- FIRST_AGENT_RUNTIME_LOOP.md  
- ERROR_HANDLING_AND_LOGGING.md  
- ENV_VARIABLES_SPEC.md  
- DOCKER_COMPOSE_FIRST_SETUP.md  
- BEGINNER_SERVER_STEP_BY_STEP.md  
- FIRST_DEPLOY_CHECKLIST.md  

### Future-Oriented Files
These are **not обязателеньны** для первого запуска бота, но важны для дальнейшего развития:

- Pixel Office full layer files  
- AGENT_MAP_AND_ROLES.md  
- IMPLEMENTATION_PHASES.md  
- MCP_AND_API_CONNECTION_MAP.md  
- FIRST_AGENT_BUILD_PLAN.md  

## Final Principle
This index is the single source of truth for “что уже есть в проекте и где это лежит”.

Любой новый файл должен:
- вписываться в один из разделов выше;
- иметь понятную роль;
- не дублировать уже существующее.