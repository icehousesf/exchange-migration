# exchange-migration project updates
## This document provides work in progress updates to the WSI Exchange on-prem to Office 365 migration project
### Composed by @icehousesf :) 

---

# Exchange Migration Project Updates for September 2016:

## 5 Issues:

### 1) Public folder sync issue

  * close to 80 public folders out of 26,000 + are not synching up.

### 2) Public folder access issue - RESOLVED

  * mailboxes created directly on Office 365 are not able to see public folder hierarchy
  * mailboxes migrated from on-prem to the cloud has no issues

### 3) Cross-Premises Free/Busy Information, mail tips, and out of office features issue

  * on-prem users cannot see Office 365 user's free/busy Information / other features and vice versa
  * *note:* Need to resolve issue #4 first before I can proceed

### 4) Federation Trust certificate expired issue

  * Winoto is working with Microsoft support on this issue

### 5) Exchange 2013 mailbox databases backup issue

  * Andrew is working with Microsoft support and the WSI BAR team

## Updates:

*Tuesday 9/27/16:*

1. Working on HCW. Sandeep from IT security has implemented the NCCR. HCW log shows Access Denied error.  Kory from Microsoft support said maybe the SSL inspection is causing problem. Sandeep is checking with his team.
2. RKEX10PF1 blue screen after patching. L2 is working with Microsoft support. I tried to repoint my mailbox database TestDB to Exchange 2007 PF server but my Outlook 2016 client still connects to RKEX10PF1.  Basically re-pointing didn’t work.  Although the MB database shows pointing to the Exchange 2007 PF server. There is no database-level setting in Exchange 2013. Exchange 2013 has a mailbox-level ability to specify the public folder mailbox, but by default Exchange auto-calculates the per-user hierarchy mailbox.  

*Monday 9/26/16:*

1. Working on issue #1. Created cptestuser21 on Exchange 2007 server. Used cptestuser21 and my account to export / import some PFs.
2. Working on issue #3, opened Microsoft support request # 116092614717505. HCW was trying to connect from hybrid server RKEX13CAS2 to Office 365 and was getting blocked. Submitted REQITEM0099625 to open the ports. Asked Breon to create TXT records for the other 10 domains.
3. Need to troubleshoot NDRs for cptestuser13,14,4.
4. Test accessing PFs using sgtestuser4 via both OWA and the Outlook client successfully.  The user was connected to RKEX10PF1.


*Friday 9/23/16:*

1. Updated firewall rules in the excel file and uploaded it to Service Now. Emailed Erik to review and approve.
2. Compared PFs.  5 of the 6 PFs that Andrew exported and imported were in sync.
3. Working on HCW. Sandeep from IT security confirmed my normal and my a_ accounts are not blocked by firewall. But the issue still persists. 

*Thursday 9/22/16:*

1. Testing emails between cptestuser13 (migrated to Office 365 mailbox) and my on-prem mailbox.  Got NDR when sending to cptestuser13. Receiving from cptestuser13 has no problem.  Found out cptestuser 13 do not have Office 365 license yet. Assigned E1 license to cptestuser13. Waiting for dirsync to complete before can test further.
2. Continued working on the firewall rules for Hybrid NCCR. Discussed with Hugo on the additional questions. 
3. Working on TXT records with Breon.  Breon created the public DNS TXT record for stores.potterybarn.com. He said TXT record has already been created for wsgc.com. The wsgc.com TXT record is needed for federation certificate renewal. However HCW still failed on validated. 
 Suspecting problem was caused by the firewall. Going to check with security team tomorrow. Once get this working, will have to create TXT records for the other 11 domains.

*Wednesday 9/21/16:*

