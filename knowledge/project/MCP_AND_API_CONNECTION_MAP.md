# MCP AND API CONNECTION MAP

## Purpose
This file defines the conceptual connection map for APIs, MCP-style tool layers, and external integrations in the Formula Finance AI Office.

## Main Principle
Every connection should exist for a clear reason.

Do not add APIs or MCP servers just because they sound powerful.

## Connection Categories

### 1. Core LLM Layer
This is the reasoning layer used by the agents.

Possible examples:
- Claude;
- OpenAI;
- local models later if useful.

## 2. Messaging Layer
This is how the system communicates with humans.

Current priority:
- Telegram

Possible later channels:
- web chat;
- internal dashboard;
- email.

## 3. Data / Memory Layer
This stores and retrieves operational information.

Possible examples:
- files in project folder;
- database;
- vector store later if actually needed.

## 4. Business Integration Layer
These are integrations tied to business workflows.

Possible examples:
- CRM systems;
- Google Sheets;
- BigQuery;
- internal parsers;
- external business APIs.

## 5. Monitoring / State Layer
This supports:
- logs;
- events;
- state transitions;
- system health.

## 6. Pixel Office Visualization Layer
This consumes operational state and renders it as visual office activity.

## MCP Role
MCP-style connectors are useful when an agent needs standardized tool access to:
- files;
- browser actions;
- documentation;
- APIs;
- databases.

## Beginner Rule
Before adding a new API or MCP integration, answer:
- what business task does this unlock;
- which agent needs it;
- what data goes in;
- what output comes out;
- who approves sensitive actions;
- what happens if it fails.

## Final Principle
Connections should serve workflows, not complexity.