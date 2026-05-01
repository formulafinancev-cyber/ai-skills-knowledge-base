# EXTERNAL SKILLS AND REFERENCES

## Purpose
This file lists external skill-like resources, guides, and reference materials that can strengthen the Formula Finance project.

Its purpose is to provide a curated reference layer for:
- coding behavior;
- prompt and instruction quality;
- Claude Code / Claude Project best practices;
- agent and skill patterns.

These resources are reference patterns, not strict rules.

## Main Principle
External skills and guides should:
- support the project’s own architecture;
- improve behavior and quality;
- not override project-specific decisions and files.

The Formula Finance project’s internal instructions and knowledge are the primary source of truth.

---

## 1. Coding Behavior and Claude Code Skills

### 1.1 Karpathy-style coding discipline (Claude Code)

**Resource:**  
forrestchang/andrej-karpathy-skills  
https://github.com/forrestchang/andrej-karpathy-skills

**Purpose:**  
A single CLAUDE.md file that encodes coding behavior guidelines for Claude Code-style assistants, based on observed pitfalls and best practices.

**What it is useful for:**
- encouraging minimal, precise changes instead of uncontrolled refactors;
- reducing hallucinated edits and “helpful but unwanted” modifications;
- enforcing clearer reasoning before changes;
- improving reliability of code assistance.

**Best used with:**
- Claude Opus 4.7 for architecture and careful code changes;
- OpenAI Codex for implementation behavior inspiration;
- any coding-related role in Tech / DevOps Agent context.

**How to treat it here:**  
As a behavior reference for code-writing agents and workflows, not as a replacement for Formula Finance project rules.

---

## 2. Prompt and Instruction Best Practices

### 2.1 Anthropic Prompt Engineering Tutorial

**Resource:**  
Anthropic’s Prompt Engineering Interactive Tutorial  
https://github.com/anthropics/prompt-eng-interactive-tutorial

**Purpose:**  
Official interactive guide on structuring prompts and instructions for Claude.

**What it is useful for:**
- designing clear, effective instructions;
- structuring complex tasks into steps;
- improving system prompts and agent role definitions;
- understanding how Claude reacts to different prompt patterns.

**Best used with:**
- Claude Opus 4.7 for designing project instructions and role prompts;
- Coordinator and Tech / DevOps Agent when shaping new instruction files.

**How to treat it here:**  
As a reference when designing or refining instructions and prompts for agent roles and project workflows.

---

### 2.2 Claude Prompting Best Practices

**Resource:**  
Claude Prompting Best Practices (Anthropic)  
https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices

**Purpose:**  
Official Anthropic guidance on how to write effective prompts for Claude.

**What it is useful for:**
- ensuring instructions are explicit and structured;
- improving file-grounded workflows;
- aligning project instructions with Claude’s strengths.

**Best used with:**
- overall Project Instructions;
- all agent prompt design;
- any time new instruction files are created.

**How to treat it here:**  
As a confirmation and refinement of how project instructions and agent instructions are written.

---

## 3. Claude Skills Collections

### 3.1 Awesome Claude Skills (Collection 1)

**Resource:**  
karanb192/awesome-claude-skills  
https://github.com/karanb192/awesome-claude-skills

**Purpose:**  
A curated list of Claude skills for various domains (dev, analysis, automation, etc.).

**What it is useful for:**
- discovering additional skill patterns for:
  - coding workflows;
  - data analysis;
  - automation;
  - documentation support;
- inspiration for new internal skill-like behaviors in the project.

**Best used with:**
- Tech / DevOps Agent;
- Analyst;
- Colleague and Coordinator when designing workflow recipes.

**How to treat it here:**  
As an idea library. Use individual patterns that fit Formula Finance; do not import everything blindly.

---

### 3.2 Awesome Claude Skills (Collection 2)

**Resource:**  
BehiSecc/awesome-claude-skills  
https://github.com/BehiSecc/awesome-claude-skills

**Purpose:**  
Another collection of Claude skills and patterns.

**What it is useful for:**
- exploring practical skill ideas for:
  - debugging;
  - code review;
  - file organization;
  - testing and automation flows.

**Best used with:**
- Tech / DevOps Agent;
- Coordinator (for integrating skill patterns into workflows).

**How to treat it here:**  
As additional inspiration for designing internal skills and workflows, especially on the technical side.

---

### 3.3 Broader Agent Skills Collection

**Resource:**  
VoltAgent/awesome-agent-skills  
https://github.com/VoltAgent/awesome-agent-skills

**Purpose:**  
A broader collection of agent skills across platforms.

**What it is useful for:**
- understanding general agent skill patterns;
- thinking about tools, capabilities, and agent behaviors;
- inspiration for future extension of the AI office.

**Best used with:**
- Tech / DevOps Agent;
- Coordinator;
- any future multi-agent orchestration work.

**How to treat it here:**  
As a cross-ecosystem reference, not specific to Claude only.

---

## 4. Claude Code and Project Best Practices

### 4.1 Claude Code and Project Best Practice Guides

**Examples and types of resources:**
- Claude Code best practices (community and official guides);
- `.claude` folder / project organization overviews;
- agent tool and skill design writeups.

Representative resources include:
- Anatomy of the .claude Folder (2026 article);
- Claude Code best practice guides and checklists.

**Purpose:**  
To inform how the project:
- organizes files;
- structures knowledge;
- defines skills and tools;
- builds robust Claude Code workflows.

**Best used with:**
- Tech / DevOps Agent;
- Coordinator;
- when adjusting folder structure or adding new technical capabilities.

**How to treat it here:**  
As a supporting layer for project organization decisions already captured in the internal files.

---

## 5. Usage Guidelines in This Project

1. **Internal project files come first.**  
   - PROJECT_OVERVIEW, ARCHITECTURE_OVERVIEW, MODEL_STRATEGY, AGENT_MAP, SHARED_RULES, and other internal documents are the primary source of truth.

2. **External references are helpers, not masters.**  
   - Use these resources to improve quality, behavior, and patterns, not to overwrite project-specific decisions.

3. **Adapt, do not copy.**  
   - Take structures and ideas that fit Formula Finance.
   - Adjust them to the project’s architecture, roles, and business reality.

4. **Model-specific alignment.**  
   - Sonnet: mainly benefits from clearer instructions and structured workflows.  
   - Opus: benefits from prompt best practices, architecture patterns, and coding behavior improvements.  
   - Codex: benefits from code-behavior guidelines and skill-like workflows.

5. **Keep the project coherent.**  
   - Do not import conflicting patterns that break the established architecture or rules.
   - If an external pattern contradicts internal decisions, internal decisions win unless the user explicitly chooses to change them.

---

## Final Principle
External skills and reference materials exist to make the Formula Finance AI Office:

- more disciplined;
- more structured;
- more effective;
- more robust.

They should always serve the project’s architecture, not replace it.