# PROJECT FILE READING ORDER

## Purpose
This file defines the recommended reading order for project files in the Formula Finance AI Office project.

Its purpose is to help the first agent, future agents, and the human avoid unnecessary context overload.

## Main Principle
Not every request requires every file.

The system should load files by priority and by topic relevance.

## Why This Matters
Without a reading order:
- the model may load too much context;
- important files may be diluted by irrelevant ones;
- responses may become vague;
- project performance may feel less focused.

## Reading Strategy
The system should read files in layers:
- first by core importance;
- then by topical relevance;
- then by implementation stage.

## Layer 1 — Always Read First
These files define the project at the highest level.

Examples:
- COMPANY_PROFILE.md
- SERVICES_OVERVIEW.md
- POSITIONING.md
- FORMULA_FINANCE_PROJECT_INDEX.txt
- FIRST_AGENT_MVP_SCOPE.md
- FIRST_AGENT_IMPLEMENTATION_ORDER.md

## Layer 2 — Read For First Agent Operation
These files define how the first agent should behave.

Examples:
- TELEGRAM_BOT_COMMAND_SPEC.md
- FIRST_AGENT_SYSTEM_PROMPT.md
- PROJECT_FOLDER_LOADING_RULES.md
- PROJECT_FILE_READING_ORDER.md

## Layer 3 — Read For Storage And Runtime Questions
These files should be loaded when the request is about infrastructure, runtime, state, or execution flow.

Examples:
- TASK_AND_STATUS_STORAGE_MODEL.md
- FIRST_DATABASE_SCHEMA.md
- BOT_MESSAGE_FLOW.md
- FIRST_AGENT_RUNTIME_LOOP.md
- ERROR_HANDLING_AND_LOGGING.md
- FIRST_DEPLOY_CHECKLIST.md
- ENV_VARIABLES_SPEC.md

## Layer 4 — Read For Deployment Questions
These files should be loaded when the request is about server setup, Docker, or first deployment.

Examples:
- BEGINNER_DEPLOYMENT_REQUIREMENTS.md
- SERVER_DEPLOYMENT_BLUEPRINT.md
- DOCKER_COMPOSE_FIRST_SETUP.md
- BEGINNER_SERVER_STEP_BY_STEP.md

## Layer 5 — Read For Pixel Office Questions
These files should be loaded when the request is about office visualization, room structure, statuses, event model, or UI.

Examples:
- PIXEL_OFFICE_CONCEPT.md
- PIXEL_OFFICE_ARCHITECTURE.md
- PIXEL_OFFICE_ROOM_MAP.md
- PIXEL_OFFICE_REFERENCES.md
- EXTERNAL_PIXEL_OFFICE_LINKS.md
- PIXEL_OFFICE_AGENT_STATUSES.md
- PIXEL_OFFICE_EVENT_MODEL.md
- PIXEL_OFFICE_EVENT_ENVELOPE.md
- PIXEL_OFFICE_JSON_SCHEMA.md
- PIXEL_OFFICE_UI_PANELS.md
- PIXEL_OFFICE_STATE_SYNC.md

## Layer 6 — Read For Agent System Questions
These files should be loaded when the request is about roles, orchestration, or future expansion.

Examples:
- AGENT_MAP_AND_ROLES.md
- IMPLEMENTATION_PHASES.md
- MCP_AND_API_CONNECTION_MAP.md
- FIRST_AGENT_BUILD_PLAN.md

## Request-Based Reading Rules

### If the user asks about the first working bot
Prefer:
- FIRST_AGENT_MVP_SCOPE.md
- FIRST_AGENT_IMPLEMENTATION_ORDER.md
- TELEGRAM_BOT_COMMAND_SPEC.md
- FIRST_AGENT_SYSTEM_PROMPT.md
- BOT_MESSAGE_FLOW.md

### If the user asks about deployment
Prefer:
- ENV_VARIABLES_SPEC.md
- DOCKER_COMPOSE_FIRST_SETUP.md
- BEGINNER_SERVER_STEP_BY_STEP.md
- FIRST_DEPLOY_CHECKLIST.md
- ERROR_HANDLING_AND_LOGGING.md

### If the user asks about storage or state
Prefer:
- TASK_AND_STATUS_STORAGE_MODEL.md
- FIRST_DATABASE_SCHEMA.md
- FIRST_AGENT_RUNTIME_LOOP.md
- BOT_MESSAGE_FLOW.md

### If the user asks about Pixel Office
Prefer:
- PIXEL_OFFICE_CONCEPT.md
- PIXEL_OFFICE_ARCHITECTURE.md
- PIXEL_OFFICE_ROOM_MAP.md
- PIXEL_OFFICE_EVENT_MODEL.md
- PIXEL_OFFICE_UI_PANELS.md

### If the user asks about future multi-agent growth
Prefer:
- AGENT_MAP_AND_ROLES.md
- IMPLEMENTATION_PHASES.md
- FIRST_AGENT_BUILD_PLAN.md
- MCP_AND_API_CONNECTION_MAP.md

## Anti-Overload Rule
The system should avoid loading:
- every file for every request;
- full Pixel Office context for simple Telegram questions;
- deployment files for branding or positioning questions;
- future-agent files for MVP-only questions unless needed.

## Beginner-Friendly Rule
When possible, the system should answer from the smallest useful set of files.

This keeps responses clearer and easier to trust.

## Final Principle
The best project memory is not the largest loaded context.

It is the right context loaded at the right time.