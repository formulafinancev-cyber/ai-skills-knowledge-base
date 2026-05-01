# TELEGRAM BOT COMMAND SPEC

## Purpose
This file defines the first command specification for the Formula Finance AI Office Telegram bot.

Its purpose is to make the first operational interface simple, predictable, and beginner-friendly.

## Main Principle
The first Telegram bot should do a small number of useful things well.

It should not try to be a full autonomous multi-agent platform from day one.

## Role Of The First Telegram Bot
The first Telegram bot acts as:
- the main human-to-agent interface;
- a command console for the first operational agent;
- a notification layer;
- an approval entry point later.

## Early Scope
The bot should support:
- simple commands;
- short free-text questions;
- project folder grounded answers;
- basic status requests;
- later, approval actions.

## Recommended First Commands

### /start
Purpose:
- initialize the interaction;
- explain what the bot can do;
- show the basic command list.

Expected behavior:
- greet the user;
- explain current bot role;
- list basic commands.

## /help
Purpose:
- show supported commands;
- explain how to ask questions.

Expected behavior:
- provide compact help;
- include examples of supported requests.

## /status
Purpose:
- show current system or first-agent status.

Expected behavior:
- indicate whether the first agent is available;
- indicate whether the backend is working;
- indicate whether any current task is active.

## /files
Purpose:
- show what project files are currently available to the first agent.

Expected behavior:
- return a compact list of files or main categories;
- optionally summarize the project folder structure.

## /summary
Purpose:
- provide a short summary of the current project.

Expected behavior:
- summarize the project idea;
- mention the current implementation stage;
- mention the next recommended step.

## /next
Purpose:
- answer what should be done next.

Expected behavior:
- identify the most logical next step based on project stage;
- keep the answer practical and short.

## /agent
Purpose:
- explain which agent is currently active in this stage.

Expected behavior:
- explain the role of the current first agent;
- explain what it can and cannot do yet.

## /tasks
Purpose:
- show current known tasks if task storage is available.

Expected behavior:
- return current active tasks;
- if not implemented yet, explain that task tracking is not active in this version.

## /approve
Purpose:
- placeholder for future approval actions.

Expected behavior:
- in early versions, explain that approval flow is planned but not yet fully implemented.

## /reject
Purpose:
- placeholder for future rejection actions.

Expected behavior:
- same as above.

## Free-Text Requests
The bot should also support natural requests such as:
- what files do we already have;
- summarize the Pixel Office concept;
- what should we build next;
- explain the deployment plan for a beginner;
- draft a short update message.

## Response Style
The bot should answer:
- clearly;
- calmly;
- in practical language;
- without pretending to have features that do not yet exist.

## Safety Rules
The bot should:
- avoid fake certainty;
- avoid claiming deployment is complete when it is not;
- distinguish between current capability and planned capability;
- escalate unclear critical actions to the human.

## Final Principle
The first Telegram bot should feel reliable, grounded, and useful, even if its scope is intentionally narrow.