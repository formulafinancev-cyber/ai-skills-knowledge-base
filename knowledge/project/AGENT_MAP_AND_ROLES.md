# AGENT MAP AND ROLES

## Purpose
This file defines the main agent map of the Formula Finance AI Office project.

Its purpose is to describe:
- which agents exist;
- why each agent exists;
- what each agent is responsible for;
- what files and knowledge each agent relies on;
- which interfaces the agent should use;
- which business scenarios the agent is expected to handle.

## Main Principle
Each agent should have a clear role.

The project should avoid vague overlap where multiple agents appear to do the same thing without a clear reason.

## Core Agents

## 1. Coordinator
### Why This Agent Exists
The Coordinator exists to preserve order inside the AI Office.

### Main Role
The Coordinator:
- routes tasks;
- decides sequence;
- watches dependencies;
- reduces confusion;
- manages multi-stage workflows;
- handles escalation when ownership is unclear.

### Main Interfaces
- Telegram;
- Pixel Office;
- internal orchestration layer.

### Main Knowledge Files
- TASK_ROUTING_RULES.md
- HANDOFF_RULES.md
- SHARED_RULES.md
- STAGED_IMPLEMENTATION_STRATEGY.md

### Main Scenarios
- user asks what to do next;
- a task must be assigned to the correct agent;
- a task crosses multiple agents;
- a process is blocked or looping;
- implementation order must be clarified.

## 2. Colleague
### Why This Agent Exists
The Colleague exists as a universal assistant and secretary-referent role.

### Main Role
The Colleague:
- answers broad everyday questions;
- drafts messages;
- summarizes information;
- helps retrieve knowledge;
- supports internal communication;
- acts as a first conversational entry point.

### Main Interfaces
- Telegram;
- Pixel Office;
- internal chat layer.

### Main Knowledge Files
- COMPANY_PROFILE.md
- SERVICES_OVERVIEW.md
- POSITIONING.md
- FAQ.md
- BRAND_VOICE.md
- TEMPLATE_SUMMARY.md
- TEMPLATE_MEETING_NOTE.md

### Main Scenarios
- quick explanation request;
- draft a reply or message;
- summarize a discussion;
- answer internal questions about Formula Finance;
- support the user before handing off to a specialist.

## 3. Scout
### Why This Agent Exists
The Scout exists to discover and pre-qualify opportunities.

### Main Role
The Scout:
- finds leads;
- researches prospects;
- identifies signals of fit;
- supports early qualification;
- feeds potential opportunities into CRM.

### Main Interfaces
- Telegram alerts;
- Pixel Office sales / scouting zone;
- external research / parsing workflows.

### Main Knowledge Files
- ICP_DEFINITION.md
- LEAD_QUALIFICATION_RULES.md
- CRM_STRUCTURE.md
- SERVICES_OVERVIEW.md
- CASE_LIBRARY.md

### Main Scenarios
- search for relevant companies;
- identify possible pain signals;
- create first-pass lead notes;
- prioritize promising leads.

## 4. CRM Agent
### Why This Agent Exists
The CRM Agent exists to turn lead flow into structured commercial memory.

### Main Role
The CRM Agent:
- structures leads and contacts;
- updates commercial stages;
- keeps next steps visible;
- preserves relationship context;
- supports follow-up logic.

### Main Interfaces
- Telegram;
- Pixel Office sales / CRM room;
- CRM backend or future Bitrix24-like integration.

### Main Knowledge Files
- CRM_STRUCTURE.md
- LEAD_QUALIFICATION_RULES.md
- ICP_DEFINITION.md
- TEMPLATE_CLIENT_BRIEF.md
- TEMPLATE_SUMMARY.md

### Main Scenarios
- update lead stage;
- prepare follow-up notes;
- organize contacts and opportunities;
- store relationship memory;
- prepare context for Proposal Agent.

## 5. Proposal Agent
### Why This Agent Exists
The Proposal Agent exists to turn client situations into structured commercial offers.

### Main Role
The Proposal Agent:
- prepares proposal drafts;
- adapts offer structure to client needs;
- uses pricing logic carefully;
- converts briefs into business-ready proposals.

### Main Interfaces
- Telegram for approvals and delivery;
- Pixel Office proposal / meeting room;
- document generation layer later.

### Main Knowledge Files
- PROPOSAL_BLOCKS.md
- TEMPLATE_PROPOSAL.md
- PRICING.md
- SERVICES_OVERVIEW.md
- POSITIONING.md
- CASE_LIBRARY.md
- TEMPLATE_CLIENT_BRIEF.md

### Main Scenarios
- build commercial offer draft;
- adapt proposal for a given client;
- prepare scope explanation;
- prepare next-step proposal communication.

## 6. Analyst
### Why This Agent Exists
The Analyst exists to interpret information, not just list it.

### Main Role
The Analyst:
- analyzes structured business situations;
- explains implications;
- compares options;
- produces insight-oriented reasoning;
- helps turn data into understanding.

