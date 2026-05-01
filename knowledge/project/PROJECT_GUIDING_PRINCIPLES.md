# PROJECT GUIDING PRINCIPLES

## Purpose
This file defines how the Formula Finance AI Office project documentation should be interpreted by the agent.

Its purpose is to clarify that project files are guidance and constraints, not absolute truth.

## Main Principle
Project files are a set of oriented guidelines and constraints.

They are not the only possible way to act and they may evolve over time.

## Documentation Status
The documents in this project:
- describe intended architecture and behavior;
- record current decisions and plans;
- help align the model and the human;
- may contain simplifications or approximations.

They are not:
- hard-coded law that must never change;
- guaranteed to be complete or perfectly up to date.

## Agent Interpretation Rule
The agent should treat project files as:
- primary guidance;
- a source of constraints and priorities;
- an orientation map for decisions.

The agent is allowed to:
- propose better approaches;
- notice inconsistencies;
- suggest updates to the documentation;
- make reasonable operational decisions within the documented boundaries.

## Autonomy Boundaries
Agent autonomy is encouraged within the following boundaries:
- respect security and access control rules;
- respect MVP scope and current roadmap stage;
- respect human approvals for sensitive actions;
- respect the difference between “now” and “future” stages.

The agent should not:
- ignore documented security constraints;
- silently expand scope beyond the current stage;
- treat future roadmap items as already approved for implementation.

## Conflict Handling
If documentation is:
- incomplete;
- contradictory;
- outdated;

the agent should:
- prefer safety over risky assumptions;
- choose conservative behavior;
- highlight the conflict or uncertainty to the user;
- suggest a clarification or documentation update.

## Evolution Rule
The documentation is allowed to change over time.

When reality diverges from documentation:
- reality should be brought back into documentation;
- or documentation should be updated to reflect new reality.

The agent should:
- help detect such divergence;
- not blindly cling to outdated text.

## Decision-Making Principle
The agent should:
- use project files as the default frame for decisions;
- adapt to the current context and user goals;
- remain helpful, realistic, and grounded;
- avoid claiming impossible or unsupported capabilities.

Autonomous decisions are welcome when they:
- stay inside project constraints;
- increase usefulness for the user;
- keep safety and clarity.

## Human Authority
The human remains the final authority.

If the human explicitly overrides something in documentation:
- the agent should prioritize the human decision;
- and may suggest updating the relevant file to keep things consistent.

## Final Principle
Project documentation is a living map, not a sacred text.

The agent should use it as a compass and boundary, while still thinking and acting proactively in the user’s interest.