# GitHub Issues

GitHub Issues Service integration allows Checkmarx One users to automate the creation, modification, and closure of GitHub issues for specific vulnerabilities detected in a scan.

Checkmarx One aggregates matching vulnerabilities during the issues creation process. As a result, the number of issues opened in the GitHub service may not align with the number of detected vulnerabilities in Checkmarx One.

{% hint style="warning" %}
Only issue **owners** and GitHub users with **push access** permissions can edit existing issues, including updating and reopening them.
{% endhint %}

## Prerequisites

**GitHub Issues** is a lightweight issue-tracking system that is available in all GitHub repositories.

When you create a GitHub repository, GitHub Issues is enabled by default.

If GitHub Issues is not enabled for the relevant repo, use the below link as a reference to enable it:

[Disabling GitHub Issues](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/disabling-issues)

{% hint style="info" %}
GitHub Issues work only for GitHub repositories that have been previously imported.
{% endhint %}

## Limitations

| **Limitation** | **Notes** |
|---|---|
| Maximum bug tracking tickets created per scanner is 2,000. If a scanner identifies more than 2,000 results (that fit the trigger conditions) in a scan, then the excess results won't have tickets created for them. | |

## Creating a New Feedback App

To create a new GitHub Issues Feedback App:

1. In the main navigation, select **Integrations**<img src="../../../assets/Integrations.png" alt="" data-size="line"> **> Feedback Apps**.
2. In the Feedback Apps window, hover over the **Github Issues** tile and click on the **Configuration** icon <img src="../../../assets/configurationicon.png" alt="" data-size="line">

   <figure><img src="../../../assets/github1.png" alt="" width="360"><figcaption></figcaption></figure>

   **Settings & Trigger Conditions** panel is opened in the right screen side.

Alternatively you can create a new GitHub Issues Feedback App by performing the following steps:

1. In the Feedback Apps window, select the **Apps** tab and click on the **Create App** button.

   <figure><img src="../../../assets/Jira2.png" alt="" width="576"><figcaption></figcaption></figure>
2. In the right side panel, select **GitHub Issues** and click **Next**.

## General Settings

GitHub Issues **Settings & Trigger Conditions** panel contains basic details for the new Feedback App in addition to its trigger conditions.

Configure the following:

1. **General Settings**:

   - **Feedback App Name**
   - **Description**
   - **Associate Tags** - Assign tags to a Feedback App. Tags are very useful for filtering purposes
2. **Filters**:

   {% hint style="info" %}
   If you edit an existing Feedback App and remove a previously selected trigger condition, tickets that were created based on that trigger will be closed automatically.
   {% endhint %}

   - **Severity** - The severity level of a vulnerability that triggers the Feedback App.
   - **State** - To decrease the number of issues created in GitHub Issues, specify also the state/s that will trigger Feedback App notifications. Possible states are: Confirmed, Urgent, Proposed Not Exploitable (PNE) or To Verify.

     {% hint style="info" %}
     The states mentioned above are pre-configured for all Checkmarx One accounts. In addition, you can create custom states in your account. Once they are created, you can assign those custom states to results. Custom states are currently supported for SAST, SCA, IaC Security and Container Security. This feature is only available for accounts that have the New Access Management (Phase 1) activated. For more info see Custom States.
     {% endhint %}

     In conjunction with the severity, this makes the setting more precise.
   - **Scan Engines** - Select which scan engine results will be reflected through the Feedback App (By default, all the licensed scanners are enabled).

     If the SCA scanner is selected, there is an option to select the **Exploitable Path** checkbox so that only SCA vulnerabilities for which an Exploitable Path was identified will trigger a notification.

     {% hint style="info" %}
     For Container Security, notifications are sent on the image level rather than for individual vulnerabilities. As a result, the **Status** filter is ignored, and images that are **Muted** or **Snoozed** are automatically excluded. The **Severity** level is determined by the highest-severity vulnerability found in the image
     {% endhint %}
3. Click **Save**

   <figure><img src="../../../assets/GitHub_Issues_Settings_and_Trigger_Conditions.png" alt="" width="216"><figcaption></figcaption></figure>

The new Feedback App will appear in the **Apps** tab of the **Feedback Apps** page.

<figure><img src="../../../assets/feedback2.png" alt="" width="216"><figcaption></figcaption></figure>

Hovering over an existing Feedback App provides the options to **Edit** or **Delete** the Feedback App.

For example:

<figure><img src="../../../assets/feedbackfinal.png" alt="" width="576"><figcaption></figcaption></figure>
