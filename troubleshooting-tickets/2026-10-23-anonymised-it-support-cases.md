# IT Support Case Studies — Week Ending 23 October 2026

Ten anonymised support cases covering Microsoft 365, Windows, SharePoint, device deployment, remote access and telephony. Each case records the issue, investigation, outcome and lessons learned.

**Reporting period:** Week ending 23 October 2026  
**Status basis:** Progress recorded during the reporting week; pending checks are listed separately from confirmed outcomes. Customer identifiers and confidential technical evidence have been excluded.

## 01 — Microsoft 365 Email Deliverability: Messages Reaching Gmail Spam

**Status:** Investigation in progress  
**Technologies:** Microsoft 365, Outlook, CRM, SPF, DKIM, DMARC

### Issue
Multiple users reported that messages sent through Outlook and a CRM were reaching Gmail spam folders.

### Investigation
- Confirmed examples of messages delivered to spam.
- Checked SPF: published, valid and within the permitted DNS lookup count.
- Checked DMARC: valid, with a reject policy and 100% enforcement.
- Found that Microsoft 365 custom-domain DKIM was disabled and the required selector CNAME records were missing.

### Outcome
An authentication configuration gap was identified, but the cause of spam placement was not confirmed. No DNS changes were made. Domain-specific DNS values are excluded from this write-up.

### Next Steps
Obtain a Gmail “Show original” header to review SPF, DKIM and DMARC results. Assess sender reputation and CRM authentication separately, and escalate DKIM configuration to an authorised administrator.

### Lessons Learned
Disabled DKIM is a finding to investigate, rather than proof of the sole cause of a deliverability problem.

---

## 02 — Exchange Online: Forwarded Messages Missing from the Inbox

**Status:** Partially investigated  
**Technologies:** Exchange Online, Outlook, message trace

### Issue
Important forwarded messages were reported missing from a recipient’s inbox.

### Investigation
- Message trace confirmed delivery of one example to the Inbox.
- No matching trace was found for another reported date.
- An older example was outside message-trace retention.
- Checked mailbox delegation; an online archive was unavailable.

### Outcome
Delivery was confirmed for one example, but the current location of the message and the explanation for the other examples remained unverified.

### Next Steps
With the account owner’s permission, check Outlook on the web, Inbox rules, Deleted Items, Junk and Recover Deleted Items. Review message trace promptly for new examples.

### Lessons Learned
A delivery result confirms a point in the message journey; it does not establish that the message remains in the Inbox.

---

## 03 — Windows Performance: OneDrive Sync Workload and Application Delays

**Status:** Improved; monitoring required  
**Technologies:** Windows, OneDrive, SharePoint, Microsoft Office, search indexing

### Issue
A laptop became severely slow after several hours, with delays in Word, Excel and File Explorer alongside high CPU and memory usage.

### Investigation
- Observed resource-intensive cloud sync activity and a search indexing backlog.
- Identified an exceptionally large SharePoint folder shortcut in OneDrive.
- Removed the shortcut without deleting the source documents.
- Paused sync to isolate its resource impact, reset OneDrive and resolved a long-path filename sync error.

### Outcome
Performance improved and applications reopened normally. Sync workload and indexing were possible contributing factors; a final root cause was not established.

### Next Steps
Recheck performance after several hours and confirm sync health and indexing progress. Escalate if the symptoms return.

### Lessons Learned
Reducing sync scope can help isolate performance issues. Immediate improvement should be followed by monitoring before declaring a lasting resolution.

---

## 04 — Windows Audio: Restoring Built-in Speaker Output

**Status:** Resolved  
**Technologies:** Windows audio, built-in speakers, headphones

### Issue
The user could not hear sound from the laptop’s built-in speakers.

### Investigation
- Device audio worked during remote support, and Windows Audio services were running.
- Connected headphones and confirmed audio output.
- Disconnected the headphones; built-in speaker output returned.

### Outcome
Speaker audio was restored after connecting and disconnecting headphones. The precise cause was not identified.

### Next Steps
If the issue recurs, inspect the default output device, audio enhancements, driver and jack-detection behaviour.

### Lessons Learned
A simple output-device change can restore audio, but a successful workaround does not by itself establish the root cause.

