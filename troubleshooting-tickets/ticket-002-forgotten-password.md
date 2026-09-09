# Ticket 002 – Forgotten Password

**Category:** User Account / Authentication  
**Environment:** Windows 11 VM  
**Status:** Resolved

## Issue
User had forgotten their Windows password and could not access their account.

## Investigation
Using an administrator account, I opened `lusrmgr.msc` and confirmed that the local user account existed and was enabled.

## Resolution
I selected the affected account and used **Set Password** to assign a new password.

## Verification
I signed out of the administrator account and successfully logged into the affected account using the new credentials.

## What I Learned
An administrator password reset is different from a user changing their own password. Windows warns that an administrator-forced reset can affect access to EFS-encrypted files, stored passwords and some certificates.
