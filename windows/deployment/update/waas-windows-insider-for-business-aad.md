---
title: Windows Insider Program for Business using Azure Active Directory
description: Benefits and configuration of corporate accounts in the Windows Insider Program
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
author: DaniHalfin
ms.localizationpriority: high
ms.author: daniha
---

# Windows Insider Program for Business using Azure Active Directory


**Applies to**

- Windows 10

> **Looking for information about Windows 10 for personal or home use?** See [Windows Update: FAQ](https://support.microsoft.com/help/12373/windows-update-faq)

We recently added features and benefits to better support the IT Professionals and business users in our Windows Insider community. This includes the option to download Windows 10 Insider Preview builds using your corporate credentials in Azure Active Directory (AAD). By enrolling devices in AAD, you increase the visibility of feedback submitted by users in your organization – especially on features that support your specific business needs. 

>[!NOTE]
>At this point, the Windows Insider Program for Business only supports Azure Active Directory (and not Active Directory on premises) as a corporate authentication method.

>[!TIP]
>New to Azure Active Directory? Go here for [an introduction to AAD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect), including guidance for [adding users](https://docs.microsoft.com/azure/active-directory/active-directory-users-create-azure-portal), [device registration](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview) and [integrating your on-premises directories with Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>If your company is currently not using AAD – but has a paid subscription to  Office 365, Microsoft Dynamics CRM Online, Enterprise Mobility Suite, or other Microsoft services – you have a free subscription to Microsoft Azure Active Directory. This subscription  can be used to create users for enrollment in the Windows Insider Program for Business.

In order to get the most benefit out of the Windows Insider Program for Business, organizations should not use a test tenant of AAD. There will be no modifications to the AAD tenant to support the Windows Insider Program as it will only be used as an authentication method.

## Register your organization's Azure AD domain to the Windows Insider Program for Business
Rather than have each user in your organization register for Windows 10 Insider Preview builds, you can now simply register your domain – and cover all users with just one registration.

1. On the [Windows Insider](https://insider.windows.com) website, go to **For Business > Getting Started** to [register your organizational Azure AD account](https://insider.windows.com/en-us/insidersigninaad/).
2. **Register your domain**. Rather than have each user register individually for Windows Insider Preview builds, administrators can simply [register their domain](https://insider.windows.com/en-us/for-business-organization-admin/) and control settings centrally.

>[!IMPORTANT]
>The signed-in user needs to be a **Global Administrator** of the Azure AD domain in order to be able to register the domain.

## Check if a device is connected to your company’s Azure Active Directory subscription
Simply go to **Settings > Accounts > Access work or school**. If a corporate account is on Azure Active Directory and it is connected to the device, you will see the account listed as highlighted in the image below.

![Device connected to Work Account](images/waas-wipfb-work-account.jpg)

## Enroll a device with an Azure Active Directory account
1. Navigate to the [**Getting Started**](https://insider.windows.com/en-us/getting-started/) page on [Windows Insider](https://insider.windows.com).
2. Go to **Register your organization account** and follow the instructions.
3. On your Windows 10 device, go to **Settings > Updates & Security >  Windows Insider Program**. 
4. Enter the AAD account that you used to register and follow the on-screen directions. 

>[!NOTE]
>Make sure that you have administrator rights to the machine and that it has latest Windows updates. 

## Switch device enrollment from your Microsoft account to your AAD account 
1. Visit [insider.windows.com](https://insider.windows.com) to register your AAD account. If you are signed in with your Microsoft account, sign out, then sign back in with your corporate AAD account. 
2. Click **Get started**, read and accept the privacy statement and program terms and click **Submit**. 
3. On your Windows 10 PC, go to **Settings > Updates & Security >  Windows Insider Program**. 
4. Under Windows Insider account, click your Microsoft account, then **Change** to open a Sign In box. 
5. Select your corporate account and click Continue to change your account. 

![Change Windows Insider account](images/waas-wipfb-change-user.png)

>[!NOTE]
>Your device must be connected to your corporate account in AAD for the account to appear in the account list.

## User consent requirement

With the current version of the Feedback Hub app, we need the user's consent to access their AAD account profile data (We read their name, organizational tenant ID and user ID). When they sign in for the first time with the AAD account, they will see a popup asking for their permission, like this:

![Feedback Hub consent to AAD pop-up](images/waas-wipfb-aad-consent.png)

Once agreed, everything will work fine, and that user won't be prompted for permission again.

### Something went wrong

The option for users to give consent for apps to access their profile data is controlled through Azure Active Directory. This means the AAD administrators have the ability to allow or block users from giving consent.

In case the administrators blocked this option, when the user signs in with the AAD account, they will see the following error message:

![Feedback Hub consent error message](images/waas-wipfb-aad-error.png)

This blocks the user from signing in, which means they won't be able to use the Feedback Hub app with their AAD credentials.

**To fix this issue**, an administrator of the AAD directory will need to enable user consent for apps to access their data.

To do this through the **classic Azure portal**:
1. Go to https://manage.windowsazure.com/ .
2. Switch to the **Active Directory** dashboard.  
   ![Azure classic portal dashboard button](images/waas-wipfb-aad-classicaad.png)
3. Select the appropriate directory and go to the **Configure** tab.
4. Under the **integrated applications** section, enable **Users may give applications permissions to access their data**.  
   ![Azure classic portal enable consent](images/waas-wipfb-aad-classicenable.png)

To do this through the **new Azure portal**:
1. Go to https://portal.azure.com/ .
2. Switch to the **Active Directory** dashboard.  
   ![Azure new portal dashboard button](images/waas-wipfb-aad-newaad.png)
3. Switch to the appropriate directory.  
   ![Azure new portal switch directory button](images/waas-wipfb-aad-newdirectorybutton.png)
4. Under the **Manage** section, select **User settings**.  
   ![Azure new portal user settings](images/waas-wipfb-aad-newusersettings.png)
5. In the **Enterprise applications** section, enable **Users can allow apps to access their data**.  
   ![Azure new portal enable consent](images/waas-wipfb-aad-newenable.png)


## Frequently Asked Questions

### Will my test machines be affected by automatic registration?
All devices enrolled in the Windows Insider Program (physical or virtual) will receive Windows 10 Insider Preview builds (regardless of registration with MSA or AAD).

### Once I register with my corporate account in AAD, do I need to keep my Microsoft account for the Windows Insider Program?
No, once you set up your device using AAD credentials – all feedback and flighting on that machine will be under your AAD account. You may need MSA for other machines that aren’t being used on your corporate network or to get Microsoft Store App updates.

### How do I stop receiving updates? 
You can simply “unlink” your account by going to **Settings > Updates & Security > Windows Insider Program**, select Windows Insider Account and click **Unlink**.


## Related Topics
- [Windows Insider Program for Business](waas-windows-insider-for-business.md)
- [Windows Insider Program for Business Frequently Asked Questions](waas-windows-insider-for-business-faq.md)
