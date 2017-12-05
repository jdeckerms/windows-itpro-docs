---
title: SurfaceHubManagement (Windows 10)
description: This section describes the SurfaceHubManagement settings that you can configure in provisioning packages for Windows 10 using Windows Configuration Designer.
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
author: jdeckerMS
ms.localizationpriority: medium
ms.author: jdecker
ms.date: 08/21/2017
---

# SurfaceHubManagement (Windows Configuration Designer reference)

Use SurfaceHubManagement settings to set the administrator group that will manage a Surface Hub that is joined to the domain.

>[!IMPORTANT]
>These settings should be used only in provisioning packages that are applied during OOBE.



## Applies to

| Setting   | Desktop editions | Mobile editions | Surface Hub | HoloLens | IoT Core |
| --- | :---: | :---: | :---: | :---: | :---: |
| All settings |  |  | X |  |   |


## GroupName

Enter the group name for the administrators group in Active Directory.

## GroupSid

Enter the SID or the administrators group in Active Directory.