---
name: master-router
description: >
  ЧИТАТЬ ПЕРВЫМ в каждом чате. Маршрутизатор скиллов — определяет какой скилл
  загрузить для текущей задачи. Триггер: начало любого чата, или когда задача
  не покрыта текущим контекстом.
---

# Master Router

> **Инструкция:** Прочитай задачу пользователя → найди совпадение в таблице ниже → вызови `view` на указанный SKILL.md → только потом начинай работу.
> Если задача сложная — загружай несколько скиллов последовательно.

---

## 🏭 FFA / HoReCa (основной контекст)

| Задача | Скилл | Путь |
|--------|-------|------|
| Разработка FFA, GAS, Google Apps Script | `agency-agents` | `/mnt/skills/user/agency-agents/SKILL.md` |
| Аудит / ревью FFA кода | `agency-agents` + `code-review-excellence` | оба |
| BDR, iiko, P&L, Cash Flow, KPI | `agency-agents` + `ar-finance` | оба |
| CFO/CEO отчётность, управленческий учёт | `ar-finance` + `ar-c-level-advisor` | оба |
| HoReCa операционная аналитика | `ar-finance` + `ar-engineering` | оба |
| Дашборд / HTML отчёт / визуализация данных | `gb-tufte-report` | `/mnt/skills/user/gb-tufte-report/SKILL.md` |
| Прогнозирование, ML, статистика | `jf-ml-pipeline` + `ar-engineering` | оба |

---

## 💻 Разработка (General)

| Задача | Скилл | Путь |
|--------|-------|------|
| Планирование фичи (до написания кода) | `brainstorming` → `writing-plans` | последовательно |
| Написание плана реализации | `writing-plans` | `/mnt/skills/user/writing-plans/SKILL.md` |
| Выполнение плана по шагам | `executing-plans` | `/mnt/skills/user/executing-plans/SKILL.md` |
| TDD, тест-driven разработка | `gb-tdd` + `test-driven-development` | оба |
| Дебаггинг, поиск бага | `systematic-debugging` + `jf-debugging-wizard` | оба |
| Code review, ревью PR | `code-review-excellence` + `code-review-pr` | оба |
| Рефакторинг, легаси-код | `jf-legacy-modernizer` | `/mnt/skills/user/jf-legacy-modernizer/SKILL.md` |
| Написание скилла / агента | `gb-skill-studio` + `skillforge` | оба |
| Верификация перед завершением | `verification-before-completion` | `/mnt/skills/user/verification-before-completion/SKILL.md` |

---

## 🐍 Python

| Задача | Скилл |
|--------|-------|
| Python разработка | `jf-python-pro` |
| pandas, DataFrame, анализ данных | `jf-pandas-pro` + `csv-data-summarizer` |
| FastAPI | `jf-fastapi-expert` |
| Django | `jf-django-expert` |
| ML pipeline | `jf-ml-pipeline` |
| RAG, векторные БД | `jf-rag-architect` |

---

## 🌐 JavaScript / TypeScript / Frontend

| Задача | Скилл |
|--------|-------|
| TypeScript | `jf-typescript-pro` |
| JavaScript | `jf-javascript-pro` |
| React | `jf-react-expert` |
| Vue | `jf-vue-expert` |
| Next.js | `jf-nextjs-developer` |
| NestJS | `jf-nestjs-expert` |
| GraphQL | `jf-graphql-architect` |
| WebSocket | `jf-websocket-engineer` |
| UI/UX дизайн | `interface-design` |

---

## 🗄️ Базы данных

| Задача | Скилл |
|--------|-------|
| SQL запросы, оптимизация | `jf-sql-pro` + `jf-database-optimizer` |
| PostgreSQL | `jf-postgres-pro` + `postgres` |
| Схема, архитектура БД | `jf-database-optimizer` |

---

## ☁️ DevOps / Инфраструктура

