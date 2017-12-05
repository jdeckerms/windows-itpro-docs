---
title: Configure exclusions for files opened by specific processes
description: You can exclude files from scans if they have been opened by a specific process.
keywords: process, exclusion, files, scans
search.product: eADQiWindows 10XVcnh
ms.pagetype: security
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: iaanw
ms.author: iawilt
ms.date: 06/13/2017
---

# Configure exclusions for files opened by processes

**Applies to:**

- Windows 10
- Windows Server 2016

**Audience**

- Enterprise security administrators


**Manageability available with**

- Group Policy
- PowerShell
- Windows Management Instrumentation (WMI)
- System Center Configuration Manager
- Microsoft Intune
- Windows Defender Security Center

You can exclude files that have been opened by specific processes from being scanned by Windows Defender AV. 

This topic describes how to configure exclusion lists for the following:

<a id="examples"></a>

Exclusion | Example 
---|---
Any file on the machine that is opened by any process with a specific file name | Specifying "test.exe" would exclude files opened by: <ul><li>c:\sample\test.exe</li><li>d:\internal\files\test.exe</li></ul>  
Any file on the machine that is opened by any process under a specific folder | Specifying "c:\test\sample\\*" would exclude files opened by:<ul><li>c:\test\sample\test.exe</li><li>c:\test\sample\test2.exe</li><li>c:\test\sample\utility.exe</li></ul> 
Any file on the machine that is opened by a specific process in a specific folder | Specifying "c:\test\process.exe" would exclude files only opened by c:\test\process.exe

When you add a process to the process exclusion list, Windows Defender AV will not scan files opened by that process, no matter where the files are located. The process itself, however, will be scanned unless it has also been added to the [file exclusion list](configure-extension-file-exclusions-windows-defender-antivirus.md).

The exclusions only apply to [always-on real-time protection and monitoring](configure-real-time-protection-windows-defender-antivirus.md). They do not apply to scheduled or on-demand scans.

