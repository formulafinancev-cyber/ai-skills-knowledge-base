# FIRST DATABASE SCHEMA

## Purpose
This file defines the first minimal database schema for the Formula Finance AI Office project.

Its purpose is to describe the smallest useful set of tables needed for the first operational version.

## Main Principle
The first schema should be minimal, readable, and directly tied to the first working workflow.

It should support the first Telegram bot and the first operational agent without unnecessary complexity.

## Recommended First Tables
The first version should focus on a very small set of tables.

Recommended first tables:
- tasks
- agent_statuses
- event_logs

Optional later:
- approvals
- users
- conversations
- integrations

## Table 1 — tasks

### Purpose
This table stores the basic lifecycle of tasks created from Telegram or other future interfaces.

### Recommended Fields
- task_id
- title
- description
- status
- assigned_agent
- priority
- source_channel
- created_at
- updated_at
- completed_at
- requires_approval
- approval_status
- output_summary

### Notes
This table should answer:
- what task was created;
- who is handling it;
- what its current state is;
- when it changed;
- what result was produced.

## Table 2 — agent_statuses

### Purpose
This table stores the current known status of each agent.

### Recommended Fields
- agent_id
- role
- current_status
- current_task_id
- last_update_at
- error_note

### Notes
This table should answer:
- which agent exists;
- what it is doing now;
- whether it is idle, working, blocked, or failed.

## Table 3 — event_logs

### Purpose
This table stores lightweight event history for debugging and observability.

### Recommended Fields
- event_id
- event_type
- timestamp
- agent_id
- task_id
- source
- payload_summary
- severity

### Notes
This table should answer:
- what happened;
- when it happened;
- which task or agent it affected;
- whether it was normal, warning, or error.

## Optional Table — approvals

### Purpose
This table may be added later if approval flow becomes active.

### Recommended Fields
- approval_id
- task_id
- requested_by
- requested_at
- approval_state
- approved_by
- resolved_at

## Recommended Minimal Relationships
- tasks.assigned_agent -> agent_statuses.agent_id
- agent_statuses.current_task_id -> tasks.task_id
- event_logs.task_id -> tasks.task_id
- event_logs.agent_id -> agent_statuses.agent_id

## Recommended ID Style
Use simple and readable ids.

Examples:
- task_001
- agent_colleague
- evt_001

Later, more robust UUID-style ids can be introduced if needed.

## Recommended First Status Values

### Task Status
Examples:
- created
- assigned
- working
- waiting_input
- review
- completed
- failed

### Agent Status
Examples:
- idle
- assigned
- working
- waiting_input
- waiting_dependency
- review
- error
- offline

## What Not To Add Yet
Do not add too early:
- highly normalized enterprise schemas;
- deep audit frameworks;
- many cross-reference tables;
- complex RBAC permissions;
- queue orchestration tables unless they become necessary.

## Final Principle
The first database schema should be just strong enough to support trust, visibility, and restartability in the first working version.