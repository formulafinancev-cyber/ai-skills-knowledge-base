# TASK AND STATUS STORAGE MODEL

## Purpose
This file defines the beginner-friendly conceptual model for storing tasks, statuses, and lightweight operational state in the Formula Finance AI Office system.

## Main Principle
The first working system should store only the minimum necessary operational state.

It should not try to become a complex enterprise workflow engine from day one.

## Why Storage Matters
Without storage:
- the system forgets tasks;
- status cannot be trusted;
- approvals cannot be tracked;
- debugging becomes difficult;
- the user does not know what is active, blocked, or completed.

## What Should Be Stored First
The first version should store:
- tasks;
- agent statuses;
- approval requests if they appear;
- basic logs or event history;
- timestamps.

## Recommended Beginner Approach
For the earliest version, a simple model is enough.

Possible beginner-friendly options:
- SQLite;
- PostgreSQL if the user wants cleaner growth later.

## Practical Recommendation
If the goal is the fastest understandable start:
- begin with SQLite.

If the goal is slightly more future-ready infrastructure:
- begin with PostgreSQL in Docker Compose.

## Core Objects To Store

### 1. Task
A task should contain:
- task_id;
- title;
- description if needed;
- status;
- assigned_agent;
- priority;
- created_at;
- updated_at;
- source_channel;
- requires_approval;
- approval_status if relevant;
- output_summary if available.

### 2. Agent Status
An agent status record should contain:
- agent_id;
- role;
- current_status;
- current_task_id if any;
- last_update_at;
- error_note if any.

### 3. Approval Record
An approval record may contain:
- approval_id;
- related_task_id;
- requested_by;
- requested_at;
- approval_state;
- approved_by if available;
- resolved_at.

### 4. Event / Log Record
A lightweight event record may contain:
- event_id;
- event_type;
- timestamp;
- related_agent_id;
- related_task_id;
- short payload summary.

## Recommended Early Status Values
Examples:
- idle;
- assigned;
- working;
- waiting_input;
- waiting_dependency;
- review;
- error;
- completed;
- offline.

## Storage Rules
- every task should have a unique id;
- every status update should update a timestamp;
- task status and agent status should be linked but not confused;
- logs should be simple and readable;
- avoid over-modeling in the first version.

## Example Early Logic
- user sends request in Telegram;
- backend creates task;
- task gets status = assigned;
- agent status becomes working;
- result is produced;
- task becomes completed;
- agent returns to idle.

## What Not To Do In Version 1
Do not start with:
- deep workflow DAGs;
- heavy queue systems;
- overly abstract event sourcing;
- too many tables;
- complex permissions.

## Final Principle
The first storage model should be small, understandable, and enough to make state visible and trustworthy.