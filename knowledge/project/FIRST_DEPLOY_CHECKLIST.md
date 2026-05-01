# FIRST DEPLOY CHECKLIST

## Purpose
This file defines the first deployment checklist for the Formula Finance AI Office project.

Its purpose is to give the beginner a practical verification list before and after the first launch.

## Main Principle
The first deployment should be verified through a simple checklist, not through guesswork.

## Pre-Deploy Checklist

### Server
- VPS exists
- server access details are available
- SSH connection works
- system packages are updated

### Docker
- Docker is installed
- Docker Compose is available
- Docker commands work without confusion

### Project Files
- application files are uploaded
- project knowledge files are uploaded
- core markdown files are present
- environment file is prepared

### Environment Variables
- Telegram bot token is set
- allowed Telegram user id list is set
- model API key is set
- project files path is set
- database variables are set if database is used

### Storage
- SQLite path is valid or PostgreSQL is configured
- database can start
- schema assumptions are understood

## Launch Checklist
- Docker Compose starts without immediate crash
- app container starts
- database container starts if used
- logs show configuration loaded
- logs show Telegram bot initialized
- logs show no immediate fatal errors

## Telegram Test Checklist
- /start works
- /help works
- /status works
- /summary works
- unauthorized user is rejected if access control is active

## State And Logging Checklist
- incoming message is logged
- task creation is logged
- agent status change is logged
- response sending is logged
- error branch is logged if failure is triggered

## Project Context Checklist
- the bot can access project files
- the bot can answer from project files
- missing file cases are handled honestly
- the bot does not invent nonexistent system capabilities

## Restart Checklist
- services can be stopped
- services can be started again
- logs remain readable after restart
- system returns to working state after restart

## Beginner Success Criteria
The first deploy is successful if:
- the bot runs;
- the bot answers in Telegram;
- the core project files are accessible;
- the user can restart the system;
- failures can be understood through logs.

## Important Rule
A first deployment does not need to be perfect.

It needs to be:
- real;
- understandable;
- restartable;
- debuggable.

## Final Principle
The first deployment checklist exists to turn “I think it works” into “I verified that it works.”