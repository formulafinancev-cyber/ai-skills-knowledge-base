# PIXEL OFFICE AGENT STATUSES

## Purpose
This file defines the standard status vocabulary for agents in the Pixel Office.

Its purpose is to make sure all interfaces and systems interpret agent state consistently.

## Main Principle
An agent should not appear “busy” or “free” based on guesswork.

Status must reflect actual operational meaning.

## Core Status Set

### 1. idle
Meaning:
- no active task is currently assigned;
- the agent is available.

### 2. assigned
Meaning:
- a task has been assigned;
- work is about to begin.

### 3. working
Meaning:
- the agent is actively processing a task.

### 4. researching
Meaning:
- the agent is gathering information or sources.

### 5. drafting
Meaning:
- the agent is preparing output.

### 6. waiting_input
Meaning:
- the agent cannot continue without human or upstream input.

### 7. waiting_dependency
Meaning:
- the agent is blocked because another agent or subsystem has not completed its part.

### 8. review
Meaning:
- the agent has produced an output and it is under review or awaiting approval.

### 9. escalated
Meaning:
- the issue has been escalated to another role or to the human.

### 10. error
Meaning:
- the agent encountered a failure or could not continue correctly.

### 11. completed
Meaning:
- the task has been completed successfully.

### 12. offline
Meaning:
- the agent or its execution layer is not available.

## Final Principle
Agent status should communicate real task state clearly enough that a human can understand the office at a glance.