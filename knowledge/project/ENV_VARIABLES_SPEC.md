# ENV VARIABLES SPEC

## Purpose
This file defines the first environment variable specification for the Formula Finance AI Office project.

Its purpose is to make the first deployment understandable, predictable, and safe.

## Main Principle
All secrets and deployment-specific configuration should live in environment variables.

They should not be hardcoded directly into the application.

## Why This Matters
Environment variables help:
- protect secrets;
- keep local and server environments cleaner;
- make Docker Compose setup easier;
- reduce accidental credential exposure;
- make future scaling easier.

## Core Variable Groups

### 1. Application Environment
These variables define the runtime environment.

Examples:
- APP_ENV
- APP_PORT
- LOG_LEVEL

### 2. Telegram Bot
These variables define Telegram integration.

Examples:
- TELEGRAM_BOT_TOKEN
- TELEGRAM_ALLOWED_USER_IDS
- TELEGRAM_ADMIN_CHAT_ID

### 3. LLM / Model Access
These variables define access to the model provider.

Examples:
- ANTHROPIC_API_KEY
- OPENAI_API_KEY

Note:
Only include the providers that are actually used in the first version.

### 4. Database
These variables define storage connectivity.

Examples:
- DATABASE_URL
- POSTGRES_DB
- POSTGRES_USER
- POSTGRES_PASSWORD

Note:
If SQLite is used in the first version, this block may be smaller and use a file path variable instead.

### 5. File / Project Loading
These variables define where the project knowledge files are located.

Examples:
- PROJECT_FILES_PATH
- PROJECT_INDEX_PATH

### 6. Optional Future Integrations
These are not required for version 1, but may appear later.

Examples:
- HUBSPOT_API_KEY
- GOOGLE_API_CREDENTIALS_PATH
- BIGQUERY_PROJECT_ID
- POSTIZ_API_KEY

## Recommended First Version Variables

### Required For The Simplest First Version
- APP_ENV
- LOG_LEVEL
- TELEGRAM_BOT_TOKEN
- TELEGRAM_ALLOWED_USER_IDS
- ANTHROPIC_API_KEY or other active model key
- PROJECT_FILES_PATH

### Required If PostgreSQL Is Used
- DATABASE_URL
or:
- POSTGRES_DB
- POSTGRES_USER
- POSTGRES_PASSWORD

## Example Variable Meanings

### APP_ENV
Purpose:
- tells the app which environment it is running in.

Example values:
- development
- staging
- production

### LOG_LEVEL
Purpose:
- controls how verbose logs should be.

Example values:
- debug
- info
- warn
- error

### TELEGRAM_BOT_TOKEN
Purpose:
- authenticates the Telegram bot.

### TELEGRAM_ALLOWED_USER_IDS
Purpose:
- restricts who can use the bot in early versions.

### TELEGRAM_ADMIN_CHAT_ID
Purpose:
- defines where alerts or important notifications may be sent.

### ANTHROPIC_API_KEY
Purpose:
- authenticates requests to the model provider.

### PROJECT_FILES_PATH
Purpose:
- tells the app where the project markdown knowledge files live.

### DATABASE_URL
Purpose:
- provides the database connection string in a single variable.

## Safety Rules
- never hardcode secrets in source code;
- never commit real production secrets into git;
- keep example values in `.env.example`, not real secrets;
- store real secrets in `.env` or secure deployment environment;
- rotate secrets if they are exposed.

## Beginner-Friendly Rule
The first deployment should use the smallest set of variables that still makes the system clear and functional.

## Final Principle
A clean environment variable spec is the bridge between architecture and real deployment.