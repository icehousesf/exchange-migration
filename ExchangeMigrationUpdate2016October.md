# exchange-migration project updates
## This document provides work in progress updates to the WSI Exchange on-prem to Office 365 migration project
### Composed by @icehousesf :) 

---

# Exchange Migration Project Updates for October 2016:

## 5 Issues:

### 1) Public folder sync issue - RESOLVED

  * close to 80 public folders out of 26,000 + are not synching up.

### 2) Public folder access issue - RESOLVED

  * mailboxes created directly on Office 365 are not able to see public folder hierarchy
  * mailboxes migrated from on-prem to the cloud has no issues

### 3) Cross-Premises Free/Busy Information, mail tips, and out of office features issue

  * on-prem users cannot see Office 365 user's free/busy Information / other features and vice versa
  * *note:* Need to resolve issue #4 first

### 4) Federation Trust certificate expired issue -RESOLVED

  * Winoto is working with Microsoft support on this issue

### 5) Exchange 2013 mailbox databases backup issue

  * Andrew is working with Microsoft support and the WSI BAR team

## Updates:

*Friday 10/7/16:*

1. Ran a comparison between RKEXPF1 and RKEX10PF1 servers today to see how the PFs doing after the re-pointing of MB DBs to the RKEX10PF1 server. There are 41 PFs are out of sync.

*Thursday 10/6/16:*

1. Document some Exchange configurations using Powershell.

*Wednesday 10/5/16:*

1. Compared AD attributes on cptestuser3 and cptestuser4. cptestuser4 was missing the smtp:username@service.wsgc.com address. Created that smtp address. Test sending email from my Exchange on-prem account to cptestuser3.  Very strange... waited for 10 to 15 minutes for the first email sent to cptestuser3 and it didn't show up.  Sent a 2nd test message and both showed up at the same time.  Sent the 3rd message and it showed up immediately.
2. Opened Microsoft Support request number: 116100514761395- Issue with Outbound TLS emails / Send connectors. Created a registry key on the 2013 ET servers to fix the problem. The edge sync was broken on all 3 servers. Removed and recreated them.

*Tuesday 10/4/16:*

1. Issue: Got NDRs when sending emails from my Exchange on-prem account to cptestuserx O365 users. Test sending email to cptestuser3 and cptestuser4 from my Exchange on-prem account. Changed the TargetAddress from SMTP:cptestuser3@wsiadmin2.mail.onmicrosoft.com to SMTP:cptestuser3@service.wsgc.com for cptestuser3 and cptestuser4.  cptestuser3 works right away but not cptestuser4.

*Monday 10/3/16:*

1. Created CHG60144 for Office 2016 and Office 365 migration.



