# FIRST AGENT MVP SCOPE

## Purpose
This file defines the MVP scope of the first Formula Finance AI Office agent.

Its purpose is to clearly limit what the first agent should do in version 1.

## Main Principle
The first agent must be useful, but intentionally narrow.

It should solve a small number of tasks reliably before any expansion begins.

## Recommended First Agent
Recommended role:
- Colleague

## Why This Agent Is Chosen First
The Colleague is the safest first operational agent because it can:
- answer questions;
- summarize project files;
- explain current project structure;
- give next-step guidance;
- work inside Telegram without requiring complex multi-agent routing.

## In Scope For MVP
The first version should support:

### 1. Basic Telegram Interaction
The agent can:
- answer /start;
- answer /help;
- answer /status;
- answer /summary;
- answer simple free-text project questions.

### 2. Project File Grounding
The agent can:
- read uploaded project markdown files;
- use them as the main source of truth;
- explain what is already defined;
- explain what is not yet implemented.

### 3. Project Navigation Help
The agent can:
- explain what files already exist;
- explain what should be done next;
- summarize the current implementation stage;
- give short project updates.

### 4. Basic State Handling
The system can:
- create a task record;
- update agent status;
- log message processing;
- return to idle after completion.

### 5. Beginner-Friendly Deployment Explanations
The agent can:
- explain deployment steps in simple language;
- explain environment variables;
- explain storage and first deploy logic using existing project files.

## Explicitly Out Of Scope For MVP
The first version should not yet include:

### 1. Full Multi-Agent Orchestration
No real multi-agent coordination engine yet.

### 2. Pixel Office Live UI
No real-time visual office implementation yet.

### 3. CRM Automation
No live CRM workflows yet.

### 4. Proposal Generation Pipeline
No real proposal automation pipeline yet.

### 5. Legal Decision-Making
No legal certainty or legal execution logic.

### 6. Broad External Integrations
No unnecessary APIs or MCP integrations beyond what is required for the first useful version.

## MVP Success Criteria
The MVP is successful if:
- the Telegram bot runs;
- the first agent answers reliably;
- the agent uses project files correctly;
- statuses and basic logs work;
- the user understands what the system is doing.

## Expansion Rule
Only after MVP works should the project expand to:
- richer storage;
- more commands;
- more agents;
- approvals;
- Pixel Office UI;
- business workflow automation.

## Final Principle
The first agent MVP should prove reliability and clarity, not ambition.