# BEGINNER SERVER STEP BY STEP

## Purpose
This file defines the beginner-oriented conceptual sequence for first deploying the Formula Finance AI Office project to a server.

## Main Principle
The user should learn deployment as a sequence of small understandable actions.

The user should not be forced to understand everything at once.

## Beginner Goal
The first goal is simple:
- rent a server;
- connect to it;
- install Docker;
- place the project on the server;
- run the first Compose setup;
- verify the Telegram bot works.

## Step-By-Step Sequence

### Step 1 — Rent A VPS
The user rents a basic VPS from a hosting provider.

The first VPS does not need to be powerful.

### Step 2 — Get Server Access Data
The user receives:
- server IP;
- username, usually root or another user;
- password or SSH key instructions.

### Step 3 — Connect Through SSH
The user connects from a terminal to the server.

The beginner should learn:
- what SSH is;
- how to run a basic ssh command;
- how to confirm the connection works.

### Step 4 — Update The Server
The user updates system packages so the server starts from a cleaner state.

### Step 5 — Install Docker
The user installs Docker.

The beginner should understand:
- Docker is used to run packaged services;
- this avoids messy manual environment setup.

### Step 6 — Install Docker Compose
The user installs Docker Compose if it is not already available through the Docker plugin setup.

### Step 7 — Create Project Folder On Server
The user creates a project directory for the AI Office application.

### Step 8 — Upload Project Files
The user uploads:
- application code;
- environment file;
- project knowledge files if they are mounted or bundled.

### Step 9 — Configure Environment Variables
The user places secrets and config values in environment variables.

Important examples:
- Telegram token;
- API keys;
- database config.

### Step 10 — Run Docker Compose
The user starts the stack.

### Step 11 — Check Logs
The user verifies:
- app started correctly;
- database is reachable if used;
- Telegram bot launched without token errors.

### Step 12 — Test Telegram
The user sends a real command such as:
- /start
- /help
- /summary

### Step 13 — Fix First Errors
The beginner should expect:
- token mistakes;
- wrong environment variable names;
- port confusion;
- database connection mistakes;
- missing file path issues.

### Step 14 — Restart And Re-Test
The user learns how to:
- stop services;
- restart services;
- inspect logs again.

## Important Beginner Lessons
The beginner should understand:
- deployment is iterative;
- errors are normal;
- logs are the main source of truth;
- stable restart matters;
- small success is better than big broken complexity.

## Final Principle
A successful first deployment is not “perfect production.”

A successful first deployment means:
- the bot runs;
- the user can restart it;
- the system is understandable;
- the next iteration becomes easier.