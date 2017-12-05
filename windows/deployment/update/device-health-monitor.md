---
title: Monitor the health of devices with Device Health
description: You can use Device Health in OMS to monitor the frequency and causes of crashes and misbehaving apps on devices in your network.
keywords: oms, operations management suite, wdav, health, log analytics
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.pagetype: deploy
author: jaimeo
---

# Monitor the health of devices with Device Health

## Introduction

Device Health is the newest Windows Analytics solution that complements the existing Upgrade Readiness and Update Compliance solutions by providing IT with reports on some common problems the end users might experience so they can be proactively remediated, thus saving support calls and improving end-user productivity.

Like Upgrade Readiness and Update Compliance, Device Health is a solution built within Operations Management Suite (OMS), a cloud-based monitoring and automation service that has a flexible servicing subscription based on data usage and retention. This release is free for customers to try and will not incur charges on your OMS workspace for its use. For more information about OMS, see [Operations Management Suite overview](http://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/).

Device Health uses Windows diagnostic data that is part of all Windows 10 devices. If you have already employed Upgrade Readiness or Update Compliance solutions, all you need to do is select Device Health from the OMS solution gallery and add it to your OMS workspace. Device Health requires enhanced telemetry, so you might need to implement this policy if you've not already done so.


Device Health provides the following:

- Identification of devices that crash frequently, and therefore might need to be rebuilt or replaced
- Identification of device drivers that are causing device crashes, with suggestions of alternative versions of those drivers that might reduce the number of crashes
- Notification of Windows Information Protection misconfigurations that send prompts to end users
- No need for new complex customized infrastructure, thanks to cloud-connected access using Windows 10 telemetry

See the following topics in this guide for detailed information about configuring and using the Device Health solution:

- [Get started with Device Health](device-health-get-started.md): How to add Device Health to your environment.
- [Using Device Health](device-health-using.md): How to begin using Device Health.

An overview of the processes used by the Device Health solution is provided below.

## Device Health licensing

Use of Windows Analytics Device Health requires one of the following licenses:

- Windows 10 Enterprise or Windows 10 Education per-device with active Software Assurance
- Windows 10 Enterprise E3 or E5 per-device or per-user subscription (including Microsoft 365 F1, E3, or E5)
- Windows 10 Education A3 or A5 (including Microsoft 365 Education A3 or A5)
- Windows VDA E3 or E5 per-device or per-user subscription
- Windows Server 2016 and on


You don't have to install Windows 10 Enterprise on a per-device basis--you just need enough of the above licenses for the number of devices using Device Health. 


## Device Health architecture
 
The Device Health architecture and data flow is summarized by the following five-step process:



**(1)** User computers send telemetry data to a secure Microsoft data center using the Microsoft Data Management Service.<BR>
**(2)** Telemetry data is analyzed by the Microsoft Telemetry Service.<BR>
**(3)** Telemetry data is pushed from the Microsoft Telemetry Service to your OMS workspace.<BR>
**(4)** Telemetry data is available in the Device Health solution.<BR>
**(5)** You are now able to proactively monitor Device Health issues in your environment.<BR>

These steps are illustrated in following diagram:

 [![](images/analytics-architecture.png)](images/analytics-architecture.png)

>[!NOTE]
>This process assumes that Windows telemetry is enabled and you [have assigned your Commercial ID to devices](update-compliance-get-started.md#deploy-your-commercial-id-to-your-windows-10-devices).



 
## Related topics

[Get started with Device Health](device-health-get-started.md)

[Use Device Health to monitor frequency and causes of device crashes](device-health-using.md)

For the latest information on Windows Analytics, including new features and usage tips, see the [Windows Analytics blog](https://blogs.technet.microsoft.com/upgradeanalytics)
