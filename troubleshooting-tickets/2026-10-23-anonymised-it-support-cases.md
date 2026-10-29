# Anonymised IT Support Troubleshooting Cases — Week Ending 23 October 2026

**Purpose:** Sanitised practical troubleshooting notes suitable for adaptation into public GitHub issues. No customer names, organisation names, personal details, email addresses, domains, tenant IDs, private URLs or real ticket numbers included.

**Week ending:** 23 October 2026

**Note:** These are cases discussed during the week, with completion status only where supported by the investigation. Do not publish internal screenshots, headers, logs or configurations without a separate confidentiality review.

## 01 — Email deliverability to Gmail spam

**Status:** Investigation in progress

**Issue and investigation:** Multiple users reported messages sent through Outlook and a CRM reaching Gmail spam folders. Confirmed examples of delivery to spam. Checked domain SPF: published, valid, permitted lookup count. DMARC: valid, reject policy, 100% enforcement. Microsoft 365 custom-domain DKIM: disabled, CNAME records missing. Recorded expected selector CNAMEs internally but deliberately excluded domain-specific DNS values here.

**Next steps / resolution:** Obtain a Gmail 'Show original' header with SPF/DKIM/DMARC results; review sender reputation and CRM authentication separately; escalate DKIM DNS configuration to authorised administrator.

**Lesson / limitation:** Do not assume disabled DKIM is the sole cause; no DNS changes made.

---

## 02 — Missing forwarded emails / information requests

**Status:** Partially investigated

**Issue and investigation:** Reports of important forwarded messages not appearing in recipient's inbox. Exchange message trace confirmed delivery of one example to Inbox; another date had no matching trace, older example exceeded trace retention. Checked mailbox delegation; online archive unavailable.

**Next steps / resolution:** Check Outlook on the web, Inbox rules, Deleted Items, Junk and Recover Deleted Items with account owner's permission. Review message trace for new examples.

**Lesson / limitation:** Delivery status does not prove the email remains in the Inbox.

---

## 03 — Severe Windows laptop slowdown and cloud sync

**Status:** Improved; monitor

**Issue and investigation:** Laptop slowed after several hours, with Word, Excel and Explorer delays, high CPU and memory usage. Cloud sync process was resource intensive. Identified an exceptionally large SharePoint folder shortcut included in OneDrive; removed the shortcut without deleting source documents. Paused sync to isolate resource impact, reset OneDrive, then resolved a long-path filename sync error. Search indexing backlog also observed. Performance improved and applications reopened normally.

**Next steps / resolution:** Monitor performance after a few hours and check sync health/indexing. Escalate if symptoms return.

**Lesson / limitation:** Likely contributing factors were sync workload and indexing; final root cause not established.

---

## 04 — No audio from laptop speakers

**Status:** Resolved

**Issue and investigation:** Built-in speakers produced no sound for user even though device audio worked during remote support and Windows Audio services were running. Plugging in headphones confirmed output, and unplugging them restored built-in speaker audio.

**Next steps / resolution:** If repeated, inspect default output device, audio enhancements, driver and jack-detection behaviour.

**Lesson / limitation:** Headphone connection reset output behaviour, but precise cause unknown.

---

## 05 — Employee departure auto-reply

**Status:** Completed

**Issue and investigation:** Configured an automatic reply on a departing employee's Microsoft 365 mailbox, advising senders that the user has left and providing a generic replacement contact. Configured for internal and external senders.

**Next steps / resolution:** Verify external and internal test messages; retain mailbox under organisation offboarding policy.

**Lesson / limitation:** No mailbox deletion performed as part of request.

---

## 06 — SharePoint site owner access removal

**Status:** Completed

**Issue and investigation:** Received request to remove an individual from a SharePoint communication site's access and ownership while keeping their email account active. Updated SharePoint site permissions rather than disabling the user account.

**Next steps / resolution:** Confirm effective permissions no longer grant site access.

**Lesson / limitation:** Least-privilege approach; mailbox and identity left intact.

---

## 07 — New laptop Autopilot wrong account at setup

**Status:** Unresolved

**Issue and investigation:** During Windows first-run setup, device displayed the wrong organisational sign-in identity. Corrected user assignment in Windows Autopilot, but the original sign-in identity persisted after a reboot.

**Next steps / resolution:** Check Autopilot device registration, assigned user, deployment profile and enrolment flow; avoid reset or deletion until prerequisites are confirmed.

**Lesson / limitation:** Correcting assigned user did not immediately resolve device screen.

---

## 08 — Browser/application website sign-in failure

**Status:** Investigated; escalation possible

**Issue and investigation:** Multiple employees could not log into a third-party website. Tested private browsing and reviewed available identity application records; no corresponding enterprise application was found in the tenant.

**Next steps / resolution:** Confirm scope across browsers/networks, record exact errors and timestamps, check provider status, SSO configuration, and filtering.

**Lesson / limitation:** No root cause confirmed.

---

## 09 — Recurring VPN sign-in and disconnections

**Status:** Under investigation

**Issue and investigation:** Reported repeated VPN sign-ins and intermittent disconnections. Investigated whether auto-connect configuration could be changed locally; centrally managed options were not visible and specialist management permissions were unavailable.

**Next steps / resolution:** Check client settings and policy with authorised VPN administrator; collect timestamps and client logs before changing policy.

**Lesson / limitation:** Separate symptoms may need different fixes.

---

## 10 — Holiday IVR time-based routing

**Status:** Configuration being validated

**Issue and investigation:** Configured six date/time conditions in a contact-centre IVR editor for a temporary bank-holiday announcement window covering a Saturday afternoon through Tuesday morning. Combined date boundaries with custom AND/OR expression.

**Next steps / resolution:** Validate expression syntax, script timezone and exact boundary behaviour; test routing before publish.

**Lesson / limitation:** No production activation or successful validation confirmed.

