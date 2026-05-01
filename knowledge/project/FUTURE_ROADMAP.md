# FUTURE ROADMAP

## Purpose
This file defines the future roadmap for the Formula Finance AI Office project.

Its purpose is to clearly separate the MVP scope from later expansion stages.

## Main Principle
The system should grow in controlled stages, not all at once.

## Stage 0 — MVP (Current Focus)

Goal:
- first working Telegram-based agent (Colleague) with project knowledge.

Core capabilities:
- answer /start, /help, /status, /summary;
- answer project-related questions from project files;
- basic task and agent state handling;
- logging and error handling;
- first deploy on a single server.

Files mainly used:
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
- SECURITY_AND_ACCESS_CONTROL.md
- OPERATIONS_PLAYBOOK.md

## Stage 1 — Strong Single-Agent Operations

Goal:
- make the first agent reliable and comfortable for daily use.

Possible additions:
- more Telegram commands;
- better summaries and project explanations;
- refined prompts and context loading;
- more detailed logs and simple metrics.

Non-goals at this stage:
- no multi-agent orchestration yet;
- no aggressive automation of external systems.

## Stage 2 — Additional Agents And Roles

Goal:
- introduce additional agents in a limited, controlled way.

Examples:
- Regulatory Advisor;
- CRM/lead-focused agent;
- simple analytics or reporting assistant.

Principles:
- each new agent must have a clear role;
- each new agent must have a defined MVP scope;
- coordination remains simple;
- human oversight remains strong.

## Stage 3 — Business Integrations

Goal:
- connect the system to real business data and tools.

Possible integrations:
- CRM (Bitrix24 or alternative);
- Google Sheets and dashboards;
- external parsers and APIs.

Rules:
- add integrations only for concrete business tasks;
- keep human approval for sensitive actions;
- avoid over-automation in early stages.

## Stage 4 — Pixel Office Visualization

Goal:
- turn the existing Pixel Office concept into a real visual office.

Possible components:
- browser-based visual office;
- rooms and desks;
- agent positions and statuses;
- event-driven animations.

Principles:
- the visual layer should reflect operational truth;
- it should remain optional for operations;
- it should not become a requirement for the first business value.

## Stage 5 — Multi-Agent Coordination And Automation

Goal:
- enable richer collaboration between agents and more autonomous workflows.

Possible features:
- internal routing between agents;
- simple coordinator logic;
- basic multi-step workflows.

Constraints:
- automation should be auditable;
- logs and state must remain understandable;
- human should remain “in the loop” for important decisions.

## Stage 6 — Advanced Optimization And Intelligence

Goal:
- optimize workflows, decisions, and suggestions using more advanced techniques.

Possible directions:
- deeper analytics and scoring;
- better lead prioritization;
- pattern detection in business data.

Rule:
- only consider this once earlier stages are stable and useful.

## Out Of Scope For Defined Roadmap (For Now)

Currently out of scope:
- full no-limit autonomy without human control;
- uncontrolled outbound communications;
- complex, hard-to-explain black-box decisions.

These are intentionally not target goals for early and mid stages.

## Roadmap Usage

Use this roadmap to:
- stop MVP from expanding unnoticed;
- decide when a new file or feature belongs to a later stage;
- keep implementation focused on the current stage.

When considering a new feature, ask:
- does it belong to the current stage;
- or is it clearly a Stage 2+ or Stage 3+ feature.

## Final Principle
The Formula Finance AI Office should grow in stages that create real value, without sacrificing control, clarity, or operational simplicity.