---
layout: post 
title:  "Exchange Cross Forest Migration Annotations" 
date:   2017-04-27T16:44
categories: exchange migration crossforest activedirectory
link: http://bertmueller18.github.io/
tags:
  - links
ogtype: article 
---
## [Exchange inter-forest migration tips](http://www.hayesjupe.com/exchange-interforest-migration-tips/)
Forest, including exchange, migrations seemed to be something I was doing every month back in the Exchange 2000/2003 days, but then they seemed to stop…. For a while.

## [Exchange 2010 Cross-Forest Migration Step by Step Guide – Part I](https://blogs.technet.microsoft.com/meamcs/2011/06/10/exchange-2010-cross-forest-migration-step-by-step-guide-part-i/)
This Guide will explain the detailed steps required to do cross forest migration from source forest running Exchange 2003 to target forest running Exchange 2010.

Active Directory Migration Tool (ADMT) will be used to migrate user accounts as well as computer accounts. There are two scenarios when using ADMT to migrate user accounts with Exchange


## [Exchange 2010 Cross-Forest Migration Step by Step Guide – Part II](https://blogs.technet.microsoft.com/meamcs/2011/10/25/exchange-2010-cross-forest-migration-step-by-step-guide-part-ii/)

In Part I of this guide I’ve explained the process of cross-forest migration and the differences between using ADMT first or using Prepare-MoveReuqest.Ps1 script first, I’ve also explained the migration scenario and the current environment.

Starting from this part we will talk about migration challenges and the best way to address these challenges.

## [Exchange 2010, 2013, 2016 Cross Forest Remote PowerShell](https://markgossa.blogspot.de/2015/10/exchange-2010-2013-cross-forest-remote-powershell.html)
If you are attempting a remote PowerShell connection to an Exchange server cross forest (no forest trust) using the method here, you will get the below error:

Connecting to remote server [server] failed with the following error message: WinRM cannot process the request. The following error with errorcode 0x80090311 occurred while using Kerberos authentication: There are currently no logon servers available to service the logon request.
 
## [Cross Forest E2K3 to 2010 Mailbox Migration with linked Mailboxes](http://msexchangeguru.com/2011/08/29/migration/)

Source and Target forest have one way trust
All CAS, HT and MBX servers are installed
All certificated are installed
Send and Receive connectors are configured
Accepted domain and email address policy is configured.
Disclaimer and any other exchange compliance or security rule configured.
Antivirus and antispam are installed and configured.
All the required ports are open between Exchange 2003 server to Exchange 2010 server
Post migration users and mailboxes will be in a separate resource and exchange forest environment.

## [Exchange 2013: Cross Forest/ORG Migration from Exchange 2010/2007](http://msexchangeguru.com/2013/11/03/e2013crossforestmigration/)
Cross forest migration steps blog was long time due from us. So here we go!

Cross forest has changed little bit and requires 3rd party cert in the source domain. 

Some related blogs which can be useful before doing cross forest migration:

