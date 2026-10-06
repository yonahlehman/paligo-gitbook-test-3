# Azure DevOps Custom Setup

{% hint style="info" %}
It is possible to add the Checkmarx One external IP addresses to the customer Firewall allowlist - For more information see [Managing Checkmarx One Traffic and AWS S3 Access](../managing-checkmarx-one-traffic-and-aws-s3-access.md)

Additionally, if the code repository is not internet accessible, it is possible to configure the code repository IP address instead of its hostname during the initial integration with the code repository - as it is not resolved via DNS.
{% endhint %}

## Overview

Checkmarx One supports Azure DevOps integration, enabling automated scanning of your Azure DevOps projects whenever the code is updated. Checkmarx One's Azure DevOps integration listens for Azure DevOps commit events and uses a webhook to trigger Checkmarx scans when a push, or a pull request occurs. Once a scan is completed, the results can be viewed in the Checkmarx One Platform.

Additionally, for pull requests, a comment is created in Azure DevOps, which includes a scan summary, list of vulnerabilities and a link to the scan results in Checkmarx One.

The integration is performed on a per-project basis, where a dedicated Checkmarx One Project corresponds to a specific Azure DevOps repository. You can select several repositories to create multiple integrations in a bulk action.

{% hint style="info" %}
This integration supports both public and private git based repos.
{% endhint %}

## Prerequisites

- The source code for your project is hosted on a Azure DevOps repo.

  {% hint style="warning" %}
  Checkmarx One does not support integration with Azure DevOps Server 2019. If you require integration, consider upgrading to a newer version of ADO.
  {% endhint %}
- You have a Checkmarx One account and have credentials to log in to your account.

  {% hint style="warning" %}
  Creating new import configurations or editing existing configurations requires `update-tenant-params` permission. Importing new Projects using an existing configuration requires `create-project` permission.

  Our best practice recommendation is to create a dedicated service user for the purpose of creating the integration. This will ensure that scans created via the integration will have a representative name.
  {% endhint %}
- The Azure DevOps user has admin privileges for this repo, see [Code Repository Integrations](README.md).
- Verify that in the Azure DevOps Organization settings under **Organization Settings → Policies → “Third-Party application access via OAuth”** is enabled - For additional assistance use the following link: [Azure DevOps connection and security policies](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/change-application-access-policies?view=azure-devops).

  For example:

  <figure><img src="../../../assets/6297288859.png" alt="" width="360"><figcaption></figcaption></figure>

<details>

<summary>Generate a PAT in Azure DevOps</summary>

To generate a PAT for the relevant organization in Azure DevOps, perform the following steps:

1. In your Azure DevOps account go to the organization for which you want to set up the integration.
2. Click on **your user > Security**.

   <figure><img src="../../../assets/Azure_SH_Security.png" alt="" width="288"><figcaption></figcaption></figure>
3. Click on **Personal Access Tokens > + New Token**.

   A panel will be opened on the right screen side.
4. Configure the following fields:

   - **Name** - Token name.
   - **Organization** - Select the current organization.

     {% hint style="info" %}
     Alternatively, you can configure the integration using **All accessible organizations**. This option is not recommended, as it grants broader access than required (violating least-privilege principles) and is scheduled for deprecation by Microsoft. To connect multiple organizations, we recommend creating a separate PAT for each organization and adding each organization individually.
     {% endhint %}
   - **Scopes** - Custom defined.

     - **Code** - Read, Status.
     - **Pull Request Thread** - Read & write.

       <figure><img src="../../../assets/Azure_SH_Config_Token.png" alt="" width="360"><figcaption></figcaption></figure>

       <figure><img src="../../../assets/Azure_SH_Config_Token2.png" alt="" width="360"><figcaption></figcaption></figure>
   - Click **Create**.
5. Copy the token.

   <figure><img src="../../../assets/Azure_SH_Copy_Token.png" alt="" width="288"><figcaption></figcaption></figure>

</details>

## Setting up the Integration and Initiating a Scan

This process involves first connecting to your repo by specifying the repo URL and your authentication credentials, and then selecting the repos to import and configuring the Project settings.