Changes made via Group Policy to the exclusion lists **will show** in the lists in the [Windows Defender Security Center app](windows-defender-security-center-antivirus.md#exclusions). However, changes made in the Windows Defender Security Center app **will not show** in the Group Policy lists.

You can add, remove, and review the lists for exclusions in [Group Policy](#gp), [System Center Configuration Manager, Microsoft Intune, and with the Windows Defender Security Center app](#man-tools), and you can [use wildcards](#wildcards) to further customize the lists.

You can also [use PowerShell cmdlets and WMI to configure the exclusion lists](#ps), including [reviewing](#review) your lists. 


By default, local changes made to the lists (by users with administrator privileges; this includes changes made with PowerShell and WMI) will be merged with the lists as defined (and deployed) by Group Policy, Configuration Manager, or Intune. The Group Policy lists will take precedence in the case of conflicts. 

You can [configure how locally and globally defined exclusions lists are merged](configure-local-policy-overrides-windows-defender-antivirus.md#merge-lists) to allow local changes to override managed deployment settings.


## Configure the list of exclusions for files opened by specified processes


<a id="gp"></a>
**Use Group Policy to exclude files that have been opened by specified processes from scans:**

1.  On your Group Policy management machine, open the [Group Policy Management Console](https://technet.microsoft.com/library/cc731212.aspx), right-click the Group Policy Object you want to configure and click **Edit**.

3.  In the **Group Policy Management Editor** go to **Computer configuration**.

4.  Click **Policies** then **Administrative templates**.

5.  Expand the tree to **Windows components > Windows Defender Antivirus > Exclusions**. 


6. Double-click the **Process Exclusions** setting and add the exclusions:

    1. Set the option to **Enabled**. 
    2. Under the **Options** section, click **Show...**
    3. Enter each process on its own line under the **Value name** column. See the [example table](#examples) for the different types of process exclusions.  Enter **0** in the **Value** column for all processes.

7. Click **OK**. 

![The Group Policy setting for specifying process exclusions](images/defender/wdav-process-exclusions.png)


<a id="ps"></a>
**Use PowerShell cmdlets to exclude files that have been opened by specified processes from scans:**

Using PowerShell to add or remove exclusions for files that have been opened by processes requires using a combination of three cmdlets with the `-ExclusionProcess` parameter. The cmdlets are all in the [Defender module](https://technet.microsoft.com/en-us/itpro/powershell/windows/defender/defender).

The format for the cmdlets is:

```PowerShell
<cmdlet> -ExclusionProcess "<item>"
```

The following are allowed as the \<cmdlet>:

Configuration action | PowerShell cmdlet
---|---
Create or overwrite the list | `Set-MpPreference` 
Add to the list | `Add-MpPreference` 
Remove items from the list | `Remove-MpPreference` 


>[!IMPORTANT]
>If you have created a list, either with `Set-MpPreference` or `Add-MpPreference`, using the `Set-MpPreference` cmdlet again will overwrite the existing list. 


For example, the following code snippet would cause Windows Defender AV scans to exclude any file that is opened by the specified process:

```PowerShell
Add-MpPreference -ExclusionProcess "c:\internal\test.exe"
```


See [Use PowerShell cmdlets to configure and run Windows Defender Antivirus](use-powershell-cmdlets-windows-defender-antivirus.md) and [Defender cmdlets](https://technet.microsoft.com/itpro/powershell/windows/defender/index) for more information on how to use PowerShell with Windows Defender Antivirus.


**Use Windows Management Instruction (WMI) to exclude files that have been opened by specified processes from scans:**

Use the [ **Set**, **Add**, and **Remove** methods of the **MSFT_MpPreference**](https://msdn.microsoft.com/en-us/library/dn455323(v=vs.85).aspx) class for the following properties:

```WMI
ExclusionProcess
```

The use of **Set**, **Add**, and **Remove** is analogous to their counterparts in PowerShell: `Set-MpPreference`, `Add-MpPreference`, and `Remove-MpPreference`.

See the following for more information and allowed parameters:
- [Windows Defender WMIv2 APIs](https://msdn.microsoft.com/en-us/library/dn439477(v=vs.85).aspx)

<a id="man-tools"></a>
**Use Configuration Manager to exclude files that have been opened by specified processes from scans:**

See [How to create and deploy antimalware policies: Exclusion settings](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#exclusion-settings) for details on configuring System Center Configuration Manager (current branch).


**Use Microsoft Intune to exclude files that have been opened by specified processes from scans:**


See [Help secure Windows PCs with Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune) and [Windows Defender policy settings in Windows 10](https://docs.microsoft.com/en-us/intune/deploy-use/windows-10-policy-settings-in-microsoft-intune#windows-defender-1) for more details.


**Use the Windows Defender Security Center app to exclude files that have been opened by specified processes from scans:**

See [Add exclusions in the Windows Defender Security Center app](windows-defender-security-center-antivirus.md#exclusions) for instructions.



<a id="wildcards"></a>
## Use wildcards in the process exclusion list

The use of wildcards in the process exclusion list is different from their use in other exclusion lists.

In particular, you cannot use the question mark ? wildcard, and the asterisk \* wildcard can only be used at the end of a complete path. You can still use environment variables (such as %ALLUSERSPROFILE%) as wildcards when defining items in the process exclusion list.

The following table describes how the wildcards can be used in the process exclusion list:

Wildcard | Use | Example use | Example matches
---|---|---|---
\* (asterisk) | Replaces any number of characters | <ul><li>C:\MyData\\*</li></ul> | <ul><li>Any file opened by C:\MyData\file.exe</li></ul>
? (question mark) | Not available | \- | \-
Environment variables | The defined variable will be populated as a path when the exclusion is evaluated |  <ul><li>%ALLUSERSPROFILE%\CustomLogFiles\file.exe</li></ul> | <ul><li>Any file opened by C:\ProgramData\CustomLogFiles\file.exe</li></ul>




<a id="review"></a>
## Review the list of exclusions

You can retrieve the items in the exclusion list with PowerShell, [System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#exclusion-settings), [Intune](https://docs.microsoft.com/en-us/intune/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune), or the [Windows Defender Security Center app](windows-defender-security-center-antivirus.md#exclusions).

If you use PowerShell, you can retrieve the list in two ways:

- Retrieve the status of all Windows Defender AV preferences. Each of the lists will be displayed on separate lines, but the items within each list will be combined into the same line.
- Write the status of all preferences to a variable, and use that variable to only call the specific list you are interested in. Each use of `Add-MpPreference` is written to a new line.

**Review the list of exclusions alongside all other Windows Defender AV preferences:**

Use the following cmdlet:

```PowerShell
Get-MpPreference
```


See [Use PowerShell cmdlets to configure and run Windows Defender Antivirus](use-powershell-cmdlets-windows-defender-antivirus.md) and [Defender cmdlets](https://technet.microsoft.com/itpro/powershell/windows/defender/index) for more information on how to use PowerShell with Windows Defender Antivirus.


**Retrieve a specific exclusions list:**

Use the following code snippet (enter each line as a separate command); replace **WDAVprefs** with whatever label you want to name the variable:

```PowerShell
$WDAVprefs = Get-MpPreference
$WDAVprefs.ExclusionProcess
```



See [Use PowerShell cmdlets to configure and run Windows Defender Antivirus](use-powershell-cmdlets-windows-defender-antivirus.md) and [Defender cmdlets](https://technet.microsoft.com/itpro/powershell/windows/defender/index) for more information on how to use PowerShell with Windows Defender Antivirus.





## Related topics

- [Configure and validate exclusions in Windows Defender AV scans](configure-exclusions-windows-defender-antivirus.md)
- [Configure and validate exclusions based on file name, extension, and folder location](configure-extension-file-exclusions-windows-defender-antivirus.md)
- [Configure exclusions in Windows Defender AV on Windows Server](configure-server-exclusions-windows-defender-antivirus.md)
- [Customize, initiate, and review the results of Windows Defender AV scans and remediation](customize-run-review-remediate-scans-windows-defender-antivirus.md)
- [Windows Defender Antivirus in Windows 10](windows-defender-antivirus-in-windows-10.md)