Exchange 2013 Design Guide (http://msexchangeguru.com/2013/07/30/exchange-2013-planning-and-design-guide/)

Exchange 2013 Migration Guide  (http://msexchangeguru.com/2013/05/10/exchange2013-migration/)

Cross Forest E2K3 to 2010 Mailbox Migration with Linked Mailboxes  (http://msexchangeguru.com/2011/08/29/migration/)

Exchange 2013 PF Migration Guide  (http://msexchangeguru.com/2013/04/18/exchange2013-public-folders/)

Cross Forest Migration Guide – Exchange 2010 to Exchange 2010  (http://www.careexchange.in/cross-forest-migration-guide-exchange-2010-to-exchange-2010/)
Cross forest Move Mailbox in Bulk – Exchange2010 to Exchange 2010  (http://www.careexchange.in/cross-forest-move-mailbox-in-bulk-exchange2010-to-exchange-2010/)

(https://blog.jasonsherry.net/2013/08/29/script-export-groups-vbs-for-exchange-cross-forest-migrations/)

## [Distributiongroups export](http://blogs.catapultsystems.com/thernandez/archive/2015/09/16/migrate-distribution-groups-from-exchange-on-premise-to-exchange-online/)
#Get all groups into temp variable
$groups = Get-DistributionGroup -ResultSize Unlimited -IgnoreDefaultScope

#Export 1) ON-PREM export all distribution groups and a few settings
````powershell
$groups | Select-Object RecipientTypeDetails,Name,Alias,DisplayName,PrimarySmtpAddress,@{name="SMTPDomain";expression={$_.PrimarySmtpAddress.Domain}},MemberJoinRestriction,MemberDepartRestriction,RequireSenderAuthenticationEnabled,@{Name="ManagedBy";Expression={$_.ManagedBy -join “;”}},@{name=”AcceptMessagesOnlyFrom”;expression={$_.AcceptMessagesOnlyFrom -join “;”}},@{name=”AcceptMessagesOnlyFromDLMembers”;expression={$_.AcceptMessagesOnlyFromDLMembers -join “;”}},@{name=”AcceptMessagesOnlyFromSendersOrMembers”;expression={$_.AcceptMessagesOnlyFromSendersOrMembers -join “;”}},@{name=”ModeratedBy”;expression={$_.ModeratedBy -join “;”}},@{name=”BypassModerationFromSendersOrMembers”;expression={$_.BypassModerationFromSendersOrMembers -join “;”}},@{Name="GrantSendOnBehalfTo";Expression={$_.GrantSendOnBehalfTo -join “;”}},ModerationEnabled,SendModerationNotifications,LegacyExchangeDN,@{Name="EmailAddresses";Expression={$_.EmailAddresses -join “;”}} | Export-Csv C:\temp\dg\distributiongroups.csv -NoTypeInformation
````

#Export 2) ON-PREM export distribution groups’ smtp aliases
````powershell
$groups | Select-Object RecipientTypeDetails,PrimarySmtpAddress -ExpandProperty emailaddresses | select RecipientTypeDetails,PrimarySmtpAddress, @{name="TYPE";expression={$_}} | Export-Csv C:\temp\dg\distributiongroups-SMTPproxy.csv -NoTypeInformation
````

#Export 3) ON-PREM export all distribution groups and members (and member type)
````powershell
$groups |% {$guid=$_.Guid;$GroupType=$_.RecipientTypeDetails;$Name=$_.Name;$SMTP=$_.PrimarySmtpAddress ;Get-DistributionGroupMember -Identity $guid.ToString() -ResultSize Unlimited | Select-Object @{name=”GroupType”;expression={$GroupType}},@{name=”Group”;expression={$name}},@{name=”GroupSMTP”;expression={$SMTP}},@{name="PrimarySMTPDomain";expression={$SMTP.Domain}},@{Label="Member";Expression={$_.Name}},@{Label="MemberSMTP";Expression={$_.PrimarySmtpAddress}},@{Label="MemberType";Expression={$_.RecipientTypeDetails}}} | Export-Csv C:\temp\dg\distributiongroups-and-members.csv -NoTypeInformation
````

## [PowerShell-Remoteverbindung mit Exchange Server 2013 / 2016 herstellen](https://community.certbase.de/blogs/mg/archive/2016/03/03/PowerShell_2D00_Remoteverbindung-mit-Exchange-Server-2013-und-2016-herstellen.aspx)
Mit der PowerShell eine Remoteverbindung zu einem entfernten Exchange Server herstellen ist schnell gemacht, sofern man denn die erforderlichen Schritte parat. Im Fall der Fälle hilft die folgende Kurzübersicht.

### Exchange Management Shell ist lokal installiert

Wenn die Exchange Management Shell lokal installiert ist, können Sie die beiden folgenden Zeilen verwenden, um die Exchange PowerShell Cmdlets in die Windows PowerShell oder die Windows PowerShell ISE zu laden und anschließend eine Verbindung mit einem Remoteserver herzustellen:
````powershell
Import-Module -Name "C:\Program Files\Microsoft\Exchange Server\V15\Bin\RemoteExchange.ps1"
Connect-ExchangeServer -ServerFqdn remoteserver.domaene.tld -ClientApplication:ManagementShell
````
Der Verzeichnispfad zum Skript RemoteExchange.ps1 gilt für eine Standardinstallation von Exchange Server 2013.

### Exchange Management Shell ist nicht lokal installiert

Wenn die Exchange Management Shell nicht lokal installiert ist können Sie mit den folgenden Befehlen eine Remotesitzung erstellen:
````powershell
$Cred = Get-Credential
$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://remoteserver.domaene.tld/PowerShell/ -Authentication Kerberos -Credential $Cred
Import-PSSession $Session
````
Um die PowerShell Sitzung zu trennen geben Sie folgendes ein:
````powershell
Remove-PSSession $Session
````
## [How to Migrate Distribution Groups Across a Forest – Random Technical Artices By Sachin Filinto](https://blogs.technet.microsoft.com/sachinf/2014/03/17/how-to-migrate-distribution-groups-across-a-forest/)

## [Configure Application Impersonation for Exchange 2010 in Resource Forest](http://port25guy.com/2012/10/23/configure-application-impersonation-for-exchange-2010-in-resource-forest/)

## [Impersonation: To be, or pretend to be](https://eightwone.com/2014/08/13/application-impersonation-to-be-or-pretend-to-be/)

With the new Exchange 2010 RBAC model, one of the configuration changes is regards to EWS and Application Impersonation.  Instead of defining the ACL’s directly, you configure roles for the appropriate permissions.

If your in a resource forest setup, things are a little different.  Here are the steps.

Your service account, named ServiceAccount needs to be assigned Application Impersonation rights to all the accounts in the Accounting OU.  The user accounts are in client.corp and the Exchange mailboxes are stored in exchange.corp and there is a forest trust between the two.

## [Understanding multiple-forest permissions](https://technet.microsoft.com/en-us/library/dd298099(v=exchg.150).aspx#Boundary)

Many organizations deploy multiple forests to create security boundaries within their organizations. Using multiple forests helps administrators to define these security boundaries to better match their requirements, whether that's ensuring the fewest number of people have access to resources, or segmenting divisions within an organization.
Microsoft Exchange Server 2013 supports two types of multiple forest topologies:

Cross-forest   Cross-forest topologies can have multiple forests, each with their own installation of Exchange.

Resource forest   Resource forest topologies have an Exchange forest and one or more accounts forests.

## [Create linked role groups that mirror built-in role groups](https://technet.microsoft.com/en-us/library/dd876918(v=exchg.150).aspx)
Using linked management role groups in Microsoft Exchange Server 2013, you can link a role group in an Exchange 2013 resource forest with a universal security group (USG) in a foreign user forest. This is useful when you want administrators with accounts in the user forest to manage the servers running Exchange in the resource forest. For more information about linked role groups, see Understanding management role groups.

By default, Exchange 2013 includes a number of built-in role groups that provide you with permissions to manage a variety of features and job functions. Each role group is tailored to provide specific permissions for each feature and job function. However, these role groups can't be linked to USGs in a foreign forest. They can only contain users and USGs from the local resource forest. Fortunately, it's possible to replicate these built-in role groups using linked role groups.

## [Linked Mailbox in Exchange Server 2013 – Part 1](http://msexchangeteam.in/linked-mailbox-in-exchange-server-2013-part-1-2/)
## [Linked Mailbox in Exchange Server 2013 – Part 2](http://msexchangeteam.in/linked-mailbox-in-exchange-server-2013-part-2/)
## [Linked Mailbox in Exchange Server 2013 – Part 3](http://msexchangeteam.in/linked-mailbox-in-exchange-server-2013-part-3/)
## [Linked Mailbox in Exchange Server 2013 – Part 4](http://msexchangeteam.in/linked-mailbox-in-exchange-server-2013-part-4/)

In this blog series we will be learning how to create linked mailbox in Exchange Server 2013. First let me explain what is linked mailbox. Linked Mailbox was first introduced in Exchange Server 2003. Configuring linked mailbox in 2003 was little difficult and time consuming. In Exchange Server 2007 and 2010 it was upgraded and we had EMC and EMS to manage linked mailbox. Exchange Server 2013 has brought some additional features which is awesome. Linked Mailbox was introduced to reduce the extra effort put by an Administrator.

## [Granting Mailbox Full Access via Groups and keeping the Automapping feature in Exchange 2010](https://dirteam.com/dave/2012/01/09/granting-mailbox-full-access-via-groups-and-keeping-the-automapping-feature-in-exchange-2010/)
Since Exchange 2010 Service Pack 1 a new feature was added for Outlook 2007 and 2010 users, namely Automapping. When a mailbox user has Full Access on another mailbox, it will be automatically mapped in Outlook. No need for the user to go trough menus to find the additional mailbox screen. It’s a small addition but I know that users and your service desk will appreciate this.

There is one catch I came across, namely automapping does not work when the Full Access permission is granted via a security group. The mailbox is however accessible, but there is no automatic mapping in Outlook.

## Export all SMTP addresses from Exchange using PowerShell
Tested with Exchange 2010. You'll need Exchange Management shell but no need for exchange admin rights.

Get-Recipient -ResultSize unlimited | Select Name -ExpandProperty EmailAddresses | Where-Object {$_.SmtpAddress -ne $null} | Select Name,SmtpAddress,IsPrimaryAddress | Export-csv -Encoding unicode -NoTypeInformation AllEmailAddress.csv

## [SID HISTORY: Fixing Exchange](http://blog.asiantuntijakaveri.fi/2014/07/sid-history-fixing-exchange.html)
Dumping my notes about fixing SID history at work. Use at your own risk. These worked for me but won't work for you without some adjustments.
Locate and repair AD user accounts with acl inheritance flag uncheck. This prevents Exchange service accounts from altering user object and breaks various admin tools. 

## [Die Service Connection Points (SCPs) abfragen](http://blog.dikmenoglu.de/2010/12/die-service-connection-points-scps-abfragen/)

Yusuf Dikmenoglu 5. Dezember 2010 0
Möchte man im Active Directory Informationen über einen Dienst der innerhalb einer Domäne zur Verfügung stehen soll veröffentlichen, so benötigt man ein Service Connection Point (SCP) Objekt. Ein SCP wird bei der Installation von vielen Applikation automatisch, ohne das Zutun des Administrators erstellt. Die SCPs gehören zur Klasse serviceConnectionPoint, die wiederum von der Klasse connectionPoint abgeleitet ist.


Beispielsweise wird bei der Installation von Remotedesktoplizenzierung, Remote-Installation-Services, Hyper-V, Microsoft basierte virtuelle Maschinen, MS Virtual Machine Manager, der Autodiscover-Funktion ab Exchange 2007 etc. ein SCP im AD erstellt. Diese und viele anderen Dienste veröffentlichen ihr Dasein in der Domäne, durch das Erstellen von SCPs. ADAM / AD LDS stellt dabei keine Ausnahme dar. Client-Anwendungen wiederum verwenden SCPs, um den entsprechenden Dienst in der Domäne zu finden und um sich mit diesem zu verbinden.


Get-ADObject -LDAPFilter “(objectClass=serviceConnectionPoint)” | Select distinguishedName | FT -A –Wrap

Get-ADObject -LDAPFilter “(objectClass=serviceConnectionPoint)” -Searchbase “CN=Configuration,DC=Root-Domäne” | Select distinguishedName | FT -A -Wrap

## Mailboxen durchsuchen und Ergebnisse mailen

search-mailbox -identity user@mail.org -searchquery 'thema:"*blabal*"' oder 'empfangen:17.05.2017'
