# DOCKER COMPOSE FIRST SETUP

## Purpose
This file defines the first beginner-friendly Docker Compose setup concept for the Formula Finance AI Office project.

## Main Principle
The first Docker Compose setup should be small and easy to reason about.

It should only include the minimum services required for the first useful version.

## Why Docker Compose Is Useful
Docker Compose helps the beginner:
- run several services together;
- keep environment setup repeatable;
- reduce “it works only on my machine” problems;
- restart the system more easily.

## Recommended First Setup
The first setup should ideally include:
- app service;
- database service if needed.

Optional later:
- reverse proxy;
- web UI service;
- monitoring service.

## Smallest Practical Variants

### Variant A — Very Simple
Services:
- app
- sqlite file volume or local file storage

Use this if:
- the user wants the simplest possible first start.

### Variant B — Better Growth Path
Services:
- app
- postgres

Use this if:
- the user wants a cleaner path toward future scaling.

## Recommended Beginner Choice
For most serious project growth, the recommended first Compose setup is:
- app
- postgres

This is slightly more effort than SQLite, but usually more stable for future expansion.

## App Service Responsibilities
The app service may include:
- Telegram bot logic;
- first agent logic;
- project folder loading logic;
- task/status storage logic;
- logging.

## Database Service Responsibilities
The database service stores:
- tasks;
- statuses;
- approvals later;
- event summaries or logs.

## Core Compose Concepts The User Must Understand
The beginner should understand:
- service;
- image;
- container;
- port;
- volume;
- environment variables;
- restart policy.

## Environment Variables
The first setup will likely need:
- Telegram bot token;
- allowed admin user id or chat id;
- LLM API key if used;
- database connection string;
- environment name.

## Volumes
The system should use volumes for:
- persistent database data;
- optional logs;
- possibly mounted project files.

## Restart Rule
The setup should include simple restart behavior so the system can recover after reboot.

## What Not To Add Yet
Do not add too early:
- Kubernetes;
- many microservices;
- Redis unless truly required;
- observability stack overload;
- multi-container complexity without need.

## Final Principle
The first Docker Compose setup should be small enough to understand in one sitting.