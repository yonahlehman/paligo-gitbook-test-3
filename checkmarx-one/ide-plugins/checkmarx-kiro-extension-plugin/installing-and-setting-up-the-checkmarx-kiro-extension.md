# Installing and Setting up the Checkmarx Kiro Extension

## Installing the Extension

The Kiro extension is available on the [Open VSX Registry](https://open-vsx.org/extension/checkmarx/ast-results). You can initiate the installation directly from within Kiro.

{% hint style="info" %}
Although there is no dedicated Checkmarx plugin for Kiro, the plugin for VS Code version 2.44.0 and above has been tested and is effective for use in Kiro.
{% endhint %}

{% hint style="warning" %}
The **Checkmarx** VS Code extension includes the Checkmarx One Assist feature as part of the Checkmarx One platform experience and should be used by Checkmarx One customers with a Checkmarx One Assist license. The **Checkmarx** and **Checkmarx Developer Assist** VS Code extensions are mutually exclusive. To use the Checkmarx extension, ensure that the Checkmarx Developer Assist extension is uninstalled before installation. If you are not a Checkmarx One customer and are trying to install the **Checkmarx Developer Assist** VS Code extension, see Initial Setup and Configuration.
{% endhint %}

**To install the extension:**

1. Open Kiro.
2. In the main menu, click on the **Extensions** icon.
3. Search for the **Checkmarx** extension, then click **Install** for that extension.

   {% hint style="info" %}
   Make sure to install version 2.44.0 or above, since older versions don't support Kiro.
   {% endhint %}

   <figure><img src="../../../assets/kiro1.png" alt="" width="648"><figcaption></figcaption></figure>

   The Checkmarx extension is installed, and the Checkmarx icon appears on the left-side navigation panel.

   <figure><img src="../../../assets/kiroicon.png" alt="" width="360"><figcaption></figcaption></figure>

## Setting up the Extension

After installing the plugin, in order to use the Checkmarx One tool you need to configure access to your Checkmarx One account, as described below.

{% hint style="info" %}
If you are only using the free KICS Auto Scanning tool and/or the SCA Realtime Scanning tool, then this setup procedure is not relevant. However, for SCA Realtime Scanning tool, if your environment doesn't have access to the internet, then you will need to configure a proxy server in the Settings, under **Checkmarx One: Additional Params**.
{% endhint %}

1. In the Kiro console, in the left-side panel, click the **Checkmarx** icon.

   The **Checkmarx One Authentication** sidebar opens.

   <figure><img src="../../../assets/kirosidebar.png" alt="" width="216"><figcaption></figcaption></figure>
2. In the **Checkmarx One Authentication** sidebar, connect to Checkmarx One either using an **API Key** or **login credentials**.

   - Login Credentials

     1. Select the **OAuth login** button.

        The OAuth Log in window opens.

        <figure><img src="../../../assets/OauthLogin.png" alt="" width="288"><figcaption></figcaption></figure>
     2. Enter the Base URL of your Checkmarx One environment and the name of your tenant account, then click **Log in**.

        {% hint style="info" %}
        Once you have submitted a base URL and tenant name, it is saved in cache and can be selected for future use (saves up to 10 accounts).
        {% endhint %}

        A confirmation dialog asks for permission to open an external website.
     3. Click on **Open** to proceed.

        {% hint style="info" %}
        If you would like to prevent this dialog from opening in the future, click on **Configure Trusted Domains** and then in the Command Pallete click on **Trust...**.
        {% endhint %}
     4. If you are logged in to your account, the system connects automatically. If you are not logged in, your account's login page opens in your browser. Enter your Username and Password, and then your One-Time Password (2FA) to log in.
   - API Key (see Generating an API Key)

     1. Select the **API Key login** button.

        The API Key Log in window opens.

        <figure><img src="../../../assets/ApiKeyLogin.png" alt="" width="288"><figcaption></figcaption></figure>
     2. Enter your Checkmarx One **API Key** and click **Log in**.
3. The **Checkmarx One Authentication** sidebar will now show that you are logged in.

   <figure><img src="../../../assets/kirologgedin.png" alt="" width="216"><figcaption></figcaption></figure>
4. A Checkmarx welcome page is displayed immediately after a successful login.
5. In the **Checkmarx One Results** sidebar, click on the more options icon in the top right and select **Settings**.

   <figure><img src="../../../assets/kirosettings.png" alt="" width="288"><figcaption></figcaption></figure>
6. In the **Additional Params** field, you can submit additional CLI params. This can be used to manually submit the base url and tenant name if there is a problem extracting them from the API Key. It can also be used to add global params such as `--debug` or `--proxy`. To learn more about CLI global params, see [Global Flags](../../cli-tool/checkmarx-one-cli-commands/global-flags.md).

   <figure><img src="../../../assets/kirosettings2.png" alt="" width="288"><figcaption></figcaption></figure>

### Configuring Checkmarx Developer Assist

1. Start the Checkmarx MCP server:

   1. Select the **Kiro** icon in the left-side navigation panel.
   2. Under **MCP servers**, click **Authenticate** for the Checkmarx MCP server.

      <figure><img src="../../../assets/Image_900.png" alt="" width="288"><figcaption></figcaption></figure>
   3. If prompted, allow Kiro to open the Checkmarx web application and complete the authentication process.
2. You can optionally adjust the Checkmarx Developer Assist Settings as follows:

   1. Add **Additional Params** to set up custom configuraitions, such as proxy servers or to run in debug mode.
   2. Enable/disable specific realtime scanners. By default, all scanners are enabled.
   3. For IaC realtime scanner you can change the container platform used, Docker (default) or Podman.
   4. The IDE’s built-in AI assistant is enabled by default, and the selected **AI Assistant** is ignored. To use a different AI Assistant:

      1. Disable **Prefer Native AI Assistant**.
      2. Select the **AI Assistant** to use for remediation. Options are **Copilot** (default) or **Claude**.
   5. **MCP Authentication** – Select the authentication method used by the Checkmarx MCP server.

      {% hint style="info" %}
      After changing the authentication method, click **Install MCP** to update the `mcp.json` configuration.
      {% endhint %}

      - **OAuth** (default) when the MCP server starts, a browser-based login session is initiated to authenticate with your Checkmarx One account.
      - **Token Based** uses the API key associated with your current Checkmarx One login and avoids browser authentication when starting the MCP server.

        {% hint style="warning" %}
        When this method is used, the API key is stored in the `mcp.json` file.
        {% endhint %}

#### Troubleshooting - Manually Configuring the Checkmarx MCP Server

The extension normally creates and configures the `mcp.json` file automatically. Manual configuration is only required if automatic configuration fails or if you prefer to create the MCP configuration yourself.

1. Select the **Kiro** icon in the left-side navigation panel.
2. Under **MCP servers**, click the **open mcp config** icon.
3. Configure the `mcp.json` file for the authentication method that you want to use:

   - **OAuth** (default) - Authenticates through your Checkmarx One account when the MCP server starts.

     ```
     {
       "mcpServers": {
         "Checkmarx": {
           "url": "<Checkmarx_one_base_url>/api/security-mcp/mcp/<tenant-name>"
         }
       }
     }
     ```
   - **Token Based** - Authenticates using a Checkmarx One API key stored in the mcp.json file. Browser authentication is not required when starting the MCP server.

     ```
     {
        "mcpServers":{
           "checkmarx":{
              "url":"<Checkmarx_one_base_url>/api/security-mcp/mcp",
              "headers":{
                 "cx-origin":"Kiro",
                 "Authorization":"<Checkmarx_one_API_key>"
              }
           }
        }
     }
     ```
4. For **OAuth** authentication method, you need to manually start the MCP server:

   1. Select the **Kiro** icon in the left-side navigation panel.
   2. Under **MCP servers**, click **Authenticate** next to the Checkmarx MCP server.
   3. When prompted, allow Kiro to open the Checkmarx web application and complete the authentication process.

      The Checkmarx MCP is now enabled.

### Configuring AI Security Champion

AI Security Champion can be used with the Checkmarx One tool as well as with the KICS Realtime Scanning tool. In order to use AI Security Champion you need to integrate the Kiro extension with your OpenAI account.

{% hint style="info" %}
If the [Global Settings](../../user-guide/configuring-account-settings/global-account-settings/plugins-settings.md) for your account have been configured to use Azure AI instead of OpenAI, then the credentials are submitted on the account level and it is not possible to submit credentials in your IDE for an alternative AI model.
{% endhint %}

**To set up the integration with your OpenAI account:**

1. Go to the **Checkmarx** extension **Settings** and select **Checkmarx AI Security Champion**.

   ![](../../../assets/kiro8.png)
2. In the **Model** field, select from the drop-down list the model of the GPT account that you are using.
3. In the **Key** field, enter the API key for your OpenAI account.

   {% hint style="info" %}
   Follow this [link](https://platform.openai.com/account/api-keys) to generate an API key.
   {% endhint %}

   The configuration is saved automatically.

## Configuring the KICS Realtime Scanning Tool (Optional)

This tool is activated automatically upon installation and no configuration is required.

{% hint style="info" %}
It is **not** necessary to configure the Checkmarx One Authentication settings in order to use the KICS Realtime Scanning feature.
{% endhint %}

If you would like to customize the scan settings, you can use the following procedure:

1. In the VS Code console, go to **Settings** > **Extensions** > **Checkmarx** > **Checkmarx KICS Auto Scanning**.

   <figure><img src="../../../assets/VSCodeSettings2.png" alt="" width="432"><figcaption></figcaption></figure>
2. By default the extension is configured to run a KICS scan whenever an infrastructure file of a [supported type](https://docs.kics.io/latest/platforms/) is opened or saved. If you would like to disable automatic scanning, deselect the **Activate KICS Auto Scanning** checkbox.

   {% hint style="info" %}
   In this case, you will still be able to trigger scans manually from the command palette.
   {% endhint %}
3. If you would like to customize the scan parameters, enter the desired flags in the **Additional Parameters** field. For a list of available options, see Scan Command Options.
