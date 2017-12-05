---
title: Configure VDA for Windows 10 Subscription Activation
description: How to enable Windows 10 Enterprise E3 and E5 subscriptions for VDA
keywords: upgrade, update, task sequence, deploy
ms.prod: w10
ms.mktglfcycl: deploy
localizationpriority: high
ms.sitesec: library
ms.pagetype: mdt
ms.date: 11/14/2017
author: greg-lindsay
---

# Configure VDA for Windows 10 Subscription Activation

This document describes how to configure virtual machines (VMs) to enable [Windows 10 Subscription Activation](windows-10-enterprise-subscription-activation.md) in a Windows Virtual Desktop Access (VDA) scenario. Windows VDA is a device or user-based licensing mechanism for managing access to virtual desktops.

Deployment instructions are provided for the following scenarios:
1. [Active Directory-joined VMs](#active-directory-joined-vms)
2. [Azure Active Directory-joined VMs](#azure-active-directory-joined-vms)
3. [Azure Gallery VMs](#azure-gallery-vms)

## Requirements

- VMs must be running Windows 10 Pro, version 1703 (also known as the Creator's Update) or later.
- VMs must be Active Directory-joined or Azure Active Directory-joined.
- VMs must be generation 1.
- VMs must hosted by a [Qualified Multitenant Hoster](https://www.microsoft.com/en-us/CloudandHosting/licensing_sca.aspx) (QMTH).

## Activation

The underlying Windows 10 Pro license must be activated prior to Subscription Activation of Windows 10 Enterprise. 

Procedures in this topic provide a Windows 10 Pro Generic Volume License Key (GVLK). Activation with this key is accomplished using a Volume License KMS activation server provided by the QMTH. Alternatively, a KMS activation server on your corporate network can be used if you have configured a private connection, such as [ExpressRoute](https://azure.microsoft.com/services/expressroute/) or [VPN Gateway](https://azure.microsoft.com/services/vpn-gateway/).

For examples of activation issues, see [Troubleshoot the user experience](https://docs.microsoft.com/windows/deployment/deploy-enterprise-licenses#troubleshoot-the-user-experience).

## Active Directory-joined VMs

1. Use the following instructions to prepare the VM for Azure: [Prepare a Windows VHD or VHDX to upload to Azure](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image)
2. (Optional) To disable network level authentication, type the following at an elevated command prompt:

    ```
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v UserAuthentication /t REG_DWORD /d 0 /f
    ```

3. At an elevated command prompt, type **sysdm.cpl** and press ENTER.
4. On the Remote tab, choose **Allow remote connections to this computer** and then click **Select Users**.
5. Click **Add**, type **Authenticated users**, and then click **OK** three times.
6. Follow the instructions to use sysprep at [Steps to generalize a VHD](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image#steps-to-generalize-a-vhd).
7. [Install Windows Configuration Designer](/windows/configuration/provisioning-packages/provisioning-install-icd).
8. Open Windows Configuration Designer and click **Provison desktop services**.
9. Under **Name**, type **Desktop AD Enrollment Pro GVLK**, click **Finish**, and then on the **Set up device** page enter a device name. 
    - Note: You can use a different project name, but this name is also used with dism.exe in a subsequent step.
10. Under **Enter product key** type the Pro GVLK key: **W269N-WFGWX-YVC9B-4J6C9-T83GX**.
11. On the Set up network page, choose **Off**.
12. On the Account Management page, choose **Enroll into Active Directory** and then enter the account details.
    - Note: This step is different for [Azure AD-joined VMs](#azure-active-directory-joined-vms).
13. On the Add applications page, add applications if desired. This step is optional.
14. On the Add certificates page, add certificates if desired. This step is optional.
15. On the Finish page, click **Create**.
16. In file explorer, double-click the VHD to mount the disk image. Determine the drive letter of the mounted image.
17. Type the following at an elevated commnand prompt. Replace the letter **G** with the drive letter of the mounted image, and enter the project name you used if it is different than the one suggested:

    ```
    Dism.exe /Image=G:\ /Add-ProvisioningPackage /PackagePath: "Desktop AD Enrollment Pro GVLK.ppkg"
    ```
18. Right-click the mounted image in file explorer and click **Eject**.
19. See instructions at [Upload and create VM from generalized VHD](https://docs.microsoft.com/azure/virtual-machines/windows/upload-generalized-managed#log-in-to-azure) to log in to Azure, get your storage account details, upload the VHD, and create a managed image.

## Azure Active Directory-joined VMs

>[!IMPORTANT]
>Azure Active Directory (Azure AD) provisioning packages have a 30 day limit on bulk token usage. You will need to update the provisioning package and re-inject it into the image after 30 days. Existing virtual machines that are Azure AD-joined and deployed will not need to be recreated.

For Azure AD-joined VMs, follow the same instructions (above) as for [Active Directory-joined VMs](#active-directory-joined-vms) with the following exceptions:
- In step 9, during setup with Windows Configuration Designer, under **Name**, type a name for the project that indicates it is not for Active Directory joined VMs, such as **Desktop Bulk Enrollment Token Pro GVLK**.
- In step 12, during setup with Windows Configuration Designer, on the Account Management page, instead of enrolling in Active Directory, choose **Enroll in Azure AD**, click **Get Bulk Token**, sign in and add the bulk token using your organization's credentials.
- In step 17, when entering the PackagePath, use the project name you entered in step 9 (ex: **Desktop Bulk Enrollment Token Pro GVLK.ppkg**)
- When attempting to access the VM using remote desktop, you will need to create a custom RDP settings file as described below in [Create custom RDP settings for Azure](#create-custom-rpd-settings-for-azure).

## Azure Gallery VMs

1. (Optional) To disable network level authentication, type the following at an elevated command prompt:

    ```
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v UserAuthentication /t REG_DWORD /d 0 /f
    ```

2. At an elevated command prompt, type **sysdm.cpl** and press ENTER.
3. On the Remote tab, choose **Allow remote connections to this computer** and then click **Select Users**.
4. Click **Add**, type **Authenticated users**, and then click **OK** three times.
(https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image#steps-to-generalize-a-vhd).
5. [Install Windows Configuration Designer](/windows/configuration/provisioning-packages/provisioning-install-icd).
6. Open Windows Configuration Designer and click **Provison desktop services**.
7. Under **Name**, type **Desktop Bulk Enrollment Token Pro GVLK**, click **Finish**, and then on the **Set up device** page enter a device name. 
    - Note: You can use a different project name, but this name is also used with dism.exe in a subsequent step.
8. Under **Enter product key** type the Pro GVLK key: **W269N-WFGWX-YVC9B-4J6C9-T83GX**.
9. On the Set up network page, choose **Off**.
10. On the Account Management page, choose **Enroll in Azure AD**, click **Get Bulk Token**, sign in, and add the bulk token using your organizations credentials.
11. On the Add applications page, add applications if desired. This step is optional.
12. On the Add certificates page, add certificates if desired. This step is optional.
13. On the Finish page, click **Create**.
14. Copy the .ppkg file to the remote Virtual machine.  Double click to initiate the provisioning package install.  This will reboot the system.

- When attempting to access the VM using remote desktop, you will need to create a custom RDP settings file as described [below](#create-custom-rpd-settings-for-azure).

## Create custom RDP settings for Azure

To create custom RDP settings for Azure:

1. Open Remote Desktop Connection and enter the IP address or DNS name for the remote host.
2. Click **Show Options**, and then under Connection settings click **Save As** and save the RDP file to the location where you will use it.
3. Close the Remote Desktop Connection window and open Notepad.
4. Drag the RDP file into the Notepad window to edit it.
5. Enter or replace the line that specifies authentication level with the following two lines of text:

    ```text
    enablecredsspsupport:i:0
    authentication level:i:2
    ```
6. **enablecredsspsupport** and **authentication level** should each appear only once in the file.
7. Save your changes, and then use this custom RDP file with your Azure AD credentials to connect to the Azure VM.

## Related topics

[Windows 10 Subscription Activation](windows-10-enterprise-subscription-activation.md)
<BR>[Recommended settings for VDI desktops](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-vdi-recommendations)
<BR>[Licensing the Windows Desktop for VDI Environments](http://download.microsoft.com/download/1/1/4/114A45DD-A1F7-4910-81FD-6CAF401077D0/Microsoft%20VDI%20and%20VDA%20FAQ%20v3%200.pdf)

