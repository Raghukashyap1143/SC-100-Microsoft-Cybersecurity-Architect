# # Excercise 3: Endpoint Security

## Exercise Overview
Contoso uses Microsoft Intune to manage its devices and provides its employees with Windows 10 and Windows 11 devices. The company has implemented several configuration profiles in the past. However, a company-wide infrastructure analysis revealed that the existing policies were created independently, making it difficult to view them holistically and trace them. As the company's cyber security architect, you have decided to consolidate all the necessary and critical configurations in one place. 

In addition, the analysis revealed that Tailwind Traders uses macOS devices in its environment. As part of the upcoming merger, you plan to prepare the Contoso tenant for the new macOS devices.

## Architecture Diagram


 ![](../media/lab4/lab4ex3.png)

## Explanation of Components

The architecture for this lab involves the following key components:

- **Endpoint Security Baseline Policy Deployment**: Configures and deploys security baseline policies to ensure consistent security configurations across organizational endpoints.

- **Antivirus Deployment on macOS Devices**: Installs and configures antivirus software on macOS devices to provide real-time protection against malware and security threats.

- **macOS Device Encryption**: Encrypts macOS devices to protect sensitive data and ensure that information remains secure in the event of device loss or theft.

## Part 1: Design a solution

In this task you will design a concept to address the challenges Contoso Ltd. is facing.

### Design Approach

In the given scenario, the following requirements can be outlined:

- Consolidate all configurations for Windows devices in one place
- Protect MacOS devices

Microsoft Endpoint Manager, with security baselines, centrally manages and secures endpoints, including desktops, laptops, mobile devices, and servers. It integrates tools like Intune and Configuration Manager, enabling efficient deployment of applications, policy enforcement, compliance, and device monitoring. 

A security baseline policy comprises a set of configuration settings recommended by Microsoft, detailing their security implications. These settings are formulated based on input from Microsoft security engineering teams, product groups, partners, and customers. These baselines encompass device configuration settings similar to those within various Intune policies. Customizing each deployed baseline enables the enforcement of necessary settings and values. When establishing a security baseline profile within Intune, you're essentially creating a template comprising multiple device configuration profiles. These recommendations must be regularly reviewed and adapted according to the respective business requirements.

### Proposed Solution

|Requirement|Solution|Action plan|
|----|----|----|
|Consolidate all configurations for Windows devices in one place|Microsoft Endpoint Manager - Endpoint Seucurity|Deploy security baseline policies
|Protect MacOS devices|Micorosft Endpoint Manager|Deploy antivirus on macOS devices|

## Part 2: Implement the solution 

### Task 1: Deploy endpoint security baseline policies

In this task, you will create **endpoint security baseline policies** for **Windows devices** in **Intune** to secure your endpoints and consolidate multiple policies in one place.

1. Log into the  VM **LON-SC1** with the local **Administrator** account. The password should be provided by your lab hosting provider.

1. Sign-in to the Microsoft Intune admin center **`https://intune.microsoft.com`** as :
    - **Email/Username:** **<inject key="AzureAdUserEmail"></inject>**  
    - **Password:** <inject key="AzureAdUserPassword"></inject>

1. If you see an information box on the top right of the screen that says **Manage multifactor authentication**, close it by selecting the **X**.

1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.

1. On the **Endpoint security | Overview** page, under **Overview** select **Security baselines**.

1. On the **Endpoint security | Security baselines** page select **Security Baseline for Windows 10 and later**.

   ![](../media/lab4/lab4i1.png)

1. On the **Security Baseline for Windows 10 and later | Profiles** page select **+ Create profile**.

1. Review the description on the **Create a profile** blade and select **Create**.

1. On the **Basics** blade enter:
    1. Name: **`Secure Windows Endpoints`**
    1. Description: **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**.

1. Select **Next**.

1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.

1. On the **Scope tags** blade select **Next**.

1. On the **Assignments** blade under **Included groups** select **Add all users** and select **Next**.

1. On the **Review + create** blade select **Create**.

1. Go back to **Endpoint security | Security baselines** page.

1. On the **Endpoint security | Security baselines** page select **Microsoft Defender for Endpoint Security Baseline**.

   ![](../media/lab4/lab4i2.png)

1. On the **Microsoft Defender for Endpoint Security baseline | Profiles** select **+ Create profile**.

1. Review the description on the **Create a profile** blade and select **Create**.

1. On the **Basics** blade enter:
    1. Name: **`Defender for Endpoint Security Baseline`**
    1. Description: **`Security best practices for the Microsoft security stack on devices managed by Intune`**.

