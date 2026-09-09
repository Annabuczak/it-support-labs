# Ticket 005 – Application Will Not Open

**Category:** Application Support  
**Environment:** Windows 11 VM  
**Status:** Resolved

## Issue
User reported that an application would not open correctly.

## Investigation
I opened Task Manager using `Ctrl + Shift + Esc` and checked the running processes.

The application process was already running and appeared to be stuck.

## Resolution
I selected the process and used **End task**, then reopened the application.

## Verification
The application launched successfully.

## What I Learned
When an application appears not to open, I should check whether an existing process is already running before reinstalling or making larger system changes.