It is possible to configure multiple configurations for connecting to Azure Custom Setup code repositories, each using a different URL and/or different authentication credentials. Once the initial configuration is set up, for each subsequent import action you can choose either to use the existing configuration or to create a new one. You can also add additional organizations to an existing configuration.

**To create Azure DevOps Custom Setup code repository Projects:**

1. In the **Workspace** <img src="../../../assets/Workspace.png" alt="" data-size="line">, click on **New** > **New Project - Code Repository Integration**.

   <figure><img src="../../../assets/Image_022-75b98b0d.png" alt="" width="576"><figcaption></figcaption></figure>

   The **Import From** window opens.

   <figure><img src="../../../assets/Image_558.png" alt="" width="432"><figcaption></figcaption></figure>
2. Select **Custom Setup** > **Azure**.

   <figure><img src="../../../assets/azureimport.png" alt="" width="432"><figcaption></figcaption></figure>
3. Configure the connection to your code repository, as follows:

   - If you are setting up an import configuration for the first time, enter data for the following fields and then click **Save & Continue**.

     - **Instance Name** - Designate a name for this import configuration.
     - **URL** - Your Azure DevOps self-managed domain.

       For example: https://azure.example.com
     - **Organization** - Enter the Azure DevOps organization name. This value must be an exact match and is recommended to be copied directly from Azure DevOps.

       {% hint style="info" %}
       If you would like to add additional organizations to this configuration, you can do so by clicking **+Add Organization**, as described below.
       {% endhint %}
     - **Token** - Enter a Personal Access Token associated with the specified organization. Each Azure DevOps organization requires its own PAT. See [Generate a PAT in Azure DevOps](#generate-a-pat-in-azure-devops) for retrieving your Azure DevOps token.

       <figure><img src="../../../assets/azureA.png" alt="" width="432"><figcaption></figcaption></figure>
   - If you are adding Projects using an existing configuration, select the radio button next to the configuration that you would like to use, and then click **Next**.

     <figure><img src="../../../assets/azureB.png" alt="" width="432"><figcaption></figcaption></figure>
   - If you are adding a new configuration in addition to an existing configuration, click **+ Add Configuration**, then fill in the data for this configuration as described above, and then click **Save & Continue**.

     <figure><img src="../../../assets/azureC.png" alt="" width="432"><figcaption></figcaption></figure>

     {% hint style="info" %}
     If you would like to edit an existing configuration (e.g., change the URL, credentials or organization), go to **Global Settings** > **Code Repository**.
     {% endhint %}
4. Select the **Azure Organization or Group** (for the requested repository) and click **Select Organization**.

   You can use the search field to quickly locate a specific organization.

   You can also choose whether to enable the **Monitor New Repositories** feature by using the toggle next to "Automatically sync with new or transferred projects in the organization."

   For more information about this feature, see [Monitor New Repositories](monitor-new-repositories.md).

   <figure><img src="../../../assets/Image_124.png" alt="" width="432"><figcaption></figcaption></figure>

   If the required organization is not listed, click **+ Add Organization**, enter the **Organization name** (exact match) and a **Token** (PAT) scoped to that organization, then click **Save and Close**.

   <figure><img src="../../../assets/Image_1055.png" alt="" width="432"><figcaption></figcaption></figure>

   The **Add Organization** dialog opens. Fill in the **Organization** name (exact match) and the **Token (PAT)** for that organization.

   <figure><img src="../../../assets/Image_1086.png" alt="" width="288"><figcaption></figcaption></figure>
5. **Select Repositories** inside the Azure Import organization and click **Select Repositories**.

   If the organization contains active repositories, suggested repos will be presented and selected automatically. For additional information see [Suggested Repositories](suggested-repositories.md).

   {% hint style="info" %}
   - A separate Checkmarx One Project will be created for each repo that you import.
   - There can’t be more than one Checkmarx One Project per repo. Therefore, once a Project has been created for a repo, that repo is greyed out in the Import dialog.
   {% endhint %}

   <figure><img src="../../../assets/Image_125.png" alt="" width="432"><figcaption></figcaption></figure>

   {% hint style="info" %}
   You will be able to add additional repos from an organization that has been connected in a previous integration. However, the organization will only be saved once you complete the entire flow of connecting at least one repo from that organization.
   {% endhint %}
6. In the **Repositories Settings** step, you can optionally adjust the settings as follows:

   <figure><img src="../../../assets/Image_389.png" alt="" width="432"><figcaption></figcaption></figure>

   - If the project has multiple repositories, click **All Repositories Settings** to adjust the settings for all repositories, or select a specific repository, to adjust the settings for that repository.
   - Expand the **Permissions Settings** and adjust the following settings:

     - **Scan Trigger: Push, Pull request** - Automatically trigger a scan when a push event or pull request is done in your SCM. (Default: On)
     - **Pull Request Decoration** - Automatically send the scan results summary to the SCM. (Default: On)
     - **SCA Auto Pull Request** - Automatically send PRs to your SCM with recommended changes in the manifest file, in order to replace the vulnerable package versions. (Default: Off)
   - Expand the **Scanner Settings** and enable the toggle for each scanner you want to use (**SAST, SCA, IaC Security, Container Security, API Security, OSSF Scorecard, Secret Detection, AI Supply Chain Security**) for your repositories. At least 1 scanner must be selected for each repository.

     {% hint style="info" %}
     The scan and permission settings shown here depend on whether this is the first project connected from this organization:

     - **First connection to this organization** — all licensed scanners are enabled by default. The settings you choose here establish the organization-level defaults, with Allow Override enabled for each setting.
     - **Organization already connected** — The settings shown reflect the existing organization-level configuration. For each setting, Allow Override is enabled or disabled at the organization level:

       - **Enabled** - You can modify the setting for this project. Changes affect only this project and do not change the organization-level configuration.
       - **Disabled** - The setting is inherited from the organization-level configuration and cannot be modified for this project.

     See [Organization-Level Configuration for Code Repository Integrations](organization-level-configuration-for-code-repository-integrations.md) for details.
     {% endhint %}
   - **Protected Branches** (when a specific repository is selected): Specify the branches to be designated as "Protected Branches".

     {% hint style="info" %}
     Specifying a branch as a **Protected Branch** affects three main areas: scan triggering (for PR and push), policy violation detection, and Feedback App notifications.
     {% endhint %}

     You can also use a wildcard symbol "\*" to designate which branches are protected. The wildcard can be used before the string, after the string, or both. All branches that match the wildcard pattern will be treated as protected branches.

     {% hint style="info" %}
     **Examples**:

     - `*` → all branches
     - `release*` → branches that begin with "release"
     - `*release` → branches that end with "release"
     - `* release *` → branches that contain "release" anywhere in the name
     {% endhint %}

     - **Tags** - For each protected branch, you can optionally assign **Tags**. When a scan is triggered for this branch (e.g., push or pull request), these tags will automatically be applied to the scan.

       Tags can be key:value pairs or simple values. For example, `env:prod` or `security`.
   - **Add SSH key** (when a specific repository is selected).
   - **Assign Tags:** Add **Tags** to the Project. Tags can be added as a simple strings or as key:value pairs.
   - **Set Criticality Level:** Manually set the project's criticality level.
7. Click **Next.**
8. In the **Select Branches** screen you can decide whether to enable the "Scan the default Branch upon the creation of the project" feature.

   For each repository, select the protected branches you want to scan during project creation, and then click **Create Project**.

   <figure><img src="../../../assets/Image_127.png" alt="" width="360"><figcaption></figcaption></figure>
9. A **Project** is created for each repository and a **scan is initiated** for each project. All projects created in this flow are associated with the same **organization** entity in Checkmarx One. The new projects are displayed on the Projects page,

   <figure><img src="../../../assets/Image_074.png" alt="" width="576"><figcaption></figcaption></figure>

## Editing Project Settings

In order to update settings for an individual code repository project, see Code Repository Project Settings. To update scanner and permission settings for all projects in an organization at once, see [Code Repository Settings](../../user-guide/configuring-account-settings/global-account-settings/code-repository-settings.md).
