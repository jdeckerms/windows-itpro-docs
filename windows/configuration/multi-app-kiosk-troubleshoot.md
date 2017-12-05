---
title: Troubleshoot multi-app kiosk (Windows 10)
description: Tips for troubleshooting multi-app kiosk configuration.
ms.assetid: 14DDDC96-88C7-4181-8415-B371F25726C8
keywords: ["lockdown", "app restrictions"]
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: edu, security
author: jdeckerms
ms.localizationpriority: medium
ms.date: 10/05/2017
ms.author: jdecker
---

# Troubleshoot multi-app kiosk


**Applies to**

-   Windows 10

## Unexpected results

For example:
- Start is not launched in full-screen
- Blocked hotkeys are allowed
- Task Manager, Cortana, or Settings can be launched
- Start layout has more apps than expected

**Troubleshooting steps**

1. [Verify that the provisioning package is applied successfully](lock-down-windows-10-to-specific-apps.md#validate-provisioning).
2. Verify that the account (config) is mapped to a profile in the configuration XML file.
3. Verify that the configuration XML file is authored and formatted correctly. Correct any configuration errors, then create and apply a new provisioning package. Sign out and sign in again to check the new configuration.


## Apps configured in AllowedList are blocked

1. Ensure the account is mapped to the correct profile and that the apps are specific for that profile. 
2. Check the EventViewer logs for Applocker and AppxDeployment (under **Application and Services Logs\Microsoft\Windows**).


## Start layout not as expected

- Make sure the Start layout is authored correctly. Ensure that the attributes **Size**, **Row**, and **Column** are specified for each application and are valid.
- Check if the apps included in the Start layout are installed for the assigned access user.
- Check if the shortcut exists on the target device, if a desktop app is missing on Start.

