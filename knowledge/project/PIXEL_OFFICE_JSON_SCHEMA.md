# PIXEL OFFICE JSON SCHEMA

## Purpose
This file defines the conceptual JSON structure principles for Pixel Office data exchange.

## Main Principle
The Pixel Office should use structured JSON objects rather than ad-hoc text blobs.

## Core Object Types

### 1. Agent Object
- agent_id
- agent_name
- role
- status
- room_id
- current_task_id
- current_task_label
- last_update_at
- availability
- interface_channels
- error_state if any

### 2. Task Object
- task_id
- title
- type
- status
- assigned_agent_id
- priority
- created_at
- updated_at
- source_channel
- requires_human_approval
- dependency_ids
- output_summary if available

### 3. Event Object
- event_id
- event_type
- timestamp
- source
- agent_id
- task_id
- correlation_id
- payload

### 4. Room Object
- room_id
- room_name
- room_type
- mapped_roles
- display_order
- position metadata if needed later

## Final Principle
Pixel Office JSON should be explicit, stable, readable, and easy to validate.