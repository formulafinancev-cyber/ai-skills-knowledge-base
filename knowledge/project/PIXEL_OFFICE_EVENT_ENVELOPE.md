# PIXEL OFFICE EVENT ENVELOPE

## Purpose
This file defines the standard event envelope structure for the Formula Finance Pixel Office.

Its purpose is to ensure that all systems exchange events in a consistent shape.

## Main Principle
Every event should have a predictable wrapper.

The payload may vary by event type, but the outer structure should remain stable.

## Standard Envelope Fields

### Required Fields
- event_id
- event_type
- timestamp
- source
- payload

### Recommended Fields
- agent_id
- task_id
- correlation_id
- room_id
- severity
- version

## Field Meanings

### event_id
A unique identifier for the event.

### event_type
A stable machine-readable event name.

Examples:
- task_assigned
- task_started
- task_completed
- status_changed
- approval_requested
- error_logged

### timestamp
The time when the event was created.

Recommended format:
- ISO 8601 UTC

### source
The subsystem that emitted the event.

Examples:
- telegram-bot
- coordinator-agent
- crm-agent
- pixel-office-ui
- deployment-service

### payload
The actual event-specific data.

This is the only part expected to vary significantly between event types.

### agent_id
Used when the event relates to a specific agent.

### task_id
Used when the event relates to a specific task.

### correlation_id
Used to connect related events across a workflow.

### room_id
Used when the event affects office position or room logic.

### severity
Useful mainly for alerts, warnings, and errors.

Example values:
- info
- warning
- critical

### version
Useful when event contracts evolve over time.

## Example Conceptual Shape

```json
{
  "event_id": "evt_001",
  "event_type": "task_assigned",
  "timestamp": "2026-04-29T16:00:00Z",
  "source": "coordinator-agent",
  "agent_id": "agent_colleague",
  "task_id": "task_123",
  "correlation_id": "corr_777",
  "room_id": "room_operations",
  "severity": "info",
  "version": "1.0",
  "payload": {
    "title": "Prepare project summary",
    "priority": "high"
  }
}
```

## Rules
- event_type should be stable and machine-readable;
- payload should remain compact and relevant;
- do not hide key routing information inside payload if it belongs in top-level fields;
- timestamps should be standardized;
- IDs should be easy to trace in logs.

## Final Principle
A stable event envelope makes synchronization, debugging, observability, and future scaling much easier.