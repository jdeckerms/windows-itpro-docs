---
title: Microsoft Security Compliance Toolkit 1.0
description: This article describes how to use the Security Compliance Toolkit in your organization
keywords: virtualization, security, malware
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: high
ms.author: sagaudre
author: brianlic-msft
ms.date: 10/17/2017
---

# Microsoft Security Compliance Toolkit 1.0

## What is the Security Compliance Toolkit (SCT)?

The Security Compliance Toolkit (SCT) is a set of tools that allows enterprise security administrators to download, analyze, test, edit, and store Microsoft-recommended security configuration baselines for Windows and other Microsoft products.

The SCT enables administrators to effectively manage their enterprise’s Group Policy Objects (GPOs). Using the toolkit, administrators can compare their current GPOs with Microsoft-recommended GPO baselines or other baselines, edit them, store them in GPO backup file format, and apply them broadly through Active Directory or individually through local policy.
<p></p>

The Security Compliance Toolkit consists of:

-   Windows 10 Security Baselines
    -   Windows 10 Version 1709 (Fall Creators Update)
    -    Windows 10 Version 1703 (Creators Update)
    -   Windows 10 Version 1607 (Anniversary Update)
    -   Windows 10 Version 1511 (November Update)
    -   Windows 10 Version 1507

-   Windows Server Security Baselines
    -   Windows Server 2016
    -   Windows Server 2012 R2

-   Tools
    -   Policy Analyzer tool
    -   Local Group Policy Object (LGPO) tool


You can [download the tools](https://www.microsoft.com/download/details.aspx?id=55319) along with the baselines for the relevant Windows versions.

## What is the Policy Analyzer tool?

The Policy Analyzer is a utility for analyzing and comparing sets of Group Policy Objects (GPOs). Its main features include:
-   Highlight when a set of Group Policies has redundant settings or internal inconsistencies
-   Highlight the differences between versions or sets of Group Policies
-   Compare GPOs against current local policy and local registry settings
-   Export results to a Microsoft Excel spreadsheet

Policy Analyzer lets you treat a set of GPOs as a single unit. This makes it easy to determine whether particular settings are duplicated across the GPOs or are set to conflicting values. Policy Analyzer also lets you capture a baseline and then compare it to a snapshot taken at a later time to identify changes anywhere across the set. 

More information on the Policy Analyzer tool can be found on the [Security Guidance blog](https://blogs.technet.microsoft.com/secguide/2016/01/22/new-tool-policy-analyzer/) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).

## What is the Local Group Policy Object (LGPO) tool?

LGPO is a tool for transferring Group Policy directly between a host’s registry and a GPO backup file, bypassing the Domain Controller. This gives administrators a simple way to verify the effects of their Group Policy settings directly. 
Documentation for the LGPO tool can be found on the [Security Guidance blog](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) or by [downloading the tool](https://www.microsoft.com/download/details.aspx?id=55319).