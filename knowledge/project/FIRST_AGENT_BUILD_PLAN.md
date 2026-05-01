# FIRST AGENT BUILD PLAN

## Purpose
This file defines the recommended plan for building the first real working agent in the Formula Finance AI Office project.

## Main Principle
The first agent should be useful, simple, and testable.

## Recommended First Agent
Recommended choice:
- Colleague

Alternative:
- Coordinator

## Why Colleague Is Recommended First
The Colleague is easier to test because it can:
- answer questions;
- summarize files;
- draft simple outputs;
- respond in Telegram;
- use the knowledge base without requiring complex orchestration.

## What The First Version Should Do
Version 1 should do only a few things well:
- answer “what is in the project” questions;
- summarize selected files;
- explain project structure;
- provide simple next-step guidance;
- answer in Telegram.

## What The First Version Should Not Do Yet
Do not require in version 1:
- full multi-agent routing;
- autonomous lead generation;
- proposal automation;
- full Pixel Office rendering;
- complex approvals;
- many external integrations.

## First Build Stages

### Stage 1 — Knowledge Access
The agent can read and use the project folder contents.

### Stage 2 — Telegram Interface
The agent can receive and answer messages in Telegram.

### Stage 3 — Basic Prompt Rules
The agent follows project role, tone, and file grounding.

### Stage 4 — Logging
The system logs incoming requests and outgoing responses.

### Stage 5 — Basic Status Exposure
The system can expose whether the agent is idle, working, or failed.

## Example Early User Requests
- what files do we already have;
- summarize the Pixel Office concept;
- what should we build next;
- explain deployment for a beginner;
- draft a short project update.

## Success Criteria
The first agent is successful if:
- it works reliably;
- it uses the project files correctly;
- it responds through Telegram;
- the user understands what it is doing;
- it can be restarted without chaos.

## Final Principle
The first agent is not meant to impress.

It is meant to create a reliable first operational foothold.