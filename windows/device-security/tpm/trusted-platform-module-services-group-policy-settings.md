---
title: TPM Group Policy settings (Windows 10)
description: This topic describes the Trusted Platform Module (TPM) Services that can be controlled centrally by using Group Policy settings.
ms.assetid: 54ff1c1e-a210-4074-a44e-58fee26e4dbd
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
author: brianlic-msft
---

# TPM Group Policy settings

**Applies to**
-   Windows 10
-   Windows Server 2016

This topic describes the Trusted Platform Module (TPM) Services that can be controlled centrally by using Group Policy settings.

The Group Policy settings for TPM services are located at:

**Computer Configuration\\Administrative Templates\\System\\Trusted Platform Module Services\\**

The following Group Policy settings were introduced in Window 10:

## Configure the list of blocked TPM commands

This policy setting allows you to manage the Group Policy list of Trusted Platform Module (TPM) commands that are blocked by Windows.

If you enable this policy setting, Windows will block the specified commands from being sent to the TPM on the computer. TPM commands are referenced by a command number. For example, command number 129 is **TPM\_OwnerReadInternalPub**, and command number 170 is **TPM\_FieldUpgrade**. To find the command number that is associated with each TPM command, at the command prompt, type **tpm.msc** to open the TPM Management Console and navigate to the **Command Management** section.

If you disable or do not configure this policy setting, only those TPM commands that are specified through the default or local lists can be blocked by Windows. The default list of blocked TPM commands is preconfigured by Windows.

-   You can view the default list by typing **tpm.msc** at the command prompt, navigating to the **Command Management** section, and exposing the **On Default Block List** column.

-   The local list of blocked TPM commands is configured outside of Group Policy by running the TPM Management Console or scripting using the **Win32\_Tpm** interface.

For information how to enforce or ignore the default and local lists of blocked TPM commands, see

