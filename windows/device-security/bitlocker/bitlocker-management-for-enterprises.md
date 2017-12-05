---
title: BitLocker Management Recommendations for Enterprises (Windows 10)
description: This topic explains recommendations for managing BitLocker.
ms.assetid: 40526fcc-3e0d-4d75-90e0-c7d0615f33b2
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
localizationpriority: high
author: brianlic-msft
---

# BitLocker Management Recommendations for Enterprises

This topic explains recommendations for managing BitLocker, both on-premises using older hardware and cloud-based management of modern devices. 

## Forward-looking recommendations for managing BitLocker

The ideal for modern BitLocker management is to eliminate the need for IT admins to set management policies using tools or other mechanisms by having Windows perform tasks that it is more practical to automate. This vision leverages modern hardware developments. The growth of TPM 2.0, Secure Boot, and other hardware improvements, for example, has helped to alleviate the support burden on the helpdesk, and we are seeing a consequent decrease in support call volumes, yielding improved user satisfaction.

Therefore, we recommend that you upgrade your hardware so that your devices comply with Modern Standby or [Hardware Security Test Interface (HSTI)](https://msdn.microsoft.com/library/windows/hardware/mt712332.aspx) specifications to take advantage of their automated features, for example, when using Azure Active Directory (Azure AD). 

Though much  Windows BitLocker [documentation](bitlocker-overview.md) has been published, customers frequently ask for recommendations and pointers to specific, task-oriented documentation that is both easy to digest and focused on how to deploy and manage BitLocker. This article links to relevant documentation, products, and services to help answer this and other related frequently-asked questions, and also provides BitLocker recommendations for:

   - [Domain-joined computers](#dom_join)

   - [Devices joined to Azure Active Directory (Azure AD)](#azure_ad)

   - [Workplace-joined PCs and Phones](#work_join)

   - [Servers](#servers)

   - [Scripts](#powershell)

   <br />

## BitLocker management at a glance

| | PC – Old Hardware | PC – New* Hardware |[Servers](#servers)/[VMs](#VMs) | Phone 
|---|---|----|---|---|
|On-premises Domain-joined |[MBAM](#MBAM25)| [MBAM](#MBAM25) | [Scripts](#powershell) |N/A|
|Cloud-managed|[MDM](#MDM) |Auto-encryption|[Scripts](#powershell)|[MDM](#MDM)/EAS|

<br />
*PC hardware that supports Modern Standby or HSTI 

<br />
<br />

 <a id="dom_join"></a>
## Recommendations for domain-joined computers

Windows continues to be the focus for new features and improvements for built-in encryption management, for example, automatically enabling encryption on devices that support Modern Standby beginning with Windows 8.1. For more information, see  [Overview of BitLocker Device Encryption in Windows 10](bitlocker-device-encryption-overview-windows-10.md#bitlocker-device-encryption).

Companies that image their own computers using Microsoft System Center 2012 Configuration Manager SP1 (SCCM) or later can use an existing task sequence to [pre-provision BitLocker](https://technet.microsoft.com/library/hh846237.aspx#BKMK_PreProvisionBitLocker) encryption while in Windows Preinstallation Environment (WinPE) and can then [enable protection](https://technet.microsoft.com/library/hh846237.aspx#BKMK_EnableBitLocker). This can help ensure that computers are encrypted from the start, even before users receive them. As part of the imaging process, a company could also decide to use SCCM to pre-set any desired [BitLocker Group Policy](https://technet.microsoft.com/library/ee706521(v=ws.10).aspx).

For older client computers with BitLocker that are domain joined on-premises, Microsoft BitLocker Administration and Management<sup>[1]</sup> (MBAM) remains the best way to manage BitLocker. MBAM continues to be maintained and receives security patches. Using MBAM provides the following functionality:

- Encrypts device with BitLocker using MBAM
- Stores BitLocker Recovery keys in MBAM Server
- Provides Recovery key access to end-user, helpdesk and advanced helpdesk
- Provides Reporting on Compliance and Recovery key access audit

<a id="MBAM25"></a>
<sup>[1]</sup>The latest MBAM version is [MBAM 2.5](https://technet.microsoft.com/windows/hh826072.aspx) with Service Pack 1 (SP1).

<br />

<a id="azure_ad"></a>
## Recommendations for devices joined to Azure Active Directory

<a id="MDM"></a>

Devices joined to Azure Active Directory (Azure AD) are managed using Mobile Device Management (MDM) policy such as [Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune). BitLocker Device Encryption status can be queried from managed machines via the [Policy Configuration Settings Provider](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (CSP), which reports on whether BitLocker Device Encryption is enabled on the device. Compliance with BitLocker Device Encryption policy can be a requirement for [Conditional Access](https://www.microsoft.com/cloud-platform/conditional-access) to services like Exchange Online and SharePoint Online.

Starting with Windows 10 version 1703 (also known as the Windows Creators Update), the enablement of BitLocker can be triggered over MDM either by the [Policy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) or the [BitLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp). The BitLocker CSP adds policy options that go beyond ensuring that encryption has occurred, and is available on computers that run Windows 10 Business or Enterprise editions and on Windows Phones.

For hardware that is compliant with Modern Standby and HSTI, when using either of these features, BitLocker Device Encryption is automatically turned on whenever the user joins a device to Azure AD. Azure AD provides a portal where recovery keys are also backed up, so users can retrieve their own recovery key for self-service, if required. For older devices that are not yet encrypted, beginning with Windows 10 version 1703 (the Windows 10 Creators Update), admins can use the [BitLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp) to trigger encryption and store the recovery key in Azure AD.


<a id="work_join"></a>
## Workplace-joined PCs and phones

For Windows PCs and Windows Phones that enroll using **Connect to work or school account**, BitLocker Device Encryption is managed over MDM, and similarly for Azure AD domain join. 

<a id="servers"></a>

##  Recommendations for servers

Servers are often installed, configured, and deployed using PowerShell, so the recommendation is to also use [PowerShell to enable BitLocker on a server](bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker.md#a-href-idbkmk-blcmdletsabitlocker-cmdlets-for-windows-powershell), ideally as part of the initial setup. BitLocker is an Optional Component (OC) in Windows Server, so follow the directions in [BitLocker: How to deploy on Windows Server 2012 and later](bitlocker-how-to-deploy-on-windows-server.md) to add the BitLocker OC. 

The Minimal Server Interface is a prerequisite for some of the BitLocker administration tools. On a [Server Core](https://docs.microsoft.com/windows-server/get-started/getting-started-with-server-core) installation, you must add the necessary GUI components first. The steps to add shell components to Server Core are described in [Using Features on Demand with Updated Systems and Patched Images](https://blogs.technet.microsoft.com/server_core/2012/11/05/using-features-on-demand-with-updated-systems-and-patched-images/) and [How to update local source media to add roles and features](https://blogs.technet.microsoft.com/joscon/2012/11/14/how-to-update-local-source-media-to-add-roles-and-features/).  

If you are installing a server manually, such as a stand-alone server, then choosing [Server with Desktop Experience](https://docs.microsoft.com/windows-server/get-started/getting-started-with-server-with-desktop-experience) is the easiest path because you can avoid performing the steps to add a GUI to Server Core.

 Additionally, lights out data centers can take advantage of the enhanced security of a second factor while avoiding the need for user intervention during reboots by optionally using a combination of BitLocker (TPM+PIN) and BitLocker Network Unlock. BitLocker Network Unlock brings together the best of hardware protection, location dependence, and automatic unlock, while in the trusted location. For the configuration steps, see [BitLocker: How to enable Network Unlock](bitlocker-how-to-enable-network-unlock.md). 

 For more information, see the Bitlocker FAQs article and other useful links in [Related Articles](#articles).
 
<a id ="powershell"></a>

## PowerShell examples

For Azure AD-joined computers, including virtual machines, the recovery password should be stored in Azure Active Directory.  

*Example: Use PowerShell to add a recovery password and back it up to Azure AD before enabling BitLocker*
``` 
PS C:\>Add-BitLockerKeyProtector -MountPoint "C:" -RecoveryPasswordProtector

PS C:\>$BLV = Get-BitLockerVolume -MountPoint "C:”

PS C:\>BackupToAAD-BitLockerKeyProtector -MountPoint "C:" -KeyProtectorId $BLV.KeyProtector[0].KeyProtectorId
``` 
For domain-joined computers, including servers, the recovery password should be stored in Active Directory Domain Services (AD DS). 

*Example: Use PowerShell to add a recovery password and back it up to AD DS before enabling BitLocker*
``` 
PS C:\>Add-BitLockerKeyProtector -MountPoint "C:" -RecoveryPasswordProtector

PS C:\>$BLV = Get-BitLockerVolume -MountPoint "C:”

PS C:\>Backup-BitLockerKeyProtector -MountPoint "C:" -KeyProtectorId $BLV.KeyProtector[0].KeyProtectorId
 ```

Subsequently, you can use PowerShell to enable BitLocker. 

*Example: Use PowerShell to enable BitLocker with a TPM protector*
 ```
PS C:\>Enable-BitLocker -MountPoint "D:" -EncryptionMethod XtsAes256 -UsedSpaceOnly -TpmProtector 
 ```
*Example: Use PowerShell to enable BitLocker with a TPM+PIN protector, in this case with a PIN set to 123456*
 ```
PS C:\>$SecureString = ConvertTo-SecureString "123456" -AsPlainText -Force

PS C:\> Enable-BitLocker -MountPoint "C:" -EncryptionMethod XtsAes256 -UsedSpaceOnly -Pin $SecureString -TPMandPinProtector
  ``` 

<a id = "articles"></a>

## Related Articles

[BitLocker: FAQs](bitlocker-frequently-asked-questions.md)

[Microsoft BitLocker Administration and Management (MBAM)](https://technet.microsoft.com/windows/hh826072.aspx)

[Overview of BitLocker Device Encryption in Windows 10](bitlocker-device-encryption-overview-windows-10.md#bitlocker-device-encryption) 

[System Center 2012 Configuration Manager SP1](https://technet.microsoft.com/library/hh846237.aspx#BKMK_PreProvisionBitLocker) *(Pre-provision BitLocker task sequence)*

[Enable BitLocker task sequence](https://technet.microsoft.com/library/hh846237.aspx#BKMK_EnableBitLocker)

[BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521(v=ws.10).aspx) 

[Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) 
*(Overview)*

[Configuration Settings Providers](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)
*(Policy CSP: See [Security-RequireDeviceEncryption](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-policies))*

[BitLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)

<br />

**Windows Server setup tools**

[Windows Server Installation Options](https://technet.microsoft.com/library/hh831786(v=ws.11).aspx)

[How to update local source media to add roles and features](https://blogs.technet.microsoft.com/joscon/2012/11/14/how-to-update-local-source-media-to-add-roles-and-features/)

[How to add or remove optional components on Server Core](https://blogs.technet.microsoft.com/server_core/2012/11/05/using-features-on-demand-with-updated-systems-and-patched-images/) *(Features on Demand)*

[BitLocker: How to deploy on Windows Server 2012 and newer](bitlocker-how-to-deploy-on-windows-server.md)  

[BitLocker: How to enable Network Unlock](bitlocker-how-to-enable-network-unlock.md)

[Shielded VMs and Guarded Fabric](https://blogs.technet.microsoft.com/windowsserver/2016/05/10/a-closer-look-at-shielded-vms-in-windows-server-2016/) 

<br />

<a id="powershell"></a>
**Powershell**

[BitLocker cmdlets for Windows PowerShell](bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker.md#a-href-idbkmk-blcmdletsabitlocker-cmdlets-for-windows-powershell) 

[Surface Pro Specifications](https://www.microsoft.com/surface/support/surface-pro-specs)