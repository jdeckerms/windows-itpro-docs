---
title: Specify cloud-delivered protection level in Windows Defender Antivirus
description: Set the aggressiveness of cloud-delivered protection in Windows Defender Antivirus.
keywords: windows defender antivirus, antimalware, security, defender, cloud, aggressiveness, protection level
search.product: eADQiWindows 10XVcnh
ms.pagetype: security
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: iaanw
ms.author: iawilt
ms.date: 08/25/2017
---

# Specify the cloud-delivered protection level



**Applies to:**

- Windows 10, version 1703

**Audience**

- Enterprise security administrators

**Manageability available with**

- Group Policy
- System Center Configuration Manager (current branch)

You can specify the level of cloud-protection offered by Windows Defender Antivirus with Group Policy and System Center Configuration Manager.

>[!NOTE] 
>The Windows Defender Antivirus cloud service is a mechanism for delivering updated protection to your network and endpoints. Although it is called a cloud service, it is not simply protection for files stored in the cloud, rather it uses distributed resources and machine learning to deliver protection to your endpoints at a rate that is far faster than traditional signature updates.



**Use Group Policy to specify the level of cloud-delivered protection:**

1.  On your Group Policy management machine, open the [Group Policy Management Console](https://technet.microsoft.com/library/cc731212.aspx), right-click the Group Policy Object you want to configure and click **Edit**.

3.  In the **Group Policy Management Editor** go to **Computer configuration**. 

4.  Click **Policies** then **Administrative templates**.

5.  Expand the tree to **Windows components > Windows Defender Antivirus > MpEngine**.

1.  Double-click the **Select cloud protection level** setting and set it to **Enabled**. Select the level of protection:  
    1.  Setting to **Default Windows Defender Antivirus blocking level** will provide strong detection without increasing the risk of detecting legitimate files.  
    2.  Setting to **High blocking level** will apply a strong level of detection. While unlikely, some legitimate files may be detected (although you will have the option to unblock or dispute that detection). 
 
1. Click **OK**.

  
**Use Configuration Manager to specify the level of cloud-delivered protection:**

1.  See [How to create and deploy antimalware policies: Cloud-protection service](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service) for details on configuring System Center Configuration Manager (current branch).




## Related topics

- [Windows Defender Antivirus in Windows 10](windows-defender-antivirus-in-windows-10.md)
- [Enable cloud-delivered protection](enable-cloud-protection-windows-defender-antivirus.md)
- [How to create and deploy antimalware policies: Cloud-protection service](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)


