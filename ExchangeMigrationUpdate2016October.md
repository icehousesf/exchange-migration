# exchange-migration project updates
## This document provides work in progress updates to the WSI Exchange on-prem to Office 365 migration project
### Composed by @icehousesf :) 

---

# Exchange Migration Project Updates for October 2016:

## 6 Issues:

### 1) Public folder sync issue - RESOLVED

  * close to 80 public folders out of 26,000 + are not synching up.

### 2) Public folder access issue - RESOLVED

  * mailboxes created directly on Office 365 are not able to see public folder hierarchy
  * mailboxes migrated from on-prem to the cloud has no issues

### 3) Cross-Premises Free/Busy Information, mail tips, and out of office features issue - RESOLVED for Free/Busy

  * on-prem users cannot see Office 365 user's free/busy Information / other features and vice versa
  * *note:* Need to resolve issue #4 first

### 4) Federation Trust certificate expired issue -RESOLVED

  * Winoto is working with Microsoft support on this issue

### 5) Exchange 2013 mailbox databases backup issue

  * Andrew is working with Microsoft support and the WSI BAR team

### 6) Outlook client via Outlook Anywhere Issue 

  * Outlook client from home is connecting to the old endpoint owa2.wsgc.com instead of the new hybrid.wsgc.com
  * Also getting certificate alert for autodiscover.rejuvention.com during Outlook profile creation
  * Cezar is working with Microsfot support on this

## Updates:

*Friday 10/14/16:*

1. Working with Kory on outbound mail issue from Exchange 2013 to @admin2.mail.onmicrosoft.com. Exchange on-prem user not able to send email to O365 users. There is no outbound connection for Exchange 2013 ET servers going out to O365.  Created new NCCR REQ0059794. Sandeep Kumar from IT security team is helping me.

2. Confirmed free/busy still works in both directions.  My Exchange on-prem account can see O365 test account’s free/busy and vice versa.  O365 test accounts used were cptestuser5 and 6 with targetAddress set to @wsiadmin2.mail.onmicrosoft.com.

3. For issue #6, opened a new case #116101414803789 with Microsoft support. Worked with Rakesh from Microsoft. My account has full access permissions to RejuvWhiteGloves shared mailbox. Removed permissions resolved the certificate alert issue. Will look into the hybrid.wsgc.com issue on Monday.

*Thursday 10/13/16:*

1. Working with Kory on issue #3. Configured smarthost for “Outbound to Office 365” Send Connector with wsgc-com.mail.protection.outlook.com in Exchange 2013. Configured virtual directories for WebServices, OWA, ECP, MAPI, OAB and ActiveSync on all 7 Exchange 2013 CAS and MB servers. Modified the the “external host name” of Outlook Anywhere from owa2.wsgc.com to hybrid.wsgc.com on all 7 Exchange 13 servers. Ran HCW from RKEX13CAS2 server using my regular AD account on wsgc.com domain only successfully. Added wsiadmin2.onmicrosoft.com to “Outbound to Office 365” Send Connector and added  wsgc-com.mail.protection.outlook.com to Smart Host. Troubleshooting the TargetAddress issue.

2. Winoto got the outbound fax working by creating a Send connector in Exchange 2013.

*Wednesday 10/12/16:*

1. For issue #3, NCCR for hybrid has been implemented finally. Free/Busy is working now going the other direction. My Office 365 test account was able to see my on-prem mailbox free busy meetings. It could see my attendee details as well. However the target address of the Office 365 users needs to be setup in a certain way in order to work. Therefore we will be doing more testings to confirm that and make sure free busy and mail flow work properly. Another test will be doing is mail tips.

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



