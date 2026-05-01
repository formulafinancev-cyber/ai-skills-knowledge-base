# FIRST AGENT IMPLEMENTATION ORDER

## Purpose
This file defines the exact implementation order for the first working Formula Finance AI Office agent.

Its purpose is to prevent хаос and make the first build sequence beginner-friendly.

## Main Principle
The first agent should be built in a strict order.

Do not build components randomly.

## Recommended Build Order

### Step 1 — Prepare Project Files
Make sure the core project markdown files already exist and are uploaded.

Minimum required groups:
- project definition files;
- Pixel Office concept files;
- agent role files;
- Telegram integration files;
- deployment files;
- storage and runtime files.

## Step 2 — Fix Environment Variables
Define the exact environment variables needed for the first version.

Reference file:
- ENV_VARIABLES_SPEC.md

## Step 3 — Fix Storage Model
Confirm which storage path is used in version 1.

Reference files:
- TASK_AND_STATUS_STORAGE_MODEL.md
- FIRST_DATABASE_SCHEMA.md

## Step 4 — Fix Telegram Command Surface
Confirm which commands the first bot supports.

Reference file:
- TELEGRAM_BOT_COMMAND_SPEC.md

## Step 5 — Fix First Agent Behavior
Confirm the first agent role and system prompt behavior.

Reference files:
- FIRST_AGENT_SYSTEM_PROMPT.md
- PROJECT_FOLDER_LOADING_RULES.md

## Step 6 — Fix Message Processing Logic
Confirm how requests travel through the bot.

Reference files:
- BOT_MESSAGE_FLOW.md
- FIRST_AGENT_RUNTIME_LOOP.md

## Step 7 — Fix Logging And Failure Handling
Confirm how the system behaves when something fails.

Reference file:
- ERROR_HANDLING_AND_LOGGING.md

## Step 8 — Fix Deployment Readiness
Confirm that deployment prerequisites and startup checks are understood.

Reference files:
- DOCKER_COMPOSE_FIRST_SETUP.md
- BEGINNER_SERVER_STEP_BY_STEP.md
- FIRST_DEPLOY_CHECKLIST.md

## Step 9 — Build Only The First Working Version
The first working version should do only a small set of things well.

Recommended scope:
- answer basic Telegram commands;
- read project files;
- summarize project context;
- explain next steps;
- log requests and responses.

## Step 10 — Test Before Expansion
Before adding new agents or new channels:
- test the first bot;
- confirm restart works;
- confirm logs are readable;
- confirm answers are grounded in project files.

## What Not To Do Yet
Do not do these things before the first agent works:
- add many new agents;
- build full Pixel Office UI;
- add many APIs;
- build advanced approval flows;
- add unnecessary infrastructure complexity.

## Final Principle
The first implementation order exists to ensure that the first agent becomes real before the system becomes ambitious.