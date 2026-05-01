# PIXEL OFFICE ARCHITECTURE

## Purpose
This file defines the high-level architecture of the Pixel Office subsystem for the Formula Finance AI Office project.

Its purpose is to make sure Pixel Office is designed as a real system with layers, not as a disconnected visual experiment.

## Main Principle
Pixel Office should be built as an event-driven visualization and control layer on top of real agent state.

## Core Architecture Layers

### 1. Agent Execution Layer
This is where actual agent logic runs.

It may include:
- Claude / Opus / Codex-driven logic;
- backend scripts;
- orchestrated task execution;
- Telegram-triggered actions;
- automation jobs.

This is the real work layer.

### 2. Event and State Layer
This layer translates actual work into structured agent state.

It should track:
- current status;
- assigned task;
- agent identity;
- timestamps;
- errors;
- waiting-for-input state;
- room / role mapping;
- task ownership.

This is the most important layer for Pixel Office usefulness.

### 3. Interface Delivery Layer
This layer pushes state into visible interfaces.

It may include:
- WebSocket event stream;
- polling endpoints;
- event feeds;
- JSON state endpoints.

Its role is to connect backend truth to front-end views.

### 4. Pixel Office Front-End Layer
This is the visual office itself.

It may include:
- pixel-art room rendering;
- agent sprites / avatars;
- movement and animation;
- click interaction;
- side panels;
- task and status indicators.

This is where users visually understand the office.

### 5. Telegram Interface Layer
This layer connects Telegram with the office.

It may include:
- bot command handling;
- outgoing alerts;
- approval requests;
- user-triggered tasks;
- status summaries.

Telegram should be treated as a command and notification surface.

## Architectural Rule
The system should not make the front-end responsible for inventing state.

The front-end should reflect state, not guess it.

## Practical Rule
Pixel Office must be useful even if visual polish is still basic.

This means:
- first make state correct;
- then make it visible;
- then make it beautiful.

## Future Extension
This architecture may later include:
- per-agent drilldown views;
- room-level metrics;
- event history;
- approval workflows;
- task reassignment controls.

## Final Principle
Pixel Office architecture should be event-driven, layered, and operationally useful from the beginning.