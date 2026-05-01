# SHARED RULES

## Purpose
This file defines the shared operating rules for the Formula Finance AI Office project.

Its purpose is to make project work more consistent, reduce confusion, and ensure that future outputs stay aligned with the approved structure of the system.

## Main Principle
The project should be built and operated with clarity.

Every task, file, and future implementation step should support:
- structure;
- consistency;
- practical usability;
- maintainability;
- low chaos.

## Rule 1 — Respect fixed decisions
If a project decision has already been fixed, do not casually replace it.

Examples of fixed decisions include:
- one shared Claude Code-based environment;
- role-based multi-agent structure;
- code-first orchestration;
- no n8n as the main orchestration layer;
- Claude Sonnet 4.6 as the main runtime model;
- Claude Opus 4.7 and OpenAI Codex both participating in code work.

Previously approved architecture should be treated as the default ground truth unless the user explicitly changes it.

## Rule 2 — Structure before implementation
For non-trivial tasks, structure should come before execution.

This means the preferred sequence is:
1. define the problem;
2. clarify constraints;
3. create structure;
4. define files or components;
5. only then move toward implementation.

Do not jump into direct implementation when the structure is still unclear.

## Rule 3 — File-first thinking
Important project knowledge should be turned into reusable files.

Do not rely only on chat context for durable project information.

When useful, always think in terms of:
- what file this belongs to;
- where it should live;
- how it should be named;
- whether it is a rule, knowledge file, template, reference, or implementation note.

## Rule 4 — One file, one main purpose
Each file should have one clear primary purpose.

Avoid mixing:
- business context with operating rules;
- templates with active knowledge;
- internal project truth with external references;
- specialist knowledge with unrelated general notes.

If a topic grows too large, create a dedicated file for it.

## Rule 5 — Clear role boundaries
Roles should remain distinct unless the user explicitly decides otherwise.

The project should prefer:
- specialist ownership;
- explicit responsibilities;
- visible boundaries.

Do not blur agents into one vague universal assistant model.

## Rule 6 — Colleague is broad, but not universal
Colleague is the broad conversational assistant role.

It may help with:
- everyday support;
- general questions;
- internal summaries;
- drafting;
- knowledge lookup.

But Colleague does not replace:
- Tech / DevOps;
- Legal & Regulatory Advisor;
- Metrics / KPI;
- Proposal Agent;
- other specialist roles.

## Rule 7 — Legal and regulatory work stays separate
Legal & Regulatory Advisor remains a dedicated specialist layer.

Regulatory monitoring, tax logic, compliance-oriented support, and contract-related reasoning should not be casually absorbed into another role.

## Rule 8 — Prefer modular growth
The project should grow by adding well-defined files and layers, not by turning existing documents into overloaded containers.

Prefer:
- modular documentation;
- small reusable files;
- explicit sections;
- progressive expansion.

Avoid giant overloaded documents whenever possible.

## Rule 9 — Use internal project truth first
When answering or planning, prefer the following source order:
1. fixed project decisions;
2. uploaded project files;
3. approved instructions;
4. the latest user clarification;
5. general outside best practices.

General best practices should support the project, not override it.

## Rule 10 — Ask when ambiguity is dangerous
If a task is unclear and the wrong assumption would damage the structure, ask a focused clarification question.

Do not invent important missing facts when those facts affect:
- architecture;
- role ownership;
- company logic;
- pricing logic;
- legal meaning;
- workflow design.

## Rule 11 — Simplicity before complexity
Do not overengineer early phases.

Prefer:
- simple foundations;
- stable structure;
- practical sequencing;
- understandable outputs.

Complexity should be added only when it helps the real project.

## Rule 12 — Support phased implementation
The system should be developed in phases.

Do not assume everything must be fully implemented at once.

Prefer:
- stable sequence;
- explicit next steps;
- manageable scope;
- clear transition from planning to execution.

## Rule 13 — Keep outputs implementation-ready
Whenever possible, outputs should be ready to become:
- project files;
- task definitions;
- role documents;
- knowledge documents;
- implementation inputs.

Avoid outputs that are vague, decorative, or difficult to reuse.

## Rule 14 — Keep the project readable
All project materials should remain easy to scan and understand.

Prefer:
- explicit headers;
- simple naming;
- stable phrasing;
- direct structure.

The project should remain understandable even after many files are added.

## Final Rule
Every future contribution should move the Formula Finance AI Office toward:
- better structure;
- better documentation;
- stronger role clarity;
- more reliable implementation;
- lower chaos;
- higher practical value.