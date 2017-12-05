---
title: Hybrid Key trust Windows Hello for Business Prerequistes (Windows Hello for Business)
description: Prerequisites for Hybrid Windows Hello for Business Deployments
keywords: identity, PIN, biometric, Hello, passport, WHFB, hybrid, key-trust
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security, mobile
author: mikestephens-MS
ms.author: mstephen
localizationpriority: high
ms.date: 10/20/2017
---
# Hybrid Key trust Windows Hello for Business Prerequisites

**Applies to**
-   Windows 10


>This guide only applies to Hybrid deployments for Windows 10, version 1703 or higher.

Hybrid environments are distributed systems that enable organizations to use on-premises and Azure-based identities and resources. Windows Hello for Business uses the existing distributed system as a foundation on which organizations can provide two-factor authentication that provides a single sign-in like experience to modern resources.

The distributed systems on which these technologies were built involved several pieces of on-premises and cloud infrastructure.  High-level pieces of the infrastructure include:
* [Directories](#directories)
* [Public Key Infrastucture](#public-key-infastructure)
* [Directory Synchronization](#directory-synchronization)
* [Federation](#federation)
* [MultiFactor Authetication](#multifactor-authentication)
* [Device Registration](#device-registration)
  
## Directories ##
Hybrid Windows Hello for Business needs two directories: on-premises Active Directory and a cloud Azure Active Directory.  The minimum required domain functional and forest functional levels for Windows Hello for Business deployment is Windows Server 2008 R2. The 

A hybrid Windows Hello for Busines deployment needs an Azure Active Directory subscription.  The hybrid key trust deployment, does not need a premium Azure Active Directory subscription.

You can deploy Windows Hello for Business in any environment with Windows Server 2008 R2 or later domain controllers.  However, the key trust deployment needs an ***adequate*** number of Windows Server 2016 domain controllers at each site where users authenticate using Windows Hello for Business.  Read the [Planning an adequate number of Windows Server 2016 Domain Controllers for Windows Hello for Business deployments](hello-adequate-domain-controllers.md) to learn more.
 
Review these requirements and those from the Windows Hello for Business planning guide and worksheet.  Based on your deployment decisions you may need to upgrade your on-premises Active Directory or your Azure Active Directory subscription to meet your needs.

### Section Review ###

> [!div class="checklist"]
> * Active Directory Domain Functional Level
> * Active Directory Forest Functional Level
> * Domain Controller version
> * Azure Active Directory subscription
> * Correct subscription for desired features and outcomes  

<br>

## Public Key Infrastructure ##
The Windows Hello for Business deployment depends on an enterprise public key infrastructure as trust anchor for authentication. Domain controllers for hybrid deployments need a certificate in order for Windows 10 devices to trust the domain controller.

Key trust deployments do not need client issued certificates for on-premises authentication.  Active Directory user accounts are automatically configured for public key mapping by Azure AD Connect synchronizing the public key of the registered Windows Hello for Business credential to an attribute on the user's Active Diretory object.

The minimum required enterprise certificate authority that can be used with Windows Hello for Business is Windows Server 2012.

> [!IMPORTANT]
> For Azure AD joined device to authenticate to and use on-premises resources, ensure you:
> * Install the root certificate authority certificate for your organization in the user's trusted root certifcate store.
> * Publish your certificate revocation list to a location that is available to Azure AD joined devices, such as a web-based url.

### Section Review
> [!div class="checklist"]  
> * Windows Server 2012 Issuing Certificate Authority

<br>

## Directory Synchronization ##
The two directories used in hybrid deployments must be synchronized.  You need Azure Active Directory Connect to synchronize user accounts in the on-premises Active Directory with Azure Active Directory.
  
Organizations using older directory synchronization technology, such as DirSync or Azure AD sync need to upgrade to Azure AD Connect.
 
### Section Review 
> [!div class="checklist"]
> * Azure Active Directory Connect directory synchronization
> * [Upgrade from DirSync](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-dirsync-upgrade-get-started)
> * [Upgrade from Azure AD Sync](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version)

<br>

## Federation with Azure ##
You can deploy Windows Hello for Business key trust in non-federated and federated environments.  For non-federated environments, key trust deployments work in environments that have deployed [Password Synchronization with Azure AD Connect](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization) and [Azure Active Directory Pass-through-Authentication](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication).  For federated environments, you can deploy Windows Hello for Business key trust using Active Directory Federation Services (AD FS) 2012 R2 or later. 

### Section Review ###
> [!div class="checklist"]
> * Non-federated environments
> * Federated environments 

<br>

## Multifactor Authentication ##
Windows Hello for Business is a strong, two-factor credential the helps organizations reduce their dependency on passwords.  The provisioning process lets a user enroll in Windows Hello for Business using their username and password as one factor, but needs a second factor of authentication.

Hybrid Windows Hello for Business deployments can use Azure’s Multifactor Authentication service or they can use multifactor authentication provides by Windows Server 2012 R2 or later Active Directory Federation Services, which includes an adapter model that enables third parties to integrate their multifactor authentication into AD FS.

### Section Review 
> [!div class="checklist"]
> * Azure MFA Service
> * Windows Server 2016 AD FS and Azure (optional, if federated)
> * Windows Server 2016 AD FS and third party MFA Adapter (optiona, if federated)

<br>

## Device Registration ##
Organizations wanting to deploy hybrid key trust need thier domain joined devices to register to Azure Active Directory.  Just as a computer has an identity in Active Directory, that same computer has an identity in the cloud.  This ensures that only approved computers are used with that Azure Active Directory.  Each computer registers its identity in Azure Active Directory. 
 

### Section Checklist ###
> [!div class="checklist"]
> * Device Registration with Azure Device Registration 

<br>

### Next Steps ###
Follow the Windows Hello for Business hybrid key trust deployment guide.  For proof-of-concepts, labs, and new installations, choose the **New Installation Basline**.  

For environments transitioning from on-premises to hybrid, start with  **Configure Azure Directory Syncrhonization**. 

For federerated and non-federated environments, start with **Configure Windows Hello for Business settings**.

> [!div class="op_single_selector"]
> - [New Installation Baseline](hello-hybrid-key-new-install.md)
> - [Configure Directory Synchronization](hello-hybrid-key-trust-dirsync.md)
> - [Configure Windows Hello for Business settings](hello-hybrid-key-whfb-settings.md)

<br><br>

<hr>

## Follow the Windows Hello for Business hybrid key trust deployment guide
1. [Overview](hello-hybrid-key-trust.md)
2. Prerequistes (*You are here*)
3. [New Installation Baseline](hello-hybrid-key-new-install.md)
4. [Configure Directory Synchronization](hello-hybrid-key-trust-dirsync.md)
5. [Configure Azure Device Registration](hello-hybrid-key-trust-devreg.md)
6. [Configure Windows Hello for Business settings](hello-hybrid-key-whfb-settings.md)
7. [Sign-in and Provision](hello-hybrid-key-whfb-provision.md)