---
title: "Enable the users for Enterprise Voice on premises"
ms.reviewer: 
ms.author: crowe
author: CarolynRowe
manager: serdars
ms.date: 2/15/2018
audience: ITPro
ms.topic: conceptual
ms.prod: skype-for-business-itpro
f1.keywords:
- NOCSH
ms.localizationpriority: medium
ms.collection:
- Ent_O365_Hybrid
- IT_Skype16
- IT_Skype4B_Hybrid
- Strat_SB_Hybrid
ms.custom: 
ms.assetid: 4598565a-c228-4265-ad03-d2aef95b31a0
description: "For a user to use Phone System (Cloud PBX), you must first enable them for Enterprise Voice and assign them a phone number. You do this using your on-premises deployment while the user is still homed in the on-premises deployment."
---

# Enable the users for Enterprise Voice on premises
 
For a user to use Phone System (Cloud PBX), you must first enable them for Enterprise Voice and assign them a phone number. You do this using your on-premises deployment while the user is still homed in the on-premises deployment.

> [!Important]
> Skype for Business Online will be retired on July 31, 2021 after which the service will no longer be accessible.  In addition, PSTN connectivity between your on-premises environment whether through Skype for Business Server or Cloud Connector Edition and Skype for Business Online will no longer be supported.  Learn how to connect your on-premises telephony network to Teams using [Direct Routing](/MicrosoftTeams/direct-routing-landing-page).
  
### To enable a user for Enterprise Voice on premises and assign a phone number

1. From a user account that is assigned to the CsUserAdministrator role or the CsAdministrator role, log on to any computer in your internal deployment.
    
2. Use the Start menu or desktop shortcut to open the Skype for Business Server Control Panel.
    
    You can also open a browser window, and then enter the Administrator URL to open the Skype for Business Server Control Panel.
    
3. In the left navigation bar, click **Users**.
    
4. In the **Search users** box, type all or the first portion of the display name, first name, last name, Security Accounts Manager (SAM) account name, SIP address, or line Uniform Resource Identifier (URI) of the user account that you want to enable, and then click **Find**.
    
5. In the table, click the Skype for Business Online user account that you want to enable for Enterprise Voice.
    
6. On the **Edit** menu, click **Show Details**.
    
7. Under **Telephony**, click **Enterprise Voice**.
    
8. Click **Line URI**, and type a unique, normalized phone number (for example, `tel:+14255550200`). Then click **Commit**.
    
## Special considerations when enabling users for Enterprise Voice on premises

In some cases, you may need to modify the way you enable users for Enterprise Voice to make sure that they can successfully make and receive calls. If you have users in your deployment that meet the following conditions, perform the steps included to enable the user for Enterprise Voice.
  
- If a user is created in your on-premises AD and then synchronized with Skype for Business Online without being enabled for Skype for Business or for Enterprise Voice and do not have a LineURI set, run the following cmdlets for each affected user, replacing the values in \< \> with actual values for your environment:
    
  ```powershell
  Enable-CsUser $username -HostingProvider sipfed.online.lync.com -SipAddress sip:<UserName>@<SIP Domain>
  ```

  ```powershell
  Set-CsUser $username -EnterpriseVoiceEnabled $true -LineUri "tel:+<Telephone Number>"
  ```

- If a user is already enabled for Skype for Business on premises, but was not enabled for Enterprise Voice or assigned a LineURI before being moved to Skype for Business Online, run the following cmdlet for each user:
    
  ```powershell
  Set-CsUser $username -EnterpriseVoiceEnabled $true -LineUri "tel:+<Telephone Number>"
  ```

- If a user is already enabled in Skype for Business on premises but not enabled for Enterprise Voice, even if already assigned a LineURI, run the following cmdlet for each affected user:
    
  ```powershell
  Set-CsUser $username -EnterpriseVoiceEnabled $true
  ```