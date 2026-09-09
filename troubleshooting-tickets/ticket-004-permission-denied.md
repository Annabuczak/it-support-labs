# Ticket 004 – Permission Denied

**Category:** File Access / Permissions  
**Environment:** Windows 11 VM  
**Status:** Resolved

## Issue
User reported problems accessing a restricted folder.

## Investigation
I checked the folder's NTFS permissions through:

Properties → Security → Advanced

I also reviewed **Effective Access** and the user's local group memberships.

I considered whether access was being provided through direct permissions, group membership or inherited permissions.

## Resolution
The relevant permissions and group memberships were reviewed to ensure the user had the intended level of access.

## Verification
Folder access was tested using the affected user account.

## What I Learned
A user's effective permissions may come from several sources. Checking only the permissions directly assigned to the username may not explain why a user can or cannot access a resource.