1. Working on firewall rules for Hybrid NCCR. Emailed Hugo for help on a few more questions. 
2. Ran Hybrid Configuration Wizard (HCW).  It failed on verifying the TXT records.  Emailed Hugo for help.
3. Email testing - send and receive emails between 2 O365 users (cptestuser1 and cptestuser2) and my cpascual on-prem account was successful.
4. Email testing - the primary SMTP address for pwmtest20 was changed from @stores.williams-sonoma.com to @wsgc.com.  Received NDR when sending email from my Exchange on-prem account.
5. Test public folder access for users migrated from Exchange 2013 on-prem to Office 365. Migrated cptestuser13 and cptestuser14 to the cloud successfully.  Sending/receiving emails and accessing public folders using Outlook client were successful before and after the migration.
  * *note:* There is no need to re-create Outlook profile after the migration

*Tuesday 9/20/16:*

1. Dirsync completed last night and validated cptestuser1,2,4,8 successfully.  Those accounts can access PFs now. Reconfigured sgtestuser5,6, ran dirsync and validated successfully. Created a new test user cptestuser12 by following the steps provided by Microsoft support and validated successfully as well.  Question:  Should we do more testing with the migrated users?
2. Working on issue #3. Per Winoto, the federation trust certificate is probably no longer an issue. Tried to reconfigure the federation trust in on-prem admin center but was unsuccessful. It failed needing TXT record for the domain. 
3. Discussed with Hugo/Collin/Breon/Beatrice on hybrid deployment protocols, ports and endpoints. One thing brought up was the primary SMTP address needs to be equal as UPN. Mofidied the primary SMTP address of pwmtest20 from @stores.xxxxx.com to @wsgc.com. Mentioned the TXT record issue in the meeting. Will send Hugo the TXT records. Should we open a case with Microsoft to fix the free/busy issue? 

*Monday 9/19/16:*

1. Continued working on issue #2. Fixed test accounts (cptestuser3 and cptestuser7) by configuring the ExchangeGUID and the X500 address. We configured (cptestuser1, cptestuser2, cptestuser4, cptestuser8) and kicked off the full dirsync.

*Friday 9/16/16:*

1. Continue working with Microsoft support on issue #2. Got cptestuser5 and cptestuser6 working. The fix seems have to do with the ExchangeGUID and the X500 address. Asked Microsoft support for steps on what needs to be changed and how to do it so we can try it on other test accounts.
2. For issue #1, Andrew exported contents on 3 public folders from one server and imported them to the other server. I ran PF reports for comparison today and the results are not as expected. It seems like the imported items got replicated to the original server on one of the 3 PFs.  The report for the other 2 PFs do not making sense.

*Thursday 9/15/16:*

1. Continue working with Microsoft support on issue #2. Below are some updates on the test accounts being worked on.
  * cptestuser5 - changed the primary SMTP address a couple of times.  The last time was changing it back to cptestuser5@wsgc.com and was having problem syncing to the cloud. I think this account has Exchange GUID configured as well.
  * cptestuser6 - configured Exchange GUID from Exchange 2013 powershell to match the GUID on Office 365. Was having problem configuring the mail profile for Outlook client for this account.
  * cptestuser7 - configured Exchange GUID from Exchange 2013 powershell to match the GUID on Office 365. 
  * *note:* Do not make any changes to the 3 accounts per Microsoft support

*Wednesday 9/14/16:*

1. Issue #2 got escalated to Microsoft Office Online team. Working with the Online team. Created cptestuser5 test account from Exchange 2013 powershell. Corrected the X500 address for cptestuser4 account. Ran full synchronization dirsync but dirsync seems to be not working. Andrew is looking into it.

*Tuesday 9/13/16:*

1. Working with Weston on issue #3. Removed expired federation trust certificate from the store in MMC and from RKEX13CAS1 ecp. RKEX13CAS2 has a new federation trust certification that expires in year 2021. Exported that and imported into RKEX13CAS1. For some reason the old certificate in RKEX13CAS1 re-appeared and prevented us from going further in fixing the free/busy issue.  Waiting for Winoto to fix the certificate.

2. Microsoft support called back on issue #1. They suggested exporting and importing the public folder content from one server to another.
