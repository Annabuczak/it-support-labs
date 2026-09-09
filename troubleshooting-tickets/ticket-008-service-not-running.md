# Ticket 008 – Windows Service Not Running

**Category:** Windows Services  
**Environment:** Windows 11 VM  
**Status:** Resolved

## Issue
A Windows feature was not operating as expected because its associated service was not running.

## Investigation
I opened `services.msc` and located the relevant service.

I checked:

- Service status
- Startup type
- Dependencies

Windows Search was used as the test service during the lab.

## Resolution
I started/restarted the affected service.

## Verification
I confirmed that the service showed **Running** and tested the associated Windows functionality.

## What I Learned
Windows features often depend on background services. If a feature suddenly stops working, checking the relevant service can identify the problem without making unnecessary changes elsewhere.
