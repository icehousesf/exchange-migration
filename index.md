# exchange-migration project updates
## This document provides work in progress updates to the WSI Exchange on-prem to Office 365 migration project
### Composed by @icehousesf :) 

---

# Exchange Migration Project Updates:

## 5 Issues:

### 1) Public folder sync issue

  * close to 80 public folders out of 26,000 are not synching up.

### 2) Public folder access issue

  * mailboxes created directly on Office 365 are not able to see public folder hierarchy
  * mailboxes migrated from on-prem to the cloud has no issues

### 3) Free/Busy Time issue

  * on-prem users cannot see Office 365 user's free/busy time + schedules and vice versa

### 4) Federation Trust certificate expired issue

  * Winoto is working with Microsoft support on this issue

### 5) Exchange 2013 mailbox databases backup issue

  * Andrew is working with Microsoft support and WSI BAR team

## Updates:

*Tuesday 9/13/16:*

1. Working with Weston on issue #3. Removed expired federation trust certificate from the store in MMC and from RKEX13CAS1 ecp. RKEX13CAS2 has a new federation trust certification that expires in year 2021. Exported that and imported into RKEX13CAS1. For some reason the old certificate in RKEX13CAS1 re-appeared and prevented us from going further in fixing the free/busy issue.  Waiting for Winoto to fix the certificate.

2. Microsoft support called back on issue #1. They suggested exporting and importing the public folder content from one server to another.

*Wednesday 9/14/16:*

1. Issue #2 got escalated to Microsoft Office Online team. Working with the Online team. Created cptestuser5 test account from Exchange 2013 powershell. Corrected the X500 address for cptestuser4 account. Ran full synchronization dirsync but dirsync seems to be not working. Andrew is looking into it.

*Thursday 9/15/16:*

1. Continue working with Microsoft support on issue #2. Below are some updates on the test accounts being worked on. I think this account has Exchange GUID configured as well.
  * cptestuser5 - changed the primary SMTP address a couple of times.  The last time was changing it back to cptestuser5@wsgc.com and was having problem syncing to the cloud.
  * cptestuser6 - configured Exchange GUID from Exchange 2013 powershell to match the GUID on Office 365. Was having problem configuring the mail profile for Outlook client for this account.
  * cptestuser7 - configured Exchange GUID from Exchange 2013 powershell to match the GUID on Office 365. 
  * *note:* Do not make any changes to the 3 accounts per Microsoft support
