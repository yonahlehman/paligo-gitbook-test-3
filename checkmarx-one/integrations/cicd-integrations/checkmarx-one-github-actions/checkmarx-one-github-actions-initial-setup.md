# Checkmarx One GitHub Actions Initial Setup

Before running Checkmarx One scans from a GitHub Action, you need to set up an authentication method for accessing your Checkmarx One environment, and configure a GitHub Secret that contains your authentication information.

Authentication is done using an OAuth Client. You need to have the **Client ID** and **Client Secret** for an OAuth Client in Checkmarx One, see [Creating an OAuth Client for Checkmarx One Integrations](../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).

{% hint style="info" %}
The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
{% endhint %}

**To configure a GitHub Secret for an OAuth 2 Client:**

1. In the GitHub console, open the repository for which you are setting up the Checkmarx One integration and click on the **Settings** tab.
2. In the left side navigation panel, click **Secrets and variables** > **Actions** and then click on **New repository secret**.

   ![](../../../../assets/Image_1178.png)
3. Enter a **Name** for the Client ID Secret in GitHub (e.g., CX_CLIENT_ID) and then in the **Value** field enter the name that you designated for the Client_ID in Checkmarx One.
4. Repeat the above step to create a GitHub Secret for the Checkmarx One Client Secret (e.g., CX_CLIENT_SECRET), using the **Value** that you copied from Checkmarx One.

   The two Secrets are shown in the Repository secrets section.

   ![](../../../../assets/Image_1179.png)
