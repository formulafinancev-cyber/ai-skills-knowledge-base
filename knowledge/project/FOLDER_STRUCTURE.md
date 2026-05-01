# FOLDER STRUCTURE

## Purpose
This file defines the target logical structure of the Formula Finance AI Office project files.

Its purpose is to keep the project organized, reduce chaos, and make future implementation easier for both planning and execution.

## Main Principle
The project should be structured as a file-first system.

This means:
- important knowledge should live in reusable files;
- each file should have a clear purpose;
- one file should cover one main topic;
- project structure should support long-term growth;
- files should be easy to update without breaking the whole system.

## Structure Philosophy
The project should not rely on one giant document.

Instead, it should use modular documentation layers:
- foundation files;
- architecture files;
- rules files;
- knowledge base files;
- domain files;
- templates;
- skills and external references;
- future implementation files.

## Recommended High-Level Structure

### 01. Foundation
This layer defines what the project is.

Typical file types in this layer:
- project overview;
- architecture overview;
- model strategy;
- agent map;
- folder structure.

### 02. Shared Rules
This layer defines how work should be done inside the project.

Typical file types in this layer:
- shared rules;
- naming conventions;
- file usage rules;
- task routing rules;
- handoff rules;
- decision rules.

### 03. Company Knowledge
This layer defines the business context.

Typical file types in this layer:
- company profile;
- services overview;
- pricing;
- positioning;
- FAQ;
- case library;
- proposal blocks.

### 04. Domain Knowledge
This layer defines operational specialist knowledge.

Typical file types in this layer:
- CRM structures;
- lead qualification logic;
- ICP definitions;
- KPI definitions;
- reporting logic;
- legal and regulatory notes;
- content rules;
- brand voice;
- source lists;
- channel notes.

### 05. Templates
This layer contains reusable operational templates.

Typical file types in this layer:
- meeting note template;
- summary template;
- proposal template;
- report template;
- client brief template;
- internal memo template.

### 06. Skills and External References
This layer contains external skill references and curated behavioral guides.

Typical file types in this layer:
- skill usage guide;
- external skills and references;
- coding behavior references;
- prompt engineering references;
- implementation reference notes.

These files should support the project, not replace its own internal rules.

### 07. Future Implementation Layer
This layer is reserved for future implementation-oriented project material.

Typical file types in this layer:
- workflow specifications;
- task plans;
- implementation plans;
- technical notes;
- integration notes;
- deployment-oriented files;
- future execution artifacts.

## File Design Rules
The project should follow these document structure rules:

- one main topic per file;
- simple and explicit filenames;
- reusable files over chat-only context;
- separate rules from business knowledge;
- separate templates from live knowledge;
- separate internal project truth from external references.

## Naming Principles
Filenames should be:
- explicit;
- readable;
- stable;
- easy to search.

Preferred style:
- uppercase or clear human-readable names for project documents;
- words separated consistently;
- no vague names like final, new, misc, temp, or draft-only labels without meaning.

## Maintenance Principle
The structure should remain understandable even as the project grows.

This means:
- do not overload one file with too many unrelated topics;
- create a new file when a topic becomes too large;
- preserve stable file roles over time;
- keep the project easy to scan.

## Skills Folder Principle
A skills or external references layer is useful, but it should not come first.

The project should first establish:
- project identity;
- architecture;
- model strategy;
- role map;
- shared rules;
- company knowledge.

Only after that should external skills and reference packs be added.

## Final Principle
The project folder structure should help Claude work with stable context.

It should make future planning, documentation, and implementation easier, not harder.