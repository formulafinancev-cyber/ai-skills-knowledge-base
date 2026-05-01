# OPERATIONS PLAYBOOK

## Purpose
This file defines the practical operating playbook for the Formula Finance AI Office MVP.

Its purpose is to describe how the first working version should be run, checked, maintained, and recovered in day-to-day use.

## Main Principle
The first version should be operated through simple repeatable routines.

## Why This Matters
Without an operations playbook:
- the system may run once but become hard to maintain;
- failures may feel chaotic;
- restart steps may be forgotten;
- the user may lose confidence in the system.

## Operational Scope
This playbook applies to:
- the first Telegram bot;
- the first working agent;
- the first storage layer;
- the first deploy on VPS or equivalent server.

## Daily Operating Goals
The operator should be able to:
- confirm the bot is running;
- confirm Telegram responses work;
- confirm logs are visible;
- confirm state handling still works;
- restart the service safely if needed.

## Standard Operating Routine

### 1. Startup Check
When the system starts, verify:
- environment variables are loaded;
- the app starts without fatal crash;
- Telegram bot initialization succeeds;
- storage is reachable;
- logs begin normally.

### 2. Functional Check
After startup, verify:
- /start works;
- /help works;
- /status works;
- a simple project question gets a grounded answer.

### 3. Logging Check
Confirm the logs show:
- service startup;
- incoming message;
- task creation;
- response generation;
- response delivery.

### 4. State Check
Confirm that:
- the agent can move from idle to working and back to idle;
- a task can move to completed or failed;
- error paths do not leave the system in a confusing state.

## Restart Procedure
If the system must be restarted:
1. identify whether the issue is temporary or persistent;
2. read the latest logs;
3. stop the service cleanly;
4. start the service again;
5. repeat the startup and functional checks.

## Incident Handling
If something goes wrong, classify the problem first.

### Common Incident Types
- startup/configuration failure;
- Telegram connection issue;
- storage/database issue;
- project file loading issue;
- model response failure;
- unexpected empty or low-quality response.

### First Reaction Rule
Do not change many things at once.

Instead:
- identify the category of failure;
- inspect logs;
- fix one issue;
- retest.

## Safe Change Rule
For MVP, changes should be small and reversible.

Good changes:
- one prompt adjustment;
- one environment fix;
- one storage fix;
- one command fix.

Bad changes:
- many architecture changes at once;
- new integrations during an unresolved outage;
- expanding scope while debugging.

## Human Approval Rule
During MVP:
- the system should suggest and explain;
- the human should approve sensitive steps;
- autonomous risky actions should remain limited.

## Operational Metrics
The operator should observe at least:
- bot uptime;
- successful replies;
- failed replies;
- restart success;
- visible error frequency.

## Backup And Recovery Basics
At minimum, the operator should know:
- where environment configuration lives;
- where storage data lives;
- how to restore the project folder;
- how to restart the app after recovery.

## Documentation Rule
When an important operational lesson is learned:
- update the relevant file;
- keep the playbook current;
- prefer clarity over long theory.

## MVP Reality Rule
The first version is not expected to be perfect.

It is expected to be:
- understandable;
- restartable;
- observable;
- improvable.

## Final Principle
A working AI Office MVP is not only something that can answer once.

It is something that can be operated repeatedly without confusion.