# AGENT CHANNELS AND INTERFACES

## Purpose
This file defines where Formula Finance AI Office agents are expected to exist and interact.

Its purpose is to prevent the system from assuming that agents live only as abstract prompts or terminal sessions.

## Main Principle
Agents in this project should be designed as practical working roles that can be accessed through visible and usable interfaces.

The primary interface directions are:

- Telegram;
- Pixel Office;
- supporting internal web panels or dashboards if needed later.

## Telegram Role
Telegram should be treated as a primary operational channel.

This means agents may:
- receive commands;
- send alerts;
- send summaries;
- ask for confirmations;
- notify about issues;
- deliver lightweight outputs.

Telegram is useful because it is fast, practical, familiar, and good for operational interaction.

## Pixel Office Role
Pixel Office should be treated as a visual control room for the AI Office.

It is not only a decorative layer.

It should help visualize:
- which agent exists;
- what the agent is doing;
- what status it is currently in;
- whether it is waiting, working, blocked, or asking for attention;
- which room or functional zone it belongs to.

## Combined Interface Logic
Agents may exist in both Telegram and Pixel Office at the same time.

Example logic:
- Telegram = command and notification layer;
- Pixel Office = visual monitoring and control layer;
- backend logic = execution and orchestration layer.

This means one agent can:
- receive a task from Telegram;
- change status in Pixel Office;
- process logic in the backend;
- return output back into Telegram or another interface.

## Interface Philosophy
The project should not think of interfaces as separate “skins”.

Interfaces should reflect actual operational reality.

If an agent is blocked, waiting for confirmation, or actively processing something, the interfaces should make this understandable.

## Role of Telegram
Telegram is especially useful for:
- owner commands;
- agent confirmations;
- alerts;
- lead notifications;
- content approvals;
- legal/regulatory alerts;
- lightweight summaries and results.

## Role of Pixel Office
Pixel Office is especially useful for:
- observing all agents at once;
- seeing task flow visually;
- understanding bottlenecks;
- seeing which roles are idle or overloaded;
- giving the AI Office a usable operational dashboard feeling.

## Future Expansion
Additional interfaces may later include:
- CRM integrations;
- web admin panels;
- dashboard views;
- internal task boards.

But Telegram and Pixel Office should be treated as the main current direction.

## Final Principle
All agent architecture decisions should respect that Formula Finance AI Office is intended to operate through practical interfaces, especially Telegram and Pixel Office, not only through hidden internal prompts.