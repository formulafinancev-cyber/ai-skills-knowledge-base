# ARCHITECTURE OVERVIEW

## Architecture Type
This project is designed as a unified multi-agent AI operating system for Formula Finance.

It is built around one shared Claude Code-based environment with multiple specialized roles, common project logic, shared knowledge, and structured coordination.

## Core Principle
The system is not a collection of unrelated bots.

It is one coherent working system where:
- each agent has a defined role;
- all agents operate inside one overall architecture;
- shared files and project rules are used as common context;
- responsibilities are separated clearly;
- implementation is phased and controlled.

## Main Components
The architecture includes the following layers:

1. interaction layer;
2. coordination layer;
3. specialist agent layer;
4. shared knowledge layer;
5. file and folder structure layer;
6. implementation layer;
7. reporting and feedback layer.

## Interaction Layer
The primary interaction channel for the owner and the team is Telegram.

Telegram acts as the operational front door for communication, task submission, updates, alerts, assistant support, and future workflow execution.

## Coordination Layer
A Coordinator role is responsible for routing, task organization, prioritization, and overall workflow control.

This role acts as the main control and dispatch layer inside the system.

## Specialist Agent Layer
The system contains multiple specialized roles with separate responsibilities.

These roles include:
- Coordinator
- Colleague / Secretary-Referent / Personal Assistant
- Scout / Lead Generation
- Content Strategist / Content Intelligence
- Analyst
- CRM Agent
- Proposal Agent
- Tech / DevOps Agent
- Metrics / KPI Agent
- Legal & Regulatory Advisor
- Designer / Media Agent
- Publisher

Each role exists to reduce confusion, preserve responsibility boundaries, and support long-term scalability.

## Shared Knowledge Layer
The system depends on a shared knowledge base.

This includes:
- company information;
- service descriptions;
- pricing logic;
- positioning;
- cases;
- proposal blocks;
- legal and regulatory notes;
- content rules;
- CRM structures;
- KPI definitions;
- operating standards.

This shared knowledge is meant to ground future agent work and reduce repeated explanation.

## File and Folder Structure Layer
The project is expected to use a structured file-first organization.

This means:
- project knowledge should be stored in reusable files;
- rules should be stored separately from business information;
- templates should be stored separately from live operational material;
- configurations should remain distinct from narrative documentation;
- future implementation should follow folder logic instead of chat-only logic.

## Implementation Layer
The implementation approach is code-first.

The system should not rely on n8n as the main orchestration layer.

Technical workflows, automation, integrations, and internal routing should be handled through code, scripts, structured logic, and well-defined technical ownership.

## Reporting and Feedback Layer
The architecture should eventually support:
- task reporting;
- progress visibility;
- KPI tracking;
- alerts;
- summaries;
- operational feedback loops.

These outputs should help the owner manage the AI office as a real operating system rather than a loose set of conversations.

## Long-Term Design Goal
The long-term goal of the architecture is to create a stable and maintainable AI office where:
- each role has a clear purpose;
- project knowledge is reusable;
- tasks can be routed correctly;
- implementation can happen step by step;
- the system remains understandable as it grows.

## Important Constraint
Architecture decisions should always prefer:
- clarity;
- maintainability;
- modular growth;
- explicit role boundaries;
- low chaos;
- practical usability.