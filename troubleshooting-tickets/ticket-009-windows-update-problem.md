# Ticket 009 – Windows Update Problem

**Category:** Windows Maintenance  
**Environment:** Windows 11 VM  
**Status:** Investigated

## Issue
Simulated support scenario in which a user reports that Windows updates will not install.

## Investigation
I checked **Settings → Windows Update** and reviewed Update History.

I considered the main first-line causes of update problems:

- Internet connectivity
- Available disk space
- Windows Update status/error codes
- Required Windows services
- Pending restart
- Previous update failures

I also opened `services.msc` and inspected the Windows Update service and its dependencies.

## Resolution
Because Windows Update was functioning normally in the lab, I did not deliberately corrupt or disable update components. Instead, I completed the diagnostic process and identified where update failures would be investigated.

## Verification
Windows Update remained operational after the investigation.

## What I Learned
The exact error code and surrounding system conditions should be investigated before attempting more invasive Windows Update repairs.
