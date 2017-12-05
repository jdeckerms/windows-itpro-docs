---
title: Configuring Hybrid key trust Windows Hello for Business - Directory Synchronization
description: Configuring Hybrid key trust Windows Hello for Business - Directory Synchronization
keywords: identity, PIN, biometric, Hello, passport, WHFB, dirsync, connect, Windows Hello, AD Connect, key trust, key-trust
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security, mobile
localizationpriority: high
author: mikestephens-MS
ms.author: mstephen
ms.date: 10/20/2017
---
# Configure Hybrid Windows Hello for Business: Directory Synchronization

**Applies to**
-   Windows 10

>This guide only applies to Hybrid deployments for Windows 10, version 1703 or higher.

## Directory Syncrhonization

In hybrid deployments, users register the public portion of their Windows Hello for Business credential with Azure.  Azure AD Connect synchronizes the Windows Hello for Business public key to Active Directory.  

### Group Memberships for the Azure AD Connect Service Account

The KeyAdmins global group provides the Azure AD Connect service with the permissions needed to read and write the public key to Active Directory.  

Sign-in a domain controller or management workstation with _Domain Admin_ equivalent credentials.

1. Open **Active Directory Users and Computers**.
2. Click the **Users** container in the navigation pane.
3. Right-click **KeyAdmins** in the details pane and click **Properties**.
4. Click the **Members** tab and click **Add**
5. In the **Enter the object names to select** text box, type the name of the Azure AD Connect service account.  Click **OK**.
6. Click **OK** to return to **Active Directory Users and Computers**.

### Section Review

> [!div class="checklist"]
> * Configure group membership for Azure AD Connect

>[!div class="step-by-step"]
[< Configure Active Directory](hello-hybrid-key-whfb-settings-ad.md)
[Configure PKI >](hello-hybrid-key-whfb-settings-pki.md)

<br><br>

<hr>

## Follow the Windows Hello for Business hybrid key trust deployment guide
1. [Overview](hello-hybrid-cert-trust.md)
2. [Prerequistes](hello-hybrid-key-trust-prereqs.md)
3. [New Installation Baseline](hello-hybrid-key-new-install.md)
4. [Configure Directory Synchronization](hello-hybrid-key-trust-dirsync.md)
5. [Configure Azure Device Registration](hello-hybrid-key-trust-devreg.md)
6. Configure Windows Hello for Business settings: Directory Syncrhonization (*You are here*)
7. [Sign-in and Provision](hello-hybrid-key-whfb-provision.md)