| Задача | Скилл |
|--------|-------|
| DevOps общее | `jf-devops-engineer` |
| Kubernetes | `jf-kubernetes-specialist` |
| Terraform | `jf-terraform-engineer` + `hashicorp-terraform` |
| Мониторинг, алертинг | `jf-monitoring-expert` |
| SRE, надёжность | `jf-sre-engineer` |
| Безопасность кода | `jf-secure-code-guardian` + `jf-security-reviewer` |

---

## 🏗️ Архитектура

| Задача | Скилл |
|--------|-------|
| Системная архитектура | `jf-architecture-designer` + `jf-microservices-architect` |
| API дизайн | `jf-api-designer` |
| Облачная архитектура | `jf-cloud-architect` |
| MCP сервер | `jf-mcp-developer` + `claude-api` |

---

## 📊 Данные / Аналитика

| Задача | Скилл |
|--------|-------|
| Анализ CSV / табличных данных | `csv-data-summarizer` + `jf-pandas-pro` |
| D3.js визуализация | `d3js-skill` |
| Spark, Big Data | `jf-spark-engineer` |
| Исследование / research | `deep-research` + `gb-firecrawl-research` |
| Академический ресёрч | `ai-research-skills` |

---

## 🤖 AI / Агенты

| Задача | Скилл |
|--------|-------|
| Prompt engineering | `jf-prompt-engineer` + `prompt-master` |
| Fine-tuning модели | `jf-fine-tuning-expert` |
| RAG система | `jf-rag-architect` |
| Параллельные агенты | `dispatching-parallel-agents` |
| Субагентная разработка | `subagent-driven-development` |

---

## 📋 Проектное управление

| Задача | Скилл |
|--------|-------|
| PM, планирование эпиков | `ar-project-management` + `know-ccpm` |
| Ретроспектива | `gb-lab-retro` |
| Принятие решений | `gb-decision-toolkit` |
| JTBD анализ | `gb-jtbd` |
| Стратегия бизнеса | `ar-business-growth` + `minimalist-entrepreneur` |

---

## ✍️ Контент / Документация

| Задача | Скилл |
|--------|-------|
| Документация кода | `jf-code-documenter` + `doc-coauthoring` |
| Написание скилла | `writing-skills` + `gb-skill-studio` |
| Контент маркетинг | `content-research-writer` + `marketing-skills` |
| Презентация / слайды | `gb-presentation-generator` + `revealjs` |
| Убрать AI-стиль из текста | `humanizer` |

---

## 🔧 Google Workspace / Интеграции

| Задача | Скилл |
|--------|-------|
| Gmail | `gmail` + `gb-gmail` |
| Google Sheets | `google-sheets` |
| Google Drive | `google-drive` |
| Google Docs | `google-docs` |
| Google Slides | `google-slides` |
| Google Calendar | `google-calendar` |
| n8n воркфлоу | `know-n8n-mcp` |

---

## 🧠 Мета / Процесс

| Задача | Скилл |
|--------|-------|
| Получение объективной обратной связи | `gb-balanced` |
| Ревью полученного code review | `receiving-code-review` |
| Запрос code review | `requesting-code-review` |
| Завершение ветки / мёрдж | `finishing-a-development-branch` |
| Git worktrees | `using-git-worktrees` |
| Параллельная работа над задачами | `dispatching-parallel-agents` + `know-subtask` |
| Оценка незнакомого репо / скилла | `acc-repo-evaluator` |
| Karpathy принципы разработки | `karpathy-guidelines` |

---

## 🔑 Правила загрузки

1. **Всегда загружай скилл** перед началом работы — не работай из памяти
2. **FFA задачи** → всегда начинай с `agency-agents`
3. **Сложные задачи** → комбинируй 2-3 скилла
4. **Не знаешь какой скилл** → прочитай `using-superpowers`
5. **Knowledge-скиллы** (`know-*`) → справочная информация об инструментах, читай когда нужно знать как работает конкретный инструмент
6. **`jf-*` скиллы** → специализированные языковые/фреймворк эксперты с reference-файлами
7. **`ar-*` скиллы** → бизнес и продуктовые эксперты (finance, C-level, PM, engineering)
8. **`gb-*` скиллы** → инструментальные (TDD, решения, ретро, презентации, балансированный диалог)
