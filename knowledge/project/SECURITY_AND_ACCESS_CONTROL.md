# SECURITY AND ACCESS CONTROL

## Purpose
This file defines the basic security and access control rules for the Formula Finance AI Office project.

Its purpose is to keep the first working version safe, understandable, and controllable.

## Main Principle
The first version should be secure by restriction, not by complexity.

## Why This Matters
Without clear access control:
- unauthorized users may reach the bot;
- sensitive actions may be triggered too easily;
- secrets may be exposed;
- trust in the system may collapse.

## Security Philosophy
The first version should follow these principles:
- allow only known users;
- keep secrets outside project files;
- require approval for sensitive actions;
- minimize automatic external actions;
- log important security-relevant events.

## Access Control Rules

### Allowed Users
The Telegram bot should respond only to:
- one admin user;
- or a small approved user list.

If the sender is not approved:
- do not provide project-sensitive answers;
- return a minimal rejection message;
- log the attempt.

### Role Simplicity
In the first version, keep roles simple:
- admin
- optional trusted user
- everyone else denied

Do not build complex RBAC in MVP.

## Sensitive Actions
The following actions should be treated as sensitive:
- changing configuration;
- triggering deployment;
- approving outbound business actions;
- sending messages to external clients automatically;
- modifying storage state beyond normal bot task handling.

Sensitive actions should require:
- explicit approval;
- or be completely disabled in MVP.

## Secrets Handling
Secrets must never be stored in regular project markdown files.

Examples of secrets:
- Telegram bot token
- model API keys
- database passwords
- service account credentials
- webhook secrets

Secrets should live in:
- environment variables;
- secure deployment configuration;
- server-side secret files if needed

## Logging And Security
Security-relevant events should be logged.

Examples:
- unauthorized access attempt
- missing token at startup
- invalid configuration
- failed authentication check
- sensitive action request

Logs should help debugging but should not expose secrets.

## Safe User Responses
If a request cannot be fulfilled for security reasons:
- do not reveal internal implementation details;
- do not reveal secret names or values;
- return a short safe explanation.

Example style:
- access denied
- this action is not allowed
- this function is not enabled in the current version

## External Action Rule
In MVP, the system should prefer:
- explanation;
- recommendation;
- draft output;
- approval request

It should avoid:
- autonomous execution of risky external actions.

## File Access Rule
The agent may read project files required for answering questions.

It should not:
- invent hidden files;
- claim access to unavailable secrets;
- expose confidential values from runtime configuration.

## Telegram Security Rule
The Telegram layer should validate:
- sender id;
- allowed chat or allowed admin scope;
- command eligibility if restricted commands exist.

## Deployment Security Basics
The first deployment should include:
- environment variables for secrets;
- restricted server access;
- simple restart procedure;
- log visibility for admin only.

## Beginner-Friendly Rule
The first version should be secure enough to operate safely,
but simple enough that the user understands why access is allowed or denied.

## Final Principle
A safe first agent is better than a powerful unsafe one.