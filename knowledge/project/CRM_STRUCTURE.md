# CRM STRUCTURE

## Purpose
This file defines the high-level CRM structure for the Formula Finance project.

Its purpose is to help the system understand how lead and client-related information should be organized, tracked, and used across the project.

## Main Principle
CRM is not just a contact list.

It is a structured system for:
- lead tracking;
- client status tracking;
- communication support;
- proposal progression;
- follow-up logic;
- opportunity visibility.

The CRM structure should reduce confusion and help the business move leads and relationships forward in an orderly way.

## CRM Role in the Project
The CRM layer supports:
- Scout;
- CRM Agent;
- Proposal Agent;
- Coordinator;
- Colleague;
- Metrics / KPI Agent.

It acts as the structured commercial memory of the project.

## Main CRM Objects
The CRM structure should be based on several main object types:

### 1. Lead
A lead is a possible potential client.

A lead may include:
- company name;
- source;
- contact person if known;
- business type;
- first signals of need;
- qualification notes;
- current status;
- next step.

### 2. Contact
A contact is a person linked to a lead or client relationship.

A contact may include:
- full name;
- role;
- communication channel;
- contact details;
- company association;
- notes;
- communication relevance.

### 3. Opportunity
An opportunity is a qualified business case with real commercial potential.

An opportunity may include:
- identified problem;
- expected need;
- service fit;
- commercial stage;
- urgency;
- next action.

### 4. Client
A client is an active or confirmed business relationship.

A client record may include:
- company identity;
- active support area;
- service structure;
- current stage of cooperation;
- important operational notes;
- key relationship notes.

## Core CRM Functions
The CRM structure should support the following functions:
- storing lead information;
- tracking communication progression;
- recording qualification signals;
- separating weak leads from strong opportunities;
- supporting proposal progression;
- preserving relationship context;
- making next steps visible.

## CRM Pipeline Logic
The CRM system should eventually support a visible movement through stages.

Typical stage logic may include:
- new lead;
- not yet qualified;
- qualified lead;
- active conversation;
- proposal stage;
- waiting for response;
- won;
- lost;
- paused.

These stage labels can be refined later, but stage logic must remain clear.

## Data Quality Principle
CRM information should be structured enough to be usable.

This means:
- important fields should not stay empty without reason;
- notes should be understandable;
- status should be current;
- next step should be visible when possible;
- scattered fragments should be reduced.

## Proposal Connection
CRM should connect naturally with proposal logic.

The system should be able to see:
- whether a lead is ready for a proposal;
- what kind of proposal is needed;
- what has already been discussed;
- what level of scope the lead appears to need.

## Scout Connection
Scout may generate leads and initial observations, but CRM is where those leads should become structured commercial records.

Scout identifies.  
CRM structures and tracks.

## Coordinator Connection
Coordinator should use CRM structure to understand:
- what stage a lead is in;
- what role should act next;
- whether a proposal is needed;
- whether follow-up is overdue;
- whether there is movement or stagnation.

## Colleague Connection
Colleague may help summarize client context, draft follow-ups, and retrieve CRM-related memory, but should not replace CRM process logic.

## Future Expansion
This file can later be expanded with:
- exact field definitions;
- stage definitions;
- CRM status dictionary;
- communication log logic;
- activity tracking logic;
- proposal-linked CRM workflows;
- Bitrix24 or other CRM mapping logic.

## Final Principle
The CRM structure should help Formula Finance treat leads, opportunities, and client relationships as structured operational assets rather than scattered conversations.