# ERROR HANDLING AND LOGGING

## Purpose
This file defines the first error handling and logging principles for the Formula Finance AI Office project.

Its purpose is to make the first operational version understandable when something goes wrong.

## Main Principle
The first version does not need advanced observability.

It does need clear, simple, readable logs and predictable failure behavior.

## Why This Matters
Without basic error handling and logging:
- the user does not know why the bot failed;
- restart becomes confusing;
- storage state may become misleading;
- debugging becomes guesswork.

## Core Logging Goals
The first version should log:
- app start;
- app stop;
- incoming Telegram message;
- sender validation result;
- task creation;
- agent status changes;
- file loading;
- response generation result;
- outgoing Telegram response;
- error events.

## Recommended Log Style
Logs should be:
- timestamped;
- readable;
- short;
- structured enough for searching.

Possible styles:
- line-based text logs;
- JSON logs later.

For the beginner phase, readable line-based logs are enough.

## Recommended Log Levels
Use simple levels:
- debug
- info
- warn
- error

## Examples Of What To Log

### Application Startup
Examples:
- app started
- config loaded
- database connected
- Telegram bot connected

### Message Processing
Examples:
- message received
- sender allowed
- task created
- files loaded
- response sent

### Errors
Examples:
- missing Telegram token
- database connection failed
- project file not found
- model request failed
- Telegram send failed

## Error Handling Principles
When an error happens, the system should:
- capture the error;
- write a clear log line;
- update task status if relevant;
- update agent status if relevant;
- return a safe user-facing message when possible.

## User-Facing Error Rule
Do not expose raw stack traces to the Telegram user.

Instead, respond with simple safe text such as:
- something went wrong while processing the request;
- the request could not be completed;
- please try again or check the server logs.

## Agent State Rule
If an error affects a running task:
- task status should become failed;
- agent status may become error or return to idle depending on severity.

## File Loading Error Rule
If the requested answer depends on a missing project file:
- log the missing file;
- do not invent the missing content;
- tell the user that the relevant file or definition is not yet available.

## Startup Error Rule
If the app cannot start because of configuration failure:
- log the exact reason;
- stop cleanly;
- avoid pretending the system is ready.

## Beginner-Friendly Recovery Rule
The beginner should learn:
- first read the latest logs;
- identify whether the error is config, storage, Telegram, file-loading, or model-related;
- fix one issue at a time;
- restart and test again.

## Minimal Logging Targets
The first version may write logs to:
- console output;
- Docker logs;
- optional simple log file later.

## Final Principle
The first operational version should fail clearly, log clearly, and recover in a way the beginner can understand.