---

## 05 — Microsoft 365 Offboarding: Configuring Mailbox Automatic Replies

**Status:** Configuration completed; testing pending  
**Technologies:** Microsoft 365, mailbox automatic replies

### Issue
A departing employee’s mailbox required an automatic reply directing senders to a generic replacement contact.

### Investigation
Configured the departure message for both internal and external senders.

### Outcome
The automatic reply configuration was completed. No mailbox deletion was performed; internal and external test results were not recorded.

### Next Steps
Send internal and external test messages to verify the reply. Retain the mailbox in accordance with the organisation’s offboarding policy.

### Lessons Learned
Record configuration completion and end-to-end verification separately in offboarding documentation.

---

## 06 — SharePoint Access Management: Removing Site Ownership and Permissions

**Status:** Permission changes completed; verification pending  
**Technologies:** SharePoint communication site, site permissions

### Issue
An individual’s access and ownership needed to be removed from a SharePoint communication site while their email account remained active.

### Investigation
Updated the SharePoint site permissions to address the site-specific request.

### Outcome
The permission changes were completed, with the mailbox and identity left intact. Effective-access verification remained outstanding.

### Next Steps
Confirm that effective permissions no longer grant the individual access to the site.

### Lessons Learned
Scope access changes to the requested resource and verify effective access after updating permissions.

---

## 07 — Windows Autopilot: Incorrect Sign-in Identity During Device Setup

**Status:** Unresolved  
**Technologies:** Windows Autopilot, Windows first-run setup

### Issue
A new laptop displayed the wrong organisational sign-in identity during first-run setup.

### Investigation
Corrected the assigned user in Windows Autopilot and rebooted the device.

### Outcome
The original sign-in identity persisted after the reboot. The assignment change did not resolve the displayed setup identity.

### Next Steps
Check device registration, assigned user, deployment profile and enrolment flow. Confirm prerequisites before considering a reset or deletion.

### Lessons Learned
An administrative assignment change should be verified on the device; it may not immediately change the setup experience.

---

## 08 — Web Application Access: Investigating Sign-in Failures Affecting Multiple Users

**Status:** Investigated; escalation may be required  
**Technologies:** Web browser, third-party application, identity application records

### Issue
Multiple employees could not sign in to a third-party website.

### Investigation
Tested private browsing and reviewed the available identity application records. No corresponding enterprise application was found in the tenant.

### Outcome
The initial checks did not establish a root cause. The absence of an enterprise application record did not establish how the website handled authentication.

### Next Steps
Confirm the scope across browsers and networks, capture exact errors and timestamps, and check provider status, single sign-on configuration and filtering.

### Lessons Learned
Establish the authentication method and the scope of affected users before drawing conclusions from tenant application records.

---

## 09 — VPN Connectivity: Repeated Authentication Prompts and Intermittent Disconnections

**Status:** Under investigation  
**Technologies:** VPN client, centrally managed policy

### Issue
A user reported repeated VPN sign-in prompts and intermittent disconnections.

### Investigation
Investigated whether auto-connect settings could be changed locally. Centrally managed options were not visible, and specialist management permissions were unavailable.

### Outcome
The investigation was limited by access to the management settings. No policy change or confirmed resolution was recorded.

### Next Steps
Review client settings and policy with an authorised VPN administrator. Collect timestamps and client logs before changing policy.

### Lessons Learned
Repeated authentication and disconnections may require separate investigations. Record management-access limitations when escalating.

---

## 10 — Contact Centre IVR: Configuring Holiday Routing Conditions

**Status:** Configuration awaiting validation  
**Technologies:** Contact-centre IVR, date/time conditions, AND/OR logic

### Issue
A temporary bank-holiday announcement needed to apply from Saturday afternoon through Tuesday morning.

### Investigation
Configured six date/time conditions in the IVR editor and combined the date boundaries using a custom AND/OR expression.

### Outcome
The routing configuration was prepared. Successful validation and production activation were not confirmed.

### Next Steps
Validate expression syntax, the script timezone and exact start/end boundary behaviour. Test the routing before publishing.

### Lessons Learned
Time-based routing requires explicit checks at the boundaries as well as within the intended announcement window.