-   [Ignore the default list of blocked TPM commands](#ignore-the-default-list-of-blocked-tpm-commands)

-   [Ignore the local list of blocked TPM commands](#ignore-the-local-list-of-blocked-tpm-commands)

## Ignore the default list of blocked TPM commands

This policy setting allows you to enforce or ignore the computer's default list of blocked Trusted Platform Module (TPM) commands.

The default list of blocked TPM commands is preconfigured by Windows. You can view the default list by typing **tpm.msc** at the command prompt to open the TPM Management Console, navigating to the **Command Management** section, and exposing the **On Default Block List** column. Also see the related policy setting, [Configure the list of blocked TPM commands](#configure-the-list-of-blocked-tpm-commands).

If you enable this policy setting, the Windows operating system will ignore the computer's default list of blocked TPM commands, and it will block only those TPM commands that are specified by Group Policy or the local list.

If you disable or do not configure this policy setting, Windows will block the TPM commands in the default list, in addition to the commands that are specified by Group Policy and the local list of blocked TPM commands.

## Ignore the local list of blocked TPM commands

This policy setting allows you to enforce or ignore the computer's local list of blocked Trusted Platform Module (TPM) commands.

The local list of blocked TPM commands is configured outside of Group Policy by typing **tpm.msc** at the command prompt to open the TPM Management Console, or scripting using the **Win32\_Tpm** interface. (The default list of blocked TPM commands is preconfigured by Windows.) Also see the related policy setting, [Configure the list of blocked TPM commands](#configure-the-list-of-blocked-tpm-commands).

If you enable this policy setting, the Windows operating system will ignore the computer's local list of blocked TPM commands, and it will block only those TPM commands that are specified by Group Policy or the default list.

If you disable or do not configure this policy setting, Windows will block the TPM commands in the local list, in addition to the commands that are specified in Group Policy and the default list of blocked TPM commands.

## Configure the level of TPM owner authorization information available to the operating system

This policy setting configures how much of the TPM owner authorization information is stored in the registry of the local computer. Depending on the amount of TPM owner authorization information that is stored locally, the Windows operating system and TPM-based applications can perform certain actions in the TPM that require TPM owner authorization without requiring the user to enter the TPM owner password.

> [!IMPORTANT]
> This policy setting is not available in the Windows 10, version 1607 and Windows Server 2016 and later versions of the ADMX files.

There are three TPM owner authentication settings that are managed by the Windows operating system. You can choose a value of **Full**, **Delegate**, or **None**.

-   **Full**   This setting stores the full TPM owner authorization, the TPM administrative delegation blob, and the TPM user delegation blob in the local registry. With this setting, you can use the TPM without requiring remote or external storage of the TPM owner authorization value. This setting is appropriate for scenarios that do not require you to reset the TPM anti-hammering logic or change the TPM owner authorization value. Some TPM-based applications may require that this setting is changed before features that depend on the TPM anti-hammering logic can be used.

-   **Delegated**   This setting stores only the TPM administrative delegation blob and the TPM user delegation blob in the local registry. This setting is appropriate for use with TPM-based applications that depend on the TPM antihammering logic. This is the default setting in Windows.

-   **None**   This setting provides compatibility with previous operating systems and applications. You can also use it for scenarios when TPM owner authorization cannot be stored locally. Using this setting might cause issues with some TPM-based applications.

> [!NOTE]
> If the operating system managed TPM authentication setting is changed from **Full** to **Delegated**, the full TPM owner authorization value will be regenerated, and any copies of the previously set TPM owner authorization value will be invalid.

**Registry information**

Registry key: HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\TPM

DWORD: OSManagedAuthLevel

The following table shows the TPM owner authorization values in the registry.

| Value Data | Setting   |
|------------|-----------|
| 0          | None      |
| 2          | Delegated |
| 4          | Full      |

 
If you enable this policy setting, the Windows operating system will store the TPM owner authorization in the registry of the local computer according to the TPM authentication setting you choose.

If you disable or do not configure this policy setting, and the **Turn on TPM backup to Active Directory Domain Services** policy setting is also disabled or not configured, the default setting is to store the full TPM authorization value in the local registry. If this policy is disabled or not
configured, and the **Turn on TPM backup to Active Directory Domain Services** policy setting is enabled, only the administrative delegation and the user delegation blobs are stored in the local registry.

## Standard User Lockout Duration

This policy setting allows you to manage the duration in minutes for counting standard user authorization failures for Trusted Platform Module (TPM) commands requiring authorization. An authorization failure occurs each time a standard user sends a command to the TPM and receives an error response that indicates an authorization failure occurred. Authorization failures that are older than the duration you set are ignored. If the number of TPM commands with an authorization failure within the lockout duration equals a threshold, a standard user is prevented from sending commands that require
authorization to the TPM.

The TPM is designed to protect itself against password guessing attacks by entering a hardware lockout mode when it receives too many commands with an incorrect authorization value. When the TPM enters a lockout mode, it is global for all users (including administrators) and for Windows features such as BitLocker Drive Encryption.

This setting helps administrators prevent the TPM hardware from entering a lockout mode by slowing the speed at which standard users can send commands that require authorization to the TPM.

For each standard user, two thresholds apply. Exceeding either threshold prevents the user from sending a command that requires authorization to the TPM. Use the following policy settings to set the lockout duration:

-   [Standard User Individual Lockout Threshold](#standard-user-individual-lockout-threshold)   This value is the maximum number of authorization failures that each standard user can have before the user is not allowed to send commands that require authorization to the TPM.

-   [Standard User Total Lockout Threshold](#standard-user-total-lockout-threshold)   This value is the maximum total number of authorization failures that all standard users can have before all standard users are not allowed to send commands that require authorization to the TPM.

An administrator with the TPM owner password can fully reset the TPM's hardware lockout logic by using the TPM Management Console (tpm.msc). Each time an administrator resets the TPM's hardware lockout logic, all prior standard user TPM authorization failures are ignored. This allows standard users to immediately use the TPM normally.

If you do not configure this policy setting, a default value of 480 minutes (8 hours) is used.

## Standard User Individual Lockout Threshold

This policy setting allows you to manage the maximum number of authorization failures for each standard user for the Trusted Platform Module (TPM). This value is the maximum number of authorization failures that each standard user can have before the user is not allowed to send commands that require authorization to the TPM. If the number of authorization failures for the user within the duration that is set for the **Standard User Lockout Duration** policy setting equals this value, the standard user is prevented from sending commands that require authorization to the Trusted Platform Module (TPM).

This setting helps administrators prevent the TPM hardware from entering a lockout mode by slowing the speed at which standard users can send commands that require authorization to the TPM.

An authorization failure occurs each time a standard user sends a command to the TPM and receives an error response indicating an authorization failure occurred. Authorization failures older than the duration are ignored.

An administrator with the TPM owner password can fully reset the TPM's hardware lockout logic by using the TPM Management Console (tpm.msc). Each time an administrator resets the TPM's hardware lockout logic, all prior standard user TPM authorization failures are ignored. This allows standard users to immediately use the TPM normally.

If you do not configure this policy setting, a default value of 4 is used. A value of zero means that the operating system will not allow standard users to send commands to the TPM, which might cause an authorization failure.

## Standard User Total Lockout Threshold

This policy setting allows you to manage the maximum number of authorization failures for all standard users for the Trusted Platform Module (TPM). If the total number of authorization failures for all standard users within the duration that is set for the **Standard User Lockout Duration** policy equals this value, all standard users are prevented from sending commands that require authorization to the Trusted Platform Module (TPM).

This setting helps administrators prevent the TPM hardware from entering a lockout mode because it slows the speed standard users can send commands requiring authorization to the TPM.

An authorization failure occurs each time a standard user sends a command to the TPM and receives an error response indicating an authorization failure occurred. Authorization failures older than the duration are ignored.

An administrator with the TPM owner password can fully reset the TPM's hardware lockout logic by using the TPM Management Console (tpm.msc). Each time an administrator resets the TPM's hardware lockout logic, all prior standard user TPM authorization failures are ignored. This allows standard users to immediately use the TPM normally.

If you do not configure this policy setting, a default value of 9 is used. A value of zero means that the operating system will not allow standard users to send commands to the TPM, which might cause an authorization failure.

> [!IMPORTANT]
> The **Turn on TPM backup to Active Directory Domain Services** is not available in the Windows 10, version 1607 and Windows Server 2016 and later versions of the ADMX files.

If you enable this policy setting, TPM owner information will be automatically and silently backed up to AD DS when you use Windows to set or change a TPM owner password. When this policy setting is enabled, a TPM owner password cannot be set or changed unless the computer is connected to the domain and the AD DS backup succeeds.

If you disable or do not configure this policy setting, TPM owner information will not be backed up to AD DS.

## Configure the system to use legacy Dictionary Attack Prevention Parameters setting for TPM 2.0

Introduced in Windows 10, version 1703, this policy setting configures the TPM to use the Dictionary Attack Prevention Parameters (lockout threshold and recovery time) to the values that were used for Windows 10 Version 1607 and below. 

> [!IMPORTANT]
> Setting this policy will take effect only if:  
-   The TPM was originally prepared using a version of Windows after Windows 10 Version 1607
-   The system has a TPM 2.0. 

> [!NOTE]
> Enabling this policy will only take effect after the TPM maintenance task runs (which typically happens after a system restart). Once this policy has been enabled on a system and has taken effect (after a system restart), disabling it will have no impact and the system's TPM will remain configured using the legacy Dictionary Attack Prevention parameters, regardless of the value of this group policy. The only ways for the disabled setting of this policy to take effect on a system where it was once enabled are to either:
> -  Disable it from group policy
> -  Clear the TPM on the system


## Related topics

- [Trusted Platform Module](trusted-platform-module-top-node.md) (list of topics)
- [TPM Cmdlets in Windows PowerShell](http://technet.microsoft.com/library/jj603116.aspx)
- [Prepare your organization for BitLocker: Planning and Policies - TPM configurations](https://technet.microsoft.com/itpro/windows/keep-secure/prepare-your-organization-for-bitlocker-planning-and-policies#bkmk-tpmconfigurations)