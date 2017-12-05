---
title: Use the command line to manage Windows Defender AV
description: Windows Defender AV has a dedicated command-line utility that can run scans and configure protection.
keywords: run windows defender scan, run antivirus scan from command line, run windows defender scan from command line, mpcmdrun, defender
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


# Use the mpcmdrun.exe command-line tool to configure and manage Windows Defender Antivirus

**Applies to:**

- Windows 10

**Audience**

- Enterprise security administrators


You can use a dedicated command-line tool to perform various functions in Windows Defender Antivirus. 

This utility can be useful when you want to automate the use of Windows Defender Antivirus. 

The utility is available in _%ProgramFiles%\Windows Defender\MpCmdRun.exe_ and must be run from a command prompt.

> [!NOTE]
> You may need to open an administrator-level version of the command prompt. Right-click the item in the Start menu, click **Run as administrator** and click **Yes** at the permissions prompt.


The utility has the following commands:

```DOS
MpCmdRun.exe [command] [-options]
```

Command | Description 
:---|:---
\- ? **or** -h | Displays all available options for the tool
\-Scan [-ScanType #] [-File <path> [-DisableRemediation] [-BootSectorScan]][-Timeout <days>] | Scans for malicious software
\-Trace  [-Grouping #] [-Level #]| Starts diagnostic tracing
\-GetFiles | Collects support information
\-RemoveDefinitions [-All] | Restores the installed signature definitions to a previous backup copy or to the original default set of signatures
\-AddDynamicSignature [-Path] | Loads a dynamic signature
\-ListAllDynamicSignature [-Path] | Lists the loaded dynamic signatures
\-RemoveDynamicSignature [-SignatureSetID] | Removes a dynamic signature
\-ValidateMapsConnection | Used to validate connection to the [cloud-delivered protection service](configure-network-connections-windows-defender-antivirus.md)
\-SignatureUpdate [-UNC [-Path <path>]] | Checks for new definition updates




## Related topics

- [Reference topics for management and configuration tools](configuration-management-reference-windows-defender-antivirus.md)
- [Windows Defender Antivirus in Windows 10](windows-defender-antivirus-in-windows-10.md)