1. Select **Next**.

1. On the **Configuration settings** blade investigate the different configuration options. When you have finished, select **Next**.

1. On the **Scope tags** blade select **Next**.

1. On the **Assignments** blade, under **Included groups** select **Add all users** and select **Next**.

1. On the **Review + create** blade select **Create**.

You have successfully created two security baseline policies for Windows devices.

### Task 2: Deploy antivirus on macOS devices

In this task, after securing **Windows devices** with endpoint security baseline policies, you will deploy **antivirus** and enable **encryption** on **macOS devices** to prepare your environment for merging with **Tailwind Traders**.

1. You should still be logged into the Microsoft Intune admin center **https://intune.microsoft.com**.

1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.

1. On the **Endpoint security | Overview** page under **Manage** select **Antivirus (1)**.

1. On the **Endpoint security | Antivirus** page select **+ Create policy (2)**.

     ![](../media/lab4/lab4i3.png)

1. On the **Create a profile** pane, under **Platform** select **macOS (1)** and under **Profile** select **Microsoft Defender Antivirus (2)**.

1. Select **Create (3)**.

    ![](../media/lab4/lab4i4.png)

1. On the **Basics** blade enter:
    1. Name: **`Deploy antivirus on macOS devices`**
    1. Description: **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Select **Next**

1. On the **Configuration settings** tab ensure the settings are configured as follows:

1. Under **Cloud delivered protection preferences**:
    - Enable / disable cloud delivered protection: **Enabled (Default) (1)**
    - Enable/ disable automatic sample submissions: **Enabled (Default) (2)**
    - Diagnostic collection level: **optional (Default) (3)**
    - Automatic security intelligence update: **Enabled (Default) (4)**

      ![](../media/lab4/lab4i6.png)

1. Under **Antivirus engine**:
    - Enable real-time protecion: **Enabled (Default) (1)**
    - Enable passive mode: **Disabled (Default) (2)**
    - Exclusion merge: **admin_only (3)**

1. Under **Threat type settings** select **+ Add**:
    - In the text box for Threat type, ensure **potentially_unwanted_application** is selected.
    - Action to take: **block**
    - Threat type settings merge: **admin_only**

1. Enable file hash computation: **True**

1. Run a scan after definitions are updated: **Enabled (Default)**

1. Enforcement level: **real_time**

1. Under **Network protection**:
    - Enforcement level: block

1. Under **Tamper protection**:
    - Enforcement level: **block (Default)**

1. Under **User interface preferences**
    - Control sign-in to consumer version: **enabled (Default)**
    - Show / hide status menu icon: **Disabled (Default)**
    - User initiated feedback: **enabled (Default)**

1. Select **Next**.

1. On the **Scope tags** blade select **Next**.

1. On the **Assignments** tab, in the text box 
enter **All users** and select it.

1. Select **Next**.

1. On the **Review + create** tab select **Save**.

You have successfully configured and deployed antivirus for macOS devices.

### Task 3: Encrypt macOS devices

In this task you will encrypt macOS devices.

1. In the Microsoft Intune admin center, in the left navigation pane select **Endpoint Security**.

1. On the **Endpoint security | Overview** page, under **Manage** select **Disk encryption**.

1. On the **Endpoint security | Disk encryption** page select **+ Create Policy**.

1. On the **Create a profile** pane, under **Platform** select **macOS** and under **Profile** select **FileVault**.

1. Select **Create**.

1. On the **Basic** blade enter:
    1. Name: **`Encrypt macOS devices`**
    1. Description: **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Select **Next**.

1. On the **Configuration settings** blade under **Encryption** configure the following settings:
   - Enable FileVault: **Yes (1)**
   - Personal recovery key rotation: **6 months (2)**
   - Escrow location description of personal recovery key: **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.` (3)**
   - Number of times allowed to bypass: **3 (4)**
   - Allow deferral until sign out: **Yes (5)**
   - Disable prompt at sign-out: **Yes (6)**
   - Hide recovery key: **Yes**
   - Select **Next**.

   ![](../media/lab4/lab4i7.png)

1. On the **Scope tags** blade select **Next**.

1. On the **Assignments** blade, under **Included groups** select **Add all users** then select **Next**.

1. On the **Review + create** blade select **Create**.

You have successfully configured and deployed a FileVault profile to encrypt macOS devices.


### Review
In this lab, you have completed the following:
- Deployed endpoint security baseline policies.
- Deployed antivirus on macOS devices.
- Encrypted macOS devices.


### You have successfully completed the lab.
