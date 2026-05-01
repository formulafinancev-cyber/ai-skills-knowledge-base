# FIRST AGENT RUNTIME LOOP

## Purpose
This file defines the first runtime loop concept for the Formula Finance AI Office application.

Its purpose is to describe how the first operational agent behaves continuously while the service is running.

## Main Principle
The first runtime loop should be simple, observable, and predictable.

It should not try to simulate complex multi-agent concurrency in the first version.

## What Runtime Loop Means
The runtime loop is the repeating operational cycle of the running application.

In the first version, this means:
- wait for incoming Telegram messages;
- validate and process them;
- update task and agent state;
- generate and send responses;
- log what happened;
- return to waiting state.

## First Runtime Loop Stages

### Stage 1 — Idle Waiting
The app is running and waiting for:
- Telegram commands;
- Telegram free-text requests;
- simple admin interactions.

At this stage:
- the first agent status is usually idle;
- no active task is being processed.

## Stage 2 — Input Received
A new Telegram input arrives.

The app should:
- capture the message;
- validate sender;
- create request context;
- decide whether to continue.

## Stage 3 — Task Initialization
If the request is valid and meaningful:
- create a task record;
- link it to the first active agent;
- update task state;
- update agent state.

Typical example:
- task status = assigned
- agent status = working

## Stage 4 — Context Loading
The app loads only the project files needed for the request.

Examples:
- deployment files for deployment questions;
- Pixel Office files for office questions;
- architecture files for structure questions.

## Stage 5 — Response Generation
The first agent produces a grounded answer.

The runtime should ensure:
- relevant context is used;
- unsupported capabilities are not invented;
- the response reflects current project reality.

## Stage 6 — Output Delivery
The app sends the answer back to Telegram.

The answer may include:
- summary;
- explanation;
- next-step suggestion;
- status output;
- file-based guidance.

## Stage 7 — State Finalization
After the response:
- task status becomes completed or failed;
- agent status returns to idle or moves to error;
- timestamps are updated;
- event logs are written.

## Stage 8 — Return To Waiting
The system returns to waiting mode for the next request.

This completes one runtime cycle.

## Error Branch
If something fails during processing:
- capture the error;
- write an error log;
- set task state to failed if a task exists;
- set agent state to error if needed;
- send a safe failure message to Telegram if possible.

## Recovery Principle
If the app restarts:
- current state should be restored from storage where possible;
- the system should avoid pretending that unfinished tasks were completed;
- restart should be safe and understandable.

## Beginner-Friendly Interpretation
The beginner can think of the runtime loop as:
- the bot waits;
- a message arrives;
- the bot thinks using project files;
- the bot answers;
- the system updates state;
- the bot waits again.

## Final Principle
The first runtime loop should be easy to trace mentally from waiting state to response and back to waiting state.