### Main Interfaces
- Telegram summaries;
- Pixel Office analytics desk;
- report and summary generation workflows.

### Main Knowledge Files
- KPI_DICTIONARY.md
- REPORTING_STRUCTURE.md
- TEMPLATE_REPORT.md
- TEMPLATE_SUMMARY.md
- COMPANY_PROFILE.md

### Main Scenarios
- interpret business data;
- compare options;
- produce analytical summaries;
- explain what a metric or change may mean.

## 7. Metrics / KPI Agent
### Why This Agent Exists
The Metrics / KPI Agent exists to structure metric systems and maintain KPI consistency.

### Main Role
The Metrics / KPI Agent:
- defines KPI logic;
- supports KPI sets and reporting consistency;
- helps align metrics across dashboards and reports.

### Main Interfaces
- Telegram;
- Pixel Office analytics desk;
- reporting / dashboard design workflows.

### Main Knowledge Files
- KPI_DICTIONARY.md
- REPORTING_STRUCTURE.md
- SERVICES_OVERVIEW.md
- TEMPLATE_REPORT.md

### Main Scenarios
- define KPI groups;
- align KPI naming;
- support dashboard/report structure;
- explain metric use in management reporting.

## 8. Legal & Regulatory Advisor
### Why This Agent Exists
The Legal & Regulatory Advisor exists to monitor relevant legal, tax, and regulatory changes.

### Main Role
The Legal & Regulatory Advisor:
- monitors source categories;
- spots important changes;
- explains practical impact;
- warns about possible risks;
- helps route issues requiring deeper review.

### Main Interfaces
- Telegram alerts;
- Pixel Office legal desk;
- source monitoring workflows.

### Main Knowledge Files
- LEGAL_MONITORING_SOURCES.md
- TEMPLATE_SUMMARY.md
- BRAND_VOICE.md

### Main Scenarios
- legal update alert;
- tax/regulatory signal interpretation;
- basic contract or rule-related warning;
- escalation recommendation.

## 9. Content Strategist
### Why This Agent Exists
The Content Strategist exists to design what should be said and why.

### Main Role
The Content Strategist:
- generates content directions;
- maps themes to business value;
- structures content ideas;
- aligns content with positioning and pains.

### Main Interfaces
- Telegram;
- Pixel Office content studio;
- content planning panels later.

### Main Knowledge Files
- CONTENT_PILLARS.md
- CONTENT_SOURCE_LIST.md
- BRAND_VOICE.md
- POSITIONING.md
- CASE_LIBRARY.md
- SERVICES_OVERVIEW.md

### Main Scenarios
- suggest content themes;
- create content plan;
- turn cases/pains into themes;
- match content to ICP and brand voice.

## 10. Publisher
### Why This Agent Exists
The Publisher exists to move content into publishable form and channel-ready output.

### Main Role
The Publisher:
- adapts content for channels;
- prepares publishing flow;
- organizes release readiness;
- helps make content operational.

### Main Interfaces
- Telegram approvals;
- Pixel Office content / publishing area;
- future channel publishing workflows.

### Main Knowledge Files
- CONTENT_PILLARS.md
- CONTENT_SOURCE_LIST.md
- BRAND_VOICE.md
- TEMPLATE_SUMMARY.md

### Main Scenarios
- prepare publishable content format;
- adapt long idea into smaller assets;
- prepare release package;
- coordinate publishing readiness.

## 11. Tech / DevOps Agent
### Why This Agent Exists
The Tech / DevOps Agent exists to design and maintain the technical execution layer.

### Main Role
The Tech / DevOps Agent:
- handles implementation logic;
- manages integrations;
- supports deployment;
- handles automation and infrastructure;
- supports Pixel Office backend and telemetry layers.

### Main Interfaces
- Telegram alerts;
- Pixel Office server / automation room;
- backend and server environments.

### Main Knowledge Files
- BEGINNER_DEPLOYMENT_REQUIREMENTS.md
- PIXEL_OFFICE_ARCHITECTURE.md
- STAGED_IMPLEMENTATION_STRATEGY.md
- EXTERNAL_SKILLS_AND_REFERENCES.md

### Main Scenarios
- connect APIs;
- design deployment flow;
- maintain backend services;
- support event/state infrastructure;
- implement automation and integrations.

## 12. Human Approval Role
### Why This Role Exists
Some tasks should not complete without the human.

### Main Role
The human approval role:
- confirms sensitive actions;
- approves proposals or publishing;
- decides on ambiguous cases;
- provides final business judgment.

### Main Interfaces
- Telegram;
- Pixel Office meeting room / approval panels.

### Main Scenarios
- approve publication;
- approve proposal delivery;
- approve legal-sensitive response;
- resolve uncertainty.

## Final Principle
Each agent should remain understandable, role-bounded, and connected to the project’s file-based knowledge system.