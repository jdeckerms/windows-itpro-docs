---
title: Open Windows Defender Firewall with Advanced Security (Windows 10)
description: Open Windows Defender Firewall with Advanced Security
ms.assetid: 788faff2-0f50-4e43-91f2-3e2595c0b6a1
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
author: brianlic-msft
---

# Open Windows Defender Firewall with Advanced Security

**Applies to**
-   Windows 10
-   Windows Server 2016

This procedure shows you how to open the Windows Defender Firewall with Advanced Security console.

**Administrative credentials**

To complete this procedure, you must be a member of the Administrators group. For more information, see Additional considerations.

## Opening Windows Defender Firewall 

-   [Using the Windows interface](#to-open-windows-firewall-with-advanced-security-using-the-ui)

-   [Using a command line](#to-open-windows-firewall-with-advanced-security-from-a-command-prompt)

## To open Windows Defender Firewall using the UI

Click Start, type **Windows Defender Firewall**, and the press ENTER.

## To open Windows Defender Firewall from a command prompt

1.  Open a command prompt window.

2.  At the command prompt, type:

    ``` syntax
    wf.msc
    ```

**Additional considerations**

Although standard users can start the Windows Defender Firewall MMC snap-in, to change most settings the user must be a member of a group with the permissions to modify those settings, such as Administrators.
