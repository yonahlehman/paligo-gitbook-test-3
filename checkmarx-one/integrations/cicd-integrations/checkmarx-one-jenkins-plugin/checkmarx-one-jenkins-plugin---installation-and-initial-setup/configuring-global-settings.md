# Configuring Global Settings

The global settings are used as the default configuration for your Checkmarx projects. They can be overridden by specifying different settings for individual projects.

In order to configure the global settings you need to have the Client ID and Client Secret for an OAuth Client in Checkmarx One, see [Creating an OAuth Client for Checkmarx One Integrations](../../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).

{% hint style="info" %}
Configuring global settings is recommended best practice, although it isn’t required. Alternatively, it is possible to configure all of the settings within the build step for each project.
{% endhint %}

**To configure the global settings for Checkmarx One:**

1. In the main navigation, click **Manage Jenkins**. Then click **Configure System.**
2. Scroll down to the **Checkmarx** section.

   <figure><img src="../../../../../assets/5972886090.png" alt="" width="648"><figcaption></figcaption></figure>
3. Fill in the **Checkmarx server URL** with the appropriate URL for your environment.

   **Checkmarx One Server Base URLs**

   - US Environment - https://ast.checkmarx.net
   - US2 Environment - https://us.ast.checkmarx.net
   - EU Environment - https://eu.ast.checkmarx.net
   - EU2 Environment - https://eu-2.ast.checkmarx.net
   - DEU Environment - https://deu.ast.checkmarx.net
   - Australia & New Zealand – https://anz.ast.checkmarx.net
   - India - https://ind.ast.checkmarx.net
   - India 2 - https://ind-2.ast.checkmarx.net/
   - Singapore - https://sng.ast.checkmarx.net
   - UAE - https://mea.ast.checkmarx.net
   - Israel - https://gov-il.ast.checkmarx.net
4. If the authentication URL is different that the server URL, then leave the **Use Authentication URL** selected (default), and enter the appropriate authentication URL.

   {% hint style="info" %}
   For Checkmarx One cloud platform, leave the checkbox selected and enter the URL for your environment.
   {% endhint %}

   **Checkmarx One Authentication URLs**

   - US Environment - https://iam.checkmarx.net
   - US2 Environment - https://us.iam.checkmarx.net
   - EU Environment - https://eu.iam.checkmarx.net
   - EU2 Environment - https://eu-2.iam.checkmarx.net
   - DEU Environment - https://deu.iam.checkmarx.net
   - Australia & New Zealand – https://anz.iam.checkmarx.net
   - India - https://ind.iam.checkmarx.net
   - Singapore - https://sng.iam.checkmarx.net
   - UAE - https://mea.iam.checkmarx.net
   - Israel - https://gov-il.iam.checkmarx.net
5. For **Tenant Name**, enter the name of your Checkmarx One Tenant account.
6. For **Credentials**, click **Add** and select **Jenkins**.

   <figure><img src="../../../../../assets/5972918327.png" alt="" width="432"><figcaption></figcaption></figure>

   The **Add Credentials** window opens.
7. For**Domain**, select **Global credentials** (default).
8. For **Kind**, select **Checkmarx Client Id and Client Secret**.

   The **Add Credentials** window options are updated.

   <figure><img src="../../../../../assets/6013452345.png" alt="" width="648"><figcaption></figcaption></figure>
9. For **Scope** select **Global** (default).
10. In the **Client Id** and **Secret** fields, enter your Checkmarx One OAuth **Client ID** and **Secret**.

    {% hint style="info" %}
    If you need to create an OAuth client, see [Creating an OAuth Client for Checkmarx One Integrations](../../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).
    {% endhint %}
11. In the **ID** field, it is recommended to give a descriptive name to these credentials (e.g., AST_Credentials) in order to make it easy to identify in the future.
12. In the **Description** field, optionally add a description to help distinguish between similar credentials.
13. Click **Add**.
14. Back in the main screen, under **Credentials**, select from the dropdown list the ID of the credentials that you just configured.
15. Under **Checkmarx Installation**, verify that the Checkmarx One CLI installation that you previously configured is selected.
16. If you want to test your connection, optionally click **Test Connection**.
17. Click **Save** at the bottom of the screen.
18. In the **Additional Arguments** section you can specify any CLI arguments that you would like to apply to scans of this project. See documentation here.

    {% hint style="info" %}
    Make sure that all argument values are inside double quotes (not single quotes) when using pipeline scripts.
    {% endhint %}

    {% hint style="info" %}
    By default all scanners that you are authorized to run (licensed or open source) will run. To limit scans to one or more specific scanners, add the argument `--scan-types {scanner}` ,where `{scanner}` is one or more of the following scanners `sast`, `sca`, `iac-security`, `api-security`, `container-security`, or `scs`.
    {% endhint %}

## Setting up a Proxy Environment Variable (Optional)

**To set up an environment variable:**

1. In the main navigation, click on **Manage Jenkins**, then click **Configure Settings**.

   <figure><img src="../../../../../assets/6151831832.bmp" alt="" width="648"><figcaption></figcaption></figure>
2. Scroll down to the **Global Properties** section, select the **Environment variables** checkbox and then click **Add**.

   <figure><img src="../../../../../assets/6151831839.bmp" alt="" width="648"><figcaption></figcaption></figure>
3. In the **Name** field, enter **HTTP_PROXY**.

   {% hint style="info" %}
   If Jenkins is running on Linux, then the variable name must use capital letters.
   {% endhint %}
4. In the **Value** field, enter the proxy address, e.g., [http://proxyuser:proxypassword@localhost:3128](http://proxyuser:proxypassword@localhost:3128).

   <figure><img src="../../../../../assets/6151831845.bmp" alt="" width="648"><figcaption></figcaption></figure>
5. Click **Save** at the bottom of the screen.

   Once the environment variable "HTTP_PROXY" is defined in Jenkins, the plugin uses the proxy automatically.
