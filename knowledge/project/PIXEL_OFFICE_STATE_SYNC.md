# PIXEL OFFICE STATE SYNC

## Purpose
This file defines the core principles for synchronizing agent and task state between Telegram, backend services, and Pixel Office UI.

## Main Principle
The office should not guess state.

It should receive state updates from a trusted backend or event stream.

## Why State Sync Matters
Without state synchronization:
- the visual office becomes misleading;
- agent status may show the wrong state;
- task panels may drift from reality;
- Telegram and Pixel Office may contradict each other.

## Recommended Model
Use a backend service as the source of truth.

The Pixel Office UI should mainly:
- render state;
- subscribe to updates;
- display events and transitions.

Telegram should mainly:
- receive commands;
- send notifications;
- trigger workflows;
- request approvals.

## Preferred Flow
1. a command enters via Telegram or UI;
2. backend creates or updates task state;
3. backend emits event;
4. agent state changes;
5. UI receives updated state;
6. Telegram receives summary or alert if needed.

## Sync Objects
The system should synchronize at least:
- agent state;
- task state;
- approval state;
- room / location state if visual movement is used;
- alert state;
- recent event feed.

## Source of Truth Principle
The source of truth should ideally be:
- backend state store;
- lightweight database;
- or orchestrator memory layer.

It should not be:
- front-end-only memory;
- ad-hoc Telegram message interpretation.

## Update Strategy
Possible strategies:
- WebSocket push;
- polling for prototype stage;
- event replay for recovery;
- state snapshot plus event updates.

## Failure Considerations
The system should handle:
- delayed event delivery;
- duplicate events;
- dropped connections;
- stale UI state;
- agent restart.

## Final Principle
Pixel Office must be synchronized from operational truth, not decorative animation logic.