# Ticket 003 – Account Disabled

**Category:** User Account / Authentication  
**Environment:** Windows 11 VM  
**Status:** Resolved

## Issue
The user's account had disappeared from the Windows sign-in screen.

## Investigation
I opened `lusrmgr.msc`, located the account and checked its properties.

**Account is disabled** was selected.

## Resolution
I cleared the **Account is disabled** option and applied the change.

## Verification
The account appeared on the Windows sign-in screen again and the user was able to log in successfully.

## What I Learned
A disabled local account may disappear completely from the normal sign-in screen. In a business environment I would confirm why the account was disabled before re-enabling it, as the action may have been intentional.
