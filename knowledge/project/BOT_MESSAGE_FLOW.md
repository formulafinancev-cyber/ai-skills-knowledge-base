# BOT MESSAGE FLOW

## Purpose
This file defines the first message flow for the Formula Finance AI Office Telegram bot.

Its purpose is to describe, in a simple operational sequence, how a user message becomes an agent response.

## Main Principle
The first bot flow should be linear, understandable, and easy to debug.

It should not depend on hidden orchestration complexity.

## Core Flow Overview
The first version of the bot should process a message in a small number of clear steps:
- receive message;
- validate sender;
- interpret request;
- create or update task;
- load relevant project context;
- generate response;
- send response;
- update status and logs.

## Step-By-Step Flow

### Step 1 — Receive Telegram Message
The bot receives:
- a slash command;
- or a free-text message.

Examples:
- /start
- /help
- summarize the Pixel Office concept
- what should we build next

## Step 2 — Validate User
The system checks whether the sender is allowed.

This early version should ideally restrict access to:
- one admin user;
- or a short allowlist.

If the user is not allowed:
- reject the request;
- do not continue processing.

## Step 3 — Create Message Context
The system records:
- sender id;
- chat id;
- message text;
- timestamp;
- message type.

This context helps with logging and task creation.

## Step 4 — Interpret Request
The system decides what kind of request this is.

Examples:
- help request;
- status request;
- file summary request;
- next-step guidance request;
- general project question.

## Step 5 — Create Or Update Task
If the message requires actual processing, the system creates a task record.

Possible examples:
- summarize current project folder;
- explain deployment step;
- list available files;
- draft a short update.

Simple command replies may not need a full task in very early versions, but task creation is preferable for visibility.

## Step 6 — Update Agent Status
The active first agent changes status.

Typical example:
- idle -> working

If the task is blocked:
- working -> waiting_input
or:
- working -> error

## Step 7 — Load Relevant Project Files
The system loads:
- core project files;
- topic-relevant files;
- only the minimum relevant context for the request.

Examples:
- Pixel Office files for office questions;
- deployment files for deployment questions;
- architecture files for structure questions.

## Step 8 — Generate Response
The first agent generates a grounded answer.

The response should:
- rely on project files;
- remain honest about missing pieces;
- distinguish defined vs planned behavior.

## Step 9 — Send Response To Telegram
The system returns the answer to the user in Telegram.

The answer may be:
- short command output;
- short summary;
- structured explanation;
- next-step recommendation.

## Step 10 — Update Storage
After responding, the system updates:
- task status;
- agent status;
- event log;
- timestamps.

Typical example:
- task -> completed
- agent -> idle

## Step 11 — Error Branch
If a failure happens, the system should:
- record the error;
- set task state to failed if relevant;
- set agent status to error if relevant;
- return a safe failure message to the user.

## Minimal Example Flow
1. User sends: /summary
2. Bot validates user
3. Bot creates request context
4. Bot recognizes summary intent
5. Bot creates summary task
6. Agent status becomes working
7. System loads project summary files
8. Agent produces summary
9. Bot sends summary to Telegram
10. Task becomes completed
11. Agent returns to idle

## Final Principle
The first bot message flow should be simple enough that a beginner can trace every step from message to answer.