# PIXEL OFFICE EVENT MODEL

## Purpose
This file defines the conceptual event model for the Pixel Office and agent telemetry system.

Its purpose is to establish a shared vocabulary of events so that the backend, Telegram, and Pixel Office front-end can stay synchronized.

## Main Principle
The Pixel Office should be driven by events, not by inferred animation.

## Event Envelope Fields
All events should ideally contain:
- event_id
- event_type
- timestamp
- source
- agent_id if relevant
- task_id if relevant
- correlation_id if relevant
- payload

## Core Event Types
- agent_registered
- agent_online
- agent_offline
- task_created
- task_assigned
- task_started
- task_progress
- task_completed
- task_failed
- status_changed
- room_changed
- output_ready
- handoff_created
- approval_requested
- approval_received
- approval_rejected
- alert_raised
- message_sent
- message_received
- error_logged

## Final Principle
The event model should provide a stable shared language for live state, transitions, approvals, errors, and task movement across the Formula Finance AI Office.