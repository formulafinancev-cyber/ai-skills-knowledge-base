# TASK ROUTING RULES

## Purpose
This file defines how tasks should be routed inside the Formula Finance AI Office project.

Its purpose is to preserve role clarity, reduce confusion, and make sure work goes to the right role instead of being handled randomly.

## Main Principle
Not every task should go to the same role.

Tasks should be routed according to:
- task type;
- required depth;
- required specialization;
- required output format;
- implementation relevance.

## Core Routing Rule
The system should prefer the most appropriate responsible role, not the broadest possible role.

This means:
- use specialist roles for specialist tasks;
- use Colleague for broad conversational support;
- use Coordinator for control, routing, and prioritization;
- do not overload one role with everything.

## Coordinator Routing Role
The Coordinator is responsible for:
- deciding where work should go;
- clarifying the next step when multiple paths are possible;
- sequencing work;
- preserving task order;
- preventing role confusion.

The Coordinator does not replace specialist execution.  
The Coordinator routes and organizes.

## Colleague Routing Role
Colleague should receive:
- broad everyday questions;
- message drafting;
- internal summaries;
- basic knowledge lookup;
- simple first-pass assistance;
- questions that are general rather than specialized.

Colleague should not be the default destination for specialist tasks that clearly belong elsewhere.

## Specialist Routing Logic

### Route to Scout when the task involves:
- lead discovery;
- prospect research;
- source identification;
- lead qualification signals;
- outreach target research;
- opportunity prioritization.

### Route to Content Strategist / Content Intelligence when the task involves:
- content research;
- content themes;
- competitor content observation;
- content planning logic;
- communication pattern analysis;
- content opportunity mapping.

### Route to Analyst when the task involves:
- structured reasoning;
- comparisons;
- interpretation;
- analytical breakdown;
- business logic analysis;
- insight-oriented tasks.

### Route to CRM Agent when the task involves:
- CRM process logic;
- pipeline support;
- contact structure;
- follow-up process;
- CRM record management logic;
- workflow support around sales records.

### Route to Proposal Agent when the task involves:
- commercial offers;
- proposal structure;
- proposal adaptation;
- service packaging into proposal form;
- proposal drafting support.

### Route to Tech / DevOps Agent when the task involves:
- implementation logic;
- integrations;
- code-related planning;
- technical structure;
- automation workflows;
- system-level engineering logic;
- configuration logic.

### Route to Metrics / KPI Agent when the task involves:
- KPI definitions;
- performance tracking;
- metric logic;
- measurement systems;
- success criteria;
- effectiveness evaluation.

### Route to Legal & Regulatory Advisor when the task involves:
- tax changes;
- legal changes;
- compliance questions;
- contract-oriented interpretation;
- regulatory monitoring;
- risk signals related to legal or regulatory topics.

### Route to Designer / Media Agent when the task involves:
- visual support;
- media packaging;
- design structure;
- presentation-oriented creative tasks;
- communication packaging.

### Route to Publisher when the task involves:
- publishing execution;
- release formatting;
- channel adaptation;
- publication workflow;
- output preparation for channels.

## Routing Priority Rule
If a task could fit several roles, use this logic:
1. choose the role with the clearest ownership;
2. if needed, let the Coordinator define the sequence;
3. if the task is still broad, use Colleague as the first conversational entry point;
4. if the task becomes specialized, move it to the correct role.

## Multi-Role Task Rule
Some tasks naturally involve multiple roles.

In such cases:
- do not collapse the whole task into one role;
- split the task into role-specific parts;
- let Coordinator manage the sequence if needed;
- preserve visible ownership.

Example logic:
- Scout finds leads;
- CRM Agent structures pipeline follow-up logic;
- Proposal Agent prepares the offer;
- Metrics / KPI Agent defines measurement logic.

## Escalation Rule
If a task becomes more specialized than first expected, it should be escalated to the correct role.

Do not keep a task in the wrong role only because it started there.

## Final Rule
Task routing should always improve:
- role clarity;
- task quality;
- implementation readiness;
- project order;
- long-term scalability.

The goal of routing is not convenience alone.  
The goal is correct ownership.