# Lab 03 — Windows Services & Event Viewer

## Objective

Practise managing Windows services and using Event Viewer to investigate system, application and security activity.

## Services

I opened Windows Services using `services.msc` and identified both running and stopped services.

I checked **Print Spooler**, which was:

- Status: Running
- Startup type: Automatic

I also identified **App Readiness** as a stopped service:

- Status: Stopped
- Startup type: Manual

I safely stopped the **Print Spooler** service to observe the effect on the system. When I opened Notepad and attempted to print, no printers were available and the Print option was unavailable. This demonstrated that the Print Spooler service is responsible for managing printing functionality.

I restarted Print Spooler and verified that printing functionality returned.

## Event Viewer

I opened Event Viewer using `eventvwr.msc` and investigated the main Windows logs.

### Application Log

I identified an application error:

- Source: Application Error
- Event ID: 1000
- Date/time: 08/09/2026, 16:13
- Faulting application: `svchost.exe`
- Faulting module: Unknown

This showed that Event Viewer can record application failures, although an individual event does not always provide enough information to determine the root cause.

### System Log

I identified a system error:

- Source: EventLog
- Event ID: 23
- Date/time: 08/09/2026, 16:19

I also filtered the System log by **Service Control Manager** to investigate events associated with Windows services.

### Security Log

I inspected the Security log and identified:

- Event ID: 4624
- Audit type: Audit Success
- Meaning: Successful account logon

I then filtered the Security log specifically for **Event ID 4624**, demonstrating how filtering can reduce thousands of log entries to events relevant to an investigation.

## Relating Events to System Activity

I locked the Windows VM, signed back into the Anna.Admin account and returned to the Security log. I refreshed and filtered the log for Event ID 4624.

This allowed me to relate a real action performed on the computer — signing into Windows — to the corresponding security event recorded by Windows.

## What I Learned

I learned how to identify running and stopped Windows services, check their startup types, safely stop and restart a service, and observe how a service failure affects system functionality.

I also learned how to use Event Viewer to investigate Application, System and Security logs; identify an event's source, Event ID and timestamp; filter large logs; and correlate Windows events with actual user or system activity.

The basic troubleshooting process I practised was:

**Symptom → identify relevant service/log → filter events → check Event ID/source/timestamp → relate the event to system activity → resolve the issue → verify recovery.**

**Skills demonstrated:** Windows 11 administration, Windows Services, Event Viewer, service troubleshooting, log analysis, event filtering, security auditing and basic incident investigation.
