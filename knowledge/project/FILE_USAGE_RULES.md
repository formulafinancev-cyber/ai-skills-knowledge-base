# FILE USAGE RULES

## Purpose
This file defines how files should be used inside the Formula Finance AI Office project.

Its purpose is to keep the project knowledge base clean, predictable, and useful over time.

## Main Principle
Different kinds of information should be stored in different kinds of files.

The project should not mix everything into one general document.

A clean file system helps preserve context, reduce repetition, and improve future implementation.

## Rule 1 — Use files as project memory
Important project information should be saved in files, not left only in chat history.

If something is likely to matter again, it should usually become a reusable file.

Examples:
- architecture decisions;
- role definitions;
- workflow rules;
- company context;
- KPI logic;
- proposal structures;
- legal notes;
- content rules.

## Rule 2 — Keep one main purpose per file
Each file should have one main purpose.

A file should not simultaneously try to be:
- a rulebook;
- a company profile;
- a template;
- a scratchpad;
- an external reference dump.

If a file becomes too broad, split it.

## Rule 3 — Separate internal truth from external references
Internal project truth should live in dedicated internal files.

External sources, outside references, community skills, and example repositories should be stored separately.

Do not mix:
- approved project rules;
- outside inspiration;
- third-party examples;
- internal operating truth.

## Rule 4 — Separate rules from knowledge
Rules define how the project should operate.

Knowledge files define what the project knows.

These are not the same thing.

Examples of rules:
- shared rules;
- naming conventions;
- task routing rules;
- handoff rules.

Examples of knowledge:
- company profile;
- services overview;
- pricing;
- KPI definitions;
- legal sources;
- content pillars.

## Rule 5 — Separate templates from active knowledge
Templates are reusable document forms.

They should not be mixed into live knowledge files.

Examples of templates:
- proposal template;
- meeting note template;
- summary template;
- client brief template.

Templates are reusable structures, not the same as real business knowledge.

## Rule 6 — Separate implementation files from planning files
Planning files should describe structure, roles, and intended logic.

Implementation files should describe execution-oriented details.

Do not merge implementation-heavy technical planning into general project overview files.

Keep planning understandable before implementation becomes detailed.

## Rule 7 — Prefer durable documents over temporary chat fragments
If a useful answer appears in chat and is likely to matter again, it should be converted into a stable project file.

Chat is useful for iteration.  
Files are useful for long-term project memory.

## Rule 8 — Keep files readable
A file should be easy to scan quickly.

Prefer:
- explicit headings;
- stable terminology;
- short sections;
- direct language;
- one clear purpose.

A readable file is more useful than a clever file.

## Rule 9 — Update the right file
When new information appears, update the correct existing file if it already fits there.

Do not create a new file every time unless:
- the topic is truly separate;
- the existing file would become overloaded;
- a new dedicated document is clearly justified.

## Rule 10 — Use files to reduce repetition
The purpose of project files is not only storage.

Their purpose is also to reduce repeated explanation in future chats.

If a topic keeps repeating, it probably deserves its own file.

## Rule 11 — Preserve retrieval value
A file should be easy to find later.

This means:
- meaningful name;
- clear topic;
- predictable placement;
- no mixed-purpose clutter.

A file that cannot be found or understood quickly is a weak project asset.

## Rule 12 — External skills are support files
Skills, outside guides, example repos, and external best-practice notes are support materials.

They should strengthen the project, but they are not the project’s primary truth.

The project’s own architecture, files, and approved rules come first.

## Final Rule
Every file in the project should improve:
- memory;
- retrieval;
- clarity;
- maintainability;
- implementation readiness.

The file system should become more useful as it grows, not more chaotic.