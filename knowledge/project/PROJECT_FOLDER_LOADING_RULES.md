# PROJECT FOLDER LOADING RULES

## Purpose
This file defines how the first agent should conceptually load and use the project folder as its main knowledge base.

## Main Principle
The project folder is the first agent memory layer.

The first agent should treat files in the project folder as the primary source of truth for project-specific answers.

## Why Folder Loading Matters
Without folder loading rules:
- the agent may answer too generically;
- project context may be lost;
- the user may need to repeat the same information many times;
- architecture decisions may drift.

## Loading Priorities

### Priority 1 — Core Project Definition Files
These files define what the project is.

Examples:
- COMPANY_PROFILE.md
- SERVICES_OVERVIEW.md
- POSITIONING.md
- PROJECT_INDEX files
- project summary files

### Priority 2 — Pixel Office Concept Files
These files define the visual and conceptual office layer.

Examples:
- PIXEL_OFFICE_CONCEPT.md
- PIXEL_OFFICE_ARCHITECTURE.md
- PIXEL_OFFICE_ROOM_MAP.md
- PIXEL_OFFICE_REFERENCES.md
- EXTERNAL_PIXEL_OFFICE_LINKS.md

### Priority 3 — Agent And Workflow Files
These files define the agent system.

Examples:
- AGENT_MAP_AND_ROLES.md
- PIXEL_OFFICE_AGENT_STATUSES.md
- PIXEL_OFFICE_EVENT_MODEL.md
- PIXEL_OFFICE_EVENT_ENVELOPE.md
- IMPLEMENTATION_PHASES.md

### Priority 4 — Deployment And Technical Files
These files define how the system may be implemented.

Examples:
- BEGINNER_DEPLOYMENT_REQUIREMENTS.md
- SERVER_DEPLOYMENT_BLUEPRINT.md
- MCP_AND_API_CONNECTION_MAP.md
- TELEGRAM_INTEGRATION_OVERVIEW.md
- TELEGRAM_BOT_COMMAND_SPEC.md
- FIRST_AGENT_SYSTEM_PROMPT.md

## Loading Strategy
The first agent does not need to load every file equally on every request.

A better approach is:
- load core files first;
- load topic-relevant files second;
- summarize when needed;
- avoid irrelevant file noise.

## Example Request Routing

### If the user asks about project meaning
Prefer:
- company files;
- service files;
- positioning files;
- project summary files.

### If the user asks about Pixel Office
Prefer:
- Pixel Office concept files;
- architecture files;
- room map files;
- reference files.

### If the user asks about agents
Prefer:
- agent map;
- statuses;
- event model;
- implementation phases.

### If the user asks about deployment
Prefer:
- deployment files;
- server blueprint;
- Telegram integration files;
- MCP/API map.

## Response Rule
When possible, the agent should answer from file-grounded understanding, not from generic assumptions.

## Missing File Rule
If a needed file does not exist yet:
- say it is not yet defined;
- point to the nearest relevant file;
- recommend the next file or next step if appropriate.

## Folder Growth Rule
As the folder grows, the system should remain organized by:
- category;
- file naming consistency;
- project index maintenance;
- staged implementation logic.

## Final Principle
The agent should treat the project folder as structured memory, not as a random pile of notes.