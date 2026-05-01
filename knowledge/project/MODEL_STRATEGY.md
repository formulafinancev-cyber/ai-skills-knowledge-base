# MODEL STRATEGY

## Purpose
This file defines how models are expected to be used inside the Formula Finance AI Office project.

Its purpose is to preserve consistency, reduce confusion, and make sure that planning, operations, and implementation are handled with the right model logic.

## Main Principle
Different models are used for different kinds of work.

This is intentional.

The project does not treat all models as interchangeable.  
Instead, each model has a primary area of strength and a preferred role inside the system.

## Claude Sonnet 4.6
Claude Sonnet 4.6 is the main runtime model for day-to-day work.

It is primarily used for:
- daily agent workflows;
- operational support;
- internal assistant work;
- structured business responses;
- summaries;
- CRM-related support;
- first-pass proposal drafting;
- content planning;
- routine multi-role execution;
- file-grounded project work.

Sonnet is the main model for ongoing project operation and practical working interaction.

## Claude Opus 4.7
Claude Opus 4.7 is a deep reasoning, architecture, and advanced implementation model.

It is primarily used for:
- architecture design;
- role design;
- boundary design;
- shared rules design;
- deep analysis;
- prompt engineering;
- system planning;
- writing important or complex code;
- reviewing code;
- improving implementation logic;
- decomposing large technical tasks.

Opus is not limited to planning only.  
Opus also participates in code writing and technical solution design.

## OpenAI Codex
OpenAI Codex is used as a strong engineering implementation model.

It is primarily used for:
- code writing;
- refactoring;
- scripting;
- integration work;
- automation logic;
- technical iteration;
- implementation acceleration;
- code-level experimentation.

Codex is a practical engineering layer, especially useful when implementation needs speed, iteration, and direct coding support.

## Required Interpretation
The model strategy for this project should be interpreted like this:

- Sonnet 4.6 = daily runtime and operational execution
- Opus 4.7 = architecture, deep reasoning, important code, and implementation review
- Codex = engineering execution, refactoring, and iterative implementation

## Important Rule
Do not assume that only Codex writes code.

Do not assume that Opus only plans and never writes code.

In this project, both **Opus 4.7** and **Codex** may be used for writing code.

The user manually decides how to combine them depending on the task.

## Mixed Workflow Logic
The expected mixed workflow looks like this:

- Sonnet helps run the operational and agent side of the system;
- Opus helps design, structure, review, and also write complex or important code;
- Codex helps implement, iterate, refactor, and accelerate engineering work.

This mixed model strategy is intentional and should be preserved in future planning.

## Planning Rule
When recommending next steps, always consider what kind of task is being handled:

- if it is an operational task, optimize for Sonnet;
- if it is a complex architecture or reasoning task, optimize for Opus;
- if it is an implementation task, optimize for Codex and/or Opus;
- if it is a hybrid task, allow a combined workflow.

## Stability Rule
All future decisions about workflows, prompts, files, and implementation should respect this model strategy.

The goal is not maximum model switching.  
The goal is effective division of labor between models.

## Final Principle
The project should use models intentionally, not randomly.

Each model should be applied where it gives the most practical value to the long-term development of the Formula Finance AI Office.