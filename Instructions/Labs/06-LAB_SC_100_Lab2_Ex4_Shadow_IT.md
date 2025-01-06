# Excercise 3: Shadow-IT
## Exercise Overview
Contoso's IT infrastructure has evolved over the past few decades, providing various server instances, applications, and services. Recently, the company has prioritized securing its environment by implementing Device Management, data governance, and Identity and Application Protection over the last two years. However, the process of restricting users to only specific applications deployed by the company has not yet been established, allowing users to install applications from various sources. As the organization's cyber security architect, your goal is to have a complete overview of all applications used by employees. Your protection measure is to block insecure applications in your environment.

### Estimated Duration: 45 Minutes

## Architecture Diagram

   ![](../media/lab02/lab2ex3.png)

## Explanation of Components

The architecture for this lab involves the following key components:  

- **Integration of Defender for Endpoint with Defender for Cloud Apps**: Connects endpoint protection with cloud security to provide enhanced visibility and control over applications and user activities.  

- **Shadow IT Investigation**: Identifies and analyzes unauthorized or unmanaged applications within Contoso Ltd's environment to uncover potential security risks.  

- **Blocking Unsecure Applications**: Implements policies to restrict access to applications that fail to meet security standards, protecting organizational resources.  

- **Automated Application Blocking**: Configures automation to detect and block unsecure applications proactively, ensuring continuous compliance and reducing manual intervention. 

## Part 1: Design a solution

In this task you will design a concept to address the challenges Contoso Ltd. is facing.

### Design Approach

In the given scenario, your initial action is to analyze and uncover all applications currently in use by employees. Unauthorized applications installed by users can pose security risks to the company, highlighting the need to identify Shadow IT. The subsequent step involves remedying the risks posed by these unsafe applications.

Defender for Cloud Apps is a security solution designed to address Shadow IT risks within cloud environments. It aids organizations in discovering and monitoring unauthorized cloud applications utilized by employees, evaluating their security posture, and enforcing policies to ensure compliance and safeguard data. By offering visibility and control over Shadow IT, Defender for Cloud Apps assists organizations in mitigating security risks associated with unauthorized cloud usage, thereby enhancing the security of their cloud environment.

### Proposed Solution

| Requirement                   | Solution                          | Action plan                                             |
| ----------------------------- | --------------------------------- | ------------------------------------------------------- |
| Discover Shadow IT            | Microsoft Defender for Cloud Apps | Investigate all applications in the Contoso environment |
| Block all unsafe applications | Microsoft Defender for Cloud Apps | Mark unsafe applications as unsanctioned                |

## Part 2: Implement the solution

### Task 1: Integrate Microsoft Defender for Endpoint with Defender for Cloud Apps

In order to control the use of application on users company owned devices you must integrate Defender for Endpoint with Defender for Cloud Apps.

1. Sign-in to the Microsoft Defender portal **`https://security.microsoft.com`** using below credentials

   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

   - **Password:** <inject key="AzureAdUserPassword"></inject>

1. In the Microsoft Defender portal, expand **Hunting** (1) and select **Advanced Hunting** (2). Wait for the completion of the new spaces preparation. This step is only for the purpose of setting up the new spaces, there is no hunting in this step.
   ![](../media/lab02/1.png)

1. In the Microsoft Defender portal, in the left navigation page and select **Settings** (1).

1. On the **Settings** page select **Endpoints** (2).

   ![](../media/lab02/2.png)

   > **NOTE**: It can take anywhere from 10 minutes to 1 hour for this option to appear. If after 10 minutes, you don't see it, continue with another exercise and then come back to this step.

1. Under **Endpoints**, select **Advanced features** (1). Scroll down until you see Microsoft Defender for Cloud Apps. Select the slider to set it to **On** (2).
1. At the bottom of the page, select **Save preferences** (3).

   ![](../media/lab02/3.png)

You have successfully enabled Microsoft Defender for Cloud Apps for Endpoints. With this set-up all signals coming from Microsoft Defender for Endpoints are forwarded to Defender for Cloud Apps giving you the ability to block unsecure applications. All applications tagged as **Unsanctoned** will now be blocked.

### Task 2: Investigate the Shadow-IT of Contoso Ltd

In this task, you will analyze all the applications currently used in your company. You will take a closer look at various applications and their respective risk assessment as well as their assessment structure.

1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud app catalog** (1).

   ![](../media/lab02/4.png)

1. The **Cloud app catalog** blade displays all applications currently utilized within your organization. Explore multiple applications and their associated risk scores by selecting each respective application.

>**NOTE**: Defender for Cloud Apps assesses risks by evaluating regulatory certification, industry standards, and best practices. The score reflects the maturity of the app's suitability for enterprise use. It calculates a total score for each app by averaging weighted subscores across various risk categories that include considerations for reliability.

You have successfully reviewed several applications that are currently used at Contoso.

### Task 3: Block unsecure applications

Once you have successfully gained an overview of the use of applications in your environment, your first remediation action is to block unsafe applications.

1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud app catalog** (1).
1. Set the filter for **Risk score** to 0 - 4 (2).
1. Select **Bulk selection** (3) then select **All in page** (4).
1. Select **Tag as unsanctioned** (5).

   ![](../media/lab02/5.png)

You have successfully blocked vulnerable applications from being used by users.

### Task 4: Block unsecure applicatons automatically

In order to automatically block unsafe applications in the future, you will create a custom app discovery policy. This policy will tag unsafe applications as **Unsanctioned**. As you have integrated Defender for Endpoint with Defender for Cloud Apps, these applications will be blocked automatically.

1. In the Microsoft Defender portal, in the left navigation page expand **Cloud apps** and select **Cloud app catalog**.
1. On the **Cloud app catalog** page select **+ New policy from search**.

   ![](../media/lab02/6.png)

1. Enter the following information:
   - **Policy Name**: Tag unsafe apps as unsanctioned (1)
   - **Policy severity**: Medium (2)
   - **Description for users**: Applications with a risk score of 4 or lower will be unsanctioned and blocked automatically (3).
1. Under **Apps matching all of the following** add a filter and set it to **Risk score equals 0-4** (4).

    ![](../media/lab02/7.png)
1. Under **Alerts** select **Create an alert for each matching event with the policy's severity** (5) and set the value for **Daily alert limit per policy** to 5 (6).
1. Under **Governance actions** select **Tag app as unsanctioned** (7).
1. Select **Create** (8).

    ![](../media/lab02/8.png)

You have successfully created a policy to tag applications with a risk score of 5 or lower as unsanctioned.


### Review
In this lab, you have completed the following:
- Enabled Defender for Cloud.
- Enabled Azure Arc on the test server.
- Added Server to Defender for Cloud and gather Logs.
- Added regulatory compliance standard.


### You have successfully completed the lab.
